Remember:
Streaming tables are ever appending data sources
Static tables contain data that may be changed or overwritten.

Problem:
Static tables break the requirement of ever-appendig source for Structured Streaming!


Features:
When joining a Streaming table and a Batch table:
- The latest version of the static table is retrieved
- The streaming table drives the JOIN
	- Add more records to the static table does not trigger the join
	- Only the new records of the streaming table will be used in the join

Streaming-static joins are not stateful
- Say you have some records in the streaming table with column `course=Math`. You join that Streaming table with a static table `Courses` where that course does not exist yet. 
- In that situation if you create the course math in the table `Courses` then all the existing math records in the Streaming table will never be joined. Only the new ones that are added from that moment will be joined.
- If you want to solve this you need to configure a batch job to join all the missing records


### Example
```python
from pyspark.sql import functions as F

def process_books_sales():
	#Streaming table
    orders_df = (spark.readStream.table("orders_silver")
                    .withColumn("book", F.explode("books"))
                )
    #Static (batch) table
    books_df = spark.read.table("current_books")
    query = (orders_df
                .join(books_df, 
	                orders_df.book.book_id == books_df.book_id, 
	                "inner")
                .writeStream
                .outputMode("append")
                .option("checkpointLocation", 
	                "dbfs:/mnt/demo_pro/checkpoints/books_sales")
                .trigger(availableNow=True)
                .table("books_sales")
            )
    query.awaitTermination()
process_books_sales()
```