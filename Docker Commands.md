Managing Containers:
```
docker run <image>: Run a container from an image.
```
```
docker ps: List running containers.
```
```
docker ps -a / docker : List all containers (running and stopped).
```
```
docker start <container>: Start a stopped container.
```
```
docker pause <container>: pause a running container.
```
```
docker unpause <container>: unpause a paused container.
```
```
docker stop <container>: Stop a running container.
```
```
docker stop$(docker ps -a -q) : Stop all containers
```
```
docker restart <container>: Restart a running container.
```
```
docker rm <container>: Remove a container.
```
```
docker rm $(docker ps -a -q) : Remove all containers
```
```
docker logs <container>: View logs of a container.
```
```
docker attach <container> : Connect to the primary shell of the container
```
```
docker exec -it <container> <shell> : Connect to the secondary shell of the container
```
```
docker inspect <container> : View details about a container
```
```
docker stats<container> : View resource consumption of the container
```
docker run options:
--name <containername>
-d : detached mode
-it : interactive terminal
-p hostport:containerpor : port mapping

-----------------------------------------------------------------------------------

Managing Images:
```
docker images / docker image ls -a : List all images.
```
```
docker pull <image>: Pull an image from a registry.
```
```
docker rmi <image>: Remove an image.
```
---------------------------------------------------------------------------------------
```
docker commit <container> <newimagename> : create an image from a container
```
---------------------------------------------------------------------------------------------

Managing Volumes:
```
docker volume ls: List Docker volumes.
```
```
docker volume create <name>: Create a Docker volume.
```
```
docker volume inspect <volume>: Inspect a volume.
```
```
docker volume rm <volume>: Remove a Docker volume.
```
```
Bind Mount: docker run -v <host-path>:<container-path> <image>
```
or
```
docker run --mount type=bind src=<pathinhost>,target=<pathincontainer> <image>
```
```
Volume: docker run --mount src=<volume name>,dst=<pathincontainer> <image>
```
```
tmpfs: docker run --mount type= tmpfs destination=<pathincontainer> <image>
```
-------------------------------------------------------------------------------------------------------
Docker Networking
```
docker network ls: List networks.
```
```
docker network inspect <network_name>: Inspect a network.
```
```
docker network create <network_name>: Create a network.
```
```
docker network connect <network_name> <container_name>: Connect a container to a network.
```
```
docker network disconnect <network_name> <container_name>: Disconnect a container from a network.
```
```
docker network rm <network_name>: Remove a network.
```
Host Network : --network host
None Network: -- network none
--------------------------------------------------------------------------------------------------------

Dockerfile Build Options:
```
FROM <image_name>:<tag>: Specifies the base image.
WORKDIR /path/to/directory: Sets the working directory inside the container.
COPY <src> <dest>: Copies files from the host to the container.
RUN <command>: Executes commands inside the container during the build.
CMD ["executable","param1","param2"]: Specifies the default command to run when the container starts.
EXPOSE <port>: Exposes a port from the container.
ENV <key> <value>: Sets environment variables in the container.
VOLUME /path/to/volume: Creates a mount point and marks it as externally mounted.
USER <username or UID>: Sets the user or UID to use when running the container.
LABEL <key>=<value>: Adds metadata to an image.
```
```
docker build -t my_image:latest .
```
-------------------------------------------------------------------------------------------------------
