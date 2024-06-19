FROM ubuntu:latest

# Instalação dos pacotes necessários
RUN apt-get update && \
    apt-get install -y \
        mysql-client \
        git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Clonando o repositório e executando os scripts
RUN git clone https://github.com/Pansiere/Automations.git ~/Automations && \
    cd ~/Automations/zsh && \
    chmod +x setup.sh && \
    ./setup.sh

# Configuração final (se houver)
WORKDIR /root

# Comando padrão para execução do container (se houver)
CMD ["bash"]
