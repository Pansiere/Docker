# Running persistent ubuntu:latest in a docker container

## Quick start

```BASH
docker pull pansiere/ubuntu && \
cd /tmp && \
git clone https://github.com/pansiere/Docker && \
cd - && \
cp -r /tmp/Docker/ubuntu_p . && \
rm -rf /tmp/Docker && \
cd ubuntu_p && \
docker compose up -d
```

You can get inside the container by running:

```BASH
docker exec -it ubuntu_p /bin/zsh
```

## Image Overview

Uses Dockerfile to create an Ubuntu
image with MySQL client, Git, and sets up zsh terminal via a cloned repository.

**Dockerfile:**

```dockerfile
FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y \
        mysql-client \
        git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/Pansiere/Automations.git ~/Automations && \
    cd ~/Automations/zsh && \
    chmod +x setup.sh && \
    ./setup.sh

WORKDIR /root

CMD ["bash"]
```

**Docker Compose:**

```yaml
version: "3.9"

services:
  ubuntu:
    build: .
    image: pansiere/ubuntu
    container_name: ubuntu_p
    hostname: ubuntu_p
    privileged: true
    volumes:
      - ubuntu_p:/data
    network_mode: host
    restart: always
    tty: true
    stdin_open: true

volumes:
  ubuntu_p:
    name: ubuntu_p
    driver: local
```

This configuration creates an Ubuntu-based Docker image that installs MySQL client and Git, then sets up the zsh terminal using a cloned repository. The Docker Compose file defines a service named 'ubuntu' with specified volumes and network settings.
