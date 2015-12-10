# Toshiba Satellite R830

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Wi-Fi & Ethernet

Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01) and Intel Corporation 82579V Gigabit Ethernet with kernel 3.8 work out of the box.

## Brightness

xbacklight from [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) works fine.

## Suspend and resume

Brightness control works until sleep but after resume it does not.

Adding `acpi_osi=Linux acpi_backlight=vendor` to kernel-line (see [Kernel Parameters](/index.php/Kernel_parameters#When_starting_the_kernel "Kernel parameters")) helped me.

There is another solution here: [https://bbs.archlinux.org/viewtopic.php?id=132044](https://bbs.archlinux.org/viewtopic.php?id=132044)

The above solution no longer works with modern kernels. Instead what did work is creating a custom xorg configuration file.

In a terminal type:

```
    sudo touch /usr/share/X11/xorg.conf.d/20-intel.conf

```

Now edit this file:

```
    sudo xdg-open /usr/share/X11/xorg.conf.d/20-intel.conf

```

Type the following code:

```
   Section "Device"
       Identifier  "card0"
       Driver      "intel"
       Option      "Backlight"  "intel_backlight"
       BusID       "PCI:0:2:0"
   EndSection

```

Save the file; log out and in again.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Toshiba_Satellite_R830&oldid=363544](https://wiki.archlinux.org/index.php?title=Toshiba_Satellite_R830&oldid=363544)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Toshiba](/index.php/Category:Toshiba "Category:Toshiba")