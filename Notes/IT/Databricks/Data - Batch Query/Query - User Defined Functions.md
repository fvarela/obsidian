You can declare SQL functions
They are saved on a database. Can be described with `DESCRIBE FUNCTION get_url` and removed with `DROP FUNCTION get_url`

Function that returns a strings. 
```sql
CREATE OR REPLACE FUNCTION get_utl(email STRING)
RETURNS STRING
RETURN concat("https://www.", split(email, "@")[1])
```

Then you can use it like this:
```sql
SELECT email, get_url(email), domain
FROM customers
```
