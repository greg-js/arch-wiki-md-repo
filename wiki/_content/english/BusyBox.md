Related articles

*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [init](/index.php/Init "Init")

**Warning:** Do not expect full drop-in replacement and compatibility. Certain utilities may not exist and for those that do, there may be missing options.

[w:BusyBox](https://en.wikipedia.org/wiki/BusyBox "w:BusyBox")

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 init](#init)
    *   [2.2 getty](#getty)
    *   [2.3 mdev](#mdev)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [busybox](https://www.archlinux.org/packages/?name=busybox) package.

Busybox commands are symbolic links to `/usr/bin/busybox` and thus take very little space. This is especially interesting for low-footprint systems.

## Usage

### init

Init scripts can be used together with busybox-init, for example [minirc](https://aur.archlinux.org/packages/minirc/). See [init](/index.php/Init "Init") for details.

### getty

The gettys are defined in the file `/etc/inittab`, By default getty is started on ttys 1 through 4.

In order to enable/disable gettys, you just put this line in /etc/inittab.

```
tty2::respawn:/sbin/agetty -8 -s 38400 tty2 linux

```

Just replace tty2 with the tty, you want getty to start on. If you want init to ask you before starting the gettty, then replace respawn with askfirst.

### mdev

See [Gentoo wiki](https://wiki.gentoo.org/wiki/Mdev).

## See also

*   [w:ToyBox](https://en.wikipedia.org/wiki/ToyBox "w:ToyBox")