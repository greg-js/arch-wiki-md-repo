| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ? |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch (mousedev) |
| Webcam | Working | ? |
| USB-C / Thunderbolt 3 | Working | ? |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Not/Working | ? |

Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")
*   [Dell XPS 13 2-in-1 (7390)](/index.php/Dell_XPS_13_2-in-1_(7390) "Dell XPS 13 2-in-1 (7390)")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Video](#Video)
*   [2 Battery](#Battery)
*   [3 Function/Multimedia Keys](#Function/Multimedia_Keys)
    *   [3.1 Volume keys](#Volume_keys)
*   [4 References](#References)

## Video

At the moment it is [not recommended](https://old.reddit.com/r/archlinux/comments/e30f09/complications_when_setting_up_arch_on_the_new/) to use [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel).

Install [acpilight](https://www.archlinux.org/packages/?name=acpilight) to set the display backlight with xbacklight. Add the following udev rule and your user to the `video` group:

 `/etc/udev/rules.d/90-backlight.rules` 
```
SUBSYSTEM=="backlight", ACTION=="add", \
  RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness", \
  RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"

```

It might be necessary to supply the `acpi_backlight=vendor` kernel parameter, see [backlight](/index.php/Backlight "Backlight").

## Battery

It is possible to set the start and stop charging thresholds similar to [tlp](/index.php/Tlp "Tlp") for ThinkPads using [dell-command-configure](https://aur.archlinux.org/packages/dell-command-configure/).

Example:

```
$ sudo /opt/dell/dcc/cctk --PrimaryBattChargeCfg=custom:75-80
PrimaryBattChargeCfg=Custom:75-80

```

To reset the thresholds at reboot simply add a [cronjob](/index.php/Cron "Cron"):

```
@reboot /opt/dell/dcc/cctk --PrimaryBattChargeCfg=custom:50-80

```

## Function/Multimedia Keys

| Function Key | Status | Description | Key |
| Fn + F1 | Working | Mute audio | `XF86AudioMute` |
| Fn + F2 | Working | Decrease volume | `XF86AudioLowerVolume` |
| Fn + F3 | Working | Increase volume | `XF86AudioRaiseVolume` |
| Fn + F4 | Working | Play previous track/chapter | `XF86AudioPrev` |
| Fn + F5 | Working | Play/Pause | `XF86AudioPlay` |
| Fn + F6 | Working | Play next track/chapter | `XF86AudioNext` |
| Fn + F7 | Working | Task view |
| Fn + F8 | ? | Switch to external display |
| Fn + F9 | Working | Search |
| Fn + F10 | Working | Toggle keyboard backlight |
| Fn + F11 | ? | Print screen |
| Fn + F12 | ? | Insert |
| Fn + Home | Working | Toggle wireless |
| Fn + End | Working | Sleep |
| Fn + Up | Not working | Increase brightness |
| Fn + Down | Not working | Decrease rightness |

### Volume keys

Use [xbindkeys](/index.php/Xbindkeys "Xbindkeys") to map the volume buttons.

 `~/.xbindkeysrc` 
```
# Increase volume
"pactl set-sink-volume @DEFAULT_SINK@ +1000"
   XF86AudioRaiseVolume

# Decrease volume
"pactl set-sink-volume @DEFAULT_SINK@ -1000"
   XF86AudioLowerVolume

# Mute volume
"pactl set-sink-mute @DEFAULT_SINK@ toggle"
   XF86AudioMute

```

## References

*   [XPS 13 7390 Setup and Specifications](https://www.dell.com/support/manuals/se/sv/sebsdt1/xps-13-7390-laptop/xps-7390-setup-and-specifications/konfigurera-din-xps-13-7390?guid=guid-f60953a1-9d6d-405f-a81c-42ba9cdfc409&lang=en-us)