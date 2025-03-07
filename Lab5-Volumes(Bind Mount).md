## Bind Mount in Docker

### Task 1: Starting Docker Containers Bind Mounts
```
mkdir /home/ubuntu/share
```
```
echo 'Hello From Docker Host' > /home/ubuntu/share/index.html
```
```
docker run -it --name container1 -p 80:80 -v /home/ubuntu/share:/var/www/html ubuntu:18.04 /bin/bash
```
Note: `-v` can also be used for Volume Mounts. When we specify a path the `-v` flag takes it a a bind mount, and if we do not specify a path and just give a name, then a volume is created by that name and then mounted as a volume mount.
This can be tested by executing the below commands
```
docker run --help
docker ps
docker volume ls
docker run -it -v ct-volume1:/data nginx
docker ps
docker volume ls
docker run -it -v /home/ubuntu/data:/data nginx
docker ps
docker  volume ls
docker container inspect c5
docker ps
docker container inspect 39
```
![image](https://github.com/user-attachments/assets/f8f60764-8d17-4dab-b2b7-02c775f46faf)

```
apt-get update -y && apt-get install apache2 -y
```
```
service apache2 start
```
```
service apache2 status
```
Press: CTRL+P+Q
```
curl localhost:80
```
```
docker exec -it container1 bash
```
```
cat /var/www/html/index.html
```
```
echo 'Hello From Container1' > /var/www/html/index.html
```
```
cat /var/www/html/index.html
```
Press Ctrl+P+Q, to switch back to Host
```
curl localhost:80
```
```
docker inspect container1
```
Check for keyword `Mounts`


```
docker run -it --name container2 -v /home/ubuntu/share:/var/www/html ubuntu:18.04
```
```
echo 'Hello From Container2' > /var/www/html/index.html 
```
```
exit
```
```
docker ps -a
```
```
docker rm -vf container1 container2 
```
```
cat /home/ubuntu/share/index.html
```

### Task 2: Create a bind mount with --mount option and verify it
```
docker run -d -it --name container3 --mount type=bind,source=/home/ubuntu/share/,target=/app nginx:latest
```
```
docker inspect container3
```
```
docker exec -it container3 bash
```
```
cd app && ls
```
```
cat index.html
```
```
echo "hello from container3" > index.html
```
```
exit
```
```
cd /home/ubuntu/share/
```
```
cat index.html
```

