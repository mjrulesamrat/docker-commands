# Docker 101

### Architecture Overview
Docker architecture:

- Client-server architecture
- Client talks to the Docker daemon
- The Docker daemon handles:
    - Building
    - Running
    - Distributing
- Both communicate using a REST API:
    - UNIX sockets
    - Network interface

The Docker daemon (`dockerd`):

- Listens for Docker API requests and manages Docker objects:
    - Images
    - Containers
    - Networks
    - Volumes

The Docker client (docker):

- Is how users interact with Docker
- Sends commands to dockerd

Docker registries:

- Stores Docker images
- Public registry such as DockerHub
- Let you run your own private registry

Docker objects:

- Images:
    - Read-only template with instructions for creating a Docker container
    - Image is based on another image
    - Create your own images
    - Use images published to a registry
    - Use a Dockerfile to build images

- Containers:
    - Runnable instance of an image
    - Connect a container to networks
    - Attach storage
    - Create a new image based on its current state
    - Isolated from other containers and the host machine

- Services:
    - Scale containers across multiple Docker daemons
    - Docker Swarm
    - Define the desired state
    - Service is load-balanced

Docker Swarm:

- Multiple Docker daemons (Master and Workers)
- The daemons all communicate using the Docker API
- Supported in Docker 1.12 and higher

### Docker Images:

- Files comprised of multiple layers
- Execute code in a Docker container
- Built from the instructions
- Use images to create an instance of a container

### Docker images and layers:

- Image are made of multiple layers.
- Each layer represents an instruction in the image’s Dockerfile.
- Each layer except, the very last one, is read-only.
- Each layer is only a set of differences from the layer before it.
- Layers are stacked on top of each other.
- Containers add new writable layers on top of the underlying layers
- All changes made to a running container is made to the Container layer

### What are containers?
- A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

### Container and layers
- Top writable layer
- All changes are stored in the writable layer
- The writable layer is deleted when the container is deleted
- The image remains unchanged

### Docker Networking demo

- Use the docker network to create the frontend network:

`docker network create frontend`

- User the docker network command to create the localhost network:

`docker network create localhost --internal`

- Create a MySQL container that is attached to the localhost network:

`docker container run -d --name database --network localhost -e MYSQL_ROOT_PASSWORD=P4ssW0rd0! mysql:5.7`

- Create an Nginx container that is attached to the localhost network:

`docker container run -d --name frontend-app --network frontend nginx:latest`

- Connect `frontend-app` to the `localhost` network:

`docker network connect localhost frontend-app`

