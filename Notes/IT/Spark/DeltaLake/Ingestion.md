Documentation: https://docs.delta.io


### Writting from a DataFrame to a Managed Delta Table

```
results_df.write.format("delta") \
	.mode("overwrite")\
	.saveAsTable("f1_demo.results_managed") 
```


### Writting from a DataFrame to a Storage Location
```
results_df.write.format("delta").mode("overwrite").save("/mnt/formula1dlfvv/demo/results_external")
```