---
title: Boot
description: 
published: true
date: 2021-04-21T18:53:36.186Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:57:34.674Z
---

# Boot

## Boot process (Legacy Bios)

* First **BIOS** do a **POST** *(Power-on self-test)* in order to define if the hardware is able to boot. 
* Then **BIOS** search, in accordance with the boot order configured, for a **MBR**, loads the first one he fund and then starts his execution. The **MBR** contains the *stage1* of **grub** and is really small *446 bytes*, the *partition table* and the *boot signature* fill the left place *66 bytes*, of the 512 bytes of the first disk sector.
* The **stage 1** purpose is to load the next step **stage 1.5**. For historical reasons the first partition of a hard drive start at sector 63. This is where **stage 1.5** resides and he has enougth place for load **filesystem driver** and load **stage 2** of grub on **fs** partition like `/boot`. 

* [Ressource](https://opensource.com/article/17/2/linux-boot-and-startup)

## Boot process (UEFI)

* An **EFI** parition must be created with the `esp` flag and **FAT32** filesystem. **GRUB** will place is efi **binary** created here with the *cmd* : `grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB`.
> Where **esp** is the mounted directory of the efi partition, and **GRUB** the name that will displayed for this boot *Entry*

* After this with : `grub-mkconfig -o /boot/grub/grub.cfg` the command find the kernel in the `boot` mounted partiton and create an entry for it in the grub **menu**.

## GRUB2

### Edit menu entry

You can edit the boot entry pressing `e`.
> Press f10 for boot when it's done.

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

You can choose the default target of systemd from grub editing the entry menu.

```
systemd.unit=multi-user.target
```

> Add this at the end of line which loads kernel.