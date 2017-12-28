This repository provides Docker images for Interdrinks for PHP projects.

**This configuration is built for development. It is not recommended to use it in production.**

Create `docker-compose.yml` file as following:

```yml
version: '3'

services:
  app:
    image: interdrinks/php:7.2
    depends_on:
      - db
    env_file:
      - .env
    volumes:
      - $HOME/.composer/cache:/root/.composer/cache
      - ./:/srv/api-platform:rw
      - /srv/api-platform/var/cache
      - /srv/api-platform/var/log

  db:
    image: healthcheck/mysql
    environment:
      - MYSQL_DATABASE=api_platform
      - MYSQL_ROOT_PASSWORD=api_platform
    volumes:
      - db-data:/var/lib/mysql:rw
    ports:
      - 3306:3306

  nginx:
    image: nginx:1.11-alpine
    volumes:
      - ./docker/nginx/conf.d:/etc/nginx/conf.d:ro
      - ./public:/srv/api-platform/public:ro
    ports:
      - 80:80

  varnish:
    image: interdrinks/varnish:4-alpine
    depends_on:
      - app
    ports:
      - 8000:80

volumes:
  db-data: {}
```
