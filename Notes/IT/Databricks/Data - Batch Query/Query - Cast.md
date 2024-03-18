Cast binary fields as Strings:

```sql
SELECT cast(key AS STRING), cast(value AS STRING)
FROM bronze
LIMIT 20
```

