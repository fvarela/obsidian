Check available rosource groups:
	az group list --output table


Create a storage account:
```
az storage account create --kind StorageV2 --resource-group VPS-Vida-Tools --location centralus --name detelethisaccountvps
```

Getting an endpoint:
```
az servicebus namespace authorization-rule keys list \
    --resource-group learn-931e3eeb-ce94-46a0-a755-7d225ed931a2 \
    --name RootManageSharedAccessKey \
    --query primaryConnectionString \
    --output tsv \
    --namespace-name myownservicebusthing
```

List available commands for 'blob':
	`az find blob`
Check azure cli version:
	`az --version`
Create a resource group:
	`az group create --name {group name} --location {azure region}`
List available resource groups:
	`az group list --output table`
Search a particular resource group:
	`az group list --query "[?name == '$RESOURCE_GROUP']"`
Create a service plan:
	`az appservice plan create --name $AZURE_APP_PLAN --resource-group $RESOURCE_GROUP --location $AZURE_REGION --sku FREE`
Create a web app:
	`az webapp create --name $AZURE_WEB_APP --resource-group $RESOURCE_GROUP --plan $AZURE_APP_PLAN`
Verify that the app was created successfully:
	`az webapp list --output table`
Get the html code from your web:
	`curl $AZURE_WEB_APP.azurewebsites.net`
Deploy code from GitHub to the web app:
	`az webapp deployment source config --name $AZURE_WEB_APP --resource-group $RESOURCE_GROUP --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration`
Restart a Virtual machine:
	`az vm restart -g MyResourceGroup - MyVM`



