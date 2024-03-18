
With the CREATE TABLE you have to specify the schema:
```
CREATE TABLE table_1
(col1 INT, col2 STRING, col3 DOUBLE)
```

With CTAs the schema is inferred: 
```
CREATE TABLE table_1
AS SELECT col1, col2, col3 FROM table_2
```