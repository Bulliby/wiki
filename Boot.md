---
title: Boot
description: 
published: true
date: 2020-05-07T14:02:49.214Z
tags: 
---

# Boot

## Grub2

You can edit the boot entry pressing `e`.
> Press f10 for boot when it's done.

You can boot a shell command line just by removing **quiet** & **splash** and other video config at end of linux kernel's load and put `init=/bin/sh` in place of it.

You can get the grub's command line by pressing `c` on the grub's screen choice.

### Command Line

`set pager=1`

`ls` permit to list the devices disk.

You can get what is in by append a slash to the disk name

`ls (hd0,gpt3)/`

> Use auto complete to navigate.

If you want to boot manually :

* get the linux kernel :

```
linux (hd0,gpt3)/vmlinuz-linux
```

* get the init fram :

```
initrd (hd0,gpt3)/initramfs-linux.img
```

* boot  (root partition) :

```
boot (hd0,gpt4)
```

### Systemd

You can choose the default target of systemd from grub editing the boot option with `e`

```
systemd.unit=multi-user.target
```

> Add this at the end of line which loads kernel.