```sql
ALTER TABLE orders_silver ADD CONSTRAINT timestamp_within_range CHECK (order_timestamp >= '2020-01-01')
```

```sql
ALTER TABLE orders_silver ADD CONSTRAINT valid_quantity CHECK (quantity >0);
```

If you attempt a write operation and the constraint fails the write operation would fail complete. It would not insert anything. This is because all transactions on delta lake are ACID so atomicity is guaranteed. It either success or nothing happens.

When adding the CONSTRAINT spark will check the existing entries and if some of them violates the constraint it will yield an AnalysisException and the CONSTRAINT will not be added to the table.

- DROP CONSTRAINT:

```sql
ALTER TABLE orders_silver DROP CONSTRAINT timestamp_within_range;
```

