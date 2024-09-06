# What is a Docker file?
A Dockerfile is a text document that contains a series of instructions or commands to build a Docker image. These instructions are executed sequentially to create the final image.

### Common Instructions

1. **FROM**: The `FROM` instruction specifies the base image.
2. **RUN**: Executes commands within the container. It executes at image build time, not at the container runtime.
3. **COPY**: Copies files from the host to the container.
4. **ADD**: Copies files from the host to the container, with automatic tar extraction.
5. **WORKDIR**: Sets the working directory within the container.
6. **ENV**: Sets environment variables.
7. **ARG**: Defines the name of a parameter and its default value.
8. **EXPOSE**: Exposes ports for the container.
9. **CMD**: Sets the default command to run when the container starts. Only one `CMD` instruction is allowed per Dockerfile.
10. **ENTRYPOINT**: Sets the default executable for the container.
11. **VOLUME**: Creates a mount point for a volume.
12. **USER**: Sets the user inside the container.

## Example Dockerfile:

```Dockerfile
FROM ubuntu:latest

# Install Nginx
RUN apt-get update && apt-get install -y nginx

# Copy Nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start Nginx as the default command
CMD ["nginx", "-g", "daemon off;"]
```

# Push a Docker Image to Docker Hub

1. Log in to Docker Hub
   
   `docker login`
   
2. Tag the Image
   
   `docker tag <local-image-name>:<tag> <DockerHub-username>/<repository-name>:<tag>`
   
3.  Push the Image to Docker Hub
   
   `docker push <DockerHub-username>/<repository-name>:<tag>`

![image](https://github.com/user-attachments/assets/63b77a32-06ea-47fc-ac63-dda9a29abf9b)

## Interview Questions

Q1 Difference between COPY and ADD.

Key differences:
- Automatic extraction: ADD extracts compressed files automatically, while COPY does not.
- URL support: ADD can extract from URLs, while COPY cannot.
- Simplicity: COPY is generally simpler to use due to its straightforward functionality.

Q2 Difference between RUN and CMD.

Key differences:

- Execution timing: RUN executes during build, while CMD executes at runtime.
- Purpose: RUN modifies the image, while CMD sets the default command.
- Overridability: CMD can be overridden, while RUN cannot.

Use cases:

- RUN: Install packages, create files, configure settings, and build your application.
- CMD: Set the default command to run when the container starts, and allow users to override it.

Q3 Difference between ENTRYPOINT and CMD.

ENTRYPOINT

- Default executable: Sets the default executable that will be executed when the container starts.
- Harder to override: While it can be overridden, it's more difficult to do so compared to CMD.

CMD

- Default command: Sets the default command that will be executed when the container starts.
- Easily overridden: Can be easily overridden when running the container using the docker run command.
  
Q4 Difference between ARG and ENV.

ARG

- Build-time variable: An ARG is a build-time variable. Its value is specified when the image is built using the `docker build` command with the `--build-arg` flag.
- Not persisted in the image: The value of an ARG is not persisted in the final image.
- Used for dynamic values: Useful for passing dynamic values during the build process, such as version numbers or configuration parameters.

ENV

- Runtime variable: An ENV sets an environment variable that is persisted in the final image.
- Accessible within the container: The value of an ENV is accessible within the running container.
- Used for default values: Useful for setting default values for environment variables that may be overridden at runtime.



