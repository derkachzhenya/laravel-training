FROM php:8.4-fpm-alpine

RUN apk add --no-cache \
    bash curl git unzip icu-dev oniguruma-dev libzip-dev \
    && docker-php-ext-install intl pdo_mysql mbstring zip opcache

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

RUN addgroup -g 1000 -S www && adduser -u 1000 -S www -G www
USER www
