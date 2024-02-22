
### Databricks CLI

La configuración de Databricks está en la carpeta de usuario y `.databricks`

Para listar los clusters y su id:
`databricks clusters list`


* Databricks File System
Para listar los volúmenes que hay montados en dbfs:
`databricks fs ls dbfs:/mnt`

Para copiar un fichero local al dbfs:
`databricks fs cp .\file_test.txt dbfs:/mnt/extract-logs-csv/file_test.txt`

### Databricks VSCode extension

Install the extension on vs code
Configure the extension using the Azure Databricks URL and a personal token
	To get the personal token click on your username on Databricks. Select configuration.

![[Pasted image 20230714181130.png]]

Cluster:
	Limitations:
		Cluster has to be > v13
		Cluster has to have Unity Catalog Enabled
			Check it here: [Create a Unity Catalog metastore - Azure Databricks | Microsoft Learn](https://learn.microsoft.com/en-us/azure/databricks/data-governance/unity-catalog/create-metastore)
			Create an 'Access Connector for Azure Databricks' in Azure
			
			
On VS CodeClick on the gear box to connect to a Cluster.

![[Pasted image 20230714180846.png]]


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