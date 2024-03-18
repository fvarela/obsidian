- Deep Cloning. Copies both data and metadata

```
CREATE TABLE table_clone
DEEP CLONE source_table;
```

If you write the code above again and again it will synchronize changes from the source to the clone every time.
Since it copies data it can take a while for large datasets


- Shallow clone

It just copies the delta transaction logs.

```
CREATE TABLE table_clone
SHALLOW CLONE source_table
```

There is not data moving. 
Good option for testing some changes on a table without the risk of modifying the actual table.


