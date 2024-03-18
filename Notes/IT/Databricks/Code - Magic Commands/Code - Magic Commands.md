%lsmagic -> See a list of available magic commands.

%python -> Python

%scala -> Scala

%sql -> SQL language

%sh -> Terminal
	`%sh pwd`

%fs -> Filesystem
	`%fs	ls /databricks-database`
	`%fs ls 'dbfs:/user/hive/warehouse/employees'`
		
%md -> Markdown

%pip
This runs the pip command on all the nodes of the currently active cluster. That is why you should run this and never do `%sh pip install...` 