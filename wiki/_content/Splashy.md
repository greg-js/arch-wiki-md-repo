# Splashy

[Splashy](http://alioth.debian.org/projects/splashy/) is a userspace implementation of a splash screen for Linux systems. It provides a graphical environment during system boot using the Linux framebuffer layer via [directfb](http://www.directfb.org).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 /etc/rc.conf](#.2Fetc.2Frc.conf)
    *   [2.2 Including Splashy in initramfs](#Including_Splashy_in_initramfs)
    *   [2.3 The kernel command line](#The_kernel_command_line)
    *   [2.4 Themes](#Themes)

## Installation

Before you can use Splashy, you should enable [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Please refer to the specific instructions for [ATI cards](/index.php/ATI#Kernel_mode-setting_.28KMS.29 "ATI"), [Intel cards](/index.php/Intel#Enable_early_KMS "Intel") or [Nvidia cards](/index.php/Nouveau#KMS "Nouveau").

Install [splashy-full](https://aur.archlinux.org/packages/splashy-full/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

You may also check out [this topic](https://bbs.archlinux.org/viewtopic.php?id=48978) on the [Arch Linux forum](https://bbs.archlinux.org/) for a repository you can add with working splashy packages.

## Configuration

### /etc/rc.conf

Add this in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`:

 `/etc/rc.conf`  `SPLASH="splashy"` 

### Including Splashy in initramfs

Add Splashy to the HOOKS array in `/etc/[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")`. It **must** be added _after_ **base**, **udev** and **autodetect** for it to work:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev autodetect splashy [...]"` 

For early KMS start add the module [radeon](/index.php/Radeon "Radeon") (for radeon cards), [i915](/index.php/I915 "I915") (for intel cards) or [nouveau](/index.php/Nouveau "Nouveau") (for nvidia cards) to the MODULES line in `/etc/mkinitcpio.conf`:

 `/etc/mkinitcpio.conf` 

```
MODULES="i915"
**or**
MODULES="radeon"
**or**
MODULES="nouveau"
```

Rebuild your kernel image (refer to the [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") article for more info):

 `# mkinitcpio -p [name of your kernel preset]` 

### The kernel command line

You now need to set `quiet splash` as you kernel command line parameters in your bootloader. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more info.

### Themes

You can install [splashy-themes](https://aur.archlinux.org/packages/splashy-themes/) from the AUR. After installing, look at the available themes like so:

 `ls /usr/share/splashy/themes` 

The folder name is the theme name. Now change the theme to the one you want, eg.:

 `# splashy_config -s darch-white` 

**Note:** Themes ending in 43 are of 4:3 aspect ratio - the others are widescreen.

Rebuild your kernel image with:

 `# mkinitcpio -p [name of your kernel preset]` 

and reboot.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Splashy&oldid=392676](https://wiki.archlinux.org/index.php?title=Splashy&oldid=392676)"