
* InferSchema option: You can set it to True and not provide a schema. It would take longer to run and it is prone to errors. Use only for exploration and once you know how the data is formatted provide the schema:

```python
circuits_schema = StructType(fields =
      [StructField("circuitId", IntegerType(), False),
      StructField("circuitRef", StringType(), False),
      StructField("name", StringType(), False),
      StructField("location", StringType(), False),
      StructField("country", StringType(), False),
      StructField("lat", DoubleType(), False),
      StructField("lng", DoubleType(), False),
      StructField("alt", IntegerType(), False),
      StructField("url", StringType(), False)])
      
my_df = spark.read\
.option("inferSchema", True) \
circuits_df = spark.read \
.option("header", True) \
.schema(circuits_schema) \
.csv(f"{raw_folder_path}/circuits.csv")

```

### Read a csv folder
Similar to reading a single csv file. Just use the path where the csv are located instead of the csv path:
```python
lap_times_df = spark.read \
.schema(lap_times_schema) \
.csv(f"{raw_folder_path}/lap_times")
```
