---
title: Backtracking
description: 
published: true
date: 2022-04-03T08:25:25.403Z
tags: algorithme, récursif
editor: markdown
dateCreated: 2021-12-18T22:15:32.672Z
---

# Backtracking

## Match

### Objectif

Le but ici est de résoudre le projet **match** de la piscine 42. Je m'éloigne un peu de la solution proposée par la plupart des étudiants qui consiste en un "**brut force**". 

Ma solution, n'est cependant pas parfaite au regard de la consigne... Le résultat est que je me comporte plus comme le **wildcard** d'une **regex**. Une étoile doit obligatoirement représenter un caractère: 

* `*t*t*s`
* `tatas`

Cela ne match pas, le première étoile ne peut pas prendre la place d'une lettre... Les autres cas semblent à peut près OK. L'objectif ici était de faire du backtracking.

### Backtracking

L'idée est de se rapprocher d'un moteur de regex. Le **wildcard** est un **Greedy** operator (opérateur glouton). C'est à dire que quand on le parcours il nous mène à la fin de la chaîne et commence ça recherche en sens inverse.

J'avais des difficultés à gérer mes valeurs de retours qui s'écrasaient les unes et les autres. Je me suis aidé avec cette référence : 

* http://blog.marcinchwedczuk.pl/matching-regexes-using-backtracking

### Le code

```c
int match(char *s1, char *s2, int count, size_t max)
{
    //La seule condition de succès
    if (*s1 == '\0' && *s2 == '\0') {
        return 1;
    }

    //Permet d'avancer en boucle sur les répétitions de wildcard
    if ('*' == *s1 && *(s1 + 1) == '*') {
        return match(++s1, s2, count, max);
    }

    //Quand sa match on mange des deux bouts
    if (*s1 == *s2) {
        return match(++s1, ++s2, count, max);
    }

    if (count == max) {
        return 0;
    }

    if ('*' == *s1) {
        // (1) Ici c'est le greedy qu'on mets en place.
        // On parcourt la chaine jusqu'à la fin
        int ret = match(s1, ++s2, ++count, max);
        // (2) Ici je suis dans le retour de la fonction (1).
        // La chaîne est parcourut en sens inverse.

        // Si la chaine n'a pas match à partir d'ici. J'écrase la valeur
        // de retour par une autre qui peut être vrai elle.
        if (!ret && count > 0) {
            ret =  match(++s1, s2, count, max);
        }
        return ret;
    }
    return 0;
}

```

L'avantage de cette méthode en comparaison d'une méthode de **brute force** est le nombre beaucoup plus petit, d'appels à la fonction récursive : sur une grande phrase avec beaucoup de wildecards.