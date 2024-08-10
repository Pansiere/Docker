FROM ubuntu:latest

# Instalação dos pacotes necessários
RUN apt-get update && \
    apt-get install -y \
        git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Criação do usuário 'user' e configuração do ambiente
RUN useradd -m -s /bin/bash user && \
    echo "user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN apt install sudo -y

# Clonando o repositório e executando os scripts como o usuário 'user'
USER user
RUN sudo apt update && \
    sudo apt install git -y && \
    cd ~/ && \
    git clone https://github.com/Pansiere/Automations.git && \
    cd Automations/zsh && \
    sudo chmod +x setup.sh && \
    ./setup.sh && \
    cd

    WORKDIR /home/user

# Comando padrão para execução do container (se houver)
CMD ["bash"]
