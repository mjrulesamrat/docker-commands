## Container Logging

How to view the logs of a container to get vital output of your application. Also logging best practices of containerized applications.

### Create a container using the weather-app image.
```
docker container run --name nginx-demo -d -p 9090:80 nginx
```

### Show information logged by a running container:

    docker container logs [NAME]

### Show information logged by all containers participating in a service:

- will be useful only when using docker swarm

```
    docker service logs [SERVICE]
```

### Nginx Example:

Logs need to be output to `STDOUT` and `STDERR`

    RUN ln -sf /dev/stdout /var/log/nginx/access.log \
        && ln -sf /dev/stderr /var/log/nginx/error.log

### Debug a failed container deploy:

```
docker container run -d --name ghost_blog \
-e database__client=mysql \
-e database__connection__host=mysql \
-e database__connection__user=root \
-e database__connection__password=P4sSw0rd0! \
-e database__connection__database=ghost \
-p 8080:2368 \
ghost:1-alpine
```
