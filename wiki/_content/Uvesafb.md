# Uvesafb

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
*   [sysctl](/index.php/Sysctl "Sysctl")

In contrast with other framebuffer drivers, uvesafb needs a userspace virtualizing daemon, called v86d. It may seem foolish to emulate x86 code on a x86, but this is important if one wants to use the framebuffer code on other architectures (notably non-x86 ones). A new framebuffer driver has been added to kernel 2.6.24\. It has many more features than the standard vesafb, including:

1.  Proper blanking and hardware suspension after delay
2.  Support for custom resolutions as in the system BIOS.

It should support as much hardware as vesafb.

## Contents

*   [1 Installation](#Installation)
*   [2 Prepare the system](#Prepare_the_system)
    *   [2.1 Boot manager](#Boot_manager)
        *   [2.1.1 GRUB](#GRUB)
        *   [2.1.2 GRUB legacy](#GRUB_legacy)
    *   [2.2 mkinitcpio hook](#mkinitcpio_hook)
*   [3 Configure uvesafb](#Configure_uvesafb)
    *   [3.1 Define a resolution](#Define_a_resolution)
    *   [3.2 Optimizing Resolution](#Optimizing_Resolution)
    *   [3.3 Checking Current Resolution](#Checking_Current_Resolution)
*   [4 kernel module parameters](#kernel_module_parameters)
*   [5 Uvesafb and 915resolution](#Uvesafb_and_915resolution)
    *   [5.1 915resolution-static](#915resolution-static)
    *   [5.2 The resolution](#The_resolution)
    *   [5.3 The Hooks Array](#The_Hooks_Array)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Uvesafb cannot reserve memory](#Uvesafb_cannot_reserve_memory)
    *   [6.2 Error: "pci_root PNP0A08:00 address space collision + Uvesafb cannot reserve memory"](#Error:_.22pci_root_PNP0A08:00_address_space_collision_.2B_Uvesafb_cannot_reserve_memory.22)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") [v86d](https://aur.archlinux.org/packages/v86d/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR").

## Prepare the system

Remove any framebuffer-related kernel boot parameter from the bootloader configuration to disable the old vesafb framebuffer from loading.

```
$ grep vga /proc/cmdline
$ grep -ir vga /etc/modprobe.d/

```

Should return no results. If you do have a `vga=` option somewhere, you will need to remove it.

### Boot manager

Make sure your boot manager does not screw with the graphics settings.

#### GRUB

First edit `/etc/default/grub` commenting the `GRUB_GFXPAYLOAD_LINUX=keep` line.

Then regenerate `grub.cfg` via the standard script:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### GRUB legacy

Remove all references to `vga=xxx` from kernel lines in `/boot/grub/menu.lst` to allow correct operation of uvesafb.

### mkinitcpio hook

Add the v86d hook to HOOKS in `/etc/mkinitcpio.conf`. This allows uvesafb to take over at boot time.

```
HOOKS="base udev v86d ..."

```

## Configure uvesafb

### Define a resolution

The settings for uvesafb are defined in `/usr/lib/modprobe.d/uvesafb.conf`:

```
# This file sets the parameters for uvesafb module.
# The following format should be used:
# options uvesafb mode_option=<xres>x<yres>[-<bpp>][@<refresh>] scroll=<ywrap|ypan|redraw> ...
#
# For more details see:
# [http://www.kernel.org/doc/Documentation/fb/uvesafb.txt](http://www.kernel.org/doc/Documentation/fb/uvesafb.txt)
#
options uvesafb mode_option=1280x800-32 scroll=ywrap

```

Documentation for `mode_option` can be found at [linux.git/tree/Documentation/fb/modedb.txt](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/fb/modedb.txt)

To prevent your customizations being overwritten when the package is updated, copy this file to `/etc/modprobe.d/uvesafb.conf`:

```
# cp /usr/lib/modprobe.d/uvesafb.conf /etc/modprobe.d/uvesafb.conf

```

and then add an entry in the FILES section of `/etc/mkinitcpio.conf` pointing to your configuration file, like so:

```
FILES="/etc/modprobe.d/uvesafb.conf"

```

To make changes take effect you need to regenerate the _initramfs_ images of the kernel.

```
# mkinitcpio -p linux

```

Reboot the system to see the changes take effect.

### Optimizing Resolution

A list of possible resolutions can be generated via the following command:

```
$ cat /sys/bus/platform/drivers/uvesafb/uvesafb.0/vbe_modes

```

Users can then modify `/usr/lib/modprobe.d/uvesafb.conf` with any entry returned above.

### Checking Current Resolution

Either of following commands can be used to show the current framebuffer resolution as a sanity check to see that settings are honored:

```
$ cat /sys/devices/virtual/graphics/fbcon/subsystem/fb0/virtual_size

```

```
$ cat /sys/class/graphics/fb0/virtual_size

```

## kernel module parameters

If you compile your own kernel, then you can also compile uvesafb into the kernel and run v86d later, e.g. from `/etc/rc.local`. In this case, the options can be passed as [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") in the format video=uvesafb:<options>. Please note that this solution is not viable in the case you want to combine uvesafb with 915resolution as suggested below.

## Uvesafb and 915resolution

In the following, we address a more complex scenario. Many intel video chipsets for widescreen laptops are known to have a buggy BIOS, which does not support the main, native resolution of the wide screen! For this reason, 915resolution was created to patch the BIOS at boot time and allow the X server to use the widescreen resolution. Nowadays, the X server is able to do this without the help of 915resolution. However, 915resolution can be combined with uvesafb in order to obtain a widescreen framebuffer, without any need to launch X at all. In this case, we need to load uvesafb after having run 915resolution, so that uvesafb can resort to the proper resolution.

### 915resolution-static

In this scenario, 915resolution needs to be compiled statically (since it is going to be in an initramfs, it can not be linked to external libraries). Thus you CAN NOT use the 915resolution package in the [community] repo. Look instead for [915resolution-static](https://aur.archlinux.org/packages/915resolution-static/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/915resolution-static)]</sup> in the AUR. It compiles 915 resolution statically and provides a 915 resolution hook, so you can run 915resolution before loading uvesafb and get the patched resolution. So install 915resolution-static via makepkg and [pacman](/index.php/Pacman "Pacman").

### The resolution

You need to edit the 915resolution hook in order to define the BIOS mode you want to replace and and the resolution you want to get. You can get information about all the options for 915resolution with:

```
$ 915resolution -h

```

Edit `/lib/initcpio/hooks/915resolution` and modify the options for 915resolution:

```
run_hook ()
{
   msg -n ":: Patching the VBIOS..."
   /usr/sbin/915resolution 5c 1280 800
   msg "done."
}

```

As default 5c is the code of the BIOS mode to replace. You can get a list of the available BIOS video modes with the command `915resolution -l`.

**Note:** You want to choose the code of a mode that you _DO NOT_ need (neither in the framebuffer nor in X), because 915resolution will replace it with a new user-defined mode. In the above example, `1280 800` is the new desired resolution.

### The Hooks Array

Add the 915resolution hook and, after it, the v86d hook to HOOKS in `/etc/mkinitcpio.conf`. Put them before the hooks for the keymap, the resume from suspension and the filesystems.

```
HOOKS="base udev 915resolution v86d ..."

```

Then you need to regenerate your initramfs with mkinitcpio (adjust the following command to your setup):

```
mkinitcpio -p linux

```

## Troubleshooting

### Uvesafb cannot reserve memory

Check if you forgot to remove any `vga=xxx` kernel parameter -- this overrides the UVESA framebuffer with a standard VESA one.

Or try to add "video=vesa:off vga=normal" to kernel cmdline.

### Error: "pci_root PNP0A08:00 address space collision + Uvesafb cannot reserve memory"

This occurs on the Acer Aspire One 751h with the 2.6.34-ARCH kernel; whether it also occurs on other systems is unknown. Even without another framebuffer interfering with the uvesafb setup, uvesafb cannot reserve the necessary memory region.

You can fix this issue by adding the following to the kernel parameters in your bootloader's configuration.

```
pci=nocrs

```

## See also

*   [Uvesafb Kernel Page](https://www.kernel.org/doc/Documentation/fb/uvesafb.txt)
*   [Gentoo's uvesafb Page](http://dev.gentoo.org/~spock/projects/uvesafb)
*   [VESA mode numbers](http://infosnews.5cz.de/VESA_BIOS_Extensions.html#VBE_mode_numbers)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Uvesafb&oldid=392773](https://wiki.archlinux.org/index.php?title=Uvesafb&oldid=392773)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Graphics](/index.php/Category:Graphics "Category:Graphics")
*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")