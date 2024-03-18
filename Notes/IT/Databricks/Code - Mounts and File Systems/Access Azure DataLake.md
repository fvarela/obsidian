

## With Access Keys

- How to:
	1. Set up the configuration
	```python
	spark.conf.set(
	"fs.azure.account.key.<storage-account>.dfs.core.windows.net",
	"<azure_storage_access_key>"
	)
	```
	2. Then you can use the abfs[s] driver to access the files:
	
```python
dbutils.fs.ls("abfss://<container_name>@<storage_name>.dfs.core.windows.net/")
```
	
- Problem: The access key gives access to everything

## With SAS Token
- How to:
	1.  Set up the configuration for the SAS token:
```python
spark.conf.set(
	"fs.azure.account.auth.type.<storage-account>.dfs.core.windows.net",
	"SAS")
spark.conf.set(
	"fs.azure.sas.token.provider.type.<storage_account>.dfs.core.windows.net",
	"org.apache.hadoop.fs.azurefs.sas.FixedSASTokenProvider")
spark.conf.set(
	"fs.azure.sas.fixed.token.<storage_account>.dfs.core.windows.net",
	"<token>")
```
## With Service Principal
Recommended. Better security
1. Register Azure AD (Microsoft Entra ID) Application / Service Principal and generate a secret for the Application

	Go to Azure Portal / Azure Entra Id / App Registrations
	Click on New Registration (this is called Service Principal)
		Call it whatever you want
		Click on Register
		Copy keys:
			Application ->(clientId)
			Directory -> (tenantId)
		Click on Certificates and Secrets
			Generate a client Secret
			Copy the Secret Value (not the id). ->(secretValue)
			

2. Set Spark Config with App/ Client Id, Directory/ Tenant Id & Secret

```python
service_credential = dbutils.secrets.get(scope="<secret-scope>",key="<service-credential-key>")

spark.conf.set(
	"fs.azure.account.auth.type.<storage-account>.dfs.core.windows.net", 
	"OAuth")
spark.conf.set(
	"fs.azure.account.oauth.provider.type.<storage-account>.dfs.core.windows.net",
	"org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")
	
spark.conf.set(
	"fs.azure.account.oauth2.client.id.<storage-account>.dfs.core.windows.net", 
	"<clientId>")
	
spark.conf.set(
	"fs.azure.account.oauth2.client.secret.<storage-account>.dfs.core.windows.net", 
	secretValue)
	
spark.conf.set(
	"fs.azure.account.oauth2.client.endpoint.<storage-account>.dfs.core.windows.net", 
	f"https://login.microsoftonline.com/{<tenantId}/oauth2/token")
```

4. Assign Role __Storage Blob Data Contributor__ to the Data Lake
Go to the storage account / Access control (IAM) / Add Role Assignment
Add the role of 'Storage Blob Data Contributor' to the Service Principal you created before.

## With Microsoft Entra ID (AAD) Credential Passthrough
This is the only authentication that is defined for individual users. All the others provide access to whoever has the keys

1. Go to the cluster configuration and check the box "Azure Data Lake Storage credential passthrough" (I can't do that)
2. Go to the storage account/ Access Control (IAM)
	1. Add the role "Blob Storage Contributor" to yourself

Then you can just access the resource without using keys:
```python
diplay(dbutils.fs.ls("abfss://demo@formula1dl.dfs.core.windows.net"))
```