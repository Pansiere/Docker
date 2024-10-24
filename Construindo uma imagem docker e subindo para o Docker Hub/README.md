# Construindo uma imagem docker e subivindo para o Docker Hub

**Sobre o Docker Hub:**

Se pensarmos no `Docker Hub` como o _repositório_ onde armazenamos e compartilhamos imagens Docker, ele pode ser comparado ao `GitHub`, que serve como um repositório para o controle de versões de código-fonte e compartilhamento de projetos de software. Ambos os serviços fornecem uma plataforma onde desenvolvedores podem armazenar, versionar e compartilhar seus projetos de software, mas enquanto o `GitHub` é focado em código-fonte e projetos de programação, o `Docker Hub` se especializa em gerenciamento de imagens Docker, facilitando o compartilhamento e distribuição de containers.

## Passo 1 - Preparar o Ambiente

**Estrutura de Arquivos:**

```BASH
/meuprojeto
│ Dockerfile
│ docker-compose.yaml
│ requirements.txt # Apenas se necessário
│ app.py # Seu script da aplicação
```

**1. Certifique-se de ter Docker instalado e configurado corretamente:**  
Certifique-se de que o Docker está instalado em sua máquina e funcionando corretamente.

Você pode confirmar isso executando:

```BASH
docker --version
```

**2. Criar um arquivo Dockerfile:**  
O Dockerfile define o ambiente, os pacotes e o comando que serão executados quando o container for iniciado. Por exemplo:

```Dockerfile
# Use uma imagem base do Python
FROM python:3.9

# Defina o diretório de trabalho
WORKDIR /app

# Copie os arquivos necessários
COPY . .

# Instale as dependências
RUN pip install -r requirements.txt

# Comando para rodar a aplicação
CMD ["python", "app.py"]
```

**3. Crie um arquivo docker-compose.yaml:**

```YAML
version: "3.9"

services:
  app:
    build: .
    container_name: app
    ports:
      - "5000:5000"
    network_mode: host
    restart: always
    tty: true
    stdin_open: true

volumes:
  app_data:
    driver: local
```

**4. Crie um arquivo requirements.txt se necessário:**  
Caso sua aplicação necessite de pacotes Python, como `Flask`, `Django` ou outros.

## Passo 2 - Criar e Fazer Login no Docker Hub

**1. Crie um repositório no Docker Hub:**

Exemplo `pansiere/ubuntu`

`pansiere` deve ser seu nick de usuario do Docker Hub, e `ubuntu` é o nome do repositório criado.

```md
pansiere/ubuntu == nick/repositório
```

**2. Faça login no Docker Hub:**

```BASH
docker login
```

**3. Substitua as credenciais quando solicitado.**

## Passo 3 - Taguear e Subir a Imagem para o Docker Hub

**1. Navegue até o diretório do projeto:**

```BASH
cd /caminho/para/o/meuprojeto
```

**2. Execute o comando para buildar a Imagem:**

```BASH
docker compose build
```

**4. Liste as imagens com o comando:**

```BASH
docker image ls
```

Exemplo de saída:

```BASH
REPOSITORY               TAG       IMAGE ID       CREATED          SIZE
pansiere/ubuntu          latest    e20332fd09d0   2 minutes ago   588MB
```

**5. Execute o comando para taguear sua Imagem:**

```BASH
docker tag e20332fd09d0 pansiere/ubuntu:latest
```

Explicação:

```BASH
docker tag [nome_da_imagem] [nome_do_repositorio]:[tag]
```

**6. Execute o comando para dar push na Imagem para o Docker Hub:**

```BASH
docker push pansiere/ubuntu:latest
```

## Passo 4 - Verifique a Imagem no Docker Hub

Confirme se a imagem foi carregada corretamente no Docker Hub

## Notas Adicionais

- **Verifique o Docker Compose:** Se você estiver usando Docker Compose, atualize o arquivo `docker-compose.yaml` e siga as etapas de build e push mencionadas anteriormente.

- **Arquivo requirements.txt:** Se sua aplicação usar pacotes Python, crie um requirements.txt com os pacotes necessários.
- **Docker Compose:** Certifique-se de que o Docker Compose e Docker estejam instalados corretamente em sua máquina.
- **Outros arquivos necessários:** Caso sua aplicação exija outros arquivos, certifique-se de incluí-los no diretório conforme necessário.

**Seguindo esse guia, você deve conseguir construir e subir sua aplicação Dockerizada com sucesso.**

Made by: João Pedro Vicente Pansiere
