FROM interdrinks/php:7.1-dev

RUN set -xe \
    && apk add --no-cache --virtual .persistent-deps docker \
    && apk add --no-cache --virtual .build-deps make g++ autoconf \
    && docker-php-source extract \
    && pecl install xdebug-2.5.0 \
    && docker-php-source delete \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && rm -rf /tmp/pear /var/cache/apk/* \
    && apk del .build-deps \
    && addgroup -g 1000 jenkins \
    && adduser -D -u 1000 -G jenkins jenkins

VOLUME /var/run/docker.sock
