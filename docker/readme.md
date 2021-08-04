
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

