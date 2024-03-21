
# Create

### From Scratch

Not necessary if you create it by writing to it some existing data.
This might be the best practice because you get to specify the schema. 

```sql
CREATE TABLE IF NOT EXISTS f1_demo.drivers_merge (
  driverId INT,
  dob DATE,
  forename STRING,
  surname STRING,
  createdDate DATE,
  updateDate DATE
)
USING DELTA;
```
### Using Delta Table Builder API (not common)

```python
from delta import DeltaTable

(DeltaTable.createOrReplace(spark)
	.tableName("dev.demo_db.flight_time_tbl")
	.addColumn("FL_DATE", "DATE")
	.execute()
	)
```

### From Dataframe

Exactly the same as writing to a parquet. Just specify the format as **delta** instead

* From DataFrame to Managed Delta Table

```python
results_df.write.format("delta") \
	.mode("overwrite")\
	.partitionBy("constructorId")\
	.saveAsTable("f1_demo.results_managed") 
```

 * From DataFrame to External Table
```python
results_df.write.format("delta")\
	.mode("overwrite")\
	.save("/mnt/formula1dlfvv/demo/results_external")
```




## Insert to Delta Table
```sql
CREATE TABLe employees
	(id INT, name STRING, salary DOUBLE);`
```

```sql
INSERT INTO employees
VALUES
	(1, "Adam", 3500.0),
	(2, "Sarah", 4020.5)
```

## Read from Delta Lake to DataFrame

Exactly the same as reading from parquet. Just specify the format as **delta** instead
```python
results_external_df = spark.read\
				.format("delta")\
				.load("/mnt/formula1dlfvv/demo/results_external")
```

