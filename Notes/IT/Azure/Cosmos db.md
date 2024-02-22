#### Get one element:
SELECT TOP 1 * FROM c
WHERE c.Timestamp >"2023-09-14"
AND c.Timestamp <"2023-09-16" 
AND c.Name_0 = "BTS"
#### Get unique values
SELECT VALUE c.Name FROM c
WHERE c.Timestamp >"2023-09-14"
AND c.Timestamp <"2023-09-16" 
AND c.Name_0 = "BTS"
GROUP BY c.Name


Get all the entries for a particular pv:
SELECT * FROM 
WHERE c.Name = "PBST:SNS:R3:0:GET_INTERLOCK_STATUS"


SELECT COUNT(1) AS Count, c.Name
FROM c
WHERE c.Name_0 = 'MCS'
GROUP BY c.Name
ORDER BY c.Name DESC