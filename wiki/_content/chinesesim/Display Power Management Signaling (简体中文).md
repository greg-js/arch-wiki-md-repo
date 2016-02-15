**[DPMS](https://en.wikipedia.org/wiki/VESA_Display_Power_Management_Signaling "wikipedia:VESA Display Power Management Signaling")** (VESA 显示电源管理信号，简称DPMS)是VESA制定的通过显示卡对显示器电源管理的标准。DPMS规定如果一定时间不对计算机进行操作时显示器自动进入节电模式。

## Contents

*   [1 在X中设定DPMS](#.E5.9C.A8X.E4.B8.AD.E8.AE.BE.E5.AE.9ADPMS)
*   [2 用xset修改DPMS和屏保设定](#.E7.94.A8xset.E4.BF.AE.E6.94.B9DPMS.E5.92.8C.E5.B1.8F.E4.BF.9D.E8.AE.BE.E5.AE.9A)
    *   [2.1 xset屏保控制](#xset.E5.B1.8F.E4.BF.9D.E6.8E.A7.E5.88.B6)
    *   [2.2 查看当前设置](#.E6.9F.A5.E7.9C.8B.E5.BD.93.E5.89.8D.E8.AE.BE.E7.BD.AE)
*   [3 例子](#.E4.BE.8B.E5.AD.90)
    *   [3.1 关闭DPMS](#.E5.85.B3.E9.97.ADDPMS)
    *   [3.2 禁止屏幕变为空白](#.E7.A6.81.E6.AD.A2.E5.B1.8F.E5.B9.95.E5.8F.98.E4.B8.BA.E7.A9.BA.E7.99.BD)
    *   [3.3 关闭DPMS并防止屏幕变为空白](#.E5.85.B3.E9.97.ADDPMS.E5.B9.B6.E9.98.B2.E6.AD.A2.E5.B1.8F.E5.B9.95.E5.8F.98.E4.B8.BA.E7.A9.BA.E7.99.BD)
    *   [3.4 立刻关闭屏幕](#.E7.AB.8B.E5.88.BB.E5.85.B3.E9.97.AD.E5.B1.8F.E5.B9.95)
    *   [3.5 Put screen into standby](#Put_screen_into_standby)
    *   [3.6 Put screen into suspend](#Put_screen_into_suspend)
    *   [3.7 Change Blank time from 5 min to 1 hour](#Change_Blank_time_from_5_min_to_1_hour)
    *   [3.8 xset display.sh](#xset_display.sh)
*   [4 DPMS interaction in a Linux console with setterm](#DPMS_interaction_in_a_Linux_console_with_setterm)
    *   [4.1 防止屏幕关闭](#.E9.98.B2.E6.AD.A2.E5.B1.8F.E5.B9.95.E5.85.B3.E9.97.AD)
    *   [4.2 Pipe the output to a cat to see the escapes](#Pipe_the_output_to_a_cat_to_see_the_escapes)
    *   [4.3 Pipe the escapes to any tty (with write/append perms) to modify that terminal](#Pipe_the_escapes_to_any_tty_.28with_write.2Fappend_perms.29_to_modify_that_terminal)
        *   [4.3.1 Bash loop to set ttys 0-256](#Bash_loop_to_set_ttys_0-256)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 xset的DPMS设置在xscreensaver不起作用](#xset.E7.9A.84DPMS.E8.AE.BE.E7.BD.AE.E5.9C.A8xscreensaver.E4.B8.8D.E8.B5.B7.E4.BD.9C.E7.94.A8)
        *   [5.1.1 xscreensaver DPMS](#xscreensaver_DPMS)
*   [6 See also](#See_also)

## 在X中设定DPMS

**Note:** As of Xorg 1.8 DPMS is auto detected and enabled if ACPI is also enabled at kernel runtime.

在 `/etc/X11/xorg.conf` 的 `Monitor` 小节写上:

```
Option "DPMS" "true"

```

把下面的配置加入 `ServerLayout` 小节, 必要时改变时间(以分钟计):

```
Option "StandbyTime" "10"
Option "SuspendTime" "20"
Option "OffTime" "30"

```

**Note:** If the _"OffTime"_ option does not work replace it with the following, (change the _"blanktime"_ to _"0"_ to disable screen blanking)

```
Option         "BlankTime" "30"

```

比较新的X推荐使用 `.conf` 文件代替 `xorg.conf`, `/etc/X11/xorg.conf.d/10-monitor.conf` 的一个例子如下：

```
Section "Monitor"
    Identifier "LVDS0"
    Option "DPMS" "false"
EndSection

Section "ServerLayout"
    Identifier "ServerLayout0"
    Option "BlankTime"  "0"
    Option "StandbyTime" "0"
    Option "SuspendTime" "0"
    Option "OffTime" "0"
EndSection

```

## 用xset修改DPMS和屏保设定

可以用[官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库")中[xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset)提供的`xset`工具关闭屏幕。注意：如果要在shell中关闭显示器，需要在命令前面加上 `sleep 1;` . 例如：

```
sleep 1; xset dpms force off

```

To control Energy Star (DPMS) features (a timeout value of zero disables the mode):

```
xset -dpms Energy Star features off
xset +dpms Energy Star features on
xset dpms [standby [suspend [off]]]     
xset dpms force standby 
xset dpms force suspend 
xset dpms force off 
xset dpms force on  (also implicitly enables DPMS features)

```

### xset屏保控制

你可以用xset控制你的屏保:

```
xset s [timeout [cycle]]  
xset s default    
xset s on
xset s blank              
xset s noblank    
xset s off
xset s expose             
xset s noexpose
xset s activate           
xset s reset

```

### 查看当前设置

```
$ xset q

...

Screen Saver:
  prefer blanking:  yes    allow exposures:  yes
  timeout:  600    cycle:  600
DPMS (Energy Star):
  Standby: 600    Suspend: 600    Off: 600
  DPMS is Enabled
  Monitor is On

```

## 例子

### 关闭DPMS

```
xset -dpms

```

### 禁止屏幕变为空白

```
xset s off

```

### 关闭DPMS并防止屏幕变为空白

在看电影或幻灯片时有用:

```
xset -dpms; xset s off

```

### 立刻关闭屏幕

如果你要离开，无须等待超时之后屏幕自动关闭。可以运行如下`xset`命令来立即关闭屏幕

```
xset dpms force off

```

### Put screen into standby

```
xset dpms force standby

```

### Put screen into suspend

```
xset dpms force suspend

```

### Change Blank time from 5 min to 1 hour

```
xset s 3600 3600

```

### xset display.sh

You could also copy this script:

 `/usr/local/bin/display.sh` 

```
#!/bin/bash
# Small script to set display into standby, suspend or off mode
# 20060301-Joffer

case $1 in
  standby|suspend|off)
    xset dpms force $1
  ;;
  *)
    echo "Usage: $0 standby|suspend|off"
  ;;
esac

```

Make it executable (`chmod u+x /usr/local/bin/display.sh`) and just run `display.sh off`. For the latter to work you need to include `/usr/local/bin` into your path.

## DPMS interaction in a Linux console with setterm

The _setterm_ utility issues terminal recognized escape codes to alter the terminal. Essentially it just writes/echos the terminal sequences to the current terminal device, whether that be in screen, a remote ssh terminal, console mode, serial consoles, etc.

setterm Syntax: (0 disables)

```
setterm -blank [0-60|force|poke]
setterm -powersave [on|vsync|hsync|powerdown|off]
setterm -powerdown [0-60]

```

**Note:** If you haven't already read the brief DPMS article linked to below, please skim it to understand how DPMS can be used in the console the same as in X.

### 防止屏幕关闭

可以运行以下命令, 并使其自启动(如添加到 /etc/rc.local):

```
$ setterm -blank 0 -powerdown 0

```

也可以通过下列命令禁止终端清空:

```
# echo -ne "\033[9;0]" >> /etc/issue

```

### Pipe the output to a cat to see the escapes

```
$ setterm -powerdown 2>&1 | exec cat -v 2>&1 | sed "s/\\^\\[/\\\\033/g"

```

### Pipe the escapes to any tty (with write/append perms) to modify that terminal

Note the use of **>>** instead of **>**. For permission issues using sudo in a script or something, you can use the **tee** program to append the output of setterm to the tty device, which tty's let appending sometimes but not writing.

```
$ setterm -powerdown 0 >> /dev/tty3

```

#### Bash loop to set ttys 0-256

```
$ for i in {0..256}; do setterm -powerdown 0 >> /dev/tty$i; done; unset i;

```

## Troubleshooting

### xset的DPMS设置在xscreensaver不起作用

[xscreensaver](/index.php/Xscreensaver "Xscreensaver")用它自己的DPMS设置。 请看xscreensaver的设置以获取更多信息。

#### xscreensaver DPMS

你可以通过编辑`~/.xscreensaver`以设置xscreensaver的DPMS设置，或者使用xscreensaver-demo.

```
timeout:	1:00:00
cycle:		0:05:00
lock:		False
lockTimeout:	0:00:00
passwdTimeout:	0:00:30
fade:		True
unfade:		False
fadeSeconds:	0:00:03
fadeTicks:	20
dpmsEnabled:	True
dpmsStandby:	2:00:00
dpmsSuspend:	2:00:00
dpmsOff:	4:00:00

```

## See also

*   [PC Monitor DPMS specification explanation](http://webpages.charter.net/dperr/dpms.htm)