Delta Live Table pipelines are defined in notebooks or code files using either SQL or PySpark.
Define your data transformation and pipeline logic using SQL or Python
DLT constructs a directed acyclic graph (DAG) of your data transformations, updating downstream tables as new data arrives

DTL vs Dataframe API.

Delta Live Tables is a high-level, declarative framework designed for ETL. 

The main benefits of the Delta Live Tables are:
- Immutability, security and integrity: 
	- Once data is recorded, it cannot be altered. Good for audit trails.
Use Cases:
- Supply chain tracking
- Financial transactions
- Identity verification

The main benefits of the Dataframe API are:
- More powerfull, scalable

### Create a Delta Live Table

- Using SQL - Regular live table:
```sql
CREATE LIVE TABLE clean_data AS 
SELECT id, name, timestamp 
FROM raw_data 
WHERE name IS NOT NULL
```

- Using SQL - Streamed live table with autoloader 
`STREAMING` - Add that to declare a streaming delta table
`cloud_files` - Use that to enable AutoLoader syntax natively in SQL

```sql
CREATE OR REFRESH STREAMING LIVE TABLE orders_raw
COMMENT "The raw books orders, ingested from orders-raw"
AS SELECT * FROM cloud_files("${datasets.path}/orders-raw", "parquet",
  map("schema", "order_id STRING, order_timestamp LONG, customer_id STRING, quantity LONG"))
```


- Using Pyspark:
```python
from pyspark.sql import functions as F
import dlt

@dlt.table(
  name="clean_data",
  comment="A cleaned version of the raw_data."
)
def clean_data():
    return (
        spark.table("raw_data")
        .where(F.col("name").isNotNull())
        .select("id", "name", "timestamp")
    )
```


### Declaring dependencies - Paths


```sql
CREATE OR REFRESH LIVE TABLE customers
COMMENT "The customers lookup table, ingested from customers.json"
AS SELECT * FROM json.`${datasets.path}/customers.json`
```

`${datasets.path}` in the example above is provided as a parameter to databricks when creating the Delta Live Pipiline (using the GUI)


### Declaring dependencies - Other Tables


In the code below the dependencies to other tables are indicated with the `LIVE` keyword. Note that if the table is a streamed one you have to use `STREAM` as well in the dependency.

```sql
CREATE OR REFRESH STREAMING LIVE TABLE orders_cleaned (
  CONSTRAINT valid_order_number EXPECT (order_id IS NOT NULL) ON VIOLATION DROP ROW
)
COMMENT "The cleaned books orders with valid order_id"
AS
SELECT order_id, quantity, o.customer_id, c.profile:first_name as f_name, c.profile:last_name as l_name,
       cast(from_unixtime(order_timestamp, 'yyyy-MM-dd HH:mm:ss') AS timestamp) order_timestamp,
       c.profile:address:country as country
FROM STREAM(LIVE.orders_raw) o
LEFT JOIN LIVE.customers c
ON o.customer_id = c.customer_id
```



### Constraints

Declare a constraint and specify what happens if it is violated

* Types of Constraint Actions:
The `ON VIOLATION` clause can specify different actions:

- `DROP ROW`: This drops any rows that violate the constraint from the output.
- `FAIL UPDATE`: This causes the entire update to fail if any violations are detected.
- Omitted: Records violating constraints will be kept and reported in metrics (default)


- Constrain examples

```sql
CREATE LIVE TABLE users (
  user_id STRING,
  signup_date DATE,
  email STRING
)
CONSTRAINT user_id_not_null EXPECT (user_id IS NOT NULL) ON VIOLATION DROP ROW
CONSTRAINT signup_date_valid EXPECT (signup_date BETWEEN '2020-01-01' AND current_date()) ON VIOLATION DROP ROW
CONSTRAINT email_valid EXPECT (email LIKE '%@%.%')
COMMENT "Table of users with constraints for data quality."
```

```sql
CREATE OR REFRESH LIVE TABLE my_table (
  CONSTRAINT my_constraint EXPECT my_column > 0 ON VIOLATION DROP ROW
)
COMMENT "Table with a constraint on my_column"
AS
SELECT *
FROM incoming_data

```


### Create a Delta Live Table

Navigate to Workflows / Delta Live Tables

- `Notebook libraries` - Navigate to the notebook that has the delta live tables definition.
- `Configuration` - Add the parameters (key - values) of your pipeline (storage paths, etc).
- `Storage location` - Enter the path where the pipeline logs and data files will be stored. For example: `dbfs:/mnt/demo/dlt/demo_bookstore`
- `Target` - Enter a target database. (Generally a DLT pipeline is designed to write to a target database). If you need to write to multiple databases you would typically create separate DLT pipelines for each target database.

Running in Development mode vs Production mode:
- Development. 
	- Allows interactive development while reusing the cluster
	- Disable retries so you can quickly find problems
- Production. Create one cluster for each run