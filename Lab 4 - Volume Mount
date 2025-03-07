## Volume Mount in Docker
### Checking Volumes in Docker Area
```
cd /var/lib/docker
```
```
pwd
```
```
ls
```
```
cd volumes
```

### Task 1: Creating a new docker volume and inspecting containers
```
docker volume create ct-volume1
```
```
docker volume ls
```
```
docker volume inspect ct-volume1
```

### Task 2: Launching a Nginx container mapped to a specific docker volume and verification
```
docker run -d -p 80:80 --name=nginx-container --mount src=ct-volume1,dst=/usr/share/nginx/html nginx
```
```
docker ps
```
```
docker container inspect nginx-container
```
```
ls /var/lib/docker/volumes/ct-volume1/_data/ 
```
```
cd /var/lib/docker/volumes/ct-volume1/_data/ 
```
```
touch f1 f2 f3
```
```
vi /var/lib/docker/volumes/ct-volume1/_data/index.html
```

### Task 3: Deleting container and attaching the volume to another container

```
docker container stop nginx-container
```
```
docker container rm nginx-container
```
```
docker ps -a
```
```
docker run -it --name busybox-container1 --mount source=ct-volume1,target=/data busybox sh
```
```
ls
```
```
cd /data
```
```
ls
```
```
exit
```
```
docker stop busybox-container1
```
```
docker rm busybox-container1
```
```
docker ps -a
```
```
docker volume ls
```
```
docker volume rm ct-volume1
```
```
docker volume ls
```
