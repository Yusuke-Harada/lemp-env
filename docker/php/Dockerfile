FROM php:8-fpm

RUN apt upgrade

# Install gd
RUN apt-get update && apt-get install -y \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd

# Install zip
RUN apt-get update \
  && apt-get install -y libzip-dev \
  && docker-php-ext-install zip

# Install git
RUN apt-get update \
  && apt-get install -y git \
  && rm -rf /var/lib/apt/lists/*

# Install opcache
RUN docker-php-ext-install opcache

# Install zip and dbclient
RUN apt-get update \
  && apt-get install -y mariadb-client \
  && docker-php-ext-install pdo_mysql \
  && rm -rf /var/lib/apt/lists/*

# Install node.js and npm
RUN apt-get update \
  && apt-get install -y apt-transport-https curl software-properties-common \ 
  && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - &&\
  apt-get install -y nodejs \
  && rm -rf /var/lib/apt/lists/*

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
