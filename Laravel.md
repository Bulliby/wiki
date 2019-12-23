---
title: Laravel
description: 
published: true
date: 2019-12-23T17:06:41.455Z
tags: 
---

# Laravel

## Change default App Namespace

To replace the App namespace in the current code : 

```shell
sed  's/App\\/Belotte\\/' `find app -type f`
```

With `-i` option to persist in file.

composer.json:
```json
"NewNamespace\\": "app/"
```

bootstrap.php, singleton.
config/app.php

To replace the folder `app` with a custom name you can override the class :

`vendor/laravel/framework/src/Illuminate/Foundation/Application.php`

in `bootstrap/app.php`, not tested yer.