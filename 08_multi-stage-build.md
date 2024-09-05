# Caching
- Caching is a technique used to speed up the build process by reusing layers from previous builds.
- Docker images are built in layers, and each instruction in a Dockerfile creates a new layer. 
- If a layer hasn’t changed, Docker can use the cached version of that layer from previous builds, saving time and resources.

### How Docker Caching Works
Docker caching works by storing the layers created during the image build process. If a build step in the Dockerfile is unchanged from a previous build, Docker will use the cached layer instead of rebuilding it.

# Docker Multi-Stage Builds
Multistage builds allow you to use multiple FROM statements in a single Dockerfile to create multiple intermediate images. 
This technique is particularly useful for creating lean, production-ready images by copying only the necessary artifacts from the build stages, thereby reducing the overall image size.

Why Use Multistage Builds?

- Smaller Images: By only copying the final artifacts needed for your application to run, you avoid including unnecessary build tools and dependencies in the final image.
- Improved Security: Smaller images have a reduced attack surface, as they contain fewer packages that could potentially have vulnerabilities.
- Separation of Concerns: You can separate the build environment from the runtime environment, making your Dockerfile cleaner and easier to manage

