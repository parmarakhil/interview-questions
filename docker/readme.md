
# Docker

1. Docker is a container management service. 
2. Features of docker
    1. Docker has the ability to reduce the size of development by providing a smaller footprint of the os via container
    2. With containers, it becomes easier for teams across different units such as development, QA and operations to work seamlessly across applications
    3. You can deploy docker containers anywhere, on any physical and virtual machines and even in cloud
    4. Since docker containers are lightweight they are easily scalable
3. Components of docker
    1. Docker for Mac -> to run containers on mac
    2. Docker for linux -> to run containers on linux
    3. Docker for Windows -> to run containers on windows
    4. Docker engine -> It is used for building docker images and creating docker containers
    5. Docker hub -> this is the registry which is used to host various docker images
    6. Docker compose -> this is used to define applications using multiple docker containers
4. Images
    1. In docker, everything is based on images
    2. An image is a combination of file system and parameters
    3. To display all images installed on the system run “docker images”
    4. Tag -> this is used to logically tag images
    5. Image ID -> this is used to uniquely identify the images
    6. Created -> the number of days since the image was created
    7. Virtual size -> the size of image
    8. Download and remove image
        1. To download from docker hub “docker run <imagename>”
        2. To remove images from system “docker rmi <imageId>”
    9. To see only image id’s
        1. Docker images -q
    10. To inspect an image
        1. Docker inspect <imageName>
5. Containers
    1. Containers are instances of docker images that can be run using the docker run command
    2. The basic purpose of docker is to run containers
    3. To run docker container “docker run <imageName>”
    4. To list all running containers on machine “docker ps”
    5. To list all containers on machine “docker ps -a”
    6. To get history of all commands that were run with an image via a container 
        1. Docker history <ImageID>
    7. Commands
        1. To see the top processes within a container
            1. Docker top <containerID>
        2. To stop a running container 
            1. Docker stop <containerID>
        3. To delete a container
            1. Docker rm <containerID>
        4. To provide statistics of running container
            1. Docker stats <containerID>
        5. To attach to a running container
            1. Docker attach <containerID>
        6. To pause the processes in running container
            1. Docker pause <containerID>
        7. To unpause the processes in running container
            1. Docker unpause <containerID>
        8. To kill the processes in a running container
            1. Docker kill <containerID>
6. Docker container life cycle
    1. Created —> initial state
    2. Running —> goes into running state when docker run command is used
    3. Killed —> the kill command is used to kill an existing docker container
    4. Paused -> pause command is used to pause an existing docker container
    5. Stopped —>  stop command is used to paise an existing docker container
    6. Run command is used to put a container back from stopped state to running state
7. Traditional Virtualization
    1.  The server is the physical server that is used to host multiple virtual machines.
    2. The Host OS is the base machine such as Linux or Windows.
    3. The Hypervisor is either VMWare or Windows Hyper V that is used to host virtual machines.
    4. You would then install multiple operating systems as virtual machines on top of the existing hypervisor as Guest OS.
    5. You would then host your applications on top of each Guest OS.
8. Virtualization using docker
    1. The server is the physical server that is used to host multiple virtual machines. So this layer remains the same.
    2. The Host OS is the base machine such as Linux or Windows. So this layer remains the same.
    3. Now comes the new generation which is the Docker engine. This is used to run the operating system which earlier used to be virtual machines as Docker containers.
    4. All of the Apps now run as Docker containers.
9. Configuring docker
    1. To stop the docker daemon process
        1. Service docker stop
    2. To start docker daemon process
        1. Service docker start
10. To attach a container and exit them cleanly without destroying the container we can use “nester”
    1. This method allows one to attached to a container without exiting the container
    2. Syntax
        1. Nester -m -u -n -p -I -t <containerID> <command>
        2. -u is used to mention the Uts namespace
        3. -m is used to mention the mount namespace
        4. -n is used to mention the network namespace
        5. -p is used to mention the process namespace
        6. -i s to make the container run in interactive mode.
        7. -t is used to connect the I/O streams of the container to the host OS.
        8. containerID − This is the ID of the container.
        9. Command − This is the command to run within the container.
11. Docker files
    1. To create our own docker images we can use docker files
    2. The name of the file used should be “Dockerfile”
    3. Some points
        1. # is used to write comments
        2. Starts from FROM keyword which tells docker from which base image you want to base your image from
        3. The next command is the person who is going to maintain this image. Here you specify the MAINTAINER keyword
        4. The RUN command is used to run instructions against the image
    4. To build a docker file
        1. Docker build
        2. Docker build  -t ImageName:TagName dir
        3. -t − is to mention a tag to the image
        4. ImageName − This is the name you want to give to your image.
        5. TagName − This is the tag you want to give to your image.
        6. Dir − The directory where the Docker File is present.
    5. To tag an image to relevant repository
        1. Docker tag <ImageID> <RepositoryName>
    6. TO push images to docker hub
        1. Docker push <repositroyName>
12. Private repository
    1. Registry is the container managed by docker which can be used to host private repositories
    2. In the run command -d option is used to run the container in detached mode. This is so that the container can run in the background
    3. docker tag <ImageID> localhost:5000/<repositoryName>
    4. Here localhost:5000 is the location of private repository
    5. To push the repository to private repository
        1. docker push <privaterRepo>/<repoName> 
13. Instruction command
    1. CMD
        1. This command is used to execute a command at runtime when the container is executed.
        2. CMD command param1 
    2. ENTRYPOINT
        1. This command can also be used to execute commands at runtime for the container. But we can be more flexible with the ENTRYPOINT command
        2. ENTRYPOINT command param1
    3. ENV
        1. This command is used to set environment variables in the container.
        2. ENV key value
    4. WORKDIR
        1.  This command is used to set the working directory of the container.
        2. WORKDIR dirname
14. Storage drivers
    1. Docker has multiple storage drivers that allow one to work with the underlying storage devices
    2. AUFS
        1. It is a stable driver and can be used for production ready applications
        2. It has good memory usage and is good for ensuring a smooth docker experience for containers
        3. There is a high-write activity associated with this driver which should. Be considered
        4. Its good for systems which are of platform as a service type work
    3. Devicemapper
        1. A stable driver to ensure smooth docker experience
        2. Good for testing applications
        3. The driver is in line with the main linux kernel functionality
    4. Btrfs
        1. This driver is in line with main linux kernel functionality
        2. There is high-write activity associated with this driver which should. Be considered
        3. This driver is good for instances where you maintain multiple build pools
    5. Ovelay
        1. Stable driver, inline with main linux kernel functionality and good memory usage
        2. Good for testing applications
    6. ZFS
        1. Stable driver, good for testing applications
        2. Good for systems which are PAAS type
    7. To see the storage driver being used, use “docker info” command
15. Data volumes
    1. In docker, you have a separate volume that can be shared across containers. These are known as data volumes
    2. There are initialised when container is created
    3. They can be shared and also reused amongst many containers
    4. Any changes to volume itself can be made directly
    5. They. Exist even after the container is deleted
    6. If you want to change the storage driver used for a container, you can do so when launching the container by using “—volume-driver” parameter
    7. Creating. Volume
        1. A volume can be created before hand using docker command
        2. Docker volume create —name=volumename —opt options
    8. Listing all volumes
        1. To list all docker volumes on a docker host use “docker volume ls”
16. Networking
    1. Docker take care of networking aspects
    2. A docker ethernet adapter is created when docker is installed on docker host
    3. This is a bridge between docker host and linux host
    4. Listing all docker networks
        1. This command can be used to list all the network associated with docker on the host
        2. Docker network ls
    5. Inspecting a docker network
        1. Use “docker network inspect network name”
    6. Create own network
        1. Docker network create —driver drivername name
17. Docker toolbox
    1. Docker engine
        1. Used as the base engine or docker daemon that is used to run docker containers
    2. Docker machine
        1. For running docker machine commands
    3. Docker compose
        1. For running docker compose commands
    4. Kinematic
        1. Docker GUI built for windows and Mac OS
    5. Oracle virtualbox
18. Docker cloud
    1. Docker cloud is a service provided by docker in which you. Can carry out the following operations
    2. Nodes
        1. You can connect the docker cloud to your existing cloud providers such as Azure and AWS to spin up containers on these environments
    3. Cloud repository
        1. Provides a place where you can store your own repositories
    4. Continuous integration
        1. Connect with GitHub and build a continuous integration pipeline
    5. Application development
        1. Deploy and scale infrastructure and containers
    6. Continuous deployment
        1. Can automate deployment
19. Logging
    1. Docker provides logging at daemon level and container level
    2. Daemon logging
        1. Debug
            1. It details all the possible information handled baby the daemon process
        2. Info
            1. It details all the errors+information handled by the daemon process
        3. Errors
            1. It details all the errors handled by the daemon process
        4. Fatal
            1. It only details all fatal errors handled by daemon process
    3. Container logging
        1. Docker logs containerID
20. Docker compose
    1. Used to run multiple containers as a single service without the need to start each one separately 
    2. docker-compose version 
    3. All docker compose files are YAML files


