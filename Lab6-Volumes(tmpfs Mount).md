### Create a container with tmpfs mount

```
docker run -d --name tmpmount --mount type=tmpfs,destination=/app nginx:latest
```
```
docker container inspect tmpmount
```
```
docker exec -it tmpmount bash
```
```
cd /app
```
```
touch demo.txt
```
```
ls
```
```
exit
```
```
docker container stop tmpmount
```
```
docker container start tmpmount
```
```
docker exec -it tmpmount bash
```
```
cd /app
```
```
ls
```
