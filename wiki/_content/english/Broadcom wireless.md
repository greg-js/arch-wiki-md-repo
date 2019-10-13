Related articles

*   [Wireless](/index.php/Wireless "Wireless")

This article details how to install and setup a Broadcom wireless network device.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 History](#History)
*   [2 Driver selection](#Driver_selection)
*   [3 Installation](#Installation)
    *   [3.1 brcm80211](#brcm80211)
    *   [3.2 b43](#b43)
    *   [3.3 broadcom-wl](#broadcom-wl)
        *   [3.3.1 Offline installation](#Offline_installation)
        *   [3.3.2 Manually](#Manually)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Setting broadcom-wl in monitor mode](#Setting_broadcom-wl_in_monitor_mode)
    *   [4.2 Device inaccessible after kernel upgrade](#Device_inaccessible_after_kernel_upgrade)
    *   [4.3 Device with broadcom-wl driver not working/showing](#Device_with_broadcom-wl_driver_not_working/showing)
    *   [4.4 Interfaces swapped with broadcom-wl](#Interfaces_swapped_with_broadcom-wl)
    *   [4.5 Interface is showing but not allowing connections](#Interface_is_showing_but_not_allowing_connections)
    *   [4.6 Suppressing console messages](#Suppressing_console_messages)
    *   [4.7 Device BCM43241 not detected](#Device_BCM43241_not_detected)
    *   [4.8 Connection is unstable with some routers](#Connection_is_unstable_with_some_routers)
    *   [4.9 No 5GHz for BCM4360 (14e4:43a0) / BCM43602 (14e4:43ba) devices](#No_5GHz_for_BCM4360_(14e4:43a0)_/_BCM43602_(14e4:43ba)_devices)
    *   [4.10 Device works intermittently](#Device_works_intermittently)

## History

Broadcom has a noted history with its support for Wi-Fi devices regarding GNU/Linux. For a good portion of its initial history, Broadcom devices were either entirely unsupported or required the user to tinker with the firmware. The limited set of wireless devices that were supported were done so by a reverse-engineered driver. The reverse-engineered `b43` driver was introduced in the 2.6.24 kernel.

In August 2008, Broadcom released the [802.11 Linux STA driver](http://www.broadcom.com/support/802.11/linux_sta.php) officially supporting Broadcom wireless devices on GNU/Linux. This is a restrictively licensed driver and it does not work with hidden ESSIDs, but Broadcom promised to work towards a more open approach in the future.

In September 2010, Broadcom [released](http://thread.gmane.org/gmane.linux.kernel.wireless.general/55418) a fully open source driver. The [brcm80211](http://wireless.kernel.org/en/users/Drivers/brcm80211) driver was introduced in the 2.6.37 kernel and in the 2.6.39 kernel it was sub-divided into the `brcmsmac` and `brcmfmac` drivers.

The types of available drivers are:

| Driver | Description |
| brcm80211 | Kernel driver mainline version (recommended) |
| b43 | Kernel driver reverse-engineered version |
| broadcom-wl | Broadcom driver with restricted license |

## Driver selection

To know what driver(s) are operable on the computer's Broadcom wireless network device, the [device ID](https://en.wikipedia.org/wiki/PCI_configuration_space "wikipedia:PCI configuration space") and chipset name will need to be detected. Cross-reference them with the driver list of supported [brcm80211](https://wireless.wiki.kernel.org/en/users/Drivers/brcm80211#supported_chips) and [b43](https://wireless.wiki.kernel.org/en/users/Drivers/b43#list_of_hardware) devices.

```
$ lspci -vnn -d 14e4:

```

## Installation

### brcm80211

The kernel contains two built-in open-source drivers: **brcmfmac** for native FullMAC and **brcmsmac** for mac80211-based SoftMAC. They should be automatically loaded when booting.

**Note:**

*   **brcmfmac** supports newer chipsets, and supports AP mode, P2P mode, or hardware encryption.
*   **brcmsmac** only supports old chipsets like BCM4313, BCM43224, BCM43225.

### b43

Two reverse-engineered open-source drivers are built-in to the kernel: **b43** and **b43legacy**. b43 supports most newer Broadcom chipsets, while the b43legacy driver only supports the early BCM4301 and BCM4306 rev.2 chipsets. To avoid erroneous detection of your WiFi card's chipset, [blacklist](/index.php/Blacklist "Blacklist") the unused driver.

Both of these drivers require non-free firmware to function. Install [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) or [b43-firmware-classic](https://aur.archlinux.org/packages/b43-firmware-classic/).

**Note:**

*   BCM4306 rev.3, BCM4311, BCM4312 and BCM4318 rev.2 have been noticed to experience problems with **b43-firmware**. Use [b43-firmware-classic](https://aur.archlinux.org/packages/b43-firmware-classic/) for these cards instead.
*   BCM4331 noticed to have problems with **b43-firmware-classic**. Use [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) for this card instead.

### broadcom-wl

There are two variants of the restrictively licensed driver:

*   the regular variant: [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)
*   the [DKMS](/index.php/DKMS "DKMS") variant: [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms)

**Tip:** The DKMS variant [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms)

*   is kernel agnostic. This means it supports different kernels you may use (e.g. [linux-ck](https://aur.archlinux.org/packages/linux-ck/)).
*   is kernel-release agnostic, too. It will be automatically rebuilt after every kernel upgrade or fresh installation. If you use [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) or another kernel release dependant variant (e.g. [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/)), it may happen that kernel upgrades break wireless from time to time until the packages are in sync again.
*   will need the [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) package for the installed kernel(s) in order to build the module. Those packages are optional to the DKMS package and will need to be installed manually.

#### Offline installation

An Internet connection is the ideal way to install the **broadcom-wl** driver; many newer laptops with Broadcom cards forgo Ethernet ports, so a USB Ethernet adapter or [Android tethering](/index.php/Android_tethering "Android tethering") may be helpful. If you have neither, you'll need to first install the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group during installation. Then, use another Internet-connected computer to download [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) and the driver tarball from the AUR, and install them in that order.

#### Manually

**Warning:** This method is not recommended. Drivers that are un-tracked can become problematic or nonfunctional on system updates.

Install the appropriate driver for your system architecture from [Broadcom's website](https://www.broadcom.com/support/?gid=1). After this, to avoid driver/module collisions with similar modules and make the driver available, do:

```
# rmmod b43
# rmmod ssb
# modprobe wl

```

The *wl* module should automatically load *lib80211* or *lib80211_crypt_tkip* otherwise they will have to be manually loaded.

If the driver does not work at this point, you may need to update dependencies:

```
# depmod -a

```

To make the module load at boot, refer to [Kernel modules](/index.php/Kernel_modules "Kernel modules"). It is recommending that you [blacklist](/index.php/Blacklist "Blacklist") conflicting modules.

## Troubleshooting

### Setting broadcom-wl in monitor mode

Monitor mode is used to capture 802.11 frames over the air. This can be useful for diagnosing issues on a network or testing the security of your wireless network. Often, monitor mode is required to capture certain frames for wireless penetration testing, but it may be unethical or even illegal to capture frames on any network you do not own, manage or have permission to perform penetration testing against.

To set broadcom-wl in monitor mode you have to set 1 to `/proc/brcm_monitor0)`:

```
# echo 1 > /proc/brcm_monitor0

```

It will create a new network interface called `prism0`.

To work in monitor mode, use this newly created network interface.

### Device inaccessible after kernel upgrade

Since the 3.3.1 kernel the **bcma** module was introduced. If using a **brcm80211** driver be sure it has not been [blacklisted](/index.php/Kernel_modules#Blacklisting "Kernel modules"). It should be blackisted if using a **b43** driver.

If you are using [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl), uninstall and reinstall it after upgrading your kernel or switch to [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) package.

### Device with broadcom-wl driver not working/showing

Be sure the correct modules are blacklisted and occasionally it may be necessary to blacklist the **brcm80211** drivers if accidentally detected before the **wl** driver is loaded. Furthermore, update the modules dependencies `depmod -a`, verify the wireless interface with `ip addr`, kernel upgrades will require an upgrade of the non-[DKMS](/index.php/DKMS "DKMS") package.

### Interfaces swapped with broadcom-wl

Users of the broadcom-wl driver may find their Ethernet and Wi-Fi interfaces have been swapped. See [Network configuration#Network interfaces](/index.php/Network_configuration#Network_interfaces "Network configuration") for an answer.

### Interface is showing but not allowing connections

Append the following [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"):

```
b43.allhwsupport=1

```

### Suppressing console messages

You may continuously get some verbose and annoying messages during the boot, similar to

```
phy0: brcms_ops_bss_info_changed: arp filtering: enabled true, count 0 (implement)
phy0: brcms_ops_bss_info_changed: qos enabled: false (implement)
phy0: brcms_ops_bss_info_changed: arp filtering: enabled true, count 1 (implement)
enabled, active

```

To disable those messages, increase the loglevel of printk messages that get through to the console - see [Silent boot#sysctl](/index.php/Silent_boot#sysctl "Silent boot").

### Device BCM43241 not detected

This device will not display with either `lspci` nor `lsusb`; there is no known solution yet. Please remove this section when resolved.

### Connection is unstable with some routers

If no other approaches help, install [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), or use a [previous driver version](/index.php/Downgrading_packages "Downgrading packages").

### No 5GHz for BCM4360 (14e4:43a0) / BCM43602 (14e4:43ba) devices

Issue appears to be linked to a [channel issue](https://askubuntu.com/questions/749420/wireless-lost-ability-to-use-5ghz-pce-ac68). Changing the wireless channel to a lower channel number (like 40) seems to allow connection to 5GHz bands.

### Device works intermittently

In some cases (e.g. using BCM4331 and [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/)), wifi connection works intermittently. One way to fix this is to check if the card is *hard-blocked* or *soft-blocked* by kernel, and if it is, unblock it with [rfkill](/index.php/Rfkill "Rfkill").