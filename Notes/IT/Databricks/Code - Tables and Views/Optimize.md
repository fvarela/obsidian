Optimize command:
`OPTIMIZE my_table`

Compacts small files into big ones.
Target file size is 1Gb


### Auto optimize (compaction)
Databricks also compacts small files during individual writes to a table

2 complementary features
	- Optimized writes: Attempts to write 128MB files
	- Auto compaction:
		- After the write completes, it checks if files can further be compacted
		- If yes, it runs and OPTIMIZE job towards a file size of 128MB (instead of 1Gb)

Auto compaction does not support z-ordering

Enabling Auto Optimize:

```sql
---New tables
CREATE TABLE myTable (id INT, name STRING)
TBLPROPERTIES
    (delta.autoOptimize.optimizeWrite = true,
     delta.autoOptimize.autoCompact = true)

---Existing table
ALTER TABLE myTable
SET TBLPROPERTIES
    (delta.autoOptimize.optimizeWrite = true,
     delta.autoOptimize.autoCompact = true)

---Spark sessions
spark.databricks.delta.optimizeWrite.enabled
spark.databricks.delta.autoCompact.enabled
```

Having many small files is not always a problem!
	It can lead to better data skipping, and help minimize rewrites during merges and deletes

Databricks can automatically tune the file size of Delta Tables, based on workloads operating on the table.
	For Frequent MERGE operations, Optimized Writes and Auto Compaction will generate data files smaller than 128 MB. This helps in reducing the duration of future MERGE operations.