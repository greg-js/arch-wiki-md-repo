# TrackPoint

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Many pages in [Category:Lenovo](/index.php/Category:Lenovo "Category:Lenovo") contain more detailed configuration, which need to be merged here. See [[1]](https://wiki.ubuntuusers.de/Trackpoint) for a comparable article (untranslated) (Discuss in [ArchWiki:Requests#TrackPoint](https://wiki.archlinux.org/index.php/ArchWiki:Requests#TrackPoint))

The TrackPoint is Lenovo's trademark for the pointing-stick in the middle of the keyboard. It is supported by [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). The evdev driver is default for [Xorg](/index.php/Xorg "Xorg").

Default [Xorg](/index.php/Xorg "Xorg") behavior supports click and point, but middle-click and scrolling requires extra configuration.

## Contents

*   [1 Middle button scroll](#Middle_button_scroll)
*   [2 Tap to select](#Tap_to_select)
*   [3 udev configuration rule](#udev_configuration_rule)
*   [4 Xorg configuration](#Xorg_configuration)
*   [5 See also](#See_also)

## Middle button scroll

For those using the `evdev` driver, middle-button scrolling is supported via the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package, with the following sane config:

 `~/.xinitrc` 

```
xinput set-prop "TPPS/2 IBM TrackPoint" "Evdev Wheel Emulation" 1
xinput set-prop "TPPS/2 IBM TrackPoint" "Evdev Wheel Emulation Button" 2
xinput set-prop "TPPS/2 IBM TrackPoint" "Evdev Wheel Emulation Timeout" 200
xinput set-prop "TPPS/2 IBM TrackPoint" "Evdev Wheel Emulation Axes" 6 7 4 5
xinput set-prop "TPPS/2 IBM TrackPoint" "Device Accel Constant Deceleration" 0.95

```

The `"Device Accel Constant Deceleration"` line configures the sensitivity of the trackpoint. Note that you can just type these commands into the shell, changing sensitivity on the fly to find a value that's sensible.

For those using the `libinput` driver, middle-button scrolling is enabled by default.

## Tap to select

The TrackPoint supports tap-to-click functionality just as most touchpads do. To enable it manually:

```
# echo -n 1 > /sys/devices/platform/i8042/serio1/press_to_select

```

**Note:** The location of the `press_to_select` file may be different depending on the device you are using. Systems with both a TrackPoint and a touchpad device will use the `/sys/devices/platform/i8042/serio1/serio2/` path, whereas systems with only a TrackPoint device will use the `/sys/devices/platform/i8042/serio1/` path.

## udev configuration rule

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** This rule does not trigger (Discuss in [Talk:TrackPoint#Udev rule](https://wiki.archlinux.org/index.php/Talk:TrackPoint#Udev_rule))

This rule increases the trackpoint **speed** and enables **tap to select** (see above) on boot. Feel free to alter the values and add other modifications to files in /sys/devices/platform/i8042/serio1/serio2/. The rule also works for trackpoint-only devices.

 `/etc/udev/rules.d/10-trackpoint.rules`  `SUBSYSTEM=="serio", DRIVERS=="psmouse", ACTION=="change", ENV{SERIO_TYPE}=="05", ATTR{press_to_select}="1", ATTR{sensitivity}="230", ATTR{speed}="200"` 

## Xorg configuration

To enable scrolling with the TrackPoint while holding down the middle mouse button, create a new file `/etc/X11/xorg.conf.d/20-thinkpad.conf` with the following content:

```
Section "InputClass"
    Identifier	"Trackpoint Wheel Emulation"
    MatchProduct	"TPPS/2 IBM TrackPoint|DualPoint Stick|Synaptics Inc. Composite TouchPad / TrackPoint|ThinkPad USB Keyboard with TrackPoint|USB Trackpoint pointing device"
    MatchDevicePath	"/dev/input/event*"
    Option		"EmulateWheel"		"true"
    Option		"EmulateWheelButton"	"2"
    Option		"Emulate3Buttons"	"false"
    Option		"XAxisMapping"		"6 7"
    Option		"YAxisMapping"		"4 5"
EndSection

```

## See also

*   [How to configure the TrackPoint - ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint)
*   [Trackpoint speed](https://gist.githubusercontent.com/noromanba/11261595/raw/478cf4c4d9b63f1e59364a6f427ffccd63db5e1e/thinkpad-trackpoint-speed.mkd)

Retrieved from "[https://wiki.archlinux.org/index.php?title=TrackPoint&oldid=409777](https://wiki.archlinux.org/index.php?title=TrackPoint&oldid=409777)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Input devices](/index.php/Category:Input_devices "Category:Input devices")
*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")