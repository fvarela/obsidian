## Aggregations

#### Group by
```
SELECT nationality, COUNT(*)
	FROM drivers
GROUP BY nationality
HAVING COUNT(*) > 100;
```


