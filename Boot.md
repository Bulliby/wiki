---
title: Boot
description: 
published: true
date: 2020-11-28T15:24:52.014Z
tags: 
editor: markdown
---

# Boot

## Boot process (MBR)

First **BIOS** do a **POST** *(Power-on self-test)* in order to define if the hardware is able to boot. Then **BIOS** search, in accordance with the boot order configured, for a **MBR**, loads the first one and then starts his execution. The **MBR** contains the *stage1* of **grub** and is really small *446 bytes*, the *partition table* and the *boot signature* fill the left place *66 bytes*, of the 512 bytes of first disk sector.

The **stage 1** purpose is to load the next step **stage 1.5**. For historical reasons the first partition of a hard drive start at sector 63. This is where **stage 1.5** resides and he has enougth place for load **filesystem driver** and load **stage 2** of grub on a partition like `/boot`. The files are located in `/boot/grub2`.

* [Ressource](https://opensource.com/article/17/2/linux-boot-and-startup)

## Usage

### Grub2

You can edit the boot entry pressing `e`.
> Press f10 for boot when it's done.

You can boot a shell command line just by removing **quiet** & **splash** and other video config at end of linux kernel's load and put `init=/bin/sh` in place of it.

You can get the grub's command line by pressing `c` on the grub's screen choice.

#### Command Line

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