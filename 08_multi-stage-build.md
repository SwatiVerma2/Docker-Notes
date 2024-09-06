# Caching

- Docker caching is a feature that helps speed up the build process by reusing layers that haven't changed. 
- When Docker builds an image, it breaks the build process into multiple steps or layers, and it caches the results of each layer. 
- If Docker detects that a layer hasn't changed between builds, it will use the cached version of that layer instead of rebuilding it, which saves time and computational resources.

### How Docker Caching Works ?
1. Layered Architecture:
- Docker images are built in layers. Each command in a Dockerfile (like RUN, COPY, ADD) creates a new layer.
- Layers are stacked on top of one another, and Docker can cache these layers for faster builds.

2. Cache Reuse:
- If Docker determines that a particular layer hasn't changed, it can reuse that cached layer.
- For example, if you have a COPY command that copies files into the container, and those files haven't changed, Docker will skip rebuilding this layer and use the cached version.

3. Invalidation of Cache:
- Docker’s caching is sequential, meaning each layer depends on the previous layer.
- If a layer in the middle of the Dockerfile changes (e.g., a RUN or COPY command), Docker will invalidate the cache for that layer and every layer after it.
- This forces Docker to rebuild the entire image from that point onward.

### Example

```dockerfile
  FROM ubuntu:latest
  COPY ./app /app
  RUN apt-get update && apt-get install -y python3
  CMD ["python3", "/app/run.py"]

```

- On the first build, Docker will create layers for each command.
- On subsequent builds, if nothing changes, Docker will reuse the cached layers.
- If you modify the COPY ./app /app command (like by updating files in the /app directory), Docker will invalidate the cache starting from the COPY command. This means both the RUN command and the CMD command layers will be rebuilt, even though they haven't changed.

### Optimizing Cache Usage: 

To optimize the use of Docker caching and avoid unnecessary rebuilds:

- Place commands that change less frequently (like RUN apt-get update) early in the Dockerfile.
- Place frequently changing commands (like COPY for application code) later in the Dockerfile.
- This way, changes to your code won't invalidate earlier cached layers (e.g., installing dependencies) and only rebuild the necessary parts.
  
# Docker Multi-Stage Builds
Docker Multi-Stage Builds is a technique used to optimize Docker images by using multiple FROM instructions in a single Dockerfile. This allows you to separate the build environment from the runtime environment, resulting in smaller, more efficient images.

Example

```dockerfile
# Stage 1: Build the application
FROM node:14 AS builder

# Set the working directory
WORKDIR /app

# Install dependencies
COPY package*.json ./

RUN npm install

# Copy application source code
COPY . .

# Build the application
RUN npm run build

# Stage 2: Create the final image
FROM nginx:alpine

# Copy built application files from the builder stage
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Command to run the application
CMD ["nginx", "-g", "daemon off;"]
```

Why Use Multistage Builds?
- Smaller Images: By only copying the final artifacts needed for your application to run, you avoid including unnecessary build tools and dependencies in the final image.
- Improved Security: Smaller images have a reduced attack surface, as they contain fewer packages that could potentially have vulnerabilities.
- Separation of Concerns: You can separate the build environment from the runtime environment, making your Dockerfile cleaner and easier to manage

Key Concepts of Multi-Stage Builds
- Multiple FROM Instructions: Each FROM instruction starts a new stage in the build process. You can use different base images for different stages.
- Named Stages: You can give names to stages using the AS keyword, making it easier to refer to specific stages later in the Dockerfile.
- Copying Artifacts: You can copy artifacts (files, binaries) from one stage to another using the COPY instruction with a specific build stage.
- Minimizing Final Image Size: By only copying the necessary artifacts into the final stage, you avoid including development tools, dependencies, and files that are not needed in the final image.
