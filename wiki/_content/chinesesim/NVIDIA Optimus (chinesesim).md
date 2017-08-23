**翻译状态：** 本文是英文页面 [NVIDIA_Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-09，点击[这里](https://wiki.archlinux.org/index.php?title=NVIDIA_Optimus&diff=0&oldid=364751)可以查看翻译后英文页面的改动。

NVIDIA Optimus是一种允许 Intel 集成 GPU 和 NVIDIA GPU 建成并通过一台笔记本电脑访问的技术。让 Optimus 显卡工作在 Arch Linux 下需要一些稍微复杂的设置步骤，下文说明了几种可用方法:

*   在 BIOS 里禁用其中之一，如果禁用 NVIDIA 显卡的话也许会提升电池续航能力。但并不适用于所有 BIOS, 也不能切换显卡。

*   使用闭源 NVIDIA 驱动提供的官方 Optimus 支持，这能让 NVIDIA 显卡发挥最大性能但不能切换显卡，同时会比开源驱动有更多 bug.

*   使用开源 nouveau 驱动提供的 PRIME 功能，它能够切换显卡但是和闭源驱动相比性能差劲，并且目前并未实现任何省电功能。

*   使用第三方程序 Bumblebee 来实现类似于 Optimus 的功能，同时支持切换显卡和省电，但需要额外设置。

这些方法在下文有详细解释。

## Contents

*   [1 禁用可交换显卡](#.E7.A6.81.E7.94.A8.E5.8F.AF.E4.BA.A4.E6.8D.A2.E6.98.BE.E5.8D.A1)
*   [2 使用 nvidia](#.E4.BD.BF.E7.94.A8_nvidia)
    *   [2.1 显示管理器](#.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [2.1.1 LightDM](#LightDM)
        *   [2.1.2 SDDM](#SDDM)
    *   [2.2 检验 3D](#.E6.A3.80.E9.AA.8C_3D)
    *   [2.3 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)
*   [3 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [3.1 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29)
*   [4 使用 nouveau](#.E4.BD.BF.E7.94.A8_nouveau)
*   [5 使用 Bumblebee](#.E4.BD.BF.E7.94.A8_Bumblebee)

## 禁用可交换显卡

如果你只使用某一显卡而不切换的话，检查你系统 BIOS 的选项，那里应该有禁用某一显卡的选项。某些笔记本只支持禁用独立显卡，另一些则相反，但是如果你只想用其中之一的话还是值得一看的。但是若你想同时使用两个显卡，或者无法禁用你不想要的显卡的话，请看以下的方法。

## 使用 nvidia

[闭源 NVIDIA 驱动](/index.php/NVIDIA "NVIDIA")并不像 nouveau 驱动一样支持动态切换 (意味着它只能使用 NVIDIA 设备). 它还有一些已被 NVIDIA 承认但仍未修复的显著问题，然而，它使用独立显卡并 (自2013年10月) 在性能上相比 nouveau 驱动有显著优势。

首先，安装[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")的驱动包 [nvidia](https://www.archlinux.org/packages/?name=nvidia) 和软件包 [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

然后，你必须创建一个 `xorg.conf`. 你需要提供 NVIDIA 显卡的 PCI 地址，可通过以下命令获取:

```
$ lspci | grep -E "VGA|3D"

```

PCI 地址是提到 NVIDIA 的输出行的前7个字符，看起来像 `01:00.0`. 在 `xorg.conf` 中，需转换为 `#:#:#` 格式；例如 `01:00.0` 应该写成 `1:0:0`.

 `# nano /etc/X11/xorg.conf` 
```
Section "ServerLayout"
    Identifier "layout"
    Screen 0 "nvidia"
    Inactive "intel"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:*PCI address determined earlier*"
    # e.g. BusID "PCI:1:0:0"
EndSection

Section "Screen"
    Identifier "nvidia"
    Device "nvidia"
    Option "AllowEmptyInitialConfiguration"
EndSection

Section "Device"
    Identifier "intel"
    Driver "modesetting"
    Option "AccelMethod"  "none"
EndSection

Section "Screen"
    Identifier "intel"
    Device "intel"
EndSection
```

之后，把以下内容添加到 `~/.xinitrc` 开头:

 `$ nano ~/.xinitrc` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

现在重启以加载驱动，X 也应该启动了。

如果在启动 X 时黑屏，确保 `~/.xinitrc` 的两个 `xrandr` 命令后没有 `&` 符号；如果有，可能是窗口管理器在 `xrandr` 命令执行完成之前启动导致了黑屏。

### 显示管理器

如果你使用显示管理器 (Display Manager, DM)，你需要创建或编辑启动管理器的脚本而不是使用 `~/.xinitrc`.

#### LightDM

对于 [LightDM](/index.php/LightDM "LightDM"):

 `# nano /etc/lightdm/display_setup.sh` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

赋予脚本可执行权限:

```
# chmod +x /etc/lightdm/display_setup.sh

```

编辑 `/etc/lightdm/lightdm.conf` 的 `[Seat:*]` 部分以配置 lightdm 运行这个脚本:

 `# nano /etc/lightdm/lightdm.conf` 
```
[Seat:*]
display-setup-script=/etc/lightdm/display_setup.sh
```

重启，你的 DM 应该启动了。

#### SDDM

对于 [SDDM](/index.php/SDDM "SDDM"):

 `# nano /usr/share/sddm/scripts/Xsetup` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

### 检验 3D

你可通过安装 [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) 并运行以下命令来检验 NVIDIA 是否被使用:

```
$ glxinfo | grep NVIDIA

```

### 更多信息

更多信息参见 NVIDIA 官方页面的[这个](http://http.download.nvidia.com/XFree86/Linux-x86_64/340.32/README/randr14.html)主题。

## 疑难问题

### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

添加 `rcutree.rcu_idle_gp_delay=1` 到内核参数。原始话题见[此](https://bbs.archlinux.org/viewtopic.php?id=169742)。

## 使用 nouveau

开源 [nouveau](/index.php/Nouveau "Nouveau") 驱动 ([xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)) 能靠一种叫 PRIME 的技术动态切换到 Intel 驱动 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)). 更多信息见 wiki 的 [PRIME](/index.php/PRIME "PRIME") 页面。

## 使用 Bumblebee

如果你想使用 Bumblebee, 并实现省电和其他有用特性，见 wiki 的 [Bumblebee](/index.php/Bumblebee "Bumblebee") 页面。