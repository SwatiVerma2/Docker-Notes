# Basic Commands in Docker

### 1. To view all the images present in your local machine
`docker images`

### 2. To find out images in docker hub
`docker search <image-name>`

Eg. docker search jenkins

### 3. To download images from docker hub to local machine
`docker pull <image-name>`

Eg. docker pull jenkins

### 4. To create and run the container
`docker run -it --name <container-name> <image-name>`

`docker run -d --name <container-name> <image-name>`

Eg. docker run -it --name container1 ubuntu

- `-it`: interactive mode terminal
- `-d`: for detached mode
- `--name`: to assign name to the container

### 5. To start container
`docker start <container-name>`

### 6. To go inside container
`docker attach <container-name>`

- This command is used to attach your terminal to a running Docker container. When you execute this command, your terminal session will be merged with the container's standard input, output, and error streams.
- This means that anything you type in your terminal will be sent to the container, and any output from the container will be displayed in your terminal.

### 7. To view all the containers or To list the status of all the containers
`docker ps -a`

### 8. To list only running containers
`docker ps`

### 9. To create a container but not to start
`docker create [Options] --name <container-name> <image-name>`

Eg. docker create -d --name my_container nginx

- It is used to create a new Docker container but does not start it.
- It essentially prepares the container for running by configuring its network, storage, and other settings based on the specified image and options.

### 10. To stop containers
`docker stop <container-name>`

### 11. To delete container
`docker rm <container-name>`

To delete a container first stop it, then use this command.

### 12. To get information about docker installation
`docker info`

It is used to get information about the Docker daemon and its environment. It includes CPU, memory, network, kernel version, OS, etc.

### 13. To check whether the service has started or not.
`service docker status`

### 14. To start the docker daemon
`service docker start`

### 15. To list all docker commands
`docker --help`
