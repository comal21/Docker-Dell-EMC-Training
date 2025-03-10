## Common Docker Hub Commands

Search for Images
```
docker search ubuntu
```

Pull an Image from Docker Hub
```
docker pull ubuntu
```

List Local Images
```
docker images
```

Create an Image (Using docker build or commit)
```
vi Dockerfile
```
```Dockerfile
FROM ubuntu
RUN apt update && apt install wget curl tree -y
```
```
docker build -t my-app:v1 .    
```
Tag the Image:
```
docker tag my-app:v1 username/my-app:v1
```

Log in to Docker Hub before pushing images to Docker Hub. You will be prompted for your Docker Hub username and password
```
docker login
```


Push the Image:
```
docker push username/my-app:v1
```

