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
`docker network inspect <network-driver>` : which container is connected with bridge network
It is used to display detailed information about a Docker network. The output contains information about the default network named bridge. This information includes details such as the network's name, ID, driver, and configuration.

![image](https://github.com/user-attachments/assets/e48aaad7-d176-4b10-827a-04cc3cfc103b)

Docker containers (represented by circle) are attached with docker bridge network that provide them the Ip address

Eg. docker network inspect bridge

![image](https://github.com/user-attachments/assets/a4bd460d-c47c-4a80-a4f9-c50675e09048)

`docker network ls`: Which networks are locally present

![image](https://github.com/user-attachments/assets/37b8c5b9-4f58-4029-a016-99fb66f03f02)

### By default 3 networks are available : bridge, host, none

1. **Bridge network** is a type of network that allows containers connected to the same bridge network to communicate with each other. When you create a container without specifying a network, Docker automatically connects it to the default bridge network named bridge.

2. **Host Network** : It specifies that the container should use the host's network stack instead of its own isolated network stack. In this mode, the container shares the network namespace with the host, effectively giving it full access to the host's network interfaces and ports.

`docker run -it --network=host busybox` : it is connected directly to our own host machine and not the default bridge.

3. **none**: This option specifies that the container should not be attached to any Docker network. In other words, the container will not have any network connectivity to other containers or the external network. It will be isolated from all networking.
4. 
`docker run -it --network=none busybox`

### Host vs Bridge

The major difference between the host and bridge network modes lies in **how the containers' ports are mapped to the host system's ports**.

The main difference in terms of port mapping between host and bridge network modes is that in host network mode, there is **no need for explicit port mapping because the container directly uses the host's network stack**, while in bridge network mode, you **need to specify port mappings** to make the container's ports accessible from outside the container or from other containers on the same network.

## Creating Custom Networks

`docker network create -d <network-driver> <your-network-name>`
The docker network create command is used to create a new Docker network.

-d bridge: This option specifies the network driver to use when creating the network

![image](https://github.com/user-attachments/assets/949ab6c1-fc28-45f4-a3e0-7ec79c974c01)

Two different containers on the same network

![image](https://github.com/user-attachments/assets/ab4b5b89-f419-405d-9567-97f9959bb838)

You can ping the other container
By creating a custom network we allow containers to communicate with each other even without the need of an IP Address. We give the host name and it will resolve it automatically.
Also  Ip addresses might change with time. But the name remains

![image](https://github.com/user-attachments/assets/5fedc6a7-e0da-44f9-8a28-4ab6684c1e51)


![image](https://github.com/user-attachments/assets/59a41689-dc08-4b5e-a098-55ba22a2fff9)


`docker network rm <my-network>` : to remove a network

![image](https://github.com/user-attachments/assets/6f0acc60-6d63-498d-ad45-6f7f9d1d28ac)


