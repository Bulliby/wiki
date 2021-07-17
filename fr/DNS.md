---
title: DNS
description: 
published: true
date: 2021-07-17T17:09:29.767Z
tags: systemd, dns, domain, resolver, cache, fqdn
editor: markdown
dateCreated: 2021-07-17T17:09:29.767Z
---

# DNS

### Introduction

Le DNS *(Domain Name System)* fait la relation entre une **IP** *(Internet Protocol)* et un **FQDN** *(Fully Qualified Domain Name)*

### URL

Prenons l’URL suivante : `www.google.fr`. Nous avons :

* `www` nom de la machine
* `google.fr` nom de domaine

`www.google.fr.` est un **FQDN**

> On ne peut jamais réellement savoir si nous sommes face à un **FQDN** car on ne peut pas savoir si `www.google.fr` n'est pas lui même un **domain** qui possède une machine *toto* qui aurait pour **FQDN** `toto.www.google.fr.`

### Fichier Host

Petit détail *marquant* à l'origine (en 1981) le fichier **/etc/hosts** servait de **DNS**. 
Chaque utilisateur téléchargeait la liste des IP des 213 machines existantes sur le web avec leurs domaines associés et plaçait cette liste en lieu et place du `/etc/hosts`

### Arborescence

Les noms de domaines sont une arborescence on interroge d'abord le serveur racine `.` puis le domaine `fr`, puis `google` *etc...*.

> Chaque serveur connaît seulement les domaines sous son propre domaine.

### 2 Types de service

* Service de cache
* Service intermédiaire

Le service de cache : il donne si configuré une réponse récursive (c.a.d **exacte**). Il donne soit la réponse **exacte** soit une réponse négative et à ce moment se charge d’interroger un vrai serveur **intermédiaire** qui lui fournira une réponse exacte ou une réponse **partielle** indiquant vers quel serveur se tourner maintenant.

#### Service de cache

Sur Archlinux on peut configurer facilement un serveur de cache **DNS** avec : [systemd-resolved](https://wiki.archlinux.org/title/Systemd-resolved)

En démarrant le service `systemd-resolved.service` le serveur de cache se mets alors à écouter sur `127.0.0.53` et enregistre localement les noms de domaines consultés par l'utilisateur.

Le DHCP configuré avec `systemd-networkd` donnera automatiquement au serveur de cache le DNS intermédiaire à utiliser si ça résolution est infructueuse. Cela peut se changer dans l'unit systemd de la *device* correspondante : (ex :`/etc/systemd/network/wlo1.network`) avec la directive **DNS=**