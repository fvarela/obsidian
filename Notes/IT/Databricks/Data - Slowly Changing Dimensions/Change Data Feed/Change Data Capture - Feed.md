CDC - Process of identifying changes (insert, update, delete) made to data in the source and delivering those changes to the target.

Use Case
	Use CDC - CDF:
		When Table changes include updates and/or deletes
		Small fraction of records updated in each batch (from CDC feed)
	Do not use CDC - CDF:
		When table's changes are append-only
		Most records in the table updated in each batch
Limitation:
- Cannot be performed if multiple source rows matched and attempted to modify the same target row in the Delta table
- CDC feed with multiple updates for the same key will generate an exception
Solution:
	Merge only the most recent changes!
	Use the Rank window function (ranking by date). Just write the first one.

What happens when you enable CDC - CDF on a Delta Lake table in Spark?
+ Spark adds the following columns to your table:
	- __\_change_type__
		- insert. Indicate that the row has been added
		- update_preimage. The state of the row before it was updated
		- update_postimage. The state of the row after it was updated
		- delete. Indicates that the row has been removed from the table.
	- __\_commit_version__
	- __\_commit_timestamp__
+ Spark creates a folder __\_change_data/__ on the same location where the delta table is.
+ You can start using the delta lake method __table_changes__ to query the changes

### Enabling CDF
CDF is not enable by default. 

You can enable it using one of the following methods:

- For a new table:
```sql
CREATE TABLE myTable (id INT, name STRING)
TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

- For an existing table:
```sql
ALTER TABLE myTable
SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

- For all tables:
```python
spark.databricks.delta.properties.defaults.enableChangeDataFeed
```

### Using table_changes

When CDC - CDF is enabled you can use the __table_changes__ method to query the specific changes (inserts, updates, deletes):


```sql
--- Using version
SELECT * 
FROM table_changes('table_name', start_version, [end_version])

--- Using timestamps
SELECT * 
FROM table_changes('table_name', start_timestamp, [end_timestamp])
```

Using pyspark you can do like this:
```python
cdf_df = (spark.readStream
			 .format("delta")
			 .option("readChangeData", True)
			 .option("startingVersion", 2)
			 .table("customers_silver"))

display(cdf_df)
```


* Reading the CDF data:
Reading all the changes from table customers_silver since version 2:
```sql
SELECT *
FROM table_changes("customers_silver", 2)
```


### Example. Implementing CDC-CDF in Databricks with Structured Streaming

See Data - Streaming Query - Save / Stream - Stream JOINS
### Handle CDF deletes and populate the changes downstream:

First you would read the changes as you did before:
```python
deleteDF = (spark.readStream
			   .format("delta")
			   .option("readchangeFeed", "true")
			   .option("startingVersion", 2)
			   .table("customers_silver"))
```

Now you declare the function that would run for each batch

```python
def process_deletes(microBatchDF, batchId):
    (microBatchDF
        .filter("_change_type = 'delete'")
        .createOrReplaceTempView("deletes"))
        
	#Here we commit deletes to other tables
    microBatchDF._jdf.sparkSession().sql("""
        DELETE FROM customers_orders
        WHERE customer_id IN (SELECT customer_id FROM deletes)
    """)
	#Then we perform an update back to the deletes table to change the status of the request to deleted.
    microBatchDF._jdf.sparkSession().sql("""
        MERGE INTO delete_requests r
        USING deletes d
        ON d.customer_id = r.customer_id
        WHEN MATCHED
        THEN UPDATE SET status = 'deleted'
    """)
```

And then you run the writeStream with your desired trigger:
```python
(deleteDf.writeStream
	.foreachBatch(process_deletes)
	.option("checkpointLocation", "dbfs:/mnt/demo_pro/checkpoints/deletes")
	.trigger(availableNow=True)
	.start())
```

Then the deleted records will be still in the table, you need to commit the changes by running the `VACUUM` command