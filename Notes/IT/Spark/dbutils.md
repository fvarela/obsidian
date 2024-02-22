
### To get help on one of the methods:
```
dbutils.help()
dbutils.fs.help()
```
## Secrets
`cosmos_db_key = dbutils.secrets.get(scope="vps-vida-keys-scope", key="cosmos-db-key")`

## FS (File System):

`dbutils.fs.ls('/')`

List available folders inside 
`dbutils.fs.ls('/databricks-datasets/COVID')`

Integrate that output in code:
```
for files in dbutils.fs.ls('/databricks-datasets/COVID'):
	print(files)
```


## Notebook

Allows you to run a notebook and pass parameters to it from a different notebook
Similar to %run BUT:
	dbutils.notebook can execute asynchronously
	No shared scope. It doesn't import anything to the parent notebook.
	Better handling errors

return values:
To add a return value add this to the notebook that will be executed:
![[Pasted image 20240131102107.png]]
Then on the notebook running that one:

![[Pasted image 20240131102425.png]]

* Run notebooks concurrently. It is an option but in production you would use Azure DataFactory instead

## Widgets

List available widgets:
`dbutils.widgets.help()

### Text - widget
Use it to create key-value parameters for your notebook
Declare it like this:
![[Pasted image 20240131095928.png]]
Then a text box would appear at the top of the notebook:
![[Pasted image 20240131100047.png]]
You can read the value of whatever you put there with the variable:
`v_data_source`

If you are using dbutils.notebook.run as an orchestrator you can set up the values for the text widgets with a dictionary:

![[Pasted image 20240131100245.png]]
