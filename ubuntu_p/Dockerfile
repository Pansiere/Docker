FROM ubuntu:latest

# Instalação dos pacotes necessários como root
RUN apt-get update && \
    apt-get install -y \
        git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Criação do usuário 'user' e configuração do ambiente
RUN useradd -m -s /bin/bash user && \
    echo "user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Instalação do sudo
RUN apt-get install -y sudo

# Executando comandos como usuário 'user'
USER user

# Clonando o repositório e executando os scripts como 'user'
RUN sudo apt update && \
    sudo apt install git -y && \
    cd /home/user && \
    git clone https://github.com/Pansiere/Automations.git && \
    cd Automations/zsh && \
    sudo chmod +x setup.sh && \
    ./setup.sh

# Definindo o diretório de trabalho como 'user'
WORKDIR /home/user

# Comando padrão para execução do container (se houver)
CMD ["bash"]
