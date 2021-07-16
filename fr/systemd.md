---
title: Systemd
description: 
published: true
date: 2021-07-16T19:31:11.863Z
tags: init, journalctl, systemctl, sysv, unit
editor: markdown
dateCreated: 2021-07-16T19:31:11.863Z
---

# Systemd

## Références

* [units file](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files)
* [tutoriel-complet](https://www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal)

## Introduction

* Les tâches sont lancées de manière asynchrones. Elles se calent les unes par rapport aux autres en fonction des règles `After` et `Before` dans les **unit files**.

* Les **unit files** créées par l'administrateur se trouve dans :

```
/etc/systemd/system
```

Les **unit files** du système peuvent être surcharger partiellement (ligne par ligne) en créant un fichier `.conf` dans un dossier avec le nom du service formaté de la manière suivante : `toto.service.d` pour un service *toto*.

## Sections

> Le nom des sections dans les **unit files** sont sensibles à la casse.

### [Install]

* `WantedBy=` : En combinaison avec la commande `systemctl enable` elle permet de démarrer le service au démarrage du système.

### [Unit]

* `Description=` : Description du service (facultative). Peut être vu dans le journal (`journalctl`) ou statu du service (`systemctl status`).

* `After=,Before=` : Une liste d'unités séparées par des espaces. Ces directives permettent de définir Avant/Après qu'elles unités elles doivent être démarrées arrêtées.

### [Service]

* `ExecStart`, `ExecStop` : sont respectivement appelés au démarrage et à l'extinction de l'unité. Cela peut se faire de manière automatique (`systemctl enable`) ou manuel (`systemctl start`).

* `RemainAfterExit` : Cette directive permet de considérer une unité comme encore active bien que son script soit *mort*. Cela deviens intéressant également pour les **unit files** sans **ExecStart** mais avec un **ExecStop** que l'on souhaite voir exécuté.

## À l'extinction

Vouloir agir sur l'**extinction** et non pas sur le **démarrage** d'un *service* demande de réfléchir la chronicité à l'inverse **After** devient **Before** *etc* ...
