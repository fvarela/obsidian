Components:
	Web server
	Scheduler
	Metastore - Database where metadata is stored
	Executor - How your task is executed
	Worker - Process executing the task

DAG - Directed Acyclic Graph
	In Airflow pipelines are defined in DAGS

Operator
	Tasks in DAGs
	Types:
		Action operators
			Python operator
			Bash operator
		Transfer operators
			To move data
		Sensor operators
			Wait for something to happen before moving to the same task
	'Task instance' is an operator running

Airflow is not a data streaming solution or a data processing framework
Airflow is an orchestrator

Single node
	That node has:
		Web Server
		Metastore
		Scheduler
		Executor . Queue
	
Multi node -> Celery (way to process your tasks on multiple different machines)
	One node has:
		Web server
		Scheduler
		Executor
	Another one has:
		Metastore
		Queue 
			This time is external to the executor)
			Based on redis or RabbitMQ
			Spread your tasks on different machines
	Then many other 'Workder Nodes' have:
		Airflow Worker


Installation:
	docker run -it --rm -p 8080:8080 python:3.8-slim /bin/bash

Create users:
	Help: airflow -users create -h
	Example: airflow users create -u admin -f admin -l admin -r Admin -e admin@airflow.com -p admin

Parameters
	`start_date` Date from which tasks of your DAG can be scheduled and triggered
	`schedule_interval` The interval of time from the min(start_date) at which your DAG shoud be triggered
	`end_date` Data at which your DAG will not be scheduled anymore
	
The DAG [X] starts being scheduled from the start_date and will be triggered after every schedule_interval
The first run of the DAG is start_date + schedule_interval

![[Pasted image 20230207212235.png]]

	