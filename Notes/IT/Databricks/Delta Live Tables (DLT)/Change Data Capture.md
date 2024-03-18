Type of changes:
* Inserting new records
* Updating existing records
* Deleting existing records

Delta Live Tables support CDC with `APPLY CHANGES INTO`:

```sql
APPLY CHANGES INTO LIVE.target_table
FROM STREAM(LIVE.cdc_feed_table)
KEYS (key_field)
APPLY AS DELETE WHEN operation_field = "DELETE"
SEQUENCE BY sequence_field
COLUMNS *
```
`KEYS` specify the primary key fields. If the keys exist the record will be updated. If not inserted.
`APPLY AS DELETE WHEN operation_field = "DELETE` specify that when the condition 
`SEQUENCE BY` specifies the sequence field on how the operation should be applied.

Pros:
* Orders late-arrive records using the sequencing key
* Default assumption is UPSERT
* Optional APPLY AS DELETE WHEN
* Allows specify one or many fields as primary key
* Specify columns to ignore with the EXCEPT keyword
* Support applying changes as SCD (Slowly changing dimensions) Type 1 or SCD Type 2.

Cons:
- Breaks the append-only requirements for streaming table sources. (Because the records with APPLY CHANGES INTO can be deleted or modified) so if you implement this you cannot work with Streaming data sources!