# Port Mapping

Port mapping in Docker is a technique used to expose ports from a Docker container to the host system or to other containers. This allows external processes to communicate with applications running inside Docker containers.
When you run a Docker container, you can specify port mappings using the -p or --publish option of the docker run command.

The syntax for port mapping is:

`docker run -d -p <host_port>:<container_port> <image_name>`

d: This flag runs the container in detached mode (in the background).

Eg. docker run -d -p 8080:80 nginx

It maps port 8080 on the host to port 80 inside the container, meaning you can access the Nginx web server via http://localhost:8080 on your machine, even though it's running on port 80 inside the container.

`docker run -it -p <host_port>:<container_port> <image_name>`

 it : interactive terminal

Q1 Difference between expose and publish

Expose:

- Purpose: Specifies ports exposed from the container to the container network for inter container communication.
- Usage: Exposes ports only within the container network (internal to Docker).
- Scope: Limited to the container network, so other containers on the same network can communicate via these ports.
- Configuration: Defined in the Dockerfile using the EXPOSE directive.
- Visibility: Ports are only visible to other containers within the same network, not to external systems or the host machine.
  
Publish:

- Purpose: Maps container ports to specific host ports for external access.
- Usage: Makes container ports available externally by mapping them to host machine ports.
- Scope: Allows access from outside the container network, enabling external systems or users to communicate with the container.
- Configuration: Defined at runtime using the -p or --publish option.
- Visibility: Ports can be accessed from the host machine and by external systems, making the container available over the internet or local network.
  
In short, **Expose** is for **internal** Docker network communication, while **Publish** allows **external access.**

Q2 Difference between docker exec and docker attach.

docker exec:

- docker exec is used to run a new command inside a running container. It doesn’t attach to the main process but runs a new process inside the container.
- Useful for tasks like opening a shell or running diagnostics.
- Example: `docker exec -it <container_name> bash` (this opens an interactive bash shell inside the running container).
- You can run multiple exec commands simultaneously.
  
docker attach:

- docker attach is used to attach your terminal to the main process of the container (the process started by CMD or ENTRYPOINT). You see the standard output (stdout) and can interact with the main process.
- Example: `docker attach container_name`
- Only one terminal can be attached to the main process at a time, and detaching from the container requires a specific key combination (Ctrl+C can stop the container).

Summary:
- `docker exec` starts a new process (e.g., shell or any command) inside a running container.
- `docker attach` attaches your terminal to the main process of a running container, allowing you to interact with it or view its logs.
 
