FROM php:8.1-fpm-buster
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

RUN \
  apt-get update && \
  apt-get -y install unzip libzip-dev libicu-dev libonig-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  composer self-update --2 && \
  docker-php-ext-install intl pdo_mysql zip bcmath opcache && \
  pecl install xdebug-3.1.0 && \
  docker-php-ext-enable xdebug && \
  docker-php-ext-configure gd --with-freetype --with-jpeg && \
  docker-php-ext-install -j$(nproc) gd exif

# When you active Node.js, remove comment block under this line.
# RUN curl -sL https://deb.nodesource.com/setup_16.x | bash - && \
#   apt-get install -y nodejs && \
#   npm install npm@latest -g

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /work/src
