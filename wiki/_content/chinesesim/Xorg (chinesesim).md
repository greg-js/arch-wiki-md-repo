**Xorg** 是 X11 窗口系统的一个开源实现。Xorg 在 Linux 用户中非常流行，已经成为图形用户程序的必备条件，所以大部分发行版都提供了它。详情参见 [Xorg](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server") 维基文章或访问[Xorg 网站](http://www.x.org/wiki/)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 驱动安装](#.E9.A9.B1.E5.8A.A8.E5.AE.89.E8.A3.85)
*   [2 运行](#.E8.BF.90.E8.A1.8C)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
*   [4 输入设备](#.E8.BE.93.E5.85.A5.E8.AE.BE.E5.A4.87)
    *   [4.1 鼠标加速](#.E9.BC.A0.E6.A0.87.E5.8A.A0.E9.80.9F)
    *   [4.2 扩展鼠标按键](#.E6.89.A9.E5.B1.95.E9.BC.A0.E6.A0.87.E6.8C.89.E9.94.AE)
    *   [4.3 触摸板](#.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [4.4 触摸屏](#.E8.A7.A6.E6.91.B8.E5.B1.8F)
    *   [4.5 键盘设置](#.E9.94.AE.E7.9B.98.E8.AE.BE.E7.BD.AE)
*   [5 显示器设置](#.E6.98.BE.E7.A4.BA.E5.99.A8.E8.AE.BE.E7.BD.AE)
    *   [5.1 开始](#.E5.BC.80.E5.A7.8B)
    *   [5.2 多个显示器](#.E5.A4.9A.E4.B8.AA.E6.98.BE.E7.A4.BA.E5.99.A8)
        *   [5.2.1 多于一个显卡](#.E5.A4.9A.E4.BA.8E.E4.B8.80.E4.B8.AA.E6.98.BE.E5.8D.A1)
        *   [5.2.2 切换笔记本内部/外部显示的脚本](#.E5.88.87.E6.8D.A2.E7.AC.94.E8.AE.B0.E6.9C.AC.E5.86.85.E9.83.A8.2F.E5.A4.96.E9.83.A8.E6.98.BE.E7.A4.BA.E7.9A.84.E8.84.9A.E6.9C.AC)
    *   [5.3 显示大小和 DPI](#.E6.98.BE.E7.A4.BA.E5.A4.A7.E5.B0.8F.E5.92.8C_DPI)
        *   [5.3.1 手动设置DPI](#.E6.89.8B.E5.8A.A8.E8.AE.BE.E7.BD.AEDPI)
            *   [5.3.1.1 专有的NVIDIA驱动程序](#.E4.B8.93.E6.9C.89.E7.9A.84NVIDIA.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F)
    *   [5.4 DPMS](#DPMS)
*   [6 Composite](#Composite)
    *   [6.1 List of composite managers](#List_of_composite_managers)
*   [7 配置文件样例](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E6.A0.B7.E4.BE.8B)
    *   [7.1 示例1 : xorg.conf & /etc/X11/xorg.conf.d/10-evdev.conf](#.E7.A4.BA.E4.BE.8B1_:_xorg.conf_.26_.2Fetc.2FX11.2Fxorg.conf.d.2F10-evdev.conf)
*   [8 技巧和技巧](#.E6.8A.80.E5.B7.A7.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [8.1 调整 X 启动参数(/usr/bin/startx)](#.E8.B0.83.E6.95.B4_X_.E5.90.AF.E5.8A.A8.E5.8F.82.E6.95.B0.28.2Fusr.2Fbin.2Fstartx.29)
    *   [8.2 Virtual X session](#Virtual_X_session)
    *   [8.3 Nested X session](#Nested_X_session)
    *   [8.4 Starting GUI programs remotely](#Starting_GUI_programs_remotely)
    *   [8.5 On-demand disabling and enabling of input sources](#On-demand_disabling_and_enabling_of_input_sources)
*   [9 故障和修复](#.E6.95.85.E9.9A.9C.E5.92.8C.E4.BF.AE.E5.A4.8D)
    *   [9.1 通用问题](#.E9.80.9A.E7.94.A8.E9.97.AE.E9.A2.98)
    *   [9.2 Black screen, No protocol specified.., Resource temporarily unavailable for all or some users](#Black_screen.2C_No_protocol_specified...2C_Resource_temporarily_unavailable_for_all_or_some_users)
    *   [9.3 CTRL 右键无法与和oss keymap一起工作](#CTRL_.E5.8F.B3.E9.94.AE.E6.97.A0.E6.B3.95.E4.B8.8E.E5.92.8Coss_keymap.E4.B8.80.E8.B5.B7.E5.B7.A5.E4.BD.9C)
    *   [9.4 Ctrl-Alt-Backspace无法退出X](#Ctrl-Alt-Backspace.E6.97.A0.E6.B3.95.E9.80.80.E5.87.BAX)
        *   [9.4.1 System-wide](#System-wide)
        *   [9.4.2 User-specific](#User-specific)
    *   [9.5 Apple 的键盘问题](#Apple_.E7.9A.84.E9.94.AE.E7.9B.98.E9.97.AE.E9.A2.98)
    *   [9.6 触摸板点击不正常](#.E8.A7.A6.E6.91.B8.E6.9D.BF.E7.82.B9.E5.87.BB.E4.B8.8D.E6.AD.A3.E5.B8.B8)
    *   [9.7 额外的鼠标按键不工作](#.E9.A2.9D.E5.A4.96.E7.9A.84.E9.BC.A0.E6.A0.87.E6.8C.89.E9.94.AE.E4.B8.8D.E5.B7.A5.E4.BD.9C)
    *   [9.8 无法用"su"以root身份启动X客户端](#.E6.97.A0.E6.B3.95.E7.94.A8.22su.22.E4.BB.A5root.E8.BA.AB.E4.BB.BD.E5.90.AF.E5.8A.A8X.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [9.9 无法加载'(null)'字体](#.E6.97.A0.E6.B3.95.E5.8A.A0.E8.BD.BD.27.28null.29.27.E5.AD.97.E4.BD.93)
    *   [9.10 无法运行在frambuffer模式下](#.E6.97.A0.E6.B3.95.E8.BF.90.E8.A1.8C.E5.9C.A8frambuffer.E6.A8.A1.E5.BC.8F.E4.B8.8B)
    *   [9.11 Matrox显卡的DRI功能失效](#Matrox.E6.98.BE.E5.8D.A1.E7.9A.84DRI.E5.8A.9F.E8.83.BD.E5.A4.B1.E6.95.88)
    *   [9.12 修复：在出现GUI登录界面之前，不启动Xorg](#.E4.BF.AE.E5.A4.8D.EF.BC.9A.E5.9C.A8.E5.87.BA.E7.8E.B0GUI.E7.99.BB.E5.BD.95.E7.95.8C.E9.9D.A2.E4.B9.8B.E5.89.8D.EF.BC.8C.E4.B8.8D.E5.90.AF.E5.8A.A8Xorg)
    *   [9.13 X failed to start : Keyboard initialization failed](#X_failed_to_start_:_Keyboard_initialization_failed)
    *   [9.14 不使用 root 权限的 Xorg (v1.16)](#.E4.B8.8D.E4.BD.BF.E7.94.A8_root_.E6.9D.83.E9.99.90.E7.9A.84_Xorg_.28v1.16.29)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 位于[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库") 的软件包 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server)。

另外，安装位于 [xorg-server-utils](https://www.archlinux.org/packages/?name=xorg-server-utils) 组中的某些工具以进行某些特定的配置工作。其他一些有用的工具可以在 [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) 组中找到。

**提示：** 用户通常需要选择安装某个 [窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)") 或 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")以配合使用 X。

### 驱动安装

Linux 内核包含了开源的视频驱动，支持硬件加速的 framebuffers。OpenGL 和 X11 的 2D 加速需要用户空间工具。

如果不知道显卡类型，请执行如下命令进行查询：

```
$ lspci | grep -e VGA -e 3D

```

输入下面命令，查看所有**开源**驱动:

```
$ pacman -Ss xf86-video | less

```

`vesa`是一个支持大部分显卡的通用驱动，不提供任何 2D 和 3D 加速功能。要充分发挥显卡性能，请按下表安装驱动程序。推荐先使用开源驱动，这些驱动出问题的可能性较小。

| 厂商 | 类型 | 驱动 | [Multilib](/index.php/Multilib "Multilib") 软件包
(适用于 Arch x86_64 上的 32 位程序) | 文档 |
| **AMD/ATI** | 开源 | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) | [ATI (简体中文)](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)") |
| 闭源 | [catalyst](https://aur.archlinux.org/packages/catalyst/) | [lib32-catalyst-libgl](https://aur.archlinux.org/packages/lib32-catalyst-libgl/) | [AMD Catalyst (简体中文)](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AMD Catalyst (简体中文)") |
| **Intel** | 开源 | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) | [Intel graphics (简体中文)](/index.php/Intel_graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel graphics (简体中文)") |
| **Nvidia** | 开源 | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) | [Nouveau (简体中文)](/index.php/Nouveau_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Nouveau (简体中文)") |
| 闭源 | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) | [NVIDIA (简体中文)](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)") |
| [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) | [lib32-nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-libgl) |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-libgl) |

## 运行

*参见: [Start X at Login (简体中文)](/index.php/Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Start X at Login (简体中文)")*

**提示：** 最简单的方法是使用 [登录管理器](/index.php/%E7%99%BB%E5%BD%95%E7%AE%A1%E7%90%86%E5%99%A8 "登录管理器") 例如 [GDM](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)") 或 [SLiM](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)").

如果不用登陆管理器启动 X，需要安装软件包 [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit)。

`startx` 和 `xinit` 命令将启动 X 服务器和客户端(`startx` 脚本是更通用命令 `xinit` 的前端)。为了确定要运行的客户端，`startx`/`xinit` 先在用户目录解析 `~/.xinitrc` 文件，如果 `~/.xinitrc` 不存在，使用默认的 `/etc/X11/xinit/xinitrc`, 其中默认会使用 [Twm](/index.php/Twm "Twm") 窗口管理器，[Xclock](https://en.wikipedia.org/wiki/Xclock "wikipedia:Xclock") 和 [Xterm](/index.php/Xterm "Xterm")（需安装 [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) 和 [xterm](https://www.archlinux.org/packages/?name=xterm)）.

**注意:** X 必须在登陆的 tty 启动，这样才能保持 logind 会话。默认的`/etc/X11/xinit/xserverrc`已经进行了处理。

更多信息请阅读 [xinitrc (简体中文)](/index.php/Xinitrc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinitrc (简体中文)").

**注意:**

*   如果出现问题，请检查日志文件 `/var/log/Xorg.0.log`. 看看有没有以`(EE)`(代表错误) 或 `(WW)` (代表警告)开头的内容。
*   如果 `$HOME` 中有空 `.xinitrc` 文件，请删除或[修改它](/index.php/Xinitrc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinitrc (简体中文)")。否则 X 会显示空白屏幕，而且 `Xorg.0.log` 中没有任何错误。删除它会运行一个默认的环境。

## 配置

**Note:** Arch 提供了位于 `/usr/share/X11/xorg.conf.d` 的默认配置文件。通常情况下，用户无需进行额外的配置与修改即可正常使用。

Xorg 可以通过 `/etc/X11/xorg.conf` 或 `/etc/xorg.conf` 和位于 `/etc/X11/xorg.conf.d/` 的配置文件配置。用户可以创建自己的配置文件，需要以 `XX-` 开头(XX 是数字)并以`.conf` 结尾(例如 10 在 20 之前读取)。

此外，显卡驱动可能提供了自动配置工具，例如 NVIDIA 提供了 `nvidia-xconfig`，ATI 提供了 `aticonfig`。

## 输入设备

[udev](/index.php/Udev "Udev") 会自动检测硬件，[evdev](https://en.wikipedia.org/wiki/evdev "wikipedia:evdev") 可以用作绝大部分设备的即插即用驱动。Udev 由 [systemd](https://www.archlinux.org/packages/?name=systemd) 和 [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)需要通过 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server)提供，所以不需要显式安装。

你应该有`10-evdev.conf` 在 `/usr/share/X11/xorg.conf.d/` 目录,它管理键盘，鼠标，触摸板和触摸屏。

如果 evdev不支持您的设备, 请从[xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/)组安装需要的驱动程序. Alike evdev, [libinput](/index.php/Libinput "Libinput") ([xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)) is a driver which supports a wide array of hardware from all device categories.

### 鼠标加速

见 [Mouse acceleration (简体中文)](/index.php/Mouse_acceleration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mouse acceleration (简体中文)").

### 扩展鼠标按键

见 [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### 触摸板

见 [Touchpad Synaptics (简体中文)](/index.php/Touchpad_Synaptics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Touchpad Synaptics (简体中文)") 或 [libinput](/index.php/Libinput "Libinput").

### 触摸屏

见 [Touchscreen](/index.php/Touchscreen "Touchscreen").

### 键盘设置

见 [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## 显示器设置

### 开始

**注意:** 这一步是可选的，除非你知道在做什么，否则不要进行这一步。
但是如果你使用双监视器或者nouveau驱动，你**必须**执行这一步。参见[Nouveau#Configuration](/index.php/Nouveau#Configuration "Nouveau")。

首先，创建一个新的配置文件，例如`/etc/X11/xorg.conf.d/10-monitor.conf`。

将下列代码加入到上述配置文件中：

```
Section "Monitor"
    Identifier    "Monitor0"
EndSection

Section "Device"
    Identifier    "Device0"
    Driver        "vesa" #Choose the driver used for this monitor
EndSection

Section "Screen"
    Identifier    "Screen0"  #Collapse Monitor and Device section to Screen section
    Device        "Device0"
    Monitor       "Monitor0"
    DefaultDepth  16 #Choose the depth (16||24)
    SubSection "Display"
        Depth     16
        Modes     "1024x768_75.00" #Choose the resolution
    EndSubSection
EndSection

```

**Note:** By default, Xorg needs to be able to detect a monitor and will not start otherwise. A workaround is to create a configuration file such as the example above and thus avoid auto-configuring. A common case where this is necessary is a headless system, which boots without a monitor and starts Xorg automatically, either from a [virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console") at [login](/index.php/Start_X_at_login "Start X at login"), or from a [display manager](/index.php/Display_manager "Display manager").

### 多个显示器

See main article [Multihead](/index.php/Multihead "Multihead") for general information.

参见GPU的具体说明:

*   [NVIDIA#Multiple monitors](/index.php/NVIDIA#Multiple_monitors "NVIDIA")
*   [Nouveau#Dual head](/index.php/Nouveau#Dual_head "Nouveau")
*   [AMD Catalyst#Double Screen (Dual Head / Dual Screen / Xinerama)](/index.php/AMD_Catalyst#Double_Screen_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29 "AMD Catalyst")
*   [ATI#Dual Head setup](/index.php/ATI#Dual_Head_setup "ATI")

#### 多于一个显卡

你必须指定正确的驱动以使用你的显卡。

```
Section "Device"
    Identifier      "Screen0"
    Driver          "nouveau"
    BusID           "PCI:0:12:0"
EndSection

Section "Device"
    Identifier      "Screen1"
    Driver          "radeon"
    BusID           "PCI:1:0:0"
EndSection

```

为了获取你的BusID：

```
$ lspci | grep VGA
01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

这个示例的BusID是 1:0:0.

#### 切换笔记本内部/外部显示的脚本

这个脚本可以用于键盘快捷键中。

```
#!/bin/bash

IN="LVDS1"
EXT="VGA1"

if (xrandr | grep "$EXT" | grep "+")
    then
    xrandr --output $EXT --off --output $IN --auto
    else
        if (xrandr | grep "$EXT" | grep " connected")
            then
            xrandr --output $IN --off --output $EXT --auto
        fi
fi

```

为了获取内部/外部显示的名字，你可以输入：

```
# xrandr -q

```

如果你没有 `xrandr`, [install](/index.php/Pacman "Pacman") [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) 来获取它。

### 显示大小和 DPI

The DPI of the X server is determined in the following manner:

1.  dpi命令行选项具有最高优先级。
2.  If this is not used, the DisplaySize setting in the X config file is used to derive the DPI, given the screen resolution.
3.  If no DisplaySize is given, the monitor size values from DDC are used to derive the DPI, given the screen resolution.
4.  如果DDC不指定大小, 75 DPI默认使用。

In order to get correct dots per inch (DPI) set, the display size must be recognized or set. Having the correct DPI is especially necessary where fine detail is required (like font rendering). Previously, manufacturers tried to create a standard for 96 DPI (a 10.3" diagonal monitor would be 800x600, a 13.2" monitor 1024x768). These days, screen DPIs vary and may not be equal horizontally and vertically. For example, a 19" widescreen LCD at 1440x900 may have a DPI of 89x87\. To be able to set the DPI, the Xorg server attempts to auto-detect your monitor's physical screen size through the graphic card with [DDC](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel"). ~~When the Xorg server knows the physical screen size, it will be able to set the correct DPI depending on resolution size.~~

To see if your display size and DPI are detected/calculated correctly:

```
$ xdpyinfo | grep -B2 resolution

```

Check that the dimensions match your display size. If the Xorg server is not able to correctly calculate the screen size, it will default to 75x75 DPI and you will have to calculate it yourself.

If you have specifications on the physical size of the screen, they can be entered in the Xorg configuration file so that the proper DPI is calculated:

```
Section "Monitor"
    Identifier             "Monitor0"
    DisplaySize             286 179    # In millimeters
EndSection

```

If you only want to enter the specification of your monitor **without** creating a full xorg.conf create a new config file. For example (`/etc/X11/xorg.conf.d/90-monitor.conf`):

```
Section "Monitor"
    Identifier             "<default monitor>"
    DisplaySize            286 179    # In millimeters
EndSection

```

If you do not have specifications for physical screen width and height (most specifications these days only list by diagonal size), you can use the monitor's native resolution (or aspect ratio) and diagonal length to calculate the horizontal and vertical physical dimensions. Using the Pythagorean theorem on a 13.3" diagonal length screen with a 1280x800 native resolution (or 16:10 aspect ratio):

```
$ echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

This will give the pixel diagonal length and with this value you can discover the physical horizontal and vertical lengths (and convert them to millimeters):

```
$ echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
$ echo 'scale=5;(13.3/1509)*800*25.4'  | bc  # 179.01920

```

**Note:** This calculation works for monitors with square pixels; however, there is the seldom monitor that may compress aspect ratio (e.g 16:10 aspect resolution to a 16:9 monitor). If this is the case, you should measure your screen size manually.

#### 手动设置DPI

**Note:** While you can set any dpi you like and applications using Qt and GTK will scale accordingly, it's recommended to set it to 96, 120 (25% higher), 144 (50% higher), 168 (75% higher), 192 (100% higher) etc., to reduce scaling artifacts to GUI that use bitmaps. Reducing it below 96 dpi may not reduce size of graphical elements of GUI as typically the lowest dpi the icons are made for is 96.

For RandR compliant drivers (for example the open source ATI driver), you can set it by:

```
$ xrandr --dpi 144

```

**Note:** Applications that comply with the setting will not change immediately. You have to start them anew.

See [Execute commands after X start](/index.php/Execute_commands_after_X_start "Execute commands after X start") to make it permanent.

##### 专有的NVIDIA驱动程序

DPI can be set manually if you only plan to use one resolution ([DPI calculator](http://pxcalc.com/)):

```
Section "Monitor"
    Identifier             "Monitor0"
    Option                 "DPI" "96 x 96"
EndSection

```

You can manually set the DPI adding the options below on `/etc/X11/xorg.conf.d/20-nvidia.conf` (inside **Device** section):

```
Option              "UseEdidDpi" "False"
Option              "DPI" "96 x 96"

```

### DPMS

DPMS (显示器电源管理信号) 是一种技术，可以在计算机不使用时，可以使用显示器的省电行为. 这将允许您的显示器在预定时间段后自动进入待机。 见: [DPMS](/index.php/DPMS "DPMS")

## Composite

The Composite extension for X causes an entire sub-tree of the window hierarchy to be rendered to an off-screen buffer. Applications can then take the contents of that buffer and do whatever they like. The off-screen buffer can be automatically merged into the parent window or merged by external programs, called compositing managers. See the following article for more information: [compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")

### List of composite managers

*   **[Cairo Composite Manager](/index.php/Cairo_Compmgr "Cairo Compmgr")** — Cairo based composite manager

	[http://cairo-compmgr.tuxfamily.org/](http://cairo-compmgr.tuxfamily.org/) || [cairo-compmgr-git](https://aur.archlinux.org/packages/cairo-compmgr-git/)

*   **[Compiz](/index.php/Compiz "Compiz")** — Composite manager for Aiglx and Xgl, with plugins and CCSM

	[http://www.compiz.org/](http://www.compiz.org/) || [compiz](https://aur.archlinux.org/packages/compiz/)

*   **[Compton](/index.php/Compton "Compton")** — Compositor (a fork of xcompmgr-dana)

	[https://github.com/chjj/compton](https://github.com/chjj/compton) || [compton](https://www.archlinux.org/packages/?name=compton)

*   **[Xcompmgr](/index.php/Xcompmgr "Xcompmgr")** — Composite window-effects manager

	[http://cgit.freedesktop.org/xorg/app/xcompmgr/](http://cgit.freedesktop.org/xorg/app/xcompmgr/) || [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr)

*   **Unagi** — Modular compositing manager which aims written in C and based on XCB

	[http://projects.mini-dweeb.org/projects/unagi](http://projects.mini-dweeb.org/projects/unagi) || [unagi](https://aur.archlinux.org/packages/unagi/)

## 配置文件样例

Anyone who has an `xorg.conf` file written up that works, go ahead and post a link to it here for others to look at. Please do not in-line the entire configuration file; upload it somewhere else and link to it.

**请只贴热插拔示例否则注明配置未使用热插拔** (Xorg 1.8 = udev)

### 示例1 : `xorg.conf` & `/etc/X11/xorg.conf.d/10-evdev.conf`

这是 `/etc/X11/xorg.conf.d/10-evdev.conf` 配置键盘布局的示例:

**注意:** "InputDevice" 部分已经注释掉，因为它们由 10-evdev.conf 负责。

```
`xorg.conf`: [http://pastebin.com/raw.php?i=EuSKahkn](http://pastebin.com/raw.php?i=EuSKahkn)
`/etc/X11/xorg.conf.d/10-evdev.conf`: [http://pastebin.com/raw.php?i=4mPY35Mw](http://pastebin.com/raw.php?i=4mPY35Mw)
`/etc/X11/xorg.conf.d/10-monitor.conf` (VMware): [http://pastebin.com/raw.php?i=fJv8EXGb](http://pastebin.com/raw.php?i=fJv8EXGb)
`/etc/X11/xorg.conf.d/10-monitor.conf` (KVM): [http://pastebin.com/raw.php?i=NRz7v0Kn](http://pastebin.com/raw.php?i=NRz7v0Kn)

```

## 技巧和技巧

### 调整 X 启动参数(`/usr/bin/startx`)

参看X的选项：

```
$ man Xserver

```

以下的选项可以附加在`/usr/bin/startx`文件的`"defaultserverargs"`变量中.

*   为16位字体使能延缓字形加载：

```
-deferglyphs 16

```

### Virtual X session

To start another X session in, for example, `Ctrl+Alt+F8`, you need to type this on a console:

```
xinit /path/to/wm -- :1

```

Change "/path/to/wm" to your window manager start file or to your login manager like gdm or slim.

### Nested X session

To run a nested session of another desktop environment:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

This will launch a Window Maker session in a 1024 by 768 window within your current X session.

This needs the package [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest) to be installed.

### Starting GUI programs remotely

See main article: [SSH#X11 forwarding](/index.php/SSH#X11_forwarding "SSH").

### On-demand disabling and enabling of input sources

With the help of *xinput* you can temporarily disable or enable input sources. This might be useful, for example, on systems that have more than one mouse, such as the ThinkPads and you would rather use just one to avoid unwanted mouse clicks.

[Install](/index.php/Pacman "Pacman") the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Find the ID of the device you want to disable:

```
$ xinput

```

For example in a Lenovo ThinkPad T500, the output looks like this:

 `$ xinput` 
```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=11   [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=10   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=9    [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=12   [slave  keyboard (3)]

```

Disable the device with `xinput --disable *device_id*`, where *device_id* is the device ID you want to disable. In this example we will disable the Synaptics Touchpad, with the ID 10:

```
$ xinput --disable 10

```

To re-enable the device, just issue the opposite command:

```
$ xinput --enable 10

```

## 故障和修复

### 通用问题

如果你在使用Xorg中遇到问题，无法启动或者黑屏，鼠标键盘不能正常工作，那么先进行以下步骤：

*   查看log日志文件：`cat /var/log/Xorg.0.log`, 可以从 **X** 启动终端之外的虚拟控制台查看错误。注意所有以 `(EE)` 开头的行，EE 代表有错误。同时注意 `(WW)` 警告，可能预示着其他问题。
*   需要安装输入驱动：(鼠标、键盘、触摸板等)
*   最后，在[ATI](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)"), [Intel](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)")和[NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)")等文章中搜索常见问题。

如果还有问题，请到 Arch 论坛提问，请安装和使用[wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste):

 `#pacman -S wgetpaste` 

在论坛提问的帖子中，用 wgetpaste 提供如下文件的链接：

*   ~/.xinitrc
*   /etc/X11/xorg.conf
*   /var/log/Xorg.0.log
*   /var/log/Xorg.0.log.old

wgetpaste 用法：

 `$wgetpaste </path/to/file>` 
**注意:** 解决 X 相关问题时，请提供上面所说的内容的详细信息。

### Black screen, No protocol specified.., Resource temporarily unavailable for all or some users

X creates configuration and temporary files in current user's home directory. Make sure there is free disk space available on the partition your home directory resides in. Unfortunately, X server does not provide any more obvious information about lack of disk space in this case.

### CTRL 右键无法与和oss keymap一起工作

编辑 `/usr/share/X11/xkb/symbols/fr`，将:

```
include "level5(rctrl_switch)"

```

改成

```
// include "level5(rctrl_switch)"

```

然后重启 X 或者系统。

### Ctrl-Alt-Backspace无法退出X

#### System-wide

Within `/etc/X11/xorg.conf.d/10-evdev.conf`, simply add the following:

```
Section "InputClass"
    Identifier          "Keyboard Defaults"
    MatchIsKeyboard	"yes"
    Option              "XkbOptions" "terminate:ctrl_alt_bksp"
EndSection

```

**注意:** 在KDE中，这种全局设置没有任何效果。恢复的方法是，通过Kickoff启动器 > 计算机 > 系统设置打开系统设置窗口。点击“输入设备”，在新窗口中选择“键盘”，然后点击“高级”标签页。点选“配置键盘选项”选框。展开“杀死X服务器的键盘序列”菜单，确定选中 `Ctrl+Alt+Backspace` ，点击“应用”按钮然后关闭系统设置窗口。`Ctrl+Alt+Backspace` 又回来啦。

#### User-specific

另外一种方法是加入以下内容到`~/.xinitrc`：

```
setxkbmap -option terminate:ctrl_alt_bksp

```

**Note:** This setting has no effect on Gnome 3.

### Apple 的键盘问题

	*参见 [Apple Keyboard](/index.php/Apple_Keyboard "Apple Keyboard")*

### 触摸板点击不正常

	*参见: [Synaptics](/index.php/Synaptics "Synaptics")*

### 额外的鼠标按键不工作

	*参见：[Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working")*

### 无法用"su"以root身份启动X客户端

如果你遇到"Client is not authorized to connect to server"，尝试将以下内容

```
 session        optional        pam_xauth.so

```

加入到`/etc/pam.d/su`文件中。`pam_xauth` 就可以正常设置环境变量以及处理 `xauth` 密钥了。

### 无法加载'(null)'字体

*   一些程序无法运行，提示无法加载`(null)'字体.

这些软件包可能需要一些额外的字体。某些程序只能使用位图字体。 目前有两种主要的位图字体包：[xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi)、[xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi)。选择其中一个就可以了。通过下面这个命令查看显示设置：

```
$ xdpyinfo | grep resolution

```

根据显示信息选择合适dpi的字体即可(用75 或 100 代替XX)：

```
# pacman -S xorg-fonts-XXdpi

```

### 无法运行在frambuffer模式下

如果X启动失败，日志中有以下信息：

```
 (WW) Falling back to old probe method for fbdev
 (II) Loading sub module "fbdevhw"
 (II) LoadModule: "fbdevhw"
 (II) Loading /usr/lib/xorg/modules/linux//libfbdevhw.so
 (II) Module fbdevhw: vendor="X.Org Foundation"
        compiled for 1.6.1, module version = 0.0.2
        ABI class: X.Org Video Driver, version 5.0
 (II) FBDEV(1): using default device

 Fatal server error:
 Cannot run in framebuffer mode. Please specify busIDs        for all framebuffer devices

```

只需要卸载[xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev)就可以了。

### Matrox显卡的DRI功能失效

如果你使用的是Matrox显卡，在升级到Xorg7后它的DRI功能失效，试着在xorg.conf的显卡设备设置段Device section中加入下面一行：

```
Option "OldDmaInit" "On"

```

### 修复：在出现GUI登录界面之前，不启动Xorg

如果Xorg设置为自动启动并且出于某些原因你不想让它出现在 登录/显示 管理器之前，有两种办法:

*   将启动目标修改为 rescue.target. 参阅 [systemd#Change default target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").
*   如果 X 无法启动，而且 GRUB 超时时间设置成了 0,无法进 Grub 禁止 Xorg boot. 可以使用 Arch CD 启动，然后挂载配置文件所在分区，

	可以以root用户使用命令

```
# fdisk -l

```

	来查看你的全部分区。通常你所要的那个是形如 `/dev/sda1` 这样的东东。然后，使用命令

```
# mount /dev/sda1 /mnt

```

挂载该分区至 `/mnt`。 这样你的文件系统就挂载在了 `/mnt` 下。例如，可以删除 `gdm` 来阻止Xorg正常启动，或者做其他一些必需的改动。

### X failed to start : Keyboard initialization failed

If your hard disk is full, startx will fail. `/var/log/Xorg.0.log` will end with:

```
(EE) Error compiling keymap (server-0)
(EE) XKB: Couldn't compile keymap
(EE) XKB: Failed to load keymap. Loading default keymap instead.
(EE) Error compiling keymap (server-0)
(EE) XKB: Couldn't compile keymap
XKB: Failed to compile keymap
Keyboard initialization failed. This could be a missing or incorrect setup of xkeyboard-config.
Fatal server error:
Failed to activate core devices.
Please consult the The X.Org Foundation support  at [http://wiki.x.org](http://wiki.x.org)
for help.
Please also check the log file at "/var/log/Xorg.0.log" for additional information.
 (II) AIGLX: Suspending AIGLX clients for VT switch

```

Make some free space on your root partition and X will start.

### 不使用 root 权限的 Xorg (v1.16)

在 1.16 版及以后 [[1]](https://www.archlinux.org/news/xorg-server-116-is-now-available/)， Xorg 可能在 `logind` 的帮助下以用户特权运行。如此运行对系统的要求如下所示：

*   [systemd](/index.php/Systemd "Systemd")： 版本 >=216 以支持多实例；
*   经由 [xinit](/index.php/Xinit "Xinit") 启动 X： 显示管理器（登陆管理器）不被支持；
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")： implementations in proprietary display drivers fail [auto-detection](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/xorg-wrapper.c#n222) and require manually setting `needs_root_rights = no` in `/etc/X11/Xwrapper.config`.

If you do not fit these requirements, re-enable root rights in `/etc/X11/Xwrapper.config`:

```
needs_root_rights = *yes*

```

同时请参见 [Xorg.wrap(1)](http://manned.org/Xorg.wrap.1) 和 [Systemd/User#Xorg as a systemd user service](/index.php/Systemd/User#Xorg_as_a_systemd_user_service "Systemd/User")。