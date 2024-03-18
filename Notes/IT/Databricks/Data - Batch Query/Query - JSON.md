
- __Pyspark__

You have to specify the schema :

```python
constructors_schema = "constructorId INT, constructorRef STRING, name STRING, nationality STRING, url STRING"

constructor_df = spark.read \
  .schema(constructors_schema) \
  .json("/mnt/formula1dlfvv/raw/constructors.json")
```

Similarly with a nested json (complex schema):

```python
name_schema = StructType(fields=[StructField("forename", StringType(), True),
                         StructField("surname", StringType(), True)])

drivers_schema = StructType(fields=[StructField("driverId", IntegerType(), True),
                         StructField("driverRef", StringType(), True),
                         StructField("number", IntegerType(), True),
                         StructField("code", StringType(), True),
                         StructField("name", name_schema),
                         StructField("dob", DateType(), True),
                         StructField("nationality", StringType(), True),
                         StructField("url", StringType(), True)                  
                         ])                      
  
drivers_df = spark.read \
  .schema(drivers_schema) \
  .json("/mnt/formula1dlfvv/raw/drivers.json")

```


Same with Structure Streaming:

```python
from pyspark.sql import functions as F

json_schema = "order_id STRING, order_timestamp Timestamp, customer_id STRING, quantity BIGINT, total BIGINT, books ARRAY<STRUCT<book_id STRING, quantity BIGINT, subtotal BIGINT>>"

query = (spark.readStream.table("bronze")
         .filter("topic = 'orders'")
         .select(F.from_json(F.col("value").cast("string"), json_schema).alias("v"))
         .select("v.*")
         .writeStream
         .option("checkpointLocation", "dbfs:/mnt/demo_pro/checkpoints/orders_silver")
         .trigger(availableNow=True)
         .table("orders_silver"))

query.awaitTermination()
```


- __SQL__

* `:` Syntax
If you have a dataframe with three columns 'id', 'hospital_name' and 'record' where 'record' is a json string you can query it like this (`:` syntax):
```sql
SELECT id, record:first_name, record:last_name, record:address:country
```

* Parse json objects into struct types
You need to provide the schema. So __this would fail__:
```sql
SELECT from_json(profile) AS profile_struct
FROM customers;
```

The way to infer the schema is as follows. Get the first record:
```sql
SELECT profile
FROM customers
LIMIT 1
```

Get the output and add it to the query to provide the schema. __This would work__:
```sql
SELECT 
	customer_id, 
	from_json(
		profile, schema_of_json('{"first_name":"Thomas","last_name":"Lane", "gender":"Male","address":"{"street":"06 Boulevard Victor Hugo","city":"Paris","country":"France"}}')) 
AS profile_struct
FROM customers;
```

The schema of json can be also specified with the actual schema:
 ```sql
SELECT v.*
FROM (
  SELECT from_json(cast(value AS STRING), 'order_id STRING, order_timestamp Timestamp, customer_id STRING, quantity BIGINT, total BIGINT, books ARRAY<STRUCT<book_id STRING, quantity BIGINT, subtotal BIGINT>>') v
  FROM bronze
  WHERE topic = 'orders'
)
```

`SELECT v.*`
	This is the outer query. Selects all the columns from the subquery.

