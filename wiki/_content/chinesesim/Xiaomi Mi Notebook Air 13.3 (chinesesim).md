| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working |  ? |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working |  ? |
| Function/Multimedia Keys | Working |  ? |

小米笔记本 Air 13.3 是一款铝合金的超级本，由小米公司生产，目前只能在中国购买，或者通过在线进口网站购买。第一代小米 Air 使用 Intel Core i5 6200U @ 2.3 Ghz a和 NVIDIA GeForce 940MX。小米笔记本以较低的价格提供了不错的性能。

如果你照着下面的步骤来安装，应该不会有任何问题

## Contents

*   [1 安装前准备](#.E5.AE.89.E8.A3.85.E5.89.8D.E5.87.86.E5.A4.87)
*   [2 显卡设置](#.E6.98.BE.E5.8D.A1.E8.AE.BE.E7.BD.AE)
    *   [2.1 只使用集显](#.E5.8F.AA.E4.BD.BF.E7.94.A8.E9.9B.86.E6.98.BE)
    *   [2.2 Intel/Nvidia 混合配置](#Intel.2FNvidia_.E6.B7.B7.E5.90.88.E9.85.8D.E7.BD.AE)
*   [3 输入](#.E8.BE.93.E5.85.A5)
    *   [3.1 触摸板](#.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [3.2 Fn功能键](#Fn.E5.8A.9F.E8.83.BD.E9.94.AE)
*   [4 显示校准](#.E6.98.BE.E7.A4.BA.E6.A0.A1.E5.87.86)
*   [5 NVME SSD](#NVME_SSD)
    *   [5.1 linux-nvme](#linux-nvme)
*   [6 硬件信息](#.E7.A1.AC.E4.BB.B6.E4.BF.A1.E6.81.AF)
*   [7 排难解惑](#.E6.8E.92.E9.9A.BE.E8.A7.A3.E6.83.91)
    *   [7.1 背光灯](#.E8.83.8C.E5.85.89.E7.81.AF)
    *   [7.2 WiFi](#WiFi)

## 安装前准备

想要从Arch安装媒介引导启动十分简单。首先插入U盘，然后按开机键，并在开机过程中按F2，会进入UEFI设置：

*   安全 -> 设置密码
*   安全-> 关闭 Secure Boot
*   点击设置密码，但是把"新密码"一栏留空，可以实现重置密码

请参考 [Installation_guide_(简体中文)](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")获取更多安装帮助，安装过程应该不会有什么问题。

**Note:** 你的SSD硬盘叫 `nvme0n1`, 而不是 `sda`.

## 显卡设置

小米笔记本同时配有Intel的集成显卡和Nvidia的独立显卡。

### 只使用集显

如果你想完全禁用Nvidia GPU以提高续航，可以操作如下：

*   安装 [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)
*   屏蔽内核模块 [nvidia](https://www.archlinux.org/packages/?name=nvidia) 和 [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) ，参见 [Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")

 `/etc/modprobe.d/nouveau.conf` 
```
blacklist nouveau
blacklist nvidia
```

*   安装 [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) ，参见 [turn off the card](/index.php/Bumblebee#Power_management "Bumblebee")

 `/etc/modprobe.d/bbswitch`  `options bbswitch load_state=0 unload_state=0` 

### Intel/Nvidia 混合配置

You can enable hybrid GPUs by either using [Bumblebee](/index.php/Bumblebee "Bumblebee") or [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"). Bumblebee is generally better for battery-life and compatibility but not officially supported by NVIDIA.

Refer to the respective articles.

## 输入

### 触摸板

想要正常使用触摸板，你需要安装 [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)。如果你使用 [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)，你的触摸板会像触摸屏那样工作（e.g. 你在触摸板上的任何操作都直接映射到屏幕上）。如果你使用 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) (强烈不建议，因为它已经弃用了，参见 [Synaptics](/index.php/Synaptics "Synaptics")) ，触摸板很可能只能偶尔正常工作。 [libinput](https://www.archlinux.org/packages/?name=libinput) 配置文件结合 如下XOrg配置，可以使用双指手续，轻触点击，双指，三指点击等（双指点击等价与按住鼠标右键，三指点击等价于按住鼠标中键）。

 `/etc/X11/xorg.conf.d/20-touchpad.conf` 
```
Section "InputClass"
        Identifier "libinput touchpad"
        Driver "libinput"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Option "Tapping" "on"
        Option "ClickMethod" "clickfinger"
        Option "NaturalScrolling" "true"
EndSection
```

### Fn功能键

默认Fn键是使能的，比如 按 F1 可以静音。 如果按这些Fn功能键没有反应，那么很可能你使用的是窗口管理器 [Window_manager_(简体中文)](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)") 而不是桌面环境 [Desktop_environment_(简体中文)](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")。这时你需要添加相应的配置，比如利用[Xbindkeys](/index.php/Xbindkeys "Xbindkeys") 或 [i3](/index.php/I3 "I3")的 `bindsym`。

大多数Fn功能键返回特定的键码，下面是一张表格：

| Fn-F-Key | Keycode |
| `F1` | `XF86AudioMute` |
| `F2` | `XF86AudioLowerVolume` |
| `F3` | `XF86AudioRaiseVolume` |
| `F4` | `XF86MonBrightnessDown` |
| `F5` | `XF86MonBrightnessUp` |
| `F6` | `Super_L + P` |
| `F7` | `无` |
| `F8` | `Super_L + Tab` |
| `F9` | `无` |
| `F10` | `Turns Keyboard backlight on/off` |
| `F11` | `Print` |
| `F12` | `Insert` |

## 显示校准

Factory display calibration is poor. In lieu of a colorimeter, try the [ICC profiles](/index.php/ICC_profiles "ICC profiles") at [tlvince/xiaomi-mi-notebook-air-13](https://github.com/tlvince/xiaomi-mi-notebook-air-13/tree/master/display-calibration).

## NVME SSD

### linux-nvme

Andy Lutomirski has created a patchset which fixes powersaving for NVME devices in Linux. Currently, this patch is not merged into mainline yet. Until it lands in mainline kernel use the AUR or repository linked below.

**linux-nvme** — Mainline linux kernel patched with Andy's patch for NVME powersaving APST.

	[https://github.com/damige/linux-nvme](https://github.com/damige/linux-nvme) || [linux-nvme](https://aur.archlinux.org/packages/linux-nvme/) (check out [[1]](http://linuxnvme.damige.net/) for compiled packages)

## 硬件信息

*lspci* 输出：

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 520 (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940MX] (rev ff)
02:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
03:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM951/PM951 (rev 01)

```

*lsusb* 输出：

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 8087:0a2b Intel Corp.
Bus 001 Device 002: ID 05c8:03a2 Cheng Uei Precision Industry Co., Ltd (Foxlink)
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## 排难解惑

### 背光灯

使用[xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight)和默认配置，你无法控制背光灯，因为背光灯路径不符合标准。想要解决这个问题，你需新建一个X-Org配置文件：

 `/etc/X11/xorg.conf.d/10-backlight.conf` 
```
Section "Device" 
        Identifier "Card0" 
        Driver     "intel" 
        Option     "Backlight"  "intel_backlight" 
        BusID      "PCI:0:2:0" 
EndSection
```

### WiFi

如果你无法自动检测WIFI驱动，可能是因为两个驱动冲突了，你可以使用 `rfkill list`解决它。屏蔽掉其中一个有问题的驱动可以这么设置：

 `/etc/modprobe.d/blacklist.conf`  `blacklist acer-wmi` 

注意，这个问题Linux 4.9以上的版本中已经解决了。