```python

from delta.tables import DeltaTable

class HandleDeltaLakeTable:
    def __init__(self, database, table, upsert_columns = ["sn", "tr", "date", "log_line"], drop_database=False, drop_table=False):
        self.database = database
        self.table = table
        self.upsert_columns = upsert_columns
        if drop_database:
            self.drop_database()
        self.initialize_database()
        if drop_table:
            self.drop_table()
    def drop_database(self):
        spark.sql(f"DROP DATABASE IF EXISTS {self.database} CASCADE")
    def initialize_database(self):
       spark.sql(f"CREATE DATABASE IF NOT EXISTS {self.database}")
    def drop_table(self):
        spark.sql(f"DROP TABLE IF EXISTS {self.database}.{self.table}")
    def upsert_dataframe_to_delta(self, new_df):
        if spark._jsparkSession.catalog().tableExists(f"{self.database}.{self.table}"):
            print("Table exists")
            deltaTable = DeltaTable.forName(spark, f"{self.database}.{self.table}")
            print(f"Total number of rows: {deltaTable.toDF().count()}")
            upsert_clause = " AND ".join([f"oldData.{col} = newData.{col}" for col in self.upsert_columns])
            deltaTable.alias("oldData").merge(
                new_df.alias("newData"),
                        upsert_clause) \
                    .whenMatchedUpdateAll() \
                    .whenNotMatchedInsertAll() \
                    .execute()
            print(f"Total number of rows after merge: {deltaTable.toDF().count()}")
        else:
            print("Table does not exist")
            new_df.write.format("delta").partitionBy("sn").saveAsTable(f"{self.database}.{self.table}")
            print(f"Total number of rows on db after inserting new records: {spark.sql(f'select * from {self.database}.{self.table}').count()}")

```