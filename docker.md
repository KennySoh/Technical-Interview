# Docker Cheat Sheet
```
//--- Step1) Build the docker image ---
docker build -t kenny/image1  // with tags , you call this iamge kenny/image1
docker images -a              // to see all the docker images u build 
docker image prune -a         // removes images that are not actively running-containers. 
docker prune system -a        // removes images & containers that are not actively running-containers. 

//--- Step2) Run the docker image
docker run -p 8000:8000 kenny/images

// Operational commands
docker exec -it <container-id> bash     // Entering container 
docker exec -it fmcs-backend_asterisk_1 sh
docker exec -it fmcs-backend_asterisk_1 /bin/bash

docker ps                               // show running container
docker ps -a                            // show all container
docker stop <container_id>              // stop running container
docker rm <container_id>


// Docker Compose
docker-compose up                    // will build container , if doesnt exist and run containers
docker-compose down                  // stop containers from running 
docker-compose build                 // build the images
docker-compose run web bash          // access container via docker-compose
docker kill $(docker ps -q)          // kill all running containers 
docker rm $(docker ps -a -q)                // delete all stopped containers
docker rmi $(docker images -q)       // delete all images

// Docker network 
Each Container has their own ip and the host is the gateway. 
Host: 172.17.0.1

// Docker volume 
Docker volume is so the container data can persist often used for databases

docker volume ls 
docker volume <volune> rm

// Docker-compose
services:
  postgres:
    env_file:
      - .env
    image: postgis/postgis
    ports:
      - "5432:5432"
    volumes:
      - postgres-db:/var/lib/postgresql/data
volumes:
  postgres-db:
  
  
```
# DockerFile
```
FROM ubuntu:20.04

ENV MY_ENV=noninteractive

# Installation packages for Ubuntu 20.04
RUN apt-get -y update
RUN wget http://mirrors.kernel.org/ubuntu/pool/universe/s/srtp/libsrtp0_1.4.5~20130609~dfsg-2ubuntu1_amd64.deb && apt install -y 

WORKDIR /usr/src/test/
RUN pwd && ls -l
COPY config/sorcery.conf /etc/asterisk/

EXPOSE 8080/tcp 8089/tcp
ENTRYPOINT ["/bin/bash", "-c", "service nginx start && tail -f /dev/null"]

```
# Docker-Compose File
```
version: "3.9"
services:                                     // we create 2 services , "web" & "redis"
  web:    
    build: ./web                              // This is the directory where ur docker file is located
    ports:
      - "8000:5000"                           // bind our host 8000 port to docker-container 5000 port
    extra_hosts:
      - "host.docker.internal:host-gateway"   // this make ur docker-container /etc/hosts follow ur localhost /etc/hosts ( Local dns)

  redis:
    image: "redis:alpine"

```


# Docker Tutorial 
https://www.youtube.com/watch?v=3c-iBn73dDE

## What is Docker 
***
- a way to package application with all the necessary depedencies and configurations
- Portable artifact , easily shared and moved around
- Makes development and deployment more efficient
***

## Where do contatiner live?
***
- Container repository
- Private repositories
- Public repository for DOcker ( Docker Hub )
***

## How docker helps
Before containers 
- Have to Manually install all the softwares (DB) on the operating system

After containers. 
- all package

## How we deploy
Before containers
- jar with instructions  -> developer team
- database with instructions -> operations
- OS conflicts

After conflict
- Operations and deevloper work together to package the application in a container
- No environment configuration needed on server except Docker Runtime

Just have the run a docker command to pull the image into the server

## What is a Container?
***
- LAyers of iamges
- Mostly Linux Base Image, Because small in size
- Application image ontop
***
***
- postgre:10.10 Layer- application image
- layer
- layer.
- Alpine:3.10 Layer-linux base image
***
```
--- go to docker hub----
docker ps // we can see the container running
docker run postgres:9.6 //advantage only different layer will be downloaded. 

Image -> artificat 
container -> official running image
```

## docker vs vm machine 
operating system
- application <- docker,vm
- os kernel <- vm
- hardware

## Install docker 
Before installing Docker 
- 
