---
title: Vim
description: 
published: true
date: 2020-01-10T22:54:41.695Z
tags: 
---

# Vim

## Installation

Get the PKGBUILD from the official archlinux's repository. See : 

[archlinux.fr](https://wiki.archlinux.fr/Pacman#R.C3.A9cup.C3.A9rer_les_sources_d.27un_paquet)

You can find a PKGBUILD sample here [github](https://github.com/Bulliby/Pkgbuild/blob/master/vim/PKGBUILD)

To install with Pacman :

```shell
pacman -U vim-8.1.2268-2-x86_64.pkg.tar.xz vim-runtime-8.1.2268-2-x86_64.pkg.tar.xz
```
### Bundle

Apply this patch for lusty explorer : [patch](https://github.com/vim-scripts/LustyExplorer/pull/1/commits/0fb46f6e2e0bcd44094c7d2d959afe156348adcd)

### Pacman packet update
Exculde Vim from pacman update add : `/etc/pacman.conf` add : `IgnorePkg   = vim vim-runtime`

## Compile Vim editor

> Here we compile the editor and use it with the host's vim runtime

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
      --enable-pythoninterp=dynamic \
      --enable-python3interp=dynamic \
      --enable-rubyinterp=dynamic \
      --enable-luainterp=dynamic \
      --enable-tclinterp=dynamic \
      --disable-canberra
    make VIMRUNTIMEDIR=HOST_VIM_RUNTIME_PATH

```

Replace HOST_VIM_RUNTIME_PATH by the path of your vim runtime instance. To get it `:echo $VIMRUNTIME` in the cli of Vim.