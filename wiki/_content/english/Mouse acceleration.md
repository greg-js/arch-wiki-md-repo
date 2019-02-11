Related articles

*   [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons")
*   [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate")

Setting the mouse acceleration depends on the windowing protocol you are using: either [Xorg](/index.php/Xorg "Xorg") or [Wayland](/index.php/Wayland "Wayland").

*   On [Xorg](/index.php/Xorg "Xorg"), there are several ways of setting mouse acceleration

*   by editing Xorg configuration files
*   [xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset) and [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) which provide *xset* and *xinput* respectively
*   and configuration interfaces common in [desktop environments](/index.php/Desktop_environments "Desktop environments").

*   If you are using [Wayland](/index.php/Wayland "Wayland"), the events are controlled via [libinput](/index.php/Libinput "Libinput"). It is the compositor's job to expose the settings brought by libinput. There is currently no standard way to change settings across compositors.[[1]](https://www.reddit.com/r/gnome/comments/3upay2/wayland_where_are_the_mouse_acceleration_options/)
*   [GNOME](/index.php/GNOME "GNOME") manages mouse acceleration by itself. A choice between "adaptive" and "flat" profiles can be chosen by installing [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor) and editing the value in org/gnome/desktop/peripherals/mouse/acceleration-profile. Alternatively, [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) can also be used to edit the org/gnome/desktop/peripherals/mouse/acceleration-profile.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Mouse acceleration with libinput](#Mouse_acceleration_with_libinput)
    *   [1.1 Changing the acceleration](#Changing_the_acceleration)
    *   [1.2 Persistent configuration](#Persistent_configuration)
*   [2 Setting mouse acceleration](#Setting_mouse_acceleration)
    *   [2.1 In Xorg configuration](#In_Xorg_configuration)
    *   [2.2 Using xset](#Using_xset)
    *   [2.3 Using xinput](#Using_xinput)
    *   [2.4 Configuration example](#Configuration_example)
*   [3 Disabling mouse acceleration](#Disabling_mouse_acceleration)
    *   [3.1 with libinput](#with_libinput)

## Mouse acceleration with libinput

When using the adaptive pointer acceleration profile, [libinput](/index.php/Libinput "Libinput") calculates the mouse acceleration depending on the DPI and the parameter `Acceleration Speed` [[2]](https://wayland.freedesktop.org/libinput/doc/latest/pointer-acceleration.html). libinput relies on the resolution reported by [evdev](/index.php/Evdev "Evdev") [[3]](https://wayland.freedesktop.org/libinput/doc/latest/motion_normalization.html). Feedback settings set with `xset m` are effectively ignored. When using the flat pointer acceleration profile, the acceleration factor is constant regardless of the velocity of the pointer. This provides 1:1 movement between the device and the pointer on-screen.

### Changing the acceleration

Find the id of your device with `xinput list` and set the acceleration speed with the following command. Note that the acceleration speed has to be in the range of [-1,1]. Check [this plot](https://wayland.freedesktop.org/libinput/doc/latest/pointer-acceleration.html#ptraccel-linear) to see the impact of different acceleration speed values.

```
$ xinput --set-prop <device id> 'libinput Accel Speed' <acceleration factor>

```

Confirm your changes with the following:

```
$ xinput --list-props <device id>

```

### Persistent configuration

libinput does not store configuration options, it is up to the caller to manage these. Under Wayland configuration is restored by the desktop environment. Under X [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) reads the xorg config files and applies the options [[4]](https://wayland.freedesktop.org/libinput/doc/latest/faq.html#faq_config_options). To make changes persistent under X create a file like this:

 `/etc/X11/xorg.conf.d/99-libinput-custom-config.conf` 
```
Section "InputClass"
  Identifier "<something to identify this snippet>"
  MatchDriver "libinput"
  MatchProduct "<substring of the device name>"
  Option "AccelSpeed" "<e.g. 0.3>"
EndSection

```

For further options see [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4).

## Setting mouse acceleration

### In Xorg configuration

See [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5) for details.

Examples:

 `/etc/X11/xorg.conf.d/50-mouse-acceleration.conf` 
```
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
# set the following to 1 1 0 respectively to disable acceleration.
	Option "AccelerationNumerator" "2"
	Option "AccelerationDenominator" "1"
	Option "AccelerationThreshold" "4"
EndSection
```
 `/etc/X11/xorg.conf.d/50-mouse-deceleration.conf` 
```
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
# some curved deceleration
#	Option "AdaptiveDeceleration" "2"
# linear deceleration (mouse speed reduction)
	Option "ConstantDeceleration" "2"
EndSection
```

You can also assign settings to specific hardware by using "MatchProduct", "MatchVendor" and other matches inside class sections. Run `lsusb` to find out the product name and vendor to match:

```
$ lsusb -v | grep -e idProduct -e idVendor

```

If you are unable to identify your device, try running `xinput list`. Some devices the use Logitech Unifying Recceiver share the same USB connection therefore, the mouse don't appear using `lsusb`

### Using xset

**Note:** xset does not use libinput.

To get the current values, use:

```
$ xset q | grep -A 1 Pointer

```

To set new values, type:

```
$ xset m *acceleration* *threshold*

```

where *acceleration* defines how many times faster the cursor will move than the default speed. *threshold* is the velocity required for acceleration to become effective, usually measured in device units per 10ms. *acceleration* can be a fraction, so if you want to slow down the mouse you can use 1/2, 1/3, 1/4, ... if you want to make it faster you can use 2/1, 3/1, 4/1, ...

*Threshold* defines the point at which acceleration should occur in pixels per 10 ms. If threshold is zero, e.g. if you use:

```
$ xset m 3/2 0

```

as suggested in the man page, then acceleration is treated as "the exponent of a more natural and continuous formula."

To get the default settings back:

```
$ xset m default

```

For more info see [xset(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xset.1).

Commands may be stored in [Xinitrc](/index.php/Xinitrc "Xinitrc") or [Xprofile](/index.php/Xprofile "Xprofile"). Alternatively, create a [Desktop entry](/index.php/Desktop_entry "Desktop entry") in `.config/autostart`:

```
[Desktop Entry]
Name=Disable mouse acceleration
Exec=xset m 0 0
Type=Application

```

This technique may be more desirable than employing the xorg configuration technique described above; latter may interfere with setting mouse speed in a display manager.

### Using xinput

First, get a list of devices plugged in (ignore any virtual pointers):

```
$ xinput list

```

Take note of the ID. You may also use the full name in commands if the ID is prone to changing.

Get a list of available properties and their current values available for modification with

```
$ xinput list-props 9

```

where `9` is the ID of the device you wish to use. Or

```
$ xinput list-props *mouse brand*

```

where *mouse brand* is the name of your mouse given by `$ xinput list`

Example, changing the property of `Constant Deceleration` to 2:

 `$ xinput list-props 9` 
```
Device '*mouse brand*':
       Device Enabled (121):   1
       Device Accel Profile (240):     0
       Device Accel Constant Deceleration (241):       1.000000
       Device Accel Adaptive Deceleration (243):       1.000000
       Device Accel Velocity Scaling (244):    10.000000

```

```
$ xinput --set-prop '*mouse brand*' 'Device Accel Constant Deceleration' 2

```

To make it permanent, edit xorg configuration (see above) or add commands to [xprofile](/index.php/Xprofile "Xprofile"). The latter won't affect speed in a [Display manager](/index.php/Display_manager "Display manager").

### Configuration example

You may need to resort to using more than one method to achieve your desired mouse settings. Here's what I did to configure a generic optical mouse: First, slow down the default movement speed 3 times so that it's more precise.

```
$ xinput --set-prop 9 'Device Accel Constant Deceleration' 3 &

```

Then, enable acceleration and make it 3 times faster after moving past 6 units.

```
$ xset mouse 3 6 &

```

If you are satisfied of the results, store the preceding commands in `~/.xinitrc`.

## Disabling mouse acceleration

Mouse acceleration has changed dramatically in recent X server versions; using `xset` to disable acceleration doesn't work as it used to and is not recommended anymore. Recent changes on `PointerAcceleration` can be read [here](http://xorg.freedesktop.org/wiki/Development/Documentation/PointerAcceleration#Introduction).

Disabling the mouse acceleration means that a linear function will be used to map from physical to virtual mouse movements. The mouse speed setting controls the inclination of this linear function.

To completely disable any sort of acceleration/deceleration, create the following file:

 `/etc/X11/xorg.conf.d/50-mouse-acceleration.conf` 
```
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
	Option "AccelerationProfile" "-1"
	Option "AccelerationScheme" "none"
	Option "AccelSpeed" "-1"
EndSection
```

and restart X.

### with libinput

Alternatively, since [libinput](https://www.archlinux.org/packages/?name=libinput)-1.1.0-1 and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)-0.15.0-1 you can use a flat acceleration profile. To enable it create the following file:

 `/etc/X11/xorg.conf.d/50-mouse-acceleration.conf` 
```
Section "InputClass"
	Identifier "My Mouse"
	Driver "libinput"
	MatchIsPointer "yes"
	Option "AccelProfile" "flat"
	Option "AccelSpeed" "0"
EndSection
```

and restart X.

Another option is this command:

```
$ xinput --set-prop <device id> 'libinput Accel Profile Enabled' 0, 1

```

Which doesn't need an X restart, but isn't persistent. Although it can be set up to run automatically with [Autostarting](/index.php/Autostarting "Autostarting").

To confirm that acceleration has been disabled, enter the following:

```
$ xinput list-props {1..50} 2>/dev/null | fgrep 'libinput Accel Profile Enabled ('

```

The profile should read `0, 1`.