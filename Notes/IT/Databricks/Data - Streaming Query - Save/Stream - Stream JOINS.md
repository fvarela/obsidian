When joining two Streaming datasets, the execution of the query is triggered by the arrival of new data in either of the input streams.

### State Storage in Stream-Stream Joins

- **What is Stored**: For each stream involved in a join, Spark maintains a "state" that consists of records that may be needed for future join operations. 
- **Purpose**: The state allows Spark to match incoming records from one stream with relevant records from the other stream, even if those records do not arrive at the same time. 

### Watermarks and State Expiry

- **Watermarking**: To manage the size of the state and ensure that the system can operate within finite memory constraints, Spark uses a concept called "watermarks". A watermark is a threshold that defines how old data can be before it is considered too late to be included in the join. It's essentially a way to define "lateness" for data.
- **Matched Records**: The match itself does not automatically remove the customer record from the state of `cdf_customers_df`. Instead, what happens to the state after a match depends on how the watermarking and state expiration policies are configured.
- **State Retention**: The state for `cdf_customers_df` will continue to retain customer records until they exceed the age defined by the watermark. This is independent of whether a match has occurred. The purpose of maintaining state is to allow future records that arrive within the watermark's time bounds to be joined.

### Implications for Join Operations

- **Potential for Missed Joins**: If a record from one stream has no matching record in the other stream within the time frame allowed by the watermark, it will eventually be removed from the state. This means that if a matching record arrives after the watermark threshold has passed, the join will not occur because the original record is no longer in the state.
- **Managing Watermarks**: The key to effective state management and join operations is to set appropriate watermarks based on the expected characteristics of your data streams, such as latency and out-of-orderness. Watermarks that are too aggressive may lead to missed joins (due to premature state expiration), while watermarks that are too lenient may cause excessive state growth and resource consumption.

### Example

Two streamed tables:
	cdf_customers_df
		Has cdc enabled.
	orders_df
		Regular streamed data source.
One output table:
	__customers_orders__
Every batch from __orders_df__  is inner joined with the __cdf_customers_df__ and the function __mybatch_upsert__ is applied to them:
	It applies a window function to get latest update only for each.	Does an upsert for the joined orders_df and cdf_customers_df entry on the output table __customers_oders__
	

```python
from pyspark.sql import functions as F
from pyspark.sql.window import Window


def my_batch_upsert(microBatchDF, batchId):
	window = Window.partitionBy("order_id", "customer_id")
					.orderBy(F.col("_commit_timestamp").desc())
    (microBatchDF
		 .filter(F.col("_change_type").isin(["insert", "update_postimage"]))
		 .withColumn("rank", F.rank().over(window))
		 .filter("rank == 1")
		 .drop("rank", "_change_type", "_commit_version")
		 .withColumnRenamed("_commit_timestamp", "processed_timestamp")
		 .createOrReplaceTempView("ranked_updates"))

	query = """
	MERGE INTO customers_orders c
	USING ranked_updates r
	ON c.order_id=r.order_id AND c.customer_id=r.customer_id
	WHEN MATCHED AND c.processed_timestamp < r.processed_timestamp
	    THEN UPDATE SET *
	WHEN NOT MATCHED
	    THEN INSERT *
	"""
	
	microBatchDF.sparkSession.sql(query)

def process_customers_orders():
    orders_df = spark.readStream.table("orders_silver")
    cdf_customers_df = (spark.readStream
                        .option("readChangeData", True)
                        .option("startingVersion", 2)
                        .table("customers_silver")
                        )
    query = (orders_df
             .join(cdf_customers_df, ["customer_id"], "inner")
             .writeStream
             .foreachBatch(my_batch_upsert)
			 .option("checkpointLocation", 
					 "dbfs:/mnt/demo_pro/checkpoints/customers_orders")
             .trigger(availableNow=True)
             .start()
    )
    query.awaitTermination()
process_customers_orders()


```


- **State Storage**: 
For each stream involved in the join, Spark maintains a state that includes records from past triggers that haven't been matched and cleared yet. This state is what enables Spark to perform joins between datasets across different micro-batches.

- **Handling of Unchanged Data**: 
If new data arrives in `orders_df` and there are no new changes in `cdf_customers_df`, the join operation doesn't result in an empty `cdf_customers_df`. Instead, Spark uses the state information it has maintained for `cdf_customers_df` to perform the join. This means it will use the existing records from `cdf_customers_df` that are stored in state to match with the new `orders_df` data.

- **CDC and Empty Batches**: 
When reading `cdf_customers_df` with CDC enabled, if there are no new changes, it doesn't mean `cdf_customers_df` is empty. Instead, it simply means there are no new changes to process. The state from the previous micro-batches (which includes the customer data that was relevant at that time) is still used for joining with new `orders_df` batches.


Why not running a stream (__orders_df__) - static (__customers_df__) join?

- **Triggering**: 
In this setup, the query is only triggered by new data in the stream (`orders_df`). The static dataset (`customers_df`) does not trigger the query because it is not treated as a stream.

- **Use Cases**
This is beneficial when you have a relatively stable dataset that doesn't change often or when the performance considerations of reloading a large static dataset are manageable.