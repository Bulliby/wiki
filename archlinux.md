---
title: archlinux
description: 
published: true
date: 2021-04-15T19:31:51.413Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:57:52.826Z
---

# Arch Linux

### Installation

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

#### Network

##### DHCP client

To obtain an **IP** from a DHCPD server like a **FAI Box** we need to configure each interface to listen for a **dhcp** request. On archlinux we use `systemd-networkd`.

Create a file `/etc/systemd/network/20-wired.network` for ethernet interface with this content :

```
[Match]
Name=enp1s0

[Network]
DHCP=yes
```

Do the same with this file `/etc/systemd/network/25-wireless.network` who handle **wifi** interface.

Enable and restart `systemd-networkd.service`.

##### Wifi

Use
```
wpa_passphrase MYSSID passphrase
```

to print the configuration needed. Use it in :

`/etc/wpa_supplicant/wpa_supplicant-interface.conf` replace interface by your **wifi interface** name do `ip a` to show it.

Enable and start the service `wpa_supplicant@interface.service`.

#### Mac

On my mac, who is old, i need an old version of arch linux iso. We can use the iso from this site to find old arch images : [archive img](https://archive.archlinux.org/iso).

> Atm i have test with the image : `archlinux-2016.01.01-dual`


#### Bose headeset

Install

`pacman -S bluez bluez-utils bluedevil pulseaudio pulseaudio-bluetooth`

Enable PulseAudio services

```
systemctl --user enable pulseaudio.socket
systemctl --user enable pulseaudio.service

systemctl --user start pulseaudio.socket
systemctl --user start pulseaudio.service
```
> If an error `too many symbolic link` appear in `journalctl -f` you have to remove the device from your bluetooth listing. I dont't find a way to do this in GUI.

Start/enable `bluetooth.service`

Run `bluetoothctl`

#### GeForce RTx2700

Install nvidia proprietary driver.
> The nouveau seems not work well.

#### Locale (for vim)

`~/.config/plasma-localerc` this file override `/etc/locale.conf` so to be able to put LANG to `en_US.UTF-8` we can delete this file.
