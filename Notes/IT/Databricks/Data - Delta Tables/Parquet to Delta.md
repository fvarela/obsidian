
Converto from a table
```
%sql
CONVERT TO DELTA f1_demo.drivers_convert_to_delta
```

Convert from a parquet file system
```
%sql
CONVERT TO DELTA parquet.`/mnt/formula1dlfvv/demo/drivers_convert_to_delta_new`
```
