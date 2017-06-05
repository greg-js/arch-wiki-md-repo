Windows 10 has a subsystem that emulates the Linux kernel interface to allow ordinary Linux applications to run. It is somewhat like the opposite of [Wine](/index.php/Wine "Wine"), but at a lower level. By default it comes with Ubuntu user space, but that can be replaced with Arch. To get it working properly you will require access to an existing Arch installation to build some packages. These instructions are based on [this guide](https://www.reddit.com/r/bashonubuntuonwindows/comments/5vnne8/howto_installing_arch_on_wsl_manually/).

## Preparation

You must be running the Windows 10 creator's update. If you have not used the Windows Subsystem for Linux yet, follow the instructions [here](https://msdn.microsoft.com/en-gb/commandline/wsl/install_guide) to enable it. Basically you enable:

*   Developer mode in *Settings > Update and Security > For developers* and
*   Windows Subsystem for Linux (beta) in *Turn Windows features on or off*.

If you already have it installed use:

```
> lxrun /uninstall /full /y

```

to delete the existing installation entirely (you might want to save some data first).

## Installation

Open a command prompt and install the official Ubuntu version:

```
> lxrun /install /y

```

Start bash:

```
> bash ~

```

Download an Arch bootstrap .tar.gz from [Arch Linux Downloads](https://www.archlinux.org/download/), and extract it:

```
$ tar -zxvf /mnt/c/Users/*username*/Downloads/archlinux-bootstrap-2017.06.01-x86_64.tar.gz

```

Uncomment a server in `~/root.x86_64/etc/pacman.d/mirrorlist`.

Make WSL autogenerate `/etc/resolv.conf`:

```
$ echo "# This file was automatically generated by WSL. To stop automatic generation of this file, remove this line." > ~/root.x86_64/etc/resolv.conf

```

Exit all bash prompts you have open.

In the Windows explorer, navigate to `C:\Users\*username*\AppData\Local\lxss\rootfs` and delete `bin`, `etc`, `lib`, `lib64`, `sbin`, `usr` and `var`.

Now move (do not copy) the same folders from `C:\Users\*username*\AppData\Local\lxss\root\root.x86_64` to `C:\Users\*username*\AppData\Local\lxss\rootfs`

Using a Linux computer build [fakeroot-tcp](https://aur.archlinux.org/packages/fakeroot-tcp/) and [glibc-wsl](https://aur.archlinux.org/packages/glibc-wsl/), then copy the packages to your Windows PC. *glibc-wsl* has a workaround for [this bug](https://github.com/Microsoft/BashOnWindows/issues/1878), and *fakeroot-tcp* is necessary until System V IPC is fully implemented [(see here)](https://github.com/Microsoft/BashOnWindows/issues/1016). This step will be unnecessary when those bugs are fixed.

Open bash again, and setup Arch:

```
# pacman-key --init
# pacman-key --populate archlinux
# pacman -U /mnt/c/Users/*username*/Downloads/glibc-wsl-2.25-2-x86_64.pkg.tar.xz
# pacman -U /mnt/c/Users/*username*/Downloads/fakeroot-tcp-1.21-2-x86_64.pkg.tar.xz
# pacman -Syyu base base-devel

```

Set up a user (does not have to be the same as your Windows username):

```
# useradd -m -G wheel -s /bin/bash *username*
# passwd root
# passwd *username*

```

Set the user as the default by running the following in a Windows command prompt:

```
> lxrun /setdefaultuser *username*

```