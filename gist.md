---
title: Gist
description: 
published: true
date: 2021-06-29T18:48:49.998Z
tags: 
editor: markdown
dateCreated: 2021-04-21T19:25:43.537Z
---

# Steelcheat

## MySQL

### Tools
```sql
show tables;
show databases;
use database;
```
### Commons
```sql
show columns from <database>;
select * from table;
update table set toto=1 where id=2;
```

### Export
```shell
mysqldump -u YourUser -p YourDatabaseName > wantedsqlfile.sql
```

### Import
```shell
mysql -uroot -proot -hlocalhost database < save.sql
```

### Users Creation

#### Locally
```sql
CREATE USER 'jeffrey'@'localhost' IDENTIFIED BY 'mypass';
GRANT ALL ON db1.* TO 'jeffrey'@'localhost';
```
#### Remotely
```sql
CREATE USER 'jeffrey'@'%' IDENTIFIED BY 'mypass';
GRANT ALL ON db1.* TO 'jeffrey'@'%';
```
#### Flush is needed
```sql
FLUSH PRIVILEGES;
```

## Ssh

### Ssh agent

```shell
# Generate ssh key
ssh-keygen -t rsa -a 100 -b 4096 -f id_rsa
ssh-agent /bin/zsh
# Regenerate pub from pivate 
ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub
```

### Screen
```shell
#Shared screen
screen -d -m -S shared
```

## RSYNC

### Save
```shell
rsync -rtvs --progress --delete --force --exclude 'vendor' --exclude '.git' --exclude 'Trash'  --files-from=.save_rsync ~/ user@host:folder
```

## Git

### Usefull commmands

``` shell
git config --global credential.helper 'cache --timeout=3600'
git push <remote_name> --delete <branch_name>
git diff --color-words
git config --list | grep crlf
git diff @{1}..
git pull --rebase <remote-name> <branch-name>
git log --graph --oneline --decorate --all
git rebase --onto newBase oldBase feature/branch
git clean -dfn
```

Create a patch of one commit and apply it :

```shell
git format-patch -1 <sha>
git am < file.patch
```

## Shell

### Permissions

#### File permission
```shell
find . -type f -exec chmod 644 {} \;
find . -type d -exec chmod 775 {} \;
```
### Path permission

```
namei -om /etc/nginx
```

#### Bash history

```bash
history -a
history -r
```
#### Zsh history
```zsh
fc -A
fc -R
```

#### Bash automplete wildcard
`press ALT+*`

## ISO
```shell
dd bs=4M if=/home/bulliby/Downloads/archlinux-2018.01.01-x86_64.iso of=/dev/sdx status=progress && sync
```

## Suppress Symlink with no target
```shell
find -L . -name . -o -type d -prune -o -type l -exec rm {} +
```

## ArchLinux

### Pacman

```shell
# Clear package's cache
pacman -Scc
# List explicitly installed packages
# -i stand for info
pacman -Qeti | less
# To delete orphan packages
pacman -Qdt | cut -d" " -f 1 | pacman -Rs -
```

## Vim

### Hex editor

#### Enter hex editor
```vim
:%!xxd
```
#### Escape hex editor
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