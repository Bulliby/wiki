---
title: cors
description: 
published: true
date: 2021-06-29T18:48:48.940Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:00.202Z
---

# CORS
> Cross-origin resource sharing
> Need rewrite

### Domain separation of client data

When you go on trucmuche.com, your **browser** download the **js** files of the site and execute it. The scripts are executed in the scope of the  `trucmuche.com` domain. The cookies are keep in a jail  and only accessible by the `trucmuche.com` site. 

### Ajax-request

* If the **js** script do an **ajax-request** to `trucmuche.com` there is no  cross-origin resource sharing, so the request is completed by the browser.  Indeed the same-origin request are by default accepted by browsers.

* If the **js** script do an **ajax-request** to `autremuche.com` there is  cross-origin so the request is not  completed, unless `autremuche.com` authorized `trucmuche.com` as origin.

### Security

It the browsers did not block the **CORS**, a script from `trucmuche.com` could make request to your bank with your browser and get some secret content.

That's why browser block **CORS**. Now if a server accept all type of orgin :  `Access-Control-Allow-Origin: *` all is data can be accessed by script from any domain. That is the case for web app like api. (e.g Github API)

### Reference

[mdn](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)