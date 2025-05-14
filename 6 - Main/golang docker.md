2025-03-18 11:56

Status:

Tags: [[Go Golang Learning]]
[[Programming]]

---

**Summary:**

Docker is used to package applications into their own independent and fully functional **containers** in order to ensure it can work on any devices as well as carefully defining and dependencies.

**Images** are the standalone packages that include everything needed to run with **containers** being their run time instance, isolated from their environment so capable of running in any environment.
**Docker Hub** or **azure container registry** or a number of other locations are where you can store images and applications like a

Want to go over:

- How to run docker
- How to create containers for applications
- How to run containers for applications
- How to upload containers so they can be used in azure or other simply ran on servers.
- Managing environment variables and key information

## Key Points
- Typically "1 Process per container", so as opposed to a giant container containing frontend, backend, batch processing, databases, streaming etc. So it's better to separate using ***compose***

**Docker Commands**

``` dockerfile
#View running containers

#Delete all images and containers
docker container rm -f $(docker container ls -aq)
docker image rm -f $(docker image ls -aq)
docker volume rm -f $(docker volume ls -q)

```


**Starting Docker**

You can start **Docker Desktop** or simply run `docker -d `to start docker daemon

**Building Docker File**

Usually build the docker file in the root of the application.
``` dockerfile
#FROM states that we are using the golang image as the base image
FROM golang:1.24.1 AS builder

# Set the Current Working Directory inside the container
WORKDIR /app
COPY go.mod ./

#Builds dependencies
RUN go mod download

# Download all files except those in .dockerignore
COPY . .

# Build the Go app
RUN CGO_ENABLED=0 GOOS=linux go build -o app

# Use a smaller image for the final stage
FROM alpine:latest

# Set the Current Working Directory inside the container

WORKDIR /root/
COPY --from=builder /app/app .
COPY --from=builder /app/web/dist ./web/dist
COPY --from=builder /app/web/src ./web/src
  
# Copy any config files needed

COPY --from=builder /app/.env .
COPY --from=builder /app/connections.json .

# This container exposes port 8080 to the outside world
EXPOSE 8080

# Command to run the executable

CMD ["./app"]
```


- Starts with `FROM` followed by system/language and version e.g. `FROM `

**Creating Image from docker file**

using 
```shell
#so same directory as docker file, you build it and include a tag via -t  to give a name. The '.' just confirms, the dockerfile is in this the curr dir.
docker build -t myDockerImage .
```


## Docker Compose


```bash
# start all services in a docker-compose.yaml at once 
$ docker compose up # add --detach to run in background 
# stop one service 
$ docker compose stop # e.g., database 
# restart stopped service (use start for removed services) 
$ docker compose restart 
# remove a stopped service 
$ docker compose rm # stop and remove all services 
$ docker compose down # rebuild all services 
$ docker compose build # create an ssh-like connection into a container 
$ docker compose exec -it # get the logs from all services
$ docker compose logs # extendable with
```

Writing Docker Compose file:

```yml
#Begin with services, so we define a list of services
services:
  app:
    image: hanadabd/myapp:latest
    ports:
    #Host of application:mapped to host of run container
      - "8080:8080"
    depends_on:
      db:
        condition: service_healthy
    environment:
      POSTGRES_HOST: db
      POSTGRES_PORT: 5432
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: testdb
    restart: always
   
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: testdb
    volumes:
    #Define volume postgres-data as well as direction
      - postgres-data:/data/db
    ports:
      - "5432:5432"
   
volumes:
#Define blank volume
  postgres-data:
```

##### References
----
[Docker Cheat Sheet ](https://docs.docker.com/get-started/docker_cheatsheet.pdf)
[Cheat Sheet for Docker CLI](https://raw.githubusercontent.com/sangam14/dockercheatsheets/master/dockercheatsheet8.png)

[Docker Compose](file:///C:/Users/Asus/Downloads/the-ultimate-docker-compose-cheat-sheet.pdf)