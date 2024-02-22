Espera a que aparezca un fichero o carpeta en un directorio local.
Documentation: [FileSensor — Airflow Documentation (apache.org)](https://airflow.apache.org/docs/apache-airflow/stable/howto/operator/file.html#howto-operator-filesensor)



![[Pasted image 20230813001420.png]]

Ojo con la edición del path desde el portal web:

![[Pasted image 20230813001628.png]]

Test:

`docker exec -it 42941491f0ea /bin/bash`

`airflow tasks test forex_data_pipeline is_forex_currencies_file_available 2021-01-01`