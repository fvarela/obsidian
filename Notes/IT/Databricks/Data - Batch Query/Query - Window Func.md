
Use case: 
You sort a dataframe based on a column value. 
Then you want to 'rank' the results:
	The row on top should have rank = 1
	The second one should have rank = 2 ...
In order to create this 'rank' column you need a Window Function

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import desc, rank

driverRankSpec = Window.partitionBy("race_year").orderBy(desc("total_points"))
demo_grouped_df.withColumn("rank", rank().over(driverRankSpec)).show()
```


```sql
SELECT 
	nationality, 
	dob, 
	RANK() OVER(PARTITION BY nationality ORDER BY dob DESC) AS age_rank
	FROM drivers
ORDER BY nationlity, age_rank
```
With `PARTITION BY nationality` you make the rank reset for each new nationality
It is ordered by `dob` (data of birth) so the youngest in the country would have 1, the oldest would have the max number.


- Example
Order the entries by __customer_id__ and  __row__time__ and get the latest one.

```python
#Get the latest entry of each customer using the window function
from pyspark.sql.window import Window
window = Window.partitionBy("customer_id").orderBy(F.col("row_time").desc())
ranked_df = (customers_df.withColumn("rank", F.rank().over(window))
             .filter("rank == 1")
             .drop("rank"))
display(ranked_df)
```
