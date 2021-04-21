---
title: Wikijs
description: 
published: true
date: 2021-04-21T19:18:37.876Z
tags: wiki, js, docker, volume
editor: markdown
dateCreated: 2021-04-21T19:18:37.876Z
---

# Wiki JS
To create the wikijs container use :

```bash
docker run -d  --restart unless-stopped --name wiki -e "DB_TYPE=mysql" -e "DB_HOST=localhost" -e "DB_PORT=3306" -e "DB_USER=wikijs" -e "DB_PASS=*******" -e "DB_NAME=wiki" --network host -v wikijs-md:/wiki requarks/wiki:2
```