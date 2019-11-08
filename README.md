# Docker Tutorial and Commands

A good tutorial and learning setup for Docker with commands and more

## Tutorial

### Install Docker

Go to the Docker Toolbox install website and download this package for your operation system

* docker-machine
* docker-compose
* docker-engine
* Kitematic (GUI)
* VirtualBox

### Check the version of docker

```bash
# Docker - Version
docker -v

# Docker Compose - Version
docker-compose -v

# Docker Machine - Version
docker-machine -v
```

### Setting Environment for Docker Machine

```bash
docker-machine env default
```

### Show all docker running systems

```bash
docker ps
```

### Show all docker machines

```bash
docker-machine ls
```

### Remove a docker machine

```bash
docker-machine rm "name"
```

### Show all docker images

```bash
docker image ls
```

### Remove a docker image

```bash
docker image rm "name"
```

### Remove all docker image

```bash
docker image rm $(docker images -q)
```

### Starting a docker container

```bash
docker start "Container"
```

### Stopping a docker container

```bash
docker stop "Container"
```

### Killing Process a docker container

```bash
docker kill "Container"
```

### Removing a docker container

```bash
docker rm "Container"
```

### Removing all docker container

```bash
docker rm $(docker ps -aq)
```

### Go to the Shell of a container

```bash
docker exec -it CONTAINER /bin/sh
```

### Show all logs of a container

```bash
docker logs -f "Container"
```

### Show all logs of a service

```bash
docker logs -f "Service"
```

### Show all input and output of a container

```bash
docker attach "Container"
```

### Show all input and output of a service

```bash
docker attach "Service"
```

### Dockerfile

The basic framework and the most important component for creating a container and executing it later.

Name: "Dockerfile"

#### [Development Environment]

```bash
FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y apache2 
RUN apt-get install -y php 
RUN apt-get install -y php-dev 
RUN apt-get install -y php-mysql 
RUN apt-get install -y libapache2-mod-php 
RUN apt-get install -y php-curl 
RUN apt-get install -y php-json 
RUN apt-get install -y php-common 
RUN apt-get install -y php-mbstring 
RUN apt-get install -y composer
RUN curl -s "https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh" | /bin/bash
RUN apt-get install -y software-properties-common
RUN apt-get install -y php 7.2-phalcon
COPY ./php.ini /etc/php/7.2/apache2/php.ini
COPY ./slc.conf /etc/apache2/sites-available/slc.conf
COPY ./apache2.conf /etc/apache2/apache2.conf
RUN rm -rfv /etc/apache2/sites-enabled/*.conf
RUN ln -s /etc/apache2/sites-available/slc.conf /etc/apache2/sites-enabled/slc.conf

CMD ["apachectl","-D","FOREGROUND"]
RUN a2enmod rewrite
EXPOSE 80
EXPOSE 443
```

# ------------------------------------------------------------------------------------

Name: "Dockerfile"

#### [Database Environment]

```bash
FROM mysql:5.7.25
ENV MYSQL_ALLOW_EMPTY_PASSWORD='yes'
EXPOSE 3306
```

### Docker Compose

Name: "docker-compose.yml"

```bash
version: '3'
services:
  devbox:
    build:
      context: ./
      dockerfile: DockerFile
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /path/of/my/local/filesystem:/path/to/mount/into/containers/filesystem
  devmysql:
    build:
      context: ./
      dockerfile: DockerFile
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: ''
      MYSQL_ALLOW_EMPTY_PASSWORD : 'yes'
    restart: always
    volumes:
      - /database/path/of/my/local/filesystem:/database/path/to/mount/into/containers/filesystem
```

### Docker Image

```bash
docker build -t "imagename"
```

### Docker Build

#### Dockerfile - Image

```bash
docker build -t "imagename"
```

#### Docker Compose - Image

```bash
docker-compose -f /path/to/docker-compose.yml/file build
```

### Docker Run

#### Dockerfile

```bash
docker run -d -p 8080:80 "imagename"
```

#### Docker Compose

```bash
docker-compose up -d "service"
```

### Docker Compose

#### Build a Service

```bash
docker-compose build
```

#### Create and start a Container

```bash
docker-compose up -d "Service"
```

#### Start a Container

```bash
docker-compose start "Service"
```

#### Stop a Container

```bash
docker-compose stop "Service"
```

#### Stop all Container

```bash
docker-compose down
```

#### Remove all Container from this stack

```bash
docker-compose rm -f
```

#### Show all logs of this Container

```bash
docker-compose logs
```

#### Show all Container and stacks

```bash
docker-compose ps
```

#### Go to the Shell of this Container / Stack

```bash
docker-compose exec "Service" /bin/sh
```

### Dockerignore

Filename: ".dockerignore"

```bash
# comment
*/temp*
*/*/temp*
temp?
```

### Docker GUI

* Kitematic

#### Alternative GUI

* Docker for Mac/Windows
* Captain
* MiniKube
* Kubernetic