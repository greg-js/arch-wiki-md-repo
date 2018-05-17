The **Logitech M570** is a wireless trackball mouse. It is quite similar to the [Logitech Marble Mouse](/index.php/Logitech_Marble_Mouse "Logitech Marble Mouse").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Temporary](#Temporary)
    *   [2.2 Permanent](#Permanent)
        *   [2.2.1 Using libinput](#Using_libinput)
        *   [2.2.2 Using evdev](#Using_evdev)
*   [3 See also](#See_also)

## Installation

No additional drivers need to be installed.

## Configuration

### Temporary

If the system is not using [libinput](/index.php/Libinput "Libinput"), the mouse can be configured on the fly using a script such as:

```
#!/bin/sh
dev="Logitech M570"
we="Evdev Wheel Emulation"

xinput set-int-prop "$dev" "$we" 8 1
xinput set-int-prop "$dev" "$we Button" 8 3

```

### Permanent

To make the changes permanent, either a script such as the one above has to be run at startup/login or changes can be made to the [Xorg configuration files](/index.php/Xorg#Using_.conf_files "Xorg"). When changing the configuration files, the product name as reported by Xorg has to be known and used. Typically, your M570 should be known as `Logitech M570`, however, it can be valuable to check `/var/log/Xorg.0.log` for the match product name.

In the two configuration files below, only the essential changes are made to get button scrolling to work. Other worthwhile options are:

*   `Option "EmulateWheelInertia" "5"`
*   `Option "EmulateWheelTimeout" "100"`

It is important to find out if your system is using **only** evdev or libinput **and** evdev. See [Xorg#Input devices](/index.php/Xorg#Input_devices "Xorg") for how to check the driver in use.

Changes made to Xorg configuration files do not take effect until the X session is restarted. To restart the X session, simply log out from your window manager and log back in.

#### Using libinput

Create a configuration file for libinput to recognise it:

 `/etc/X11/xorg.conf.d/41-libinput.conf` 
```
Section "InputClass"
        Identifier      "Logitech M570"
        MatchProduct    "Logitech M570"
        Driver          "libinput"
        Option          "ScrollMethod" "button"
        Option          "ScrollButton" "3"
	Option		"MiddleEmulation" "on"
EndSection
```

#### Using evdev

Create a configuration file for evdev to recognise it:

 `/etc/X11/xorg.conf.d/10-evdev.conf` 
```
Section "InputClass"
    Identifier      "Logitech M570"
    MatchProduct    "Logitech M570"
    Driver          "evdev"
    Option "EmulateWheel" "true"
    Option "EmulateWheelButton" "3"
EndSection
```

## See also

*   [Scroll Like A Ninja - Logitech M570 Trackball & Linux Mint](https://web.archive.org/web/20171102201106/http://dailyherold.net/linux/trackball/m570/2014/10/31/ninja-scrolling-linux-m570-trackball/)
*   [Ubuntu documentation](https://help.ubuntu.com/community/Logitech_Marblemouse_USB)