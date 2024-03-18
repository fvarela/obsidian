
* Get aggregated values based on some column values

The inner query runs first
The pivot operation transforms the data from the subquery:
	`customer_id` would be in the rows
	Each of the `book_id` specifies would be in the columns
	`sum(quantity)` will be the value of each cell
The outer query just selects everything from the inner one.

```sql
CREATE OR REPLACE TABLE transaction AS

SELECT * FROM (
	SELECT
		customer_id,
		book.book_id AS book_id,
		book.quantity AS quantity
	FROM orders_enriched
) PIVOT (
	sum(quantity) FOR book_id IN (
	'B01', 'B02', 'B03', 'B04', 'B05', 'B06',
	'B07', 'B08', 'B09', 'B10', 'B11', 'B12'
	)
);

SELECT * FROM transactions

```

