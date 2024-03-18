In an incremental ingestion you have new data that should be append to an existing table.
Easiest way to achieve this is by writing in append mode:

```python
results_final_df.write.mode("append").partitionBy('race_id').format("parquet").saveAsTable("f1_processed.results")
```

**Problem!**: 
* If the notebook is rerun multiple time the same data would be appended over and over again.
* Without using Delta Lake there is no way in Spark to run an UPDATE or a MERGE. You only have INSERT or LOAD

**Solution 1 (Drop Partition)**:

* Use _partitions_ and make one for each bunch of data you receive. Splunk allows you to drop the whole partition: 

```sql
ALTER TABLE table_identifier DROP [ IF EXISTS ] partition_spec [PURGE]
```


You can put that statement in a loop to drop the partitions:

```python
for race_id_list in results_final_df.select("race_id").distinct().collect():

  spark.sql(f"ALTER TABLE f1_processed.results DROP IF EXISTS PARTITION (race_id = {race_id_list.race_id})")
```

* Note that ALTER TABLE is only available in SQL, not pyspark.
* The following code would check if the races_id received in the current bunch of data exist in the database. If they do it would drop them. Then you can append to the existing dataframe safely:

```python
for race_id_list in results_final_df.select("race_id").distinct().collect():
  if (spark._jsparkSession.catalog().tableExists("f1_processed.results")):
    spark.sql(f"ALTER TABLE f1_processed.results DROP IF EXISTS PARTITION (race_id = {race_id_list.race_id})")
  results_final_df.write.mode("append").partitionBy('race_id').format("parquet").saveAsTable("f1_processed.results")
```


**Solution 2 (Overwrite Data with insertInto). Slightly more efficient:**

* Set the partition overwrite mode to be dynamic
By doing this when doing a write.mode("overwrite") it will overwrite only partitions received on the dataframe, not the whole table.
```python
spark.conf.set("spark.sql.sources.partitionOverwriteMode", "dynamic")
```

* Arrange the columns of your dataframe so that the one used as partition id comes last:
```python
restults_final_df = results_final_df.select("result_id", "driver_id", "Constructor_id, "number", ...."race_id")
```

You can use this function to achieve that:
```python
def re_arrange_partition_column(input_df, partition_column):
  column_list = []
  for column_name in input_df.schema.names:
    if column_name != partition_column:
      column_list.append(column_name)
  column_list.append(partition_column)
  output_df = input_df.select(column_list)
  return output_df
```


* Check if the table exists, create it if not. If it exists overwrite:
```python
if (spark._jsparkSession.catalog().tableExists("f1_processed.results")):
	results_final_df.write.mode("overwrite")\
	.insertInto("f1_processed.results")
else:
	results_final_df.write.mode("overwrite")\
	.partitionBy('race_id').format("parquet")\
	.saveAsTable("f1_processed.results")
```

```python
def overwrite_partition(input_df, db_name, table_name, partition_column):
	output_df = re_arrange_partition_column(input_df, partition_column)
	spark.conf.set("spark.sql.sources.partitionOverwriteMode","dynamic")
	if (spark._jsparkSession.catalog().tableExists(f"{db_name}.{table_name}")):
		output_df.write.mode("overwrite").insertInto(f"{db_name}.{table_name}")
	else: 
		output_df.write.mode("overwrite")\ 
			.partitionBy(partition_column)\ 
			.format("parquet") \ 
			.saveAsTable(f"{db_name}.{table_name}")
```
* Very important note about insertInto

```python
output_df.write.mode("overwrite").insertInto(f"{db_name}.{table_name}")
``` 

In order for the following line to work the output_df should have the partition column in the last position!