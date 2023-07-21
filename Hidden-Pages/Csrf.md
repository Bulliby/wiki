---
title: Csrf
description: An explanation of CSRF
published: true
date: 2023-07-21T18:16:49.431Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:57:38.390Z
---

# CSRF

## Introduction

**CSRF** for Cross-site-request forgery. Some malicious site can execute request with your cookie credentials.

## Mitigation

To mitigate **CSRF**, a *CSRF-Token* is generated.

This **token** can be passed to the client in several form :

* an input hidden field or meta-tag.

* a Cookie set by the Set-Cookie header response.

This two different technique see [SO](https://stackoverflow.com/questions/34782493/difference-between-csrf-and-x-csrf-token)