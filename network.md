---
title: Network
description: 
published: true
date: 2020-12-28T19:48:27.478Z
tags: 
editor: markdown
---

# Network

## Openclassrooms

> https://openclassrooms.com/fr/courses/857447-apprenez-le-fonctionnement-des-reseaux-tcp-ip

### Modèle OSI

Le modèle **OSI** *(Open Systems Interconnection)* est composé de 7 couches. Elles n'appartiennent pas spécifiquement à une machine en particulier mais peu décrire différents matériels chacun à leur niveau (switch, routeur, ordinateur).

Les couches peuvent être parcourues dans les **deux sens** (envoi / réception).

Chaque couches est indépendante et ne peut communiquer qu'avec ça voisine.

### Câblage *(couche 1)*

Actuellement on utilise les câbles a paire torsadées que l'on connecte à des prises de câble **RJ45**
> Les câbles RJ45 n’existent pas.

### Réseaux local *(couche 2)*

Le **protocole Ethernet** est le plus utilisé au niveau deux du modèle.

A la réception d'un message la couche 2 est la première touché sur une machine. Elle applique un filtre et n'accepte que les messages adressés a son **adresse MAC**.

#### Switch

Le switch est un matériel de couche 2. Il possède une table **CAM** créé dynamiquement.

> La table **CAM** relie un numéro de port à une adresse MAC.

* Si l'adresse **MAC** de l'envoyeur n'est pas encore dans sa table **CAM** il relie le port par lequel la **trame** est passée a l'adresse MAC de l'envoyeur.

* Quand une trame est adressée à une adresse **MAC** qui n'est pas connectée à un de ses ports. Il envoie le message à tout ces ports. Ainsi le message est forcément reçue et lors de la réponse le switch pourra relier son port a l'adresse MAC de l’émetteur de la même manière qu'en *point 1*.

Le **TTL** permet de nettoyer les relations dans la table **CAM** trop ancienne.

#### VLAN

Les VLANs permettent de diviser un switch et de créer des réseaux locaux physiquement séparé et donc non interconnectable.

### Interconnecter les réseaux *(couche 3)*

#### IP

Une adresse possède deux parties :

* Une partie réseau qui sert à être contacté.
* Une partie locale qui contient une plage avec les machines locales.

Pour différencier ces deux parties on utiliser un masque (255.255.255.0 ou `/24` à la fin de l'ip).

La partie avec tout ces bits à `1` est la partie réseaux, la partie à `0` est la partie machine.

Le masque est toujours fournis avec une adresse **IP** mais cette adresse n'influent pas sur la plage représenté par le masque.

`192.168.34.20/24` ici nous avons l'adresse IP `192.168.34.20` comprise dans une plage entre `192.168.34.0` et `192.68.34.255`.

La première et la dernière adresse de la plage sont des adresses réservées :

`192.168.34.0` est une adresse de réseau et `192.168.34.255` est une adresse de broadcast.

---

Le nombre de machines possible dans un réseaux corresponds a deux puissance le nombre de 0 dans le masque `2^nb0`.

#### RFC 1918

Cette RFC définie des plages d'adresses **IP** qu'il est possible d'utiliser sur un réseau local sans interférer avec des adresses publiques.
Ces plages sont donc réservé et aucun réseau publique n'utilise une de ces IPs.

Ces plages sont :

`10.0.0.0/8`
`172.16.0.0/14`
`192.168.0.0/16`
