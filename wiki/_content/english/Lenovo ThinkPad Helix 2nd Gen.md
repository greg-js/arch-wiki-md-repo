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

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Suspend & Resume](#Suspend_&_Resume)
    *   [1.1 Enable suspend-to-idle (freeze/s2idle)](#Enable_suspend-to-idle_(freeze/s2idle))
    *   [1.2 Disable embedded-controller wake-ups](#Disable_embedded-controller_wake-ups)
    *   [1.3 Workaround for no wifi connection on resume](#Workaround_for_no_wifi_connection_on_resume)
*   [2 ACPI CPU load and Battery Power](#ACPI_CPU_load_and_Battery_Power)
*   [3 Sensors](#Sensors)
*   [4 Touch Screen](#Touch_Screen)
*   [5 Touch Pad and Pointing Stick](#Touch_Pad_and_Pointing_Stick)
*   [6 Graphics](#Graphics)
*   [7 Softare](#Softare)
    *   [7.1 Firefox](#Firefox)
*   [8 Unresolved Issues](#Unresolved_Issues)

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

### Workaround for no wifi connection on resume

The WiFi chip in this computer (Intel Wireless 7265) has a problem where it can stop re-connecting after waking from suspend. The system can no longer communicate with the card, so restarting NetworkManager (etc) is not sufficient to regain a connection, nor is unloading and reloading the `iwlwifi` module after resuming. A casual internet search reveals this to be a hardware problem that affects Windows users as well.

An effective workaround, however, is to unload the kernel modules before suspending and reloading them upon resuming. For example, using systemd:

 `/etc/systemd/system/suspend-unload-iwlwifi.service` 
```
[Unit]
Description=Unload iwlwifi before suspending
Before=suspend.target
StopWhenUnneeded=no

[Service]
type=oneshot
ExecStart=/usr/bin/bash -c "rmmod iwlmvm && rmmod iwlwifi"

[Install]
WantedBy=suspend.target
```
 `/etc/systemd/system/suspend-unload-iwlwifi.service` 
```
[Unit]
Description=Unload iwlwifi before suspending
Before=suspend.target
StopWhenUnneeded=no

[Service]
type=oneshot
ExecStart=/usr/bin/bash -c "lsmod iwlmvm iwlwifi"

[Install]
WantedBy=suspend.target
```

## ACPI CPU load and Battery Power

Many ACPI Interrupt - Events are triggered on older Kernels making CPU load up to 80% of one Kernel => Battery goes empty within 3 hours. With me this problem was fixed when upgrading to Kernel 5.1rc1\. Powertop estimates over 7 hours with a pro keyboard attached. Use tlp package for further improvements.

## Sensors

In order to use the sensors (particularly the accelerometer and the ambient light sensor) in [GNOME](/index.php/GNOME "GNOME"), you should install the [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) package. There is presumably a quirk with this sensor hardware. The effect is that `iio-sensor-proxy` loads too early, requiring the service to be restarted before the sensors can be read properly. To fix this, edit the systemd unit so that it starts after GDM (`After=gdm.service`; see [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd")).

If you are using [GNOME](/index.php/GNOME "GNOME"), a program called [tp-helix-orientation-lock](http://brandon.invergo.net/software/tp-helix-orientation-lock.html) enables the use of the "rotation lock" button on the Helix 2, as well as optionally automatically locking/unlocking the screen orientation when docking/undocking the tablet.

## Touch Screen

In order to enable multitouch, install [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) and [libwacom](https://www.archlinux.org/packages/?name=libwacom). By default, [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) handles multitouch, however it is limited to two-finger input. In order to allow true multitouch, you must disable this built-in support. Multitouch events will then be passed on to XServer. To test this, try running

```
$ xset "Wacom HID 501D Finger touch" Gesture off

```

To make it permanent, copy `/usr/share/X11/xorg.conf.d/70-wacom.conf` to `/etc/X11/xorg.conf.d/70-wacom.conf` and edit it so the input entries all contain `Option "Gesture" "Off"`.

## Touch Pad and Pointing Stick

After detaching and attaching a Pro Keyboard the mouse stops working in gnome. Probably there is a sync problem. Attempt to load psmouse with "proto=imps" option. To do that, add this line to your `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf`  `options psmouse proto=imps` 

You can test this before making it permanent by:

$ modprobe -r psmouse

$ modprobe psmouse proto=imps

## Graphics

Install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) for graphics acceleration.

## Softare

### Firefox

Touch Screen Scrolling can be activated by the ScrollAnywhere firefox Plugin

## Unresolved Issues

*   The fingerprint reader is apparently not supported by any driver.
*   The speakers make popping sounds.