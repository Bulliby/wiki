---
title: Network
description: 
published: true
date: 2021-06-29T18:48:51.240Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:37.035Z
---

# Network

## Openclassrooms

Ces notes viennent du tutoriel :
> https://openclassrooms.com/fr/courses/857447-apprenez-le-fonctionnement-des-reseaux-tcp-ip

### Modèle OSI

Le **modèle OSI** *(Open Systems Interconnection)* est composé de 7 couches. Elles n'appartiennent pas spécifiquement à une machine en particulier mais peut décrire différents matériels chacun à leur niveau (switch, routeur, ordinateur).

Les couches peuvent être parcourues dans les **deux sens** (envoie / réception).

Chaque couche est indépendante et ne peut communiquer qu'avec sa voisine.

### Câblage *(couche 1)*

Actuellement on utilise les câbles à paire torsadées que l'on connecte à des prises **RJ45**
> Les câbles RJ45 n’existent pas.

### Réseau local *(couche 2)*

Le **protocole Ethernet** est le plus utilisé au niveau **2** du modèle *osi*.

À la réception d'un message la couche 2 est la première touchée sur une machine. Elle applique un filtre et n'accepte que les messages adressés à son **adresse MAC**.

> Il existe une adresse MAC spécial ou tous les bits sont a 1. Cette adresse mac est une adresse de broadcast. Quand elle est envoyée sur le réseaux elle est reçut par tous les appareils.

#### Switch

Le **switch** est un matériel de couche 2. Il possède une table **CAM** créée dynamiquement.

> La table **CAM** relie un numéro de port à une adresse MAC.

* Si l'adresse **MAC** de l'envoyeur n'est pas encore dans sa table **CAM** il relie le port par lequel la **trame** est passée a l'adresse MAC de l'envoyeur.

* Quand une trame est adressée à une adresse **MAC** qui n'est pas encore dans sa table *CAM*. Il envoie le message à tout ces ports. Ainsi le message est forcément reçu et lors de la réponse le *switch* pourra relier son port à l'adresse MAC de l’émetteur de la même manière qu'en *point 1*.

Le **TTL** (*Time To Live*) permet de nettoyer les relations dans la table **CAM** trop ancienne.

#### VLAN

Les **VLAN** (*Virtual LAN*) permettent de diviser un *switch* et de créer des réseaux locaux virtuels séparés et donc non interconnectables.

### Interconnecter les réseaux *(couche 3)*

#### IP

Une adresse possède deux parties :

* Une partie réseau qui sert à être contacté et qui est fixe.
* Une partie locale qui grâce au **netmask** définie une plage d'ip adressable sur le réseaux.

Ce **netmask** peut se représenter sous les formes suivantes :

* 255.255.255.0
* `/24` *CIDR notation*.

Celle-ci correspond à une série de **32 bits** (soit **4 octets**) avec la partie gauche qui est une série de `1` consécutifs représentant la partie fixe de l'**IP** celle qui définit le réseau, et la partie de droite une série de `0` qui représente la partie réseau adressables et qui peut être utilisée pour définir chaque machine sur le réseau.

Le masque est toujours fournit avec une adresse **IP** mais cette adresse n'influent pas sur la plage représenté par le masque.

`192.168.34.20/24` ici nous avons l'adresse IP `192.168.34.20` comprise dans une plage entre `192.168.34.0` et `192.68.34.255`.

La première et la dernière adresse de la plage sont des adresses réservées :

`192.168.34.0` est une adresse de **réseau** et `192.168.34.255` est une adresse de **broadcast**.
> Le nombre de machines possible dans un réseaux corresponds a deux puissance le nombre de 0 dans le masque `2^nb0`.

#### RFC 1918

Cette RFC définie des plages d'adresses **IP** qu'il est possible d'utiliser sur un réseau local sans interférer avec des adresses publiques externes. Ces plages sont donc réservées et aucun réseaux publique n'utilise une de ces **IP**.

Ces plages sont :

`10.0.0.0/8`
`172.16.0.0/14`
`192.168.0.0/16`
