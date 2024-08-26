# Docker
 Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly
# container
  A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
# Image
A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
# Dockerfile
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Docker can build images automatically by reading the instructions from a Dockerfile.
 FROM:
    The FROM instruction initializes a new build stage and sets the base image for subsequent instructions. As such, a valid Dockerfile must start with a FROM instruction. ARG is the only instruction that may precede FROM in the Dockerfile
    EG:
    ARG  CODE_VERSION=latest
    FROM base:${CODE_VERSION}
 RUN:
    The RUN instruction will execute any commands to create a new layer on top of the current image. RUN instruction allows you to install your application and packages required for it.
 CMD:
    The CMD instruction sets the command to be executed when running a container from an image. If CMD is used to provide default arguments for the ENTRYPOINT instruction, both the CMD and ENTRYPOINT instructions should be specified in the exec form.
     EG: CMD ["executable","param1","param2"]
 LABEL:
    The LABEL instruction adds metadata to an image. A LABEL is a key-value pair.
 EXPOSE:
    The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if you don't specify a protocol.
 ENV:
    The ENV instruction sets the environment variable <key> to the value <value>. This value will be in the environment for all subsequent instructions in the build stage and can be replaced inline in many as well.
    EG:  ENV MY_NAME="John Doe"
 ADD:
    The ADD instruction copies new files or directories from <src> and adds them to the filesystem of the image at the path <dest> . Files and directories can be copied from the build context, a remote URL, or a Git repository.
 COPY:
    The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the image at the path <dest>. Files and directories can be copied from the build context, build stage, named context, or an image.  
    EG:
      COPY [OPTIONS] <src> ... <dest> 
      link https://docs.docker.com/reference/dockerfile/#copy---from
      --from:           
      --chown
      --chmod
      --link
      --parents
      --exclude
 ENTRYPOINT:
    An ENTRYPOINT allows you to configure a container that will run as an executable. The term "executable" refers to a program or script that can be executed, meaning it performs a specific function or set of functions when run.It typically refers to a binary file or a script with execution permissions that performs some operation when invoked.     
 VOLUME:
    The VOLUME instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers. 
    EG:
      FROM ubuntu
      RUN mkdir /myvol
      RUN echo "hello world" > /myvol/greeting
      VOLUME /myvol
 USER:
    The USER instruction sets the user name (or UID) and optionally the user group (or GID) to use as the default user and group for the remainder of the current stage. 
 WORKDIR:
    The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile. The WORKDIR instruction can be used multiple times in a Dockerfile.
 ARG: 
    The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag. 
    
# Genarations of running Applications:
## Run directly on physical server:
* A physical server is used to run a single instance of an OS. It runs Windows, Linux or another OS and, very often, it's used to run a single application. Running and maintaining a physical server is expensive because of the various resources and components associated with it. 
Disadvantages:
 *  Scaling out requires purchasing and setting up additional physical servers, which can be time-consuming and expensive.
 * Underutilization can occur if the application doesn't use all the server's resources, leading to inefficiency.
## By using hypervisor:
 * A hypervisor is a software that you can use to run multiple virtual machines on a single physical machine. Every virtual machine has its own operating system and applications. The hypervisor allocates the underlying physical computing resources such as CPU and memory to individual virtual machines as required. 
 Disadvantages:
 * Licensing cost 
 * Additional tools for managing virtual environments (e.g., VMware vCenter, Microsoft System Center) may also require licenses, further increasing costs
## Virtualization:
 * Virtualization is technology that you can use to create virtual representations of servers, storage, networks, and other physical machines.  

## Containarization: 
  * Containerization is a software deployment process that bundles an application’s code with all the files and libraries it needs to run on any infrastructure.
  Benefits of containerization:
  * Portability
  * Scalability
  * Fault tolerance


# what is microservice
* Microservices are an architectural and organizational approach to software development where software is composed of small independent services that communicate over well-defined APIs.

# Docker image tag:
 * Docker image tags are used to identify and manage different versions of Docker images. They allow you to specify which version of an image you want to use, whether it's the latest, a specific version, or a custom tag.

# Docker Volumes: 

 * Volumes are the preferred mechanism for persisting data generated by and used by Docker containers
 a) Bind mount: A file or directory on the host computer gets mounted into a container when you use bind mount. The absolute path of the file or directory on the host computer is used as a reference.
 b) Docker volume:  Docker volume is the recommended method for storing data created and utilized by Docker containers is to use volumes. Docker manages volumes entirely, whereas bind mounts rely on the host machine’s operating system and directory structure. 
 c) Tmpfs:
 *  When you create a container with a tmpfs mount, the container can create files outside the container's writable layer. As opposed to volumes and bind mounts, a tmpfs mount is temporary, and only persisted in the host memory. When the container stops, the tmpfs mount is removed, and files written there won't be persisted.

# Docker networking:
*  Bridge: If you build a container without specifying the kind of driver, the container will only be created in the bridge network, which is the default network. Containers on a bridge network are isolated from the host system and other networks by default. 
* Host: Containers will not have any IP address they will be directly created in the system network which will remove isolation between the docker host and containers. Since the container uses the host's network interface, it can directly access the host's network interfaces, ports, and services without the need for port mapping.
* Overlay: overlay network will enable the connection between multiple Docker demons and make different Docker swarm services communicate with each other.

# Docker swarm:
* Swarm mode is an advanced feature for managing a cluster of Docker daemons.
Nodes:
* Manager Nodes: These nodes are responsible for managing the Swarm cluster, including maintaining the state, scheduling services, and orchestrating tasks. They also handle membership and voting in case of node failures.
* Worker Nodes: These nodes receive and execute tasks as assigned by the manager nodes. They do not participate in the management of the cluster

# Docker compose file:
* Docker Compose is a tool for defining and running multi-container applications. 
* Compose works in all environments; production, staging, development, testing, as well as CI workflows. It also has commands for managing the whole lifecycle of your application:
   * Start, stop, and rebuild services
   * View the status of running services
   * Stream the log output of running services
   * Run a one-off command on a service


# Commands:
* sudo usermod -aG docker <username> # Add  user to docker group
* docker info # Information about your Docker installation and environment  
* docker image ls
* docker start my-container
* docker stop my-container
* docker pause my-container
* docker unpause my-container
* docker container run --name <cont-name> <image>:<tag>
* docker stats # To know the cpu/RAM utilization
* docker container run -it containername /bin/sh
* docker commit <containername> # To create image from container
* docker container run -p 8081:80 -it ubuntu:22.04 /bin/bash
* docker container run -P -it ubuntu:22.04 /bin/bash
* docker image build -t new:1.0 . or if dockerfile is not in current directory "docker image build -t new:1.0 -f <dockerfilename>
* docker image build --build-arg "key=value" -t new:1.0 .
* docker container rm <container-id/name> or docker rm <container-id/name>
* docker container rm -f $(docker container ls -a -q) # To remove all containers
* docker image rm -f $(docker image ls -q)
* docker container run -e "TEST=hai" <image> # For environmental variables
* docker container exec <containername> <command execute in container>
* docker container run -d --mount "type=bind,source=/tmp/cont-
temp,target=/tmp" --name bind6 alpine sleep 1d # Bind mount volume
* docker volume create <volume name> # Create a volume
* docker volume inspect <volume name> # Display detailed information
* docker volume ls 
* docker volume prune <volume name>
* docker volume rm <volume name>
* docker container run --name mysql-primary -d -P --mount "source=mysql-employee-vol,target=/var/lib/mysql" -e "MYSQL_ROOT_PASSWORD=rootroot" -e "MYSQL_USER=qtdevops" -e "MYSQL_PASSWORD=qtdevops" -e "MYSQL_DATABASE=employee" mysql
* docker network create <network name> # Create a volume
* docker network create <network name> -d bridge --subnet <iprange> <nameofbridge>
* docker network inspect <network name> # Display detailed information
* docker network ls 
* docker network prune <network name>
* docker network rm <network name>
* docker network connect <Containername>
* docker network disconnect <Containername>
* docker swarm init --advertise-addr "10.2.0.6"
* docker service create --replicas 2 --name nginx-srv nginx # create a service of nginx
* docker service ls
* docker compose up -d
* docker compose up -f <filename> <filename>
* docker compose down -d
* docker service create --replicas 2 --publish mode=host,target=80,published=8080 nginx
* docker logout # logout of any other registry if logged in
* docker container logs <container name>
* docker ps -a





    

