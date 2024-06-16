
## Images

- List
```bash
docker images
```

- Delete image:
```bash
docker rmi <IMAGE_ID>
```

- Delete all unused images:
```bash
docker image prune
```

- Create an image based on a DockerFile:
```bash
docker build .
```


## Containers

- List running.
```bash
docker ps
```

- List all (running and stopped)
```bash
docker ps -a
```

- Stop container
```bash
docker stop my-container
```

- Delete container
```bash
docker rm my-container
```

- Delete all stopped containers
```bash
docker container prune
```

- Run container based on prebuilt image (from https://hub.docker.com/):
```bash
docker run mongo-express
```

- Run container in interactive mode (terminal)
```bash
docker run -it node
```

- Run container exposing a port
```bash
docker run -p 3000:8000 your-image
```
