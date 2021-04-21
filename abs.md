---
title: Advanced Bash Scripting
description: 
published: true
date: 2021-04-21T18:53:46.180Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:57:49.171Z
---

# TLDP (Advanced Bash Scripting)

## Special Chars

`find .git -print -user root -exec chown bulliby: {} \;`
> Ici le point virgule est **escape** pour éviter son interprétation par le shell comme un séparateur de 2 commandes. Il est nécessaire à l'option `-exec` de **find**.

---

`.` est utilisé pour sourcer des scripts en **bash** (ne fonctionne pas sur **zsh**). Ainsi les deux expressions suivantes sont équivalentes :

* `source ~/.bashrc`
* `. ~/.bashrc`

---

`:` est le caractère **NOP** c'est un **builtin** de *bash*. Il renvoie toujours **true** et peut donc être utilisé dans une boucle à la place de la builtin **true** ou dans une condition if/else pour ne rien faire dans un des cas :

```shell
if condition
then :   # Do nothing and branch ahead
else     # Or else ...
   take-some-action
fi
```

`: > data.xxx` est équivalent à `cat /dev/null > data.xxx` comme c'est un builtin il n'y a pas de **fork**.

`:` Peut servir à remplir une fonction vide.

## Here Documents

Vous pouvez escape la chaîne qui délimite pour éviter l'interprétation à l'intérieur du document.

## Getopt 3

Gabarit pour `getopt(3)` fonctionne avec bash ou zsh

```bash
#!/bin/bash

: <<'COMMENT'
    * -n is the name of application shown when bad option given
    * +|- in optstring define if the option will be parsed after the
    first parameter of the command :
    ./cmd.sh parameter -a
    in this form with a `+` in optstring the `-a` option will not be parsed
COMMENT

ops=$(getopt -n "My application" -l "help,aide" -- "-ha" "$@")

: <<'COMMENT'
    Permit to pass option argument in the form of --arg="argument"
    in positional parameter form :
    ./cmd.sh --user="toto"
    ops=$(getopt -l "user:" -- "a" "$@")
    echo "$1" = "user=toto"
    eval set --$ops
    echo "$1 $2" = "user" "toto"
COMMENT

eval set --$ops

while [ ! -z "$1" ]
do
    case "$1" in
        -a) echo "Option \"a\"";;
        -h) echo "Option \"h\"";;
        --help|--aide ) echo "Long option Aide";;
    esac
    shift
done
```
