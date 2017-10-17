## Any vendor

You can control your computer keyboard backlight via the [D-Bus](/index.php/D-Bus "D-Bus") interface. The benefits of using it are that no modification to device files is required and it is vendor agnostic.

Here is an example implementation in [Python](/index.php/Python "Python") 3. [Install](/index.php/Install "Install") the [upower](https://www.archlinux.org/packages/?name=upower) package then place the following script in `/usr/local/bin/` and make it executable. You can then map your keyboard shortcuts to run `/usr/local/bin/kb-light.py +` and `/usr/local/bin/kb-light.py -` to increase and decrease your keyboard backlight level.

 `/usr/local/bin/kb-light.py` 
```
#!/usr/bin/env python3
# coding: utf-8

from sys import argv
import dbus

def kb_light_set(delta):
    bus = dbus.SystemBus()
    kbd_backlight_proxy = bus.get_object('org.freedesktop.UPower', '/org/freedesktop/UPower/KbdBacklight')
    kbd_backlight = dbus.Interface(kbd_backlight_proxy, 'org.freedesktop.UPower.KbdBacklight')

    current = kbd_backlight.GetBrightness()
    maximum = kbd_backlight.GetMaxBrightness()
    new = max(0, current + delta)

    if 0 <= new <= maximum:
        current = new
        kbd_backlight.SetBrightness(current)

    # Return current backlight level percentage
    return 100 * current / maximum

if __name__ == '__main__':
    if len(argv[1:]) == 1:
        if argv[1] == "--up" or argv[1] == "+":
            # ./kb-light.py (+|--up) to increment
            print(kb_light_set(1))
        elif argv[1] == "--down" or argv[1] == "-":
            # ./kb-light.py (-|--down) to decrement
            print(kb_light_set(-1))
        else:
            print("Unknown argument:", argv[1])
    else:
        print("Script takes exactly one argument.", len(argv[1:]), "arguments provided.")
```

## Asus

**Warning:** The following way is not recommended. It provides world-writeable permissions to the keyboard backlight device file meaning that any and every user can control it.

The keyboard backlight file is usually locked out from editing. To unlock this file at bootup, you will need to create a [systemd](/index.php/Systemd "Systemd") service.

 `/usr/lib/systemd/system/asus-kbd-backlight.service` 
```
[Unit]
Description=Asus Keyboard Backlight
Wants=systemd-backlight@leds:asus::kbd_backlight.service
After=systemd-backlight@leds:asus::kbd_backlight.service

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/bin/chmod 666 /sys/class/leds/asus::kbd_backlight/brightness

[Install]
WantedBy=multi-user.target
```

You are now able to use a keyboard backlight changer script. For an example, see [ASUS G55VW#keyboard backlight script](/index.php/ASUS_G55VW#keyboard_backlight_script "ASUS G55VW").

For an example of how you might set up a tiny daemon (running as root) that edits these files, hook it up to [dbus](/index.php/Dbus "Dbus"), and map the keyboard brightness keys to [dbus](/index.php/Dbus "Dbus") method calls, see [[1]](https://github.com/GambolingPangolin/KbdBacklight).