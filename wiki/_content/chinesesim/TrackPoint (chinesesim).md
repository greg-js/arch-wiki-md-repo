**翻译状态：** 本文是英文页面 [TrackPoint](/index.php/TrackPoint "TrackPoint") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-17，点击[这里](https://wiki.archlinux.org/index.php?title=TrackPoint&diff=0&oldid=425743)可以查看翻译后英文页面的改动。

小红点(TrackPoint)是联想所有的键盘中间的指点杆的商标。[xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) 和 [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) 都支持它。evdev是 [Xorg](/index.php/Xorg "Xorg") 的默认驱动。

在默认设置中，[Xorg](/index.php/Xorg "Xorg") 支持点击和指点, 但是用中键做滚轮需要更多的配置。

## Contents

*   [1 GUI 配置](#GUI_.E9.85.8D.E7.BD.AE)
*   [2 用中键作滚轮](#.E7.94.A8.E4.B8.AD.E9.94.AE.E4.BD.9C.E6.BB.9A.E8.BD.AE)
*   [3 Tap to select](#Tap_to_select)
*   [4 udev configuration rule](#udev_configuration_rule)
*   [5 Xorg configuration](#Xorg_configuration)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Trackpoint is not detected or is detected after X minutes](#Trackpoint_is_not_detected_or_is_detected_after_X_minutes)
*   [7 See also](#See_also)

## GUI 配置

安装 [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings) 软件包。

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

## Tap to select

The TrackPoint supports tap-to-click functionality just as most touchpads do. To enable it manually:

```
# echo -n 1 > /sys/devices/platform/i8042/serio1/press_to_select

```

**Note:** The location of the `press_to_select` file may be different depending on the device you are using. Systems with both a TrackPoint and a touchpad device will use the `/sys/devices/platform/i8042/serio1/serio2/` path, whereas systems with only a TrackPoint device will use the `/sys/devices/platform/i8042/serio1/` path.

## udev configuration rule

This rule increases the trackpoint **speed** and enables **tap to select** (see above) on boot. Feel free to alter the values and add other modifications to files in /sys/devices/platform/i8042/serio1/serio2/. The rule also works for trackpoint-only devices.

 `/etc/udev/rules.d/10-trackpoint.rules`  `ACTION=="add", SUBSYSTEM=="input", ATTR{name}=="TPPS/2 IBM TrackPoint", ATTR{device/sensitivity}="240"` 

## Xorg configuration

To enable scrolling with the TrackPoint while holding down the middle mouse button, create `/etc/X11/xorg.conf.d/20-thinkpad.conf`, replacing `TPPS/2 IBM TrackPoint` with the device name from *xinput*:

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

## Troubleshooting

### Trackpoint is not detected or is detected after X minutes

This appears to be a kernel bug. See: [https://bugzilla.kernel.org/show_bug.cgi?id=33292](https://bugzilla.kernel.org/show_bug.cgi?id=33292)

A workaround is passing proto=bare to the psmouse module. However this disable scrolling with the clickpad and the two finger middle click.

```
modprobe psmouse proto=bare

```

## See also

*   [How to configure the TrackPoint - ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint)
*   [Trackpoint speed](https://gist.githubusercontent.com/noromanba/11261595/raw/478cf4c4d9b63f1e59364a6f427ffccd63db5e1e/thinkpad-trackpoint-speed.mkd)
*   [What is the best way to configure a Thinkpad's TrackPoint?](https://askubuntu.com/questions/37824/what-is-the-best-way-to-configure-a-thinkpads-trackpoint/553926)