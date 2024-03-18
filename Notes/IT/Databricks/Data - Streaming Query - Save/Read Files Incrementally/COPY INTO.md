
- Files that have been already loaded are skipped
- Not the recommended option from Databricks
- Good for thousands of files
- Less efficient at scale than the alternative (Autloader)

```sql
COPY INTO my_table
FROM '/path/to/files'
FILEFORMAT=CSV
FORMAT_OPTIONS ('delimeter'='|',
				'header'='true')
COPY_OPTIONS ('mergeSchema'='true');
```
