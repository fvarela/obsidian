Dynamic views allow dynamic ACL (access control list) to be applied to data in a table at the column or row level.

Say you have information that may be used to identify a patient. You can set the private columns not to be printed in plain test for non admin users like this:

* At column level
```sql
CREATE OR REPLACE VIEW customers_vw AS
SELECT
    customer_id,
    CASE 
        WHEN is_member('admins_demo') THEN email 
        ELSE 'REDACTED'
    END AS email,
    gender,
    CASE 
        WHEN is_member('admins_demo') THEN first_name 
        ELSE 'REDACTED'
    END AS first_name,
    CASE 
        WHEN is_member('admins_demo') THEN last_name 
        ELSE 'REDACTED'
    END AS last_name,
    CASE 
        WHEN is_member('admins_demo') THEN street 
        ELSE 'REDACTED'
    END AS street,
    city,
    country,
    row_time
FROM customers_silver
```

- At row level:
```sql
CREATE OR REPLACE VIEW customers_fr_vw AS 
SELECT * FROM customers_vw 
WHERE
CASE 
	WHEN is_member('admins_demo') THEN TRUE
	ELSE country = "France" AND row_time > "2022-01-01" 
END
```
