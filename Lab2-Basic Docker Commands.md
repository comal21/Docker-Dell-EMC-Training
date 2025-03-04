## Basic Docker Commands

### Task 1: Creating your first Docker container
Pull the image from Docker Hub to the Local repo and start the container
```
docker container run hello-world  
```
### Task 2: Basic Commands to run the Container in Interactive mode
Download the image from Docker Hub to the Local repo
```
docker image pull ubuntu
```
List all the images in the local repo
```
docker image ls
```
List all running processes related to containers
```
docker ps
```
List all processes related to containers including exited or terminated
```
docker ps -a
```
Run the container in interactive mode
```
docker container run -it --name ct1 ubuntu
```
```
touch f1 f2 f3
```
```
ls
```
```
exit
```
```
docker ps -a
```
Create another container in interactive mode
```
docker container run -it --name ct2 ubuntu
```
Press Crtl+P+Q to switch the terminal to Docker Host.
```
docker ps
```
Execute commands in an active container
```
docker container exec -it ct2 /bin/sh
```
List all the processes in the container.
```
ps all  #Or ps aux
```
```
exit
```
```
docker ps
```
Attach to the running container. Note that when you attach,  the primary process is triggered but when you exec again a new process is triggered. This can be checked by using `ps all`
```
docker container attach ct2
```
```
exit
```
```
docker ps
```
```
docker ps -a
```
Run container in detach mode
```
docker container run -d --name ct4 nginx
```
```
docker ps -a
```
```
docker container exec -it ct4 /bin/bash
```
```
apt update && apt install -y wget curl
```
```
apt install procps
```
```
ps aux
```
```
exit
```
```
ps aux
```

### Task 3: Port Mapping from Docker Host to container
```
docker run -d -p 8080:80 httpd
```
```
docker ps
```
```
docker exec -it < replace container id/name > /bin/bash
```
```
exit
```
```
docker ps
```
```
docker exec -it < replace container id/name > /bin/bash
```
```
kill 1
```
```
docker ps -a
```
```
docker container stop < replace container id/name >
```
```
docker container rm < replace container id/name >
```
```
docker image ls
```
```
docker image rm < replace image id >
```
