---
title: Csrf
description: An explanation of CSRF
published: true
date: 2021-04-21T18:53:38.696Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:57:38.390Z
---

# CSRF

## Introduction

**CSRF** for Cross-site-request forgery. Some malicious site can execute request with your cookie credentials.

## Mitigation

 To mitigate this a **CSRF**, a generated token is registered in a session server who is directly relied to an application user.

 This **token** can be passed to the client in several form :

 * an input hidden field or meta-tag.

 * a Cookie set by the Set-Cookie header response.


 The client get this token and pass it to the server with a custom HTTP header.
 > With the **Set-Cookie** method it's realy important that the token's verification rely only on custom HTTTP header not on Request CSRF cookie.
