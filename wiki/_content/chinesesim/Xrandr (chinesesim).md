Related articles

*   [Xorg (简体中文)](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")
*   [Multihead](/index.php/Multihead "Multihead")

**翻译状态：** 本文是英文页面 [Xrandr](/index.php/Xrandr "Xrandr") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-6-16，点击[这里](https://wiki.archlinux.org/index.php?title=Xrandr&diff=0&oldid=477117)可以查看翻译后英文页面的改动。

"xrandr" 是一款官方的 [RandR](https://en.wikipedia.org/wiki/RandR "wikipedia:RandR") [Wikipedia:X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") 扩展配置工具。它可以设置屏幕显示的大小、方向、镜像等。对多显示器的情况，请参考 [Multihead](/index.php/Multihead "Multihead") 页面。 当前使用的显示器用 ***** 标记，优先使用的显示器用 **+** 标记。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 设置分辨率](#.E8.AE.BE.E7.BD.AE.E5.88.86.E8.BE.A8.E7.8E.87)
*   [3 添加未被检测到的有效分辨率](#.E6.B7.BB.E5.8A.A0.E6.9C.AA.E8.A2.AB.E6.A3.80.E6.B5.8B.E5.88.B0.E7.9A.84.E6.9C.89.E6.95.88.E5.88.86.E8.BE.A8.E7.8E.87)
*   [4 使xrandr所更改的分辨率设置永久生效](#.E4.BD.BFxrandr.E6.89.80.E6.9B.B4.E6.94.B9.E7.9A.84.E5.88.86.E8.BE.A8.E7.8E.87.E8.AE.BE.E7.BD.AE.E6.B0.B8.E4.B9.85.E7.94.9F.E6.95.88)
    *   [4.1 在xorg.conf设置分辨率（推荐）](#.E5.9C.A8xorg.conf.E8.AE.BE.E7.BD.AE.E5.88.86.E8.BE.A8.E7.8E.87.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)
    *   [4.2 在xprofile设定xrandr命令](#.E5.9C.A8xprofile.E8.AE.BE.E5.AE.9Axrandr.E5.91.BD.E4.BB.A4)
    *   [4.3 在KDM/GDM的启动脚本设定xrandr命令](#.E5.9C.A8KDM.2FGDM.E7.9A.84.E5.90.AF.E5.8A.A8.E8.84.9A.E6.9C.AC.E8.AE.BE.E5.AE.9Axrandr.E5.91.BD.E4.BB.A4)
*   [5 图形前端](#.E5.9B.BE.E5.BD.A2.E5.89.8D.E7.AB.AF)
    *   [5.1 ARandR](#ARandR)
    *   [5.2 LXrandR](#LXrandR)
*   [6 脚本](#.E8.84.9A.E6.9C.AC)
*   [7 在VNC上使用xrandr](#.E5.9C.A8VNC.E4.B8.8A.E4.BD.BF.E7.94.A8xrandr)
*   [8 疑难排除](#.E7.96.91.E9.9A.BE.E6.8E.92.E9.99.A4)
    *   [8.1 添加未检测到的分辨率](#.E6.B7.BB.E5.8A.A0.E6.9C.AA.E6.A3.80.E6.B5.8B.E5.88.B0.E7.9A.84.E5.88.86.E8.BE.A8.E7.8E.87)
        *   [8.1.1 EDID 校验和无效](#EDID_.E6.A0.A1.E9.AA.8C.E5.92.8C.E6.97.A0.E6.95.88)
    *   [8.2 纠正电视机分辨率过扫](#.E7.BA.A0.E6.AD.A3.E7.94.B5.E8.A7.86.E6.9C.BA.E5.88.86.E8.BE.A8.E7.8E.87.E8.BF.87.E6.89.AB)
    *   [8.3 Full RGB in HDMI](#Full_RGB_in_HDMI)
        *   [8.3.1 Screen resolution reverts back after a blink](#Screen_resolution_reverts_back_after_a_blink)
*   [9 参见](#.E5.8F.82.E8.A7.81)

## 安装

请从 [官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")[安装](/index.php/Pacman "Pacman") [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) 软件包。除此之外，也可使用 [arandr](https://www.archlinux.org/packages/?name=arandr) 或 [lxrandr](https://www.archlinux.org/packages/?name=lxrandr) 等图形前端作为替代。

## 设置分辨率

`xrandr`命令可以直接向您分别显示系统当前有效输出设备的名称(LVDS或VGA-0等等)和所有有效分辨率。

```
Screen 0: minimum 320 x 200, current 1400 x 1050, maximum 1400 x 1400
VGA disconnected (normal left inverted right x axis y axis)
LVDS connected 1400x1050+0+0 (normal left inverted right x axis y axis) 286mm x 214mm
   1400x1050      60.0*+   50.0  
[...]

```

您可以通过xrandr为某显示器指定一种分辨率，示例，且其中--output参数指定显示器，--mode参数指定一种有效分辨率：

```
 xrandr --output LVDS --mode 1024x768

```

也可以与此同时地，或独立地使用--rate参数来修改刷新率，：

```
 xrandr --output LVDS --mode 1024x768 --rate 75

```

**注意:** 您通过`xrandr`所作出的更改只能在当前会话暂时生效。详情请参考 [xrandr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xrandr.1)。

## 添加未被检测到的有效分辨率

由于出错的硬件或驱动，xrandr 可能并不能检测出您的显示器所有的有效分辨率。不过，我们可以在xrandr里添加所需要的分辨率。 Also, this same procedure can be used to add refresh rates you know are supported, but not enabled by your driver。

首先，运行`gtf`或者`cvt`，查询某分辨率的有效扫描频率。对于个别LCD显示器（例如samsung 2343NW），可能需要用到"cvt -r"（具有减少空白显示的效果）命令。

```
 $ cvt 1280 1024

 # 1280x1024 59.89 Hz (CVT 1.31M4) hsync: 63.67 kHz; pclk: 109.00 MHz
 Modeline "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync

```

然后通过--newmode参数新建一种xrandr模式，输入上面所得到的查询结果，其中Modeline关键词自然需要被省略。

```
   xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync

```

新建模式后，我们需要把这模式添加到当前的输出设备（假定为VGA1）上。由于一些参数已经事先设置，只需输入模式名称即可，即1280x1024_60.00。

```
   xrandr --addmode VGA1 1280x1024_60.00

```

最后，再把VGA1的分辨率指定为刚刚添加的新模式。

```
   xrandr --output VGA1 --mode 1280x1024_60.00

```

注意，以上设置同样地只能在当前会话暂时生效。

如果您对所要添加的某分辨率感到不放心，您可以追加新命令“sleep 5”以及一条切换到已有有效分辨率的命令，以保证不会被困在实际无效的分辨率，示例：

```
   xrandr --output VGA1 --mode 1280x1024_60.00 && sleep 5 && xrandr --newmode "1024x768-safe" 65.00 1024 1048 1184 1344 768 771 777 806 -HSync -VSync && xrandr --addmode VGA1 1024x768-safe && xrandr --output VGA1 --mode 1024x768-safe

```

其他输出设备如法炮制：VGA1或DVI-I……

## 使xrandr所更改的分辨率设置永久生效

使xrandr定制永久生效的方案有：

*   `xorg.conf`（推荐）
*   `.xprofile`
*   kdm/gdm

### 在xorg.conf设置分辨率（推荐）

示例：

 `/etc/X11/xorg.conf` 
```
Section "Monitor"
    Identifier      "External DVI"
    Modeline        "1280x1024_60.00"  108.88  1280 1360 1496 1712  1024 1025 1028 1060  -HSync +Vsync
    Option          "PreferredMode" "1280x1024_60.00"
EndSection
Section "Device"
    Identifier      "ATI Technologies, Inc. M22 [Radeon Mobility M300]"
    Driver          "ati"
    Option          "Monitor-DVI-0" "External DVI"
EndSection
Section "Screen"
    Identifier      "Primary Screen"
    Device          "ATI Technologies, Inc. M22 [Radeon Mobility M300]"
    DefaultDepth    24
    SubSection "Display"
        Depth           24
        Modes   "1280x1024" "1024x768" "640x480"
    EndSubSection
EndSection

Section "ServerLayout"
        Identifier      "Default Layout"
        Screen          "Primary Screen"
EndSection

```

关于更多的配置细节，请阅读[Xorg (简体中文)](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")或[xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5)。

### 在xprofile设定xrandr命令

请阅读[xprofile](/index.php/Xprofile "Xprofile").

这方案具有缺点：如果您使用[Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")的话，那么在启动进程之后很大程度上就会执行失败，最终无法顺利修改分辨率。

### 在KDM/GDM的启动脚本设定xrandr命令

KDM和GDM都具备在X初始化时，会被自动执行的启动脚本。GDM的启动脚本放在`/etc/gdm/`， KDM的则是`/usr/share/config/kdm/Xsetup`。您可以把相关的xrandr命令添加到这些启动脚本里。

这些脚本需要root权限及其他系统配置的配合，不过在启动进程里会比xprofile更早生效。

## 图形前端

有若干`xrandr`的图形前端可供您使用：

### ARandR

ARandR为xrandr提供了一个简单易用的前端。

其软件包可通过community仓库下载到：[arandr](https://www.archlinux.org/packages/?name=arandr)

### LXrandR

[LXDE](/index.php/LXDE "LXDE")桌面环境默认的显示器配置工具。

这软件也是community仓库的一部分：[lxrandr](https://www.archlinux.org/packages/?name=lxrandr)

## 脚本

控制第二显示器的开关状态，默认显示器保持开启：

 `~/bin/xdisplay` 
```
#!/bin/bash
#
# This script toggles the extended monitor outputs if something is connected
#

# all available outputs
OUTPUTS=$(xrandr |awk '$2 ~ /connected/ {print $1}')

# your notebook LVDS monitor
DEFAULT_OUTPUT=$(sed -ne 's/.*(LVDS[^ ]*).*/1/p' <<<$OUTPUTS)

# get info from xrandr
XRANDR=`xrandr`

EXECUTE=""

for CURRENT in $OUTPUTS
do
        if [[ $XRANDR == *$CURRENT\ connected*  ]] # is connected
        then
                if [[ $XRANDR == *$CURRENT\ connected\ \(* ]] # is disabled
                then
                        EXECUTE+="--output $CURRENT --auto --above $DEFAULT_OUTPUT "
                else
                        EXECUTE+="--output $CURRENT --off "
                fi
        else # make sure disconnected outputs are off 
                EXECUTE+="--output $CURRENT --off "
        fi
done

xrandr --output $DEFAULT_OUTPUT --auto $EXECUTE

```

在显示器之间切换，且只开启其中一个。

 `/usr/local/bin/toggle-display` 
```
#!/bin/bash
#
# toggle-display.sh
#
# Iterates through connected monitors in xrander and switched to the next one
# each time it is run.
#

# get info from xrandr
xStatus=`xrandr`
connectedOutputs=$(echo "$xStatus" | grep " connected" | sed -e "s/\([A-Z0-9]\+\) connected.*/\1/")
activeOutput=$(echo "$xStatus" | grep -e " connected [^(]" | sed -e "s/\([A-Z0-9]\+\) connected.*/\1/") 
connected=$(echo $connectedOutputs | wc -w)

# initialize variables
execute="xrandr "
default="xrandr "
i=1
switch=0

for display in $connectedOutputs
do

	# build default configuration
	if [ $i -eq 1 ]
	then
		default=$default"--output $display --auto "
	else
		default=$default"--output $display --off "
	fi

	# build "switching" configuration
	if [ $switch -eq 1 ]
	then
		execute=$execute"--output $display --auto "
		switch=0
	else
		execute=$execute"--output $display --off "
	fi

	# check whether the next output should be switched on
	if [ $display = $activeOutput ]
	then
		switch=1
	fi

	i=$(( $i + 1 ))

done

# check if the default setup needs to be executed then run it
echo "Resulting Configuration:"
if [ -z "$(echo $execute | grep "auto")" ]
then
	echo "Command: $default"
	`$default`
else
	echo "Command: $execute"
	`$execute`
fi
echo -e "
$(xrandr)"

```

您也可以使用xrr-events (from [AUR](https://aur.archlinux.org/packages/xrr-events-git/))，一种负责监听XrandR事件的daemon服务。当某台显示器接通状态发生变动时，就会执行相关脚本。可在man页面进一步查询具体信息。

## 在VNC上使用xrandr

如果您在使用某台支持xrandr的VNC服务器，您可以通过"xrandr -s <width>x<height>"命令实时修改VNC的分辨率。tigervnc就是一种支持xrandr的VNC客户端。

示例：

```
xrandr -s 1920x1200

```

登陆VNC之后，如果您在控制台上输入"xrandr"，您将得到列出当前已配置模式的清单。每个模式均可通过xrandr -s选项激活。不过，若您所需要的模式并不在清单中，您可以按照以下来添加它。

示例：不妨想添加的是1024x600（上网本的一种常见分辨率）

首先执行CVT，得到理想分辨率所对应的正确刷新频率。

```
$ cvt 1024 600

```

您会得到如下类似的输出：

```
# 1024x600 59.85 Hz (CVT) hsync: 37.35 kHz; pclk: 49.00 MHz
Modeline "1024x600_60.00"   49.00  1024 1072 1168 1312  600 603 613 624 -hsync +vsync

```

在以下命令使用那些关于刷新频率的输出部分。

```
xrandr --newmode "1024x600"   49.00  1024 1072 1168 1312  600 603 613 624 -hsync +vsync
xrandr --addmode default "1024x600"

```

通过以上流程，输入xrandr -s 1024x600，就可以设置当前分辨率为1024x600，但是这设置只在当前的X会话暂时生效。为确保其模式永久可用，在~/.vnc/xstartup添加以下：

```
xrandr --newmode "1024x600"   49.00  1024 1072 1168 1312  600 603 613 624 -hsync +vsync
xrandr --addmode default "1024x600"r

```

## 疑难排除

### 添加未检测到的分辨率

由于硬件以及驱动程序可能的缺陷，例如，请求的EDID数据块不正确，导致 xrandr 可能不能准确侦测到显示器的分辨率。不过我们可以手工添加期望的分辨率。

首先，运行 `gtf` 或 `cvt` 以获取所需分辨率的 **模式行（Modeline）** ：

 `$ cvt 1280 1024` 
```
# 1280x1024 59.89 Hz (CVT 1.31M4) hsync: 63.67 kHz; pclk: 109.00 MHz
Modeline "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync

```

**Tip:** For some LCD screens (e.g. Samsung 2343NW, Acer XB280HK), the command `cvt -r` (= with reduced blanking) is to be used.

**注意:** 如果使用了 Intel 的显示驱动程序 [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)，期望的分辨率会在 `/var/log/Xorg.0.log` 中与其他特征值一并报告——如果该值不同于 `gtf` or `cvt` 的输出应首选该值。这里给出一个log文件的报告值与 xrandr 使用值的实例：
```
[    45.063] (II) intel(0): clock: 241.5 MHz   Image Size:  597 x 336 mm
[    45.063] (II) intel(0): h_active: 2560  h_sync: 2600  h_sync_end 2632 h_blank_end 2720 h_border: 0
[    45.063] (II) intel(0): v_active: 1440  v_sync: 1443  v_sync_end 1448 v_blanking: 1481 v_border: 0

```

```
xrandr --newmode "2560x1440" 241.50 2560 2600 2632 2720 1440 1443 1448 1481 -hsync +vsync

```

然后创建一个新的 xandr 模式。注意模式行中那些被忽略的关键字。

```
$ xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync

```

创建完毕还需要一个操作步骤，把这个新模式追加到当前显示输出端口（VGA1）。我们只需引用模式的名称，因为参数已经在前面设置好了。

```
$ xrandr --addmode VGA1 1280x1024_60.00

```

现在，我们可以把屏幕分辨率切换为刚刚追加的值：

```
$ xrandr --output VGA1 --mode 1280x1024_60.00

```

注意，上述这些设置仅在本次会话中有效。

如果你不能确保将要测试的分辨率可用，可以在后面附加一个延迟和一个安全分辨率命令行，就像这样：

```
$ xrandr --output VGA1 --mode 1280x1024_60.00 && sleep 5 && xrandr --newmode "1024x768-safe" 65.00 1024 1048 1184 1344 768 771 777 806 -HSync -VSync && xrandr --addmode VGA1 1024x768-safe && xrandr --output VGA1 --mode 1024x768-safe

```

还有，要把 `VGA1` 改为正确的输出端口名。

#### EDID 校验和无效

如果前述方法导致引导期间发生 `*ERROR* EDID checksum is invalid` 错误，参阅 [这里](/index.php/Kernel_mode_setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.BC.BA.E8.AE.BE.E6.A8.A1.E5.BC.8F.E5.92.8C_EDID "Kernel mode setting (简体中文)") 和 [这里](http://askubuntu.com/questions/201081/how-can-i-make-linux-behave-better-when-edid-is-unavailable).

也许 `xrandr --addmode` 会返回错误 `X Error of failed request: BadMatch`。NVIDIA 用户请参阅 [NVIDIA/Troubleshooting#xrandr BadMatch](/index.php/NVIDIA/Troubleshooting#xrandr_BadMatch "NVIDIA/Troubleshooting")。`BadMatch` 能指示出无效的 EDID 校验和。要验证确实是这种情况，请以 verbose mode 运行 X 服务（例如：`startx -- -logverbose 6`）然后查阅 Xorg 日志中有关 EDID 错误的信息。

### 纠正电视机分辨率过扫

With a flat panel TV, [w:overscan](https://en.wikipedia.org/wiki/overscan "w:overscan") looks like the picture is "zoomed in" so the edges are cut off.

Check your TV if there is a parameter to change. If not, apply an `underscan` and change border values. The required `underscan vborder` and `underscan hborder` values can be different for you, just check it and change it by more or less.

`$ xrandr --output HDMI-0 --set underscan on --set "underscan vborder" 25 --set "underscan hborder" 40`

### Full RGB in HDMI

It may occur that the [Intel](/index.php/Intel "Intel") driver will not configure correctly the output of the HDMI monitor. It will set a limited color range (16-235) using the [Broadcast RGB property](https://patchwork.kernel.org/patch/1972181/), and the black will not look black, it will be grey.

To see if it is your case:

```
$ xrandr --output HDMI1 --set "Broadcast RGB" "Full"

```

#### Screen resolution reverts back after a blink

If you use [GNOME](/index.php/GNOME "GNOME") and your monitor doesn't have an EDID, above [#Adding undetected resolutions](#Adding_undetected_resolutions) might not work, with your screen just blinking once, after `xrandr --output`.

Poke around with `~/.config/monitors.xml`, or delete the file completely, and then reboot.

It is better explained in [this](http://unix.stackexchange.com/questions/184941/gnome-prevents-high-resolution-vga-without-edid-info-over-vga) article.

## 参见

*   [DualScreen](/index.php/DualScreen "DualScreen") Arch wiki page. How to get dual screens with Xrandr
*   [https://wiki.ubuntu.com/X/Config/Resolution](https://wiki.ubuntu.com/X/Config/Resolution)
*   [Debian Wiki - RandR 1.2 tutorial](https://wiki.debian.org/XStrikeForce/HowToRandR12 "debian:XStrikeForce/HowToRandR12")
*   [https://bbs.archlinux.org/viewtopic.php?pid=652861](https://bbs.archlinux.org/viewtopic.php?pid=652861)
*   [http://nouveau.freedesktop.org/wiki/Randr12Howto](http://nouveau.freedesktop.org/wiki/Randr12Howto)
*   [http://wiki.debian.org/XStrikeForce/HowToRandR12](http://wiki.debian.org/XStrikeForce/HowToRandR12)
*   man xrandr