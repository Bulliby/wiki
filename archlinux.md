---
title: archlinux
description: 
published: true
date: 2020-11-24T21:28:47.027Z
tags: 
editor: markdown
---

# Arch Linux

### Installation

#### Mac

On my mac, who is old, i need an old version of arch linux iso. We can use the iso from this site to find old arch images : [archive img](https://archive.archlinux.org/iso).

> Atm i have test with the image : `archlinux-2016.01.01-dual`

#### Flash media
On linux to create a bootable usb stick we can use the following cmd :

```shell
dd bs=4M if=path/to/archlinux.iso of=/dev/sdx status=progress oflag=sync
```

> We must not put the partion number it's `/dev/sdx` not `/dev/sdxn`.

For recover a clean usb for other use we need to exec this cmd :

```shell
wipefs --all /dev/sdx
```

#### Bose headeset

Install

`pacman -S bluez bluez-utils bluedevil pulseaudio pulseaudi-bluetooth`

Enable PulseAudio services

```
systemctl --user enable pulseaudio.socket
systemctl --user enable pulseaudio.service

systemctl --user start pulseaudio.socket
systemctl --user start pulseaudio.service
```
> If an error `too many symbolic link` appear in `journalctl -f` you have to remove the device from your bluetooth listing. I dont't find a way to do this in GUI.

Run `bluetoothctl`

#### GeForce RTx2700

Install nvidia proprietary driver.
> The nouveau seems not work well.