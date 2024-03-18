By mounting a file storage you abstract away the used driver (ABFS or WASBS etc) and use only DBFS (Databricks File System). When accessing data. DBFS handles the interaction with ABFS or WASBS services behind the scenes, simplifying the user experience
Provide the credentials to mount the storage. When it is mounted everybody with access to the Databricks workspace will have access to it. Recommended solution for accessing the Azure Storage until the introduction of Unity Catalog!

### Mount a volume to DBFS
* Access the Azure DataLake in any of the way seen before
	* Note that abfss requires oauth authentication (Service Principal)
- Run this:
```python

config = {
"fs.azure.account.auth.type": "OAuth",
....
}

dbutils.fs.mount(
	source = "abfss://demo@formula1dl.dfs.core.windows.net/",
	mount_point = "/mnt/<mount-name>",
	extra_configs = config
)
```
### Unmount a volume:
`dbutils.fs.unmount('/mnt/python-libraries')`

### List all the available mounts
`dbutils.fs.mounts()`


### Snippet

```python
def mount_adls(storage_account_name, container_name, auth_type):  
  assert auth_type in ["oauth", "key"], "auth_type must be either 'oauth' or 'key'"
  account_key = dbutils.secrets.get(scope="vps-vida-keys-scope", key="formula1dl-access-key")
  if auth_type == "oauth":
    source = f"abfss://{container_name}@{storage_account_name}.dfs.core.windows.net/"
    extra_configs = {f"fs.azure.account.key.{storage_account_name}.dfs.core.windows.net":account_key}  
  else:
    source = f"wasbs://{container_name}@{storage_account_name}.blob.core.windows.net"
    extra_configs = {f"fs.azure.account.key.{storage_account_name}.blob.core.windows.net": f"{account_key}"}    

  try:
    dbutils.fs.mount(
        source = source,
        mount_point = f"/mnt/{storage_account_name}/{container_name}",
        extra_configs = extra_configs
    )
    print("Storage mounted successfully.")
  except Exception as e:
      if "already mounted" in str(e):
          print("Storage is already mounted.")
      else:
          print(f"Error mounting storage: {e}")


mount_adls('formula1dlfvv', 'processed', auth_type='key')
mount_adls('formula1dlfvv', 'raw', auth_type='key')
mount_adls('formula1dlfvv', 'presentation', auth_type='key')
mount_adls('formula1dlfvv', 'demo', auth_type='key')

```
