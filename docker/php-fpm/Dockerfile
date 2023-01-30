FROM php:8.1-fpm-alpine as base
WORKDIR /app
RUN docker-php-ext-install pdo pdo_mysql
COPY ../php/conf.d/security.ini /usr/local/etc/php/conf.d/security.ini

FROM base as production
RUN mv $PHP_INI_DIR/php.ini-prooduction $PHP_INI_DIR/php.ini

FROM base as development
RUN mv $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini
RUN apk add --no-cache autoconf g++ make \
    && pecl install xdebug \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable xdebug
COPY ../php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
