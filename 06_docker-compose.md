# Docker Compose

- The docker-compose up command is used to start the services defined in a Docker Compose configuration file. 
- Docker Compose is a tool for defining and running multi-container Docker applications. 
- It allows you to define a multi-container application in a single file (docker-compose.yml) and manage the lifecycle of the application's services as a single unit.
- Docker Compose makes it easier to manage complex, multi-container applications, such as microservices architectures, by enabling you to start all the containers with a single command.

`docker-compose.yml`

```docker-compose
version: "3.8"

services:
  postgres:
    image: postgres # hub.docker.com
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: postgres
      POSTGRES_DB: review
      POSTGRES_PASSWORD: password

  redis:
    image: redis
    ports:
      - "6379:6379"
```

`docker compose up` or `docker compose up -d` d → detached mode (bg )

![image](https://github.com/user-attachments/assets/79d18a9c-8b35-4abf-b3db-1e189e1be67b)

![image](https://github.com/user-attachments/assets/aceb69ff-30c1-41fe-be3d-2e06cfbef211)

`docker compose down`

![image](https://github.com/user-attachments/assets/af6f36f9-d2e7-41d2-bd68-6e3eed58daf6)

Check this repo for use case:

[Docker-compose-for-MERN-App](https://github.com/SwatiVerma2/Docker-Compose-MERN)

