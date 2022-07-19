---
title: XDebug
description: 
published: true
date: 2022-07-19T14:11:37.316Z
tags: debug, dbg, xdebug, debugger
editor: markdown
dateCreated: 2022-07-19T14:11:37.316Z
---

# XDebug

## Installation

* Utiliser le paquet standard : `pacman -S xdebug`
* Éditer le fichier `/etc/php/conf.d/xdebug.ini` (`php --ini`)

```ini
zend_extension=/lib/php/modules/xdebug.so
xdebug.mode=debug
xdebug.client_port=9003
xdebug.client_host=172.22.0.1
```

Dans `xdebug.client_host` je signal à XDebug ou il doit chercher un client. Ici `XDebug` tourne dans un docker je lui donne l'IP de la gateway du docker.

## VIM

Le [vdebug](https://github.com/vim-vdebug/vdebug) permet de transformer **vim** en client de debug. `F10` pour placer un breakpoint et `F5` pour commencer à écouter.

```.vimrc
let g:vdebug_options = {}
let g:vdebug_options["port"] = 9003
let g:vdebug_options.path_maps = {"/srv/http": "/home/toto/mycode"}
```

* `vdebug_options.path_maps` permets de faire correspondre le code du docker avec celui dans vim qui est ouvert dans l'**host**.

## VSCODE

* Installer l'extension : `felixfbecker.php-debug`

Si l'éditeur n'est pas sur la même machine que le code exécuté il faut faire le lien entre les chemins et éditer la configuration du plugin :

```
"pathMappings": {
	"/srv/http": "${workspaceFolder}",
} 
```

## Debug

Pour lancer le debug depuis un serveur web on peut ajouter un paramètre GET au client :

* http://myapp:23001/url/?XDEBUG_SESSION_START=vscode

Pour lancer le debug depuis php-cli on passe la variable d’environnement `XDEBUG_TRIGGER=yes` avant la commande. Dans un **docker** on peut procéder de la manière suivante :

* `docker exec  --user www-owner --env XDEBUG_TRIGGER=yes -it belote-docker-auth-1 php bin/console  app:test-xdebug`