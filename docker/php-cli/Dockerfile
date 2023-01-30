FROM php:8.1-cli-alpine as base
RUN docker-php-ext-install pdo pdo_mysql
WORKDIR /app
COPY ../php/conf.d/security.ini /usr/local/etc/php/conf.d/security.ini

FROM base as production
RUN mv $PHP_INI_DIR/php.ini-production $PHP_INI_DIR/php.ini

FROM base as development
RUN apk add --no-cache autoconf g++ make unzip wget bash git \
    && pecl install xdebug \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable xdebug
COPY ../php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
RUN mv $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/bin --filename=composer --quiet
