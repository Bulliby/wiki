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

### Zone Mémoire d'un Processus

![Process Memory Layout](/uploads/process-memory-layout.png "Process Memory Layout"){.align-left}




