**翻译状态：** 本文是英文页面 [Mouse_acceleration](/index.php/Mouse_acceleration "Mouse acceleration") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-22，点击[这里](https://wiki.archlinux.org/index.php?title=Mouse_acceleration&diff=0&oldid=331574)可以查看翻译后英文页面的改动。

这里有以下几种方式设置鼠标加速:

1.  通过设置xorg配置文件
2.  [xorg-server-utils](https://www.archlinux.org/packages/?name=xorg-server-utils)包提供了这两个命令让您能通过Shell和脚本方式来调整鼠标设置:
    *   **xset**
    *   **xinput**
3.  大部分的[desktop environment](/index.php/Desktop_environment "Desktop environment")提供了图形化的鼠标设置界面，您可以非常容易的找到并使用它。

## Contents

*   [1 设置鼠标加速](#.E8.AE.BE.E7.BD.AE.E9.BC.A0.E6.A0.87.E5.8A.A0.E9.80.9F)
    *   [1.1 通过xorg配置文件](#.E9.80.9A.E8.BF.87xorg.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [1.2 通过使用xset](#.E9.80.9A.E8.BF.87.E4.BD.BF.E7.94.A8xset)
    *   [1.3 通过使用xinput](#.E9.80.9A.E8.BF.87.E4.BD.BF.E7.94.A8xinput)
    *   [1.4 设置范例](#.E8.AE.BE.E7.BD.AE.E8.8C.83.E4.BE.8B)
*   [2 取消鼠标加速](#.E5.8F.96.E6.B6.88.E9.BC.A0.E6.A0.87.E5.8A.A0.E9.80.9F)

## 设置鼠标加速

### 通过xorg配置文件

参见 [xorg.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5) 来获得详细信息.

范例:

 `/etc/X11/xorg.conf.d/50-mouse-acceleration.conf` 
```
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
# set the following to 1 1 0 respectively to disable acceleration.
	Option "AccelerationNumerator" "2"
	Option "AccelerationDenominator" "1"
	Option "AccelerationThreshold" "4"
EndSection
```
 `/etc/X11/xorg.conf.d/50-mouse-deceleration.conf` 
```
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
# some curved deceleration
#	Option "AdaptiveDeceleration" "2"
# linear deceleration (mouse speed reduction)
	Option "ConstantDeceleration" "2"
EndSection
```

您还可以通过使用"MatchProduct", "MatchVendor" 等设置特定的硬件。

### 通过使用xset

查看现在的设置，请键入以下命令:

```
$ xset q | grep -A 1 Pointer

```

如要改变设置，输入:

```
$ xset m *acceleration* *threshold*

```

在*acceleration*处输入想要加快的倍速. *threshold*为鼠标加速的阀值。

*acceleration*也可以用分数来表示,如果想要减慢鼠标的移动速度，您可以尝试1/2, 1/3, 1/4等速率, ... 如果想要更快，您也可以尝试 2/1, 3/1, 4/1等速率，比如:

```
$ xset m 3/2 0

```

as suggested in the man page, then acceleration is treated as "the exponent of a more natural and continuous formula."

如要恢复默认设置:

```
$ xset m default

```

获得更多细节，参见[xset(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/xset.1)页面.

To make it permanent, edit xorg configuration (see above) or add commands to [xprofile](/index.php/Xprofile "Xprofile"). The latter won't affect speed in a [display manager](/index.php/Display_manager "Display manager").

### 通过使用xinput

首先，列出所有已连接电脑的输入设备(忽略Virtual pointer):

```
$ xinput list

```

记下ID号码.您也有可能需要记下设备全名当在ID容易改变的情况下。

列出鼠标的所有设置和它们的值：

```
$ xinput list-props 9

```

`9`是您希望使用的设备的ID值

您也可以通过使用下面的命令来达到相同的效果

```
$ xinput list-props *mouse brand*

```

请将*mouse brand*替换为在`$ xinput list`中得到的名字

例如,改变`Constant Deceleration`属性的值为2:

 `$ xinput list-props 9` 
```
Device '*mouse brand*':
       Device Enabled (121):   1
       Device Accel Profile (240):     0
       Device Accel Constant Deceleration (241):       1.000000
       Device Accel Adaptive Deceleration (243):       1.000000
       Device Accel Velocity Scaling (244):    10.000000

```

```
$ xinput --set-prop '*mouse brand*' 'Device Accel Constant Deceleration' 2

```

`Device Accel Constant Deceleration`可以调整鼠标的移动速度。

To make it permanent, edit xorg configuration (see above) or add commands to [xprofile](/index.php/Xprofile "Xprofile"). The latter won't affect speed in a [Display manager](/index.php/Display_manager "Display manager").

### 设置范例

You may need to resort to using more than one method to achieve your desired mouse settings. Here's what I did to configure a generic optical mouse: First, slow down the default movement speed 3 times so that it's more precise.

```
$ xinput --set-prop 9 'Device Accel Constant Deceleration' 3 &

```

Then, enable acceleration and make it 3 times faster after moving past 6 units.

```
$ xset mouse 3 6 &

```

If you are satisfied of the results, store the preceding commands in `~/.xinitrc`.

## 取消鼠标加速

鼠标加速度的在最近的版本的x server中已经发生了很很大的变化;、，所以用`xset`来改变设置是不成功和不被推荐的。

在[here](http://xorg.freedesktop.org/wiki/Development/Documentation/PointerAcceleration#Introduction)页面中您可以查看`PointerAcceleration`变化的内容。

想要完全取消鼠标加速、减速, 请创建以下文件:

 `/etc/X11/xorg.conf.d/50-mouse-acceleration.conf` 
```
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
	Option "AccelerationProfile" "-1"
	Option "AccelerationScheme" "none"
EndSection
```

并重启X。