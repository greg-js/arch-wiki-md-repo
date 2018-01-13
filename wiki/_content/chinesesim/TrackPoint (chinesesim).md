**翻译状态：** 本文是英文页面 [TrackPoint](/index.php/TrackPoint "TrackPoint") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-08，点击[这里](https://wiki.archlinux.org/index.php?title=TrackPoint&diff=0&oldid=437637)可以查看翻译后英文页面的改动。

小红点(TrackPoint)是联想所有的键盘中间的指点杆的商标。[xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) 和 [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) 都支持它。evdev是 [Xorg](/index.php/Xorg "Xorg") 的默认驱动。

在默认设置中，[Xorg](/index.php/Xorg "Xorg") 支持点击和指点, 但是用中键做滚轮需要更多的配置。

## Contents

*   [1 GUI 配置](#GUI_.E9.85.8D.E7.BD.AE)
*   [2 用中键作滚轮](#.E7.94.A8.E4.B8.AD.E9.94.AE.E4.BD.9C.E6.BB.9A.E8.BD.AE)
*   [3 按压选择](#.E6.8C.89.E5.8E.8B.E9.80.89.E6.8B.A9)
*   [4 udev规则](#udev.E8.A7.84.E5.88.99)
*   [5 Xorg配置](#Xorg.E9.85.8D.E7.BD.AE)
*   [6 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [6.1 小红点没被检测到或者在X分钟后被检测到](#.E5.B0.8F.E7.BA.A2.E7.82.B9.E6.B2.A1.E8.A2.AB.E6.A3.80.E6.B5.8B.E5.88.B0.E6.88.96.E8.80.85.E5.9C.A8X.E5.88.86.E9.92.9F.E5.90.8E.E8.A2.AB.E6.A3.80.E6.B5.8B.E5.88.B0)
*   [7 参考](#.E5.8F.82.E8.80.83)

## GUI 配置

安装 [gpointing-device-settings](https://aur.archlinux.org/packages/gpointing-device-settings/) 软件包。

## 用中键作滚轮

使用 [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) 时，用中键作滚轮的功能默认启用。

使用 [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) 时，用中键作滚轮的功能由 [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) 软件包的 *xinput* 支持。例如：

 `~/.xinitrc` 
```
tpset() { xinput set-prop "*TPPS/2 IBM TrackPoint*" "$@"; }

tpset "Evdev Wheel Emulation" 1
tpset "Evdev Wheel Emulation Button" 2
tpset "Evdev Wheel Emulation Timeout" 200
tpset "Evdev Wheel Emulation Axes" 6 7 4 5
tpset "Device Accel Constant Deceleration" 0.95

```

**Note:**

*   可以用 `xinput --list` 或 [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) 列出设备名。
*   `"Device Accel Constant Deceleration"` 一行配置小红点的敏感度。

## 按压选择

小红点和很多触摸板一样支持按压选择功能。要手工打开此功能：

```
# echo -n 1 > /sys/devices/platform/i8042/serio1/press_to_select

```

**Note:** `press_to_select` 文件的位置可能会因为你使用的设备而有所不同。同时带有小红点和触摸板的系统会用 `/sys/devices/platform/i8042/serio1/serio2/` 路径，而只有小红点的设备会用 `/sys/devices/platform/i8042/serio1/` 路径。

## udev规则

这条规则增大小红点的**速度**并在启动时打开**按压选择**功能（如上所述）。 随便改变这些数值并添加其他修改到 /sys/devices/platform/i8042/serio1/serio2/ 的文件中。这个规则也使用于只有小红点的设备。

 `/etc/udev/rules.d/10-trackpoint.rules`  `ACTION=="add", SUBSYSTEM=="input", ATTR{name}=="TPPS/2 IBM TrackPoint", ATTR{device/sensitivity}="240", ATTR{device/press_to_select}="1"` 

## Xorg配置

要打开按下中键时用小红点作滚轮的功能，创建 `/etc/X11/xorg.conf.d/20-thinkpad.conf`，用*xinput*给的设备名字替换 `TPPS/2 IBM TrackPoint`:

```
Section "InputClass"
    Identifier	"Trackpoint Wheel Emulation"
    MatchProduct	"*TPPS/2 IBM TrackPoint*"
    MatchDevicePath	"/dev/input/event*"
    Option		"EmulateWheel"		"true"
    Option		"EmulateWheelButton"	"2"
    Option		"Emulate3Buttons"	"false"
    Option		"XAxisMapping"		"6 7"
    Option		"YAxisMapping"		"4 5"
EndSection

```

## 故障排除

### 小红点没被检测到或者在X分钟后被检测到

这看起来是个内核的bug: [https://bugzilla.kernel.org/show_bug.cgi?id=33292](https://bugzilla.kernel.org/show_bug.cgi?id=33292)

一个方案是往 psmouse 模块传入 proto=bare 参数。但是这会禁止触摸板的滚动功能和两指中键点击功能。

```
modprobe psmouse proto=bare

```

## 参考

*   [How to configure the TrackPoint - ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint)
*   [Trackpoint speed](https://gist.githubusercontent.com/noromanba/11261595/raw/478cf4c4d9b63f1e59364a6f427ffccd63db5e1e/thinkpad-trackpoint-speed.mkd)
*   [What is the best way to configure a Thinkpad's TrackPoint?](https://askubuntu.com/questions/37824/what-is-the-best-way-to-configure-a-thinkpads-trackpoint/553926)