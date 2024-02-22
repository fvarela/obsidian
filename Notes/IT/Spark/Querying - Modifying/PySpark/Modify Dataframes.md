### Select only some columns
```
#Option 1
circuits_selected_df = 
	circuits_df.select("circuitId", "circuitRef")

#Option 2
circuits_selected_df = 
	circuits_df.select(circuits_df.circuitId, circuits_df.circuitRef)

#Option 3
circuits_selected_df = 
	circuits_df.select(circuits_df["circuitId"], circuits_df["circuitRef"])

#Option 4
circuits_selected_df = 
	circuits_df.select(col("circuitId"), col("circuitRef"))

```
### Add column to existing dataframe:
`circuits_final_df = circuits_final_df.withColumn("env", lit("Production"))`

```
races_with_timestamp_df = races_df.withColumn("ingestion_date", current_timestamp()) \
.withColumn("race_timestamp", to_timestamp(concat(col('date'), lit(' '),      col('time')), 'yyy-MM-dd HH:mm:ss'))
```

### Rename columns and add new columns:
```
final_df = qualifying_df \
.withColumnRenamed("qualifyId", "qualify_id") \
.withColumn("ingestion_date", current_timestamp()) \
.withColumn("name", concat(col("name.forename"), lit(" "), col("name.surname")))
```

### Select and rename at once
```
circuits_selected_df = 
	circuits_df.select(
		col("circuitId").alias("circuit_id"),
		col("circuitRef").alias("circuit_ref"))
```

### Remove unnecessary columns:

```
results_final_df = results_with_columns_df.drop(col("statusId"))
```

### Apply filters

```
demo_df = race_results_df.filter("race_year IN (2019, 2020) AND race_month=5")
```


