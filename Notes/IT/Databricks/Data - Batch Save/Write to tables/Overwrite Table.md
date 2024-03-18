* With statement `CREATE OR REPLACE`
```sql
CREATE OR REPLACE TABLE orders AS
SELECT * FROM parquet.`${dataset.bookstore}/orders`
```

* With statement `INSERT OVERWRITE
```sql
INSERT OVERWRITE orders
SELECT * FROM parquet.`${dataset.bookstore}/orders`
```
Achieves exactly the same as `CREATE OR REPLACE`
Differences:
1. `INSERT OVERWRITE` cannot create a new table
2. `INSERT OVERWRITE` It inserts only if the records have the same schema than the table.

