---
title: SMTP Gmail
description: 
published: true
date: 2022-07-14T14:59:58.657Z
tags: gmail, mail, mailer, smtp, symfony
editor: markdown
dateCreated: 2022-07-14T14:58:44.807Z
---

# SMTP Google

Pour utiliser le SMTP google dans symfony, il faut tout d'abord lancer l'agent qui va s'occuper d'envoyer les mails : 

```shell
docker exec --user www-owner -it belote-docker-auth-1 php bin/console messenger:consume
```

> Utiliser `-vv` si on veut également voir les mails qui réussissent.

## Installer les dépendances composer

```shell
# Pour l'agent de mail asynchrone
docker exec --user www-owner -it belote-docker-auth-1 composer require amphp/http-client
composer require symfony/google-mailer
```

## Configurer le .env

```shell
MAILER_DSN="gmail+smtp://monmail@gmail.com:motdepasse@default?verify_peer=0"
```

> **default** est l'host qui corresponds au DN du serveur smtp ici : **smtp.gmail.com**

## Envoyer des mails

```php
	$email = (new Email())
    		->from('monmail@gmail.com')
        	->to('maildestinataire@gmail.com')
       	->subject('Time for Symfony Mailer!')
       	->text('Sending emails is fun again!');

       $mailer->send($email);
```