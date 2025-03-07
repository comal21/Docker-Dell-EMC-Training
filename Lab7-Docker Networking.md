## Docker Networking
### Task 1: Create containers and check the connectivity between them.
```
docker network ls
```
```
docker run -d --name ct1 alpine sleep 3600
```
```
docker run -d --name ct2 alpine sleep 3600
```
```
docker ps
```
```
docker inspect network bridge
```
```
docker exec -it ct1 sh
```
```
ping <IP address of ct2> -c 5
```
```
ping ct2
```
Press Ctrl+P+Q, to switch back to Host
```
docker exec -it ct2 sh
```
```
ping <IP address of ct1> -c 5
```
```
ping ct1
```
Press Ctrl+P+Q, to switch back to Host


### Task 2: Create a new docker bridge and check connectivity between containers of same bridge
```
docker network create ct-bridge1    # docker network create --driver bridge ct-bridge1
```
```
docker network inspect ct-bridge1
```
```
docker network ls
```
```
docker run -it --network ct-bridge1 --name=ct3 busybox
```

Press Ctrl+P+Q, to switch back to Host
```
docker run -it --network ct-bridge1 --name=ct4 busybox
```
Press Ctrl+P+Q, to switch back to Host
```
docker network inspect ct-bridge1
```
```
docker ps
```
```
docker attach ct3
```
```
ip addr
```
```
ping -c 5 ct4
```
```
ping <IP address of ct1> -c 5
```
Press Ctrl+P+Q, to switch back to Host
```
docker exec -it ct1 sh
```
```
ping <ip addr of ct3> -c 5
```
Press Ctrl+P+Q, to switch back to Host


### Task 3: Using 'Docker network connect' command create a successful connection between containers of different bridges
```
docker network ls
```
```
docker network connect ct-bridge1 ct1
```
```
docker network inspect ct-bridge1
```
```
docker exec -it ct1 sh
```
```
ping -c 5 ct3
```
Press Ctrl+P+Q, to switch back to Host
```
docker network connect bridge ct3
```
```
docker network inspect the bridge
```
Also to check the network connection to the outside world we can run the below commands
```
ping 8.8.8.8
```

### Task 4: Launch a container to host network
```
docker run -d --network host --name=ct7 nginx
```
```
docker ps -a
```
```
docker exec -it ct7 sh
```
Also to check the network connection to the outside world we can run the below commands
```
apt update
```
Download the ping utility if not already available
```
apt install inetutils-ping
```
```
ping 8.8.8.8
```
Also if you check the default port 80, the container would be accessible although we have not published the container since the default port for an nginx web-server is 80

Press Ctrl+P+Q, to switch back to Host
```
docker network inspect host
```
You can have multiple containers in the same host network only if they are not using the same port
```
docker run -d --network host python:3 sh -c "python -m http.server 3000"
```
`python -m http.server 3000` is used to start a simple HTTP server in Python


### Task 5: Launch a container to none network 
```
docker run -it --network none --name=ct11 nginx bash
```
Also to check the network connection to the outside world we can run the below commands
```
apt update
```
Download the ping utility if not already available
```
apt install inetutils-ping
```
```
ping 8.8.8.8
```
```
docker inspect ct11
```

