FROM php:8.1-fpm

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN docker-php-ext-install pdo_mysql

RUN pecl install apcu

RUN apt-get update && \
apt-get install -y \
libzip-dev

RUN docker-php-ext-install zip
RUN docker-php-ext-enable apcu

WORKDIR /usr/src/app

COPY --chown=1000:1000 app /usr/src/app

RUN PATH=$PATH:/usr/src/app/vendor/bin:bin

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

RUN composer install --no-scripts --prefer-dist --no-interaction
