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

	This processor requires the i686 (32-bit) version of Arch Linux. The two RAM slots physically support 2x2GB=4GB RAM. However with a 32-bit kernel only up to ~3GB will be accessible. Unfortunately due to a chipset limitation, even compiling a kernel with the Physical Address Extension (PAE) option (CONFIG_HIGHMEM64G) [[1]](https://aur.archlinux.org/packages.php?ID=24469) will not allow access to more than 3GB.

*   Core **2** Duo

	This processor can run the x86_64 (64-bit) version of Arch Linux, and this is recommended in this case. The full 4GB RAM will be available with the standard Arch x86_64 kernel.

A basic Arch Linux installation will do just fine for almost everything. Select the i686 or x86_64 version as indicated above. Install from a USB CD drive or a USB flash drive following the instructions in the [Installation guide](/index.php/Installation_guide "Installation guide").

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

See [Wireless network configuration#iwl3945.2C iwl4965 and iwl5000-series](/index.php/Wireless_network_configuration#iwl3945.2C_iwl4965_and_iwl5000-series "Wireless network configuration").

## Special Keys

See [http://www.thinkwiki.org/wiki/How_to_get_special_keys_to_work](http://www.thinkwiki.org/wiki/How_to_get_special_keys_to_work).

## Suspend

### With pm-utils

See the article on [pm-utils](/index.php/Pm-utils "Pm-utils"). This works fine.