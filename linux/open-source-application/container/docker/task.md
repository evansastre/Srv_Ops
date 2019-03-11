# Task

## 1. Write a Docker file to create a Docker image which should have WordPress installed 

{% code-tabs %}
{% code-tabs-item title="Dockerfile" %}
```text
FROM wordpress:latest
LABEL name="mywordpress"
LABEL maintainer="evans"
RUN echo wordpress
#If FROM centos then RUN yum update && yum install -y wordpress

#WORKDIR /root
#WORKDIR /test

#ADD and COPY
#COPY test.sh /root/test
EXPOSE 80
EXPOSE 443
#CMD bash /root/test/test.sh

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="test.sh" %}
```text
echo Hello,Docker.WordPress.
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
#build
docker build -t evansastre/evans:wordpress .
```



## 2. Write a Docker file to create a Docker image for database Now, use Docker compose to bring up the above Docker images as containers. Database container should mount the local host's “/etc/mysql” volume into it's \(containers\) /etc/mysql directory.



{% code-tabs %}
{% code-tabs-item title="Dockerfile" %}
```text
FROM mysql:5.7
LABEL name="mysql"
LABEL maintainer="evans"
RUN echo mysql_for_wordpress
#VOLUME /etc/mysql /etc/mysql

#ADD and COPY
EXPOSE 3306
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
#build
docker build -t evansastre/evans:mysql .
```

{% code-tabs %}
{% code-tabs-item title="docker-compose.yml" %}
```text
version: '3.2'

services:
   db:
     image: evansastre/evans:mysql
     #volumes:
     # - /etc/mysql:/etc/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: evansastre/evans:wordpress
     ports:
       - "80:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
#run
docker-compose up -d
```















