
NOT NULL

```
ALTER TABLE table_name ADD CONSTRATINTS constraint_name constraint_details
```

CHECK

```
ALTER TABLE orders ADD CONSTRAINT valid_date CHECK (date > '2020-01-01');
```
