# Docker Networking

Docker networking refers to the networking capabilities and features provided by Docker to allow containers to communicate with each other and with external networks/ internet. Docker provides various networking options that allow you to control how containers connect to networks, how they communicate with each other, and how they interact with external systems.

### Network Drivers
There are several default network drivers available in Docker and some can be installed with the help of plugins, Command to see the list of containers in Docker mentioned below.
`docker network ls`

### Types of Network Drivers
- bridge: If you build a container without specifying the kind of driver, the container will only be created in the bridge network, which is the default network. 
- host: Containers will not have any IP address they will be directly created in the system network which will remove isolation between the docker host and containers. 
- none: IP addresses won’t be assigned to containers. These containments are not accessible to us from the outside or from any other container.
- overlay: overlay network will enable the connection between multiple Docker demons and make different Docker swarm services communicate with each other.
- ipvlan: Users have complete control over both IPv4 and IPv6 addressing by using the IPvlan driver.
- macvlan: macvlan driver makes it possible to assign MAC addresses to a container.

## Commands

1. It is used to display detailed information about a Docker network.
   
`docker network inspect <network-driver>` 

-  The output contains information about the nextwork. 
-  This information includes details such as the network's name, ID, driver, container attached to this network and configuration.

![image](https://github.com/user-attachments/assets/e48aaad7-d176-4b10-827a-04cc3cfc103b)

Docker containers (represented by circle) are attached with docker bridge network that provide them the Ip address

Eg. docker network inspect bridge

![image](https://github.com/user-attachments/assets/a4bd460d-c47c-4a80-a4f9-c50675e09048)

2. Lists all the networks available on your Docker host.

`docker network ls`

![image](https://github.com/user-attachments/assets/37b8c5b9-4f58-4029-a016-99fb66f03f02)

3. To start a Docker container with specific network settings.

`docker run -it --network=host busybox` or `docker run -it --network=none busybox`

## By default 3 networks are available : bridge, host, none

1. **Bridge network** is a type of network that allows containers connected to the same bridge network to communicate with each other. When you create a container without specifying a network, Docker automatically connects it to the default bridge network named bridge.

2. **Host Network** : It specifies that the container should use the host's network stack instead of its own isolated network stack. In this mode, the container shares the network namespace with the host, effectively giving it full access to the host's network interfaces and ports.

3. **none**: This option specifies that the container should not be attached to any Docker network. In other words, the container will not have any network connectivity to other containers or the external network. It will be isolated from all networking.

### Host vs Bridge

The major difference between the host and bridge network modes lies in **how the containers' ports are mapped to the host system's ports**.

The main difference in terms of port mapping between host and bridge network modes is that in host network mode, there is **no need for explicit port mapping because the container directly uses the host's network stack**, while in bridge network mode, you **need to specify port mappings** to make the container's ports accessible from outside the container or from other containers on the same network.

## Creating Custom Networks

To create a new Docker network

`docker network create -d <network-driver> <your-network-name>`

-d bridge: This option specifies the network driver to use when creating the network

![image](https://github.com/user-attachments/assets/949ab6c1-fc28-45f4-a3e0-7ec79c974c01)

### Two different containers within the same network can communicate with each other.

Example:

Two containers are running within the same network named "mern"

`docker run -it --name=container1 --network=mern busybox`

`docker run -it --name=container2 --network=mern ubuntu`

One conatiner can ping the other container - `ping container1`

![image](https://github.com/user-attachments/assets/a562d416-a0ef-444e-b7f4-54da20ffb771)

- By creating a custom network we allow containers to communicate with each other even without the need of an IP Address. 
- It automatically resolves the name.
- Also  Ip addresses might change with time but the name remains the same


 To remove a network
 
`docker network rm <my-network>`



