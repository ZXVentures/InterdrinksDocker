FROM mhart/alpine-node:9

RUN addgroup -g 1000 jenkins \
    && adduser -D -u 1000 -G jenkins jenkins \
    && yarn global add swagger-cli

USER jenkins
