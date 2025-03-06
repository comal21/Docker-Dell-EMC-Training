## Docker container life cycle

### Task 1: Docker Lifecycle 
Pull Docker Image
```
docker pull httpd
```
List all images available in Local Repo
```
docker image ls
```
Check the history of the image
```
docker image history httpd
```
Create container
```
docker container create httpd
```
List all containers
```
docker container ls -a
```
Start the created container
```
docker container start < container id/name >
```
```
docker container ls
```
Stop the created container
```
docker container stop < container id/Name >
```
```
docker container ls -a
```
```
docker container start < container id/Name >
```
Pause the container
```
docker container pause < container id/Name >
```
```
docker container ls -a
```
Unpause the container
```
docker container unpause < container id/Name >
```
```
docker container ls -a
```
```
docker exec -it < container id/name > /bin/bash
```
```
cd htdocs
```
```
apt update
```
```
apt install wget -y
```
```
rm index.html
```
```
wget https://s3.ap-south-1.amazonaws.com/files.cloudthat.training/devops/docker-essentials/index.html
```
```
exit
```
Save the container as an image 
```
docker commit < replace container id/name > myhttpd:version
```
```
docker image ls
```
Create a new container with the newly created image
```
docker run -d -p 8080:80 myhttpd:version
```
```
curl < public IP>:8080  #Public IP of your host machine
```
```
docker container ls
```
Check the logs of the container
```
docker logs < container id/name >
```
Monitor real-time resource usage for running Docker containers

docker stats         # Shows usage statistics for only running containers

docker stats -a      # Shows usage for all containers
```
docker stats < container id/name > 
```
```
docker container ls
```
```
docker stop < replace container id/name >
```
Remove a stopped container
```
docker container rm < replace container id/name > 
```
Remove a running container 
```
docker container rm < replace container id/name > -f
```
```
docker image ls
```
```
docker image rm < replace image id/name > < replace image id/name >
```
```
docker image ls
```
```
docker image ls -a
```
