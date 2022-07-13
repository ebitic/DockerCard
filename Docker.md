# Docker

## Basic commands

Show active containers
`
docker ps
`

Show all containers
`
docker ps -a
`

Lancer un conteneur avec une image (-i for interactive)
`
docker run -it ubuntu bash  
`  
_Docker run contain this next tasks : `docker create` et `docker start`_
Stop a container
`
docker stop $id
`

Start a container
`
docker start $id
`

Delete a container
`
docker rm $id
`

# Docker images

Show images
`
docker image ls
`

Download an image
`
docker image pull ubuntu:latest
`

Delete a image
`
docker image rm $id
`

## Create image

**Dockerfile**:
```
FROM python:3.9.10-slim-buster
WORKDIR /app
COPY . /app
RUN pip install install -r requirements.txt
EXPOSE 80
ENV NOM ebitic
CMD ["python", "app.py"]
```
`
docker build -t test .
`

Create container from an image
`
docker run -p "80:80" $nomImage
`

## Create a docker-compose

**docker-compose.yml**:
```
version: "3"
services:
  monapp:
    image: test
    depends_on:
      - redis
    ports:
      - "80:80"
    networks:
      - mynetwork
    environment:
      - NOM=ebitic
  redis:
    image: redis
    ports:
      - "6379:6379"
    networks:
      - mynetwork
networks:
  mynetwork:
```
`
docker-compose up
`

Delete all objects linked with docker-compose.yml
`
docker-compose down
`

## Clean

Delete all elements from a category if it's not up
```
docker container prune
docker image prune
...
```
