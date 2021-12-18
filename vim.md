---
title: Vim
description: 
published: true
date: 2021-12-18T22:01:20.189Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:59:10.773Z
---

# Vim

## Installation

### Download

Get the PKGBUILD from the official archlinux's repository. See : 

[archlinux.fr](https://wiki.archlinux.org/title/Pacman_(Fran%C3%A7ais)#R.C3.A9cup.C3.A9rer_les_sources_d.27un_paquet)

> (C'est moi qui ai fait ce bout de doc. À l'origine sur archlinux.fr)

To install with Pacman :

```shell
pacman -U vim-8.1.2268-2-x86_64.pkg.tar.xz vim-runtime-8.1.2268-2-x86_64.pkg.tar.xz
```
### Pacman packet update
Exculde Vim from pacman update : `/etc/pacman.conf` add : `IgnorePkg   = vim vim-runtime`

#### Bundle

#### Lusty Explorer

Apply this patch for lusty explorer : [patch](https://github.com/vim-scripts/LustyExplorer/pull/1/commits/0fb46f6e2e0bcd44094c7d2d959afe156348adcd)

### Compile Vim editor (at home)

Edit the **PKGBUILD** after have clone the offcial projetc [see above](/en/vim#Installation)

* modify the `with-x` option to yes to allow clipboard copy and past

### Compile Vim editor (work)

```shell
uname -a
```
`Linux guillaume 5.3.0-51-generic #44-Ubuntu SMP Wed Apr 22 21:09:44 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux`

```shell
sudo apt-get install python3-dev
```

```shell
cd ~/vim
echo 2.2.2 > .ruby-version
```

```shell
./configure \
      --prefix=/usr \
      --localstatedir=/var/lib/vim \
      --with-features=huge \
      --with-compiledby='Guillaume Wells' \
      --enable-gpm \
      --enable-acl \
      --with-x=yes \
      --disable-gui \
      --enable-multibyte \
      --enable-cscope \
      --enable-netbeans \
      --enable-perlinterp=dynamic \
      --enable-python3interp=yes \
      --with-python3-config-dir=$(python3-config --configdir) \
      --enable-rubyinterp=yes \
      --enable-luainterp=dynamic \
      --enable-tclinterp=dynamic \
      --disable-canberra
      make VIMRUNTIMEDIR=HOST_VIM_RUNTIME_PATH
```

Runtime Path :

```
/usr/share/vim/vim81
```


## Usage

### Registers

* `"_` : Unamed register is pointing on the content of the last register used.

* `"0` : Contain the most recent yank even if it's not an enitre line.

* `"1` : Contain the last deleted or changed element if contains not less than one line.