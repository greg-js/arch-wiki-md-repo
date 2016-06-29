**翻译状态：** 本文是英文页面 [Nouveau](/index.php/Nouveau "Nouveau") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-29，点击[这里](https://wiki.archlinux.org/index.php?title=Nouveau&diff=0&oldid=439290)可以查看翻译后英文页面的改动。

本文包含安装和配置NVIDIA显卡开源驱动 [Nouveau](http://nouveau.freedesktop.org/) 的内容. 有关官方闭源驱动的信息请查看[NVIDIA](/index.php/NVIDIA "NVIDIA").

查找硬件的 [代号](http://nouveau.freedesktop.org/wiki/CodeNames) ([Wikipedia 包含更详细的列表](https://en.wikipedia.org/wiki/Comparison_of_Nvidia_Graphics_Processing_Units "wikipedia:Comparison of Nvidia Graphics Processing Units")), 然后和 [功能矩阵](http://nouveau.freedesktop.org/wiki/FeatureMatrix/) 进行比较，缺人支持的功能。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 加载](#.E5.8A.A0.E8.BD.BD)
    *   [2.1 尽早启动 KMS](#.E5.B0.BD.E6.97.A9.E5.90.AF.E5.8A.A8_KMS)
*   [3 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [3.1 保留已安装的Nvidia驱动](#.E4.BF.9D.E7.95.99.E5.B7.B2.E5.AE.89.E8.A3.85.E7.9A.84Nvidia.E9.A9.B1.E5.8A.A8)
    *   [3.2 安装最新的开发包](#.E5.AE.89.E8.A3.85.E6.9C.80.E6.96.B0.E7.9A.84.E5.BC.80.E5.8F.91.E5.8C.85)
    *   [3.3 双输出](#.E5.8F.8C.E8.BE.93.E5.87.BA)
    *   [3.4 设置控制台分辨率](#.E8.AE.BE.E7.BD.AE.E6.8E.A7.E5.88.B6.E5.8F.B0.E5.88.86.E8.BE.A8.E7.8E.87)
    *   [3.5 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [3.6 风扇控制](#.E9.A3.8E.E6.89.87.E6.8E.A7.E5.88.B6)
    *   [3.7 Optimus](#Optimus)
*   [4 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [4.1 禁用 MSI](#.E7.A6.81.E7.94.A8_MSI)
        *   [4.1.1 Phantom Output Issue](#Phantom_Output_Issue)
    *   [4.2 Random lockups with kernel error messages](#Random_lockups_with_kernel_error_messages)

## 安装

[安装](/index.php/Pacman "Pacman") [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) 包, 这个软件包提供了[Xorg](/index.php/Xorg "Xorg") DDX 驱动进行 2D加速，它还会引入 [mesa](https://www.archlinux.org/packages/?name=mesa)，为 DRI 驱动提供 3D 加速功能

为x86_64提供32-bit支持, 请从[multilib](/index.php/Multilib "Multilib")源中安装[lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa)。

要支持 OpenGL，请安装 [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl), 使用 [multilib](/index.php/Multilib "Multilib") 的话，还需要安装 [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl)。

## 加载

Nouveau的内核模块应该在系统启动时就已自动加载，如果没有的话：

*   确保你的[内核参数](/index.php/Kernel_parameters "Kernel parameters")中没有`nomodeset` 或者 `vga=`， 因为Nouveau需要内核模式设置。
*   另外，确保你没有在 modprobe 配置文件 `/etc/modprobe.d/` 或 `/usr/lib/modprobe.d/` 中屏蔽 Nouveau。
*   检查 dmesg 中有没有 opcode 错误，如果有的话，将 `nouveau.config=NvBios=PRAMIN` 加入 [内核参数](/index.php/Kernel_parameters "Kernel parameters")禁止模块卸载[[1]](http://nouveau.freedesktop.org/wiki/TroubleShooting/#index10h3)

### 尽早启动 KMS

**Tip:** 如果你对这个问题的解决有问题的话，请访问[这个页面](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting").

Nouveau 驱动依赖[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS)。当系统启动时，KMS 模块会在其它模块之后启用，所以显示的分辨率发生改变。查看[Nouveau KernelModeSetting 页面](http://nouveau.freedesktop.org/wiki/KernelModeSetting)获取更多细节。

可以设置将 KMS 尽早启动，在 [initramfs](/index.php/Initramfs "Initramfs") 加载时就接管功能。

将 `nouveau` 加入 `/etc/mkinitcpio.conf` 的 `MODULES` 数组:

```
MODULES="... nouveau ..."

```

如果你使用了一个自定义的EDID文件，你应该像这样把它加入到initramfs 中：

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

重新生成初始ramdisk映像：

```
# mkinitcpio -p <kernel preset; e.g. *linux*>

```

如果 Nouneau 出问题了，不得不多次重建 nouveau-drm 进行测试，请不要在 initramfs 中添加`nouveau`。因为这样会容易忘记重建 initramfs 而使测试更加困难。先使用“延迟启动”，直到系统已经稳定。如果需要自定义固件，使用 initrams 可能会有更多问题（一般不建议）

## 提示与技巧

### 保留已安装的Nvidia驱动

如果你想保留已经安装的官方驱动但又想要使用Nouveau驱动，像下面注释掉`/etc/modprobe.d/nouveau_blacklist.conf` 中的内容

```
#blacklist nouveau

```

并通过新建文件`/etc/X11/xorg.conf.d/20-nouveau.conf` 来告诉Xorg引导Nouveau驱动而不是Nvidia驱动，文件内容如下:

```
Section "Device"
    Identifier "Nvidia card"
    Driver "nouveau"
EndSection

```

**Tip:** 如果你需要经常性在两种驱动间切换，你可以使用 [这些脚本](/index.php/NVIDIA#Switching_between_nvidia_and_nouveau_drivers "NVIDIA").

如果你已经安装了官方驱动，又想在不重启的情况下测试Nouveau驱动，请确保‘nvidia’模块未被加载：

```
# rmmod nvidia

```

然后加载'nouveau' 模块:

```
# modprobe nouveau

```

并且通过内核信息确保它已被正常加载:

```
$ dmesg

```

### 安装最新的开发包

你可以通过AUR安装最新的git包：

*   你可以通过[mesa-git](https://aur.archlinux.org/packages/mesa-git/)安装最新的Mesa（包含最新的DRI驱动）。
*   你可以通过[xf86-video-nouveau-git](https://aur.archlinux.org/packages/xf86-video-nouveau-git/) 安装最新的DDX驱动。
*   你也可以尝试安装像 [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) 这样比较新的内核版本，这可能会带来更好的性能。
*   要获得Nouveau最新的更新, 你应该使用AUR中的[linux-git](https://aur.archlinux.org/packages/linux-git/) 包，并且编辑PKGBUILD 以使用Nouveau自己的内核库，目前它位于： [git://anongit.freedesktop.org/git/nouveau/xf86-video-nouveau](git://anongit.freedesktop.org/git/nouveau/xf86-video-nouveau).

你可以在 [Nouveau Source page](http://nouveau.freedesktop.org/wiki/Source)找到上游驱动源.

### 双输出

Nouveau 支持xrandr拓展和多显示器，教程详见[RandR12](/index.php/RandR12 "RandR12")

这是一个完整的例子 `/etc/X11/xorg.conf.d/20-nouveau.conf` 用来演示在双输出模式下运行两个显示器。当然，你可能更喜欢像GNOME显示控制中心 (`gnome-control-center display`)这样的图形化配置工具.

```
# the right one
Section "Monitor"
          Identifier   "NEC"
          Option "PreferredMode" "1280x1024_60.00"
EndSection

# the left one
Section "Monitor"
          Identifier   "FUS"
          Option "PreferredMode" "1280x1024_60.00"
          Option "LeftOf" "NEC"
EndSection

Section "Device"
    Identifier "nvidia card"
    Driver "nouveau"
    Option  "Monitor-DVI-I-1" "NEC"
    Option  "Monitor-DVI-I-2" "FUS"
EndSection

Section "Screen"
    Identifier "screen1"
   Monitor "NEC"
    DefaultDepth 24
      SubSection "Display"
       Depth      24
       Virtual 2560 2048
      EndSubSection
    Device "nvidia card"
EndSection

Section "ServerLayout"
    Identifier "layout1"
    Screen "screen1"
EndSection
```

### 设置控制台分辨率

使用[fbset](https://www.archlinux.org/packages/?name=fbset)工具调整控制台分辨率. 你也可以通过 video= kernel 这样的选项来调整控制台分辨率 (详见 [KMS](/index.php/KMS "KMS")).

### 电源管理

GPU缩放依赖于GPU上的各个阶段的准备。kernel 3.18 之后内核包含电源管理功能，如果要玩游戏的话，可以将 `nouveau.pstate=1` 加入模块参数，启用 pstate，这样会获得更高的频率。

查看 [Nouveau PowerManagement page](http://nouveau.freedesktop.org/wiki/PowerManagement) 以获得更多细节。

### 风扇控制

如果硬件支持，可以通过 `/sys` 控制风扇转速。

```
$ find /sys -name pwm1_enable
/sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0/hwmon/hwmon1/pwm1_enable
$ readlink /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0/driver
../../../../bus/pci/drivers/nouveau

```

`pwm1_enable` 可以设置为 0, 1 或 2，意思是 NONE, MANUAL 和 AUTO 风扇控制。设置为手动时，可以手动设置 `pwm1`，例如设置为 40 表示 40% 的转速.

**警告:** 风险自担，不要太热烧了显卡!

可以通过 udev 规则设置:

```
$ cat /etc/udev/rules.d/50-nouveau-hwmon.rules
ACTION=="add", SUBSYSTEM=="hwmon", DRIVERS=="nouveau", ATTR{pwm1_enable}="2"

```

参考:

*   [http://floppym.blogspot.de/2013/07/fan-control-with-nouveau.html](http://floppym.blogspot.de/2013/07/fan-control-with-nouveau.html)
*   [https://kalgan.cc/blog/posts/Controlling_nVidia_cards_fans_with_nouveau_in_Debian/](https://kalgan.cc/blog/posts/Controlling_nVidia_cards_fans_with_nouveau_in_Debian/)

### Optimus

要在笔记本上使用 [Optimus](/index.php/Optimus "Optimus")(使用两个 GPUs)，请阅读 [bumblebee](/index.php/Bumblebee "Bumblebee") 和 [PRIME](/index.php/PRIME "PRIME")

## 故障排除

添加以下内容到内核命令(如果使用grub启动，在启动菜单下按`e`)来打开视频调试:

```
drm.debug=14 log_buf_len=16M

```

建立详细的Xorg日志：

```
startx -- -logverbose 9 -verbose 9

```

查看加载的视频模块的参数和值：

```
modinfo -p video

```

### 禁用 MSI

如果出现模块加载错误或 X 服务器无法启用，请尝试将 `nouveau.config=NvMSI=0` 加入 [内核参数](/index.php/Kernel_parameters "Kernel parameters").

Source: [https://bugs.freedesktop.org/show_bug.cgi?id=78441](https://bugs.freedesktop.org/show_bug.cgi?id=78441)

#### Phantom Output Issue

It is possible for the nouveau driver to detect "phantom" outputs. For example, both VGA-1 and LVDS-1 are shown as connected but only LVDS-1 is present.

This causes display problems and a corrupted screen.

The problem can be overcome by disabling the phantom output (VGA-1 in the examples given) on the kernel command line of your boot loader. This can be achieved by appending the following:

```
video=VGA-1:d

```

Where **d** = disable.

The phantom output can also be disabled in X by adding the following to `/etc/X11/xorg.conf.d/20-nouveau.conf`:

```
Section "Monitor"
Identifier "VGA-1"
Option "Ignore" "1"
EndSection

```

Source: [http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues](http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues)

### Random lockups with kernel error messages

Specific Nvidia chips with Nouveau may give random system lockups and more commonly throw many kernel messages, seen with *dmesg*. Try adding the `nouveau.noaccel=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). See [[2]](https://fedoraproject.org/wiki/Common_kernel_problems#Systems_with_nVidia_adapters_using_the_nouveau_driver_lock_up_randomly) for more information.