
Allows you to work directly with __struct__ (hierarchical data like arrays or map objects).

### `Filter` function
Filters an array based on a given __lambda__ function
```sql
SELECT
	order_id,
	books,
	FILTER (books, i -> i.quantity >=2) AS multiple_copies
FROM orders
```
If you want to remove the entries where `multiple_copies` are empty arrays you can wrap the query like this:

```sql
SELECT order_id, multiple_copies
FROM(
	SELECT
		order_id,
		books,
		FILTER (books, i -> i.quantity >=2) AS multiple_copies
	FROM orders)
WHERE size(multiple_copies) >0;
```

### `TRANSFORM` function
Apply a transformation to all the items in an array and extract the transformed value
```sql
SELECT 
	order_id,
	books,
	TRANSFORM (
		books,
		b -> CAST(b.subtotal * 0.8 AS INT)
	) AS subtotal_after_discount
FROM orders;
```