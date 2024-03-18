Merge allows you to add new data to a dataframe without dropping partitions etc.
Merge one dataframe into other.
	Specify the join condicion
	Specify how to do the UPDATE when there is a MATCH
	Specify how to do the INSERT when there is no MATCH
This is really powerful and can only be done with Delta Lake.

* SQL:
```sql
MERGE INTO f1_demo.drivers_merge tgt
USING drivers_day1 upd
ON tgt.driverId = upd.driverId
WHEN MATCHED THEN
UPDATE SET tgt.dob = upd.dob,
          tgt.forename = upd.forename,
          tgt.surname = upd.surname,
          tgt.updateDate = current_timestamp
WHEN NOT MATCHED
THEN INSERT (driverId, dob, forename, surname, createdDate) VALUES (driverId, dob, forename, surname, current_timestamp)
```

* PySpark:

```python
from pyspark.sql.functions import current_timestamp
from delta.tables import DeltaTable

deltaTable = DeltaTable.forPath(spark, "/mnt/formula1dlfvv/demo/drivers_merge")
deltaTable.alias("tgt")\
	.merge(
		drivers_day3_df.alias("upd"),
		"tgt.driverId = upd.driverId") \
	.whenMatchedUpdate(
	  set = { "dob" : "upd.dob", 
		  "forename" : "upd.forename", 
		  "surname" : "upd.surname", 
		  "updateDate": "current_timestamp()" 
			  } ) \
	.whenNotMatchedInsert(
	  values = { "driverId": "upd.driverId",
		  "dob": "upd.dob",
		  "forename" : "upd.forename",
		  "surname" : "upd.surname",
		  "createdDate": "current_timestamp()"
			} ) \
	.execute()
```
The following wrapper will in addition check if the table exists and create it if not:


```python
def merge_delta_data(input_df, db_name, table_name, folder_path, merge_condition, partition_column):
  spark.conf.set("spark.databricks.optimizer.dynamicPartitionPruning","true")
  from delta.tables import DeltaTable
  if (spark._jsparkSession.catalog().tableExists(f"{db_name}.{table_name}")):
    deltaTable = DeltaTable.forPath(spark, f"{folder_path}/{table_name}")
    deltaTable.alias("tgt")\
		.merge(
	        input_df.alias("src"),
	        merge_condition) \
		.whenMatchedUpdateAll()\
		.whenNotMatchedInsertAll()\
		.execute()
  else: 
	  input_df.write\
		  .mode("overwrite")\ 
		  .partitionBy(partition_column)\ 
		  .format("delta")\
		  .saveAsTable(f"{db_name}.{table_name}")
```

The `merge_condition` could be something like:


```python
merge_condition = "tgt.result_id = src.result_id AND tgt.race_id = src.race_id"
```

In this case `race_id` is the partition column, that is why the following configuration has to be set:


```python
spark.conf.set("spark.databricks.optimizer.dynamicPartitionPruning","true")
```

This allows Spark to filter using the partition id if that filter is provided and will make the filter better.

This could be a call to that function:
```python
merge_condition = "tgt.result_id = src.result_id AND tgt.race_id = src.race_id"

merge_delta_data(results_deduped_df, 'f1_processed', 'results', processed_folder_path, merge_condition, 'race_id')
```