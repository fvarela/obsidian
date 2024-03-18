
## Managed vs External

There are Managed tables and External tables.
* Managed tables
	* Databricks handles both the data and the metadata of managed tables
	* If the table is dropped the data is lost
	* The user don't have to specify the location of the data.
	* Saved automatically on :
		* Metadata: Central Hive Metastore
		* Data: Saved on schema location. If it was not specified during the creation of the schema it will be: `dbfs:/user/hive/warehouse`
	* Good for datasets that:
		* Are going to be used only within Databricks
		* Are temporary
* External tables:
	* Databricks handles the metadata only
	* If the table is dropped the data is not deleted.
	* The user specify the external storage (Blob) where the data is located
	* Saved on:
		* Metadata: Central Hive Metastore
		* Data: Wherever you want.
	* Good for datasets that
		* Are persistent
		* Are used by other apps, not only Databricks.


### Managed Tables

If you don't specify the `SCHEMA` the managed table would be created on the `default`one.
* Create on the default schema:
```
CREATE TABLE race_results_sql
COMMENT "Contains Personal Helth Information"
AS
SELECT *
FROM demo.race_results_python
WHERE race_year = 2020;
```

- Create specifying the schema
```
CREATE SCHEMA db_x
USE db_x;
CREATE TABLE table1;
CREATE TABLE table2;
```

Create a managed table from a Dataframe:


```
# OPTIONAL (Specify the schema if you don't want to use the default one)
# spark.sql("CREATE SCHEMA IF NOT EXISTS db_x")
# spark.sql("USE db_x")

race_results_df.write.format("parquet").saveAsTable("race_results_python")

```


* Drop:

Deletes both the table and the metadata (everything).


### External Tables
Just use the `LOCATION` keyword
* Create
Same as managed table but specifying the path:

```
CREATE TABLE demo.race_results_ext_sql
( race_year INT,
race_name STRING,
race_date TIMESTAMP,
circuit_location STRING,
driver_name STRING,
driver_number INT,
driver_nationality STRING,
team STRING,
grid INT,
fastest_lap INT,
race_time STRING,
points FLOAT,
position INT,
created_date TIMESTAMP
)
USING PARQUET
LOCATION "/mnt/formula1dlfvv/presentation/race_results_ext_sql"
-- LOCATION "dbfs:/mnt/demo/..."
```

Then you can for instance add data with: 
```
INSERT INTO demo.race_results_ext_sql
SELECT * FROM demo.race_results_ext_py WHERE race_year = 2020;
```

If you then delete the table with drop:
`DROP TABLE demo.race_results_ext_sql;`

The data would not be affected! You would only delete the table metadata.
If then you call again the CREATE TABLE statement the table would be created and it will be already populated with the data, because the data is already there.






