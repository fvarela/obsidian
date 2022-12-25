## For a rabbitmq server:
  `docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.10-management`  

Then you can access it from:  
  http://localhost:15672/


### General usage (python):
### Create a 'Dockerfile' in the root of your project  
The DockerFile would look like this:  

```
FROM python:3.8.5-alpine  
WORKDIR /app  
ADD . /app  
RUN pip install -r requirements.txt  
CMD ["python","app.py"]
```  

### Build the docker image with:  
  `docker build -t python-test .`  
where:  
  `-t`  indicates the name of the image  
  `.`   indicates all  

### Check your images with:  
  `docker images`  

### Run the image with:  
  `docker run -it --name python-container -p 3200:3200 python-test`  
where:  
  `-it`   run it from the console  
  `3200`  is the port you are using  

### Run in the background with:  
  `docker run -d --name python-container -p 3200:3200 pyhton-test`  

### Check which containers are running:  
  `docker ps`  

### Check which container have run in the past:
  `docker ps -a`  

### Remove the image with 
  `docker rm [container_id]`  