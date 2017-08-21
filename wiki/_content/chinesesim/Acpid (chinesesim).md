**翻译状态：** 本文是英文页面 [Acpid](/index.php/Acpid "Acpid") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-18，点击[这里](https://wiki.archlinux.org/index.php?title=Acpid&diff=0&oldid=463489)可以查看翻译后英文页面的改动。

[acpid2](http://acpid2.sourceforge.net/)是用于处理电源相关事件的守护进程，它非常灵活且易于扩展。当某个事件发生时，执行相关程序来处理该事件。这些事件是由某些动作触发的，比如：

*   按下电源按钮
*   按下睡眠/挂起按钮
*   合上笔记本盖子
*   拔下/插上笔记本外接电源

**警告:** 请注意[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")比如[GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")，[systemd](/index.php/Power_management#ACPI_events "Power management") 和 [额外按键处理进程](/index.php/Extra_keyboard_keys "Extra keyboard keys")会有它自己的一套管理方法。同时运行多套系统可能产生意想不到的结果，比如，当按下电源键时电脑同时执行挂起和关机；或者当按下睡眠按钮时电脑执行了两次挂起操作。所以，使用多套系统时你应只激活一套系统的电源事件管理方法，以免引起冲突。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 其它配置方案](#.E5.85.B6.E5.AE.83.E9.85.8D.E7.BD.AE.E6.96.B9.E6.A1.88)
*   [3 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [3.1 脚本示例](#.E8.84.9A.E6.9C.AC.E7.A4.BA.E4.BE.8B)
    *   [3.2 音量调整](#.E9.9F.B3.E9.87.8F.E8.B0.83.E6.95.B4)
    *   [3.3 获取当前登陆的用户名](#.E8.8E.B7.E5.8F.96.E5.BD.93.E5.89.8D.E7.99.BB.E9.99.86.E7.9A.84.E7.94.A8.E6.88.B7.E5.90.8D)
        *   [3.3.1 连接到 acpid 套接字](#.E8.BF.9E.E6.8E.A5.E5.88.B0_acpid_.E5.A5.97.E6.8E.A5.E5.AD.97)
*   [4 参考](#.E5.8F.82.E8.80.83)

## 安装

使用[Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装 [acpid](https://www.archlinux.org/packages/?name=acpid)。 然后 [start](/index.php/Start "Start") 并 [enable](/index.php/Enable "Enable") `acpid.service`.

## 配置

[acpid](https://www.archlinux.org/packages/?name=acpid)预置了许多事件触发行为，比如它定义了当你按下电源按钮时应当发生什么。这些触发行为默认在`/etc/acpi/handler.sh`中定义。在`/etc/acpi/events/anything`)规定：任何侦测到的电源事件都会按照`/etc/acpi/handler.sh`中定义的触发行为执行相关动作。

下面是一个定义触发行为的简单例子。在这个例子中，当按下睡眠按钮时acpid运行命令`echo -n mem >/sys/power/state`，这将会使你的电脑挂起：

```
button/sleep)
    case "$2" in
        SLPB) echo -n mem >/sys/power/state ;;
	 *)    logger "ACPI action undefined: $2" ;;
    esac
    ;;

```

不幸的是计算机上的这些电源事件标识并不统一，比如，在一些计算机上睡眠按钮可能被标识为*SLPB*，而在另一些计算机上为*SBTN*。

要想确定各种按钮或`Fn`快捷键在你的计算机上是如何定义的：

```
# journalctl -f

```

现在在你计算机上按下电源按钮或睡眠按钮（比如`Fn+Esc`），你会得到类似以下的结果：

```
logger: ACPI action undefined: PBTN
logger: ACPI action undefined: SBTN

```

如果这不起作用的话，运行：

```
# acpi_listen

```

或者[openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat)：

```
$ netcat -U /var/run/acpid.socket

```

然后按下电源按钮，你会看到类似以下输出：

```
button/power PBTN 00000000 00000b31

```

`acpi_listen`的输出会被作为$1, $2 , $3 & $4参数发送给`/etc/acpi/handler.sh`。 举例：

```
$1 button/power
$2 PBTN
$3 00000000
$4 00000b31

```

像你看到的那样，在这个例子中睡眠按钮被识别为*SBTN*，而不是*SLPB*（这是`/etc/acpi/handler.sh`中默认定义的标识符）。所以，要想让你的睡眠按钮正常工作的话，你需要编辑`/etc/acpi/handler.sh`把*SLPB)*替换为*SBTN)*。

参照上面的例子，你应该可以很容易的通过定制`/etc/acpi/handler.sh`来根据侦测到的电源时间来执行不同的命令。更多例子可参考下面的[小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)部分。

### 其它配置方案

默认所有的电源事件都是交由`/etc/acpi/handler.sh`处理的。这是由`/etc/acpi/events/anything`规定的：

```
# Pass all events to our one handler script
event=.*
action=/etc/acpi/handler.sh %e

```

尽管这样配置工作起来没有任何问题，但一些用户可能更喜欢使用各自独立的脚本来定义不同的电源事件。下面举例说明了如何使用不同的事件定义文件和行为定义文件：

作为root，创建以下文件：

 `/etc/acpi/events/sleep-button` 
```
event=button sleep.*
action=/etc/acpi/actions/sleep-button.sh %e
```

然后建立以下文件：

 `/etc/acpi/actions/sleep-button.sh` 
```
#!/bin/sh
case "$3" in
    SLPB) echo -n mem >/sys/power/state ;;
    *)    logger "ACPI action undefined: $3" ;;
esac
```

最后，给脚本加上可执行权限：

```
# chmod +x /etc/acpi/actions/sleep-button.sh

```

用这种方法，你可以任意的独立的事件/行为脚本。

## 小技巧

**Note:** 一些在这里描述的动作，例如无线网络切换和背光控制，可能已经由驱动直接管理。在这种情况下，您应该查询相应的内核模块。

### 脚本示例

下面给出的例子可以用在你的`/etc/acpi/handler.sh`脚本中，只是在使用的时候记得将事件变量更改为`acpi_listen`侦测到的那个。

实现插拔外接电源时自动设置屏幕亮度（数值可能需要调整，参考`/sys/class/backlight/acpi_video0/max_brightness`）：

```
ac_adapter)
    case "$2" in
        AC*|AD*)
            case "$4" in
                00000000)
                    echo -n 50 > /sys/class/backlight/acpi_video0/brightness
                    ;;
                00000001)
                    echo -n 100 > /sys/class/backlight/acpi_video0/brightness
                    ;;
            esac

```

### 音量调整

下面的一系列脚本是用来控制音量的。用上面讲到的方法找到音量键的标识符，然后替换掉下面文件中的事件标识就可以用在自己电脑上了：

 `/etc/acpi/events/vol-d` 
```
event=button/volumedown
action=amixer set Master 5-
```
 `/etc/acpi/events/vol-m` 
```
event=button/mute
action=amixer set Master toggle
```
 `/etc/acpi/events/vol-u` 
```
event=button/volumeup
action=amixer set Master 5+
```

**Note:** 这些命令在 PulseAudio 下可能有问题[[1]](https://lists.freedesktop.org/archives/pulseaudio-discuss/2015-December/025062.html)。要实现全部功能，以当前用户执行并将设置 `XDG_RUNTIME_DIR` 环境变量 [environment variable](/index.php/Environment_variable "Environment variable"),例如 `sudo -u *user* XDG_RUNTIME_DIR=/run/user/*1000* pactl`.

**Tip:** 在 Xorg 中禁用或绑定这些音量按键，以避免和其他程序冲突。详情请参考或 [Xmodmap](/index.php/Xmodmap "Xmodmap").

参阅 [[2]](http://web.archive.org/web/20150711044207/http://blog.lastlog.de/posts/fixing_volume_change_in_linux).

### 获取当前登陆的用户名

你可以使用`getuser`函数来获取当前登陆的用户名：

```
getuser ()
    {
     export DISPLAY=`echo $DISPLAY | cut -c -2`
     user=`who | grep " $DISPLAY" | awk '{print $1}' | tail -n1`
     export XAUTHORITY=/home/$user/.Xauthority
     eval $1=$user
    }

```

然后这个函数就可以被用在下面的例子中，它可以在你按下电源按钮时正常的关闭[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")：

```
button/power)
    case "$2" in
        PBTN)
            getuser "$user"
            echo $user > /dev/tty5
            su $user -c "dcop ksmserver ksmserver logout 0 2 0"
            ;;
          *) logger "ACPI action undefined $2" ;;
    esac
    ;;

```

#### 连接到 acpid 套接字

除了规则文件之外，acpid 也接受 UNIX 域套接字连接，默认是 `/var/run/acpid.socket`. 用户程序可以连接到此套接字。

```
#!/bin/bash
coproc acpi_listen
trap 'kill $COPROC_PID' EXIT

while read -u "${COPROC[0]}" -a event; do
    *handler.sh* "${event[@]}"
done

```

*handler.sh* 可以参考 `/etc/acpi/handler.sh`.

## 参考

*   [http://acpid.sourceforge.net/](http://acpid.sourceforge.net/) - acpid 主页
*   [Gentoo wiki](http://www.gentoo-wiki.info/ACPI/Configuration)
*   [ACPI 热键](/index.php/ACPI_hotkeys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ACPI hotkeys (简体中文)")