How to query from a DataFrame. It doesn't matter if you read the Dataframe from a file, group of files, Table or View.

Example:
```
from pyspark.sql.functions import upper
drivers_day3_df = spark.read \
  .option("inferSchema", True) \
    .json("/mnt/formula1dlfvv/raw/2021-03-28/drivers.json")\
      .filter("driverId BETWEEN 1 AND 5 OR driverId BETWEEN 16 AND 20") \
        .select("driverId", "dob", upper("name.forename").alias("forename"), upper("name.surname").alias("surname"))
```

* Filter
`.filter("driverId BETWEEN 1 AND 5 OR driverId BETWEEN 16 AND 20")`

* Select
`.select("driverId", "dob")`

* Upper
`upper("name.forename")`

* Alias
`.alias("forename")`
