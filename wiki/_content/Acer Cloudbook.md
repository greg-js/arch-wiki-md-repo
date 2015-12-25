# Acer Cloudbook

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Hardware](#Hardware)
*   [2 Installation](#Installation)
    *   [2.1 BIOS configuration](#BIOS_configuration)
    *   [2.2 Kernel parameters](#Kernel_parameters)
    *   [2.3 Installation](#Installation_2)
*   [3 Post-installation](#Post-installation)
    *   [3.1 Issue with GDM](#Issue_with_GDM)

## Hardware

**Processor:** Intel Celeron N3050 @ 1.60GHz

**Video:** Intel Corporation Device 22dc (rev 21)

**Audio:** Intel Corporation Device 2284 (rev 21)

**Wireless NIC:** Intel Corporation Dual Band Wireless AC 3160 (rev 83)

## Installation

_**Installation made with the 2015_12_01 image, which includes the kernel version 4.2.5.**_

### BIOS configuration

*   Touchpad: Basic
*   Boot Mode: Legacy
*   Boot priority order: the eMMC block device needs to have a lower boot priority than the USB bootable device.

Then save and exit.

### Kernel parameters

Without these options, the installation image won't load at all:

*   edd=off
*   noapic

Without this option, the kernel will automatically load the **pinctrl_cherryview** module which is incompatible with the Acer Cloudbook:

*   modprobe.blacklist=pinctrl_cherryview

If that module gets loaded, multiple ACPI issues will arise; systemd-udevd will freeze and report multiple errors.

Therefore these parameters needs to be added at the end of the kernel parameters' line of the boot launcher:

```
linux /vmlinuz-linux ... edd=off noapic modprobe.blacklist=pinctrl_cherryview

```

### Installation

*   Everything should function without any issues thanks to the previous kernel parameters, proceed to install the image as normal.
    *   The module for the wireless NIC is included with the kernel, so Wi-Fi works out of the box.
*   Do not forget to add **edd=off noapic modprobe.blacklist=pinctrl_cherryview** to the kernel parameters of the boot launcher's configuration file. With GRUB, these options can be added to the _GRUB_CMDLINE_LINUX=_ in the **/etc/default/grub** file. Do not forget that **/boot/grub/grub.cfg** needs to be regenerated.

Example:

```
GRUB_CMDLINE_LINUX="quiet edd=off noapic modprobe.blacklist=pinctrl_cherryview"

```

## Post-installation

### Issue with GDM

If Gnome/GDM is installed and started, the login page will flicker up-to the point that it becomes nonfunctional. To resolve this issue, simply uncomment this line in the file **/etc/gdm/custom.conf** and restart GDM:

```
[daemon]
WaylandEnable=false

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Cloudbook&oldid=413367](https://wiki.archlinux.org/index.php?title=Acer_Cloudbook&oldid=413367)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")