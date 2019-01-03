# Certbot

## Introduction

C'est une app écrite en python qui permet l'installation de **ssl** sur des
**vhost**.

## Installation (Archlinux/Apache)

* `pacman -S certbot certbot-apache`

* Décommenter `LoadModule ssl_module modules/mod_ssl.so` dans
`/etc/httpd/conf/httpd.conf`

## Utilisation

### Cli sans interaction

```sh
certbot --agree-tos --email wellsguillaume@gmail.com --apache -n --redirect -d nomdeddomaine.fr
```

* `-n` : lance la commande en mode **non interactive**. Si les options ne sont
pas set la commande utilisera les valeurs par défault

* `--email` & `--agree-tos` : sont seulement nécessaire lors de la première 
utilisation de la commande.

* `--redirect` : configure le vhost pour redigérer sur **https** quand on demande
http.

* `--apache` : précise le type de serveur.

* `-d` : précise le nom de domaine. Tel qu' il apparait dans le vhost (*http*).
si on a un `ServerAlias` en www, on peut ajouter : `-d www.nomdedomain.fr`

### Aide

On peut obtenir l'aide des sous commandes (e.g: apache) : `certbot -h apache`

Ou la totalité de l'aide : `certbot -h all`.
