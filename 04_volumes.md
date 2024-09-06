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

- Run a container
  
  `docker run -it --name=c1 ubuntu`

   ![image](https://github.com/user-attachments/assets/b5c66956-2ba4-4f35-892c-a12537dabbec)

- Open a new terminal and Mount a volume :
   You can mount a local directory from your host machine into a container. This makes it possible for the container to access files from the host, and any changes 
   made in the container to that directory will also reflect on the host.
  
  Create a folder on your local machine
  
   `mkdir /d/test-folder`
  
  Run the container and mount the volume
  
  `docker run -it -v /d/test-folder:/home/abc ubuntu`

Explanation:

- -v /d/test-folder:/home/abc: This mounts the directory `/d/test-folder` from your local machine (host) to `/home/abc` inside the container.
- Now, the container can access the contents of /d/test-folder via /home/abc.

![image](https://github.com/user-attachments/assets/9bb18621-544a-4a71-a943-0489a06487cb)

- Data Persistence:
The mounted volume ensures data persistence. Even if the container is deleted or stopped, any data saved in the /home/abc directory within the container is stored on the host in /d/test-folder. Therefore, it remains intact on the host machine even after the container is removed.

![image](https://github.com/user-attachments/assets/7dfaae3c-ecfc-4f52-90a3-4cac1c6ddd58)
