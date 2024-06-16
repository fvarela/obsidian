1º Vete a esta ruta para conseguir un password de gmail:
https://security.google.com/settings/security/apppasswords

Genera el password
Vete a `mnt/airflow/airflow.cfg`

Edita esto:
![[Pasted image 20230814210549.png]]

Después tienes que reiniciar airflow con:
`docker-compose restart airflow`

El operador en sí:
