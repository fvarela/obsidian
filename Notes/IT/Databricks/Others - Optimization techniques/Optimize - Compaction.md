
## Optimize (or auto compaction)

Delta Lake can improve the speed of read queries from a table by coalescing small files into large ones (1GB max file size). You trigger compaction by running the OPTIMIZE command.
The 1GB target can be modified with: `spark.databricks.delta.optimize.maxFileSize`

```sql
OPTIMIZE my_table
```

#### ZORDER BY

Optionally you can add a __ZORDER BY__ clausule:
When you perform an `OPTIMIZE` operation on a Delta table with Z-ordering on certain columns, Delta Lake rearranges the data in the table so that the values in the specified columns are grouped closely together on disk. This is particularly useful for queries that filter on those columns, as it can significantly reduce the number of files and the amount of data that needs to be read.

```sql
OPTIMIZE my_table ZORDER BY (column1, column2, ...)
```

#### Autotune
To minimize the need for manual tuning Databricks automatically tunes the file size of Delta tables based on the size of the table.

The autotune can work to make operation more efficient based on different things.
- workload. For instance it can try to reduce the duration of MERGE operations
	- The target file size will vary. (Could be 64Mb, etc)
- Based on table size:

Table size 10 GB -> Target file size 256MB -> Approximate number of files: 40
Table size 1 TB    -> Target file size 256MB -> Approximate number of files: 4096
...
Table size 100 TB    -> Target file size 1GB -> Approximate number of files: 114437

Autotune vs Auto Optimize
1. Auto Optimize:
    
    - Is triggered after each individual write operation.
    - Its primary function is bin-packing, which helps in mitigating the small file problem that can occur after incremental data loads, especially with streaming data.
    - The target file size for Auto Optimize bin-packing is usually around 128 MB, which is a balance between avoiding too many small files and not delaying the write pipeline too much.
2. Autotune:
    
    - Works by dynamically adjusting the target file size based on the table's size, not on each individual write but as a broader optimization strategy.
    - For smaller tables, smaller file sizes are chosen to keep the number of files manageable.
    - For larger tables, the file size is increased, up to 1 GB for tables larger than 10 TB, because managing a large number of even moderately sized files can be detrimental to performance.

When autotune adjusts the target file size based on the table size, it is considering the overall data size and structure. However, Auto Optimize is more about maintaining a manageable number of files post-write operations, ensuring that the data written is optimized quickly without a significant wait time for compaction to occur.

The seeming discrepancy arises because these optimizations occur at different points in the data lifecycle. After data is written, you want immediate optimization to prevent small file proliferation, which is what Auto Optimize achieves with its quick bin-packing. Autotune, on the other hand, is more about setting strategic file sizes for ongoing maintenance and larger-scale optimizations.

### Auto optimize

After an individual write, Delta checks if files can further be compacted, and run a quick OPTIMIZE job (with 128 MB files instead of 1GB) to further compact files.
Auto optimize only does the bin-packing of files. It does not perform z-ordering.
 

