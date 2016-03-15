**翻译状态：** 本文是英文页面 [Touchpad_Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-11-04，点击[这里](https://wiki.archlinux.org/index.php?title=Touchpad_Synaptics&diff=0&oldid=280563)可以查看翻译后英文页面的改动。

本文描述了 ***Synaptics 输入驱动*** 的安装和配置过程，适用于大多数笔记本电脑上的Synaptics(或ALPS)触摸板

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 常用选项](#.E5.B8.B8.E7.94.A8.E9.80.89.E9.A1.B9)
    *   [2.2 其他选项](#.E5.85.B6.E4.BB.96.E9.80.89.E9.A1.B9)
    *   [2.3 GNOME](#GNOME)
    *   [2.4 MATE](#MATE)
    *   [2.5 实时配置](#.E5.AE.9E.E6.97.B6.E9.85.8D.E7.BD.AE)
        *   [2.5.1 命令行工具](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.B7.A5.E5.85.B7)
        *   [2.5.2 图形化工具](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E5.B7.A5.E5.85.B7)
*   [3 高级配置](#.E9.AB.98.E7.BA.A7.E9.85.8D.E7.BD.AE)
    *   [3.1 使用xinput来检测您的触摸板有什么功能](#.E4.BD.BF.E7.94.A8xinput.E6.9D.A5.E6.A3.80.E6.B5.8B.E6.82.A8.E7.9A.84.E8.A7.A6.E6.91.B8.E6.9D.BF.E6.9C.89.E4.BB.80.E4.B9.88.E5.8A.9F.E8.83.BD)
    *   [3.2 Synclient](#Synclient)
    *   [3.3 Evtest](#Evtest)
    *   [3.4 环状滚动](#.E7.8E.AF.E7.8A.B6.E6.BB.9A.E5.8A.A8)
    *   [3.5 自然滚动(触摸屏式滚动)](#.E8.87.AA.E7.84.B6.E6.BB.9A.E5.8A.A8.28.E8.A7.A6.E6.91.B8.E5.B1.8F.E5.BC.8F.E6.BB.9A.E5.8A.A8.29)
    *   [3.6 软开关](#.E8.BD.AF.E5.BC.80.E5.85.B3)
    *   [3.7 在打字时禁用触摸板](#.E5.9C.A8.E6.89.93.E5.AD.97.E6.97.B6.E7.A6.81.E7.94.A8.E8.A7.A6.E6.91.B8.E6.9D.BF)
        *   [3.7.1 使用掌压感应](#.E4.BD.BF.E7.94.A8.E6.8E.8C.E5.8E.8B.E6.84.9F.E5.BA.94)
        *   [3.7.2 利用 .xinitrc](#.E5.88.A9.E7.94.A8_.xinitrc)
        *   [3.7.3 利用登录管理器](#.E5.88.A9.E7.94.A8.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)
*   [4 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [4.1 xorg.conf.d/50-synaptics.conf在 GNOME 和 MATE 上失效](#xorg.conf.d.2F50-synaptics.conf.E5.9C.A8_GNOME_.E5.92.8C_MATE_.E4.B8.8A.E5.A4.B1.E6.95.88)
    *   [4.2 ALPS 触摸板](#ALPS_.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [4.3 触摸板无法工作, Xorg.0.log 中显示 "Query no Synaptics: 6003C8"](#.E8.A7.A6.E6.91.B8.E6.9D.BF.E6.97.A0.E6.B3.95.E5.B7.A5.E4.BD.9C.2C_Xorg.0.log_.E4.B8.AD.E6.98.BE.E7.A4.BA_.22Query_no_Synaptics:_6003C8.22)
    *   [4.4 触摸板被识别为"PS/2 Generic Mouse" 或者 "Logitech PS/2 mouse"](#.E8.A7.A6.E6.91.B8.E6.9D.BF.E8.A2.AB.E8.AF.86.E5.88.AB.E4.B8.BA.22PS.2F2_Generic_Mouse.22_.E6.88.96.E8.80.85_.22Logitech_PS.2F2_mouse.22)
    *   [4.5 Synaptics触摸板某些功能失效 (比如触击,滚动)](#Synaptics.E8.A7.A6.E6.91.B8.E6.9D.BF.E6.9F.90.E4.BA.9B.E5.8A.9F.E8.83.BD.E5.A4.B1.E6.95.88_.28.E6.AF.94.E5.A6.82.E8.A7.A6.E5.87.BB.2C.E6.BB.9A.E5.8A.A8.29)
    *   [4.6 在探测到外置鼠标后禁用触摸板](#.E5.9C.A8.E6.8E.A2.E6.B5.8B.E5.88.B0.E5.A4.96.E7.BD.AE.E9.BC.A0.E6.A0.87.E5.90.8E.E7.A6.81.E7.94.A8.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [4.7 指针跳跃](#.E6.8C.87.E9.92.88.E8.B7.B3.E8.B7.83)
    *   [4.8 在/dev/input/*中没有触摸板设备}](#.E5.9C.A8.2Fdev.2Finput.2F.2A.E4.B8.AD.E6.B2.A1.E6.9C.89.E8.A7.A6.E6.91.B8.E6.9D.BF.E8.AE.BE.E5.A4.87.7D)
    *   [4.9 Firefox和特殊触摸板事件](#Firefox.E5.92.8C.E7.89.B9.E6.AE.8A.E8.A7.A6.E6.91.B8.E6.9D.BF.E4.BA.8B.E4.BB.B6)
    *   [4.10 Opera:水平滚动问题](#Opera:.E6.B0.B4.E5.B9.B3.E6.BB.9A.E5.8A.A8.E9.97.AE.E9.A2.98)
    *   [4.11 在LG笔记本上的滚动和多功能](#.E5.9C.A8LG.E7.AC.94.E8.AE.B0.E6.9C.AC.E4.B8.8A.E7.9A.84.E6.BB.9A.E5.8A.A8.E5.92.8C.E5.A4.9A.E5.8A.9F.E8.83.BD)
    *   [4.12 外置鼠标的其他问题](#.E5.A4.96.E7.BD.AE.E9.BC.A0.E6.A0.87.E7.9A.84.E5.85.B6.E4.BB.96.E9.97.AE.E9.A2.98)
    *   [4.13 触摸板的同步问题](#.E8.A7.A6.E6.91.B8.E6.9D.BF.E7.9A.84.E5.90.8C.E6.AD.A5.E9.97.AE.E9.A2.98)
    *   [4.14 触击与按键点击之间出现延迟](#.E8.A7.A6.E5.87.BB.E4.B8.8E.E6.8C.89.E9.94.AE.E7.82.B9.E5.87.BB.E4.B9.8B.E9.97.B4.E5.87.BA.E7.8E.B0.E5.BB.B6.E8.BF.9F)
    *   [4.15 出现错误:SynPS/2 Synaptics TouchPad cannot grab event device, errno=16](#.E5.87.BA.E7.8E.B0.E9.94.99.E8.AF.AF:SynPS.2F2_Synaptics_TouchPad_cannot_grab_event_device.2C_errno.3D16)
    *   [4.16 从Windows系统重启后触摸板失去多点触控的能力](#.E4.BB.8EWindows.E7.B3.BB.E7.BB.9F.E9.87.8D.E5.90.AF.E5.90.8E.E8.A7.A6.E6.91.B8.E6.9D.BF.E5.A4.B1.E5.8E.BB.E5.A4.9A.E7.82.B9.E8.A7.A6.E6.8E.A7.E7.9A.84.E8.83.BD.E5.8A.9B)
    *   [4.17 一体化触摸板 (也被称为 ClickPads)](#.E4.B8.80.E4.BD.93.E5.8C.96.E8.A7.A6.E6.91.B8.E6.9D.BF_.28.E4.B9.9F.E8.A2.AB.E7.A7.B0.E4.B8.BA_ClickPads.29)
    *   [4.18 触摸板被误检测为鼠标 ("Elantech" 出品的触摸板)](#.E8.A7.A6.E6.91.B8.E6.9D.BF.E8.A2.AB.E8.AF.AF.E6.A3.80.E6.B5.8B.E4.B8.BA.E9.BC.A0.E6.A0.87_.28.22Elantech.22_.E5.87.BA.E5.93.81.E7.9A.84.E8.A7.A6.E6.91.B8.E6.9D.BF.29)
*   [5 链接](#.E9.93.BE.E6.8E.A5)

## 安装

Synaptics 驱动当前被打包为[xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)，可以从[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")。

## 配置

配置的主要方法是通过修改 [xorg](/index.php/Xorg "Xorg") Server 配置文件来完成配置。在安装了 `xf86-input-synaptics` 之后，一个默认的配置文件位于 `/etc/X11/xorg.conf.d/10-synaptics.conf`。

用户可以通过编辑这个文件来对驱动的各种选项进行配置，完整的选项列表请参考synaptics的man page：

 `$ man synaptics` 

### 常用选项

下面列举了大多数用户希望进行配置的选项。请注意，所有的这些选项都可以直接被添加到主配置文件 `/etc/X11/xorg.conf.d/10-synaptics.conf` 中，比如，下面的例子里，我们启用了水平，垂直和环形滚动:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 Section "InputClass"
       Identifier "touchpad"
       Driver "synaptics"
       MatchIsTouchpad "on"
              Option "TapButton1" "1"
              Option "TapButton2" "2"
              Option "TapButton3" "3"
              Option "VertEdgeScroll" "on"
              Option "VertTwoFingerScroll" "on"
              Option "HorizEdgeScroll" "on"
              Option "HorizTwoFingerScroll" "on"
              Option "CircularScrolling" "on"
              Option "CircScrollTrigger" "2"
              Option "EmulateTwoFingerMinZ" "40"
              Option "EmulateTwoFingerMinW" "8"
              ...
 EndSection

```

	**TapButton1**

	(integer) 配置 “当用一根手指在非角落区域触击时，哪个鼠标键点击事件被上报”

	**TapButton2**

	(integer) 配置 “当用两根手指在非角落区域触击时，哪个鼠标键点击事件被上报”

	**TapButton3**

	(integer) 配置 “当用三根手指在非角落区域触击时，哪个鼠标键点击事件被上报”

	**RBCornerButton**

	(integer) 配置 “当在右下角单指触及时，哪个鼠标键点击事件被上报"（使用`Option "RBCornerButton" "3"`来完成Ubuntu式的右键点击设定（右下角轻触代表点击右键））

	**RTCornerButton**

	(integer) 对右上角轻触进行配置，和RBCornerButton类似

	**VertEdgeScroll**

	(boolean) 在触摸板的由边缘滑动时，启用垂直滚动

	**HorizEdgeScroll**

	(boolean) 在触摸板的下边缘滑动时，启用水平滚动

	**VertTwoFingerScroll**

	(boolean) 启用双指垂直滚动

	**HorizTwoFingerScroll**

	(boolean) 启用双指水平滚动

	**EmulateTwoFingerMinZ/W**

	(integer) 使用这两个参数来对双指滚动的精度进行调教

这个[例子](/index.php?title=Touchpad_Synaptics/10-synaptics.conf_example&action=edit&redlink=1 "Touchpad Synaptics/10-synaptics.conf example (page does not exist)")包含了所有选项的简短介绍. 因为不同计算机的配置一般也不同. 我们推荐使用 [synclient](/index.php/Touchpad_Synaptics#Fine-tuning_with_synclient "Touchpad Synaptics")来对你的计算机进行针对性调教

**Note:** 如果你经常因为手掌扫过触摸板而导致TabButton2属性被触发(大多数时候都是"粘贴”动作)，而你又不介意关闭掉双指触击功能，请将`TapButton2`设置为0

### 其他选项

	**VertScrollDelta** and **HorizScrollDelta**

	(integer)配置滚动速度, 对它们的配置比较直观,因为值越高滚动精度就越高而速度越低.设置成负值就能实现类似OS X系统的"自然滚动"

	SHMConfig

	(boolean) 是否开启共享内存以支持实时调试. 现在这个选项已经无效,并且它也只能提供针对事件的实时调试

### GNOME

[GNOME](/index.php/GNOME "GNOME")用户可能必须对这些选项进行客制化，因为GNOME默认禁用了触击，水平滚动，并且不允许在打字时暂时禁用触摸板。

当在**Gnome 2**下想要修改这些设定时:

1.  运行 `gconf-editor`
2.  编辑 `/desktop/gnome/peripherals/touchpad/` 文件夹中的键.

当在**Gnome 3**下想要修改这些设定时:

1.  打开 *System Settings*.
2.  点击 *Mouse and Touchpad*.
3.  在 *Touchpad* 选项卡里对这些配置进行更改.

Gnome的配置监控程序可能会覆盖现存设定(比如在 `xorg.conf.d` 中进行的预设),而那些设定可能和您的配置完全不一样。不过，我们可以完全停止Gnome在鼠标设定上的监控:

1.  运行`dconf-editor`
2.  编辑 `/org/gnome/settings-daemon/plugins/mouse/`
3.  将 **active** 的勾选取消

这样，您对synaptics触摸板的设定就可以生效了。

**Remember**: 既然Gnome是基于用户配置的，当你运行了dconf-editor或者gconf-editor进行更改，那么这些变化也只会体现当前用户的会话上。你在其他账户上可能需要重复上述过程。

### MATE

在MATE上，可以通过类似于[GNOME](/index.php/GNOME "GNOME")的方法来配置触摸板：

1.  运行 `mateconf-editor`
2.  编辑 `desktop/mate/peripherals/touchpad/` 文件夹里面的键

可以通过下面的方法来阻止Mate配置守护程序改写当前配置：

1.  运行 `mateconf-editor`
2.  编辑 `/apps/mate_settings_daemon/plugins/mouse/`
3.  取消**active**勾选 .

### 实时配置

除了提供传统的配置方法，Synaptics驱动现在还支持实时配置。这意味着用户能通过软件来进行实时设置而不需要重启X服务器。在你将配置项添加到主配置文件之前，这个特性可以帮助你进行测试。

**Warning:** 实时配置是非永久的，当重启，挂起/恢复，或者重启udev后就会失效。所以这个功能只适合用来对配置进行测试和精校。

#### 命令行工具

*   **Note** :

**[Synclient](/index.php/Touchpad_Synaptics#Synclient "Touchpad Synaptics")** — cSynclient是一个可以对Synaptics驱动进行查询并进行配置的命令行工具，这个工具是由synaptics维护者开发并和synaptics驱动一起提供给用户

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)

**[xinput](/index.php/Touchpad_Synaptics#xinput "Touchpad Synaptics")** — 调试设备的小型通用命令行程序

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput)

#### 图形化工具

*   **GPointing Device Settings** — 提供对当前系统上的指针设备进行实时配置的图形界面(包括Synaptics触摸板),这个应用替代GSynaptics成为了对Synaptics驱动进行图形化配置的优先程序.

	[http://live.gnome.org/GPointingDeviceSettings](http://live.gnome.org/GPointingDeviceSettings) || [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings)

**Note:** 需要安装 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) 和 [libsynaptics](https://www.archlinux.org/packages/?name=libsynaptics) , GPointingDeviceSettings工具才能在Synaptics触摸板上运行!

*   **kcm-touchpad** — 在[KDE](/index.php/KDE "KDE")的一个新的触摸板配置工具，提供了一个在“系统设置”中的模块。在2014年2月发布，工作于KDE SC 4.12+。这将被作为一个 [synaptiks](https://aur.archlinux.org/packages/synaptiks/) 和 [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/) 的替代品。

	[https://projects.kde.org/projects/kde/workspace/kcm-touchpad/repository](https://projects.kde.org/projects/kde/workspace/kcm-touchpad/repository) || [kcm-touchpad](https://www.archlinux.org/packages/?name=kcm-touchpad)

## 高级配置

### 使用xinput来检测您的触摸板有什么功能

根据型号不同，Synaptics可能有以下特性:

*   拥有物理左键，物理中键，物理右键
*   能够进行两指检测
*   能够进行三指检测
*   能够配置分辨率

使用 `xinput list`来找到您的synaptics设备名

首先，找到触摸板的名字

 `$ xinput -list` 

然后，您可以使用`xipunt`来查看您的触摸板有什么特性

```
$ xinput list-props "SynPS/2 Synaptics TouchPad" | grep Capabilities

      Synaptics Capabillities (309):  1, 0, 1, 0, 0, 1, 1

```

从左到右，分别代表：

*   (1) 设备有物理左键
*   (0) 设备有物理中键
*   (1) 设备有物理右键
*   (0) 设备支持两指检测
*   (0) 设备支持三指检测
*   (1) 设备可以配置垂直分辨率
*   (1) 设备可以配置水平分辨率

使用`xinput list-props "SynPS/2 Synaptics TouchPad"` 来列出设备的所有属性

详情请阅读xinput和synaptics的帮助文档

### Synclient

在synaptics manpage里面列出的所有参数都可以通过synclient进行配置.下面命令列出了一个完整的用户设置的清单：

 `$ synclient -l` 

所有列出的参数都可以用synclient进行配置, 比如:

```
$ synclient PalmDetect=1 (to enable palm detection)
$ synclient TapButton1=1 (configure button events)
$ synclient TouchpadOff=1 (disable the touchpad)

```

使用synclient进行成功的设定和测试后,你可以将这些设定添加到`/etc/X11/xorg.conf.d/10-synaptics.conf`中

### Evtest

[evtest](/index.php/Evdev "Evdev")工具能够实时的显示触摸板上的压力和位置信息,允许对默认的Synaptics设定进行精校.可以通过如下方式启动evtest

```
$ evtest /dev/input/event*X*

```

*X*代表触摸板的ID,可以通过查看`cat /proc/bus/input/devices`的输出来获取它. evtest需要对设备进行排他访问,因此,evtest不能和X Server的实例共存.你可以通过杀死X Server进程或者在虚拟终端上运行evtest来解决这个问题(例如,通过`CTRL+ALT+2`来切换到2号虚拟终端)

### 环状滚动

Synaptics提供和ipod触控方式类似的环状滚动功能。您可以在触摸板上画圈，来代替在边缘上垂直或水平地滑动。有些用户发现这样滚动的更快也更精确.

添加下面几行到`/etc/X11/xorg.conf.d/10-synaptics.conf`中以启用环状滚动：

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 Section "InputDevice"
         ...
         Option      "CircularScrolling"          "on"
         Option      "CircScrollTrigger"          "0"
         ...
 EndSection

```

选项**CircScrollTrigger**可以设置为下面的值之一，它能够决定环状滚动应该从哪个边缘开始：

```
0    所有边缘
1    顶部边缘
2    右上角
3    右边缘
4    右下角
5    底部边缘
6    左下角
7    左边缘
8    左上角

```

设置一个非0值对于同时使用水平/垂直滚动和环状滚动的用户非常有用.设定后,会根据你开始的边缘决定到底使用哪种滚动.

如果您想要快速滚动，请在触摸板中部画小圈，相反，如果您想要慢速地且更精确地滚动，请画大圈。

### 自然滚动(触摸屏式滚动)

可以在synaptics上启用自然滚动(触摸屏那种滚动).只要将`VertScrollDelta`和`HorizScrollDelta`的值设定为负就行(翻转滚动方向):

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
    ...
    Option      "VertScrollDelta"          "-111"
    Option      "HorizScrollDelta"         "-111"
    ...
EndSection

```

### 软开关

有一个能启用禁用触摸板的软开关会方便许多，特别是您要大量录入文字而触摸板又很灵敏的时候.请参阅[#在探测到外置鼠标后禁用触摸板](#.E5.9C.A8.E6.8E.A2.E6.B5.8B.E5.88.B0.E5.A4.96.E7.BD.AE.E9.BC.A0.E6.A0.87.E5.90.8E.E7.A6.81.E7.94.A8.E8.A7.A6.E6.91.B8.E6.9D.BF)，它也许更方便,因为有一个守护程序自动启用/禁用触摸板.软开关的好处是可以主动启用/禁用触摸板.

如果你的系统上没有快捷键绑定工具,可以下载一个[xbindkeys](/index.php/Xbindkeys "Xbindkeys")

将下面的脚本保存到`/sbin/trackpad-toggle.sh`中：

 `/sbin/trackpad-toggle.sh` 
```
 #!/bin/bash

 synclient TouchpadOff=$(synclient -l | grep -c 'TouchpadOff.*=.*0')

```

最后绑定一个快捷键来运行这段脚本，如果采用xbindkeys(配置文件为`~/.xbindkeysrc`),那么修改如下：

 `~/.xbindkeysrc` 
```
 "/sbin/trackpad-toggle.sh"
     m:0x5 + c:65
     Control+Shift + space

```

重启 `xbindkeys`然后`Ctrl`+`Shift`+`Space`, 现在能够启用/禁用您的触摸板了吧！

当然您可以使用其它快捷键软件，例如Xfce4 ,GNOME都提供了快捷键设定工具.

### 在打字时禁用触摸板

#### 使用掌压感应

首先,你需要测试您的触摸板是否支持掌压感应,如果支持,需要测试设定是否精确:

```
$ synclient PalmDetect=1

```

试着打字,通过如下方式调整感应精度:

```
$ synclient PalmMinWidth=

```

PalmMinWidth用来设定接触面的最小值

```
$ synclient PalmMinZ=

```

PalmMinZ用来设定在什么压力下会启动掌压感应.

当你找到了合适的设定后,将它们加入 `/etc/X11/xorg.conf.d/10-synaptics.conf`中.

```
#synclient PalmDetect=1
Option "PalmDetect" "1"
#synclient PalmMinWidth=10
Option "PalmMinWidth" "10"
#synclient PalmMinZ=200
Option "PalmMinZ" "200"

```

#### 利用 `.xinitrc`

将下面一行添加到 `.xinitrc` 中（将这行添加在exec开头的行前,否则命令可能不会被执行）：

 `$ syndaemon -t -k -i 2 -d &` 

	**-i 2**参数

	设定一个等待时间，它决定了在最后一个键盘按键按下后要过多少秒后才重新启用触摸板。

	**-t**参数

	仅仅在打字时禁用触击和滚动而不禁用鼠标移动。

	**-k**

	告诉守护程序在监控键盘活动时忽略修饰键 (比如: 允许 Ctrl+单机左键).

	**-d**

	在后台做为守护程序启动.

更多的细节请参考manpage：

 `$ man syndaemon` 

如果您使用了登录管理器，那么您需要将上面的指令添加到登录管理器允许的地方。

#### 利用登录管理器

"-d"参数可以在登录前将syndaemon作为守护进程启动。

**对于Gnome(GDM)用户**

您需要利用Gnome启动程序首选项程序(Gnome's Startup Applications Preferences program)来将syndaemon做为守护进程启动。登录到Gnome中，找到**系统 > 首选项 > 启动程序**,在启动程序标签页，单击**“添加”**(**Add**)按钮，根据您的喜好给这个启动项起一个名字，然后输入注释(或留空).在**“命令”**(**Command**)栏中填入：

 `$ syndaemon -t -k -i 2 -d &` 

完成后，单击对话框中的**添加**(**Add**)按钮.请在**额外的启动程序**(**Addtional StartUp Programms**)清单中确保刚才添加的程序旁边的复选框被选中.最后,关闭窗口,完事大吉~

**对于KDE(KDM)用户**

到 **系统设置 > 高级 > 自动启动**，单击 **添加程序**，输入:

 ` syndaemon -t -k -i 2 -d &` 

并且选上“在命令行下运行”

## 疑难解答

### xorg.conf.d/50-synaptics.conf在 GNOME 和 MATE 上失效

[GNOME](/index.php/GNOME "GNOME") 和[MATE](/index.php/MATE "MATE") 会覆盖您的个性化设定,包括那些没法在GNOME或者MATE下进行图形化设定的选项.所以这导致`/etc/X11/xorg.conf.d/50-synaptics.conf` 里的设置不起作用了.请参考本文GNOME一节来避免这种情况的发生.

*   [Touchpad_Synaptics#GNOME](/index.php/Touchpad_Synaptics#GNOME "Touchpad Synaptics")

### ALPS 触摸板

对于ALPS触摸板，如果采用以上的配置不能正常工作，请尝试下面的配置：

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
  Section "ServerLayout"
    ...
    InputDevice    "USB Mouse" "CorePointer"
    InputDevice    "Touchpad"  "SendCoreEvents"
  EndSection

  Section "InputDevice"
    Identifier  "Touchpad"
    Driver  "synaptics"
    Option  "Device"   "/dev/input/mouse0"
    Option  "Protocol"   "auto-dev"
    Option  "LeftEdge"   "130"
    Option  "RightEdge"   "840"
    Option  "TopEdge"   "130"
    Option  "BottomEdge"   "640"
    Option  "FingerLow"   "7"
    Option  "FingerHigh"   "8"
    Option  "MaxTapTime"   "180"
    Option  "MaxTapMove"   "110"
    Option  "EmulateMidButtonTime"   "75"
    Option  "VertScrollDelta"   "20"
    Option  "HorizScrollDelta"   "20"
    Option  "MinSpeed"   "0.25"
    Option  "MaxSpeed"   "0.50"
    Option  "AccelFactor"   "0.010"
    Option  "EdgeMotionMinSpeed"   "200"
    Option  "EdgeMotionMaxSpeed"   "200"
    Option  "UpDownScrolling"   "1"
    Option  "CircularScrolling"   "1"
    Option  "CircScrollDelta"   "0.1"
    Option  "CircScrollTrigger"   "2"
    Option  "Emulate3Buttons"   "on"
  EndSection

```

### 触摸板无法工作, Xorg.0.log 中显示 "Query no Synaptics: 6003C8"

一般这是因为在系统上设置synaptics的方法不对:同时载入了两个synaptics模块.我们可以通过查看xorg log(`/var/log/Xorg.0.log`)来识别这种情况:

 `/var/log/Xorg.0.log` 
```
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "evdev touchpad catchall"
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "touchpad catchall"

```

这里可以看到两个不同的模块被载入了.在某些情况下,这会导致触摸板不可用.

我们可以通过将 `MatchDevicePath "/dev/input/event*"` 添加到 `/etc/X11/xorg.conf.d/10-synaptics.conf` 中来防止这种双重载入:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 Section "InputClass"
       Identifier "touchpad catchall"
       Driver "synaptics"
       MatchIsTouchpad "on"
       MatchDevicePath "/dev/input/event*"
             Option "TapButton1" "1"
             Option "TapButton2" "2"
             Option "TapButton3" "3"
 EndSection 

```

重启X Server,检查Xorg.0.log,这个错误应该会消失,触摸板也应该可用了

相关bug报告:[FS#20830](https://bugs.archlinux.org/task/20830)

相关论坛主题:

*   [https://bbs.archlinux.org/viewtopic.php?id=104769](https://bbs.archlinux.org/viewtopic.php?id=104769)
*   [https://bbs.archlinux.org/viewtopic.php?pid=825690](https://bbs.archlinux.org/viewtopic.php?pid=825690)

### 触摸板被识别为"PS/2 Generic Mouse" 或者 "Logitech PS/2 mouse"

这是由[kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=27442)(内核bug)造成的问题.被误识别的触摸板不能由Synaptics驱动.安装[AUR](/index.php/AUR "AUR")包[psmouse-elantech](https://aur.archlinux.org/packages/psmouse-elantech/)即可解决这个问题.

已知被影响的笔记本型号有:

*   Acer Aspire 7750G
*   Dell Latitude e6520 (ALPS touchpad)
*   Samsung NC110/NF210/QX310/QX410/QX510/SF310/SF410/SF510/RF410/RF510/RF710/RV515

可以通过如下方式检查你的触摸板是否由Synaptics驱动:

 `$ xinput list` 

详情请参考[这个帖子](https://bbs.archlinux.org/viewtopic.php?id=117109).

### Synaptics触摸板某些功能失效 (比如触击,滚动)

有些时候Synaptics触摸板会失去某些功能.即使正确配置了也不能使用诸如双指滚动,双指触发中键点击等功能.这个问题可能和上面提到的

如果阻止了重复加载模块后还有问题,可以尝试将"MatchIsTouchPad"配置项注释掉(这个选项synaptics默认开启)

### 在探测到外置鼠标后禁用触摸板

在[udev](/index.php/Udev "Udev")的协助下，可以实现当外置鼠标插入后自动禁用触摸板的功能。添加以下udev规则到`/etc/udev/rules.d/01-touchpad.rules`来实现这一点：

 `/etc/udev/rules.d/01-touchpad.rules` 
```
ACTION=="add", SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/<your username>/.Xauthority", ENV{ID_CLASS}="mouse", ENV{REMOVE_CMD}="/usr/bin/synclient TouchpadOff=0", RUN+="/usr/bin/synclient TouchpadOff=1"

```

[GDM](/index.php/GDM "GDM")将Xauthority文件存放在一个随机命名的文件夹中.所以,GDM下的udev规则一般是这样的:

```
ACTION=="add", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=1"
ACTION=="remove", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=0"

```

**Note:**

*   [udev](/index.php/Udev "Udev") 规则要求每个配置项必须独立占一行, 请注意格式! (以上"add","remove"分别是一条配置项)
*   这种配置和syndaemon冲突,请参考[#Using .xinitrc](#Using_.xinitrc).

如果想要在禁用触摸板的同时杀掉syndaemon进程,可以使用如下规则

```
ACTION=="add", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0",ENV{XAUTHORITY}="$result/database", RUN+="/bin/sh -c '/usr/bin/synclient TouchpadOff=1 ; sleep 1; /bin/killall syndaemon; '"

```

你可以配置与此类似的remove规则来阻止外置鼠标移除后syndaemon自动启动.手动启动syndaemon时,请注意使用合适的选项.

### 指针跳跃

某些用户会发现鼠标指针奇怪地在屏幕上“跳跃”，当前没有有效的办法来解决这个问题，但是有开发者正在关注这个BUG.

另一个可能是你遇到了和i8042控制器有关的*IRQ losses*问题(很多笔记本用这个i8042来控制键盘,触摸板).你有两个选择: 1.重新加载psmouse模组(rmmod&&insmod) 2.将i8042.nomux=1加入到启动行里,然后重启电脑

### 在`/dev/input/*`中没有触摸板设备}

如果出现这种情况，您可以利用这条命令来显示您的输入设备信息：

 `$ cat /proc/bus/input/devices` 

找寻一个名字为"SynPS/2 Synaptics TouchPad"的输入设备。"Handlers"一节就是触摸板设备的正确位置。

**样例输出**

 `$ cat /proc/bus/input/devices` 
```
 I: Bus=0011 Vendor=0002 Product=0007 Version=0000
 N: Name="SynPS/2 Synaptics TouchPad"
 P: Phys=isa0060/serio4/input0
 S: Sysfs=/class/input/input1
 H: Handlers=mouse0 event1
 B: EV=b
 B: KEY=6420 0 7000f 0

```

在这个例子中 `Handlers` 是 `mouse0` 和 `event1`，所以应该使用 `/dev/input/mouse0` 作为触摸板设备的位置。

### Firefox和特殊触摸板事件

默认的，firefox会设置触摸板上特殊区域完成特殊功能。你可以在地址栏输入**about:config**设置这些功能。编辑就是双击这些行，让true变成false，如果是数值你就必须手动改变了。

如果想让firefox不从滚动历史记录，而让它在网页滚动，你可以在about:config里面改变下面两个选项。

```
mousewheel.horizscroll.withnokey.action = 1
mousewheel.horizscroll.withnokey.sysnumlines = true

```

如果不想firefox当你点击触摸板右上（或者鼠标中键）把剪切板里面内容粘贴到地址栏并且打开，你需要设置如下内容为false：

```
middlemouse.contentLoadURL = false

```

### Opera:水平滚动问题

点击工具 -> 首选项 -> 高级 -> 快捷方式,在这里选择 "Opera Standard" 鼠标属性,点击“编辑”,在“应用程序”部分：

*   将 "Button 6" 键赋值给命令 "Scroll left"
*   将 "Button 7" 键赋值给命令 "Scroll right"

### 在LG笔记本上的滚动和多功能

这些问题可能出现在多种型号的LG笔记本上。 症状包括：当按下鼠标键1时snaptics误认为同时有ScrollUP操作和一个鼠标键1按下；鼠标键2的情况类似.

滚动问题可以通过添加下面一行到`xorg.conf`中：

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option "UpDownScrolling" "0"` 

注意这会让synaptics对其它键的响应出错。有一个Oskar Sandberg写的补丁[[1]](http://www.math.chalmers.se/~ossa/linux/lg_tx_express.html) 能够解决这个问题。

但是不能为最新版的synaptics驱动打上面的补丁，编译会出错。您可以用GIT包来安装synaptics[[2]](http://web.telia.com/~u89404340/touchpad/synaptics/.git) 。

AUR中也提供了一个相应的包：[xf86-input-synaptics-lg](https://aur.archlinux.org/packages/xf86-input-synaptics-lg/)

To build the package after downloading the tarball and unpacking it, execute:

 `$ cd synaptics-git`  `$ makepkg` 

### 外置鼠标的其他问题

首先，你需要确定你的外部鼠标描述设置里面包含（或者类似）这一行：

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option     "Device" "/dev/input/mice"` 

如果"Device"行不一样，改成如上的，并且重新启动X。如果没有解决，修改"Server Layout"设置，将**touchpad**设置为 CorePointer：

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "Touchpad" "CorePointer"` 

将你的外接鼠标设置为"SendCoreEvents":

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "USB Mouse" "SendCoreEvents"` 

最后，将这个添加到你的外接鼠标设置里面去：

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option      "SendCoreEvents"    "true"` 

如果还是不行，说不定是鼠标硬件有问题。请检查是不是bug，或者查看论坛，看是否有人有更好的解决方法。

### 触摸板的同步问题

有些时候指针会没有原因地“卡住”几秒或随机乱动。可以在`/var/log/messages.log`中看到出现了如下提示：

 `/var/log/messages.log`  `psmouse.c: TouchPad at isa0060/serio1/input0 lost synchronization, throwing 3 bytes away` 

这个问题没有一个通用的解决办法，但是您可以尝试以下的方法：

*   如果您使用CPU频率调节，不要使用"ondemand"模式而是"performance"模式 ，因为触摸板可能会在cpu频率变化时失去同步。
*   尝试不要使用ACPI电池监视器。
*   尝试用"proto=imps"选项载入pmouse模块，添加下面一行到`/etc/modprobe.d/modprobe.conf`中

 `/etc/modprobe.d/modprobe.conf`  `options psmouse proto=imps` 

*   尝试其它桌面环境。据某些用户报告，这个问题仅在使用Xfce，GNOME时才出现，不知道什么原因。

### 触击与按键点击之间出现延迟

如果出现了这种情况,建议启用FastTaps

将**Option "FastTaps" "1"** 添加到`/etc/X11/xorg.conf.d/10-synaptics.conf` 中:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
 Section "InputClass"
      Identifier "Synaptics Touchpad"
      Driver "synaptics"
      ...
      Option "FastTaps" "1"
      ...
 EndSection

```

### 出现错误:SynPS/2 Synaptics TouchPad cannot grab event device, errno=16

如果你使用Xorg 7.4，查看Xorg日志(/var/log/Xorg.0.log)时候可能会发现有这么一条警告信息。这是因为当使用linux2.6事件协议，驱动默认会试图独占此设备。失败就会出现此条提示。也就是说其他无论是内核空间还是用户空间的程序都无法获取此设备上的信号。当你的xorg.conf里面还定义了一个/dev/misc输入设备时候，这点很有用。但是如果你想测试设备的信号，那么就很麻烦了。

开启和关闭这项功能，可以修改你定义的xorg.conf的触摸板部分:

```
Section "InputDevice"
       ...
       Option "GrabEventDevice" "*boolean*"
       ...
EndSection

```

*boolean*部分可以是yes或者false，分别代表启用和禁止此功能。

当然你也可以使用synclient来调整，不过不能马上生效，只有触摸板驱动被禁用然后重新启用才能有效果。你可以通过切换到控制台然后切换回X来实现。

### 从Windows系统重启后触摸板失去多点触控的能力

许多驱动都会在电脑启动时将固件载入到内存中.这些固件信息在重启后不一定会被清除,而且有可能和Linux下的驱动不兼容.唯一清除内存中此类信息的方法就是用关机取代重启.在实践中,一般认为不同操作系统的切换最好不要用重启来进行.

### 一体化触摸板 (也被称为 ClickPads)

一些笔记本使用按键与触摸板面一体的触摸板.比如HP 4500系列笔记本,ThinkPad X220,X1 系列笔记本.默认情况下所有按键都被识别为左键,这样就不能使用右键中键,Click-Drag手势等功能. 在synaptics 1.6.0版驱动之前,一般使用第三方补丁来支持此类设备.但从1.6.0开始,Synaptics使用*mtdev*库实现了对多点触控的原生支持. 请注意,尽管支持多点触控,但是Synaptics驱动不会识别是不是不同的手指(至少到1.7.1都是这样),这样的话,当使用物理按键或者拖放手势时会有一些奇怪的现象出现.xf86-input-mtrack驱动对多点触控有更好的支持.

可以修改`/etc/X11/xorg.conf.d/50-synaptics.conf`来启用其他按键(或者给自定义的synaptics配置文件赋一个更高的优先级(前缀号更高),比如55-synaptics.conf):

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
...
Option "ClickPad"         "true"
Option "EmulateMidButtonTime" "0"
Option "SoftButtonAreas"  "50% 0 82% 0 0 0 0 0"
...

```

这三个选项是开启其他按键的关键,第一个启用多点触控,第二个关闭中键模拟(ClickPad不支持),第三个定义软按键区域

SoftButtonAreas选项的格式是(请参考`man 4 synaptics`):

 `RightButtonAreaLeft RightButtonAreaRight RightButtonAreaTop RightButtonAreaBottom  MiddleButtonAreaLeft MiddleButtonAreaRight MiddleButtonAreaTop MiddleButtonAreaBottom` 

上面的例子一般在synaptics驱动包提供的文档中都能找到,它将触摸板的X坐标50%以右,Y坐标82%以下区域定义为右键.这里没有中键的定义,.定义的时候请注意:

```
**将边缘设置为0代表将边缘设置到当前方向的无限远处.**

```

下面的例子将右键定义为X坐标60%以右,Y坐标82%以下;X坐标40%以右,59%以左,Y坐标82%以下被定义为中键

```
...
Option     "SoftButtonAreas"  "60% 0 82% 0 40% 59% 82% 0"
...

```

可以使用`synclient`来检查新的软按键区域设置:

 `$ synclient -l | grep -i ButtonArea` 
```
        RightButtonAreaLeft     = 3914
        RightButtonAreaRight    = 0
        RightButtonAreaTop      = 3918
        RightButtonAreaBottom   = 0
        MiddleButtonAreaLeft    = 3100
        MiddleButtonAreaRight   = 3873
        MiddleButtonAreaTop     = 3918
        MiddleButtonAreaBottom  = 0

```

如果发现上述设定失效,请确认是否有其他设置覆盖了您的设置(比如,一些AUR包给其配置档赋予了很高的优先级)

### 触摸板被误检测为鼠标 ("Elantech" 出品的触摸板)

This can happend on some laptops with elantech touchpad, for example ASUS x53s. In this situation you need [psmouse-elantech](https://aur.archlinux.org/packages/psmouse-elantech/) package from [AUR](/index.php/AUR "AUR"). 这个问题一般发生在使用Elantech(义发科技)出品的触摸板上,比如ASUS x53s.安装[psmouse-elantech](https://aur.archlinux.org/packages/psmouse-elantech/)即可解决这个问题

## 链接

*   [Synaptics 触摸板驱动](http://cgit.freedesktop.org/xorg/driver/xf86-input-synaptics/)