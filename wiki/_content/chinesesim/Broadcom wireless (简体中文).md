## Contents

*   [1 介绍](#.E4.BB.8B.E7.BB.8D)
*   [2 Determine which driver you need/can use](#Determine_which_driver_you_need.2Fcan_use)
*   [3 Getting the driver](#Getting_the_driver)
    *   [3.1 brcmsmac/brcmfmac](#brcmsmac.2Fbrcmfmac)
    *   [3.2 b43/b43legacy](#b43.2Fb43legacy)
        *   [3.2.1 Loading the b43/b43legacy kernel module](#Loading_the_b43.2Fb43legacy_kernel_module)
    *   [3.3 broadcom-wl](#broadcom-wl)
        *   [3.3.1 Loading the wl kernel module](#Loading_the_wl_kernel_module)
*   [4 加载多博通网卡的内核驱动模块](#.E5.8A.A0.E8.BD.BD.E5.A4.9A.E5.8D.9A.E9.80.9A.E7.BD.91.E5.8D.A1.E7.9A.84.E5.86.85.E6.A0.B8.E9.A9.B1.E5.8A.A8.E6.A8.A1.E5.9D.97)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 更新 Kernel 后设备无法访问](#.E6.9B.B4.E6.96.B0_Kernel_.E5.90.8E.E8.AE.BE.E5.A4.87.E6.97.A0.E6.B3.95.E8.AE.BF.E9.97.AE)
    *   [5.2 使用 broadcom-wl 驱动的设备不工作/不显示](#.E4.BD.BF.E7.94.A8_broadcom-wl_.E9.A9.B1.E5.8A.A8.E7.9A.84.E8.AE.BE.E5.A4.87.E4.B8.8D.E5.B7.A5.E4.BD.9C.2F.E4.B8.8D.E6.98.BE.E7.A4.BA)
    *   [5.3 使用 broadcom-wl 驱动时接口交换](#.E4.BD.BF.E7.94.A8_broadcom-wl_.E9.A9.B1.E5.8A.A8.E6.97.B6.E6.8E.A5.E5.8F.A3.E4.BA.A4.E6.8D.A2)
    *   [5.4 接口显示正常但是不能连接](#.E6.8E.A5.E5.8F.A3.E6.98.BE.E7.A4.BA.E6.AD.A3.E5.B8.B8.E4.BD.86.E6.98.AF.E4.B8.8D.E8.83.BD.E8.BF.9E.E6.8E.A5)
    *   [5.5 Suppressing console messages](#Suppressing_console_messages)
    *   [5.6 不能检测到设备 BCM43241](#.E4.B8.8D.E8.83.BD.E6.A3.80.E6.B5.8B.E5.88.B0.E8.AE.BE.E5.A4.87_BCM43241)
    *   [5.7 在连接到某些路由器时可能不稳定](#.E5.9C.A8.E8.BF.9E.E6.8E.A5.E5.88.B0.E6.9F.90.E4.BA.9B.E8.B7.AF.E7.94.B1.E5.99.A8.E6.97.B6.E5.8F.AF.E8.83.BD.E4.B8.8D.E7.A8.B3.E5.AE.9A)

## 介绍

博通对于其Wifi卡在 GNU/Linux 上的支持不好可谓是臭名昭著。直到最近，大部分的博通芯片要么是完全不被支持，或者需要用户自行修改内核。一组有限的无线芯片由不同的逆向工程提供支持（比如：`brcm4xxx`, `b43`。从 Kernel 2.6.24 开始，这些逆向工程 [`b43`](http://wireless.kernel.org/en/users/Drivers/b43) 的驱动已经被收录。

2008年8月，博通发布了GNU/ Linux上的 [802.11 Linux STA 驱动r](http://www.broadcom.com/support/802.11/linux_sta.php) 正式为其无线设备提供 GNU/Linux 支持。这些驱动是闭源的, 但博通承诺，在未来将以一种更加开放的方式提供支持。此外，它们不具有隐藏 ESSID 的功能。

在2010年9月，博通完全开源的硬件驱动[[1]](http://thread.gmane.org/gmane.linux.kernel.wireless.general/55418终于发布)。该驱动程序[ `brcm80211`](http://wireless.kernel.org/en/users/Drivers/brcm80211)已被列入到自2.6.37之后的内核中。随着2.6.39发布，这些驱动程序已被重新命名为 `brcmsmac`和 `brcmfmac`。

在写这篇文章时，使用博通芯片组的用户有以下三种选择：

| Driver | Description |
| brcmsmac/brcmfmac | 开源内核驱动 |
| b43 | 逆向工程内核驱动 |
| broadcom-wl | 专有的 Broadcom STA 驱动 |

## Determine which driver you need/can use

First, determine your card's [PCI-ID](https://en.wikipedia.org/wiki/PCI_configuration_space "wikipedia:PCI configuration space"). Type the following (case-sensitive) command into a console:

```
$ lspci -vnn | grep 14e4:

```

Then check your card against this [list of supported b43 devices](http://linuxwireless.org/en/users/Drivers/b43#Supported_devices) and this [list of supported brcm80211 devices](http://linuxwireless.org/en/users/Drivers/brcm80211#Supported_Chips).

## Getting the driver

### brcmsmac/brcmfmac

The `brcm80211` drivers have been included in the kernel since 2.6.37\. Since the release of 2.6.39, they have been renamed to `brcmsmac` (for PCI cards) and `brcmfmac` (for SDIO).

These drivers should be automatically loaded during startup and no further action should be required of the user. If the driver doesn't auto load, try the following commands.

```
# modprobe brcmsmac

```

or

```
# modprobe brcmfmac

```

**Note:** The `bcma` module can prevent some cards from showing up and may need to be [blacklisted](#Wi-Fi_card_does_not_work.2Fshow_up_since_kernel_upgrade_.28brcmsmac.29).

**Note:** Since linux 3.3.1 the `brcmsmac` driver depends on the `bcma` module and blacklisting is no longer required.

**Note:** [wireless.kernel.org](http://wireless.kernel.org/en/users/Drivers/brcm80211) states that brcm80211 does not support older PCI/PCI-E chips with ssb backplane.

### b43/b43legacy

The drivers are included in the kernel since 2.6.24.

#### Loading the b43/b43legacy kernel module

Verify which module you need by looking up your device [here](http://wireless.kernel.org/en/users/Drivers/b43#Known_PCI_devices). You can also check by computer model [here](http://linuxwireless.org/en/users/Drivers/b43/devices). Blacklist the other module (either `b43` or `b43legacy`) to prevent possible problems/confusion. For instructions, see [Kernel_modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

Install the appropriate [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) or [b43-firmware-legacy](https://aur.archlinux.org/packages/b43-firmware-legacy/) package from the [AUR](/index.php/AUR "AUR").

You can now configure your device.

### broadcom-wl

**Warning:** This driver is more likely to cause problems than to resolve them. Most of the problems reported by users on Broadcom chips are caused by this driver. Using this is HIGHLY NOT recommended. Before you even think of trying out this one, make sure to try the other drivers first.

For users of the `broadcom-wl` driver, there is a PKGBUILD available in the AUR ([broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)). You can also download this driver directly from [Broadcom](http://www.broadcom.com/support/802.11/linux_sta.php). However, the PKGBUILD method is strongly encouraged, as that way will have [pacman](/index.php/Pacman "Pacman") track all of the files.

#### Loading the wl kernel module

The `wl` module may need to be manually loaded if there are other usable modules present. Before loading the `wl` module, remove the `b43` or other module that may have been automatically loaded instead:

```
# rmmod b43

```

Also unload `ssb`, if loaded:

```
# rmmod ssb

```

**Note:** Failure to unload `ssb` may result in the wireless interface not being created.

Load the `wl` module

```
# modprobe wl

```

The `wl` module should automatically load `lib80211` or `lib80211_crypt_tkip`. Check with `lsmod` to see if this is the case. If not, you may need to add one of those two modules as well.

```
# modprobe lib80211

```

or

```
# modprobe lib80211_crypt_tkip

```

If you installed the driver directly from Broadcom, you may also need to update the dependencies:

```
# depmod -a

```

To make the module load at boot, add `wl` (and `lib80211`/`lib80211_crypt_tkip`, if needed) to your MODULES array in `/etc/rc.conf`.

```
MODULES=(... wl...)

```

You can also blacklist other modules (to prevent them from interfering) in `/etc/modprobe.d/modprobe.conf`. To blacklist a module just append a new line with the syntax `blacklist <module name>`:

```
blacklist b43
blacklist ssb

```

**Warning:** Broadcom Corporation BCM4311 802.11b/g WLAN [14e4:4311] does not work with blacklisting `b43` and `ssb`.

## 加载多博通网卡的内核驱动模块

在我的戴尔 Inspiron笔记本上，拥有BCM4401有线网卡和BCM4328无线网卡。如果我仅仅是移除b43模块，我能加载wl无线驱动，但是没有无线网卡显示。然而，如果我先移除有线网卡的b44(和ssb)驱动模块，然后加载wl无线驱动，则会有一个eth0无线网卡设备出现。之后，再重新加载b44驱动，这样就同时能有一个eth1的有线网卡出现。

短文版:

*   Put "lib80211_crypt_tkip" and "wl" at the BEFORE b44 (if you have it) position in MODULES= 在 /etc/rc.conf 模块部分，b44(如果你需要这个驱动的话)之前加入lib80211_crypt_tkip wl
*   不要忘记把 b43 模块加入黑名单
*   您的无线网卡设备为eth0
*   您的有线网卡设备为eth1
*   两者能同是正常工作

## 故障排除

各种可以纠正的错误。

### 更新 Kernel 后设备无法访问

Since the 3.3.1 kernel the **bcma** module was introduced. If using a **brcm80211** driver be sure it has not been [blacklisted](/index.php/Kernel_modules#Blacklisting "Kernel modules"). If using a **b43** driver be sure the it has been.

### 使用 broadcom-wl 驱动的设备不工作/不显示

Be sure the correct modules are blacklisted and occasionally it may be necessary to blacklist the **brcm80211** drivers if accidentally detected before the **wl** driver is loaded. Furthermore, update the modules dependencies `depmod -a`, verify the wireless interface with `ip addr`, kernel upgrades will require an upgrade of the non-[DKMS](/index.php/DKMS "DKMS") package.

### 使用 broadcom-wl 驱动时接口交换

使用 broadcom-wl 驱动也许会发现它们的以太网和 Wi-Fi 接口交换了。查看这里（[device naming](/index.php/Network_configuration#Device_names "Network configuration")）的解决方案。

### 接口显示正常但是不能连接

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

To disable those messages, increase the loglevel of printk messages that get through to the console.

Create a file in `/etc/sysctl.d/` called `printk.conf` or something similar:

 `printk.conf` 
```

kernel.printk = 3 3 3 3

```

Refere to [StackExchange thread](http://unix.stackexchange.com/questions/44999/how-can-i-hide-messages-of-udev/45525#45525%7Cthis) for an explanation of this variable.

### 不能检测到设备 BCM43241

无论是 `lspci` 还是 `lsusb` 都不能检测到设备。这个问题目前无法解决。 请在解决后删除此节点。

### 在连接到某些路由器时可能不稳定

如果没有其他的解决方法，安装[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)，或者使用[低版本的驱动](/index.php/Downgrading_packages "Downgrading packages")。