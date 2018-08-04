<!-- TITLE: Accueil-->
<!-- SUBTITLE: Ici, je stock de la documentation sur différents sujets -->

# Reverse engineering
> Ces notes reflètent mes connaissances actuelles et ne sont pas forcément exactes...

### Notation

* 1 bit corresond à une unité possédant soit la valeur 0 soit la valeur 1.

Un ordinateur base ses calculs sur 8 de ces unités que l'on nomme Byte ou Octect. 

> Pour résumer on a :  8 bits = 1 Byte = 1 Octect

### Mémoire Virtuelle vs Mémoire Physique

Le système d'exploitation ne donne pas directement accès à sa mémoire physique. Il créer un système d'adressage virtuel qu'il connecte à la mémoire physique, c'est la *Mémoire Virtuelle* .

### Mémoire et Processus

La *mémoire virtuelle* est chargée dans chaque processus. Avec un espace d'adressage correspondant à l'architecture du processeur.

> ex: pour un système 32-bit nous avons: 4Gb d'espace adressable.

Chaque processus possède sa propre mémoire virtuelle évitant ainsi les conflits. C'est le système d'exploitation qui si charge de placer la data dans un endroit libre de la RAM si il en reste. 

### Binaires

* Dans un système **Windows** les binaires sont appellés exécutable et possèdent l'extension *.exe*.
* Dans un système **OsX** les binaires sont connus sous le format *Mach-O*.
* Dans un système **Linux** les binaires sont connus sous le format *ELF* (**E**xecutable and **L**inkable **F**ormat.

Ces formats de fichier possèdent leur propre architecutre.

### Zones Mémoire d'un Processus

![Process Memory Layout](/uploads/process-memory-layout.png "Process Memory Layout"){.align-left}

Pour être éxécuté le code d'un binaire doit tout d'abord être chargé dans la mémoire d'un processus. L'architecture d'un binaire de type ELF au seins d'un processus est la suivante :

* La zone *.text* : Contient les instructions du bianire.
* La zone *.rodata*: Contient les variables globales initialisées en lecture seule.
* La zone *.data*: Contient les variables globales initialisées.
* La *heap*: Contient les données qui ont été allouée dynamiquement à l'aide de la fonction C:  malloc.
* Il y a ensuite les librairies partagées et un vide qui séparent les sections précedentes de la suivante.
* La *Stack*: Contient toutes les variables créée statiquement.

### Indexation des Zones Mémoires

Les zone mémoires précedentes apparaissent toujours dans cette ordre dans un système **Linux**. La partie haute avant l'espace vide est adressée de haut en bas. La partie basse (*La Stack*) est adressée de bas en haut. L'espace entre les deux parties haute et basse de la mémoire d'un processus a tendance à se réduire. 