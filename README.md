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

docker image instruction command
================================
```
COPY --> Copy new files / directories in to container file system.

ADD --> Allows tar file auto extraction in image ADD app.tar.gz  /opt/var/myapp .
   Can download files from remote url

RUN : used for installing software package
     ex: RUN apt-get update && apt-get install -y git
         RUN /opt/jboss/wildfly/bin/add-user.sh admin Admin#007 -silent

CMD : defaults for executing container;can be overriden from CLI
      CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0" , "-bmanagement" , "0.0.0.0"]
      docker run wildfly bash
      
ENTRYPOINT : configures the container executable;can be overriden using --entrypoint from CLI
              Default value : /bin/sh -c
              
EXPOSE : network ports on which the container is listening

VOLUME :creates a mount point with the specified name

USER : sets the user name or UID to use when running the image

HEALTH CHECK : performs a healthcheck on the application inside the container

HEALTHCHECK --interval=5s --timeout=3s CMD curl --fail http://localhost:8091/pools || exit 1

******************
Sample docker image:   
FROM openjdk:jdk-alpine
COPY helloworldApp/target/helloworldApp.jar /deployments/
CMD java -jar /deployments/helloworldApp.jar
*******************

```

TAG Image
=========
```
If u build the image without specifying the tag it will be defaultly tagged as latest
docker image build .

Below command builds image with tagged as 1
docker image build -t myapp:1

Below command specify the build image with tagged as 1
docker image build -t myapp:latest

assiging the image to latest
docker image tag myapp:1 myapp:latest

docker run container myapp

pushing image to docker hub:
docker image tag myapp:1 puneethkumarck/myapp:latest
docker login
username:***************
password:***************

docker push puneethkumarck/myapp:latest

Local registry:
docker run -d -p 5000:5000 --restart always --name registry registry:2.6.0
docker image tag myapp:1 localhost:5000/puneethkumarck/myapp:latest
docker image push localhost:5000/puneethkumarck/myapp:latest

```

Docker Compose
==============

 - define and run multi container applications
 - configuration defined in one or more files
    - docker-compose.yaml (default file name)
    - docker-compose.override.yml (default)
    - multiple files specified using -f option
- single command to up and running/destroy all the application containers 
    - docker compose up
    - docker compose down
    
- docker-compose commands

```
build              Build or rebuild services
  bundle             Generate a Docker bundle from the Compose file
  config             Validate and view the Compose file
  create             Create services
  down               Stop and remove containers, networks, images, and volumes
  events             Receive real time events from containers
  exec               Execute a command in a running container
  help               Get help on a command
  images             List images
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pull service images
  push               Push service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  top                Display the running processes
  unpause            Unpause services
  up                 Create and start containers
  version            Show the Docker-Compose version information
```

- docker compose up options

```
-d                         Detached mode: Run containers in the background,
                               print new container names. Incompatible with
                               --abort-on-container-exit and --timeout.
    --no-color                 Produce monochrome output.
    --no-deps                  Don't start linked services.
    --force-recreate           Recreate containers even if their configuration
                               and image haven't changed.
                               Incompatible with --no-recreate.
    --no-recreate              If containers already exist, don't recreate them.
                               Incompatible with --force-recreate.
    --no-build                 Don't build an image, even if it's missing.
    --no-start                 Don't start the services after creating them.
    --build                    Build images before starting containers.
    --abort-on-container-exit  Stops all containers if any container was stopped.
                               Incompatible with -d.
    -t, --timeout TIMEOUT      Use this timeout in seconds for container shutdown
                               when attached or when containers are already.
                               Incompatible with -d.
                               running. (default: 10)
    --remove-orphans           Remove containers for services not
                               defined in the Compose file
    --exit-code-from SERVICE   Return the exit code of the selected service container.
                               Implies --abort-on-container-exit.
    --scale SERVICE=NUM        Scale SERVICE to NUM instances. Overrides the `scale`
                               setting in the Compose file if present.

```

- docker compose down options

```
      --rmi type              Remove images. Type must be one of:
                              'all': Remove all images used by any service.
                              'local': Remove only images that don't have a
                              custom tag set by the `image` field.
    -v, --volumes           Remove named volumes declared in the `volumes`
                            section of the Compose file and anonymous volumes
                            attached to containers.
    --remove-orphans        Remove containers for services not defined in the
                            Compose file
    -t, --timeout TIMEOUT   Specify a shutdown timeout in seconds.

```

Usefull commands
================
```
Remove all the images from docker host using single line command instruction
docker image rm -f $(docker image ls -aq)

Remove all the container running in docker host using single command line instruction
docker container rm -f $(docker container ls -aq)

```
