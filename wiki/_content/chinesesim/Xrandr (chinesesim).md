**翻译状态：** 本文是英文页面 [Xrandr](/index.php/Xrandr "Xrandr") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-5-13，点击[这里](https://wiki.archlinux.org/index.php?title=Xrandr&diff=0&oldid=256070)可以查看翻译后英文页面的改动。

"xrandr" 是一款官方的 [RandR](https://en.wikipedia.org/wiki/RandR "wikipedia:RandR") [Wikipedia:X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") 扩展配置工具。它可以设置屏幕显示的大小、方向、镜像等。对多显示器的情况，请参考 [Multihead](/index.php/Multihead "Multihead") 页面。

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
*   [6 疑难排除](#.E7.96.91.E9.9A.BE.E6.8E.92.E9.99.A4)
    *   [6.1 分辨率低于理想值](#.E5.88.86.E8.BE.A8.E7.8E.87.E4.BD.8E.E4.BA.8E.E7.90.86.E6.83.B3.E5.80.BC)
        *   [6.1.1 修改xorg.conf](#.E4.BF.AE.E6.94.B9xorg.conf)
*   [7 通过Windows客户端查询有效扫描频率](#.E9.80.9A.E8.BF.87Windows.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.9F.A5.E8.AF.A2.E6.9C.89.E6.95.88.E6.89.AB.E6.8F.8F.E9.A2.91.E7.8E.87)
*   [8 脚本](#.E8.84.9A.E6.9C.AC)
*   [9 在VNC上使用xrandr](#.E5.9C.A8VNC.E4.B8.8A.E4.BD.BF.E7.94.A8xrandr)
*   [10 参见](#.E5.8F.82.E8.A7.81)

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

**注意:** 您通过`xrandr`所作出的更改只能在当前会话暂时生效。

## 添加未被检测到的有效分辨率

由于出错的硬件或驱动，xrandr可能并不能检测出您的显示器所有的有效分辨率。不过，我们可以在xrandr里添加所需要的分辨率。

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

关于更多的配置细节，请阅读[Xorg (简体中文)](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")或`man xorg.conf`。

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

## 疑难排除

### 分辨率低于理想值

#### 修改xorg.conf

如果您在xorg.conf所设置的显卡能被正确识别出，但是实际分辨率仍低于理想值，您不妨先参考下这方案：

假如您有一块ATI X1550基础显卡和两台LCD显示器：DELL 2408（1920x1200）和Samsung 206BW（1680x1050）。但是xrandr所列出的最高有效分辨率只有默认的1152x864。您可以试试再编辑/etc/X11/xorg.conf，即添加一条虚拟分辨率：

修改xorg.conf

 `/etc/X11/xorg.conf` 
```
Section "Screen"
        ...
        SubSection "Display"
                Virtual 3600 1200
        EndSubSection
EndSection

```

关于数字部分的理解：DELL与Samsung左右并列。于是双LCD的总宽度就共有1920+1680=3600，总高度则计为两者中的最大高度数，即max(1200,1050)=1200。如果您打算把其中一台LCD置于另一台之上，就这样计算：(max(宽度1, 宽度2), 高度1+高度2)。

再重新登录下，看看是否有效果。

## 通过Windows客户端查询有效扫描频率

请阅读[Obtaining modelines from Windows program PowerStrip](http://www.x.org/wiki/FAQVideoModes#ObtainingmodelinesfromWindowsprogramPowerStrip)。

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

## 参见

*   [DualScreen](/index.php/DualScreen "DualScreen") Arch wiki page. How to get dual screens with Xrandr
*   [https://wiki.ubuntu.com/X/Config/Resolution](https://wiki.ubuntu.com/X/Config/Resolution)
*   [https://bbs.archlinux.org/viewtopic.php?pid=652861](https://bbs.archlinux.org/viewtopic.php?pid=652861)
*   [http://nouveau.freedesktop.org/wiki/Randr12Howto](http://nouveau.freedesktop.org/wiki/Randr12Howto)
*   [http://wiki.debian.org/XStrikeForce/HowToRandR12](http://wiki.debian.org/XStrikeForce/HowToRandR12)
*   man xrandr