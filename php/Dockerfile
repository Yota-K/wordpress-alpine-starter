FROM wordpress:5.2.4-fpm-alpine

RUN apk update \
    && apk add mysql-client \
    && rm -rf /var/cache/apk/*

COPY php.ini /usr/local/etc/php

WORKDIR /var/www/html
