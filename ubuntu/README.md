# Image Overview:

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
    container_name: ubuntu
    hostname: ubuntu
    privileged: true
    volumes:
      - ubuntu_data:/data
    network_mode: host
    restart: always
    tty: true
    stdin_open: true

volumes:
  ubuntu_data:
    driver: local
```

This configuration creates an Ubuntu-based Docker image that installs MySQL client and Git, then sets up the zsh terminal using a cloned repository. The Docker Compose file defines a service named 'ubuntu' with specified volumes and network settings.
