---
title: Set-Cookie
description: 
published: true
date: 2022-04-03T08:35:02.591Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:52.538Z
---

# Set-Cookie

Cookies can be set between two `vhost` with the same domain and a different subdomain :

```
auth.gitgraph.com
client.gitgraph.com
```

With a header like this : 

```
Set-Cookie: oauth=3ed8356ba3d54f8ef98d45b63ba9dd43519183d6; Path=/; Domain=gitgraph.com
```