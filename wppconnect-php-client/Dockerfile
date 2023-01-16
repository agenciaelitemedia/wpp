FROM php:8.0.10-fpm-alpine3.14 as builder

WORKDIR /var/www

RUN apk add --no-cache zip libzip-dev
RUN docker-php-ext-configure zip && \
    docker-php-ext-install zip && \
    docker-php-ext-install mysqli pdo pdo_mysql && \
    docker-php-ext-enable pdo_mysql

RUN apk add --no-cache composer bash bash-completion git

RUN cd /var/www
RUN composer require wppconnect-team/wppconnect-php-client
RUN rm -rf html
RUN git clone https://github.com/agenciaelitemedia/wpp-php.git html

RUN chown -R www-data:www-data /var/www

EXPOSE 9000
CMD [ "php-fpm" ]