# AMP PHP

## Non blocking I/O

C'est l'**event loop** qui permet de ne pas bloquer, l'application sur les **inputs** **outputs**. **AMP PHP** arrive avec ces propres fonctions non **bloquantes** qui lors d'une tâche de lecture ou d'écriture pas le relais à une autre tâche (on parle de *coroutines*) dans sa **queue**.

## Fiber

**Fiber** est arrivé dans un second temps pour faciliter le fonctionnement. TODO