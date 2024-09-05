# Virtualization
Virtualization is the process of creating a virtual version of a computing resource, such as a server, operating system, or storage device. This allows multiple virtual machines (VMs) to run simultaneously on a single physical machine, improving resource utilization and efficiency.

Example
- Splitting the resources : A machine that has 2 tb HDD, RAM 16GB rthat can be virtually divided into two resources having 8GB RAM and 1TB HDD.
- Adding the resources : A mobile has internal storage and SD Card. By using memory card as internal memory we can accomodate a bigger file. It's like a signle memory or virtualized memory. If you take out your memory card the file will be corrupted
  
## Scenarios and Problems Without Virtualization
Before virtualization became widespread, organizations faced significant challenges in managing their computing resources:

- Underutilization: Physical servers often had excess capacity, leading to inefficient resource allocation.
- Resource Isolation: It was difficult to isolate different applications or workloads on a single physical server, increasing the risk of conflicts and security vulnerabilities.
- Hardware Costs: Acquiring and maintaining physical servers was expensive, especially for organizations with rapidly changing workloads.
- Deployment Time: Deploying new applications or services on physical hardware was time-consuming and involved manual configuration.
- Disaster Recovery: Implementing effective disaster recovery plans was challenging due to the reliance on physical hardware.

## How Virtualization Solved These Problems
- Improved Resource Utilization: Virtualization allows multiple VMs to share the resources of a single physical server, maximizing efficiency.
- Enhanced Isolation: VMs can be isolated from each other, reducing the risk of conflicts and improving security.
- Reduced Hardware Costs: Organizations can consolidate multiple physical servers onto fewer virtual machines, saving on hardware costs.
- Faster Deployment: New applications can be deployed quickly by creating virtual machines and configuring them as needed.
- Simplified Disaster Recovery: Virtual machines can be easily backed up and restored, making disaster recovery more efficient
  
## Hypervisor and its Types

A hypervisor is a software or firmware layer that creates and manages virtual machines (VMs). It acts as a bridge between the physical hardware and the virtual machines running on top of it.

![image](https://github.com/user-attachments/assets/9eeb53de-67e1-459d-94a1-ec8a2189e7ca)

Types of Hypervisors

![image](https://github.com/user-attachments/assets/9409ba22-d97b-413d-9a0e-8ce1d78dbfb6)

Type 1 (Bare-Metal Hypervisor):

- Runs directly on the physical hardware without an underlying operating system.
- It has direct access to hardware resources.
- Provides the highest performance and security.
- Examples: VMware ESXi, KVM, XenServer

Type 2 (Hosted Hypervisor):

- Runs on top of an operating system.
- It does not have direct access to the host hardware.
- Offers flexibility but may have slightly lower performance compared to Type 1.
- Examples: VirtualBox, VMware Workstation, Parallels Desktop

## OS-level virtualization and hardware-level virtualization 
Both approaches to creating virtual environments, but they differ in terms of how the underlying system is managed and isolated. 

  1. OS-Level Virtualization
- Definition: OS-level virtualization, also known as containerization, involves creating isolated user spaces on top of the same operating system kernel. Each isolated environment (or container) shares the same OS kernel but behaves like an independent system.

- How it works: Containers use the underlying OS kernel and share its resources, but each container is isolated from others. Processes in one container cannot affect processes in another. Technologies like Docker, LXC (Linux Containers), and OpenVZ are examples of OS-level virtualization.

2. Hardware-Level Virtualization
- Definition: Hardware-level virtualization, also known as full virtualization or virtual machine (VM) virtualization, involves virtualizing the hardware resources, allowing multiple virtual machines (VMs) to run on a single physical host. Each VM runs its own operating system and has its own virtualized hardware, like CPU, memory, and storage.

- How it works: A hypervisor (also known as a virtual machine monitor) abstracts the physical hardware and allocates resources to each VM. The hypervisor can either run directly on the hardware (bare-metal) or on top of an existing OS (hosted). Examples of hypervisors are VMware ESXi, Microsoft Hyper-V, and KVM.


# What is Docker?
- Docker is an open source containerization platform designed to create, deploy and run applications. 
- Docker allows you to decouple the application software from  the underlying infrastructure.
- It provides the ability to run an application in an isolated environment called a container.
- It is written in GO language.
- It performs OS level virtualization called Containerization.

![image](https://github.com/user-attachments/assets/9f6c3416-7c43-4637-b2fe-8c2623486c2d)

## Docker's Problem Addressed

- “It works on my machine” problem: Docker provides a consistent and portable environment for applications, allowing developers to package and run their software in a self-contained manner, regardless of the underlying operating system or environment. This solves the issue of application compatibility and portability across different machines and environments.

- Dependency Hell: Docker isolates applications in containers, ensuring that each application has its own environment and dependencies, preventing conflicts.
- Environment Differences: Docker images can be built once and run consistently across different environments, eliminating the problem of variations in hardware, operating systems, and software configurations.
- Deployment Challenges: Docker simplifies the deployment process by providing a standardized unit of software (containers) that can be easily shared and run on any machine with Docker installed.
- Scaling Issues: Docker makes it easy to scale applications horizontally by running multiple containers of the same image, ensuring that applications can handle increased demand efficiently.
- Portability: Docker images can be easily shared and run on any machine with Docker installed, making it easy to move applications between different environments or cloud platforms.

Advantages

- Less expensive because it does not reqire OS liscence.
- No pre Allocation of resources as it performs OS level virtualization.
- Portability: Docker images can be easily shared and run on any machine with Docker installed, making it easy to move applications between different environments.
- Isolation: Docker isolates applications in containers, ensuring that each application has its own environment and dependencies, preventing conflicts.
- Efficiency: Docker containers are lightweight and start up quickly, making them ideal for microservices architectures.
- Scalability: Docker makes it easy to scale applications horizontally by running multiple containers of the same image, ensuring that applications can handle increased demand efficiently.
- Consistency: Docker provides a consistent environment for applications, regardless of the underlying infrastructure, making it easier to maintain and debug applications.

Disadvantages

- Not a good solution for applications that requires rich GUI.
- Difficult to manage large amount of containers.
- Limited OS Support: Containers must use the same OS kernel as the host (e.g., Linux containers on Linux).
- Security Risks: Containers share the OS kernel, leading to potential security vulnerabilities.
- Dependency on Orchestration Tools: Scaling requires additional tools like Kubernetes, adding complexity.

## Architecture of Docker

![image](https://github.com/user-attachments/assets/7721d75b-bca0-40d9-969e-35f3e62bb27c)

Here’s a brief explanation of the main Docker components:

1. **Docker Daemon**:
- Manages Docker services, including images, containers, networks, and volumes.
- Communicates with other daemons and receives API requests from the Docker client to execute actions.

2. **Docker Client**:
- The interface for users to interact with Docker.
- Sends commands like `docker build`, `docker pull`, and `docker run` to the daemon through the Docker API.
- Can communicate with multiple Docker daemons.

3. **Docker Host**:
- The machine that runs Docker containers.
- Includes the Docker daemon, images, containers, networks, and storage.

4. **Docker Registry**:
- Stores Docker images.
- Docker Hub is the default public registry, but private registries can also be configured.
- `docker pull` and `docker push` commands are used to retrieve and store images.

5. **Docker Objects**:
- **Docker Images**: Read-only templates used to create containers. They store the application and its dependencies.
- **Docker Containers**: Instances of Docker images, which can be started, stopped, and managed via CLI or API.
- **Docker Storage**: Allows containers to store data persistently, managed by storage drivers on the Docker host.
- **Docker Networking**: Provides networking capabilities for containers, allowing communication between containers or external networks. Containers can be isolated or linked to multiple networks with minimal OS resource usage.

## 1. **Docker Images**
**Definition**: Docker images are read-only templates used to create Docker containers. They contain everything needed to run an application, including the code, libraries, environment variables, and configuration files.

**Purpose**: Docker images serve as blueprints for containers. They are built in layers, allowing for reusability and efficiency, as shared layers can be cached across different images.

**Characteristics**:
  - Immutable (unchangeable once created).
  - Created using a **Dockerfile** or pulled from a registry (like Docker Hub).
  - Can be versioned, shared, and distributed.

Ways to create / access images

1. pulling image from dockerhub
2. Creating image from dockerfile
3. Creating image from existing docker container
   
## 2. **Docker Containers**
**Definition**: Docker containers are instances of Docker images. They are lightweight, portable environments that run the applications defined in the image.

**Purpose**: Containers isolate the application and its dependencies from the host system, ensuring consistent execution across different environments.

**Characteristics**:
  - Containers are **ephemeral** by default (temporary), but can be configured to persist data with volumes.
  - They can be started, stopped, moved, and deleted through Docker commands.
  - Containers share the host OS kernel but are isolated from each other in terms of processes, files, and networks.

### Key Difference:
- **Docker Image**: A blueprint or template, static and read-only.
- **Docker Container**: A live, running instance of an image that executes the application in an isolated environment.

# Interview Questions

Q1 Does container has OS or not?

Answer: A Docker container does not have a full OS. It shares the host OS kernel but can include the necessary binaries, libraries, and dependencies to run applications. The container isolates the application from the underlying host, but unlike virtual machines, containers do not have a complete OS. They rely on the host OS for low-level operations while packaging the app's environment.

Q2 On what circumstances will you loose data stored in a container?

Answer: You can lose data stored in a container under the following circumstances:
- Container Deletion: If the container is deleted (docker rm), any data stored inside the container’s writable layer will be lost.
- Container Stopping: Stopping and restarting a container can result in data loss if the data was not stored in a persistent volume.
- Ephemeral Containers: Containers are ephemeral by nature, so when they are stopped or restarted without properly mounted volumes, their internal state and data can be lost.

Q3 Can a container restarts by itself?

Answer: Yes, a Docker container can restart by itself if it is configured to do so using Docker's restart policies. These policies define how and when a container should automatically restart in the event of a failure, stop, or system reboot.
Common restart policies include:
- no: The container will not restart automatically (default).
- on-failure: The container will restart only if it exits with a failure code.
- always: The container will always restart, regardless of exit status.
- unless-stopped: The container will always restart unless explicitly stopped.

Q4 Difference between image and layer?

Docker Image:

- Definition: A Docker image is a complete package that contains everything needed to run an application, including the application code, libraries, dependencies, and environment settings. It is a read-only template used to create containers.

- Role: It serves as the blueprint for creating Docker containers.

Docker Layer:

- Definition: Layers are individual components of a Docker image. Each command in a Dockerfile (e.g., RUN, COPY) creates a new layer. These layers are stacked on top of each other to form the complete image.

- Role: Layers make Docker images more efficient by allowing shared, reusable layers between images. Changes are made by adding new layers rather than modifying existing ones, which allows for caching and faster builds.
