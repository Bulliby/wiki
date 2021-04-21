---
title: Web Server
description: Knowledge about server
published: true
date: 2021-04-21T18:56:46.330Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:59:18.214Z
---

# Apache

### My configuration for docker on por 80

Pour utiliser un **Docker** en serveur HTTP tout en ayant un serveur **Apache** écoutant sur le port 80, il faut : 

For use **Docker** as a `http` server and continue to use the **apache** host i usually the **Reverse Proxy** functionnality of Apache. Like this :

```apache_conf
<VirtualHost *:80>
    ServerName  "mon.nom.de.domaine.com" 

    ProxyPass         "/" "http://127.0.0.1:22567/"
    ProxyPassReverse  "/" "http://127.0.0.1:22567/" 

    CustomLog "/var/log/httpd/mon.nom.de.domaine.com-access.log"
</VirtualHost>
```

> To works it needs some apache **modules** : **mod_proxy.so** and **mod_proxy_http.so**

Like this apache can listen apache redirect http request on the specified domain to the port `22567` who is binded to a docker container.