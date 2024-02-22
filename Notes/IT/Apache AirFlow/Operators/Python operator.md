
### Old way. PythonOperator instance
```
from airflow.operators.python import PythonOperator

def download_rates():
	pass

with DAG("forex_data_pipeline", default_args=default_args,
    start_date=datetime(2021, 1, 1), schedule_interval="@daily", catchup=False) as dag:
    
    do_python_stuff = PythonOperator(
        task_id = "do_python_stuff",
        python_callable = download_rates,
        op_kwargs={}
        op_args=[]
    )
```


### Passing parameters to the python function:

In Airflow -> Admin -> Variables create individual variables:

![[Pasted image 20230204153415.png]]

Then access the variables in your code like this:

```
def download_rates(file_name, path):
	print(f"This is the filename: {file_name}. This is the path: {path}")
(...)	
    do_python_stuff = PythonOperator(
        task_id = "do_python_stuff",
        python_callable = download_rates,
        op_kwargs={'file_name': '{{ var.value.file_name }}', 'path': '{{ var.value.path}}'}
        op_args=[]     

```

In Airflow -> Admin -> Variables encapsulate related variables in a dictionary:

![[Pasted image 20230204152843.png]]

Then use the `op_kwargs` like this:

```
from airflow.models import Variable
(...)

def download_rates(file_name, path):
	print(f"This is the filename: {file_name}. This is the path: {path}")
(...)	
    do_python_stuff = PythonOperator(
        task_id = "do_python_stuff",
        python_callable = download_rates,
        op_kwargs=Variable.get("my_dag_settings", deserialize_json==True)
        op_args=[]
        
```

### Accessing the context variables
Add `**context` at the end of your python function parameters:
```
def download_rates(file_name, path, **context):
	pass
```
	

## New way. Using the task decorator

```
from airflow.decorators import task
from airflow.models import Variable

@task(task_id="do_python_stuff")
def download_rates(params):
	print(f"File name: {parameters.get('file_name')}. Path: {parameters.get('path')}")

with DAG("forex_data_pipeline", default_args=default_args,
    start_date=datetime(2021, 1, 1), schedule_interval="@daily", catchup=False) as dag:
    
	download_rates(Variable.get("my_dag_settings", deserialize_json==True))
```

