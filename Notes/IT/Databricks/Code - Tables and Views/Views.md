First you need Tables, then you can create Views based on those tables.
Difference between Tables and Views:
	Tables 
		Store data
	Views 
		Are virtual tables that do not store data
		Think of them as "SAVED QUERIES" that do not store data themselves
	
3 choices of Views:
* Local Temp View
	* Dropped when session ends.
		* When does a Spark session end?
			* Opening a new notebook.
			* Detaching and reattaching to a cluster
			* Installing a python package
			* Restarting a cluster
	* They are not registered anywhere
	* Removed when the notebook is rebooted
* Global Temp View
	* Accessible between Spark sessions within the same Spark application
	* Registered under the **'global_temp'** database
	* Dropped when the cluster is restarted
		* As long as the cluster is running all notebooks running on that cluster can access the Global Temp Views
* Permanent View
	* Stored in the meta-store and thus visible across different Spark sessions and applications
	* Registered under any database of your choice.
	* Dropped only by `DROP VIEW`
	* Useful for more permanent data access patterns.
Temp view - Only accessible through the Spark session
Global Temp View - Accessible though the Spark application (cluster).


### Local Temp View
#### Create from DataFrame:
```
race_results_df.createOrReplaceTempView("v_race_results")
```

#### Create from Table:
```
CREATE OR REPLACE TEMP VIEW v_race_results
AS
SELECT *
  FROM demo.race_results_python
WHERE race_year = 2018;
```

#### Query Local Temp View
Just use the name of the table. Do not specify any database:
```
	%sql
	SELECT * 
	FROM v_race_results;
```

### Global Temp View

* Create from DataFrame
```
race_results_df.createOrReplaceGlobalTempView("gv_race_results")
```

* Create from Table
```
CREATE OR REPLACE GLOBAL TEMP VIEW gv_race_results
AS
SELECT *
  FROM demo.race_results_python
WHERE race_year = 2018;
```

* Query Global Temp View
Global temp views are registered under the database `global_temp`
```
%sql
SELECT * 
FROM global_temp.v_race_results;
```

See what Global Temp Views are available with:
`SHOW TABLES IN global_temp;`

### Permanent View
This are registered just like Tables. 
They persist until you drop them.

* See available permanent views with:

`SHOW VIEWS;`

* Create a Permanent View

```
CREATE OR REPLACE VIEW demo.pv_race_results
AS
SELECT *
  FROM demo.race_results_python
WHERE race_year = 2000;
```

- Drop a permanent view:
`DROP VIEW`

