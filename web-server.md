---
title: Web Server
description: Knowledge about server
published: true
date: 2022-10-14T18:00:43.810Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:59:18.214Z
---

# Apache

## Reverse Proxy

### Apache

```apacheconf
<VirtualHost *:80>
    ServerName  "mon.nom.de.domaine.com" 

    ProxyPass         "/" "http://127.0.0.1:22567/"
    ProxyPassReverse  "/" "http://127.0.0.1:22567/" 

    CustomLog "/var/log/httpd/mon.nom.de.domaine.com-access.log"
</VirtualHost>
```

> To works it needs some apache **modules** : **mod_proxy.so** and **mod_proxy_http.so**

Like this **apache** redirect http request on the specified domain to the port `22567` who is binded to a docker container.

### Nginx

```nginx
server {
    server_name server.fr;

    location / {
        proxy_set_header   X-Forwarded-For $remote_addr;
        proxy_set_header   Host $http_host;
        proxy_pass         http://127.0.0.1:22100;
    }

		#$log_ip permet d'exclure mon IP des logs
    access_log /var/log/nginx/server/server-access.log combined if=$log_ip;
    error_log /var/log/nginx/server/server-error.log;
}
```

