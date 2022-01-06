---
title: VPN
description: 
published: true
date: 2022-01-06T22:17:09.815Z
tags: 
editor: markdown
dateCreated: 2022-01-06T22:17:09.814Z
---

# VPN

* Je connecte mon ordinateur portable sur la 4G de mon mobile.

* J'ai un Raspberry PI avec un serveur VPN et un port ouvert sur ma box.

* Je créé une route sur le client grâce au VPN `push route` poussant le client à passer par VPN quand il essaye d'accéder au wikijs.

* Quand je me connecte au Raspberry PI en VPN celui est configuré pour faire du forwarding `echo 1 > /proc/sys/net/ipv4/ip_forward` quand j'essaye de toucher le wikijs depuis le portable il transfert le paquet vers celui-ci. Ainsi il agit comme un routeur.

* J'utilise une règle `iptables -t nat -A POSTROUTING -s 10.8.1.0/24 -o eth0 -j MASQUERADE` qui permet de "masquer" en sortie mon adresse TUN du serveur VPN par l'adresse du routeur qui est celle du RPI sur mon réseau local.

**Déroulement** :

Ainsi, le PC portable effectue une requête vers le wiki (push route). Atteint ma box et passe par le port ouvert. Le Raspberry forward la requête avec son IP local (MASQUERADE) de nouveau à la box. La box touche la cible le wikijs qui lui réponds. Le nat de la box sait qu'elle a envoyé la requête de cette réponse depuis le port VPN du RPI et lui envoie donc la réponse. Le serveur VPN gère la réponse et le `MASQUERADE` associe de nouveau ce paquet à l'interface TUN du Raspberry qui redirige le paquet vers le client.
