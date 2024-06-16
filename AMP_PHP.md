# AMP PHP

## PHP

**PHP** est intrinsèquement **single threaded**, c'est le serveur (nginx, apache) qui fournit plusieurs processus de **PHP**.


## Non blocking I/O

C'est l'**event loop** qui permet de ne pas bloquer l'application sur les **inputs** **outputs**. **AMP PHP** arrive avec ces propres fonctions non **bloquantes** qui lors d'une tâche de lecture ou d'écriture passe le relais à une autre tâche (on parle de *coroutines*) dans sa **queue**. On parle de **cooperative multitasking [[1]](https://revolt.run/)**.

## Fiber

**Fiber** est arrivé dans un second temps et a permis de faciliter le fonctionnement asynchrone de PHP. Plus besoin de **callback** ou de **promesses** comme en javascript [[1]](https://revolt.run/). 

**Fiber** se comporte comme un thread dans le sens ou il embarque ça propre **pile d'appel**. Les **Fibers** sont gérées par le **scheduler** qui est dans le cas d'**amp php** l'**event loop** **revolt**.

Une **Fiber** peut être suspendue à tout moment et une seule **Fiber** s’exécute à un instant **T**.