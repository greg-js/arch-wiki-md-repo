There a various methods to control the *keyboard backlight* brightness level.

## Any vendor

There are a variety ways to manage the brightness level and different helpers tools to accomplish this, such as [brightnessctl](https://www.archlinux.org/packages/?name=brightnessctl) or [light](https://www.archlinux.org/packages/?name=light).

The the `sys` pseudo-file system exposes an interface to the keyboard backlight. The current brightness level can be get by reading `/sys/class/leds/tpacpi::kbd_backlight/brightness`. For example to get the maximum brightness level:

```
 cat /sys/class/leds/tpacpi::kbd_backlight/max_brightness

```

To set the brightness to 1:

```
 echo 1 | sudo tee /sys/class/leds/tpacpi::kbd_backlight/brightness

```

When using `brightnessctl` you can get a list of available brightness controls with `brightnessctl --list`, then to show the kbd backlight information:

```
 brightnessctl --device='tpacpi::kbd_backlight' info

```

This will show the absolute and relative current value and the maximum absolute value. To set a different value:

```
 brightnessctl --device='tpacpi::kbd_backlight' set 1 

```

### D-Bus

You can control your computer keyboard backlight via the [D-Bus](/index.php/D-Bus "D-Bus") interface. The benefits of using it are that no modification to device files is required and it is vendor agnostic.

Here is an example implementation in [Python](/index.php/Python "Python") 3.

[Install](/index.php/Install "Install") [upower](https://www.archlinux.org/packages/?name=upower) and [python-dbus](https://www.archlinux.org/packages/?name=python-dbus) packages then place the following script in `/usr/local/bin/` and make it executable. You can then map your keyboard shortcuts to run `/usr/local/bin/kb-light.py + x` and `/usr/local/bin/kb-light.py - x` to increase and decrease your keyboard backlight level by `x`.

**Tip:** You should try with an x = 1 to determine the limits of the keyboard backlight levels
 `/usr/local/bin/kb-light.py` 
```
#!/usr/bin/env python3

import dbus
import sys

def kb_light_set(delta):
    bus = dbus.SystemBus()
    kbd_backlight_proxy = bus.get_object('org.freedesktop.UPower', '/org/freedesktop/UPower/KbdBacklight')
    kbd_backlight = dbus.Interface(kbd_backlight_proxy, 'org.freedesktop.UPower.KbdBacklight')

    current = kbd_backlight.GetBrightness()
    maximum = kbd_backlight.GetMaxBrightness()
    new = max(0, min(current + delta, maximum))

    if 0 <= new  <= maximum:
        current = new
        kbd_backlight.SetBrightness(current)

    # Return current backlight level percentage
    return 100 * current / maximum

if __name__ ==  '__main__':
    if len(sys.argv) == 2 or len(sys.argv) == 3:
        if sys.argv[1] == "--up" or sys.argv[1] == "+":
            if len(sys.argv) == 3:
                print(kb_light_set(int(sys.argv[2])))
            else:
                print(kb_light_set(17))
        elif sys.argv[1] == "--down" or sys.argv[1] == "-":
            if len(sys.argv) == 3:
                print(kb_light_set(-int(sys.argv[2])))
            else:
                print(kb_light_set(-17))
        else:
            print("Unknown argument:", sys.argv[1])
    else:
        print("Script takes one or two argument.", len(sys.argv) - 1, "arguments provided.")

```

Alternatively the following bash one-liner will set the backlight to the value specified in the *argument*:

```
setKeyboardLight () {
    dbus-send --system --type=method_call  --dest="org.freedesktop.UPower" "/org/freedesktop/UPower/KbdBacklight" "org.freedesktop.UPower.KbdBacklight.SetBrightness" int32:$1 
}

```

### D-Bus control backlight in MATE environment

In case you use [MATE](/index.php/MATE "MATE") environment you might get tired with repeated lighting keyboard backlight while logging in, unlocking screen or waking up dimmed display. Following setup prevent from automatic lighting up during any action. The only triggers remain plugging in the adapter and fresh boot. After that you can control keyboard backlight only via hotkeys (eg. ThinkPad Fn + spacebar).

To prevent automatic lightning up just edit file `/usr/share/dbus-1/system.d/org.freedesktop.UPower.conf` as follows (two occurrences of "deny"):

 `/usr/share/dbus-1/system.d/org.freedesktop.UPower.conf` 
```
<?xml version="1.0" encoding="UTF-8"?> <!-- -*- XML -*- -->

<!DOCTYPE busconfig PUBLIC
 "-//freedesktop//DTD D-BUS Bus Configuration 1.0//EN"
 "http://www.freedesktop.org/standards/dbus/1.0/busconfig.dtd">
<busconfig>
  <!-- Only root can own the service -->
  <policy user="root">
    <allow own="org.freedesktop.UPower"/>
  </policy>
  <policy context="default">

    <allow send_destination="org.freedesktop.UPower"
           send_interface="org.freedesktop.DBus.Introspectable"/>

    <allow send_destination="org.freedesktop.UPower"
           send_interface="org.freedesktop.DBus.Peer"/>
    <allow send_destination="org.freedesktop.UPower"
           send_interface="org.freedesktop.DBus.Properties"/>
    <allow send_destination="org.freedesktop.UPower.Device"
           send_interface="org.freedesktop.DBus.Properties"/>
    <deny  send_destination="org.freedesktop.UPower.KbdBacklight"
           send_interface="org.freedesktop.DBus.Properties"/>
    <allow send_destination="org.freedesktop.UPower.Wakeups"
           send_interface="org.freedesktop.DBus.Properties"/>

    <allow send_destination="org.freedesktop.UPower"
           send_interface="org.freedesktop.UPower"/>
    <allow send_destination="org.freedesktop.UPower"
           send_interface="org.freedesktop.UPower.Device"/>
    <deny  send_destination="org.freedesktop.UPower"
           send_interface="org.freedesktop.UPower.KbdBacklight"/>
    <allow send_destination="org.freedesktop.UPower"
	   send_interface="org.freedesktop.UPower.Wakeups"/>
  </policy>
</busconfig>

```