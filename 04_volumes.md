# Volumes

- A Docker volume is a storage mechanism that allows Docker containers to persist data beyond the lifecycle of a container.
- Volumes are managed by Docker and can be shared between containers.
- This is especially useful for storing data that needs to survive even after the container stops, restarts, or is removed.


Key features of Docker volumes:

- They exist outside the container's filesystem, making them independent of the container's lifecycle.
- They can be shared across multiple containers.
- Docker automatically manages volumes, which simplifies handling persistent data.

## Creating volumes

### Using Dockerfile
   
- Create a Dockerfile
  
```dockerfile
FROM ubuntu
VOLUME ["/myvolume1"]
```

- Create an image
  
`docker build -t <image1-name>`

- Create a container
  
`docker run -it --name <container1-name> <image1-name>`

- Share volume with another container

`docker run -it --name <container2-name>  --privileged=true --volumes-from <container1-name> <image1-name>`

  Eg. docker run -it  --name mycontainer2 --privileged=true --volume-from mycontainer1 ubuntu

Explanation of Volume Sharing:

- When you use the --volumes-from flag, the new container (container2) will have access to the same volume as the first container (container1). 
- Any data written in the /myvolume1 directory by container1 will be accessible to container2 and vice versa.
- This is particularly useful when you want multiple containers to access the same persistent data without explicitly creating and managing external volumes.
  
2. Using CLI

`docker run -it --name <container1-name>`

Share volume

`docker run -it --name <container2-name>  --privileged=true --volumes-from <container1-name> <image1-name>`
