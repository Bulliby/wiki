<!-- TITLE: Shell -->
<!-- SUBTITLE: A quick summary of Shell -->

# Shell
> Ici je stock quelques informations sur l'utilisation d'un shell.

### Global

* Pour certaines commandes (voir le *man*) le `-` est utilisé par ces commandes comme un charactères spécial représentant l'entrée standart. Pour éviter l'interprétation, il faut faire référence au `-` avec un path comme dans :  `cat ./-`. On peut également utiliser `--` pour marquer la fin des options. Ainsi la commande suivante rends le resultat escompté : `cat -- -file`. Elle est cepedant inutile et il faut donc utiliser la technique du dessus pour le cas d'un nom de fichier strictement égale au `-`.
