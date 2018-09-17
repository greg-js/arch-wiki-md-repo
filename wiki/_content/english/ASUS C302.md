The [Asus C302](https://www.asus.com/uk/2-in-1-PCs/ASUS-Chromebook-Flip-C302CA/) ([also known as](https://www.reddit.com/r/chromeos/comments/7z6208/asus_c302ca_vs_asus_c302_any_differences/) Asus C302C and Asus C302CA) is a Chromebook, which can have Linux installed. Here are some pointers on the smooth running of Arch Linux.

## Contents

*   [1 Bootup](#Bootup)
*   [2 Kernel Modules](#Kernel_Modules)
*   [3 Screen](#Screen)
    *   [3.1 Vsync](#Vsync)
*   [4 Keyboard](#Keyboard)
    *   [4.1 Keyboard Backlight](#Keyboard_Backlight)
*   [5 Touchpad](#Touchpad)
*   [6 Mouse](#Mouse)
*   [7 Sound](#Sound)
    *   [7.1 Pulseaudio](#Pulseaudio)
*   [8 Coil Whine](#Coil_Whine)

# Bootup

In /etc/default/grub

```
GRUB_CMDLINE_LINUX_DEFAULT="acpi_osi=Linux intel_iommu=on,igfx_off"

```

*intel_iommu=on,igfx_off* is from [forum](https://bbs.archlinux.org/viewtopic.php?id=228604), to prevent the dmesg error:

```
[drm:intel_cpu_fifo_underrun_irq_handler [i915]] *ERROR* CPU pipe A FIFO underrun

```

The CPU is an Intel Core M3, so install [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode)

# Kernel Modules

In e.g. /etc/modprobe.d/skylake.conf

```
# Needed, for the nau8825 kernel sound modules to initialize
blacklist snd_hda_intel

```

```
options tpm_tis interrupts=0

```

# Screen

The screen is 12.5 inches diagonally. At 1920x1080 resolution, this is 176 DPI.

In ~/.xinitrc:

```
xrandr --fbmm 277x156

```

## Vsync

For proper vsync (including e.g. fullscreen Youtube in Firefox) in XFCE, install [xfwm4-git](https://aur.archlinux.org/packages/xfwm4-git) (which also requires libxpresent), and enable XFCE's compositor.

Proper vsync also requires [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), rather than modesetting.

In /etc/X11/xorg.conf.d/20-intel.conf

```
Section "Device"
    Identifier "Intel Graphics"
    Driver "intel"
EndSection

```

# Keyboard

To use the top row of Chromebook keys as useful keys in xorg, use e.g.:

In ~/.Xmodmap

```
keycode   9 = Escape NoSymbol Escape
keycode  22 = BackSpace BackSpace BackSpace BackSpace Delete NoSymbol Delete
keycode  37 = Control_L NoSymbol Control_L
keycode  50 = Shift_L NoSymbol Shift_L
keycode  66 = Caps_Lock NoSymbol Caps_Lock
keycode  67 = Home F1 Home F1 F1 F1 XF86Switch_VT_1
keycode  68 = End F2 End F2 F2 F2 XF86Switch_VT_2
keycode  69 = Prior F3 Prior F3 F3 F3 XF86Switch_VT_3
keycode  70 = Next F4 Next F4 F4 F4 XF86Switch_VT_4
keycode  71 = Delete F5 Delete F5 F5 F5 XF86Switch_VT_5
keycode  72 = XF86MonBrightnessDown F6 XF86MonBrightnessDown F6 F6 F6 XF86Switch_VT_6
keycode  73 = XF86MonBrightnessUp F7 XF86MonBrightnessUp F7 F7 F7 XF86Switch_VT_7
keycode  74 = XF86AudioMute F8 XF86AudioMute F8 F8 F8 XF86Switch_VT_8
keycode  75 = XF86AudioLowerVolume F9 XF86AudioLowerVolume F9 F9 F9 XF86Switch_VT_9
keycode  76 = XF86AudioRaiseVolume F10 XF86AudioRaiseVolume F10 F10 F10 XF86Switch_VT_10
keycode 111 = Up Up Up Up Prior Prior
keycode 112 = Prior NoSymbol Prior
keycode 113 = Left Left Left Left Home Home
keycode 114 = Right Right Right Right End End
keycode 115 = End NoSymbol End
keycode 116 = Down Down Down Down Next Next
keycode 117 = Next NoSymbol Next
keycode 118 = Insert NoSymbol Insert
keycode 119 = Delete NoSymbol Delete
keycode 121 = XF86AudioMute NoSymbol XF86AudioMute
keycode 122 = XF86AudioLowerVolume NoSymbol XF86AudioLowerVolume
keycode 123 = XF86AudioRaiseVolume NoSymbol XF86AudioRaiseVolume
keycode 124 = XF86PowerOff NoSymbol XF86PowerOff
keycode 167 = XF86Forward NoSymbol XF86Forward
keycode 182 = XF86Close NoSymbol XF86Close

```

(This list can be pruned.)

And then call it in ~/.xinitrc:

```
xmodmap ~/.Xmodmap

```

## Keyboard Backlight

To be able to change the keyboard backlight brightness as a normal user, run as root:

```
b="/sys/devices/platform/GOOG0002:00/leds/chromeos::kbd_backlight/brightness"
chgrp users "$b" &&
chmod 660 "$b" &&
echo 6 > "$b"

```

It is a value between 0 (off) and 100 (full brightness). The default on ChromeOS is 25\. 6 is a reasonable lower value.

ChromeOS is able to disable the keyboard backlight, when the keyboard is not being used - that functionality does not appear to be available in the Linux kernel.

# Touchpad

See [TrackPoint](/index.php/TrackPoint "TrackPoint") - the pressure sensitivity can be changed:

In /etc/udev/hwdb.d/99-touchpad-pressure.hwdb

```
libinput:name:*Elan Touchpad:dmi:*svnGOOGLE:*pnCave*
 LIBINPUT_ATTR_PRESSURE_RANGE=1:41

```

Current [libinput bug report](https://gitlab.freedesktop.org/libinput/libinput/issues/140).

# Mouse

Due to the limited amount of USB ports, a Bluetooth mouse is a good option. The Logitech M590 mouse works great.

Run "bluetoothctl power on &" at startup, e.g. in ~/.xinitrc

In e.g. /etc/X11/xorg.conf.d/99-mouse.conf

```
Section "InputClass"
    Identifier "Logitech M590"
    MatchIsPointer "on"
    MatchDevicePath "/dev/input/event*"
    Driver "libinput"
    Option "AccelProfile" "flat"
EndSection

```

Then, the "speed" of the mouse can be set using the XFCE GUI, in "Settings - Mouse", setting the "acceleration" to e.g. 2.0

# Sound

Sound is a [work in-progress](https://github.com/GalliumOS/galliumos-distro/issues/379). Sound is reliable when using headphones only.

Save the audio firmware as /lib/firmware/9d70-CORE-COREBOOT-0-tplg.bin (filesize 23120 bytes).

To set audio to a sensible level, run in ~/.xinitrc:

```
amixer -q -c0 sset Headphone 70% &

```

## Pulseaudio

To prevent audio "clicks", comment out "load-module module-suspend-on-idle" in /etc/pulse/default.pa and /etc/pulse/system.pa

# Coil Whine

There is occasional [coil whine](https://www.notebookcheck.net/FAQ-Coil-Whine.225152.0.html), with no apparent method to reduce/eliminate it.