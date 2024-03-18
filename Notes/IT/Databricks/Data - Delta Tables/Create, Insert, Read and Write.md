
## Create Delta Lake from scratch
Not necessary if you create it by writing to it some existing data

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
## Write from DataFrame to Delta Lake

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

## Read from Delta Lake to DataFrame

Exactly the same as reading from parquet. Just specify the format as **delta** instead
```python
results_external_df = spark.read\
				.format("delta")\
				.load("/mnt/formula1dlfvv/demo/results_external")
```
