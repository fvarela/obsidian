
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

