Con este operador puedes comprobar si un request http tiene el response adecuado.
Puedes hacerlo más complejo que un simple ping analizando el texto que da el response y parseándolo como te de la gana.

Ojo con el parámetro `http_conn_id`, es el root de la web a la que te quieres connectar. Mira el ejemplo de abajo.

Test:
	`docker exec -it b9sfg456... /bin/bash`
	`airflow tasks test my_http_sensor_test does_this_name_matters 2023-08-08`

Ejemplo.
DAG llamado `my_http_sensor_test.py`

![[Pasted image 20230812180252.png]]


El http_conn_id está configurado en el portal web en Admin/Connections:
Como mínimo hay que poner esos tres campos:
![[Pasted image 20230812180546.png]]



