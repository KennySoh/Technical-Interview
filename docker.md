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

## What is a Conatiner?
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
