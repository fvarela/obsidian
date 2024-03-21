


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