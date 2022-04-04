---
title: Wikijs
description: 
published: true
date: 2022-04-04T20:45:24.915Z
tags: docker, js, volume, wiki
editor: markdown
dateCreated: 2021-04-21T19:18:37.876Z
---

# Wiki JS

## Container

To create the wikijs container use :

```bash
docker run -d  --restart unless-stopped --name wiki -e "DB_TYPE=mysql" -e "DB_HOST=localhost" -e "DB_PORT=3306" -e "DB_USER=wikijs" -e "DB_PASS=*******" -e "DB_NAME=wiki" --network host -v wikijs-md:/wiki requarks/wiki:latest
```
## Github

To configure the github storage :

* Create **rsa** public and private key. Put the public key in Settings > Deploy Key. Give write access.

* Put the private key content in wikijs configuration and allow only push to target.