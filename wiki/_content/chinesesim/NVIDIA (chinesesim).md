本文包含安装和配置 [NVIDIA](http://www.nvidia.com) *专有* 显卡驱动的信息。想要了解开源驱动的信息，参见 [Nouveau](/index.php/Nouveau "Nouveau").

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 备用安装：定制内核](#.E5.A4.87.E7.94.A8.E5.AE.89.E8.A3.85.EF.BC.9A.E5.AE.9A.E5.88.B6.E5.86.85.E6.A0.B8)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 自动配置](#.E8.87.AA.E5.8A.A8.E9.85.8D.E7.BD.AE)
    *   [2.2 最小配置模式](#.E6.9C.80.E5.B0.8F.E9.85.8D.E7.BD.AE.E6.A8.A1.E5.BC.8F)
    *   [2.3 多台显示器](#.E5.A4.9A.E5.8F.B0.E6.98.BE.E7.A4.BA.E5.99.A8)
        *   [2.3.1 TwinView](#TwinView)
        *   [2.3.2 使用 NVIDIA Settings](#.E4.BD.BF.E7.94.A8_NVIDIA_Settings)
*   [3 调整](#.E8.B0.83.E6.95.B4)
    *   [3.1 图形用户界面：nvidia-settings](#.E5.9B.BE.E5.BD.A2.E7.94.A8.E6.88.B7.E7.95.8C.E9.9D.A2.EF.BC.9Anvidia-settings)
        *   [3.1.1 启用桌面组合](#.E5.90.AF.E7.94.A8.E6.A1.8C.E9.9D.A2.E7.BB.84.E5.90.88)
        *   [3.1.2 关闭启动时的Logo](#.E5.85.B3.E9.97.AD.E5.90.AF.E5.8A.A8.E6.97.B6.E7.9A.84Logo)
        *   [3.1.3 启用硬件加速](#.E5.90.AF.E7.94.A8.E7.A1.AC.E4.BB.B6.E5.8A.A0.E9.80.9F)
        *   [3.1.4 覆盖显示器检测](#.E8.A6.86.E7.9B.96.E6.98.BE.E7.A4.BA.E5.99.A8.E6.A3.80.E6.B5.8B)
        *   [3.1.5 启用三重缓存](#.E5.90.AF.E7.94.A8.E4.B8.89.E9.87.8D.E7.BC.93.E5.AD.98)
        *   [3.1.6 使用系统级事件](#.E4.BD.BF.E7.94.A8.E7.B3.BB.E7.BB.9F.E7.BA.A7.E4.BA.8B.E4.BB.B6)
        *   [3.1.7 启用省电功能](#.E5.90.AF.E7.94.A8.E7.9C.81.E7.94.B5.E5.8A.9F.E8.83.BD)
        *   [3.1.8 启用亮度控制](#.E5.90.AF.E7.94.A8.E4.BA.AE.E5.BA.A6.E6.8E.A7.E5.88.B6)
        *   [3.1.9 启用SLI](#.E5.90.AF.E7.94.A8SLI)
        *   [3.1.10 强制Powermizer性能水平(适用于笔记本)](#.E5.BC.BA.E5.88.B6Powermizer.E6.80.A7.E8.83.BD.E6.B0.B4.E5.B9.B3.28.E9.80.82.E7.94.A8.E4.BA.8E.E7.AC.94.E8.AE.B0.E6.9C.AC.29)
            *   [3.1.10.1 让GPU根据温度来设置自己的性能水平](#.E8.AE.A9GPU.E6.A0.B9.E6.8D.AE.E6.B8.A9.E5.BA.A6.E6.9D.A5.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.B7.B1.E7.9A.84.E6.80.A7.E8.83.BD.E6.B0.B4.E5.B9.B3)
        *   [3.1.11 禁用vblank中断(适用于笔记本)](#.E7.A6.81.E7.94.A8vblank.E4.B8.AD.E6.96.AD.28.E9.80.82.E7.94.A8.E4.BA.8E.E7.AC.94.E8.AE.B0.E6.9C.AC.29)
        *   [3.1.12 启用超频](#.E5.90.AF.E7.94.A8.E8.B6.85.E9.A2.91)
            *   [3.1.12.1 设置静态的2D/3D时钟](#.E8.AE.BE.E7.BD.AE.E9.9D.99.E6.80.81.E7.9A.842D.2F3D.E6.97.B6.E9.92.9F)
        *   [3.1.13 通过XRandR启用屏幕旋转](#.E9.80.9A.E8.BF.87XRandR.E5.90.AF.E7.94.A8.E5.B1.8F.E5.B9.95.E6.97.8B.E8.BD.AC)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 启用 Pure Video HD 高清视频解码(VDPAU/VAAPI)](#.E5.90.AF.E7.94.A8_Pure_Video_HD_.E9.AB.98.E6.B8.85.E8.A7.86.E9.A2.91.E8.A7.A3.E7.A0.81.28VDPAU.2FVAAPI.29)
    *   [4.2 使用电视输出](#.E4.BD.BF.E7.94.A8.E7.94.B5.E8.A7.86.E8.BE.93.E5.87.BA)
    *   [4.3 使用一台电视(DFP)作为X的唯一输出](#.E4.BD.BF.E7.94.A8.E4.B8.80.E5.8F.B0.E7.94.B5.E8.A7.86.28DFP.29.E4.BD.9C.E4.B8.BAX.E7.9A.84.E5.94.AF.E4.B8.80.E8.BE.93.E5.87.BA)
    *   [4.4 检查电源状态](#.E6.A3.80.E6.9F.A5.E7.94.B5.E6.BA.90.E7.8A.B6.E6.80.81)
    *   [4.5 在shell显示GPU温度](#.E5.9C.A8shell.E6.98.BE.E7.A4.BAGPU.E6.B8.A9.E5.BA.A6)
        *   [4.5.1 途径一 - nvidia-settings](#.E9.80.94.E5.BE.84.E4.B8.80_-_nvidia-settings)
        *   [4.5.2 途径二 - nvidia-smi](#.E9.80.94.E5.BE.84.E4.BA.8C_-_nvidia-smi)
        *   [4.5.3 途径三 - nvclock](#.E9.80.94.E5.BE.84.E4.B8.89_-_nvclock)
    *   [4.6 登陆时设置风扇速度](#.E7.99.BB.E9.99.86.E6.97.B6.E8.AE.BE.E7.BD.AE.E9.A3.8E.E6.89.87.E9.80.9F.E5.BA.A6)
    *   [4.7 改变驱动程序的安装/反安装顺序](#.E6.94.B9.E5.8F.98.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.AE.89.E8.A3.85.2F.E5.8F.8D.E5.AE.89.E8.A3.85.E9.A1.BA.E5.BA.8F)
    *   [4.8 在nvidia和nouveau之间切换](#.E5.9C.A8nvidia.E5.92.8Cnouveau.E4.B9.8B.E9.97.B4.E5.88.87.E6.8D.A2)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [5.1 游戏中使用双头显示输出](#.E6.B8.B8.E6.88.8F.E4.B8.AD.E4.BD.BF.E7.94.A8.E5.8F.8C.E5.A4.B4.E6.98.BE.E7.A4.BA.E8.BE.93.E5.87.BA)
    *   [5.2 旧的Xorg的设置](#.E6.97.A7.E7.9A.84Xorg.E7.9A.84.E8.AE.BE.E7.BD.AE)
    *   [5.3 屏幕损坏："六屏"问题](#.E5.B1.8F.E5.B9.95.E6.8D.9F.E5.9D.8F.EF.BC.9A.22.E5.85.AD.E5.B1.8F.22.E9.97.AE.E9.A2.98)
    *   [5.4 '/dev/nvidia0' Input/Output error](#.27.2Fdev.2Fnvidia0.27_Input.2FOutput_error)
    *   [5.5 '/dev/nvidiactl' errors](#.27.2Fdev.2Fnvidiactl.27_errors)
    *   [5.6 32位应用程序无法启动](#32.E4.BD.8D.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
    *   [5.7 更新内核之后的错误](#.E6.9B.B4.E6.96.B0.E5.86.85.E6.A0.B8.E4.B9.8B.E5.90.8E.E7.9A.84.E9.94.99.E8.AF.AF)
    *   [5.8 通常奔溃的问题](#.E9.80.9A.E5.B8.B8.E5.A5.94.E6.BA.83.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [5.9 安装新版本的驱动后性能很糟糕](#.E5.AE.89.E8.A3.85.E6.96.B0.E7.89.88.E6.9C.AC.E7.9A.84.E9.A9.B1.E5.8A.A8.E5.90.8E.E6.80.A7.E8.83.BD.E5.BE.88.E7.B3.9F.E7.B3.95)
    *   [5.10 400系列显卡与CPU峰值](#400.E7.B3.BB.E5.88.97.E6.98.BE.E5.8D.A1.E4.B8.8ECPU.E5.B3.B0.E5.80.BC)
    *   [5.11 X在登入/注销时挂起，用Ctrl+Alt+Backspace来实现](#X.E5.9C.A8.E7.99.BB.E5.85.A5.2F.E6.B3.A8.E9.94.80.E6.97.B6.E6.8C.82.E8.B5.B7.EF.BC.8C.E7.94.A8Ctrl.2BAlt.2BBackspace.E6.9D.A5.E5.AE.9E.E7.8E.B0)
    *   [5.12 XRandR检测的刷新率不正确依赖实用工具](#XRandR.E6.A3.80.E6.B5.8B.E7.9A.84.E5.88.B7.E6.96.B0.E7.8E.87.E4.B8.8D.E6.AD.A3.E7.A1.AE.E4.BE.9D.E8.B5.96.E5.AE.9E.E7.94.A8.E5.B7.A5.E5.85.B7)
    *   [5.13 No screens found on a laptop / Nvidia Optimus](#No_screens_found_on_a_laptop_.2F_Nvidia_Optimus)
    *   [5.14 没有笔记本电脑上的亮度控制](#.E6.B2.A1.E6.9C.89.E7.AC.94.E8.AE.B0.E6.9C.AC.E7.94.B5.E8.84.91.E4.B8.8A.E7.9A.84.E4.BA.AE.E5.BA.A6.E6.8E.A7.E5.88.B6)
*   [6 一些额外的链接](#.E4.B8.80.E4.BA.9B.E9.A2.9D.E5.A4.96.E7.9A.84.E9.93.BE.E6.8E.A5)

## 安装

该部分仅适用于 [linux](https://www.archlinux.org/packages/?name=linux) 内核包，定制内核请[略过](#.E5.A4.87.E7.94.A8.E5.AE.89.E8.A3.85.EF.BC.9A.E5.AE.9A.E5.88.B6.E5.86.85.E6.A0.B8)该小节。

**提示：** 您最好是使用ArchLinux的[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")来安装驱动，而不是直接到[英伟达官网](http://www.nvidia.cn)去下载驱动，因为这样会在更新系统时同时更新。

1\. 如果你不知道显卡情况，可运行以下命令获知：

	 `$ lspci -k | grep -A 2 -E "(VGA|3D)"` 

2\. 也从以下渠道可确定你的显卡型号以及下载相应的版本：

*   查找代号(如 NV50, NVC0等）： [英伟达代号查询页](https://nouveau.freedesktop.org/wiki/CodeNames/)
*   如果在上面的页面找不到你的型号的显卡，可到[英伟达历史型号列表页](http://www.nvidia.com/object/IO_32667.html)查找。
*   驱动下载： [英伟达驱动下载站](http://www.nvidia.com/Download/index.aspx)

3\. 为你的显卡安装和合适的驱动：

*   GeForce 400 及以上版本安装 [nvidia](https://www.archlinux.org/packages/?name=nvidia) 或者 [nvidia-lts](https://www.archlinux.org/packages/?name=nvidia-lts) 。

**注意:** 假如您是使用最新的显卡，如果以上两个驱动安装后都不能正常工作，您也许需要使用[nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/)和[nvidia-utils-beta](https://aur.archlinux.org/packages/nvidia-utils-beta/)，他们引入了一些新的特性。

*   GeForce 8000/9000、ION 以及 100-300（NV5x, NV8x, NV9x and NVAx）等2006-2010的显卡型号，安装[nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) 或者 [nvidia-340xx-lts](https://www.archlinux.org/packages/?name=nvidia-340xx-lts) 。

*   FGeForce 6000/7000 （NV4x and NV6x）等2004-2006的显卡型号，安装[nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) 或[nvidia-304xx-lts](https://www.archlinux.org/packages/?name=nvidia-304xx-lts) 。

*   更老的显卡型号参看 [#Unsupported drivers](#Unsupported_drivers).

**注意:** nvidia {-173xx,-96xx}-utils 包会跟 libgl 冲突，所以安装的时候，如果 pacman 询问您移除 libgl 并且因为依赖无法移除，您可以使用 `# pacman -Rdd libgl` 移除 libgl。

4\. 在64位的操作系统上，假如您想32位的程序发挥好nvidia-utils的优势，还必须启用[multilib](/index.php/Multilib "Multilib")源来安装lib32的包(例如[lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils), [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) 或者 [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils))。

5\. **重新启动您的计算机**， 以使得nouveau加入模块的黑名单生效。

一旦驱动安装完毕，就可以进入下一步了：[配置英伟达驱动](#.E9.85.8D.E7.BD.AE)。

### 备用安装：定制内核

在此之前，您最好了解一下Arch的打包系统(the Arch Build System)的工作原理：

*   这里是一篇[Arch Build System (简体中文)](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")的介绍
*   还有[makepkg (简体中文)](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")
*   还有[Creating packages (简体中文)](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)")

**注意:** 在[AUR](/index.php/AUR "AUR")上有一个叫[nvidia-all](https://aur.archlinux.org/packages/nvidia-all/)的软件包可以帮助您更方便地安装英伟达的专有驱动，它适合于定制内核或者多内核。

下面的这篇短小精悍的教程将教您怎样使用[ABS](/index.php/ABS "ABS")来定制您的驱动。

安装ABS和生成目录树：

```
# pacman -S abs
# abs

```

作为一个标准的ArchLinux用户，请为新的软件包创建一个临时目录：

```
$ mkdir -p ~/devel/abs

```

为英伟达的驱动包创建一个拷贝：

```
$ cp -r /var/abs/extra/nvidia/ ~/devel/abs/

```

下面，可以进入英伟达驱动的工程目录了：

```
$ cd ~/devel/abs/nvidia

```

您可以编辑一下一些文件`nvidia.install`和`PKGBUILD`以便它们包含的正确的内核版本变量。

在运行定制内核的时候，可以用下面的方式得到相应的内核和本地版本的名称：

```
$ uname -r

```

1.  In nvidia.install, replace the `EXTRAMODULES='extramodules-3.4-ARCH'` variable with the custom kernel version, such as `EXTRAMODULES='extramodules-3.4.4'` or `EXTRAMODULES='extramodules-3.4.4-custom'` depending on what the kernel's version is and the local version's text/numbers. Do this for all instances of the version number within this file.
2.  In PKGBUILD, change the `_extramodules=extramodules-3.4-ARCH` variable to match the appropriate version, as above.
3.  If there are more than one kernels in the system installed in parallel (such as a custom kernel alongside the default -ARCH kernel), change the `pkgname=nvidia` variable in the PKGBUILD to a unique identifier, such as nvidia-344 or nvidia-custom. This will allow both kernels to use the nvidia module, since the custom nvidia module has a different package name and will not overwrite the original. You will also need to comment the line in `package()` that blacklists the nvidia module in `/usr/lib/modprobe.d/nvidia.conf` (no need to do it again).

跟着：

```
$ makepkg -ci

```

参数`-c`告诉makepkg构建完英伟达驱动后清理一些文件, 而参数`-i`告诉makepkg自动运行pacman来安装构建后的软件包。

## 配置

安装完驱动之后，您需要创建Xorg的配置文件。您可以运行一次[测试](/index.php/Xorg#Running "Xorg")来检验没有配置文件Xorg能否正确运行。但是，您可能需要创建配置文件`/etc/X11/xorg.conf`来调整Xorg运行时的一些变量。您可以用nvidia-xconfig配置工具来生成这些文件，也可以手动创建。假如您是手动创建的话，它可以是一个最小的配置文件(也就是意味着它仅仅把一些基础的选项传给[Xorg](/index.php/Xorg "Xorg")服务器)，或者包含[一些自定义的配置](/index.php/Xorg#Configuration "Xorg")来绕开Xorg的自动发现或者是预配置的选项。

### 自动配置

英伟达的软件包已经包含一个自动配置的工具来帮助您创建Xorg的配置文件(`xorg.conf`)您可以通过运行下面的命令来实现自动配置：

```
# nvidia-xconfig

```

当Xorg的配置文件`xorg.conf`不存在时，这条命令会自动检测您的硬件，并创建文件`/etc/X11/xorg.conf`。假如配置文件已经存在的话，它会进行一些编辑，以方便在Xorg运行时能成功载入英伟达的专有驱动。

假如您想载入DRI(Direct Rendering Infrastructure)，确定已经把您的配置文件修改为：

```
#    Load        "dri"

```

再一次检查您的配置文件`/etc/X11/xorg.conf`中的默认色深，水平同步，垂直刷新和分辨率是否正确，不正确的配置可能会损害您的硬件，请仔细进行检查。

**警告:** 可能在Xorg-server 1.8下仍旧不能正常工作

### 最小配置模式

用根用户创建一个基本的配置文件`/etc/X11/xorg.conf`：

```
# vi /etc/X11/xorg.conf

```

把英伟达的驱动添加到配置文件里面去：

```
Section "Device"
   Identifier     "Device0"
   Driver         "nvidia"
   VendorName     "NVIDIA Corporation"
EndSection

```

**提示：** 假如您已经预先安装了开源驱动nouveau，请确定已经从`/etc/mkinitcpio.conf`里面去除"nouveau"。您也可以通过使用[这些脚本](#.E5.9C.A8nvidia.E5.92.8Cnouveau.E4.B9.8B.E9.97.B4.E5.88.87.E6.8D.A2)来在开源和闭源驱动之间进行切换。

### 多台显示器

To activate dual screen support, you just need to edit the `/etc/X11/xorg.conf.d/10-monitor.conf` file which you made before.

Per each physical monitor, add one Monitor, Device, and Screen Section entry, and then a ServerLayout section to manage it. Be advised that when Xinerama is enabled, the NVIDIA proprietary driver automatically disables compositing. If you desire compositing, you should comment out the `Xinerama` line in "`ServerLayout`" and use TwinView (see below) instead.

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "ServerLayout"
    Identifier     "DualSreen"
    Screen       0 "Screen0"
    Screen       1 "Screen1" RightOf "Screen0" #Screen1 at the right of Screen0
    Option         "Xinerama" "1" #To move windows between screens
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    Screen         0
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Screen         1
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1280x800_75.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "Device1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
    EndSubSection
EndSection

```

#### TwinView

You want only one big screen instead of two. Set the `TwinView` argument to `1`. This option should be used instead of Xinerama (see above), if you desire compositing.

```
Option "TwinView" "1"

```

#### 使用 NVIDIA Settings

你也可以使用由软件包[nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils)提供的`nvidia-settings`工具. 通过这个方法你可以使用NVIDIA公司随驱动程序提供的受限软件. 只需要以root权限运行命令`nvidia-settings`就可以自由设置驱动,你的设置将会被保存到文件`/etc/X11/xorg.conf.d/10-monitor.conf`中.

## 调整

### 图形用户界面：nvidia-settings

英伟达的驱动包提供了一个`nvidia-settings`的程序来给您调整一些额外的选项。

假如您想在登录时载入设置，请在终端输入：

```
$ nvidia-settings --load-config-only

```

或者添加到您的桌面环境的启动应用程序里面。

For a dramatic 2D graphics performance increase in pixmap-intensive applications, e.g. Firefox, set the `InitialPixmapPlacement` parameter to 2:

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

This is documented in [nvidia-settings source code](http://cgit.freedesktop.org/~aplattner/nvidia-settings/tree/src/libXNVCtrl/NVCtrl.h?id=b27db3d10d58b821e87fbe3f46166e02dc589855#n2797). For this setting to persist, this command needs to be run on every startup or added to your `~/.nvidia-settings-rc`.

**提示：** 在极少数情况下`~/.nvidia-settings-rc`可能会出现问题。若真如此，Xorg服务器可能会崩溃，并且需要删除这个文件来解决问题。

*   请到[NVIDIA Accelerated Linux Graphics Driver README and Installation Guide](http://us.download.nvidia.com/XFree86/Linux-x86_64/256.53/README/index.html)查看一些额外的细节和选项。

#### 启用桌面组合

从180.44版本开始，英伟达的驱动默认使用 Damage 和 Composite X 扩展支持 GLX。请参阅 [Composite](/index.php/Composite "Composite") 了解一些详细的说明。

#### 关闭启动时的Logo

添加`"NoLogo"`选项到`Device`节里：

```
Option "NoLogo" "1"

```

#### 启用硬件加速

**注意:** 从97.46.xx版本开始RenderAccel就已经被默认启用。

添加`"RenderAccel"`选项在`Device`节下面：

```
Option "RenderAccel" "1"

```

#### 覆盖显示器检测

`Device`节下面的`"ConnectedMonitor"`选项允许您重载X服务器在启动时的显示器检测选项，它可以在启动的时候节约您大量的宝贵时间。有用的选项是：`"CRT"`是用于CRT显示器，`"DFP"`是用于数字显示器，`"TV"`是用于电视的。

下面的例子是强制英伟达的驱动绕开启动检测并且强制把显示器识别为DFP：

```
Option "ConnectedMonitor" "DFP"

```

**注意:** "CRT"适用于所有模拟的15pin的VGA连接器，甚至是平板显示器。"DFP"仅仅适合于DVI数字连接器。

#### 启用三重缓存

您可以在`Device`节下面添加`"TripleBuffer"`选项来启用三重缓存：

```
Option "TripleBuffer" "1"

```

假如您的显卡有充足的显存(128MB或者更多)的话，建议您启用该选项。这个只有在垂直同步(nvidia-settings中的一个特性)启用的时候才会生效。

**注意:** 此选项可能会引致全屏花屏和降低性能。

#### 使用系统级事件

这是来自英伟达驱动的[README](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt)文件： *"[...] 使用系统级事件，可以在当某个客户端进行直接渲染到组合窗口的时候，可以有效地通知X。"* 它可以帮助您提高性能，但是它如今还不能完全支持SLI和多GPU模式。

在`Device`节下添加：

```
Option "DamageEvents" "1"

```

**注意:** 在较新的驱动程序版本中，此选项是默认启用的。

#### 启用省电功能

在`Monitor`节下添加：

```
Option "DPMS" "1"

```

#### 启用亮度控制

在`Device`节下添加:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

#### 启用SLI

**警告:** 截至2011年5月7日，你可能会遇到SLI在GNOME 3下会遇到视频性能低迷的情况。

根据英伟达驱动的[README](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-8774/README/appendix-d.html) 附录: *这个选项可以在支持的配置中控制 SLI 渲染的配置。*一个*支持的配置*适用于有一块SLI认证的主板以及2或者3个SLI认证的GPU的计算机。在[SLI Zone](http://www.slizone.com/page/home.html)上面有更加详细的信息。

您可以用`lspci`查找第一个GPU的PCI总线ID：

```
$ lspci | grep VGA

```

跟着会返回类似的信息：

```
03:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)
05:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)

```

在`Device`节下添加BusID(3个先前例子)：

```
BusID "PCI:3:0:0"

```

**注意:** 这个格式很重要。BusID的值必须指定为`"PCI:<BusID>:0:0"`的格式

根据需要的SLI渲染模式来添加值到`Screen`节下面：

```
Option "SLI" "SLIAA"

```

下表列出了可用的渲染模式。

| Value | Behavior |
| 0, no, off, false, Single | 渲染时仅使用单GPU。 |
| 1, yes, on, true, Auto | 启用SLI并让驱动自动选择合适的渲染模式。 |
| AFR | 启用SLI并使用交替帧渲染模式。 |
| SFR | 启用SLI并使用的分割帧渲染模式。 |
| SLIAA | 启用SLI和使用SLI抗锯齿。使用全场景反锯齿结合，以改善视觉效果。 |

另外，您可以使用`nvidia-xconfig`实用工具的命令行参数来插入这些改变到`xorg.conf`：

```
# nvidia-xconfig --busid=PCI:3:0:0 --sli=SLIAA

```

从shell来验证一下SLI是否被启动：

```
$ nvidia-settings -q all | grep SLIMode
 Attribute 'SLIMode' (arch:0.0): AA 
   'SLIMode' is a string attribute.
   'SLIMode' is a read-only attribute.
   'SLIMode' can use the following target types: X Screen.

```

#### 强制Powermizer性能水平(适用于笔记本)

在`Device`节下添加：

```
# 强制Powermizer任何时间都在在特定级别
# level 0x1=highest
# level 0x2=med
# level 0x3=lowest

```

```
# 交流电源设置：
Option "RegistryDwords" "PowerMizerLevelAC=0x3"
# 电池设置：
Option	"RegistryDwords" "PowerMizerLevel=0x3"

```

或许[NVIDIA Driver for X.org:Performance and Power Saving Hints](http://tutanhamon.com.ua/technovodstvo/NVIDIA-UNIX-driver/)这篇文章可以更好地解释这些设置。

##### 让GPU根据温度来设置自己的性能水平

在`Device`节下添加：

```
Option "RegistryDwords" "PerfLevelSrc=0x3333"

```

#### 禁用vblank中断(适用于笔记本)

当运行中断检测的实用工具`powertop`， When running the interrupt detection utility `powertop`,它可以观察到英伟达驱动将会为每个vblank产生一个中断。在`Device`节下放置以下选项来禁用：

```
Option "OnDemandVBlankInterrupts" "1"

```

这将减少约一或两个每秒的中断。

#### 启用超频

**警告:** **请注意，超频可能会严重地损害您的硬件，所以在启用之前您必须要三思而后行。**

您可以在`Device`节里添加下面的选项来启用超频：

```
Option "Coolbits" "1"

```

这将会在X会话上启动超频：

```
$ nvidia-settings

```

{{注意|GTX 4xx/5xx系列的Fermi核心没办法使用Coolbits的方式来超频。另一种方法是在DOS下编辑和刷新BIOS来实现(当然，这是最好的方法)，或者在Win32环境下使用[nvflash](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,127/orderby,2/page,1/)和[NiBiTor 6.0](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,135/orderby,2/page,1/)来实现。通过更新BIOS，不仅可以提高电压限制，同时稳定地提高软件超频。

##### 设置静态的2D/3D时钟

在`Device`节里面添加以下字串来启用PowerMizer的最大性能级别：

```
Option "RegistryDwords" "PerfLevelSrc=0x2222"

```

在`Device`节里面设置一下字串的其中一个来通过`nvidia-settings`来手动控制GPU风扇：

```
Option "Coolbits" "4"

```

```
Option "Coolbits" "5"

```

#### 通过XRandR启用屏幕旋转

把下面的行添加到`Device`节里面：

```
Option "RandRRotation" "True"

```

重新启动Xorg后可以用旋转屏幕：

```
$ xrandr -o left

```

可以用下面的方法恢复默认：

```
$ xrandr -o normal

```

**注意:** 可能您不需要编辑`xorg.conf`来启用屏幕旋转，因为它已经被默认被启用来。最好是使用各自桌面环境的工具，例如KDE的系统设置工具。

## 提示和技巧

### 启用 Pure Video HD 高清视频解码(VDPAU/VAAPI)

**硬件需求：**

至少是一块第二代的PureVideo HD[wikipedia:PureVideo_HD#Table_of_PureVideo_.28HD.29_GPUs](https://en.wikipedia.org/wiki/PureVideo_HD#Table_of_PureVideo_.28HD.29_GPUs "wikipedia:PureVideo HD")

**软件需求：**

安装英伟达显卡的专有驱动将会根据不同PureVideo的显卡来提供到VDPAU的接口来提供视频解码能力。

您也可以通过下面的方式来添加VA-API的支持：

```
# pacman -S vdpau-video

```

您可以通过下面的方式来验证VA-API是否被当前系统所支持：

```
$ vainfo

```

假如您想充分发挥您的显卡的硬件解码能力的话，您可能需要一个支持VDPAU或者VA-API的媒体播放器。

假如您想启用 [MPlayer](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)") 的硬件加速能力的话，您可以编辑`~/.mplayer/config`

```
vo=vdpau
vc=ffmpeg12vdpau,ffwmv3vdpau,ffvc1vdpau,ffh264vdpau,ffodivxvdpau,

```

启用[VLC](/index.php/VLC "VLC")的硬件加速能力可以使用下面的方法：

工具 -> 首选项 -> 输入和解码器 -> 检查“使用GPU加速(实验性的)”

启用**smplayer**的硬件加速能力可以使用下面的方法：

选项 -> 首选项 -> 常规 -> 视频 标签页 -> 选择vdpau作为输出设备

启用**gnome-mplayer**的硬件加速能力可以使用下面的方法：

编辑 -> 首选项 -> 设置vdpau为视频输出

**在低显存下播放高清电影：**

假如您的显卡没有太多的显存(>521MB?)，当您播放1080p甚至是720p可看到锯齿。 您可以使用TWM或者MWM之类的窗口管理器来避免这些问题。

此外可以配置`~/.mplayer/config`增加 MPlayer 的缓存大小。

### 使用电视输出

下面的文章将指导您去实现[电视输出](http://en.wikibooks.org/wiki/NVidia/TV-OUT)

### 使用一台电视(DFP)作为X的唯一输出

假如CRT-0上面的备用显示器没有被自动检测，这可能是使用DVI作为主要输出的一个问题，或许是X启动时电视被关闭或者是还没有被连接到计算机上。

强制英伟达使用DFP，把一个EDID的拷贝储存在文件系统上，好让X可以解释文件，而不是从TV/DFP上面读EDID。

运行nvidia-settings来获得EDID，它会用树格式来显示一些信息，并会忽略余下的设置和选择的GPU(相应条目应该为"GPU-0"或者类似的选项)，点击"DFP"节(再提醒一下，是"DFP-0"或者类似的选项)，点击"获取 Edid"按钮来储存，例如`/etc/X11/dfp0.edid`。

在xorg.conf的"Device"节添加：

```
Option "ConnectedMonitor" "DFP"
Option "CustomEDID" "DFP-0:/etc/X11/dfp0.edid"

```

选项`ConnectedMonitor`会强制驱动调整连接的DFP。选项`CustomEDID`会提供EDID数据给设备，这将意味着连接到TV/DFP的设备会被在X的进程中启动。

通过这种方法，可以在启动时自动启动一个登录管理器并且通过开机进程来启动电视，并且正确配置屏幕。

### 检查电源状态

英伟达的Xorg驱动可以检测电源。可以检查'GPUPowerSource'这个只读参数来实现(0 - 交流电源，1 - 电池)：

```
   $ nvidia-settings -q GPUPowerSource -t
   1

```

为了能够实现检测，您需要预先安装[acpid](/index.php/Acpid "Acpid")，并且把它添加到rc.conf的DAEMONS里面，否则系统日志会出现警告：

```
ACPI: failed to connect to the ACPI event daemon; the daemon
may not be running or the "AcpidSocketPath" X
configuration option may not be set correctly.  When the
ACPI event daemon is available, the NVIDIA X driver will
try to use it to receive ACPI event notifications.  For
details, please see the "ConnectToAcpid" and
"AcpidSocketPath" X configuration options in Appendix B: X
Config Options in the README.

```

### 在shell显示GPU温度

#### 途径一 - nvidia-settings

**注意:** 您必须要用X才能使用该途径。如果你没有X，使用途径二或途径三。还要注意途径三目前对于较新的显卡(例如 G210/220)以及嵌入式 GPUs (如 Zotac IONITX's 8800GS) 不工作，

您可以用下面的方法让nvidia-settings在shell下面显示GPU温度：

```
$ nvidia-settings -q gpucoretemp

```

这将输出类似下面的信息：

```
Attribute 'GPUCoreTemp' (hostname:0.0): 41.
'GPUCoreTemp' is an integer attribute.
'GPUCoreTemp' is a read-only attribute.
'GPUCoreTemp' can use the following target types: X Screen, GPU.

```

The GPU temps of this board is 41 C.

您可以使用rrdtool或者conky其它的实用工具来输出GPU的温度。

```
$ nvidia-settings -q gpucoretemp -t
41

```

#### 途径二 - nvidia-smi

使用nvidia-smi可以直接获取GPU的温度，而不需要使用X。这对于一部分没有运行X的用户很有用，也许是因为这些机器无显示器而运行着服务器软件。

您可以使用下面的方法来使用nvidia-smi让shell输出GPU温度：

```
$ nvidia-smi

```

将会输出类似下面的信息：

```
$ nvidia-smi
Fri Jan  6 18:53:54 2012       
+------------------------------------------------------+                       
| NVIDIA-SMI 2.290.10   Driver Version: 290.10         |                       
|-------------------------------+----------------------+----------------------+
| Nb.  Name                     | Bus Id        Disp.  | Volatile ECC SB / DB |
| Fan   Temp   Power Usage /Cap | Memory Usage         | GPU Util. Compute M. |
|===============================+======================+======================|
| 0\.  GeForce 8500 GT           | 0000:01:00.0  N/A    |       N/A        N/A |
|  30%   62 C  N/A   N/A /  N/A |  17%   42MB /  255MB |  N/A      Default    |
|-------------------------------+----------------------+----------------------|
| Compute processes:                                               GPU Memory |
|  GPU  PID     Process name                                       Usage      |
|=============================================================================|
|  0\.           ERROR: Not Supported                                          |
+-----------------------------------------------------------------------------+

```

仅输出温度：

```
$ nvidia-smi -q -d TEMPERATURE

==============NVSMI LOG==============

Timestamp                       : Fri Jan  6 18:50:57 2012

Driver Version                  : 290.10

Attached GPUs                   : 1

GPU 0000:01:00.0
    Temperature
        Gpu                     : 62 C

```

您可以使用rrdtool或者conky其它的实用工具来输出GPU的温度。

```
$ nvidia-smi -q -d TEMPERATURE | grep Gpu | cut -c35-36

```

```
62

```

参考: [http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli](http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli)

#### 途径三 - nvclock

nvclock可以从[extra]的软件源中得到。注意nvclock无法访问G210/220或者更新的热传感器。

nvclock获取的温度跟nvidia-settings/nv-control获取的温度会有明显的差异。根据[这里](http://sourceforge.net/projects/nvclock/forums/forum/67426/topic/1906899)，一篇来自nvclock的名叫thunderbird的作者提到，nvclock的数值或许更加准确。

### 登陆时设置风扇速度

您可以使用`nvidia-settings`的命令行借口来调整。首先确定您的Xorg的配置文件的`Device`节是否已经把Coolbits设置为4或者5.

```
Option "Coolbits" "4"

```

**注意:** GTX 4xx/5xx系列的显卡目前还不能在用这种方法设置登录的风扇速度。该途径仅仅允许在当前的X会话的nvidia-settings设置风扇转速。

在您的[`~/.xinitrc`](/index.php/Xinitrc "Xinitrc")文件放置下面的行来调整运行Xorg下的风扇。把<n>替换为您要设置的风扇转速百分比。

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=<n>"

```

您还可以用递增的方法来配置第二个GPU：

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" \ 
-a "[gpu:1]/GPUFanControlState=1" \
-a "[fan:0]/GPUCurrentFanSpeed=<n>" \
-a  [fan:1]/GPUCurrentFanSpeed=<n>" &

```

假如您使用GDM或者KDM之类的登录管理器，您可以创建一个桌面的入口文件来处理这个设定。创建`~/.config/autostart/nvidia-fan-speed.desktop`并且把这些文本放置到里面。**把<n>替换为您要设置的风扇转速百分比。**

```
[Desktop Entry]
Type=Application
Exec=nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=<n>"
X-GNOME-Autostart-enabled=true
Name=nvidia-fan-speed

```

### 改变驱动程序的安装/反安装顺序

在这里，旧的英伟达驱动被定义为nvidiaO，而新的英伟达驱动则被定义为nvidiaN。

```
移除 nvidiaO
安装 nvidia-libglN
安装 nvidiaN
安装 lib32-nvidia-libgl-N (假如有必要的话)

```

### 在nvidia和nouveau之间切换

假如您经常在nvidia和nouveau两个驱动之间切换，您可以使用这两个脚本来让您的工作更加简单有效：

```
#!/bin/bash
# nvidia -> nouveau

/usr/bin/sudo /bin/sed -i 's/#options nouveau modeset=1/options nouveau modeset=1/' /etc/modprobe.d/modprobe.conf
/usr/bin/sudo /bin/sed -i 's/#MODULES="nouveau"/MODULES="nouveau"/' /etc/mkinitcpio.conf

/usr/bin/sudo /usr/bin/pacman -Rdds --noconfirm nvidia-173xx{,-utils}
/usr/bin/sudo /usr/bin/pacman -S --noconfirm nouveau-dri xf86-video-nouveau

#/usr/bin/sudo /bin/cp {10-monitor,30-nouveau}.conf /etc/X11/xorg.conf.d/

/usr/bin/sudo /sbin/mkinitcpio -p linux

```

```
#!/bin/bash
# nouveau -> nvidia

/usr/bin/sudo /bin/sed  -i 's/options nouveau modeset=1/#options nouveau modeset=1/' /etc/modprobe.d/modprobe.conf
/usr/bin/sudo /bin/sed -i 's/MODULES="nouveau"/#MODULES="nouveau"/' /etc/mkinitcpio.conf

/usr/bin/sudo /usr/bin/pacman -Rdds --noconfirm nouveau-dri xf86-video-nouveau libgl
/usr/bin/sudo /usr/bin/pacman -S --noconfirm nvidia-173xx{,-utils}

#/usr/bin/sudo /bin/rm /etc/X11/xorg.conf.d/{10-monitor,30-nouveau}.conf

/usr/bin/sudo /sbin/mkinitcpio -p linux

```

**想要成功地完成切换，一次重启是很有必要的。** 请根据您正在使用的驱动版本来修改一些地方(在这里我使用的是nvidia-173xx)

假如您正在使用的xorg-server的版本低于1.10.2-1，取消注释行，复制和删除{10-monitor,30-nouveau}.conf。自从1.10.2-1之后的版本，xorg-server修补为自动加载nouveau。我保留了10-monitor.conf和[30-nouveau.conf](/index.php/Nouveau#Configuration "Nouveau")在同一个目录作为这个脚本，必要时还要调整一下路径。

## 故障排除

### 游戏中使用双头显示输出

当您使用全屏进行游戏的时候，您会发现游戏会把两个屏幕识别为一个大屏幕。虽然这在技术上是正确的(虚拟出来的大屏幕是您的几个屏幕的组合)，您可能不需要在两个屏幕上同时玩游戏。 您可以在SDL上改变这些行为，试一下：

```
export SDL_VIDEO_FULLSCREEN_HEAD=1

```

在OpenGL里面，添加适当的Metamodes到您的xorg.conf的`Device`节下面，然后重启X：

```
Option "Metamodes" "1680x1050,1680x1050; 1280x1024,1280x1024; 1680x1050,NULL;  1280x1024,NULL;"

```

另一种方法，可单独工作或连同上面提到的那些是[在单独的X服务器里面开始游戏](/index.php/Gaming#Starting_games_in_a_separate_X_server "Gaming").

### 旧的Xorg的设置

如果您是从旧的版本升级过来的，请移除旧的`/usr/X11R6`，防止在安装过程中引发问题。

### 屏幕损坏："六屏"问题

一些使用Geforce GT 100M系列显卡的用户，屏幕会在X启动的时候转为损坏；分为六个限制为640x480的区域。

为了解决这个问题，可以在`Device`节里启动验证模式`NoTotalSizeCheck`：

```
Section "Device"
 ...
 Option "ModeValidation" "NoTotalSizeCheck"
 ...
EndSection

```

### '/dev/nvidia0' Input/Output error

这个错误可以是由几个不同的原因引发，此错误最常见的解决方案是检查组/文件权限，这也许不能说是一个问题。在英伟达的文档里面并没有详细地告诉您如何解决这个问题但还有一些东西对一些人有用。这个问题可以是IRQ与其它驱动冲突或者是错误的路由，甚至是内核或者BIOS的问题。

首先您得尝试移除视频采集卡或者其它视频设备来解决问题。如果在同一系统中有太多的视频处理器，可能由于视频控制器的内存分配问题导致内核无法启动。特别是显存比较低的系统可能发生这种情况，即使只有一个视频处理器。你应该找出你的系统的显存(例如运行*lspci -v*)并分配参数传递到内核：

```
vmalloc=64M
或者
vmalloc=256M

```

另一种方法是尝试的是从“操作控制系统”改变你的BIOS IRQ路由“BIOS控制”或其他方式。第一个可以通过内核参数：

```
PCI=biosirq

```

*noacpi*的内核参数也可以作为一个建议，但是因为它完全禁用ACPI的，应谨慎使用，毕竟一些硬件很容易因过热损坏。

**注意:** 您可以在内核的命令行或者在启动管理器的配置文件上传输参数。您可以到你的启动管理器的Wiki页面上面了解更详细的信息。

### '/dev/nvidiactl' errors

启动一个OpenGL的应用程序可能会引致以下的错误：

```
Error: Could not open /dev/nvidiactl because the permissions are too
restrictive. Please see the `FREQUENTLY ASKED QUESTIONS` 
section of `/usr/share/doc/NVIDIA_GLX-1.0/README` 
for steps to correct.

```

您可以把适当的用户添加到"video"组并重新登录来解决这个问题：

```
# gpasswd -a username video

```

### 32位应用程序无法启动

在64位系统下，安装`lib32-nvidia-libgl`对应相同版本的64位驱动可以修复这个问题。

### 更新内核之后的错误

使用自定义构建的NVIDIA模块来替代[extra]里面的软件包，每次内核更新后驱动都需要重新编译。一般建议更新内核和图形驱动程序后重新启动。

### 通常奔溃的问题

*   尝试在xorg.conf里面关闭`RenderAccel`。
*   假如Xorg输出一些错误如"conflicting memory type"或者"failed to allocate primary buffer: out of memory"，在`/boot/grub/menu.lst`添加`nopat`到`kernel`行的末尾。

*   如果NVIDIA编译器提示当前版本的gcc和用于编译的内核的版本号不同，请在`/etc/profile`里面添加：

```
export IGNORE_CC_MISMATCH=1

```

*   假如Xorg使用nvidia-96xx驱动时由于"Signal 11"奔溃，尝试禁用PAT。把参数`nopat`传输到`menu.lst`的`kernel`行。

您可以在[NVIDIA forums.](http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14)找到更多的关于故障排除的信息。

### 安装新版本的驱动后性能很糟糕

假如和旧版本的驱动相比，FPS有下降，首先检查是否打开直接渲染：

```
$ glxinfo | grep direct

```

假如输出：

```
direct rendering: No 

```

跟着FPS可能会突然下降。

一种可能的解决方案是降级您的驱动为先前的版本并重新启动。

### 400系列显卡与CPU峰值

如果您遇到间歇性的CPU峰值与400系列显卡的问题，这可能是PowerMizer不断变化的GPU的时钟频率引起。选择PowerMizer自适应性能的设置，请把一下内容添加到您的Xorg的配置文件的Device节里面：

```
 Option "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"

```

### X在登入/注销时挂起，用Ctrl+Alt+Backspace来实现

假如在使用传统的英伟达驱动启用Xorg的登入/注销时挂起，但登录仍然可以通过Ctrl-Alt-Backspace，尝试添加下面的行到`/etc/modprobe.d/modprobe.conf`：

```
options nvidia NVreg_Mobile=1

```

一些用户可能很幸运地实现，但其他用户反而实现性能下降：

```
options nvidia NVreg_DeviceFileUID=0 NVreg_DeviceFileGID=33 NVreg_DeviceFileMode=0660 NVreg_SoftEDIDs=0 NVreg_Mobile=1

```

注意`NVreg_Mobile`需要根据您的笔记本来修改：

*   1 适用于Dell笔记本.
*   2 适用于non-Compal Toshiba 笔记本.
*   3 适用于其它笔记本.
*   4 适用于Compal Toshiba笔记本.
*   5 适用于Gateway笔记本.

在[NVIDIA Driver's Readme:Appendix K](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt)可以看到更多的信息。

### XRandR检测的刷新率不正确依赖实用工具

XRandR的X扩展目前还不能识别到一个X屏幕上的多个显示设备；它仅仅可以看到`MetaMode`的边界框，XRandR将无法区分它们。 为了支持动态双头输出，NVIDIA的驱动程序必须使每个MetaMode是唯一的，目前，NVIDIA的驱动程序来通过使用一个唯一的标识符刷新率完成。 XRandR扩展目前正在由Xorg社区进行了重新设计，所以刷新率的解决方法可能在未来的某个节点上删除。

此可用的办法也被禁用的“DynamicTwinView”X配置选项设置为“false”，这将禁用NV-CONTROL支持操纵MetaModes，但会造成XRandR和XF86VidMode可见刷新率要准确。

### No screens found on a laptop / Nvidia Optimus

假如在一些笔记本上英伟达的驱动找不到任何屏幕，您可以用下面的方法实现：

```
lspci | grep VGA

```

将会输出类似的信息：

```
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)

```

不幸的是，英伟达已经没有计划在他们的Linux驱动程序支持。

您需要安装[Intel](/index.php/Intel "Intel")的驱动来处理屏幕，让3D软件使用，您需要通过[Bumblebee](/index.php/Bumblebee "Bumblebee")告诉他们使用英伟达的显卡。

### 没有笔记本电脑上的亮度控制

尝试在20-nvidia.conf添加下面的行：

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

如果X无法启动，尝试改为下边的样子：

Section "Device"

```
   Identifier     "Device0"
   Driver         "nvidia"
   VendorName     "NVIDIA Corporation"
   BoardName      "Quadro NVS 3100M"
   Option         "RegistryDwords" "EnableBrightnessControl=1"

```

EndSection

假如它仍旧不能工作的话，您可以尝试安装[nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/)。

## 一些额外的链接

*   [NVIDIA forums](http://www.nvnews.net/vbulletin/forumdisplay.php?s=&forumid=14)
*   [Official readme for NVIDIA drivers](http://http.download.nvidia.com/XFree86/Linux-x86/1.0-7182/README/readme.txt)