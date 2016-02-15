本文包含安装和配置NVIDIA显卡开源驱动 [Nouveau](http://nouveau.freedesktop.org/) 的内容. 有关官方闭源驱动的信息请查看[NVIDIA](/index.php/NVIDIA "NVIDIA").

## Contents

*   [1 针对已安装官方专有驱动的](#.E9.92.88.E5.AF.B9.E5.B7.B2.E5.AE.89.E8.A3.85.E5.AE.98.E6.96.B9.E4.B8.93.E6.9C.89.E9.A9.B1.E5.8A.A8.E7.9A.84)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 加载](#.E5.8A.A0.E8.BD.BD)
    *   [3.1 KMS](#KMS)
        *   [3.1.1 延迟启动](#.E5.BB.B6.E8.BF.9F.E5.90.AF.E5.8A.A8)
        *   [3.1.2 提早启动](#.E6.8F.90.E6.97.A9.E5.90.AF.E5.8A.A8)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 保留已安装的Nvidia驱动](#.E4.BF.9D.E7.95.99.E5.B7.B2.E5.AE.89.E8.A3.85.E7.9A.84Nvidia.E9.A9.B1.E5.8A.A8)
    *   [4.2 安装最新的开发包](#.E5.AE.89.E8.A3.85.E6.9C.80.E6.96.B0.E7.9A.84.E5.BC.80.E5.8F.91.E5.8C.85)
    *   [4.3 Tear-free compositing](#Tear-free_compositing)
    *   [4.4 双输出](#.E5.8F.8C.E8.BE.93.E5.87.BA)
    *   [4.5 设置控制台分辨率](#.E8.AE.BE.E7.BD.AE.E6.8E.A7.E5.88.B6.E5.8F.B0.E5.88.86.E8.BE.A8.E7.8E.87)
    *   [4.6 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [4.7 启用 MSI (Message Signaled Interrupts)](#.E5.90.AF.E7.94.A8_MSI_.28Message_Signaled_Interrupts.29)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)

## 针对已安装官方专有驱动的

**Note:** 此部分内容仅针对已安装[NVIDIA](/index.php/NVIDIA "NVIDIA")专有驱动的，其他人可略过此部分

**Tip:** 如果你要继续保留专有驱动， 你需要[配置一些东西](#Keep_NVIDIA_driver_installed)来加载Nouvean驱动

如果你已经安装了专有驱动，请先卸载它们：

```
 # pacman -Rdds nvidia nvidia-utils nvidia-libgl

```

请确保已经删除Nvidia专有驱动创建的`/etc/X11/xorg.conf` 文件 (或者你可以撤销对这个文件的修改), 否则X将无法正确加载nouveau驱动。

## 安装

在继续操作之前，请先弄清楚你显卡[型号](http://nouveau.freedesktop.org/wiki/CodeNames) (更详细的列表请看 [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Nvidia_Graphics_Processing_Units "wikipedia:Comparison of Nvidia Graphics Processing Units")) 的 [特性矩阵](http://nouveau.freedesktop.org/wiki/FeatureMatrix/) ，看看你的显卡支持什么功能，另外，请确保您的[Xorg](/index.php/Xorg "Xorg") 已经正确安装。

[安装](/index.php/Pacman "Pacman") 位于 [官网](/index.php/Official_repositories "Official repositories")的DDX 驱动通过[xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) 包, 它会引入 [mesa](https://www.archlinux.org/packages/?name=mesa)，为DRI驱动提供3D加速功能

为x86_64提供32-bit支持, 请从[multilib](/index.php/Multilib "Multilib")源中安装[lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa)。

**Note:** 在为3D驱动提交Bug前请先参阅 [Nouveau MesaDrivers 页](http://nouveau.freedesktop.org/wiki/MesaDrivers)。

## 加载

Nouveau的内核模块应该在系统启动时就已加载完成。 如果没有的话：

*   确保你的[内核参数](/index.php/Kernel_parameters "Kernel parameters")中没有`nomodeset` 或者 `vga=`， 因为Nouveau需要内核模式设置才能成功运行（见下文）。
*   另外，确保你没有在`/etc/modprobe.d/`中通过modprobe名单禁用Nouveau。

### KMS

**Tip:** 如果你对这个问题的解决有问题的话，请访问[这个页面](/index.php/Kernel_Mode_Setting#Forcing_modes_and_EDID "Kernel Mode Setting").

Nouveau 驱动依赖[Kernel Mode Setting](/index.php/Kernel_Mode_Setting "Kernel Mode Setting") (KMS)。当系统启动时，由于KMS初始化显示驱动程序可能会使分辨率发生改变。只需要安装Nouveau驱动，足以使系统能够识别并使用"延迟启动"模式初始化它。查看 [Nouveau KernelModeSetting page](http://nouveau.freedesktop.org/wiki/KernelModeSetting) 获取更多细节

**Note:** 用户可能会更喜欢提前启动的方法，因为它不会在引导过程中产生讨厌的分辨率变化问题

#### 延迟启动

这种方法会在其他内核模块都加载完成后启动KMS。你可以去看看名为"Loading modules"的那段文本

#### 提早启动

这种方法会在[initramfs](/index.php/Initramfs "Initramfs")加载后尽可能早的启动KMS。 为了实现这个，可以在`/etc/mkinitcpio.conf`的`MODULES` 数组中添加 `nouveau`：

```
MODULES="... nouveau ..."

```

如果你使用了一个自定义的EDID文件，你应该像这样把它加入到initramfs 中：

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

重新生成初始ramdisk映像：

```
# mkinitcpio -p <kernel preset; e.g. _linux_>

```

如果你的Nouneau出问题了，导致你不得不多次重建nouveau-drm去测试，请不要在initramfs中添加`nouveau` ，那样太容易因为忘记重建initramfs而使测试更加艰难。仅仅使用“延迟启动”知道你能确保你的系统已经稳定。如果你需要自定义固件，使用initrams可能会有更多问题（一般不建议）

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

### Tear-free compositing

编辑`/etc/X11/xorg.conf.d/20-nouveau.conf`, 并在`Device` 部分添加以下内容:

```
Section "Device"
    Identifier "nvidia card"
    Driver "nouveau"
    Option "GLXVBlank" "true"
EndSection

```

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

GPU缩放依赖于GPU上的各个阶段的准备。 查看 [Nouveau PowerManagement page](http://nouveau.freedesktop.org/wiki/PowerManagement) 以获得更多细节。

### 启用 MSI (Message Signaled Interrupts)

这可能会有轻微的性能提高，不过只支持NV50以后的显卡，并且默认是禁用的。

**Warning:** 这可能会导致一些主板/GPU的不稳定！

配置文件位于： `/etc/modprobe.d/nouveau.conf`:

```
options nouveau msi=1

```

如果使用 [提早启动](#Early_start), 把 `FILES="/etc/modprobe.d/nouveau.conf"` 这行加入到 `/etc/mkinitcpio.conf`中, 然后重建内核镜像:

```
# mkinitcpio -p <kernel preset; e.g. _linux_>

```

重启系统使更改生效.

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