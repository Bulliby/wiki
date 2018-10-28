<!-- TITLE: Web Server -->
<!-- SUBTITLE: Knowledge about server -->

# Apache2/httpd

### Docker + Apache

Pour utiliser un **Docker** en serveur HTTP tout en ayant un serveur **Apache** écoutant sur le port 80, il faut : 

* Utiliser un port différent que le port par défault comme entré du container : `0.0.0.0:22567->3000/tcp`. Ici nous utilisons le port 22567.

* Utiliser Apache comme **Reverse Proxy** et redirigé les appels au *nom de domaine* choisi sur le port standart sur le port **22567**. Pour cela on peut écrire le virtual host suivant :


```apache_conf
<VirtualHost *:80>
    ServerName  "mon.nom.de.domaine.com" 

    ProxyPass         "/" "http://127.0.0.1:22567/"
    ProxyPassReverse  "/" "http://127.0.0.1:22567/" 

    CustomLog "/var/log/httpd/mon.nom.de.domaine.com-access.log"
</VirtualHost>
```

> Il faut activer la librairie dynamique mod_proxy.so et mod_proxy_http.so.
