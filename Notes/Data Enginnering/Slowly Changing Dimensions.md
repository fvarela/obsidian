Type 0
No changes allowed
Implemented on tables that are either static or append-only

Type 1
Overwrite
No history retained (use Delta Time Travel if needed)

Type 2
Add new row for each change and mark the old as obsolete
Retains the full history of values.

In addition to the other columns you need to add three columns to implement Type 2 SCD:
- current
- Effective Date
- End Date

```sql

+------------+--------------+-------+---------+---------------+----------+
| Product ID | Product Name | Price | Current | Effective Date| End Date |
+------------+--------------+-------+---------+---------------+----------+
| 1          | Product A    | 10    | True    | 2023-01-01    | NULL     |
| 2          | Product B    | 20    | True    | 2023-01-01    | NULL     |
| 3          | Product C    | 30    | True    | 2023-01-01    | NULL     |
+------------+--------------+-------+---------+---------------+----------+
```