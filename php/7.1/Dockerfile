FROM php:7.1-fpm-alpine

ENV APCU_VERSION 5.1.8
ENV WKHTMLTOPDF_BINARY /usr/bin/wkhtmltopdf

COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm.conf /usr/local/etc/php-fpm.d/php-fpm.conf
COPY wkhtmltopdf /usr/bin/wkhtmltopdf

HEALTHCHECK --interval=10s --timeout=3s \
    CMD \
    SCRIPT_NAME=/ping \
    SCRIPT_FILENAME=/ping \
    REQUEST_METHOD=GET \
    cgi-fcgi -bind -connect 127.0.0.1:9000 || exit 1

WORKDIR /srv/api-platform

RUN set -xe \
    && apk add --no-cache --virtual .persistent-deps \
        icu-libs \
        zlib \
        fcgi \
        libgcc \
        libstdc++ \
        libx11 \
        glib \
        libxrender \
        libxext \
        libintl \
        libcrypto1.0 \
        libssl1.0 \
        ttf-dejavu \
        ttf-droid \
        ttf-freefont \
        ttf-liberation \
        ttf-ubuntu-font-family \
    && apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        icu-dev \
        zlib-dev \
        libxml2-dev \
    && docker-php-ext-install \
        intl \
        pdo_mysql \
        zip \
        soap \
    && pecl install \
        apcu-${APCU_VERSION} \
        redis \
    && docker-php-ext-enable \
        apcu \
        opcache \
        redis \
    && rm -rf /tmp/pear \
    && apk del .build-deps \
    && mkdir -p var/cache var/log \
    && chmod -R 777 var /tmp

CMD ["php-fpm"]
