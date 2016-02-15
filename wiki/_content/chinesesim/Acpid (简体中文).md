**翻译状态：** 本文是英文页面 [Acpid](/index.php/Acpid "Acpid") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-10-13，点击[这里](https://wiki.archlinux.org/index.php?title=Acpid&diff=0&oldid=277906)可以查看翻译后英文页面的改动。

[acpid](http://acpid.sourceforge.net/)是用于处理电源相关事件的守护进程，它非常灵活且易于扩展。它侦听`/proc/acpi/event`，当某个事件发生时，执行相关程序来处理该事件。这些事件是由某些动作触发的，比如：

*   按下电源按钮
*   按下睡眠/挂起按钮
*   合上笔记本盖子
*   拔下/插上笔记本外接电源

**警告:** 请注意[桌面环境](/index.php/Desktop_Environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop Environment (简体中文)")比如[GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")倾向于使用自己的电源事件管理方法（独立于acpid）,[systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")的登陆管理器也有它自己的一套管理方法。同时运行多套系统可能产生意想不到的结果，比如，当按下电源键时电脑同时执行挂起和关机；或者当按下睡眠按钮时电脑执行了两次挂起操作。所以，使用多套系统时你应只激活一套系统的电源事件管理方法，以免引起冲突。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 其它配置方案](#.E5.85.B6.E5.AE.83.E9.85.8D.E7.BD.AE.E6.96.B9.E6.A1.88)
*   [3 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [3.1 脚本示例](#.E8.84.9A.E6.9C.AC.E7.A4.BA.E4.BE.8B)
    *   [3.2 音量调整](#.E9.9F.B3.E9.87.8F.E8.B0.83.E6.95.B4)
    *   [3.3 关闭笔记本显示器](#.E5.85.B3.E9.97.AD.E7.AC.94.E8.AE.B0.E6.9C.AC.E6.98.BE.E7.A4.BA.E5.99.A8)
    *   [3.4 获取当前登陆的用户名](#.E8.8E.B7.E5.8F.96.E5.BD.93.E5.89.8D.E7.99.BB.E9.99.86.E7.9A.84.E7.94.A8.E6.88.B7.E5.90.8D)
    *   [3.5 ACPI 快捷键](#ACPI_.E5.BF.AB.E6.8D.B7.E9.94.AE)
*   [4 参考](#.E5.8F.82.E8.80.83)

## 安装

[acpid](https://www.archlinux.org/packages/?name=acpid)在[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中，你可以使用[Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")来安装它。

To have _acpid_ started on boot, [enable](/index.php/Systemd#Using_units "Systemd") `acpid.service`.

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

不幸的是计算机上的这些电源事件标识并不统一，比如，在一些计算机上睡眠按钮可能被标识为_SLPB_，而在另一些计算机上为_SBTN_。

要想确定各种按钮或`Fn`快捷键在你的计算机上是如何定义的，以root身份在终端运行：

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
power/button PBTN 00000000 00000b31

```

`acpi_listen`的输出会被作为$1, $2 , $3 & $4参数发送给`/etc/acpi/handler.sh`。 举例：

```
$1 power/button
$2 PBTN
$3 00000000
$4 00000b31

```

像你看到的那样，在这个例子中睡眠按钮被识别为_SBTN_，而不是_SLPB_（这是`/etc/acpi/handler.sh`中默认定义的标识符）。所以，要想让你的睡眠按钮正常工作的话，你需要编辑`/etc/acpi/handler.sh`把_SLPB)_替换为_SBTN)_。

参照上面的例子，你应该可以很容易的通过定制`/etc/acpi/handler.sh`来根据侦测到的电源时间来执行不同的命令。更多例子可参考下面的 [小技巧](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.B0.8F.E6.8A.80.E5.B7.A7 "Acpid (简体中文)")部分。

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

**Tip:** 一些在这里描述的动作，例如无线网络切换和背光控制，可能已经由驱动直接管理。在这种情况下，您应该查询相应的内核模块。

### 脚本示例

下面给出的例子可以用在你的`/etc/acpi/handler.sh`脚本中，只是在使用的时候记得将事件变量更改为`acpi_listen`侦测到的那个。

实现合上笔记本盖子时使用`xscreensaver`锁屏：

```
button/lid)
    case $3 in
        close)
            # The lock command need to be run as the user who owns the xscreensaver process and not as root.
            # See: man xscreensaver-command. $xs will have the value of the user owning the process, if any.

            xs=$(ps -C xscreensaver -o user=)
            if test $xs; then su $xs -c "xscreensaver-command -lock"; fi
            ;;

```

实现合上笔记本盖子时挂起系统并用`slimlock`锁屏：

```
button/lid)
    case $3 in
        close)
            #echo "LID switched!">/dev/tty5
	     /usr/sbin/pm-suspend &
	     DISPLAY=:0.0 su -c - username /usr/bin/slimlock
            ;;

```

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

下面的一系列脚本是用来控制音量的（假设你用的是[ALSA](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Advanced Linux Sound Architecture (简体中文)")）。用上面讲到的方法找到音量键的标识符，然后替换掉下面文件中的事件标识就可以用在自己电脑上了：

 `/etc/acpi/actions/volume_up.sh` 

```
  #!/bin/bash
  /usr/bin/amixer set Master 5%+

```

 `/etc/acpi/actions/volume_down.sh` 

```
  #!/bin/bash
  /usr/bin/amixer set Master 5%-

```

定义事件的文件：

 `/etc/acpi/events/volume_up` 

```
  event=button[ /]volumeup
  action=/etc/acpi/actions/volume_up.sh

```

 `/etc/acpi/events/volume_down` 

```
  event=button[ /]volumedown
  action=/etc/acpi/actions/volume_down.sh

```

用于切换静音的配置文件：

 `/etc/acpi/events/volume_mute` 

```
  event=button[ /]volumemute
  action=/usr/bin/amixer set Master toggle

```

### 关闭笔记本显示器

下面这个小技巧修改自[Gentoo Wiki](http://en.gentoo-wiki.com/wiki/ACPI/Configuration)。把下面的内容添加到`/etc/acpi/actions/lm_lid.sh`最后，或者添加到`/etc/acpi/handler.sh`的_button/lid_部分。这个配置会实现当合上笔记本盖子时自动切断LCD背光，揭开盖子时自动打开LCD背光。

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force off ;;
    open)   XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force on  ;;
esac

```

如果你想提高、降低亮度或做其他一些跟X有关的事情，你应当明确指定你的X显示接口以及那个神奇的MIT cookie文件（一个用于对X服务器和其它输入设备进行读写访问的安全凭证）。

下面的脚本没有用到XAUTHORITY，使用了sudo：

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) sudo -u `ps -o ruser= -C xinit` xset -display :0 dpms force off ;;
    open)   sudo -u `ps -o ruser= -C xinit` xset -display :0 dpms force on  ;;
esac

```

在一些难缠的硬件上当使用某些版本的[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")时，`xset dpms force off`只会使屏幕变黑并不会关闭屏幕背光。这个bug可以用 [vbetool](https://www.archlinux.org/packages/?name=vbetool)（来自[official repositories](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")）来修复。做以下更改：

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) vbetool dpms off ;;
    open)   vbetool dpms on  ;;
esac

```

如果显示器只是快速的关闭然后又打开，很可能是xscreensaver自带的电源管理跟_dpms_的设置冲突了。

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

### ACPI 快捷键

您可以直接编辑`/etc/acpi/handler.sh`, 将快捷键反应到ACPI事件, 或者您也可以将这些快捷键指向别的自己定义的一些脚本 (例如: /etc/acpi/hotkeys.sh)

在这行之下

```
case "$1" in

```

添加如下行的内容:

```
hkey)
	case "$4" in
		00000b31)
		echo "PreviousButton pressed!"
		exailectl p
		;;
	00000b32)
		echo "NextButton pressed!"
		exailectl n
		;;
	00000b33)
		echo "Play/PauseButton pressed!"
		exailectl pp
		echo "executed.."
		;;
	00000b30)
		echo "StopButton pressed!"
		exailectl s
		;;
	*)
		echo "Hotkey Else: $4"
		;;
	esac
	;;

```

这个 '00000b31' 之类的值就是通过acpi_listen监听到的快捷键的值. 在acpi_listen监听到的值中'hkey VALZ 00000000 00000b31', $4也就是最后部分, 就是区别于其他键的部分.

并且,我为了控制Exaile音乐播放器写了一个简单的 exailectl 脚本. 因为ACPID是在root级别的守护进程, 所以您需要用下面方式来写控制脚本

```
sudo -u (用户名) exaile

```

不然的话,快捷键的动作不会检测到您的用户正在运行的程序,它就会去重新启动另一个程序而不是对当前的程序作出反应.

## 参考

*   [http://acpid.sourceforge.net/](http://acpid.sourceforge.net/) - acpid homepage
*   [http://www.gentoo-wiki.info/ACPI/Configuration](http://www.gentoo-wiki.info/ACPI/Configuration) - RIP Gentoo wiki entry - New Gentoo Wiki Archives
*   [ACPI hotkeys](/index.php/ACPI_hotkeys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ACPI hotkeys (简体中文)")