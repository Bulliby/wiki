---
title: Laravel
description: 
published: true
date: 2022-02-26T18:39:28.451Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:57:41.958Z
---

# Laravel

## Change default App Namespace

To replace the `App` namespace in the current code : 

```shell
sed  's|App/NewNameSpace|' `find app -type f`
```

With `-i` option to persist in file.

composer.json:
```json
"NewNamespace\\": "app/"
```

`bootstrap/app.php`, `config/app.php`

To replace the folder `app` with a custom name you can override the class :

`vendor/laravel/framework/src/Illuminate/Foundation/Application.php`

in `bootstrap/app.php`, not tested yet.

## Difference between timestamp and datetime in migration

They are close to be the same. They store both a date string (Y-m-d H:i:s). A difference of range is effective. For detail see : [laracast post](https://laracasts.com/discuss/channels/laravel/migrations-timestamp-vs-datetime-vs-date-vs-timestamps?page=0).
