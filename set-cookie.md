---
title: Set-Cookie
description: 
published: true
date: 2020-10-31T17:03:55.600Z
tags: 
editor: undefined
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
Set-Cookie: oauth=3ed8356ba3d54f8ef98d45b63ba9dd43519183d6; Path=/; Domain=gitgraph.com
```

You have to allow credentials in back with a header like this : 
```
Access-Control-Allow-Credentials: true
```

And in front with your `XMLHttpRequest` :

```
XMLHttpRequest.withCredentials 
or axios : axios.post(process.env.OAUTH_URL, { code, state }, {withCredentials: true})
```