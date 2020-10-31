---
title: Docker
description: Notes about docker use
published: true
date: 2020-10-31T17:03:27.939Z
tags: 
editor: undefined
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
