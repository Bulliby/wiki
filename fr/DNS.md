---
title: DNS
description: 
published: true
date: 2021-12-28T22:31:55.979Z
tags: cache, dns, domain, fqdn, resolver, systemd
editor: markdown
dateCreated: 2021-07-17T17:09:29.767Z
---

# DNS

### Introduction

Le DNS *(Domain Name System)* fait la relation entre une **IP** *(Internet Protocol)* et un **FQDN** *(Fully Qualified Domain Name)*

### URL

Prenons l’URL suivante : `www.google.fr`. Nous avons :

* `www` nom de la machine
* `google` nom de domaine
* `fr` nom domaine de premier niveau

`www.google.fr.` est un **FQDN**

> Nous ne pouvons jamais avoir la certitude que nous sommes en présence d'un **FQDN**, nous ne pouvons assurer qu'il n'y a pas un préfixe à ce que nous pensons être un FQDN.


### Fichier Host

Petit détail *marquant* à l'origine (en 1981) le fichier **/etc/hosts** servait de **DNS**. 
Chaque utilisateur téléchargeait la liste des IP des 213 machines existantes sur le web avec leurs domaines associés et plaçait cette liste en lieu et place du `/etc/hosts`

### Arborescence

Les noms de domaines sont une arborescence on interroge d'abord le serveur racine `.` puis le domaine `fr`, puis `google` *etc...*.

> Chaque serveur connaît seulement les domaines sous son propre domaine.

Ou peut tracer ces appels avec la commande suivante :

```bash
drill -T [-V 5] www.google.com
```

### 2 Types de requêtes

* Récursive
* Itérative

La **requête récursive** apporte une réponse exacte. Le client n'a pas besoin de d’effectuer lui même une autre requête pour obtenir une réponse.

Avec la **requête itérative** on obtient une réponse partielle. Si le serveur ne connaît pas la réponse il envoie un **referral** qui est l'adresse d'un serveur qui devrait avoir la réponse.

### Fonctionnement courant

Le client effectue une requête récursive au serveur DNS. Si le serveur ne peut pas apporter la réponse directement il fait une requête itérative à un serveur qui devrait avoir la réponse. Si celui-ci à la réponse il l'envoie ou donne un **referral** qui sera utilisé dans une nouvelle requête itérative par le serveur	 et ainsi de suite.

### 2 Types de service

* Service de cache
* Service intermédiaire

Le service de cache : il donne si configuré une réponse récursive (c.a.d **exacte**). Il donne soit la réponse **exacte** soit une réponse négative et à ce moment se charge d’interroger un vrai serveur **intermédiaire** qui lui fournira une réponse exacte ou une réponse **partielle** indiquant vers quel serveur se tourner maintenant.

#### Service de cache

Sur Archlinux on peut configurer facilement un serveur de cache **DNS** avec : [systemd-resolved](https://wiki.archlinux.org/title/Systemd-resolved)

En démarrant le service `systemd-resolved.service` le serveur de cache se mets alors à écouter sur `127.0.0.53` et enregistre localement les noms de domaines consultés par l'utilisateur.

Le DHCP configuré avec `systemd-networkd` donnera automatiquement au serveur de cache le DNS intermédiaire à utiliser si ça résolution est infructueuse. Cela peut se changer dans l'unit systemd de la *device* correspondante : (ex :`/etc/systemd/network/wlo1.network`) avec la directive **DNS=**