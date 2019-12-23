---
title: Laravel
description: 
published: true
date: 2019-12-23T17:04:32.166Z
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