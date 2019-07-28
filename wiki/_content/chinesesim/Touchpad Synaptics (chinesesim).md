**翻译状态：** 本文是英文页面 [Touchpad_Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-01，点击[这里](https://wiki.archlinux.org/index.php?title=Touchpad_Synaptics&diff=0&oldid=443547)可以查看翻译后英文页面的改动。

相关文章

*   [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")

**警告:** `xf86-input-synaptics` 已经停止维护，请尽量使用 [libinput](/index.php/Libinput "Libinput")。

本文描述了 ***Synaptics 输入驱动*** 的安装和配置过程，适用于大多数笔记本电脑上的Synaptics(或ALPS)触摸板。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 常用选项](#常用选项)
    *   [2.2 实时配置](#实时配置)
        *   [2.2.1 命令行工具](#命令行工具)
        *   [2.2.2 图形化工具](#图形化工具)
    *   [2.3 其他选项](#其他选项)
    *   [2.4 Xfce4/Cinnamon](#Xfce4/Cinnamon)
    *   [2.5 MATE](#MATE)
*   [3 高级配置](#高级配置)
    *   [3.1 使用xinput来检测您的触摸板有什么功能](#使用xinput来检测您的触摸板有什么功能)
    *   [3.2 Evtest](#Evtest)
    *   [3.3 xev](#xev)
    *   [3.4 环状滚动](#环状滚动)
    *   [3.5 自然滚动(触摸屏式滚动)](#自然滚动(触摸屏式滚动))
    *   [3.6 软开关](#软开关)
    *   [3.7 在打字时禁用触摸板](#在打字时禁用触摸板)
        *   [3.7.1 使用驱动的掌压感应](#使用驱动的掌压感应)
        *   [3.7.2 使用 syndaemon](#使用_syndaemon)
    *   [3.8 检测到鼠标后禁用触摸板](#检测到鼠标后禁用触摸板)
        *   [3.8.1 基本桌面](#基本桌面)
        *   [3.8.2 GDM](#GDM)
            *   [3.8.2.1 With syndaemon running](#With_syndaemon_running)
            *   [3.8.2.2 touchpad-state](#touchpad-state)
        *   [3.8.3 GNOME](#GNOME)
        *   [3.8.4 KDE](#KDE)
        *   [3.8.5 System with multiple X sessions](#System_with_multiple_X_sessions)
    *   [3.9 一体化触摸板 (也被称为 ClickPads)](#一体化触摸板_(也被称为_ClickPads))
        *   [3.9.1 Bottom edge correction](#Bottom_edge_correction)
*   [4 疑难解答](#疑难解答)
    *   [4.1 在从挂起/休眠恢复后触摸板不工作](#在从挂起/休眠恢复后触摸板不工作)
    *   [4.2 xorg.conf.d/70-synaptics.conf在 MATE 上失效](#xorg.conf.d/70-synaptics.conf在_MATE_上失效)
    *   [4.3 触摸板无法工作, Xorg.0.log 中显示 "Query no Synaptics: 6003C8"](#触摸板无法工作,_Xorg.0.log_中显示_"Query_no_Synaptics:_6003C8")
    *   [4.4 触摸板被识别为"PS/2 Generic Mouse" 或者 "Logitech PS/2 mouse"](#触摸板被识别为"PS/2_Generic_Mouse"_或者_"Logitech_PS/2_mouse")
        *   [4.4.1 Elan Touchpad](#Elan_Touchpad)
        *   [4.4.2 Laptops with touchscreen & touchpad](#Laptops_with_touchscreen_&_touchpad)
    *   [4.5 Synaptics触摸板某些功能失效 (比如触击,滚动)](#Synaptics触摸板某些功能失效_(比如触击,滚动))
        *   [4.5.1 在一些笔记本的Elantech touchpads触摸板多点触控失效](#在一些笔记本的Elantech_touchpads触摸板多点触控失效)
    *   [4.6 指针跳跃](#指针跳跃)
    *   [4.7 在/dev/input/*中没有触摸板设备}](#在/dev/input/*中没有触摸板设备})
    *   [4.8 Firefox和特殊触摸板事件](#Firefox和特殊触摸板事件)
        *   [4.8.1 Firefox 17.0 and later](#Firefox_17.0_and_later)
    *   [4.9 Opera:水平滚动问题](#Opera:水平滚动问题)
    *   [4.10 在LG笔记本上的滚动和多功能](#在LG笔记本上的滚动和多功能)
    *   [4.11 外置鼠标的其他问题](#外置鼠标的其他问题)
    *   [4.12 触摸板的同步问题](#触摸板的同步问题)
    *   [4.13 触击与按键点击之间出现延迟](#触击与按键点击之间出现延迟)
    *   [4.14 出现错误:SynPS/2 Synaptics TouchPad cannot grab event device, errno=16](#出现错误:SynPS/2_Synaptics_TouchPad_cannot_grab_event_device,_errno=16)
    *   [4.15 从Windows系统重启后触摸板失去多点触控的能力](#从Windows系统重启后触摸板失去多点触控的能力)
    *   [4.16 Touchpad not recognized after shutdown from Arch](#Touchpad_not_recognized_after_shutdown_from_Arch)
    *   [4.17 Trackpoint and Clickpad](#Trackpoint_and_Clickpad)
    *   [4.18 ASUS Touchpads only recognised as PS/2 FocalTech emulated mouse](#ASUS_Touchpads_only_recognised_as_PS/2_FocalTech_emulated_mouse)
*   [5 参阅](#参阅)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)。

## 配置

配置的主要方法是通过修改 [xorg](/index.php/Xorg "Xorg") Server 配置文件来完成配置。在安装了 `xf86-input-synaptics` 之后，一个默认的配置文件位于 `/usr/share/X11/xorg.conf.d/70-synaptics.conf`。

用户可以将此文件复制到 `/etc/X11/xorg.conf.d/`然后编辑配置，完整的选项列表请参考synaptics的 `synaptics(4)` 手册页。

### 常用选项

下面列举了大多数用户希望进行配置的选项。比如，下面的例子里，我们启用了水平，垂直和环形滚动:

 `/etc/X11/xorg.conf.d/70-synaptics.conf` 
```
 Section "InputClass"
       Identifier "touchpad"
       Driver "synaptics"
       MatchIsTouchpad "on"
              Option "TapButton1" "1"
              Option "TapButton2" "3"
              Option "TapButton3" "2"
              Option "VertEdgeScroll" "on"
              Option "VertTwoFingerScroll" "on"
              Option "HorizEdgeScroll" "on"
              Option "HorizTwoFingerScroll" "on"
              Option "CircularScrolling" "on"
              Option "CircScrollTrigger" "2"
              Option "EmulateTwoFingerMinZ" "40"
              Option "EmulateTwoFingerMinW" "8"
              Option "FingerLow" "30"
              Option "FingerHigh" "50"
              Option "MaxTapTime" "125"
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

	**FingerLow**

	(integer) 手指压力低于此数值时视为手指移开。

	**FingerHigh**

	(integer) 手指压力高于此数值时视为手指按压.

	**MaxTapTime**

	Determines how "crisp" a tap must be to be considered a real tap. Decrease the value to require a more crisp tap. Properly adjusting this parameter can reduce false positives when the hands hover over or lightly touch the pad.

	**VertScrollDelta** and **HorizScrollDelta**

	(integer) configures the speed of scrolling, it is a bit counter-intuitive because higher values produce greater precision and thus slower scrolling. Negative values cause natural scrolling like in OS X.

这个[例子](/index.php?title=Touchpad_Synaptics/10-synaptics.conf_example&action=edit&redlink=1 "Touchpad Synaptics/10-synaptics.conf example (page does not exist)")包含了所有选项的简短介绍. 因为不同计算机的配置一般也不同. 我们推荐使用 [synclient](/index.php/Touchpad_Synaptics#Synclient "Touchpad Synaptics")来对你的计算机进行针对性调教

如果你经常因为手掌扫过触摸板而导致TabButton2属性被触发(大多数时候都是"粘贴”动作)，而你又不介意关闭掉双指触击功能，请将`TapButton2`设置为0.

Recent versions include a "Coasting" feature, enabled by default, which may have the undesired effect of continuing almost any scrolling until the next tap or click, even if you are no longer touching the touchpad. This means that to scroll just a bit, you need to scroll (by using the edge, or a multitouch option) and then almost immediately tap the touchpad, otherwise scrolling will continue forever. If wish to avoid this, set `CoastingSpeed` to 0.

如果触摸板太敏感，可以使用更高的 `FingerLow` 和 `FingerHigh` 值，`FingerLow` 应该比 `FingerHigh` 小。

### 实时配置

除了提供传统的配置方法，Synaptics驱动现在还支持实时配置。这意味着用户能通过软件来进行实时设置而不需要重启X服务器。在你将配置项添加到主配置文件之前，这个特性可以帮助你进行测试。

**Warning:** 实时配置是非永久的，当重启，挂起/恢复，或者重启udev后就会失效。所以这个功能只适合用来对配置进行测试和精校。

#### 命令行工具

**[Synclient](/index.php/Touchpad_Synaptics#Synclient "Touchpad Synaptics")** — Synclient是一个可以对Synaptics驱动进行查询并进行配置的命令行工具，这个工具是由synaptics维护者开发并和synaptics驱动一起提供给用户

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)

**[xinput](/index.php/Touchpad_Synaptics#Using_xinput_to_determine_touchpad_capabilities "Touchpad Synaptics")** — 调试设备的小型通用命令行程序

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput)

#### 图形化工具

*   **GPointing Device Settings** — 提供对当前系统上的指针设备进行实时配置的图形界面(包括Synaptics触摸板),这个应用替代GSynaptics成为了对Synaptics驱动进行图形化配置的优先程序.

	[http://live.gnome.org/GPointingDeviceSettings](http://live.gnome.org/GPointingDeviceSettings) || [gpointing-device-settings](https://aur.archlinux.org/packages/gpointing-device-settings/)

**Note:** 需要安装 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) 和 [libsynaptics](https://aur.archlinux.org/packages/libsynaptics/) , GPointingDeviceSettings工具才能在Synaptics触摸板上运行!

*   **kcm-touchpad** — 在[KDE](/index.php/KDE "KDE")的一个新的触摸板配置工具，提供了一个在“系统设置”中的模块。在2014年2月发布，工作于KDE SC 4.12+。这将被作为一个 [synaptiks](https://aur.archlinux.org/packages/synaptiks/) 和 [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/) 的替代品。

	[https://projects.kde.org/projects/kde/workspace/kcm-touchpad/repository](https://projects.kde.org/projects/kde/workspace/kcm-touchpad/repository) || [kcm-touchpad](https://www.archlinux.org/packages/?name=kcm-touchpad)

### 其他选项

	**VertScrollDelta** and **HorizScrollDelta**

	(integer)配置滚动速度, 对它们的配置比较直观,因为值越高滚动精度就越高而速度越低.设置成负值就能实现类似OS X系统的"自然滚动"

	SHMConfig

	(boolean) 是否开启共享内存以支持实时调试. 现在这个选项已经无效,并且它也只能提供针对事件的实时调试

### Xfce4/Cinnamon

当在**XFCE 4**下想要修改这些设定时:

1.  打开 *System Settings*.
2.  点击 *Mouse and Touchpad*.
3.  在 *Touchpad* 选项卡里对这些配置进行更改.

To change these settings in **Cinnamon**:

1.  Open *Cinnamon System Settings*.
2.  Click *Mouse and Touchpad*.
3.  Change the settings on the *Touchpad* tab.

### MATE

在MATE上，可以通过下面方法配置触摸板：

1.  运行 `dconf-editor`
2.  编辑 `org.mate.peripherals-touchpad` 文件夹里面的键

可以通过下面的方法来阻止Mate配置守护程序改写当前配置：

1.  运行 `dconf-editor}`
`*   编辑 `org.mate.SettingsDaemon.plugins.mouse`*   取消**active**勾选 .`

`

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

`
```
`$ xinput list-props "SynPS/2 Synaptics TouchPad"` 

```

### Evtest

[evtest](/index.php/Evdev "Evdev")工具能够实时的显示触摸板上的压力和位置信息,允许对默认的Synaptics设定进行精校.可以通过如下方式启动evtest

```
$ evtest /dev/input/event*X*

```

*X*代表触摸板的ID,可以通过查看`cat /proc/bus/input/devices`的输出来获取它. evtest需要对设备进行排他访问,因此,evtest不能和X Server的实例共存.你可以通过杀死X Server进程或者在虚拟终端上运行evtest来解决这个问题(例如,通过`CTRL+ALT+2`来切换到2号虚拟终端)

### xev

工具 [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) 可以实时显示按压、点击、压力、位置和其它检测到的数据，可以更深入的优化 Synaptics 设置。xev 可以通过 "-event" 参数设置报告的事件。

### 环状滚动

Synaptics提供和ipod触控方式类似的环状滚动功能。您可以在触摸板上画圈，来代替在边缘上垂直或水平地滑动。有些用户发现这样滚动的更快也更精确.

添加下面几行到`/etc/X11/xorg.conf.d/70-synaptics.conf`中以启用环状滚动：

 `/etc/X11/xorg.conf.d/70-synaptics.conf` 
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

 `/etc/X11/xorg.conf.d/70-synaptics.conf` 
```
Section "InputClass"
    ...
    Option      "VertScrollDelta"          "-111"
    Option      "HorizScrollDelta"         "-111"
    ...
EndSection

```

### 软开关

有一个能启用禁用触摸板的软开关会方便许多，可以用 *xinput* 脚本绑定到键盘事件，详情参考 [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg")。

 `/usr/local/bin/touchpad_toggle.sh` 
```
#!/bin/bash

declare -i ID
ID=`xinput list | grep -Eio '(touchpad|glidepoint)\s*id\=[0-9]{1,2}' | grep -Eo '[0-9]{1,2}'`
declare -i STATE
STATE=`xinput list-props $ID|grep 'Device Enabled'|awk '{print $4}'`
if [ $STATE -eq 1 ]
then
    xinput disable $ID
    # echo "Touchpad disabled."
    # notify-send 'Touchpad' 'Disabled' -i /usr/share/icons/Adwaita/48x48/devices/input-touchpad.png
else
    xinput enable $ID
    # echo "Touchpad enabled."
    # notify-send 'Touchpad' 'Enabled' -i /usr/share/icons/Adwaita/48x48/devices/input-touchpad.png
fi

```

**Tip:** 使用 [bumblebee](/index.php/Bumblebee "Bumblebee") 下的外置显示时，可以通过在命令中加入 `DISPLAY=:8` 设置第二个 X Server.

此外可以使用 `synclient` 切换 touchpad. 这个方式仅能禁用触摸事件，无法禁用物理按键的使用：

 `/sbin/trackpad-toggle.sh` 
```
 #!/bin/bash

 synclient TouchpadOff=$(synclient -l | grep -c 'TouchpadOff.*=.*0')

```

### 在打字时禁用触摸板

#### 使用驱动的掌压感应

首先,你需要测试您的触摸板是否支持掌压感应,如果支持,需要测试设定是否精确:

```
$ synclient PalmDetect=1

```

试着打字,通过如下方式调整感应精度，PalmMinWidth 用来设定接触面的最小值

```
$ synclient PalmMinWidth=8

```

PalmMinZ用来设定在什么压力下会启动掌压感应

```
$ synclient PalmMinZ=100

```

**Tip:** 可以使用 [evtest](https://www.archlinux.org/packages/?name=evtest) 查看 touchpad 使用时的宽度和 Z 值.

当你找到了合适的设定后,将它们加入 `/etc/X11/xorg.conf.d/70-synaptics.conf`中.

```
Option "PalmDetect" "1"
Option "PalmMinWidth" "8"
Option "PalmMinZ" "200"

```

**Warning:** For some touchpads, an [issue](https://bugzilla.kernel.org/show_bug.cgi?id=77161) with the kernel can cause the palm width to always be reported as 0\. This breaks palm detection in a majority of cases. Pending an actual fix, you can [patch](https://gist.github.com/silverhammermba/a231c8156ecaa63c86f1) the synaptics package to use only Z for palm detection.

**Tip:** If you experience problems with consistent palm detection for your hardware, an alternative to try is [libinput](/index.php/Libinput "Libinput").

#### 使用 syndaemon

`syndaemon` 可以监控键盘活动并在打字时禁用触摸板，有多个选项可以控制禁用条件。可以通过下面命令查看帮助：

```
$ syndaemon -h

```

例如要在打字 0.5 秒后禁用点击和滚动，忽略 Ctrl 等修饰键，使用

```
$ syndaemon -i 0.5 -t -K -R

```

确定好需要的选项后，在登录管理器或 [xinitrc](/index.php/Xinitrc "Xinitrc") 中配置为随 X 启动，使用 `-d` 选项程序会在后台运行。

### 检测到鼠标后禁用触摸板

在[udev](/index.php/Udev "Udev")的协助下，可以实现当外置鼠标插入后自动禁用触摸板的功能。可以使用下面规则：

#### 基本桌面

非桌面环境可以使用下面通用规则：

 `/etc/udev/rules.d/01-touchpad.rules` 
```
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="add", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/*username*/.Xauthority", RUN+="/usr/bin/synclient TouchpadOff=1"
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="remove", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/*username*/.Xauthority", RUN+="/usr/bin/synclient TouchpadOff=0"
```

#### GDM

GDM usually stores the Xauthority files inin a randomly-named directory. You should find your actual path to the Xauthority file which can be done using `ps ax`. For some reason multiple authority files may appear for a user, so a rule like will be necessary:

GDM 将 Xauthority 文件存放在 `/var/run/gdm` 下随机命名的文件夹中. `ps ax` 可以查到 Xauthority 文件的位置，udev规则一般是这样的:

```
ACTION=="add", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=1"
ACTION=="remove", KERNEL=="mouse[0-9]", SUBSYSTEM=="input", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0.0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=0"

```

Furthermore, you should validate that your udev script is running properly! You can check for the conditions using `udevadm monitor -p` which must be run as root.

##### With syndaemon running

`syndaemon` whether started by the [user](#Using_syndaemon) or the desktop environment can conflict with synclient and will need to be disabled. A rule like this will be needed:

 `/etc/udev/rules.d/01-touchpad.rules`  `SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ACTION=="add", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="$result/database", RUN+="/bin/sh -c '/usr/bin/synclient TouchpadOff=1 ; sleep 1; /bin/killall syndaemon; '"` 

##### touchpad-state

An AUR package [touchpad-state-git](https://aur.archlinux.org/packages/touchpad-state-git/) has been created around the udev rules above. It includes a udev rule and script:

```
touchpad-state [--off] [--on]

```

#### GNOME

GNOME users can install GNOME shell extension [Touchpad Indicator](https://extensions.gnome.org/extension/131/touchpad-indicator/), change "Switch Method" to "Synclient" and enable "Automatically switch Touchpad On/Off" in its preferences.

#### KDE

If using Plasma, the package [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) can be used to manage the touchpad.

#### System with multiple X sessions

For an environment where multiple users are present, a slightly different approach is needed to detect the current users X environment. This script will help achieving this:

 `/usr/bin/mouse-pnp-event-handler.sh` 
```
#!/bin/sh
## $1 = "add" / "remove"
## $2 = %k from udev 

## Set TRACKPAD_NAME according to your configuration. 
## Check your trackpad name with: 
## find /sys/class/input/ -name mouse* -exec udevadm info -a {} \; | grep 'ATTRS{name}'
TRACKPAD_NAME="SynPS/2 Synaptics TouchPad"

USERLIST=$(w -h | cut -d' ' -f1 | sort | uniq)
MOUSELIST=$(find /sys/class/input/ -name mouse*)

for CUR_USER in ${USERLIST}; do
         CUR_USER_XAUTH="$(sudo -Hiu ${CUR_USER} env | grep -e "^HOME=" | cut -d'=' -f2)/.Xauthority"

        ## Can't find a way to get another users DISPLAY variable from an isolated root environment. Have to set it manually.
        #CUR_USER_DISPL="$(sudo -Hiu ${CUR_USER} env | grep -e "^DISPLAY=" | cut -d'=' -f2)"
        CUR_USER_DISPL=":0"

        export XAUTHORITY="${CUR_USER_XAUTH}"
        export DISPLAY="${CUR_USER_DISPL}"

        if [ -f "${CUR_USER_XAUTH}" ]; then
                case "$1" in
                        "add")
                                /usr/bin/synclient TouchpadOff=1
                                /usr/bin/logger "USB mouse plugged. Disabling touchpad for $CUR_USER. ($XAUTHORITY - $DISPLAY)"
                        ;;
                        "remove")
                                ## Only execute synclient if there are no external USB mice connected to the system.
                                EXT_MOUSE_FOUND="0"
                                for CUR_MOUSE in ${MOUSELIST}; do
                                        if [ "$(cat ${CUR_MOUSE}/device/name)" != "${TRACKPAD_NAME}" ]; then
                                                EXT_MOUSE_FOUND="1"
                                        fi
                                done
                                if [ "${EXT_MOUSE_FOUND}" == "0" ]; then
                                        /usr/bin/synclient TouchpadOff=0
                                        /usr/bin/logger "No additional external mice found. Enabling touchpad for $CUR_USER."
                                else
                                        logger "Additional external mice found. Won't enable touchpad yet for $CUR_USER."
                                fi
                        ;;
                esac
        fi
done

```

Update the `TRACKPAD_NAME` variable for your system configuration. Run `find /sys/class/input/ -name mouse* -exec udevadm info -a {} \; | grep 'ATTRS{name}'` to get a list of useful mice-names. Choose the one for your trackpad.

Then have udev run this script when USB mices are plugged in or out, with these udev rules:

 `/etc/udev/rules.d/01-touchpad.rules` 
```
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="add", RUN+="/usr/bin/mouse-pnp-event-handler.sh add %k"
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="remove", RUN+="/usr/bin/mouse-pnp-event-handler.sh remove %k"
```

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

SoftButtonAreas选项的格式是(请参考[synaptics(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/synaptics.4)):

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

#### Bottom edge correction

In some cases, for example Toshiba Satellite P50, everything work out of the box except often your click are seen as mouse movement and the cursor will jump away just before registering the click. This can be easily solved running

```
$ synclient -l | grep BottomEdge

```

take the BottomEdge value and subtract a the wanted height of your button, then temporary apply with

```
$ synclient AreaBottomEdge=4000

```

when a good value has been found make it a fixed correction with

 `/etc/X11/xorg.conf.d/70-synaptics.conf` 
```
...
Option "AreaBottomEdge"         "4000"
...

```

**Note:** The area will not act as touchpad if the touch **begins** in that area, but it can still be used if the touch has originated outside.

## 疑难解答

### 在从挂起/休眠恢复后触摸板不工作

Occasionally touchpads will fail to work when the computer resumes from sleep or hibernation. This can often be corrected without rebooting by

*   Switching to a console and back again,
*   entering sleep mode again, and resuming again, or
*   locating the correct kernel module, then removing it and inserting it again.

**Note:** You can use Ctrl-Alt-F1 through F8 to switch to a console without using the mouse.

```
modprobe -r psmouse #psmouse happens to be the kernel module for my touchpad (Alps DualPoint)
modprobe psmouse

```

Now switch back to the tty that X is running on. If you chose the right module, your touchpad should be working again.

如果您使用的是笔记本电脑，在合上笔记本电脑盖子后再次打开之后遇到这个问题，可以修改您的电源管理策略，将合上盖子的行为改为“关闭屏幕”，而不是”挂起“或者”休眠“

### xorg.conf.d/70-synaptics.conf在 MATE 上失效

[MATE](/index.php/MATE "MATE") 会覆盖您的个性化设定,包括那些没法在 MATE 下进行图形化设定的选项.这会导致`/etc/X11/xorg.conf.d/70-synaptics.conf` 里的设置不起作用了.请参考本文MATE 一节来避免这种情况的发生.

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

#### Elan Touchpad

某些设备例如 ASUS x53s 使用 Elan touchpad，可能会出现此问题。.安装[AUR](/index.php/AUR "AUR")包[psmouse-alps-driver](https://aur.archlinux.org/packages/psmouse-alps-driver/)即可解决这个问题.

#### Laptops with touchscreen & touchpad

There also seems to be a problem with laptops which have both a touchscreen & a touchpad, such as the Dell XPS 12 or Dell XPS 13\. To fix this, you can [blacklist](/index.php/Blacklisting "Blacklisting") the `i2c_hid` driver, this does have the side-effect of disabling the touchscreen though.

This [seems to be a known problem](http://www.spinics.net/lists/linux-input/msg27768.html). Also see [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1419078).

Post kernel 3.15, having the module blacklisted may cause touchpad to stop working completely. Removing the blacklist should allow this to start working with limited functionality, see [FS#40921](https://bugs.archlinux.org/task/40921).

### Synaptics触摸板某些功能失效 (比如触击,滚动)

有些时候Synaptics触摸板会失去某些功能.即使正确配置了也不能使用诸如双指滚动,双指触发中键点击等功能.这个问题可能和上面提到的

如果阻止了重复加载模块后还有问题,可以尝试将"MatchIsTouchPad"配置项注释掉(这个选项synaptics默认开启)

If clicking with either 2 or 3 fingers is interpreted as a right-click, so you cannot get a middle click either way regardless of configuration, this bug is probably the culprit: [https://bugs.freedesktop.org/show_bug.cgi?id=55365](https://bugs.freedesktop.org/show_bug.cgi?id=55365)

#### 在一些笔记本的Elantech touchpads触摸板多点触控失效

在内核启动选项加上"i8042.reset i8042.nomux=1 i8042.nopnp i8042.noloop"等. 在我的联想小新笔记本上我增加了"i8042.reset i8042.nomux=1"两个选项，触摸板正常识别，多点触控可用。

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

#### Firefox 17.0 and later

Horizontal scrolling will now by default scroll through pages and not through your history. To reenable Mac-style forward/backward with two-finger swiping, edit:

```
mousewheel.default.action.override_x = 2

```

You may encounter accidental forwards/backwards while scrolling vertically. To change Firefox's sensitivity to horizontal swipes, edit:

```
mousewheel.default.delta_multiplier_x

```

The optimum value will depend on your touchpad and how you use it, try starting with `10`. A negative value will reverse the swipe directions.

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

### Touchpad not recognized after shutdown from Arch

Certain touchpads (elantech in particular) will fail to be recognized as a device of any sort after a standard shutdown from Arch linux. There are multiple possible solutions to this problem:

*   Boot into a Windows partition/install disk and shutdown from there.
*   Wait approximately 1 minute before turning on the computer after shutdown.
*   As discussed in [https://bugzilla.kernel.org/show_bug.cgi?id=81331#c186](https://bugzilla.kernel.org/show_bug.cgi?id=81331#c186) a patch has been merged into the stable kernel that provides a fix for Elantech touchpads. Gigabyte P34, P35v2 and X3 models are supported by default, for others (especially rebranded Gigabyte laptops, like XMG's) `i8042.kbdreset=1` can be set as kernel parameter.

### Trackpoint and Clickpad

Newer Thinkpads do not have physical buttons for their Trackpoint anymore and instead use the upper area of the Clickpad for buttons (Left, Middle, Right). Apart from the ergonomic viewpoint this works quite well with current Xorg. Unfortunately mouse wheel emulation using the middle button is not supported yet. Install [xf86-input-evdev-trackpoint](https://aur.archlinux.org/packages/xf86-input-evdev-trackpoint/) from the AUR for a patched and properly configured version if you intend to use the Trackpoint.

### ASUS Touchpads only recognised as PS/2 FocalTech emulated mouse

1.  Install the linux header for your kernel
2.  Install the focaltech-dkms from [https://github.com/hanipouspilot/focaltech-dkms](https://github.com/hanipouspilot/focaltech-dkms)
3.  Restart your computer
4.  Edit your settings in the "Mouse and Trackpad" settings.

## 参阅

*   [Synaptics 触摸板驱动](http://cgit.freedesktop.org/xorg/driver/xf86-input-synaptics/)