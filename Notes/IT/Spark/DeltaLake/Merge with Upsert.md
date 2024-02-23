Merge one dataframe into other.
	Specify the join condicion
	Specify how to do the UPDATE when there is a MATCH
	Specify how to do the INSERT when there is no MATCH
This is really powerful and can only be done with Delta Lake.

* SQL:
```
%sql
MERGE INTO f1_demo.drivers_merge tgt
USING drivers_day1 upd
ON tgt.driverId = upd.driverId
WHEN MATCHED THEN
UPDATE SET tgt.dob = upd.dob,
          tgt.forename = upd.forename,
          tgt.surname = upd.surname,
          tgt.updateDate = current_timestamp
WHEN NOT MATCHED
THEN INSERT (driverId, dob, forename, surname, createdDate) VALUES (driverId, dob, forename, surname, current_timestamp)
```

* PySpark:

```
from pyspark.sql.functions import current_timestamp
from delta.tables import DeltaTable

deltaTable = DeltaTable.forPath(spark, "/mnt/formula1dlfvv/demo/drivers_merge")
deltaTable.alias("tgt").merge(
    drivers_day3_df.alias("upd"),
    "tgt.driverId = upd.driverId") \
  .whenMatchedUpdate(set = { "dob" : "upd.dob", "forename" : "upd.forename", "surname" : "upd.surname", "updateDate": "current_timestamp()" } ) \
  .whenNotMatchedInsert(values =
    {
      "driverId": "upd.driverId",
      "dob": "upd.dob",
      "forename" : "upd.forename",
      "surname" : "upd.surname",
      "createdDate": "current_timestamp()"
    }
  ) \
  .execute()

```