Compact small files into larger files

```sql
OPTIMIZE my_table
```

Optionally you can add a ZORDER BY clausule:
When you perform an `OPTIMIZE` operation on a Delta table with Z-ordering on certain columns, Delta Lake rearranges the data in the table so that the values in the specified columns are grouped together. This is particularly useful for queries that filter on those columns, as it can significantly reduce the number of files and the amount of data that needs to be read.

```sql
OPTIMIZE my_table ZORDER BY (column1, column2, ...)
```
