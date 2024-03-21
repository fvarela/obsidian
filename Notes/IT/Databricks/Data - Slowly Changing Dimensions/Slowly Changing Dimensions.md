

| SCD Type | Summary                                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------------- |
| Type 0   | No changes allowed                                                                                                         |
| Type 1   | Overwrite the changes. No history.                                                                                         |
| Type 2   | New records are added as new rows. Old records are kept for history                                                        |
| Type 3   | Update the values in the same row. In addition to the current value, one or more columns are used to store previous values |
| Type 4   | Instead of using columns like in Type 3, a separate history table is used.                                                 |

This is an implementation of a type 2 SCD (Saves the history of previous records and flags them as no longer active along with two other columns, start date and end date that shows the period when the entries were (or are) valid)

```sql
---Specifies the target table for the upsert.
MERGE INTO books_silver

---Specifies the source table for the upsert, referred to as staged_updates in the merge condition.
USING (
    ---Selects all rows from the updates table and includes their book_id as merge_key.
    
    SELECT updates.book_id as merge_key, updates.*
    FROM updates
    
    UNION ALL
    
    ---Selects rows where the current price in books_silver is different from updates. The merge_key is set to NULL for these rows so they are treated as new insertions in the WHEN NOT MATCHED clause.
    
    SELECT NULL as merge_key, updates.*
    FROM updates
    ---Inner JOIN. Retrieves records that are present in both tables.
    
    JOIN books_silver ON updates.book_id = books_silver.book_id
    WHERE books_silver.current = TRUE AND updates.price <> books_silver.price
) staged_updates
ON books_silver.book_id = merge_key

---When the book_id matches and the current book price is different in the books_silver table, it updates the current flag to false and sets the end_date to the updated timestamp from staged_updates.

WHEN MATCHED 
    AND books_silver.current = true 
    AND books_silver.price <> staged_updates.price 
THEN
    UPDATE SET current = false, end_date = staged_updates.updated

---When there is no match found (which will be the case for rows with a NULL merge_key), it inserts the record from staged_updates into the books_silver table.

WHEN NOT MATCHED 
THEN
    INSERT (book_id, title, author, price, current, effective_date, end_date)
    VALUES (staged_updates.book_id, staged_updates.title, staged_updates.author, staged_updates.price, true, staged_updates.updated, NULL)

```

In Structured streaming you would use the query above in forEach batch in the following way:

```python
def type2_upsert(microBatchDF, batch):
    microBatchDF.createOrReplaceTempView("updates")

    sql_query = """
    MERGE INTO books_silver
    USING (
        SELECT updates.book_id as merge_key, updates.*
        FROM updates

        UNION ALL

        SELECT NULL as merge_key, updates.*
        FROM updates
        JOIN books_silver ON updates.book_id = books_silver.book_id
        WHERE books_silver.current = true AND updates.price > books_silver.price
    ) staged_updates
    ON books_silver.book_id = merge_key
    WHEN MATCHED 
        AND books_silver.current = true 
        AND books_silver.price <> staged_updates.price 
    THEN
        UPDATE SET current = false, end_date = staged_updates.updated
    WHEN NOT MATCHED THEN
        INSERT (book_id, title, author, price, current, effective_date, end_date)
        VALUES (staged_updates.book_id, staged_updates.title, staged_updates.author, staged_updates.price, true, staged_updates.updated, NULL)
    """

    microBatchDF.sparkSession.sql(sql_query)
```



### Example. Deduplication


A read stream to process the changes in the table __bronze__
__bronze__ has Change Data Feed available
where you use each received batch to upsert entries on another table. For that you apply the function __foreachBatch__


```python
query = (spark.readStream
            .table("bronze")
            .filter("topic = 'customers'")
            .select(F.from_json(F.col("value").cast("string"), schema).alias("v"))
            .select("v.*")
            .join(F.broadcast(df_country_lookup), F.col("country_code") == F.col("code"), "inner")
            .writeStream
            .foreachBatch(my_batch_upsert)
            .option("checkpointLocation", "dbfs:/mnt/demo_pro/checkpoints/customers_silver")
            .trigger(availableNow=True)
            .start()
)

query.awaitTermination()
```

__my_batch_upsert___ gets the microBatchDF

```python
from pyspark.sql.window import Window

def my_batch_upsert(microBatchDF, batchId):
	#The partitionBy in the Window function acts like a GROUP BY in sql.
    window = Window.partitionBy("customer_id").orderBy(F.col("row_time").desc())
    #This gets only the entries with rank = 1. It dropes the column 'rank' since 
    #it is no longer needed.
    (microBatchDF.filter(F.col("row_status").isin("insert", "update"))
                 .withColumn("rank", F.rank().over(window))
                 .filter("rank == 1")
                 .drop("rank")
                 .createOrReplaceTempView("ranked_updates"))

	query = """
		MERGE INTO customers_silver c
		USING ranked_updates r
		ON c.customer_id=r.customer_id
		WHEN MATCHED AND c.row_time < r.row_time
		    THEN UPDATE SET *
		WHEN NOT MATCHED
		    THEN INSERT *
	"""

	microBatchDF.sparkSession.sql(query)
```

`broadcast` is an optimization technique where the small dataframe will be sent to all the executors in the cluster.