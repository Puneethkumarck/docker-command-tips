# docker-command-tips
This repo contains useful docker commands for java developers in development

```
docker -v ( displays docker version installed on the machine)
docker info ( docker information Os verison , kernal version etc)
docker COMMAND --help 
docker image ls (list docker images)
docker container ls (list docker contaniers)
docker contanier run --help

```

Run docker container
===================

```
docker container run cassandra:latest
===> cassandra:latest here refers to cassandra is the image name available in docker hub registry and latest refers to version of the        cassandra image .

docker container run -it cassandra:latest
===>  start the container interactive mode (-it refers to interactive)
      ctrl c kills the container in interactive mode.

docker container run -d cassandra:latest 
===> run the container in background

docker container stop container_id 
===> get the container id by running docker container ls / docker conatiner ls -a command

docker conatiner rm container_id 
===> (it removes the container from docker host)

docker container run -d --name my_cassandra cassandra:latest 
===> Naming the conatiner using --name parameter

docker container rm -f container_id 
===> which will stop and remove the container using single command

docker container run -it jboss/wildfly bash 
===> starting bash shell in wildfly -bash command overrides running container)

```

Run Container ports /volumes
===========================

```
Expose ports & attach volume
docker container run -d --name my_cassandra -P cassandra:latest
===> run the container using -P command which will choose random port to be accessible by localhost

docker container logs my_assandra 
===> to check the container logs

docker container run -d --name my_cassandra -p 9042:9042 cassandra:latest 
===> -p 9042:9042 which makes cassandra accessible in 9042 in localhost

docker container run -d -name my_cassnadra -p 9042:9042 -v /temp/logs:bin/logs cassandra:latest
===> here -v option to mount the volume from cassandra container to local disk

```

docker images
=============
```
FROM -> its used to refer base image .
CMD -> cmd which needs to be executed in dockerimage
docker image --help
docker image build -t <imagename> . --> to build docker image .(dot) refers context current directory.
docker history <image_name> --> to check history of the docker image     
```

