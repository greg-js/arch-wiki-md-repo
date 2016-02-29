This page is a set of instructions, known issues, tips and workarounds for installing and configuring Arch Linux on the ASUS N56-VJ/VZ and ASUS N76-VJ/VZ Laptops

## Contents

*   [1 Installation](#Installation)
*   [2 Configuring](#Configuring)
    *   [2.1 Video](#Video)
    *   [2.2 Desktop Environment](#Desktop_Environment)
    *   [2.3 Sound](#Sound)

## Installation

**Note:** Since these laptops' BIOS does not support legacy boot, please read [UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") pages before following further instructions.

**Note:** To choose a boot device: please press `Escape` after machine starts and then choose the suitable installation source e.g. [USB Installation Media](/index.php/USB_Installation_Media "USB Installation Media").

An installation process is quite common. Please refer to [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") or [Installation guide](/index.php/Installation_guide "Installation guide") regarding installation on machines with UEFI motherboards. Please be advised that you **do not need** to create/format EFI partition in case you want to keep Windows 8 installed.

* * *

## Configuring

Thus, post-installation steps are very-well described in [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") and most features will work out of the box, there are some specific tips for ASUS N-series laptops (N56/76).

### Video

**Note:** You may want to read more about benchmark tools in the [Benchmarking](/index.php/Benchmarking "Benchmarking") article.

Disabling a discrete GPU is well-written described in [Bumblebee](/index.php/Bumblebee "Bumblebee") article. However, there is a poorly explored issue with

```
$ optirun *command1*

```

as well as with

```
$ primus *command1*

```

An Nvidia card with [nvidia](https://www.archlinux.org/packages/?name=nvidia) or [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) driver shows lower performance results than an integrated Intel HD4000 in both syntetic tests and real world applications (e.g. FPS in games).

You can check it by comparing (of course, you can use *glxgears* or any other benchmark instead of glxspheres)

```
$ vblank_mode=0 primusrun glxspheres
$ vblank_mode=0 optirun glxspheres
$ vblank_mode=0 glxspheres

```

The latter which is an integrated Intel GPU shows the best results (as of primus-20131226-1), which is not intended by the very basic idea of dual graphics.

The nature of the issue is described in this [article](https://github.com/amonakov/primus/issues/33). Some ideas and a patch is [here](https://lists.launchpad.net/bumblebee/msg00155.html), thus no reliable workaround is known yet. The issue is proven to exist at least in Arch Linux and OpenSUSE.

Arch users on the Russian Arch Linux forum are also trying to come up with the solution. You may want to check this [page](http://archlinux.org.ru/forum/topic/12655/?page=4).

Since the issue is not resoloved, you will help the community if you post your workaround.

### Desktop Environment

As Arch Linux is all about [The Arch Way](/index.php/The_Arch_Way "The Arch Way") and you are free to choose whatever DE you want. However you should keep in mind that ASUS N56-VJ laptops have a high pixel density for a 15,6" displays. In this case you may want to consider DE's supporting such density, e.g. GNOME 3.10.x or later.

### Sound

In development