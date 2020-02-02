<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Drivers](#Drivers)
*   [3 Screen Brightness](#Screen_Brightness)
*   [4 Keyboard Backlight](#Keyboard_Backlight)
*   [5 Palm Detection](#Palm_Detection)
*   [6 X11](#X11)
*   [7 Suspend/Resume](#Suspend/Resume)

## Installation

Installation was uneventful. This particular laptop does use Coreboot, but it was otherwise a normal EFI installation.

One may consider mounting their boot partition to /boot/efi instead of /boot, since [System76's firmware update tool hard-codes /boot/efi as the mount point](https://github.com/pop-os/system76-firmware/blob/dde2142ccfc6aeed90873d639b38049303385967/daemon/src/main.rs#L29-L30).

## Drivers

Driver support for the System76 Darter Pro 6 should be [included the kernel as of Linux 5.5](https://old.reddit.com/r/System76/comments/ev4jry/archlinux_on_the_system76_darter_pro/fftl66v/). For older kernels, there are various drivers in the AUR.

Otherwise, the [system76-firmware-daemon](https://aur.archlinux.org/packages/system76-firmware-daemon/) (or [system76-firmware-daemon-git](https://aur.archlinux.org/packages/system76-firmware-daemon-git/)) package provides the `system76-firmware-cli` tool, which can be used to schedule firmware updates.

## Screen Brightness

Works out of the box with the `xorg-xbacklight` package.

## Keyboard Backlight

The keyboard backlight can be controlled programmatically via `/sys` entries. Specifically,

```
$ sudo sh -c "echo 255 > /sys/class/leds/system76_acpi::kbd_backlight/brightness"

```

will increase the brightness to its maximum, and

```
$ sudo sh -c "echo FFA500 > /sys/class/leds/system76_acpi::kbd_backlight/color"

```

will set the color of the backlight via a 6-digit RGB hex code.

## Palm Detection

If the touchpad is not sensitive enough to detect your palm, then it is possible to reduce the palm pressure detection threshold using libinput's quirks. The first step is to [follow the instructions for debugging touchpad pressure](https://wayland.freedesktop.org/libinput/doc/latest/touchpad-pressure-debugging.html) (you'll need the `python-pyudev` and `python-libevdev` packages installed). Once you run the program, you’ll be able to experiment with different ways to touch the touchpad and see which things are registered as clicks and which are registered as a palm.

Once you've found the ideal palm pressure threshold, you can make it persistent by creating a libinput quirks file at `/etc/libinput/local-overrides.quirks`. For example, the following decreases the threshold to `70`:

```
[Touchpad pressure override]
MatchUdevType=touchpad
MatchName=*SynPS/2 Synaptics TouchPad
MatchDMIModalias=dmi:*svnSystem76*pvrdarp6*
AttrPalmPressureThreshold=70

```

To confirm it is working correctly, run

```
$ libinput quirks list /dev/input/eventXX

```

where `XX` is the number of the event device. (It should be shown in the output of the `libinput measure touchpad-pressure` command that you ran above.) The output should look something like this, with no errors:

```
ModelSynapticsSerialTouchpad=1
AttrPalmPressureThreshold=70

```

At this point, you can reboot and the setting should be applied persistently.

## X11

If X11 doesn't start properly (e.g., screen artifacts or invisible windows), then you may need to disable DRI. This can be done via an X11 configuration file.

Drop the following into `/etc/X11/xorg.conf.d/20-intel.conf`:

```
Section "Device"
  Identifier "Intel Graphics"
  Driver "intel"

  Option "AccelMethod" "sna"
  Option "TearFree" "true"
  Option "DRI" "false"
EndSection

```

This was found to be necessary on Linux 5.4.

## Suspend/Resume

Occasionally, on Linux 5.4, it was found that the laptop would become unresponsive when resuming from sleep. After about 90 seconds, the laptop would unfreeze itself and resume normal operation. After profiling the kernel with [suspendresume](https://github.com/01org/suspendresume), it was found that the culprit was the thunderbolt port. Namely, this error message was found in `dmesg`:

```
[  803.725685] thunderbolt 0000:03:00.0: failed to send driver ready to ICM

```

One approach to fix this is to disable thunderbolt support on suspend and then re-enable it on resume. This can be done via a systemd hook script.

Drop the following into `/usr/lib/systemd/system-sleep/system76-darter-hook-sleep` and make it executable:

```
#!/bin/sh

# This is a systemd hook script that is run whenever
# suspend/resume takes place. It should be symlinked into
# /usr/lib/systemd/system-sleep.

# $1 is 'pre' (going to sleep) or 'post' (waking up)
# $2 is 'suspend', 'hibernate' or 'hybrid-sleep'
case "$1/$2" in
  pre/*)
    if lsmod | grep -q thunderbolt; then
      rmmod thunderbolt
    fi
    ;;
  post/*)
    modprobe thunderbolt
    ;;
esac

```

Alternatively, System76 support [suggested disabling the corresponding PCI device on suspend and then reloading it on resume.](https://github.com/pop-os/system76-driver/blob/354d396bd7d37e591e5ed204b566c2d0c3f0dc3d/system76-thunderbolt-reload#L1) Adapting their `Pop!_OS` fix for Archlinux, the above file might look like this instead:

```
#!/bin/sh

# This is a systemd hook script that is run whenever
# suspend/resume takes place. It should be symlinked into
# /usr/lib/systemd/system-sleep.

# $1 is 'pre' (going to sleep) or 'post' (waking up)
# $2 is 'suspend', 'hibernate' or 'hybrid-sleep'
case "$1/$2" in
  pre/*)
    echo 1 > '/sys/devices/pci0000:00/0000:00:1c.0/remove'
    ;;
  post/*)
    echo 1 > '/sys/devices/pci0000:00/pci_bus/0000:00/bus_rescan'
    ;;
esac

```