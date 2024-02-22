Puedes ver que imágenes hay en docker hub: https://hub.docker.com/

La idea es que no guardes nada dentro de los contenedores.

docker images
Para ver qué imágenes tienes en local

docker ps
Ver que contenedores están corriendo
-a
Ver que contenedores corrieron en el pasado

Docker run -it <docker_image>
El `it` escríbelo siempre o lo que hace es correr la imagen y cerrarla al momento
Si haces docker run y no tienes la imagen te la descarga en el momento.
Si generaste la imagen a partir de un dockerfile éste es el momento en que ejecuta el CMD
Si tiene la imagen la ejecuta en un contenedor
-d Ejecuta el contenedor en el background
-p 3000:3000 si quieres conectar el puerto 3000 tuyo al puerto 3000 del contenedor
-v /users/kbs/ejemplo:/etc/todos para mapear una carpeta local a otra remota
	También te permite modificar los ficheros (código o lo que sea) sin modificar la imagen
	Es iimportante utilizarlo si quieres que los datos persistan

Otro ejemplo:
docker run --name delta_quickstart --rm -it --entrypoint bash delta_quickstart
- `--name delta_quickstart`: This names the container `delta_quickstart`.
- `--rm`: This option automatically removes the container when it exits. It helps in cleaning up and not leaving behind stopped containers.
- `-it`: This combines two options: `-i` (interactive) keeps the standard input open, and `-t` allocates a pseudo-TTY (terminal), which is useful for interactive sessions.
- `--entrypoint bash`: This overrides the default entrypoint of the Docker image with `bash`. It means instead of running the default command, it will start a bash shell, allowing you to interactively work inside the container.
- `delta_quickstart`: This is the name of the Docker image that the container will be based on.

Essentially, this command starts an interactive bash shell inside a new container based on the `delta_quickstart` image, allowing you to execute commands inside the container and explore its environment.

Docker start <container_id>
Si ya tienes el contenedor creado. Lo ejecutas.

Docker stop <container_id>
Paras el contenedor

Docker pull
Si la quieres descargar antes puedes hacer `docker pull postgres`
Para descargar una imagen en concreto `docker pull postgres:9.6`

Docker logs <container_id o conatiner_name>
Para ver los logs que está dando tu contenedor
-f Te muestra los logs pero se queda esperando imprimiendo los logs nuevos

Docker exec
Ejecuta comandos dentro de contenedores que ya están corriendo
-it La 'i' crea una sesión interactiva y la 't' emula un terminal
Ejemplo:
	docker exect -it f2a09f7a79db sh

Docker build . -t getting-started .
Para construir una imagen a partir de un dockerfile
Con eso le das el nombre 'getting-started'
Con el . indicas que el dockerfile está en la misma ruta

docker tag
Para dar un nombre a tu contenedor en lugar del nombre genérico:
Ejemplo: `docker tag pablokbs/getting-started:v2 78b6f5560d5f`


### DockerFile
Te facilita crear imágenes configuradas acorde a tus necesidades
Llámale siempre `dockerfile`
Siempre empieza con la instancia `FROM`
Normalmente usa distribución de linux alpine porque es muy ligera
Declaras que ruta se crea y en la que vas a trabajar con `WORKDIR /app`
Copias todos los directorios de la ruta del dockerfile en /app del contenedor con `COPY . .`
Ejecuta comandos durante la creación de la imagen con run, por ejemplo `RUN yarn install --production`
Ejecuta comandos cuando arranque el contenedor con CMD, por ejemplo `CMD ["node", "/app/src/index.js"]`
Entrypoint es como cmd pero te permite pasar parámetros luego.
Indica que puertos utiliza la imagen con `EXPOSE 80` Ojo, despés tienes que linkar los puertos igual a la hora de correr la imagen.


## Docker Network
docker network create todo-app

docker run -d \
	--network todo-app --network-alias mysql \
	-v todo-mysql-data:/var/lib/mysql \
	-e MYSQL_ROOT_PASSWORD=secret \
	-e MYSQL_DATABASE=todos \
	mysql:5.7


## Docker Compose
docker-compose.yaml
Todos los servicios que arranques con un docker compose van a compartir red


