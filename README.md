# Meu Docker Hub :D

## Dica 1 - Limpar o cache de build do Docker

Às vezes, mesmo removendo o container e o volume, o Docker ainda pode usar cache de build para etapas específicas. Você pode limpar completamente o cache de build usando o seguinte comando:

```BASH
docker builder prune --all --force
```

Este comando remove todos os build cache, forçando o Docker a reconstruir tudo desde o início na próxima vez que você construir as imagens.


# Docker Commands Cheat Sheet

**By Dennis**  
*2-minute read*

Whether you’re just starting with Docker or already a professional, there are times when remembering the correct commands or the order of parameters can be challenging.  

To make things easier, we’ve created this Docker commands cheat sheet to share with you.  

Whenever you build your own container or need to timestamp the container you’re using, check out the free [Timestamp Service for Code and Container](#).  

---

## Top 16 Docker Commands

1. **`docker ps`** – List running containers.  
2. **`docker ps -a`** – List all containers, including stopped ones.  
3. **`docker pull`** – Download an image from Docker Hub registry.  
   - The image link is displayed on the right on Docker Hub.  
4. **`docker build`** – Build your own container based on a Dockerfile.  
   - Example: `docker build .` builds from the current directory.  
   - Example: `docker build -t "myimage:latest" .` creates and tags an image.  
5. **`docker images`** or **`docker image ls`** – Show all locally stored images.  
6. **`docker run`** – Run a Docker container based on an image.  
   - Example: `docker run myimage -it bash`.  
   - If the image is not found locally, Docker pulls it from the registry.  
7. **`docker logs`** – Display logs of a specified container.  
   - Example: `docker logs -f mycontainer` continues showing updates.  
8. **`docker volume ls`** – List volumes, commonly used to persist container data.  
9. **`docker network ls`** – List all Docker networks.  
10. **`docker network connect`** – Add a container to a network for communication by name instead of IP.  
11. **`docker rm`** – Remove containers.  
    - Example: `docker rm mycontainer` (ensure it’s not running).  
12. **`docker rmi`** – Remove images.  
    - Example: `docker rmi myimage` (ensure no container uses the image).  
13. **`docker stop`** – Stop containers.  
    - Example: `docker stop mycontainer` stops one.  
    - Example: `docker stop $(docker ps -a -q)` stops all.  
14. **`docker start`** – Start a stopped container with its last state.  
15. **`docker update`** – Update container policies.  
    - Example: `docker update --restart=no` helps with crash loops.  
16. **`docker cp`** – Copy files between a container and the host.  
    - Example: `docker cp <container_name_or_id>:/etc/file .`  

---

## Helpful Combinations

- **Kill all running containers:**  
  `docker kill $(docker ps -q)`  
- **Delete all stopped containers:**  
  `docker rm $(docker ps -a -q)`  
- **Delete all images:**  
  `docker rmi $(docker images -q)`  
- **Stop a container in a crash loop:**  
  `docker update --restart=no && docker stop <container_name>`  
- **Bash into a container:**  
  `docker exec -i -t <container_name> /bin/bash`  
  - Use `/bin/sh` if Bash is unavailable.  
- **Bash as root in a container:**  
  `docker exec -i -t -u root <container_name> /bin/bash`  

---

## Resource Usage

- **Get Docker containers with size:**  
  `docker ps -s`  
- **Get disk utilization:**  
  `docker system df`  

---

## Cleaning Up

- **Remove unused, untagged images:**  
  `docker image prune`  
- **Delete all unused images:**  
  `docker image prune -a`  
- **Clean up images older than 24 hours:**  
  `docker image prune -a --filter "until=24h"`  
- **Clean up stopped containers:**  
  `docker container prune`  

---

## Bonus Command

- **Truncate container logs:**  
  `truncate -s 0 $(docker inspect --format='' <container_name_or_id>)`  

---

Let us know if there are any commands you think are essential!  

> **Note:** Many of these commands also work with Podman instead of Docker.
```
