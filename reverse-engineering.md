---
title: reverse-engineering
description: 
published: true
date: 2020-10-31T17:03:53.176Z
tags: 
editor: undefined
---

# Reverse engineering
> Ces notes reflètent mes connaissances actuelles et ne sont pas forcément exactes...

<!-- TITLE: Reverse Engineering -->
<!-- SUBTITLE: Some note about Reverse Engineering who aim explore deep computer's architecture -->


### Notation

* 1 bit correspond à une unité possédant soit la valeur 0 soit la valeur 1.

Un ordinateur base ses calculs sur 8 de ses unités que l'on nomme Byte ou Octect. 

> Pour résumer on a :  8 bits = 1 Byte = 1 Octect

### Mémoire Virtuelle vs Mémoire Physique

Le système d'exploitation ne donne pas directement accès à sa mémoire physique. Il crée un système d'adressage virtuel qu'il connecte à la mémoire physique, c'est la *Mémoire Virtuelle* .

### Mémoire et Processus

La *mémoire virtuelle* est chargée dans chaque processus. Avec un espace d'adressage correspondant à l'architecture du processeur.

> ex : pour un système 32-bit nous avons : 4Gb d'espace adressable.

Chaque processus possède sa propre mémoire virtuelle évitant ainsi les conflits. C'est le système d'exploitation qui si charge de placer la data dans un endroit libre de la RAM s'il en reste. 

### Binaires

* Dans un système **Windows** les binaires sont appellés exécutables et possèdent l'extension *.exe*.
* Dans un système **OsX** les binaires sont connus sous le format *Mach-O*.
* Dans un système **Linux** les binaires sont connus sous le format *ELF* (**E**xecutable and **L**inkable **F**ormat.

Ces formats de fichier possèdent leur propre architecutre.

### Zones Mémoire d'un Processus

![Process Memory Layout](/uploads/process-memory-layout.png "Process Memory Layout"){.align-left}

Pour être éxécuté, le code d'un binaire doit tout d'abord être chargé dans la mémoire d'un processus. L'architecture d'un binaire de type ELF au sein d'un processus est la suivante :

* La zone *.text* : Contient les instructions du binaire.
* La zone *.rodata* : Contient les variables globales initialisées en lecture seule.
* La zone *.data* : Contient les variables globales initialisées.
* La *heap* : Contient les données qui ont été allouées dynamiquement à l'aide de la fonction C :  malloc.
* Il y a ensuite les librairies partagées et un vide qui séparent les sections précedentes, de la suivante.
* La *Stack* : Contient toutes les variables crées statiquement.

### Indexation des Zones Mémoires

Les zones mémoires précédentes apparaissent toujours dans cette ordre dans un système **Linux**. La partie haute avant l'espace vide est adressée de haut en bas. La partie basse (*La Stack*) est adressée de bas en haut. L'espace entre les deux parties haute et basse de la mémoire d'un processus, a tendance à se réduire. Du fait de cet indexation par le bas, les adresses de la stack sont très élevées.

### Buffer Overflow

Quand on effectue un **Buffer Overflow** avec un code de type : 

```c_cpp
int x;
int buffer[64];
printf("%c\n", buffer[x]);
```

* Si `x` dépasse *64* nous parcourons la pile à contre-courant pour écraser les variables dont les adresses sont plus haute que la fin du buffer.
* Si `x` est inférieur à *0* alors nous parcourons la pile dans son sens et nous écrasons les variables situées plus basses que le debut du buffer.
> L'origine est toujours le buffer qu'on *Overflow*