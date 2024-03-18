
### Databricks CLI

La configuración de Databricks está en la carpeta de usuario y `.databricks`

Install with:
	`pip install databricks-cli`

Configure the token with:
	`databricks configure --token`

See available options:
	`databricks -h`

* Examples
Clusters:
	List available clusters and their ids:
		`databricks clusters list`
	To start a cluster:
		`databricks cluster start --cluster-id 0218-151607-hotpnnoa`

Filesystem:
	Para listar los volúmenes que hay montados en dbfs:
		`databricks fs ls dbfs:/mnt`
	Para copiar un fichero local al dbfs:
		`databricks fs cp .\file_test.txt dbfs:/mnt/extract-logs-csv/file_test.txt`

Secrets
	Just like Azure key vault. Secrets are grouped on containers called 'secrets-scopes'
	See available scopes:
		-`databricks secrets list-scopes`
	Create a scope
		-`databricks secrets create-scope --scope bookstore-dev`
	Put a secret in a scope:
		- `databricks secrets put --scope bookstore-dev --key db_password --string-value 12345`
	List the passwords in a secret scope:
		-`databricks secrets list --scope bookstore-dev`
	To read the secrets from a notebook use dbutils:
		`dbutils.secrets.help()`
	Databricks administrators have permission to manage/read/write all the secrets from a workspace.
### Databricks VSCode extension
Features:
- Synchronizes local code with Databricks:
	- It works always
- Run local code in Databricks clusters
	- It works only if cluster v>13
	- Unity Catalog is enabled.
- Debug local code in Databricks (experimental and requires full connection)
	

Documentation:
- https://docs.databricks.com/en/dev-tools/vscode-ext/index.html
Tutorial:
- https://docs.databricks.com/en/dev-tools/vscode-ext/tutorial.html


Install the extension on vs code
Configure the extension using the Azure Databricks URL and authenticate:
- Using Oauth
- Using Personal access token:
	To get the personal token click on your username on Databricks. Select configuration.

![[Pasted image 20230714181130.png]]


### Databricks Connect
Hay que instalar y configurar dos cosas:
	Databricks CLI
	Librería de python database-connect

Dabatricks CLI
	Comandos:
		`databricks auth profiles`
		`databricks auth env --profiles DEFAULT`
		`database configure list`
			List the databricks url and personal access token
		
Después en el entorno virtual de python instala:
`pip install databricks-connect`


Recibo el error de que el cluster no tiene habilitado el Unity Catalog. 
Hay que tirar por aquí:
[Create a Unity Catalog metastore - Azure Databricks | Microsoft Learn](https://learn.microsoft.com/en-us/azure/databricks/data-governance/unity-catalog/create-metastore)