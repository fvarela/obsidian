
```python
spark.read
	.table("bronze")
	.dropDuplicates(["order_id", "order_timestamp"])
```


With spark.readStream it would work the same:

```python
deduped_df = (spark.readStream
				 .table("bronze"
				 .filter("topic = 'orders'")
				 .select(F.from_json(F.col("value").cast("string"), json_schema).alias("v"))
				 .select("v.*")
				 .withWatermark("order_timestamp", "30 seconds")
				 .dropDuplicates(["order_id", "order_timestamp"]))
```