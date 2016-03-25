**翻译状态：** 本文是英文页面 [Display_Power_Management_Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-25，点击[这里](https://wiki.archlinux.org/index.php?title=Display_Power_Management_Signaling&diff=0&oldid=419340)可以查看翻译后英文页面的改动。

**[DPMS](https://en.wikipedia.org/wiki/VESA_Display_Power_Management_Signaling "wikipedia:VESA Display Power Management Signaling")** (显示电源管理信号，简称DPMS) 可以在计算机一定时间无操作时，将显示器置于节电模式。具体的时间设置可以参考 [[1]](http://linux.die.net/man/3/dpmssettimeouts). 注意有些显示器在不同 DPMS 状态下表现不变。

## Contents

*   [1 在 X 中设定 DPMS](#.E5.9C.A8_X_.E4.B8.AD.E8.AE.BE.E5.AE.9A_DPMS)
*   [2 用xset修改DPMS和屏保设定](#.E7.94.A8xset.E4.BF.AE.E6.94.B9DPMS.E5.92.8C.E5.B1.8F.E4.BF.9D.E8.AE.BE.E5.AE.9A)
*   [3 Linux 终端和 DPMS 的交互](#Linux_.E7.BB.88.E7.AB.AF.E5.92.8C_DPMS_.E7.9A.84.E4.BA.A4.E4.BA.92)
    *   [3.1 防止屏幕关闭](#.E9.98.B2.E6.AD.A2.E5.B1.8F.E5.B9.95.E5.85.B3.E9.97.AD)
    *   [3.2 通过 cat 显示输出中的转义](#.E9.80.9A.E8.BF.87_cat_.E6.98.BE.E7.A4.BA.E8.BE.93.E5.87.BA.E4.B8.AD.E7.9A.84.E8.BD.AC.E4.B9.89)
    *   [3.3 将转义输出到任意 tty (with write/append perms) 进行终端修改](#.E5.B0.86.E8.BD.AC.E4.B9.89.E8.BE.93.E5.87.BA.E5.88.B0.E4.BB.BB.E6.84.8F_tty_.28with_write.2Fappend_perms.29_.E8.BF.9B.E8.A1.8C.E7.BB.88.E7.AB.AF.E4.BF.AE.E6.94.B9)
        *   [3.3.1 用循环设置 ttys 0-256](#.E7.94.A8.E5.BE.AA.E7.8E.AF.E8.AE.BE.E7.BD.AE_ttys_0-256)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 在 X 中设定 DPMS

**Note:** 从 Xorg 1.8 开始，只要内核启用了 ACPI， DPMS 就会自动启用。

在 `/etc/X11/xorg.conf` 的 `Monitor` 段落中加上上:

```
Option "DPMS" "true"

```

把下面的配置加入 `ServerLayout` 小节, 必要时改变时间(以分钟计):

```
Option "StandbyTime" "10"
Option "SuspendTime" "20"
Option "OffTime" "30"

```

**Note:** If the *"OffTime"* option does not work replace it with the following, (change the *"blanktime"* to *"0"* to disable screen blanking)
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

可以用[官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库")中[xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset)提供的`xset`工具关闭屏幕。如果要在shell中关闭显示器，需要在命令前面加上 `sleep 1;` . 例如：

```
sleep 1; xset dpms force off

```

命令示例：

| 命令 | 描述 |
| xset s off | 禁用屏保清空 |
| xset s 3600 3600 | 将清空时间设置到 1 小时 |
| xset -dpms | 关闭 DPMS |
| xset s off -dpms | 禁用 DPMS 并阻止屏幕清空 |
| xset dpms force off | 立即关闭屏幕 |
| xset dpms force standby | 待机界面 |
| xset dpms force suspend | 休眠界面 |

查看当前设置:

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

运行 `xset` 可以查看全部可用命令.

**Note:** 如果在 [xinitrc](/index.php/Xinitrc "Xinitrc") 中使用 `xset` 无法工作，在配置文件中进行设置。

**Warning:** [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") 和 [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) 会使用自己的 DPMS 设置，详情参考 [XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver") 和 [Xfce#Display blanking](/index.php/Xfce#Display_blanking "Xfce").

## Linux 终端和 DPMS 的交互

*setterm* 工具可以通过终端能够识别的转义字符修改终端。可以写入/echo 终端序列到当前终端设备，包括再显示设备，远程 SSH 终端， 控制台，串口控制台。

setterm Syntax: (0 disables)

```
setterm -blank [0-60|force|poke]
setterm -powersave [on|vsync|hsync|powerdown|off]
setterm -powerdown [0-60]

```

### 防止屏幕关闭

可以运行以下命令：

```
$ setterm -blank 0 -powerdown 0

```

也可以通过下列命令禁止终端清空:

```
# echo -ne "\033[9;0]" >> /etc/issue

```

### 通过 cat 显示输出中的转义

```
$ setterm -powerdown 2>&1 | exec cat -v 2>&1 | sed "s/\\^\\[/\\\\033/g"

```

### 将转义输出到任意 tty (with write/append perms) 进行终端修改

```
$ setterm -powerdown 0 >> /dev/tty3

```

**Note:** 使用 `>>` 而不是 `>`. 如果脚本有 *sudo* 权限问题，tty 可能允许附加但是不允许写入， 可以使用 **tee** 阻止 setterm 输出到 tty 。

#### 用循环设置 ttys 0-256

```
$ for i in {0..256}; do setterm -powerdown 0 >> /dev/tty$i; done; unset i;

```

## 参阅

*   [PC Monitor DPMS specification explanation](http://webpages.charter.net/dperr/dpms.htm)
*   [DPMS control in X](http://ptspts.blogspot.be/2009/10/screen-blanking-dpms-screen-saver.html)