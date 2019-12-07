# docker-commands

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

