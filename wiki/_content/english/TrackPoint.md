The TrackPoint is Lenovo's trademark for the pointing-stick in the middle of the keyboard. It is supported by [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

Default [Xorg](/index.php/Xorg "Xorg") behavior supports click and point. For the `evdev` driver middle-click and scrolling requires extra configuration.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 GUI configuration](#GUI_configuration)
*   [2 Middle button scroll](#Middle_button_scroll)
    *   [2.1 Xorg configuration](#Xorg_configuration)
    *   [2.2 Two-button trackpoints](#Two-button_trackpoints)
*   [3 Sysfs attributes](#Sysfs_attributes)
    *   [3.1 Configuration at boot](#Configuration_at_boot)
        *   [3.1.1 udev rule](#udev_rule)
        *   [3.1.2 systemd.path unit](#systemd.path_unit)
        *   [3.1.3 udev hwdb entry](#udev_hwdb_entry)
        *   [3.1.4 device-quirks](#device-quirks)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Trackpoint is not detected or is detected after X minutes](#Trackpoint_is_not_detected_or_is_detected_after_X_minutes)
    *   [4.2 Trackpoint buttons do not always work](#Trackpoint_buttons_do_not_always_work)
    *   [4.3 Two-finger scroll ceases to work after suspending](#Two-finger_scroll_ceases_to_work_after_suspending)
*   [5 See also](#See_also)

## GUI configuration

[Install](/index.php/Install "Install") the [gpointing-device-settings](https://aur.archlinux.org/packages/gpointing-device-settings/) package.

**Note:** This software is not maintained anymore (last release in 2013). It may not allow deep configuration when [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) is used.

## Middle button scroll

When using [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput), middle-button scrolling is enabled by default.

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

Alternative to an `~/.xinitrc` configuration, you can also create an [Xorg#Configuration](/index.php/Xorg#Configuration "Xorg") for the [evdev(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/evdev.4)driver. For example, as `/etc/X11/xorg.conf.d/20-thinkpad.conf`, replacing `TPPS/2 IBM TrackPoint` with the device name from *xinput*:

```
Section "InputClass"
    Identifier	"Trackpoint Wheel Emulation"
    Driver "evdev"
    MatchProduct	"*TPPS/2 IBM TrackPoint*"
    MatchDevicePath	"/dev/input/event*"
    Option		"EmulateWheel"		"true"
    Option		"EmulateWheelButton"	"2"
    Option		"Emulate3Buttons"	"false"
    Option		"XAxisMapping"		"6 7"
    Option		"YAxisMapping"		"4 5"
EndSection

```

### Two-button trackpoints

On two-button trackpoints, using [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput), the scroll button can be set to right-click button without removing functionality.

Replacing *device* with the device name from `xinput`:

```
$ xinput set-prop "*device*" "libinput Button Scrolling Button" 3

```

## Sysfs attributes

TrackPoints expose their attributes as files in `/sys/devices/platform/i8042/serio1/`. For example, to manually enable the tap-to-click functionality:

```
# echo -n 1 > /sys/devices/platform/i8042/serio1/press_to_select

```

**Note:** The location of the attribute files may be different depending on the device you are using. Systems with both a TrackPoint and a touchpad device will use either `/sys/devices/platform/i8042/serio1/serio2/` or `/sys/devices/platform/i8042/serio1/serio3/` for the path, whereas systems with only a TrackPoint device will use the `/sys/devices/platform/i8042/serio1/` path.

### Configuration at boot

#### udev rule

This rule increases the trackpoint **speed** and enables **tap to select** (see above) on boot.

 `/etc/udev/rules.d/10-trackpoint.rules`  `ACTION=="add", SUBSYSTEM=="input", ATTR{name}=="TPPS/2 IBM TrackPoint", ATTR{device/sensitivity}="240", ATTR{device/press_to_select}="1"` 

#### systemd.path unit

There have been [reports on the forums](https://bbs.archlinux.org/viewtopic.php?id=199998) that the attributes/files under `/sys/devices/platform/i8042/serio1/serio2/` appear too late in the boot process for the above (or similar) udev rule(s) to have an effect on them. Instead, a *systemd.path* unit can be used to configure attributes of the TrackPoint.

First create an executable script named e.g. `/usr/local/bin/trackpoint_configuration.sh` that sets the TrackPoint attributes as shown in the [#Sysfs attributes](#Sysfs_attributes) section. Then create the following systemd units. Make sure that all attributes modified by the script are listed with `PathExists`.

 `/etc/systemd/system/trackpoint_parameters.path` 
```
[Unit]
Description=Watch for, and modify, Trackpoint attributes

[Path]
PathExists=/sys/devices/platform/i8042/serio1/press_to_select

[Install]
WantedBy=default.target
```
 `/etc/systemd/system/trackpoint_parameters.service` 
```
[Unit]
Description=Set TrackPoint attributes

[Service]
ExecStart=/usr/local/bin/trackpoint_configuration.sh
```

Finally, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `trackpoint_parameters.path` systemd unit.

#### udev hwdb entry

Libinput applies its own parameters to sysfs based on entries in the [udev hardware database](https://github.com/systemd/systemd/blob/master/hwdb/70-pointingstick.hwdb). This is the behavior on systems running a Wayland compositor, as libinput is the only supported input interface in that environment. Changes made prior to the start of a Wayland compositor or X session will be overwritten.

To override libinput's default settings, add a local hwdb entry:

 `/etc/udev/hwdb.d/99-trackpoint.hwdb` 
```
evdev:name:TPPS/2 IBM TrackPoint:dmi:bvn*:bvr*:bd*:svnLENOVO:pn*:pvrThinkPad??60?:*
  POINTINGSTICK_SENSITIVITY=250
```

You can find various vendor/model keys in the [udev hardware database](https://github.com/systemd/systemd/blob/master/hwdb/70-pointingstick.hwdb). Note that since [this commit](https://cgit.freedesktop.org/wayland/libinput/commit/src/evdev.c?id=3669fa10dff95371658647272ef7ac7a3ef29a61) libinput ignores the POINTINGSTICK_CONST_ACCEL parameter and uses POINTINGSTICK_SENSITIVITY. The range is 0-255.

Reload udev's hwdb to apply the changes:

```
# udevadm hwdb --update

```

To test the changes prior to restarting your compositor or X session, first find your device input node `/dev/input/eventX` using:

```
# libinput list-devices

```

Run the following to generate some debug output:

```
# udevadm trigger /sys/class/input/eventX
# udevadm test /sys/class/input/eventX

```

**Note:** This will not actually apply the parameters from hwdb, but you can verify the changes in the output of the `udevadm test` command.

Finally, restart your Wayland compositor or X session to apply the changes.

#### device-quirks

With the `libinput` switch to the new device-quirks `.ini`-style configuration files, you can adjust trackpoint parameters via local overrides in `/etc/libinput/`.

For example, to override the pointing speed, create `/etc/libinput/local-overrides.quirks`:

```
[Trackpoint Override]
MatchUdevType=pointingstick
AttrTrackpointMultiplier=0.75

```

For more information, see [libinput: Installing temporary local device quirks](https://wayland.freedesktop.org/libinput/doc/latest/device-quirks.html#installing-temporary-local-device-quirks)

**Note:** Model quirks are internal API and may change at any time. No backwards-compatibility is guaranteed. Local overrides should only be used until the distribution updates the libinput packages.

## Troubleshooting

### Trackpoint is not detected or is detected after X minutes

This appears to be a kernel bug. See: [https://bugzilla.kernel.org/show_bug.cgi?id=33292](https://bugzilla.kernel.org/show_bug.cgi?id=33292)

A workaround is passing `proto=bare` to the `psmouse` module. However, this disables scrolling with the clickpad and the two-finger middle click:

```
# modprobe psmouse proto=bare

```

### Trackpoint buttons do not always work

If you discover that disabling the touchpad in the BIOS disables the wrong buttons and/or that the trackpoint buttons work very unreliable a workaround is to pass `proto=imps` to the `psmouse` module.

```
# rmmod psmouse; modprobe psmouse proto=imps

```

### Two-finger scroll ceases to work after suspending

On some laptops, psmouse seems to fail on start up, or after suspend:

```
psmouse serio1: synaptics: Unable to initialize device

```

One workaround is to use add `psmouse.synaptics_intertouch=0` to your kernel commandline.

## See also

*   [How to configure the TrackPoint - ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint)
*   [Trackpoint speed](https://gist.githubusercontent.com/noromanba/11261595/raw/478cf4c4d9b63f1e59364a6f427ffccd63db5e1e/thinkpad-trackpoint-speed.mkd)
*   [What is the best way to configure a Thinkpad's TrackPoint?](https://askubuntu.com/questions/37824/what-is-the-best-way-to-configure-a-thinkpads-trackpoint/553926)