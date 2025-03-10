## Creating containers from Custom Images
### Task 1: Manual - Using commit to build a docker image
```
docker run -it --name ct1 ubuntu sh
```
```
curl
```
```
wget
```
```
tree
```
```
apt update && apt install curl wget tree -y
```
```
curl
```
```
wget
```
```
tree
```
CTRL+P+Q
```
docker image ls
```
```
docker commit ct1 ubuntu:newimage
```
```
docker image ls
```
```
docker run -it --name ct2 ubuntu:newimage
```
```
curl
```
```
wget
```
```
tree
```
CTRL+P+Q
```
docker ps 
```
Clean up
```
docker stop $(docker ps -a -q)
```
```
docker rm $(docker ps -a -q)
```
```
docker ps -a
```

### Task 2: Automation - Using Dockerfile to build docker image.
```
vi Dockerfile
```
```Dockerfile
FROM ubuntu
RUN apt update && apt install wget curl tree -y
```
```
docker build -t ubuntu:Dockerfile .    # docker build -t <image-name> <path of the Docker-file>
```
```
docker image ls
```
To check if multiple images can be built from same Dockerfile, we build another image as well
```
docker build -t ubuntu:Dockerfile1 .
```
```
docker image ls
```
```
docker run -it --name ct3 ubuntu:Dockerfile
```
