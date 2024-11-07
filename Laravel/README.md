# Configuração do Docker para Projetos Laravel

Este guia oferece um passo a passo para configurar um ambiente de desenvolvimento Laravel utilizando Docker.

## Pré-requisitos

- Certifique-se de ter o [Docker](https://www.docker.com/get-started) e o [Docker Compose](https://docs.docker.com/compose/) instalados.

## Passo a Passo

### 1. Clone os Repositórios e Configure o Projeto

```sh
git clone https://github.com/pansiere/docker-laravel.git setup-docker-laravel && \
git clone https://github.com/laravel/laravel.git docker-laravel && \
rm docker-laravel/.env && \
rm docker-laravel/.env.example && \
cp -rf setup-docker-laravel/* docker-laravel/ && \
cp -rf setup-docker-laravel/.env.example docker-laravel/
rm -rf setup-docker-laravel && \
cd docker-laravel/ && \
cp .env.example .env && \
rm -rf .github
rm -rf .git
```

### 2. Atualize as Variáveis de Ambiente

Edite o arquivo `.env` e defina as seguintes variáveis:

```ini
APP_NAME="Laravel"
APP_URL=http://localhost:8000

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=password
```

### 3. Inicie os Containers do Projeto

```sh
docker-compose up -d
```

### 4. Acesse o Container

```sh
docker exec -it php /bin/bash
```

### 5. Instale as Dependências do Projeto

```sh
composer install
```

### 6. Gere a Key do Projeto Laravel

```sh
php artisan key:generate
```

### 7. Rode as Migrações do Banco de Dados

```sh
php artisan migrate
```

### 8. Acesse o Projeto

Abra seu navegador e vá para: [http://localhost:8000](http://localhost:8000)

---

Seu ambiente Laravel com Docker está configurado! Se tiver problemas, consulte a documentação oficial do Laravel ou do Docker.