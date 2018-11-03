<caption>Hardware Information</caption>
| Form Factor | Tablet/Ultrabook Convertible (detachable keyboard dock) |
| Display | 11.6" 1920x1080 LCD with Capacitive and Pen Digitizers |
| CPU | Intel Core M-5Y10c or M-5Y71 |
| RAM | 4GiB or 8GiB DDR3L RAM |
| Storage | 128/256GB M.2 SSD |
| WiFi | Intel Dual Band Wireless-AC 7265 with Bluetooth 4.0 |
| Bluetooth | Intel Dual Band Wireless-AC 7265 |
| Camera | 5MP Rear and 2MP Front (also USB) |

This hardware is substantially different from the [Lenovo ThinkPad Helix 1st Gen](/index.php/Lenovo_ThinkPad_Helix "Lenovo ThinkPad Helix") and thus the solutions outlined there are not helpful. Note: the following was tested with the standard ThinkPad Ultrabook keyboard, not the Pro one.

## Contents

*   [1 Suspend & Resume](#Suspend_.26_Resume)
    *   [1.1 Enable suspend-to-idle (freeze/s2idle)](#Enable_suspend-to-idle_.28freeze.2Fs2idle.29)
    *   [1.2 Disable embedded-controller wake-ups](#Disable_embedded-controller_wake-ups)
*   [2 Sensors](#Sensors)
*   [3 Touch Screen](#Touch_Screen)
*   [4 Graphics](#Graphics)
*   [5 Unresolved Issues](#Unresolved_Issues)

## Suspend & Resume

### Enable suspend-to-idle (freeze/s2idle)

This device does not support suspend-to-RAM. It only supports suspend-to-idle (aka "freeze" or "s2idle"). In order for this to work completely, you must update the BIOS to the latest version (1.99 works) using the disc image provided by Lenovo. If you do not do this, you may only be able to suspend-to-idle and resume while docked in the keyboard (detaching to tablet mode while suspended would prevent the device from resuming). With an updated BIOS, it appears the device can resume from suspend-to-idle under all conditions.

Older versions of the BIOS misreport the suspend capabilities, and thus the system will try to suspend to RAM. To verify this, run `cat /sys/power/mem_sleep`. If you see `mem` in the output, you are susceptible to this problem. If you are unable to update the BIOS, you can force the system to use suspend-to-idle. Simply create the file `/etc/systemd/sleep.conf` containing:

 `/etc/systemd/sleep.conf` 
```
[Sleep]
SuspendState=freeze
```

On the most recent BIOS versions, this isn't necessary, since `/sys/power/mem_sleeep` will only contain `s2idle` and thus any attempt to suspend in any manner will default to suspend-to-idle.

### Disable embedded-controller wake-ups

By default, s2idle will still exhibit a significant battery drain while suspended (the batteries will be dead within a few hours). It appears that the device suffers from embedded controller wake-ups. For a more reasonable drain while suspended (i.e. you can leave it suspended for days), you must set the `acpi.ec_no_wakeup=1` kernel parameter.

**Note:** If you set the `acpi.ec_no_wakeup=1` kernel parameter, the device will not be able to wake up after any lid events (attaching/detaching the tablet from the base). So, it's a trade-off: enable the parameter and enjoy proper suspend behavior as long as you don't remove the device from the base (e.g. to close it), or do not set the parameter and enjoy the ability to close and re-open the laptop but suffer wake-level battery drainage.

## Sensors

In order to use the sensors (particularly the accelerometer and the ambient light sensor) in [GNOME](/index.php/GNOME "GNOME"), you should install the [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) package. There is presumably a quirk with this sensor hardware. The effect is that `iio-sensor-proxy` loads too early, requiring the service to be restarted before the sensors can be read properly. To fix this, edit the systemd unit so that it starts after GDM (`After=gdm.service`; see [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd")).

If you are using [GNOME](/index.php/GNOME "GNOME"), a program called [tp-helix-orientation-lock](http://brandon.invergo.net/software/tp-helix-orientation-lock.html) enables the use of the "rotation lock" button on the Helix 2, as well as optionally automatically locking/unlocking the screen orientation when docking/undocking the tablet.

## Touch Screen

In order to enable multitouch, install [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) and [libwacom](https://www.archlinux.org/packages/?name=libwacom). By default, [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) handles multitouch, however it is limited to two-finger input. In order to allow true multitouch, you must disable this built-in support. Multitouch events will then be passed on to XServer. To test this, try running

```
$ xset "Wacom HID 501D Finger touch" Gesture off

```

To make it permanent, copy `/usr/share/X11/xorg.conf.d/70-wacom.conf` to `/etc/X11/xorg.conf.d/70-wacom.conf` and edit it so the input entries all contain `Option "Gesture" "Off"`.

## Graphics

Install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) for graphics acceleration.

## Unresolved Issues

*   The fingerprint reader is apparently not supported by any driver.
*   The speakers make popping sounds.