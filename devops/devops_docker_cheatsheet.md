# Docker Cheat Sheet

## Docker Basics

| **Command**                    | **Description**                                                    |
|--------------------------------|--------------------------------------------------------------------|
| `docker --version`             | Check the installed Docker version.                                |
| `docker info`                  | Display system-wide information about Docker.                      |
| `docker help`                  | Get help for Docker commands.                                      |

## Working with Docker Images

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker images`                 | List all locally available Docker images.                          |
| `docker pull [image:tag]`       | Download an image from a Docker registry (e.g., Docker Hub).       |
| `docker build -t [image-name:tag] .` | Build a Docker image from a Dockerfile in the current directory. |
| `docker build -f [Dockerfile] -t [image-name:tag] .` | Build a Docker image using a specific Dockerfile. |
| `docker rmi [image:tag]`        | Remove a Docker image from the local machine.                      |
| `docker tag [image:tag] [new-tag]` | Add a new tag to an existing image.                            |

## Running Docker Containers

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker run [image:tag]`        | Run a container from an image.                                     |
| `docker run -d [image:tag]`     | Run a container in detached mode (in the background).              |
| `docker run -it [image:tag]`    | Run a container in interactive mode with a TTY (terminal).         |
| `docker run --name [container-name] [image:tag]` | Run a container with a custom name.                     |
| `docker run -p [host-port:container-port] [image:tag]` | Map a host port to a container port.           |
| `docker run -v [host-dir:container-dir] [image:tag]` | Mount a host directory as a volume in the container. |

## Managing Containers

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker ps`                     | List all running containers.                                       |
| `docker ps -a`                  | List all containers, including stopped ones.                       |
| `docker stop [container-name]`  | Stop a running container.                                          |
| `docker start [container-name]` | Start a stopped container.                                         |
| `docker restart [container-name]` | Restart a running or stopped container.                          |
| `docker rm [container-name]`    | Remove a stopped container.                                        |
| `docker rm $(docker ps -a -q)`  | Remove all stopped containers.                                     |
| `docker exec -it [container-name] /bin/bash` | Start a bash session inside a running container.         |
| `docker logs [container-name]`  | View the logs of a container.                                      |
| `docker inspect [container-name]` | View detailed information about a container.                     |

## Docker Networks

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker network ls`             | List all Docker networks.                                          |
| `docker network create [network-name]` | Create a new Docker network.                                |
| `docker network inspect [network-name]` | View detailed information about a network.                  |
| `docker network connect [network-name] [container-name]` | Connect a container to a network.       |
| `docker network disconnect [network-name] [container-name]` | Disconnect a container from a network. |

## Docker Volumes

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker volume ls`              | List all Docker volumes.                                           |
| `docker volume create [volume-name]` | Create a new Docker volume.                                   |
| `docker volume inspect [volume-name]` | View detailed information about a volume.                   |
| `docker volume rm [volume-name]` | Remove a Docker volume.                                           |
| `docker run -v [volume-name:/container-dir] [image:tag]` | Attach a volume to a container at runtime. |

## Docker Compose

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker-compose up`             | Create and start containers defined in a `docker-compose.yml` file.|
| `docker-compose up -d`          | Start containers in detached mode.                                 |
| `docker-compose down`           | Stop and remove containers, networks, and volumes defined in the file. |
| `docker-compose ps`             | List containers managed by Docker Compose.                         |
| `docker-compose build`          | Build or rebuild services defined in a `docker-compose.yml` file.  |
| `docker-compose logs`           | View logs from Docker Compose-managed containers.                  |
| `docker-compose exec [service-name] /bin/bash` | Start a bash session inside a running container managed by Compose. |

## Docker Swarm

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker swarm init`             | Initialize a new swarm.                                            |
| `docker swarm join --token [token] [manager-ip]:[port]` | Join a node to an existing swarm.         |
| `docker node ls`                | List all nodes in the swarm.                                       |
| `docker service create --name [service-name] [image:tag]` | Create a new service in the swarm.        |
| `docker service ls`             | List all services running in the swarm.                            |
| `docker service ps [service-name]` | List tasks for a service in the swarm.                         |
| `docker service scale [service-name]=[replicas]` | Scale a service to the specified number of replicas. |

## Docker Images Cleanup

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker system prune`           | Remove all unused containers, networks, images, and volumes.       |
| `docker image prune`            | Remove unused Docker images.                                       |
| `docker container prune`        | Remove all stopped containers.                                     |
| `docker volume prune`           | Remove all unused volumes.                                         |
| `docker network prune`          | Remove all unused networks.                                        |

## Docker Tips and Tricks

| **Command**                     | **Description**                                                    |
|---------------------------------|--------------------------------------------------------------------|
| `docker save -o [image.tar] [image:tag]` | Save an image to a tar file.                               |
| `docker load -i [image.tar]`    | Load an image from a tar file.                                   |
| `docker export -o [container.tar] [container-name]` | Export a container’s filesystem to a tar file. |
| `docker import -i [container.tar] [image:tag]` | Import a container's filesystem as an image.            |
| `docker commit [container-name] [new-image:tag]` | Create a new image from a container’s changes.          |
| `docker cp [container-name]:/path/to/file /host/path` | Copy files from a container to the host.           |
| `docker rename [old-name] [new-name]` | Rename a container.                                           |
| `docker stop $(docker ps -q)`   | Stop all running containers.                                      |
| `docker rm $(docker ps -a -q)`  | Remove all containers.                                            |
