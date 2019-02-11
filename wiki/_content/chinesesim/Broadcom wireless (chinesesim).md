<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 介绍](#介绍)
*   [2 查看你可以使用何种驱动](#查看你可以使用何种驱动)
*   [3 获取驱动](#获取驱动)
    *   [3.1 brcm80211](#brcm80211)
    *   [3.2 b43/b43legacy](#b43/b43legacy)
    *   [3.3 broadcom-wl](#broadcom-wl)
        *   [3.3.1 加载broadcom-wl的内核模块](#加载broadcom-wl的内核模块)
*   [4 加载多博通网卡的内核驱动模块](#加载多博通网卡的内核驱动模块)
*   [5 故障排除](#故障排除)
    *   [5.1 更新 Kernel 后设备无法访问](#更新_Kernel_后设备无法访问)
    *   [5.2 使用 broadcom-wl 驱动的设备不工作/不显示](#使用_broadcom-wl_驱动的设备不工作/不显示)
    *   [5.3 使用 broadcom-wl 驱动时接口交换](#使用_broadcom-wl_驱动时接口交换)
    *   [5.4 接口显示正常但是不能连接](#接口显示正常但是不能连接)
    *   [5.5 奇怪的报错信息](#奇怪的报错信息)
    *   [5.6 不能检测到设备 BCM43241](#不能检测到设备_BCM43241)
    *   [5.7 在连接到某些路由器时可能不稳定](#在连接到某些路由器时可能不稳定)

## 介绍

博通对于其Wifi卡在 GNU/Linux 上的支持不好可谓是臭名昭著。直到最近，大部分的博通芯片要么是完全不被支持，或者需要用户自行修改内核。一组有限的无线芯片由不同的逆向工程提供支持（比如：`brcm4xxx`, `b43`。从 Kernel 2.6.24 开始，这些逆向工程 [`b43`](http://wireless.kernel.org/en/users/Drivers/b43) 的驱动已经被收录。

2008年8月，博通发布了GNU/ Linux上的 [802.11 Linux STA 驱动](https://www.broadcom.cn/support/download-search/?pg=&pf=Wireless+LAN+Infrastructure&pn=&po=&pa=&dk=) 正式为其无线设备提供 GNU/Linux 支持。这些驱动是闭源的, 但博通承诺，在未来将以一种更加开放的方式提供支持。此外，它们不具有隐藏 ESSID 的功能。

在2010年9月，博通完全开源的硬件驱动[[1]](http://thread.gmane.org/gmane.linux.kernel.wireless.general/55418终于发布)。该驱动程序[ `brcm80211`](http://wireless.kernel.org/en/users/Drivers/brcm80211)已被列入到自2.6.37之后的内核中。随着2.6.39发布，这些驱动程序已被重新命名为 `brcmsmac`和 `brcmfmac`。

在写这篇文章时，使用博通芯片组的用户有以下三种选择：

| 驱动 | 描述 |
| brcmsmac/brcmfmac | 开源内核驱动 |
| b43 | 逆向工程内核驱动 |
| broadcom-wl | 专有的 Broadcom STA 驱动 |

## 查看你可以使用何种驱动

首先，向你的终端输入以下内容来检测网卡的 [PCI-ID](https://en.wikipedia.org/wiki/PCI_configuration_space "wikipedia:PCI configuration space"):

```
$ lspci -vnn | grep 14e4:

```

然后在以下列表中检查 [[2]](http://linuxwireless.org/en/users/Drivers/b43#b43驱动的支持设备列表) 以及 [[3]](http://linuxwireless.org/en/users/Drivers/brcm80211#brcm80211的支持设备列表).

## 获取驱动

### brcm80211

Kernel內建了两个开源驱动: **brcmfmac** 提供原生硬MAC支持， **brcmsmac** 提供基于mac80211的软MAC支持。 它们应该会在启动时自行加载。

**Note:**

*   **brcmfmac** 提供较新的芯片支持，并且支持AP模式，P2P模式，高级加密。
*   **brcmsmac** 仅提供对于较老芯片的支持，例如BCM4313, BCM43224, BCM43225。

### b43/b43legacy

**b43** 以及 **b43legacy**两个逆向工程驱动已经被內建在Kernel中。b43支持大部分的博通无线芯片组，而b43legacy驱动仅支持早期的BCM4301以及BCM4306 rev.2 芯片组。为了避免与别的驱动造成冲突，请 [blacklist](/index.php/Blacklist "Blacklist") 未使用的驱动。

这些驱动的运行都需要安装闭源固件，请从[AUR](/index.php/AUR "AUR")安装[b43-firmware](https://aur.archlinux.org/packages/b43-firmware/)， [b43-firmware-classic](https://aur.archlinux.org/packages/b43-firmware-classic/) 或者 [b43-firmware-legacy](https://aur.archlinux.org/packages/b43-firmware-legacy/) 。

**Note:**

*   BCM4306 rev.3, BCM4311, BCM4312 与 **b43-firmware** 固件不能良好的工作。对于这些芯片组请使用 [b43-firmware-classic](https://aur.archlinux.org/packages/b43-firmware-classic/) 代替。
*   BCM4331 与 **b43-firmware-classic** 固件不能良好的工作。 对于这些芯片组请使用 [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) 代替。

### broadcom-wl

[AUR](/index.php/AUR "AUR") 中有两个版本的Broadcom STA闭源驱动：

*   通常的 [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)
*   以及 [DKMS](/index.php/DKMS "DKMS") 版本 [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms)

**Tip:** DKMS版本 [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms)

*   可以在不同的Kernel中工作 (例如 [linux-ck](https://aur.archlinux.org/packages/linux-ck/)).
*   每次安装新的Kernel时，dkms都会重新构建驱动，如果你使用 [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) 或者其他依赖于单个Kernel版本的驱动 (例如 [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/)), 那么在更新Kernel或者使用新的Kernel时都有可能使驱动崩溃。

#### 加载broadcom-wl的内核模块

`wl` 模块可能会与其他模块冲突而无法加载。加载`wl`模块之前， 请移除`b43`或者其他可能造成冲突的模块：

```
# rmmod b43

```

如果 `ssb` 加载了，也请一并移除:

```
# rmmod ssb

```

**Note:** 错误的加载 `ssb` 可能导致无线界面无法被创建。

加载 `wl` 模块：

```
# modprobe wl

```

加载 `wl` 模块的同时 `lib80211` 或者 `lib80211_crypt_tkip` 应该也会被自动加载。 使用 `lsmod` 来进行检查，如果没有，请手动加载二者之一；

```
# modprobe lib80211

```

或

```
# modprobe lib80211_crypt_tkip

```

如果你直接从博通官方网站下载驱动冰安装，你可能同时需要更新依赖模块:

```
# depmod -a

```

如果模块无法在启动时加载，请将 `wl` (以及 `lib80211`/`lib80211_crypt_tkip`如果需要) 到 `/etc/rc.conf`的MODULES列：

```
# MODULES=(... wl...)

```

你也可以Blacklist掉可能冲突的模块，在 `/etc/modprobe.d/modprobe.conf`中加入:

```
# blacklist b43
# blacklist ssb

```

**Warning:** Broadcom Corporation BCM4311 802.11b/g WLAN [14e4:4311] 在Blacklist `b43` 以及 `ssb`后可能不工作。

## 加载多博通网卡的内核驱动模块

**b43**的博通无线网卡驱动与**b44**博通有线网卡驱动可能产生冲突，因此建议您使用**broadcom-wl**驱动

*   Put "lib80211_crypt_tkip" and "wl" at the BEFORE b44 (if you have it) position in MODULES= 在 /etc/rc.conf 模块部分，b44(如果你需要这个驱动的话)之前加入lib80211_crypt_tkip wl
*   不要忘记把 b43 模块加入黑名单
*   您的无线网卡设备为eth0
*   您的有线网卡设备为eth1
*   两者能同是正常工作

## 故障排除

各种可以纠正的错误。

### 更新 Kernel 后设备无法访问

如果您使用 **brcm80211** 请确保没有被 [blacklisted](/index.php/Kernel_modules#Blacklisting "Kernel modules")。如果你使用 **b43** 驱动确保它在工作。如果你使用**Broadcom STA**驱动的[broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)包，请重新安装或一劳永逸地切换成[broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms)。

### 使用 broadcom-wl 驱动的设备不工作/不显示

请查看dmesg是否存在报错信息，**broadcom-wl**经常发生奇怪的问题，重新加载Kernel模块或者重启一般能解决问题

### 使用 broadcom-wl 驱动时接口交换

使用 broadcom-wl 驱动也许会发现它们的以太网和 Wi-Fi 接口交换了。查看这里（[device naming](/index.php/Network_configuration#Device_names "Network configuration")）的解决方案。

### 接口显示正常但是不能连接

加入以下 [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"):

```
b43.allhwsupport=1

```

### 奇怪的报错信息

你可能会在启动时接收到奇怪的报错信息，类似于：

```
phy0: brcms_ops_bss_info_changed: arp filtering: enabled true, count 0 (implement)
phy0: brcms_ops_bss_info_changed: qos enabled: false (implement)
phy0: brcms_ops_bss_info_changed: arp filtering: enabled true, count 1 (implement)
enabled, active

```

一般情况下这并不影响驱动的正常工作，如果你想不想收到这些信息，可以提高printk的日志级别。

在`/etc/sysctl.d/`中创建一个`printk.conf`或者类似的配置文件:

 `printk.conf` 
```

kernel.printk = 3 3 3 3

```

最后`sysctl -p`确保配置被成功写入。

### 不能检测到设备 BCM43241

无论是 `lspci` 还是 `lsusb` 都不能检测到设备。这个问题目前无法解决。 请在解决后删除此部分。

### 在连接到某些路由器时可能不稳定

如果没有其他的解决方法，安装[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)，或者使用[低版本的驱动](/index.php/Downgrading_packages "Downgrading packages")。