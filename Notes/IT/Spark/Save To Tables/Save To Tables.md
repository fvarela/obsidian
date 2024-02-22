### Table from dataframe - PySpark:

* Managed table
	```
	circuits_final_df.write.mode("overwrite")\
		.format("parquet)\
		.saveAsTable("f1_processed.circuits")
	```

* External table:
```
	circuits_final_df.write\
		.mode("overwrite")\
		.format("parquet)\
		.save("/mnt/formula1dlfvv/demo/results_external")
```

### Table from csv - SQL:
**External table. From one csv**

```
DROP TABLE IF EXISTS f1_raw.circuits;
CREATE TABLE IF NOT EXISTS f1_raw.circuits(
circuitId INT,
circuitRef STRING,
name STRING,
location STRING,
country STRING,
lat DOUBLE,
lng DOUBLE,
alt INT,
url STRING)
USING csv
OPTIONS (path "/mnt/formula1dlfvv/raw/circuits.csv", header true)
```

**External table. From a list of csv (path is a folder**)
```
DROP TABLE IF EXISTS f1_raw.lap_times;
CREATE TABLE IF NOT EXISTS f1_raw.lap_times(
raceId INT,
driverId INT,
lap INT,
position INT,
time STRING,
milliseconds INT
)
USING csv
OPTIONS (path "/mnt/formula1dlfvv/raw/lap_times")
```


### Table from json - SQL:
**External table. From nested json**:
```
DROP TABLE IF EXISTS f1_raw.drivers;
CREATE TABLE IF NOT EXISTS f1_raw.drivers(
  driverId INT,
  driverRef STRING,
  number INT,
  code STRING,
  name STRUCT<forename: STRING, surname STRING>,
  dob DATE,
  nationality STRING,
  url STRING)
  USING json
  OPTIONS (path "/mnt/formula1dlfvv/raw/drivers.json")
)
```

**External table. From Multiline Json**
```
DROP TABLE IF EXISTS f1_raw.pit_stops;
CREATE TABLE IF NOT EXISTS f1_raw.pit_stops(
driverId INT,
duration STRING,
lap INT,
milliseconds INT,
raceId INT,
stop INT,
time STRING)
USING json
OPTIONS(path "/mnt/formula1dlfvv/raw/pit_stops.json", multiLine true)
```


