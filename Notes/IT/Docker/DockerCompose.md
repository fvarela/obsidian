Define and run multi-container Docker applications.
All containers inside the compose will share the same network.

Ejecutar varios contenedores creados previamente con docker compose
Tiene que tener el docker-compose.yml en la misma ruta
`docker-compose up -d --build`

Restart the containers
`docker-compose restart`

Start all the containers at once
`docker-compose up` 

Stop all the containers at once:
`docker-compose down`


