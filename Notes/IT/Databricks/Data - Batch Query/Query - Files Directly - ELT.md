
1. Extract text files as raw strings (`text`, `json`, `tsv`, ...)
	- Useful for self describing format:
		- Json, parquet, etc
	- Not so good for csv, tsv, etc
```sql
--- Query one file:

SELECT * FROM json.`/path/to/file.json`

---Query multiple files with wildcard *:

SELECT * FROM json.`/path/to/some_files_*.json`

---Extract data as raw strings (from json, csv, text files, etc) with `text`:

SELECT * FROM; text.`/path/to/file.json*

---Extract data as raw bytes

SELECT * FROM binaryFile.`/path/to/file`
```

2. Register extracted data as Tables with CTAs (`CREATE TABLE AS...`)
```sql
CREATE TABLES table_name
AS SELECT * FROM file_format.`/path/to_file`
```
* CTA automatically infers the schema from the file
	* Only useful for files with well defined schema (parquet, json, etc)


3. Solution. CTAS with `USING` keyword.
	- Use `USING` keyword (this creates a external table).
	- The files are kept in their original format (No delta tables!)
	```sql
	CREATE TABLE table_name
	(col_name1 col_type1, ...)
	USING CSV
	OPTIONS (header = "true",
			delimiter = ";")
	LOCATION = path
	```
	- Problem: 
		Do not support file options

4. Solution. `CTAS` + `USING` and `TEMP VIEWS`
- Create a `TEMP VIEW` using the external data source
- On a different query `CREATE TABLE` using the previously created `TEMP VIEW`

```sql
CREATE TEMP VIEW temp_view_name (col_name1 col_type1, ...)
	USING data_source
	OPTIONS (key1 = vl1, key2 = val2, ...)

CREATE TABLE table_name
	AS SELECT * FROM temp_view_name*
```

