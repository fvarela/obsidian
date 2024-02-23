Delta Tables have be default a 'version control'. It works similar to git

#### See version log (similar to git log)
`%sql DESC HISTORY f1_demo.drivers_merge`

#### Checkout a previous 'commit'
* Using Timestamp
```
%sql
SELECT * FROM f1_demo.drivers_merge TIMESTAMP AS OF '2024-02-23T07:55:08Z';
```

```
%python
df = spark.read.format("delta")\
	.option("timestampAsOf", "2024-02-23T08:15:09Z")\ 
	.load("/mnt/formula1dlfvv/demo/drivers_merge")
```

 * Using version
```
 %sql
SELECT * FROM f1_demo.drivers_merge VERSION AS OF 10
```

```
df = spark.read.format("delta").option("versionAsOf", 10).load("/mnt/formula1dlfvv/demo/drivers_merge")

```

* Delete previous versions
Normally this is done only if there is a legal requirement.
Remove all the 'commits ' older than 72 hours:
```
%sql
VACUUM f1_demo.drivers_merge RETAIN 72 HOURS
```

* Use case. 
Say you deleted by error an entry
```
%sql
DELETE FROM f1_demo.drivers_merge WHERE driverId = 1;
```
You check the version log and get the version number where that data was still present : **9**. The latest version, where you performed the delete is version **10**.
Then you can rollback like this :
```
%sql
MERGE INTO f1_demo.drivers_merge tgt
USING f1_demo.drivers_merge VERSION AS OF 9 src
   ON (tgt.driverId = src.driverId)
WHEN NOT MATCHED THEN
   INSERT *
```