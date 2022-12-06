FROM php:8.1.5-fpm-alpine

RUN mkdir -p /var/www/html

RUN apk --no-cache add shadow && usermod -u 1000 www-data && groupmod -g 1000 www-data

RUN docker-php-ext-install pdo pdo_mysql

ADD .config/php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

ADD .config/php/conf.d/error_reporting.ini /usr/local/etc/php/conf.d/error_reporting.ini

RUN apk add --no-cache --virtual .build-deps $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && apk del -f .build-deps
