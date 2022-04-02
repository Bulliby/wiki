---
title: Web Server
description: Knowledge about server
published: true
date: 2022-04-02T18:44:58.970Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:59:18.214Z
---

# Apache

## Proxy

```apache_conf
<VirtualHost *:80>
    ServerName  "mon.nom.de.domaine.com" 

    ProxyPass         "/" "http://127.0.0.1:22567/"
    ProxyPassReverse  "/" "http://127.0.0.1:22567/" 

    CustomLog "/var/log/httpd/mon.nom.de.domaine.com-access.log"
</VirtualHost>
```

> To works it needs some apache **modules** : **mod_proxy.so** and **mod_proxy_http.so**

Like this **apache** redirect http request on the specified domain to the port `22567` who is binded to a docker container.