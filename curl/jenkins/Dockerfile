FROM debian:9-slim

RUN apt-get update \
    && apt-get install -y curl git \
    && addgroup --gid 1000 jenkins \
    && adduser --disabled-password --gecos '' --uid 1000 --ingroup jenkins jenkins

USER jenkins
