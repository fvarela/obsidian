### Inner Join
Only returns if matches both tables
```
SELECT
	FROM v_driver_standings_2018 d_2018
	JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Left Join
All the entries from the left table, only matches from the right one
```
SELECT
	FROM v_driver_standings_2018 d_2018
	LEFT JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```


### Right Join
All the entries from the right table, only matches from the left one
```
SELECT
	FROM v_driver_standings_2018 d_2018
	LEFT JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Full Outer Join
All the matches from the left table OR the right one
```
SELECT
	FROM v_driver_standings_2018 d_2018
	FULL JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Semi Join
Inner Join (matches on both tables only) with only the data from the left table
```
SELECT
	FROM v_driver_standings_2018 d_2018
	SEMI JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Anti Join
Retrieves entries that have no match
```
SELECT *
	FROM v_driver_standings_2018 d_2018
	ANTI JOIN v_driver_standings_2020 d_2020
	ON (d_2018.driver_name = d_2020.driver_name)
```

### Cross Join
Every record on the left joined with every record on the right.
Cartesian product.
Use with caution!
```
SELECT *
	FROM v_driver_standings_2018 d_2018
	CROSS JOIN v_driver_standings_2020 d_2020
```