

* Parquet folder:
`df = spark.read.parquet("/mnt/formula1dlfvv/processed/circuits")`

* Parquet file:
If you want to filter inside the parquet to get only the data coming from one file use the .filter:

```python
results_df = spark.read.parquet(f"{processed_folder_path}/results") \
.filter(f"file_date = '{v_file_date}'") \
.withColumnRenamed("time", "race_time")
```
