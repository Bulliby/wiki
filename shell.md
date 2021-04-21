---
title: Shell
description: A quick summary of Shell
published: true
date: 2021-04-21T18:52:46.816Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:59.803Z
---

# Shell

## Global

 Pour certaines commandes (voir le *man*) le `-` est utilisé par ces commandes comme un caractère spécial représentant l'entrée standard. Pour éviter l'interprétation, il faut faire référence au `-` avec un path comme dans :  `cat ./-`. On peut également utiliser `--` pour marquer la fin des options. Ainsi la commande suivante rends le résultat escompté : `cat -- -file`.

> Dans le cas d'un nom de fichier strictement égale à `-`, il faut utiliser la première technique celle du path.

## Pipes

Les **pipes** permettent de rediriger la **sortie** d'un programme dans l'**entrée** d'un autre.
> `ls | wc -c` va ainsi permettre la redirection de la sortie de *ls* dans l'entrée de *wc*.

### Développement Système

Les pipes sont des objets Unix/Linux, utilisables de manière programmatique.
> (man 3 pipe)

Avec eux nous pouvons **chaîner** des commandes à l'aide de quatre autres fonctions dup2, close, execvp et fork.
> (man 3 dup2) , (mas 2 close), (man 3 execvp), (man 2 fork)

Voici un exemple concret en Python qui permet d’exécuter la commande suivante :

`ls | wc | wc` :

```python
import os #Module who wrap system call

def exex_command(cmd1, cmd2, cmd3):
    r, w = os.pipe() #Create the pipe with a read/write side.
    pid = os.fork() #Create a new process.

    if pid == 0: #(1)
        os.close(r) #Close the read side of pipe.
        os.dup2(w, 1) #Duplicate stdout on the write side of the pipe. (2)
        os.execvp(cmd1, [cmd1])# Execute command.

    #Create a second pipe for communicate with the other part of the command
    r2, w2 = os.pipe()
    pid2 = os.fork() #Second fork for second command "wc"

    if pid2 == 0: #(1)
        os.close(w)
        os.dup2(r, 0) #Duplicate sdin on read side of first pipe
        os.close(r2)
        os.dup2(w2, 1)
        os.execvp(cmd2, [cmd2])

    pid3 = os.fork()
    if pid3 == 0: #(1)
        os.close(w2)
        os.dup2(r2, 0)
        os.execvp(cmd3, [cmd3])
    else:
        #Wait that the last fork return berfore continue to execute the father
        #code
        os.wait()

exex_command("ls", "wc", "wc")

```



#### fork()

Nous exécutons chaque commande au sein d'un **fork**. Cela a pour effet de diviser le code en deux. Une partie (le fils), pour qui le processus ID (pid) vaut 0 *(voir 1)* une autre ou le **pid** est supérieur à 0 et fait référence au père du processus enfant qui lui ne change pas lors des différents **fork**.

#### execvp()

Permet d'exécuter une commande en fonction de son **nom**. Ainsi, `os.execvp(cmd3, [cmd3])` permet d’exécuter la commande `cmd3` avec les arguments `[cmd3]` qui représentent un tableau d'arguments contenant toujours par défaut en premier lieu le nom de la commande (d’où `cmd3` dans le tableau).  

La particularité de cette commande est qu'une fois exécutée elle met fin au processus. Du code peut être écrit après `execvp()` mais si elle n’échoue pas aucune des instructions ne seront exécutées.

#### dup2(oldfd, newfd)

La commande dup2 permet de **dupliquer** `newfd` et de le placer à la place de `oldfd`.

Comportement :  

Quand on créer un nouvel fd (**file descriptor**) celui-ci prend le plus petit index disponible. Ainsi  avec le code `dup2(w, 1)` *(voir 2)*. Je ferme w laissant un trou dans les index de *file descriptor* ouvert. Puis je duplique le *file descriptor 1 (stdout)* qui va automatiquement le placer à l'index de w le **remplaçant**.


## History expansion

* `!!` Last history entry
* `!str` History starting string
* `!n` History line
* `!#` Current line

### Word history expansion `(:)`:

* `!!:n` n Word
* `!!n-x` x-n range words
* `!!:$` last word

> [ZSH manual](http://zsh.sourceforge.net/Doc/Release/zsh_toc.html)