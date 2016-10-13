The TrackPoint is Lenovo's trademark for the pointing-stick in the middle of the keyboard. It is supported by [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

Default [Xorg](/index.php/Xorg "Xorg") behavior supports click and point. For the `evdev` driver middle-click and scrolling requires extra configuration.

## Contents

*   [1 GUI configuration](#GUI_configuration)
*   [2 Middle button scroll](#Middle_button_scroll)
    *   [2.1 Xorg configuration](#Xorg_configuration)
*   [3 Tap to select](#Tap_to_select)
*   [4 udev configuration rule (but see "TrackPoint configuration by systemd.path unit" below)](#udev_configuration_rule_.28but_see_.22TrackPoint_configuration_by_systemd.path_unit.22_below.29)
*   [5 TrackPoint configuration by systemd.path unit](#TrackPoint_configuration_by_systemd.path_unit)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Trackpoint is not detected or is detected after X minutes](#Trackpoint_is_not_detected_or_is_detected_after_X_minutes)
*   [7 See also](#See_also)

## GUI configuration

[Install](/index.php/Install "Install") the [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings) package.

## Middle button scroll

When using [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput), middle-button scrolling is enabled by default.

**Tip:** On two button trackpoints, the scroll button can be set to right click button without removing functionality.

When using [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev), middle-button scrolling is supported via *xinput* from the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package. For example:

 `~/.xinitrc` 
```
xinput set-prop "*TPPS/2 IBM TrackPoint*" "Evdev Wheel Emulation" 1
xinput set-prop "*TPPS/2 IBM TrackPoint*" "Evdev Wheel Emulation Button" 2
xinput set-prop "*TPPS/2 IBM TrackPoint*" "Evdev Wheel Emulation Timeout" 200
xinput set-prop "*TPPS/2 IBM TrackPoint*" "Evdev Wheel Emulation Axes" 6 7 4 5

```

**Note:**

*   Devices names can be listed with `xinput --list` or [hwinfo](https://www.archlinux.org/packages/?name=hwinfo).
*   The `"Device Accel Constant Deceleration"` line configures the sensitivity of the trackpoint.

### Xorg configuration

Alternative to an `~/.xinitrc` configuration, you can also create an [Xorg#Configuration](/index.php/Xorg#Configuration "Xorg") for the `evdev` driver. For example, as `/etc/X11/xorg.conf.d/20-thinkpad.conf`, replacing `TPPS/2 IBM TrackPoint` with the device name from *xinput*:

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

## Tap to select

The TrackPoint supports tap-to-click functionality just as most touchpads do. To enable it manually:

```
# echo -n 1 > /sys/devices/platform/i8042/serio1/press_to_select

```

**Note:** The location of the `press_to_select` file may be different depending on the device you are using. Systems with both a TrackPoint and a touchpad device will use the `/sys/devices/platform/i8042/serio1/serio2/` path, whereas systems with only a TrackPoint device will use the `/sys/devices/platform/i8042/serio1/` path.

## udev configuration rule (but see "TrackPoint configuration by systemd.path unit" below)

This rule increases the trackpoint **speed** and enables **tap to select** (see above) on boot. Feel free to alter the values and add other modifications to files in /sys/devices/platform/i8042/serio1/serio2/. The rule also works for trackpoint-only devices.

 `/etc/udev/rules.d/10-trackpoint.rules`  `ACTION=="add", SUBSYSTEM=="input", ATTR{name}=="TPPS/2 IBM TrackPoint", ATTR{device/sensitivity}="240", ATTR{device/press_to_select}="1"` 

## TrackPoint configuration by systemd.path unit

There have been [reports on the forums](https://bbs.archlinux.org/viewtopic.php?id=199998) that the attributes/files under /sys/devices/platform/i8042/serio1/serio2/ appear too late in the boot process for the above (or similar) udev rule(s) to have an effect on them. Instead, a systemd.path unit can be used to configure attributes of the TrackPoint in the following manner:

1) Add the following content to an executable script in `/usr/local/bin/` named:

 `trackpoint_configuration.sh` 
```
#!/usr/bin/env bash

/usr/bin/echo -n "1" > /sys/devices/platform/i8042/serio1/serio2/press_to_select
/usr/bin/echo -n "235" > /sys/devices/platform/i8042/serio1/serio2/sensitivity
/usr/bin/echo -n "90" > /sys/devices/platform/i8042/serio1/serio2/speed
/usr/bin/echo -n "200" > /sys/devices/platform/i8042/serio1/serio2/rate
/usr/bin/echo -n "25" > /sys/devices/platform/i8042/serio1/serio2/drift_time
/usr/bin/echo -n "6" > /sys/devices/platform/i8042/serio1/serio2/inertia
```

Adjust the above attributes and their parameters to your preferences and/or remove those that you don't need.

2) Add the following content to a systemd.path unit file in `/etc/systemd/system/` named:

 `trackpoint_tweaked_parameters.path` 
```
[Unit]
Description=Watch for, and modify, Trackpoint attributes

[Path]
PathExists=/sys/devices/platform/i8042/serio1/serio2/press_to_select
PathExists=/sys/devices/platform/i8042/serio1/serio2/sensitivity
PathExists=/sys/devices/platform/i8042/serio1/serio2/speed
PathExists=/sys/devices/platform/i8042/serio1/serio2/rate
PathExists=/sys/devices/platform/i8042/serio1/serio2/drift_time
PathExists=/sys/devices/platform/i8042/serio1/serio2/inertia

[Install]
WantedBy=default.target
```

Adjust the above list of attributes to reflect those given in the script from #1.

3) Add the following content to a systemd.service unit file in `/etc/systemd/system/` named:

 `trackpoint_tweaked_parameters.service` 
```
[Unit]
Description=Watch for, and modify, Trackpoint attributes

[Service]
Type=simple
ExecStart=/usr/local/bin/trackpoint_configuration.sh
```

4) Enable and start the new systemd.path unit with systemctl:

```
# systemctl enable trackpoint_tweaked_parameters.path && systemctl start trackpoint_tweaked_parameters.path

```

5) Check the parameters of the attributes in /sys/devices/platform/i8042/serio1/serio2/ at your next reboot, which should now be modified according to the script from #1.

## Troubleshooting

### Trackpoint is not detected or is detected after X minutes

This appears to be a kernel bug. See: [https://bugzilla.kernel.org/show_bug.cgi?id=33292](https://bugzilla.kernel.org/show_bug.cgi?id=33292)

A workaround is passing `proto=bare` to the `psmouse` module. However, this disables scrolling with the clickpad and the two-finger middle click:

```
# modprobe psmouse proto=bare

```

## See also

*   [How to configure the TrackPoint - ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint)
*   [Trackpoint speed](https://gist.githubusercontent.com/noromanba/11261595/raw/478cf4c4d9b63f1e59364a6f427ffccd63db5e1e/thinkpad-trackpoint-speed.mkd)
*   [What is the best way to configure a Thinkpad's TrackPoint?](https://askubuntu.com/questions/37824/what-is-the-best-way-to-configure-a-thinkpads-trackpoint/553926)