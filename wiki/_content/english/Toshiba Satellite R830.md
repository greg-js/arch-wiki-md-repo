## Wi-Fi & Ethernet

Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01) and Intel Corporation 82579V Gigabit Ethernet with kernel 3.8 work out of the box.

## Brightness

xbacklight from [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) works fine.

## Brightness control after Suspend and resume

Brightness control works until sleep but after resume it does not.

In the past, adding `acpi_osi=Linux acpi_backlight=vendor` to kernel-line (see [Kernel Parameters](/index.php/Kernel_parameters#When_starting_the_kernel "Kernel parameters")) helped me.

A better solution that works on all DEs I've tested (XFCE,Gnome, Cinnamon) is using the `video.disable_backlight_sysfs_if=1` kernel paramater. This should not be combined with the previously-mentioned kernel parameters.

There is another solution here: [https://bbs.archlinux.org/viewtopic.php?id=132044](https://bbs.archlinux.org/viewtopic.php?id=132044)

Another possibility is using a custom xorg configuration file. *(Ignored by Gnome 3.16+)*

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