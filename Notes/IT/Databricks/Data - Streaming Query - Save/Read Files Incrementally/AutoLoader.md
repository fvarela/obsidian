
- Uses Structure Streaming
- Recommended by Databricks.
- Can process billions of files
- Store metadata of the discovered files
- Exactly-once guarantees
- Fault tolerance

It uses the Structured Streaming __readStream__ but has a specific format __cloudFiles__

```python
spark.readStream
		.format("cloudFiles")
		.option("cloudFiles.format","parquet")
		.option("cloudFiles.schemaLocation","dbfs:/mnt/demo/orders_checkpoint")
		.load('/orders-raw')

	.writeStream
		.option("checkpointLocation","dbfs:/mnt/demo/orders_checkpoint")
		.option("mergeSchema","true")
		.table("orders_updates")

	.createOrReplaceTempView("orders_raw_temp")

```

