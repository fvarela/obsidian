

```dockerfile
FROM node

# WORKDIR. All the subsequent commands will be executed in this path
WORKDIR /app 

#COPY. First your local path, second the path inside the image
COPY . /app 

RUN npm install

#DONT! Do not run a server. The dockerfile contains the instruction to crate # the image, not to run software!
#RUN node server.js

#EXPOSE Optional! Documents the port we want to export from the container.
#EXPOSE doesn't really expose anything. It just documents. When starting the container you still have to specify what ports to expose with docker run -p 80:80 your-image
EXPOSE 80

#CMD does not run when the image is created BUT when a container is started
#If you don't specify a CMD, the CMD of the base image will be executed.
CMD ["node", "server.js"]

```



