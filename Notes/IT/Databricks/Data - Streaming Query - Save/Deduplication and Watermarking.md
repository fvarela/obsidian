```python
deduped_df = spark.readStream
	.table("bronze") 
	.filter("topic = 'orders'")
	.select(F.from_json(F.col("value").cast("string"), json_schema).alias("v"))
	.select("v.*")
	.withWatermark("order_timestamp", "30 seconds")
	.dropDuplicates(["order_id", "order_timestamp"])
```

`.withWatermark("order_timestamp", "30 seconds")` 
	This method call defines a watermark on the `order_timestamp` column. The watermark tells Spark to wait for up to 30 seconds for late data. If data arrives with a `order_timestamp` that is older than the current event time minus 30 seconds, it may be ignored in the context of certain operations like window aggregations and deduplication.

`.dropDuplicates(["order_id", "order_timestamp"])` 
	This method is used to remove duplicate data based on the `order_id` and `order_timestamp` columns. The watermark helps with this operation by giving Spark a frame of reference for how long to wait for late-arriving data before deciding what is considered a duplicate. Without a watermark, Spark would have to maintain state indefinitely and would not drop any state data, potentially leading to resource issues over time.

With the above query you know there is not going to be duplicates within the time period defined in the watermark but if you then want to insert into a table you should do an upsert to make sure no duplicates go there:

```python
def upsert_data(microBatchDF, batch):
    microBatchDF.createOrReplaceTempView("orders_microbatch")
    
    sql_query = """
    MERGE INTO orders_silver a
    USING orders_microbatch b
    ON a.order_id=b.order_id AND a.order_timestamp=b.order_timestamp
    WHEN NOT MATCHED THEN INSERT *
    """
    microBatchDF._sparkSession.sql(sql_query)

```


Then you would call the function like this:

```python
query = (deduped_df.writeStream
			.foreachBatch(upsert_data)
			.option("checkpointLocation", "dbfs:/mnt/demo_pro_checkpoints/silver"))
			.trigger(availableNow=True)
			.start()
query.awaitTermination()	
```
