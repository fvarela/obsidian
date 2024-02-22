Databases in Databricks are just a namespace or a logical grouping of tables. Tables can be managed or external but databased don't. This is an important distiction.
### Create database:
`CREATE DATABASE IF NOT EXISTS demo;`

### List databases:
`SHOW databases;`

### Describe database:
`DESCRIBE DATABASE EXTENDED demo;`

### See what the current database is:
`SELECT CURRENT_DATABASE();`

### Select a database:
`USE database_name;`

### Show tables in current database
`SHOW TABLES;`

### Show tables in default database:
`SHOW TABLES IN default;`

