
## Aggregate
### Based on one condition: Count, CountDistinct, Sum
```
from pyspark.sql.functions import count, countDistinct, sum

demo_df.select(count("*"))

demo_df.select(countDistinct("race_name"))

demo_df.select(sum("points"))

```

### Based on several conditions: AGG

```
#Does not work! Cannot aggregate sequencially based on several conditions
# demo_df\
#   .groupBy("driver_name") \
#   .sum("points") \
#   .countDistinct("race_name") \
#   .show()

#Works!
demo_df\
  .groupBy("driver_name") \
  .agg(
    sum("points").alias("total_points"),                                               countDistinct("race_name").alias("number_of_races")) \
  .show()
```




