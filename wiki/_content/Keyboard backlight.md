# Keyboard backlight

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Asus

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Keyboard_backlight&oldid=365410](https://wiki.archlinux.org/index.php?title=Keyboard_backlight&oldid=365410)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Keyboards](/index.php/Category:Keyboards "Category:Keyboards")