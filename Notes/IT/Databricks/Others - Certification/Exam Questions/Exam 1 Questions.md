![[Pasted image 20240318191324.png]]

Solution: C. D and E are wrong because there is no Structured Streaming here. There is a batch work. total_sales_summary needs to be upsert (option C), not overwritten (option A) or appended (option B).


- Jobs with multiple tasks. What happens when a task fails. How dependencies are handled? How do rollbacks work?

![[Pasted image 20240318191419.png]]

Solution: A. If the tasks are finished they are finished. There is no rolling back


* Understanding an StackTrace error. 'Cannot Resolve ' heartrateheartrateheartrate '  given input colums: ...

![[Pasted image 20240318192332.png]]

Answer: B

- Ganglia Metrics. How to spot a bottleneck on the driver node.

![[Pasted image 20240318193013.png]]


E. If the overall cluster CPU utilization is around 25% it means that the driver node is not using the available resources efficiently.


- How display() works.

![[Pasted image 20240318193642.png]]

Solution: D. Display() uses catching. Several executions of the same cell that uses display() won't have the same execution time because of the catching.

- Job run history. How many days are logs retained.

![[Pasted image 20240318215909.png]]

Answer C. After 60 days the logs are lost. If you want to keep them you should archive them before that.


- Managed and External tables. Specifying a location when  creating a database.
![[Pasted image 20240318220329.png]]

Solution D. 
	A and C cannot be right because there is no such thing as logical tables. The table is managed because it was created without specifying a location.


- Process JSON files and handling the schema.

![[Pasted image 20240318221104.png]]Solution D. Setting the types manually ensures 100% accuracy.
	Cannot be B because you cannot manually modify the parquet file
	Cannot be E. Schema inference might not always work!



- Capture Data Changes and how readChangeFeed works by default.

![[Pasted image 20240318222028.png]]

Solution D: readChangeFeed without providing a version results in the latest snapshot being fetched.
	A, B are wrong because this is a batch job
	C doesn't make sense to filter on current_timestamp()
	E is just getting the files but it is not checking if they have been process or not


- Delta tables and Change Data Feed.

![[Pasted image 20240318224031.png]]

Solution: B. It will append all the entries on each run because it queries the changes from version 0 on every run. 


- How merge works:
![[Pasted image 20240319094241.png]]

Solution B.

- Clusters configuration

![[Pasted image 20240319094509.png]]

Solution D. (This one is not clear). It offers the best balance between process and parallelism.


- Troubleshoot long running task
![[Pasted image 20240319095055.png]]


Solution D. Skew means that some partition have more data, some has less data.
	A If the task is queue that does not count as execution time.
	B Spill is when you don't have enough memory and data goes to the disk. If that is the case it should affect all tasks, not only a few.
	C All the executions of the task will always be in one region. 
	E It will apply to all the tasks, not only some


- Size of Spark Partitions

![[Pasted image 20240319100011.png]]

Solution A. Maximum number of bytes to part into a single partition when reading files.
	D. That option does not exists. The correct one is `spark.sql.files.minPartitionNum`
	E. That is the advisory size in bytes of the shuffle partition during adaptive optimization.
	C. OpenCostInbytes is the estimated cost to open a file.
	B. autoBroadcastJoinThreshold. Maximum size in bytes for a table that will be broadcast to all nodes when performing a join

- Structured Streaming
![[Pasted image 20240319101823.png]]

Solution D

- Delta Lake auto compaction

![[Pasted image 20240319102149.png]]

Solution E. Auto optimize tries to compact to 128 in contrast to manual OPTIMIZE that targets 1GB.


- Structured Streaming scheduling

![[Pasted image 20240319102755.png]]

Solution E. By decreasing the trigger interval you will be reducing the size of the batches.
	A In the text it doesn't say anything about idle executors.


- Structured Streaming and checkpoints.

![[Pasted image 20240319103945.png]]

Solution E. Each stream needs to have its own checkpoint directory


- Structured Streaming. Group by and Window function.

![[Pasted image 20240319104456.png]]

Solution B. Window function that get record in a 5 minutes interval.
	E Lag is a window function 

- Stream - Static joins

![[Pasted image 20240319105911.png]]

Solution A. For each microbatch received in the streming table Spark gets the latest version of the static table.


- OPTIMIZE and auto tune.

![[Pasted image 20240319110248.png]]

Solution A. In order to reduce workload autotune can modify the file size.



![[Pasted image 20240319121727.png]]

Solution B. The logic executes when the table is created. The table goes to DBFS because no location was provided.
	A. It will not return anything. It will store the data in the table recent_orders.



![[Pasted image 20240319122839.png]]

Solution E. To filter for changes look for change data feed!
	A. We are not checking if predictions changed.

- 

![[Pasted image 20240319123756.png]]

Solution C. You select the most recent update and do a merge operation.
	A. There might be duplicates in the batch and with this solution there is no way to handle that.
	B. last_updated will not give you the latest record, you should filter as well using last_login.


![[Pasted image 20240319125035.png]]

Solution D. Go for change data feed.

- REST API and Jobs

![[Pasted image 20240319125443.png]]

Solution C. There is no trigger defined. The name is optional (it does not have to be unique) so it will create three different jobs. 

![[Pasted image 20240319125936.png]]

Solution E. The default retention period is 7 days. 


![[Pasted image 20240319131325.png]]

Solution D. The Delta log is scanned for min and max values.


![[Pasted image 20240319131830.png]]

Solution E. You cannot pass a python variable to an sql cell like that.


![[Pasted image 20240319132400.png]]

Solution B. Each write will contain unique records but the write uses a simple append so there might be duplicate entries in the target table.


![[Pasted image 20240319135527.png]]

Solution A. Write in append mode will give the desired behaviour.
	There is no readStream, you cannot use C or E
	D. If you do an overwrite you cannot check its history



![[Pasted image 20240319140236.png]]

Solution E. The connection would work. The string REDACTED will appear.


![[Pasted image 20240319140909.png]]

Solution B. I think it is E so this one is not clear for me.


- Databricks SQL. Alerts.

![[Pasted image 20240319143224.png]]

Solution E. The averate temperature was greater than 120 for at least one sensor on three consecutive executions of the query.


![[Pasted image 20240319143838.png]]

Solution D. Job Cluster instead of All-Purpose and Max concurrent runs 1.


![[Pasted image 20240319144230.png]]

Solution C. They don't need to manage and with the 'Can Restart' they can start and stop the cluster. 


![[Pasted image 20240319160214.png]]

Solution E. widgets is the way to pass parameters to notebooks.


![[Pasted image 20240319160517.png]]

Solution C. That is the only way to make sure that all the tables are external.


![[Pasted image 20240319160723.png]]
Solution C. They use their personal access tokens. One will be associated with the job creation and the other with the job execution.


![[Pasted image 20240319161230.png]]

Solution A. Separate databases allow handling access easily.


![[Pasted image 20240319161908.png]]Solution E. It will contain only two columns and the email will be REDACTED

![[Pasted image 20240319162601.png]]
Solution B. 

![[Pasted image 20240319162649.png]]
Solution B

![[Pasted image 20240319162925.png]]
Solution A.

![[Pasted image 20240319163031.png]]
Solution C


![[Pasted image 20240319163113.png]]
Solution C. Compute should be deployed in the same region the data is stored.


![[Pasted image 20240319163531.png]]
Solution B. The table will be overwritten.

![[Pasted image 20240319174609.png]]
Solution D. Believe it or not if you loop and print character by character you can output the whole secret in plain text.

![[Pasted image 20240319175558.png]]
Solution D. Can Read

![[Pasted image 20240319180715.png]]
Solution C. The table contain records that violate the check

- Predicate push down
Predicate pushdown works by evaluating filtering predicates in the query againsta metadata stored in the Parquet files.
![[Pasted image 20240319181831.png]]
Solution E


![[Pasted image 20240319184921.png]]
Solution B. It is not clear to me. It should be a type 2, that is correct but I dont see how old values are marked as no longer current.


![[Pasted image 20240319191434.png]]
Solution E.


![[Pasted image 20240319192206.png]]
Solution D. Jobs/Get


![[Pasted image 20240319212046.png]]
Solution E. Until you run the VACUUM the record are available if you do a time travel.


![[Pasted image 20240319212335.png]]
Solution B.


![[Pasted image 20240319213214.png]]
Solution C.

![[Pasted image 20240319213430.png]]
Solution D.

![[Pasted image 20240319213803.png]]
Solution A.

![[Pasted image 20240319214035.png]]
Solution A.
