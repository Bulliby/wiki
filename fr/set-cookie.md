---
title: Set-cookie
description: 
published: true
date: 2021-07-16T18:51:25.076Z
tags: navigateur, cookie, header
editor: markdown
dateCreated: 2021-07-16T18:51:25.076Z
---

# Set-Cookie

`Set-Cookie` est un **header** dans la réponse du serveur qui demande l'insertion d'un cookie dans le navigateur.

Afin que le cookie soit accepté il doit respecter certaines règles. Il ne doit pas être **cross-site**. En revanche ils peuvent partager un même domaine. Ex :

```
auth.gitgraph.com
client.gitgraph.com
```

Le serveur pour ajouter un cookie au navigateur peut utiliser le **header** de réponse suivant :

```
Set-Cookie: oauth=3ed8356ba3d54f8ef98d45b63ba9dd43519183d6; Path=/; Domain=gitgraph.com
```