FROM php:8.3-fpm

# Define seu nome de usuario aqui, ex: Joao Pedro
ARG user=laravel
ARG uid=1000

# Instala dependencias do sistema
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

# Limpa o cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Instalar extensões do php
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd sockets

# Obtem a ultima versao do composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Cria usuario do sistema para rodar comandos Composer e Artisan 
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user

# Define o diretorio de trabalho
WORKDIR /var/www

USER $user
