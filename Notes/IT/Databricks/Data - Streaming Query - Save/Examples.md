
* Read in streaming from a delta table and create a temp view to handle the stream
```python
spark.readStream
	.table("books)
	.creawteOrReplaceTempView("books_streaming_tmp_vw")
```

- Now you can query that data using the temp view:
```sql
SELECT * FROM books_streaming_tmp_vw
```
Note that the query would run indefinitely since it was created with a Stream

* Save the temp view back to a dataframe:
```python
spark.table("books_streaming_tmp_vw")
	.writeStream
	.trigger(processingTime='4 seconds')
	.outputMode("complete")
	.option("checkpointLocation", "dbfs:/mnt/demo/author_counts_checkpoint")
	.table("author_counts")
```
When using aggregation always select outputMode: complete to overwrite the table with the new calculation

```python
spark.table("books_streaming_tmp_vw")
	.writeStream
	.trigger(availableNow=True)
	.outputMode("complete")
	.option("checkpointLocation", "dbfs:/mnt/demo/author_counts_checkpoint")
	.table("author_counts")
	.awaitTermination()
```

`.trigger(availableNow=True)`
	Runs microbatches until all the available data at the time the job started has been processed. 
	Treats available data as a batch immediately rather than waiting for a trigger
	This is specific of Databricks (it is not on standard Spark)
	Other trigger options:
		- `.trigger(Trigger.ProcessingTime("10 minutes"))`
			- Every 10 minutes
		- `.trigger(Trigger.Never())`
			- It will not automatically trigger any processing
			- It sill only process data if explicity call the `processAllAvailable()`
		- `.trigger(Trigger.Continuous("interval"))`
			- It will run in continuous mode with a checkpoint at the specified interval
`.trigger(Trigger.Once())`
	Similar to the `.trigger(availableNow=True)` but it runs one microbatch and finish. Regardless if all the available data were processed.
`outputMode("complete")` 
	The entire table is updated and outputted every time there are updates.
`awaitTermination()` 
	Blocks the execution of other cells until the process ends.
`.option("checkpointLocation", "dbfs://...")` 
	Important for fault tolerance and state management.


Another example: 
```python
def process_bronze():
    schema = "key BINARY, value BINARY, topic STRING, partition LONG, offset LONG, timestamp LONG"

    query = (spark.readStream 
                 .format("cloudFiles")
                 .option("cloudFiles.format", "json")
                 .schema(schema)
                 .load(f"{dataset_bookstore}/kafka-raw")
                 .withColumn("timestamp", (F.col("timestamp")/1000).cast("timestamp"))
                 .withColumn("year_month", F.date_format("timestamp", "yyyy-MM"))
             .writeStream
                 .option("checkpointLocation", "dbfs:/mnt/demo_pro/checkpoints/bronze")
                 .option("mergeSchema", True)
                 .partitionBy("topic", "year_month")
                 .trigger(availableNow=True)
                 .table("bronze"))

    query.awaitTermination()
```

`spark.readStream` 
	Initializes a streaming dataframe. Continuously monitors a directory and processes files as they arrive.
`.format("cloudFiles")` 
	Specifies that the source format of the files is `cloudFiles`. Features:
		- Uses cloud storage notifications. It does not have to list all the directories all the time
		- Can handle changes in the schema. (json cannot).
	The alternative would be `format("json")` It would be more basic
		- It would rely on the file modification time to find new files
		- Once picked up by the stream the files should not be modified.
`.option("cloudFiles.format", "json")` 
	The format of the actual data is json.
`option("mergeSchema",True)` 
	Allows the schema of the DataFrame to be updated as new data is ingested.

