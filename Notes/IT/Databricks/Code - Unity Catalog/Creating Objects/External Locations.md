### Create External Locations - Alternative to Mounts
You can use the catalog explorer for it.
With this you use an Azure container inside Databricks but you can handle permissions with Unity Catalog.

Then you can access it like this:

```sql
DESCRIBE EXTERNAL LOCATION `external-data`;
```

The url would be something like:
`abfss://my-dtabricks-container@mydbstoragetestaccount.dfs.core.windows.net/`

If you want to use it you need to type the whole url:
```
%fs ls abfss://my-dtabricks-container@mydbstoragetestaccount.dfs.core.windows.net/
```


To do this you need to define the 
- Storage Credential
- External Location

1. Create an Access Connector for Azure Databricks
The Access Connector has no configuration that is specific to the Azure Storage Account.

2. Create the Storage Account (external) if needed.
Make sure you enable the hierarchical namespace (to enable data lake).
3. Assign Storage Blob Contributor Role:
	- Go to IAM on the Storage Account
	- Look for the role Storage Blob Contributor
	- Select Managed Identity
	- Click on Select Members and look for the Azure Databricks connector:
![[Pasted image 20240227090735.png]]

4. Assign Databricks credentials
	If you have access... 
	- Go to Databricks / Catalog 
	- Click on External Data/Storage Credentials
	- Click on create credential
		- Enter the connector id generated on Azure
		- Once it is created: Provide access to team members if needed
	
5. Create External Location
	If you have access...
	- Go to Databricks /Catalog
	- Click on External Data/External Locations
	- Click on Create External Location on the top right corner
		- Enter the url:
			- abfss://{container_name}@{storage_account}.dfs.core.windows.net/
		- Select the storage credentials from the dropdown (The one you created before)
6. Access the External Storage
	- Using dbutils it would be: 
		`dbutils.fs.ls('abfss://demo@databrickscoursextdl.dfs.core.windows.net')`

You can also create the External Location with sql:
```
CREATE EXTERNAL LOCATION <loation_name>
URL 'abfss://<container_name>@<storage_account>.dfx.core.windows.net/<path_subfolder>'
WITH (STORAGE CREDENTIAL databrickscourse_ext_storage_credential);
```

Describe external location:
`DESC EXTERNAL LOCATION <location_name>;`