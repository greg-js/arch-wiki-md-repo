# IBM ThinkPad X60s

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
*   [6 Suspend](#Suspend)
    *   [6.1 With pm-utils](#With_pm-utils)

## Installation

First note that this laptop is available with two different processors.

*   Core Duo

NaN

*   Core **2** Duo

NaN

A basic Arch Linux installation will do just fine for almost everything. Select the i686 or x86_64 version as indicated above. Install from a USB CD drive or a USB flash drive following the instructions in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

It is easiest to do the initial installation with a wired ethernet connection which you can set up in the installation menu. In the base install package selection you can install the packages required for the wireless networking

```
[*] wireless-tools
[*] iwlwifi-3945-ucode

```

Follow the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") step by step to install sudo, add users, add to groups, video card driver, then install Xorg, and a desktop environment.

## Graphics

See [Intel graphics](/index.php/Intel_graphics "Intel graphics"). The required driver is xf86-video-intel.

## Ethernet

Gigabit ethernet works out of the box with the e1000e kernel module.

## Wireless Networking

See [Wireless network configuration#iwl3945.2C iwl4965 and iwl5000-series](/index.php/Wireless_network_configuration#iwl3945.2C_iwl4965_and_iwl5000-series "Wireless network configuration").

## Special Keys

See [http://www.thinkwiki.org/wiki/How_to_get_special_keys_to_work](http://www.thinkwiki.org/wiki/How_to_get_special_keys_to_work).

## Suspend

### With pm-utils

See the article on [pm-utils](/index.php/Pm-utils "Pm-utils"). This works fine.

Retrieved from "[https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_X60s&oldid=376825](https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_X60s&oldid=376825)"