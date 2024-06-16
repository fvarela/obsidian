docker exec -it 9cc23d... /bin/bash
	Open a bash terminal in the container
airflow -h
	Get help
airflow db init
	Initialize database
airflow db reset
	Remove all metadata.
	Don't use it in production
airflow db upgrade
	Upgrade
airflow webserver
	Run the webserver
airflow scheduler
	Run the scheduler
airflow celery worker
	If you are on a machine that is a worker in the celery configuration (multiple workers)
airflow dags list
airflow dags trigger example_bash_operator -e 2021-01-01
	Trigger a dag
airflow dags list-runs -d example_bash_operator
	List the dag runs of a specific dag
airflow dags backfill -s 2021-01-01 e- 2021-01-05 --reset -dagruns
	Rerun old dags
airflow tasks list example_bash_operator
	To obtain the tasks for a dag
`airflow tasks test example_bash_operator runme_0 2021-01-01`
	To test a task. Where
		`example_bash_operator` is the DAG id
		`runme_0` is the task id
		`2021-01-01` is an arbitrary past date
	

