
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

Libraries
	To upload a custom python wheel.