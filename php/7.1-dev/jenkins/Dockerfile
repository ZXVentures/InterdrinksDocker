FROM interdrinks/php:7.1-dev

RUN set -xe \
    && apk add --no-cache --virtual .persistent-deps docker \
    && addgroup -g 1000 jenkins \
    && adduser -D -u 1000 -G jenkins jenkins

VOLUME /var/run/docker.sock

USER jenkins
