
### Add column to existing dataframe:

* Column based on string with `lit`:
```python
circuits_final_df = circuits_final_df.withColumn("env", lit("Production"))
```

* Column with line number:
```python
.withColumn(
	"log_line", 
	row_number().over(Window.orderBy(monotonically_increasing_id()))-1)
```
* Current timestamp:
```python
.withColumn("ingestion_date", current_timestamp())
```

* Concat + timestamp:
```python
.withColumn("race_timestamp", to_timestamp(concat(col('date'), lit(' '),      col('time')), 'yyy-MM-dd HH:mm:ss'))
```
- With String split extracted value:.
```python
split_col = split(col("value"), "\t")
self.final_df = self.combined_df\
	.withColumn("system", split_col.getItem(3))
```

* With Regex Replacement
```python
.withColumn("logging_level", regexp_replace("[22]", "[\\[\\]]", ""))
```

### Rename columns and add new columns:
```python 
final_df = qualifying_df \
.withColumnRenamed("qualifyId", "qualify_id") \
.withColumn("ingestion_date", current_timestamp()) \
.withColumn("name", concat(col("name.forename"), lit(" "), col("name.surname")))
```

### Select and rename at once
```python
circuits_selected_df = 
	circuits_df.select(
		col("circuitId").alias("circuit_id"),
		col("circuitRef").alias("circuit_ref"))
```

### Remove unnecessary columns:

```python
results_final_df = results_with_columns_df.drop(col("statusId"))
```

### Apply filters

```python
demo_df = race_results_df.filter("race_year IN (2019, 2020) AND race_month=5")
```


### Combine two dataframes

```python
union_df = df1.union(df2)
```

```sql
SELECT * FROM orders
UNION
SELECT * FROM orders_updates
```