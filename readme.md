## Description

Traefik blog proxy config

## Prerequisite

- docker >= 20
- docker-compose >= 1.25

## Congigration

```
entryPoints:
  web:
    - address:":80"
  websecure:
    - address:":443"
http:
  routers:
    lab:
      service: release-tapnow
      rule: "Host(`tapnow.localhost`)"
      entryPoints:
        - web
  services:
    release-tapnow:
      loadBalancer:
        servers:
          - url: "https://release-tapnow.presslogic.com/"

```

## Installation

```bash
# create traefik-net
$ docker network create -d bridge traefik-net
# run traefik
$ docker-compose -f docker-compose.yml up -d
```
