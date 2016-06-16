The TrackPoint is Lenovo's trademark for the pointing-stick in the middle of the keyboard. It is supported by [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). The evdev driver is default for [Xorg](/index.php/Xorg "Xorg").

Default [Xorg](/index.php/Xorg "Xorg") behavior supports click and point, but middle-click and scrolling requires extra configuration.

## Contents

*   [1 GUI configuration](#GUI_configuration)
*   [2 Middle button scroll](#Middle_button_scroll)
*   [3 Tap to select](#Tap_to_select)
*   [4 udev configuration rule](#udev_configuration_rule)
*   [5 Xorg configuration](#Xorg_configuration)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Trackpoint is not detected or is detected after X minutes](#Trackpoint_is_not_detected_or_is_detected_after_X_minutes)
*   [7 See also](#See_also)

## GUI configuration

[Install](/index.php/Install "Install") the [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings) package.

## Middle button scroll

When using [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput), middle-button scrolling is enabled by default.

When using [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev), middle-button scrolling is supported via *xinput* from the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package. For example:

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

*   Devices names can be listed with `xinput --list` or [hwinfo](https://www.archlinux.org/packages/?name=hwinfo).
*   The `"Device Accel Constant Deceleration"` line configures the sensitivity of the trackpoint.

## Tap to select

The TrackPoint supports tap-to-click functionality just as most touchpads do. To enable it manually:

```
# echo -n 1 > /sys/devices/platform/i8042/serio1/press_to_select

```

**Note:** The location of the `press_to_select` file may be different depending on the device you are using. Systems with both a TrackPoint and a touchpad device will use the `/sys/devices/platform/i8042/serio1/serio2/` path, whereas systems with only a TrackPoint device will use the `/sys/devices/platform/i8042/serio1/` path.

## udev configuration rule

This rule increases the trackpoint **speed** and enables **tap to select** (see above) on boot. Feel free to alter the values and add other modifications to files in /sys/devices/platform/i8042/serio1/serio2/. The rule also works for trackpoint-only devices.

 `/etc/udev/rules.d/10-trackpoint.rules`  `ACTION=="add", SUBSYSTEM=="input", ATTR{name}=="TPPS/2 IBM TrackPoint", ATTR{device/sensitivity}="240", ATTR{device/press_to_select}="1"` 

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