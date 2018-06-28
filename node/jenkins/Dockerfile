FROM mhart/alpine-node:9

RUN apk add --update --virtual .persitent-deps python make g++ \
    && addgroup -g 1000 jenkins \
    && adduser -D -u 1000 -G jenkins jenkins \
    && yarn global add swagger-cli node-sass

USER jenkins
