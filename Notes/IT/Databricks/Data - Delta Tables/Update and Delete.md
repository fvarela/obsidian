This is the main difference between Delta Lake and others. With Delta Lake you can Update and Delete entries.
You can use both SQL or Python

### Update

* Using SQL on a table that was saved with format Delta:
```sql
UPDATE f1_demo.results_managed
  SET points = 11 - position
WHERE position <= 10
```

* Using python:
```python
from delta.tables import DeltaTable
deltaTable = DeltaTable.forPath(spark, "/mnt/formula1dlfvv/demo/results_managed")
deltaTable.update("position <= 10", {"points" : "21 - position"})
```


### Delete

* Using SQL:
```sql
DELETE FROM f1_demo.results_managed
WHERE position > 10;
```

* Using Python
```python
from delta.tables import DeltaTable

deltaTable = DeltaTable.forPath(spark, "/mnt/formula1dlfvv/demo/results_managed")
deltaTable.delete("points = 0")
```

