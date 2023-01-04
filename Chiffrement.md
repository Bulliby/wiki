---
title: Chiffrement
description: 
published: true
date: 2023-01-04T10:25:36.548Z
tags: 
editor: markdown
dateCreated: 2023-01-01T17:48:45.040Z
---

# Chiffrement

Deux types de chiffrement

## Symétrique

On partage une clef entre les deux parties qu'on utilise pour chiffrer la communication. Ce chiffrement est plus rapide que le chiffrement **asymétrique**. La clef doit être connue des deux parties. La question est comment la partagé de manière sécurisé ? C'est la qu'entre en jeux le chiffrement **asymétrique**.

## Asymétrique

Le chiffrement asymétrique est utilisé par exemple dans le protocole SSH pour partager une clef de chiffrement symétrique de manière sécurisé. Le chiffrement asymétrique étant plus coûteux en ressource il n'est utilisé que pour le partage de la clef.

### Type de chiffrement asymétrique : RSA

Avec le type de chiffrement **RSA** les deux parties doivent par avance se connaître pour partager des informations de manière sécurisé. Cela passe par la génération d'une clef publique et le partage de celle-ci avec le serveur. Le serveur l'utilise par la suite pour chiffrer le secret que le client pourra décrypter et utiliser comme clef de chiffrement **symétrique** pour le reste des communications.

Ce système se base sur des fonctions mathématiques qui sont tels que la génération de la donné est facile (Chiffrement avec la clef publique). Mais très difficile à inverser (Déchiffrer sans la clef privé).

#### Chiffrement

* La clef publique sert à chiffrer.
* La clef privée sert à déchiffrer.

#### Signature

* La clef privée sert à chiffrer.
* La clef public sert à authentifier.

## Ressources

* [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography)
* [One-way function](https://en.wikipedia.org/wiki/One-way_function)
