
* Flatten struct types into columns with *
The extracted columns combines the names of the outer struct and its inner fields using a dot ('.')
```sql
CREATE OR REPLACE TEMP VIEW customers_final AS
	SELECT customer_id, profile_struct.*
	FROM parsed_customers;
SELECT * fROM customers_final
```


### Explode function

Create one row for each value of an original array.
Check in the example below how __phone_details__ is an array. In the exploded version the column __phone_details_exploded__ has each individual value of that array

```
Input Dataframe: df  
  
+---+----+---------------------------+  
|id |name|phone_details              |  
+---+----+---------------------------+  
|1  |A   |[1654123, 2654122, 3654121]|  
|2  |B   |[1254123, 2354122, 3454121]|  
|3  |C   |[]                         |  
|4  |D   |null                       |  
+---+----+---------------------------+  
  
Output Dataframe: df_exploded  
  
+---+----+---------------------------+----------------------+  
|id |name|phone_details              |phone_details_exploded|  
+---+----+---------------------------+----------------------+  
|1  |A   |[1654123, 2654122, 3654121]|1654123               |  
|1  |A   |[1654123, 2654122, 3654121]|2654122               |  
|1  |A   |[1654123, 2654122, 3654121]|3654121               |  
|2  |B   |[1254123, 2354122, 3454121]|1254123               |  
|2  |B   |[1254123, 2354122, 3454121]|2354122               |  
|2  |B   |[1254123, 2354122, 3454121]|3454121               |  
+---+----+---------------------------+----------------------+
```


* python
```python
  val df = List(
    ("1", "A", List("1654123", "2654122", "3654121")),
    ("2", "B", List("1254123", "2354122", "3454121")),
    ("3", "C", List()),
    ("4", "D", null)
  ).toDF("id", "name", "phone_details")

  df.show(false)
  df.printSchema()

  val df_exploded =
    df.withColumn("phone_details_exploded", explode($"phone_details"))

  df_exploded.show(false)
  df_exploded.printSchema()
```

- SQL
```sql
SELECT order_id, customer_id, explode(books) AS book
FROM orders
```


### Collect Set Function

Get unique values for a field (including structs) removing duplicates within each group defined by GROUP BY:
```sql
SELECT customer_id,
	collect_set(order_id) AS orders_set,
	collect_set(books.book_id) AS books_set
FROM orders
GROUP BY customer_id
```
	
Advanced scenario with collect_set:
	
```sql
SELECT customer_id,
	collect_set(books.book_id) AS before_flatten,
	array_distinct(flatten(collect_set(books.book_id))) AS after_flatten
FROM orders
GROUP BY customer_id
```
In the query above:
`collect_set(books.book_id)` returns a set(array) of unique items for each group.
`flatten`merges arrays from collect_set into a single array
`array_distinct` removes duplicates from the flattened array


