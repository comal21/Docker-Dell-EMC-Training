## Two-Tier Architecture

Building a Dockerfile to setup an Ubuntu container with WordPress application

```
mkdir Wordpress
```
```
cd Wordpress
```
```
vi Dockerfile
```
Content of Dockerfile to paste
```Dockerfile
FROM ubuntu:20.04
MAINTAINER ADMIN "admin@cloudthat.com"
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
apt-get -q -y install apache2 \
php7.4 \
php7.4-fpm \
php7.4-mysql \
libapache2-mod-php7.4
ADD http://wordpress.org/latest.tar.gz /tmp
RUN tar xzvf /tmp/latest.tar.gz -C /tmp  \
&& cp -R /tmp/wordpress/* /var/www/html
RUN rm /var/www/html/index.html && \
chown -R www-data:www-data /var/www/html
EXPOSE 80
CMD ["/usr/sbin/apache2ctl","-D","FOREGROUND"]

#End of Dockerfile
```
You can download the above Dockerfile from S3 using - wget https://hpe-content.s3.ap-south-1.amazonaws.com/Dockerfile
```
docker build -t ct-wordpress:v1 .
```
```
docker image ls
```
```
docker network create --driver bridge ct-bridge
```
```
docker run -d --network ct-bridge --name mysql -e MYSQL_DATABASE=wordpress -e MYSQL_USER=admin -e MYSQL_PASSWORD=password -e MYSQL_ROOT_PASSWORD=password mysql:5.7
```
```
docker ps
```
```
docker run -d --name wordpress --network ct-bridge -p 80:80 ct-wordpress:v1
```
```
docker ps
```
```
docker exec -it wordpress sh
```
```
apt update && apt install iputils-ping -y
```
```
ping -c 5 mysql
```

