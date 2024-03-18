### ABFS, WASBS
ABFS:
	Designed for Azure Data Lake Storage Gen2
	Optimized for big data analytics
	Supports hierarchical namespaces:
		Create, rename and delete Directories like in a traditional file system.
	Supports fine grained access control
	Supports atomic file/folder operations:
		File rename or directory moves do not interfere with data integrity, even in the presence of concurrent operations
WASBS
	Good for accessing blobs without the advanced features of ABFS.
	Flat Namespaces.
		It can simulate hierarchical structures using virtual directories (prefixes in blobs names) but it is limited 


### DBFS

- DBFS Root
This is where the default Blob storage was mounted during the creation of the Databricks workspace
Can be access from any of the clusters mounted in the workspace
Can be browse using the UI interface (enable it on Settings/Advanced/DBFS File Browser)
Has a folder called FileStore that can be used for temporary storage
Managed tables are stored in here

To check what you have in dbfs root:
`display(dbutils.fs.ls('/')`
It contains the following:
- `dbfs:/databricks-datasets/` - Some sample datasets
- `dbfs:/databricks-results/` - Where databricks save temporary outputs during execution
- `dbfs:/FileStore/` - This one would appear only if you upload any file using the GUI or programmatically. It is like the default 'integrated hd' location

