### Inner Join
Only returns if matches both tables

- Python
```python
# Here circuits_df is the LEFT table
# races_df is the RIGHT table

race_circuits_df = circuits_df.join(races_df, circuits_df.circuit_id == races_df.circuit_id, "inner") \
  .select(circuits_df.circuit_name, circuits_df.location, circuits_df.country, races_df.race_name, races_df.round)
```

- SQL
```sql
SELECT
	FROM v_driver_standings_2018 d_2018
	JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Outer Left Join
Gets the entries from the left table and matches from the right one

- Python
```python
# Some circuits will have no race (because it was filtered out).
# Missing data would appear as null in the joined df.

race_circuits_df = circuits_df\
 .join(races_df, circuits_df.circuit_id == races_df.circuit_id, "left") \
 .select(circuits_df.circuit_name, circuits_df.location, races_df.race_name)
```

- SQL
```sql
SELECT
	FROM v_driver_standings_2018 d_2018
	LEFT JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```



### Outer Right Join
Gets the entries from the right table and only matches from the left one

- Python
```python
# Some races will have no circuit (because it was filtered out). 
# Missing data would appear as null in the joined df.

race_circuits_df = circuits_df\
	.join(races_df, circuits_df.circuit_id == races_df.circuit_id, "right") \
	.select(circuits_df.circuit_name, circuits_df.location, races_df.race_name)
```

- SQL
```sql
SELECT
	FROM v_driver_standings_2018 d_2018
	LEFT JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```


### Full Outer Join
Gets all the records from the Left and Right tables

- Python
```python
race_circuits_df = circuits_df\
	.join(races_df, circuits_df.circuit_id == races_df.circuit_id, "full") \
	.select(circuits_df.circuit_name, circuits_df.location, circuits_df.country, races_df.race_name, races_df.round)
```

- SQL
```sql
SELECT
	FROM v_driver_standings_2018 d_2018
	FULL JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```



### Semi Join
Similar to Inner Join but only returns all rows from the LEFT TABLE that have a corresponding match on the right table
You can achieve the same thing using an Inner join and selecting what columns you want to get.
- Python
```python
race_circuits_df = circuits_df\
.join(races_df, circuits_df.circuit_id == races_df.circuit_id, "semi")
```

- SQL
```sql
SELECT
	FROM v_driver_standings_2018 d_2018
	SEMI JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Anti Join
Opposite of Semi Join. Retrieve everything on the LEFT TABLE that had no match on the right table
- Python
```python
race_circuits_df = circuits_df.join(races_df, circuits_df.circuit_id == races_df.circuit_id, "anti")
```

- SQL
```sql
SELECT *
	FROM v_driver_standings_2018 d_2018
	ANTI JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Cross Join
Use with caution!
Returns a cartesian product. Results can be huge
If you have 'n' records on the left and m on the right it would return n\*m records
So each record on the left would be match with EACH record on the right.

- Python. 
```python
race_circuits_df = races_df.crossJoin(circuits_df)
```

- SQL:
```sql
SELECT *
	FROM v_driver_standings_2018 d_2018
	CROSS JOIN v_driver_standings_2020 d_2020
```