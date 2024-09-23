# Docker

## Install

https://docs.docker.com/engine/install/debian/
```bash
sudo apt install docker-io docker-compose
sudo usermod -aG docker seb
```

## Basic commands
List all docker container:
```bash
docker ps
docker ps -a
docker container ls
docker container ls -a
```

List all available images:
```bash
docker image ls
```

Stop container:
```bash
docker stop <container_name>
```

Remove container:
```bash
docker rm <container_name>
```

Enter in container:
```bash
docker exec -it <container_name> sh
```

Volume:
```bash
docker volume create <volume_name>
docker volume ls
docker volume inspect <volume_name>
```

Secret:
```bash
docker secret ls
```

Logs:
```bash
docker logs <container_name>
```

## Docker build image HA

```bash
docker pull alpine:latest
docker build --no-cache -t website:latest .
```

Or build with HA image:

```bash
docker pull ghcr.io/home-assistant/amd64-base:latest
docker build --no-cache --build-arg="BUILD_FROM=ghcr.io/home-assistant/amd64-base:latest" -t website-ha:latest .
```

Run locally to test:
```bash
docker run --mount type=bind,source="${PWD}/site",target=/data/site --name website -p 80:80 website &
docker run --mount type=bind,source="${PWD}/site",target=/data/site --name website -p 80:80 website-ha &
```


## Update docker
Generate a new image from the source:
```bash
./build_image.sh
docker stop keepass
docker rm keepass
./start_container.sh 55002 /var/log/docker/keepass/
```

Or manual method Pull latest image:
```bash
docker pull alpine:latest
docker pull ghcr.io/home-assistant/amd64-base:latest
docker stop keepass
...
```

## Docker Hub

Push image:
```bash
docker tag local-image:tagname seb9192/server:tagname
docker push seb9192/server:tagname
```
```bash
docker tag keepass:latest seb9192/server:keepass-230804
docker push seb9192/server:keepass-230804
```
