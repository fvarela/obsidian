
```
SELECT 
	nationality, 
	dob, 
	RANK() OVER(PARTITION BY nationality ORDER BY dob DESC) AS age_rank
	FROM drivers
ORDER BY nationlity, age_rank
```
With `PARTITION BY nationality` you make the rank reset for each new nationality
It is ordered by `dob` (data of birth) so the youngest in the country would have 1, the oldest would have the max number.
![[Pasted image 20240211100852.png]]


