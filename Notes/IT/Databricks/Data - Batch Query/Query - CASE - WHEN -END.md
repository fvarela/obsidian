```sql
CREATE FUNCTION site_type(extension STRING)
RETURNS STRING
RETURN CASE
	WHEN email LIKE "%.com" THEN "Commercial business"
	WHEN email LIKE "%.org" THEN "Non-profits organizations"
	WHEN email LIKE "%.edu" THEN "Educational institution"
	ELSE concat("Unknown extension for domain: ", split(email, "@")[1])
	END;
```