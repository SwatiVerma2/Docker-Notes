# What is a Docker file?
A Dockerfile is a text document that contains a series of instructions or commands to build a Docker image. 

It specifies the base image, operating system, packages to install, files to copy, and commands to run within the container. 

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
