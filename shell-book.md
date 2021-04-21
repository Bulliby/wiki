---
title: Shell Book
description: 
published: true
date: 2021-04-21T18:54:32.747Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:56.102Z
---

# Shell Book
## Tips 
```shell
(ls -Ra)
```
> Run `ls -Ra` in a subshell

```shell
trap "/bin/rm -rf my_file.sh" EXIT
```
> Permit to act on a specific UNIX **signal**

```shell
variable=my_script.bash echo ${variable#toto}
# Echo .bash
variable=my_script.bash echo ${variable%.bash}
# Echo toto
```
> Permit to extract a sub-string from a variable. `#` prefix like regex `^` suffix `%` like regex `$`. We can use double oerator `##` or `%%` to extact the longer string

```shell
echo ${PWD/$HOME/\~}
# if PWD is /home/bulliby/dev/shell we get ~/dev/shell
```
> This can be used for simple task in replacement of sed

```shell
echo $((2 + 4))
# Give 6, simple calculation
```

```shell
variable=$(ls -la)
# Place the result of cmd in `variable`.
```
> we can also use backtick but the primer form is recommended

```shell
declare -r A
A="Modification"
```
> Variable in read-only mode the modification give an error
