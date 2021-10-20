---
title: Gist
description: 
published: true
date: 2021-10-20T20:22:33.632Z
tags: 
editor: markdown
dateCreated: 2021-04-21T19:25:43.537Z
---

# Cheat Sheet

## MySQL CLI

### Tools
```sql
show tables;
show databases;
use database;
```

### Export
```shell
mysqldump -u YourUser -p YourDatabaseName > wantedsqlfile.sql
```

#### Compressed
```shell
TODO
```

### Import
```shell
mysql -uroot -proot -hlocalhost database < save.sql
```


### Users Creation

#### Locally
```sql
CREATE USER 'waxer'@'localhost' IDENTIFIED BY 'mypass';
GRANT ALL ON db1.* TO 'waxer'@'localhost';
```

> For remote use `%`

### Flush
```sql
FLUSH PRIVILEGES;
```

## Ssh

### Generate ssh keys

```shell
ssh-keygen -t rsa -a 100 -b 4096 -f id_rsa
```

### Regenerate pub key from private one

```shell
ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub
```
> Todo check if it's the same

## Screen

#### Shared screen
```shell
screen -d -m -S shared
```

#### Nested screen

```
Ctrl + A + A + D in place of Ctrl + A + D
```

## Rsync

## Git

### Usefull commmands

``` shell
# For deprecated HTTPS
git config --global credential.helper 'cache --timeout=3600'
git push <remote_name> --delete <branch_name>
# Remove `-|+` from output
git diff --color-words
# Reminder ("A dog")
git log --graph --oneline --decorate --all
# Rebase from a given base (Awesome...)
git rebase --onto newBase oldBase feature/branch
# `n` for dry run
git clean -dfn
# Création remote
git init --bare /howe/guillaume/gittest.git
# Remote sur port ssh
git remote add origin ssh://guillaume@wellsguillaume.fr:12345/home/guillaume/git/gittest.git
```

Create a patch of one commit and apply it :

```shell
git format-patch -1 <sha>
git am < file.patch
```

## Find

### File and directory permissions
```shell
find . -type f -exec chmod 644 {} \;
find . -type d -exec chmod 775 {} \;
```
> `{}` represent the find iterated value

### delete symlink with no target

```shell
find -L . -name . -o -type d -prune -o -type l -exec rm {} +
```

### Path permissions

```
namei -om /etc/nginx
```

## Bash

### History

```bash
# Append
history -a
# Read
history -r
```

### Expand on current line

`press ALT+*`

## Zsh

### Zsh history

```zsh
# Append
fc -A
# Read
fc -R
```

## DD

### Archlinux image

```shell
dd bs=4M if=/home/bulliby/Downloads/archlinux-2018.01.01-x86_64.iso of=/dev/sdx status=progress && sync
```

### Recover a disk

```shell
dd if=/dev/sdX of=/dev/sdX conv=noerror,sync status=progress
```
> Block size must be default (512)

## ArchLinux

### Pacman

#### Clear package cache

```shell
pacman -Scc
```
> Usefull if `/var` is full

#### Obtain user's package inforamtions

```shell
# List explicitly installed packages
# -i stand for info
pacman -Qeti | less
# To delete orphan packages
pacman -Qdt | cut -d" " -f 1 | pacman -Rs -
```

## Vim

### Hex editor

#### Convert to HEX

```vim
:%!xxd
```

#### Convert to Binary

```vim
:%!xxd -r
```

### Fold

**Create** Fold :
`zf` on current selection

**Open** Close Fold : 
`zo`, `zc`

## Python

```
python setup.py install --user
```

### Pip
Use local env for pip install file .local/lib ...
```shell
pip install --user package
```

## Docker

```shell
docker build -t waxer/php56 .
docker run --name php56 -p 20789:80 -d  --rm waxer/php56:latest
docker tag waxer/php56:latest waxer/php56:v1
docker exec -it php56 /bin/bash
docker cp php56:/etc/htttp/conf/httpd.conf .
docker system prune
docker volume prune
```
## Postman XRH request

Key `X-Requested-With` Value `XMLHttpRequest`

> In headers

## Linux

### Set keyboard Layout

#### For current session

```shell
localectl set-keymap us
```

> To persist edit or create `/etc/vcsonsole.conf`