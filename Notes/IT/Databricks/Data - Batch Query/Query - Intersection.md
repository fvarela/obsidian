
* Returns columns present in both tables:

```sql
SELECT * FROM orders
INTERSECT
SELECT * FROM orders_updates
```