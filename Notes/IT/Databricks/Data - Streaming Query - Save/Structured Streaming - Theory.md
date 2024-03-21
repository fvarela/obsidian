
### Overview
Structured Streaming treats a live data stream as a table that is being continuously appended

Streaming Sources -> Structured Streaming -> Output sink

Structure Streaming works by incrementally reading and writing to tables. 
It uses almost the same methods available in regular spark


Basic recipe:
	1. Define a __readStream__ that connects to your streamed input source.
	2. Define the return type for the readStream
		1. Dataframe
			1. This is the default. Use if you want to handle the input data with pyspark
		2. Streamed TempView
			1. Use it if you want to use SQL
	3. Declare the __writeStream__ and declare checkpoint, output mode, location etc.


### Output Modes

In the writeStream is where you defined the output mode you want to use:
- Append
	- Only reads new data from the streaming source
	- Does not support aggregation (since aggregation need old data).
- Complete
	- For aggregations where the whole results table is recomputed on each trigger
- Update
	- Only reads from streaming source new or updated records.
	- Good for upsert operations

### Features

Guarantees
- Fault tolerance:
	In case of failure it starts where it left thanks to:
		Checkpoints + write ahead logs
- Exactly-once guarantee
	Multiple writes of the same data do not produce duplicates on the sink -> Idempotent sinks.

Limitations:
- Sorting
- Deduplication
	

### ReadStream

Read from a Stream input table:

- Output a DataFrame
```python
streamDF = spark.readStreamm
			.table("Input_Table")
```

- Output to a TempView:
You can also read from the stream input and save that in a temp view.
The temp view created this way is a streaming one. If you query it the query would be dynamic running permanently and showing the incremental updates.
You would define it like this in you readStream statement:
```python
spark.readStream
	.table("books)
	.creawteOrReplaceTempView("books_streaming_tmp_vw")
```

Now you can query it in real time with:
```sql
SELECT * FROM books_streaming_tmp_vw
```

### WriteStream

It writes the data to the destination

- If you were working with a dataFrame:
```python
streamDF.writeStream
	.trigger(processingTime="2 minutes")
	.outputMode("append")
	.option("checkpointLocation", "/path")
	.table("Output_Table")
```

- If you were working with a tempView
```python
spark.table("books_streaming_tmp_vw")
	.writeStream
	.trigger(processingTime='4 seconds')
	.outputMode("complete")
	.option("checkpointLocation", "dbfs:/mnt/demo/author_counts_checkpoint")
	.table("author_counts")
```

### Others

* Trigger interval:

Process every 5 minutes
`trigger(processingTime="5 minutes")`

Process all data in a single batch and stop
`.trigger(once=True)`

Process all data in multiple micro-batches and stop
`.trigger(availableNow=True)`



- Stop all active streams:
```python
for s in spark.streams.active:
	print("Stopping stream: " + s.id)
	s.stop()
	s.awaitTermination()
```


- Convert a static table into a streaming temp view:
```python
(spark.readStream
	.table("bronze")
	.createOrReplaceTempView("bronze_tmp"))
```


* Deleted data.
If old data was deleted from table and that data is read in Streaming it would break the execution because the readStream assumes that the input data only has append rows to it. Never deletion.
In order for the readStream to work you need to ignore the deleted rows:

```python
spark.readStream
	.option("ignoreDeletes",True)
	.table("my_table")
```