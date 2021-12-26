---
title: Docker
description: Notes about docker use
published: true
date: 2021-12-26T11:23:33.588Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:07.459Z
---

# Docker

## Introduction

**Docker** est "state-less" on ne peut pas compter sur les sur le **système de fichier**, une fois relancé les donnés du docker disparaissent si elles ne se situent pas dans un **volume**.

Il ne peut y avoir qu' **un seul** processus en **background** c'est celui là qui fait que le container reste **UP**.

## Useful commands

* `docker build -t waxer/docker-php-v8-js:v1 .`
* `docker push waxer/docker-php-v8-js:v1`
* `docker login`
* `docker container ls -a`
* `docker images`
* ` docker exec lfs -it /bin/bash`

## Logs

### Emplacement

```bash
/var/lib/docker/containers/<container id>/<container id>-json.log
```

### Conf

Par défault j'ai mis dans `/etc/docker/deamon.json` :

```json
{
		"log-driver": "local"
}
```

J'obtiens en retour un binaire. Seulement lisible par la commande `docker logs "containername"` mais optimisé et avec rotation.

# Docker compose

### Volumes

Pour monter un volume externe dans `docker-compose` on peut utiliser les lignes suivantes

```yaml
volumes:
  transmission-config:
    external: true
    name: transmission-config
```