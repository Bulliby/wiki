---
title: Set-Cookie
description: 
published: true
date: 2020-10-15T20:34:43.562Z
tags: 
editor: markdown
---

# Set-Cookie

You can set a cookie between two `Vhost` in the form of a **cross-site request**. For this you have to your local domain in `/etc/hosts`. Cross-site Set-Cookie only works on the same origin or on the same **sub-domain**. 

You for example put this two domain on your `/etc/hosts` : 

```
auth.gitgraph.com
client.gitgraph.com
```

With a header like this : 

```

```