Each delta table has a column named `_delta_log/`
This folder contains .json files
Each commit to the table is written as a json file. 

Problem:
You may end up with many tiny json files and databricks has to read them all to see the current state of the

To solve this every 10 commits Databricks generates a Parquet checkpoint file.
So it is 10 json files, 1 parquet file, 10 json files, 1 parquet file...


Databricks also captures statistics for each added data files (for the first 32 columns):
- Minimun value in each column
- Maximum value in each column
- Null value counts for each of the columns
These statistics will be leveraged for file skipping
Nested field counts when determining the first 32 columns
- Example: 4 struct fields with 8 nested fields will total the 32 columns
Statistics are uninformative for string fields with very high cardinality:
- Example: Free text fields
- Time consuming! Move them outside the first 32 columns

Clean up:
Running the `VACUUM` command does not delete Delta log files. It only deletes the data files
Log files are automatically cleaned up by Databricks (default 30 days)
You can change that with `delta.logRetentionDuration`