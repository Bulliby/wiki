---
title: Laravel
description: 
published: true
date: 2022-04-02T18:36:00.663Z
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
