
Use case: 
You sort a dataframe based on a column value. 
Then you want to 'rank' the results:
	The row on top should have rank = 1
	The second one should have rank = 2 ...
In order to create this 'rank' column you need a Window Function

```
from pyspark.sql.window import Window
from pyspark.sql.functions import desc, rank

driverRankSpec = Window.partitionBy("race_year").orderBy(desc("total_points"))
demo_grouped_df.withColumn("rank", rank().over(driverRankSpec)).show()
```
