Related articles

*   [IBM ThinkPad X60](/index.php/IBM_ThinkPad_X60 "IBM ThinkPad X60")
*   [Lenovo Thinkpad X60 Tablet](/index.php/Lenovo_Thinkpad_X60_Tablet "Lenovo Thinkpad X60 Tablet")

The IBM Thinkpad X60s is a small light laptop with a Core Duo or Core 2 Duo processor and [Intel graphics](/index.php/Intel_graphics "Intel graphics"). It has no internal optical drive. You can see the specs at [ThinkWiki](http://www.thinkwiki.org/wiki/Category:X60s), a wonderful resource with additional information.

## Contents

*   [1 Installation](#Installation)
*   [2 Graphics](#Graphics)
*   [3 Ethernet](#Ethernet)
*   [4 Wireless Networking](#Wireless_Networking)
*   [5 Special Keys](#Special_Keys)

## Installation

First note that this laptop is available with two different processors.

*   Core Duo

	This is a 32-bit processor, which is **not supported** by Arch Linux. Have a look at [Arch Linux 32](https://archlinux32.org/) instead.

*   Core **2** Duo

	This processor can run the x86_64 (64-bit) version of Arch Linux, and this is recommended in this case. The full 4GB RAM will be available with the standard Arch x86_64 kernel.

A basic Arch Linux installation will do just fine for almost everything. Install from a USB CD drive or a USB flash drive following the instructions in the [Installation guide](/index.php/Installation_guide "Installation guide").

It is easiest to do the initial installation with a wired ethernet connection which you can set up in the installation menu. In the base install package selection you can install the packages required for the wireless networking

```
[*] wireless-tools
[*] iwlwifi-3945-ucode

```

## Graphics

See [Intel graphics](/index.php/Intel_graphics "Intel graphics"). The required driver is xf86-video-intel.

**Tip:** When adjusting the screen backlight with the keyboard, flickering might be encountered. This can be fixed with adding `acpi_backlight=native` to the kernel command options.

## Ethernet

Gigabit ethernet works out of the box with the e1000e kernel module.

## Wireless Networking

See [Wireless network configuration#iwlegacy](/index.php/Wireless_network_configuration#iwlegacy "Wireless network configuration").

## Special Keys

See [http://www.thinkwiki.org/wiki/How_to_get_special_keys_to_work](http://www.thinkwiki.org/wiki/How_to_get_special_keys_to_work).