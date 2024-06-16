

## Create a dataframe
Data types: [Data types — Polars documentation](https://docs.pola.rs/py-polars/html/reference/datatypes.html)

```python
data = {
    "date": ["2024-04-01", "2024-04-02", "2024-04-03"],
    "time": ["12:00", "13:00", "14:00"],
    "location": ["A", "B", "C"],
    "log_level": ["INFO", "ERROR", "DEBUG"],
    "spv_time": ["100", "200", "300"],
    "sn": ["001", "002", "003"],
    "node": ["N1", "N2", "N3"],
    "log_type": ["Type1", "Type2", "Type3"],
    "log_message": ["Message1", "Message2", "Message3"],
    "line_number": [1, 2, 3]
}

df = pl.DataFrame(data)
```

## Modify 

```python
# Add a column for line numbers starting from 1
line_numbers = pl.Series("line_number", range(1, len(data) + 1))
df = df.with_columns([line_numbers])
```



## Filter

```python
# Example: Filter rows where log_level is "ERROR"
filtered_df = df.filter(pl.col("log_level") == "ERROR")

# Example: Filter rows where line_number is greater than 1
filtered_df = df.filter(pl.col("line_number") > 1)

# Example: Filter rows where location is "B" or "C"
filtered_df = df.filter(pl.col("location").is_in(["B", "C"]))

```

## Select