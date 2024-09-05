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

-it: interactive mode terminal

-d: for detached mode

--name: to assign name to the container

### 5. To start container
`docker start <container-name>`

### 6. To go inside container
`docker attach <container-name>`

### 7. To view all the containers or To list the status of all the containers
`docker ps -a`

### 8. To list only running containers
`docker ps`

### 9. To stop containers
`docker stop <container-name>`

### 10. To delete container
`docker rm <container-name>`


