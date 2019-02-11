相关文章

*   [Bumblebee](/index.php/Bumblebee "Bumblebee")
*   [Nouveau](/index.php/Nouveau "Nouveau")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [With Xorg 1.17.1](/index.php?title=With_Xorg_1.17.1&action=edit&redlink=1 "With Xorg 1.17.1 (page does not exist)")

**翻译状态：** 本文是英文页面 [NVIDIA_Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-13，点击[这里](https://wiki.archlinux.org/index.php?title=NVIDIA_Optimus&diff=0&oldid=364751)可以查看翻译后英文页面的改动。

NVIDIA Optimus是一种允许 Intel 集成 GPU 和 NVIDIA GPU 建成并通过一台笔记本电脑访问的技术。让 Optimus 显卡工作在 Arch Linux 下需要一些稍微复杂的设置步骤，下文说明了几种可用方法:

*   在 BIOS 里禁用其中之一，如果禁用 NVIDIA 显卡的话也许会提升电池续航能力。但并不适用于所有 BIOS, 也不能切换显卡。

*   使用闭源 NVIDIA 驱动提供的官方 Optimus 支持，这能让 NVIDIA 显卡发挥最大性能但不能切换显卡，同时会比开源驱动有更多 bug.

*   使用开源 nouveau 驱动提供的 PRIME 功能，它能够切换显卡但是和闭源驱动相比性能差劲，并且目前并未实现任何省电功能。

*   使用第三方程序 Bumblebee 来实现类似于 Optimus 的功能，同时支持切换显卡和省电，但需要额外设置。

*   利用nvidia-xrun，一个使用全性能的离散NVIDIA图形功能来单独运行X的使用程序。

这些方法在下文有详细解释。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 禁用可交换显卡](#禁用可交换显卡)
*   [2 使用 nvidia](#使用_nvidia)
    *   [2.1 可选配置](#可选配置)
    *   [2.2 显示管理器](#显示管理器)
        *   [2.2.1 LightDM](#LightDM)
        *   [2.2.2 SDDM](#SDDM)
        *   [2.2.3 GDM](#GDM)
    *   [2.3 检验 3D](#检验_3D)
    *   [2.4 更多信息](#更多信息)
*   [3 疑难问题](#疑难问题)
    *   [3.1 垂直同步撕裂](#垂直同步撕裂)
    *   [3.2 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_(GPU_fallen_off_the_bus_/_RmInitAdapter_failed!))
    *   [3.3 分辨率和屏幕扫描错误“EDID errors in Xorg.log”](#分辨率和屏幕扫描错误“EDID_errors_in_Xorg.log”)
    *   [3.4 锁定问题(lspci 挂起)](#锁定问题(lspci_挂起))
    *   [3.5 笔记本电脑未发现屏幕/NVIDIA Optimus](#笔记本电脑未发现屏幕/NVIDIA_Optimus)
*   [4 使用 nouveau](#使用_nouveau)
*   [5 使用 Bumblebee](#使用_Bumblebee)
*   [6 使用 nvidia-xrun](#使用_nvidia-xrun)

## 禁用可交换显卡

如果你只使用某一显卡而不切换的话，检查你系统 BIOS 的选项，那里应该有禁用某一显卡的选项。某些笔记本只支持禁用独立显卡，另一些则相反，但是如果你只想用其中之一的话还是值得一看的。但是若你想同时使用两个显卡，或者无法禁用你不想要的显卡的话，请看以下的方法。

另一种完全关闭独立显卡的方法请查看 [Hybrid graphics#Fully Power Down Discrete GPU](/index.php/Hybrid_graphics#Fully_Power_Down_Discrete_GPU "Hybrid graphics").

如果您想使用这两张显卡，或者不能禁用您不想要的卡，请参见下面的选项。

## 使用 nvidia

[闭源 NVIDIA 驱动](/index.php/NVIDIA "NVIDIA")并不像 nouveau 驱动一样支持动态切换 (意味着它只能使用 NVIDIA 设备). 它还有一些已被 NVIDIA 承认但仍未修复的显著问题，然而，它使用独立显卡并 (自2013年10月) 在性能上相比 nouveau 驱动有显著优势。

首先，安装[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")的驱动包 [nvidia](https://www.archlinux.org/packages/?name=nvidia) 和软件包 [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

然后，你必须创建一个 `xorg.conf`. 你需要提供 NVIDIA 显卡的 PCI 地址，可通过以下命令获取:

```
$ lspci | grep -E "VGA|3D"

```

PCI 地址是提到 NVIDIA 的输出行的前7个字符，看起来像 `01:00.0`. 在 `xorg.conf` 中，需转换为 `#:#:#` 格式；例如 `01:00.0` 应该写成 `1:0:0`.

**注意:** 在一些设置中，此设置要通过对NVIDIA的驱动程序通过EDID文件来中断对显示器值的自动检测。可查看该文章——[#分辨率和屏幕扫描错误“EDID errors in Xorg.log”](#分辨率和屏幕扫描错误“EDID_errors_in_Xorg.log”)以了解详情

如果安装了1.17.2或者更高版本的X服务([[1]](http://us.download.nvidia.com/XFree86/Linux-x86/358.16/README/randr14.html))

 `/etc/X11/xorg.conf` 
```
Section "Module"
    Load "modesetting"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "<BusID for NVIDIA device here>"
    Option "AllowEmptyInitialConfiguration"
EndSection

```

之后，把以下内容添加到 `~/.xinitrc` 开头:

 `~/.xinitrc` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

现在重启以加载驱动，X 也应该启动了。 如果你的DPI显示不正确，在上面的`~/.xinitrc`配置中指定dpi（实际dpi以你的设备为准），如：

```
 xrandr --dpi 96

```

如果在启动 X 时黑屏，确保 `~/.xinitrc` 的两个 `xrandr` 命令后没有 `&` 符号；如果有，可能是窗口管理器在 `xrandr` 命令执行完成之前启动导致了黑屏。

如果依然黑屏，参考下文[#可选配置](#可选配置)

### 可选配置

如果你使用1.17.1以上版本的Xorg服务出现崩溃，修改`/etc/X11/xorg.conf`配置如下（Intel设备）：

 `# nano /etc/X11/xorg.conf` 
```
Section "Device"
    Identifier  "intel"
    Driver      "modesetting"
    BusID       "PCI:0:2:0"
    Option      "AccelMethod"  "sna"
    #Option      "TearFree" "True"
    #Option      "Tiling" "True"
    #Option      "SwapbuffersWait" "True"
EndSection
```

上面文件中的`BusID`必须和lspci命令的输出相匹配。搜索带有“VGA兼容控制器”的行，其中包含英特尔的内容。例如:

```
$ lspci |grep VGA
00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)

```

**提示：** 上面配置文件中后三项的选项如果不注释掉**可能导致画面撕裂**，但（注释掉）换取的是一定的性能损失。注意， `TearFree` 选项只用于`"sna"` 加速, 参看 [Intel graphics (简体中文)](/index.php/Intel_graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel graphics (简体中文)")。`"AccelMethod"` 选项中，你可以使用 `"sna"` 或 `"uxa"`。

如果X服务启动后屏幕上什么也没有出现，检查`/var/log/xorg.conf`，确保该文件含有类似此行内容：

 `/var/log/xorg.conf` 
```
[ 16112.937] (EE) Screen 1 deleted because of no matching config section.

```

如过具有类似上诉内容，更改`/etc/X11/xorg.conf`文件的serverlayout段，问题可能会消失：

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
    Identifier "layout"
    Screen 1 "nvidia"
    Inactive "intel"
EndSection
```

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

#### GDM

对于[GDM](/index.php/GDM "GDM")，创建以下两个.desktop文件：

```
/usr/share/gdm/greeter/autostart/optimus.desktop
/etc/xdg/autostart/optimus.desktop
```

```
[Desktop Entry]
Type=Application
Name=Optimus
Exec=sh -c "xrandr --setprovideroutputsource modesetting NVIDIA-0; xrandr --auto"
NoDisplay=true
X-GNOME-Autostart-Phase=DisplayServer

```

确保GDM[使用Xorg作为后端](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用Xorg作为后端 "GDM (简体中文)")。

### 检验 3D

你可通过安装 [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) 并运行以下命令来检验 NVIDIA 是否被使用:

```
$ glxinfo | grep NVIDIA

```

### 更多信息

更多信息参见 NVIDIA 官方页面的[这个](http://http.download.nvidia.com/XFree86/Linux-x86_64/340.32/README/randr14.html)主题。

## 疑难问题

### 垂直同步撕裂

[xorg-server](https://www.archlinux.org/packages/?name=xorg-server)需要 1.19 或更高版本，[linux](https://www.archlinux.org/packages/?name=linux)内核需要4.5 或更高版本，[nvidia](https://www.archlinux.org/packages/?name=nvidia)需要370.23更高版本。还需要开启[DRM kernel mode setting](/index.php/NVIDIA#DRM_kernel_mode_setting "NVIDIA")设置项以修复撕裂问题。

官方论坛查看详细信息：[forum thread](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/)。

### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

添加 `rcutree.rcu_idle_gp_delay=1` 到内核参数。原始话题见[[2]](https://bbs.archlinux.org/viewtopic.php?id=169742)。

### 分辨率和屏幕扫描错误“EDID errors in Xorg.log”

这是由于NVIDIA的驱动程序没有检测显示器的EDID。你需要手动指定路径的EDID文件或以类似的方式提供相同的信息。

增加这些线路和变化部分反映你自己的系统：

 `/etc/X11/xorg.conf` 
```
Section "Device"
       	Option		"ConnectedMonitor" "CRT-0"
       	Option		"CustomEDID" "CRT-0:/sys/class/drm/card0-LVDS-1/edid"
	Option		"IgnoreEDID" "false"
	Option		"UseEDID" "true"
EndSection

```

如果xorg不会开始尝试更换所有CRT到DFB。显示器连接通过LVDS，card0是标识为英特尔卡。EDID二进制是这个目录。如果硬件配置不同，CustomEDID的值可能有所不同，但这已得到证实。不管怎样，路径都将从/sys/class/drm开始

或者你可以生成你的工具，如读取[read-edid](https://www.archlinux.org/packages/?name=read-edid),将驱动点指向这个文件。也可以使用modelines，但是务必要修改 "UseEDID" 和 "IgnoreEDID"。

### 锁定问题(lspci 挂起)

问题：lspci挂起，系统暂停失败，关机时挂起，optirun挂起。多出现在新的笔记本电脑或使用了类似bbswitch GTX的965m时（例如bumblebee）以及nouveau的情况。

当独立显卡接通电源，可能出现这种情况，参见 ([kernel bug 156341](https://bugzilla.kernel.org/show_bug.cgi?id=156341))。

具体解决方法参见 [this issue](https://github.com/Bumblebee-Project/Bumblebee/issues/764#issuecomment-234494238)。 你可以添加`acpi_osi="!Windows 2015"` 或`acpi_osi=! acpi_osi="Windows 2009"` 到[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")中。

### 笔记本电脑未发现屏幕/NVIDIA Optimus

检查`$ lspci | grep VGA`输入内容是否类似：

```
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)

```

NVIDIA驱动自319.12 Beta [[3]](http://www.nvidia.com/object/linux-display-amd64-319.12-driver.html)起已经包含在内核（版本3.9级以上)中。

另一个解决方案是安装[Intel](/index.php/Intel "Intel")驱动进行显示，如果需要运行3D软件，可以使用 [Bumblebee (简体中文)](/index.php/Bumblebee_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bumblebee (简体中文)")来使用NVIDIA显卡。

## 使用 nouveau

开源 [nouveau](/index.php/Nouveau "Nouveau") 驱动 ([xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)) 能靠一种叫 PRIME 的技术动态切换到 Intel 驱动 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)). 更多信息见 wiki 的 [PRIME](/index.php/PRIME "PRIME") 页面。

## 使用 Bumblebee

如果你想使用 Bumblebee, 并实现省电和其他有用特性，见 wiki 的 [Bumblebee](/index.php/Bumblebee "Bumblebee") 页面。

## 使用 nvidia-xrun

安装[nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/)。github上查看该项目 [https://github.com/Witko/nvidia-xrun](https://github.com/Witko/nvidia-xrun)