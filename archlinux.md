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
