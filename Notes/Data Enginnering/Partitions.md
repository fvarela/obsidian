Choose a good partition:
- Choose a low cardinality field
- Partitions should be at least 1Gb in size
- If records with a given value will continue to arrive indefinitely that could help you define your partition better, for instance Datetime fields can be used for patitioning.

If partition by year you can the partition boundaries to Delete/Archive old data easily
```sql
DELETE FROM my_table
WHERE year<2023
```

The actual deletion will not occur until you run the `VACUUM` 
Be careful if you delete data not to break readStream executions! Make sure you have the following option enabled so that you don't break the execution:

```python
spark.readStream
	.option("ignoreDeletes", True)
	.table("my_table")
```
 