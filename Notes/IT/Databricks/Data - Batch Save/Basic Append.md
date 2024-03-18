- INSERT INTO
It does not prevent to add the same records many times! If you need to UPSERT you have to use Delta.
```sql
INSERT INTO orders
SELECT * FROM parquet.`${dataset.bookstore}/orders-new`
```
