# HedgeDoc

[HedgeDoc](https://docs.hedgedoc.org/) lets you create real-time collaborative markdown notes.
It is inspired by Hackpad, Etherpad and similar collaborative editors.

## Running

```sh
cd container/hedgedoc
# First time
docker compose up
# All other times
docker compose start
docker compose stop
```

## Installation via Docker

Basic docker-compose.yml file from the [official documentation](https://docs.hedgedoc.org/setup/docker/):

```yml
version: '3'
services:
  database:
    image: postgres:13.4-alpine
    environment:
      - POSTGRES_USER=hedgedoc
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=hedgedoc
    volumes:
      - database:/var/lib/postgresql/data
    restart: always
  app:
    # Make sure to use the latest release from https://hedgedoc.org/latest-release
    image: quay.io/hedgedoc/hedgedoc:1.10.3
    environment:
      - CMD_DB_URL=postgres://hedgedoc:password@database:5432/hedgedoc
      - CMD_DOMAIN=localhost
      - CMD_URL_ADDPORT=true
    volumes:
      - uploads:/hedgedoc/public/uploads
    ports:
      - "3000:3000"
    restart: always
    depends_on:
      - database
volumes:
  database:
  uploads:
```

