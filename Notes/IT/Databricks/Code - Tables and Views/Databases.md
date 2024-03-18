Databases in Databricks are just a namespace or a logical grouping of tables. Tables can be managed or external but databased don't. This is an important distinction.
### Create database:

* With the default location:
```sql
CREATE DATABASE IF NOT EXISTS demo;
```

* With a custom location:
```sql
CREATE DATABASE IF NOT EXISTS f1_processed
LOCATION " /mnt/formula1dlfvv/processed";
```
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
### Drop database
`DROP DATABASE IF EXISTS f1_processed CASCADE;`
