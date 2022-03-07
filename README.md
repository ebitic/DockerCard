# revisionDocker

## Commandes classiques

Voir les conteneurs actifs
`
docker ps
`

Voir tous les conteneurs
`
docker ps -a
`

Lancer un conteneur avec une image (-i pour interaction)
`
docker run -it ubuntu bash
`

Stopper un conteneur
`
docker stop $id
`

Start un conteneur
`
docker start $id
`

Supprimer un conteneur
`
docker rm $id
`

Lister les images
`
docker image ls
`

Télécharger une image
`
docker image pull ubuntu:latest
`

Supprimer une image
`
docker image rm $id
`

## Créer une image

Le **Dockerfile**:
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

Créer un conteneur à partir d'une image
`
docker run -p "80:80" $nomImage
`

## Créer un docker compose

Le fichier **docker-compose.yml**:
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
      - monreseau
    environment:
      - NOM=ebitic

  redis:
    image: redis
    ports:
      - "6379:6379"
    networks:
      - monreseau

networks:
  monreseau:
```
`
docker-compose up
`

Supprimer tous ce qui est lié au docker-compose.yml 
`
docker-compose down
`

## Nettoyer

Supprimer tous les éléments d'une catégories à condition qu'il ne soit pas up
```
docker container prune
docker image prune
...
```
