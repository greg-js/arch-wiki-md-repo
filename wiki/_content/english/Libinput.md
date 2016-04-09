From the [libinput](http://wayland.freedesktop.org/libinput/doc/latest/index.html) project:

	libinput is a library that handles input devices for display servers and other applications that need to directly deal with input devices.

	libinput originates from weston, the [Wayland](/index.php/Wayland "Wayland") reference compositor.

The driver supports most regular [Xorg#Input devices](/index.php/Xorg#Input_devices "Xorg"). Particularly notable is the project's goal to provide advanced support for touch (multitouch and gesture) features of touchpads and touchscreens. See the [project documentation](http://wayland.freedesktop.org/libinput/doc/latest/pages.html) for more information.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Touchpad configuration](#Touchpad_configuration)
    *   [3.2 Mouse button re-mapping](#Mouse_button_re-mapping)
    *   [3.3 Debugging](#Debugging)
    *   [3.4 Multitouch events](#Multitouch_events)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package. If it does not pull the [libinput](https://www.archlinux.org/packages/?name=libinput) driver, it will already be installed as a dependency of a graphical environment. You may also want to install [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) to be able to change settings at runtime.

## Configuration

For [Xorg](/index.php/Xorg "Xorg"), a default configuration file is installed in `/usr/share/X11/xorg.conf.d/90-libinput.conf`. No extra configuration is necessary for it to autodetect keyboards, touchpads, trackpointers and supported touchscreens.

First, execute:

```
# libinput-list-devices 

```

It will output the devices on the system and their respective features supported by libinput.

After a [restart](/index.php/Restart "Restart") of the graphical environment, the devices should be managed by libinput with default configuration, if no other drivers are configured to take precedence.

See the libinput(4) manual page for general options to set. The *xinput* tool is used to view or change options available for a particular device at runtime. For example:

```
$ xinput list-props *device-number* 

```

to view and

```
$ xinput set-prop *device-number* *option-number* *setting* 

```

to change a setting.

See [Xorg#Using .conf files](/index.php/Xorg#Using_.conf_files "Xorg") for permanent option settings. [Logitech Marble Mouse#Using libinput](/index.php/Logitech_Marble_Mouse#Using_libinput "Logitech Marble Mouse") and [#Touchpad configuration](#Touchpad_configuration) illustrate examples.

Alternative drivers for [Xorg#Input devices](/index.php/Xorg#Input_devices "Xorg") can generally be installed in parallel. If you intend to switch driver for a device to use libinput, ensure no legacy configuration files `/etc/X11/xorg.conf.d/` for other drivers take precedence. One way to check which devices are managed by libinput is the *xorg* logfile. For example, the following:

 `$ grep -e "Using input driver 'libinput'" ~/.local/share/xorg/Xorg.0.log` 
```
[    28.799] (II) Using input driver 'libinput' for 'Power Button'
[    28.847] (II) Using input driver 'libinput' for 'Video Bus'
[    28.853] (II) Using input driver 'libinput' for 'Power Button'
[    28.860] (II) Using input driver 'libinput' for 'Sleep Button'
[    28.872] (II) Using input driver 'libinput' for 'AT Translated Set 2 keyboard'
[    28.878] (II) Using input driver 'libinput' for 'SynPS/2 Synaptics TouchPad'
[    28.886] (II) Using input driver 'libinput' for 'TPPS/2 IBM TrackPoint'
[    28.895] (II) Using input driver 'libinput' for 'ThinkPad Extra Buttons'
```

is a notebok without any configuration files in `/etc/X11/xorg.conf.d/`, i.e. devices are autodetected.

Of course you can elect to use an alternative driver for one device and libinput for others. A number of factors may influence which driver to use. For example, in comparison to [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") the libinput driver has fewer options to customize touchpad behaviour to one's own taste, but far more programmatic logic to process multitouch events (e.g. palm detection as well). Hence, it makes sense to try the alternative, if you are experiencing problems on your hardware with one driver or the other.

## Tips and tricks

### Touchpad configuration

Tapping may be disabled by default. To enable it, add a configuration file:

 `/etc/X11/xorg.conf.d/30-touchpad.conf` 
```
Section "InputClass"
        Identifier "MyTouchpad"
        MatchIsTouchpad "on"
        Driver "libinput"
        Option "Tapping" "on"
EndSection
```

### Mouse button re-mapping

For some devices it is desirable to change the button mapping. A common example is the use of a thumb button instead of the middle button (used in X11 for pasting) on mice where the middle button is part of the mouse wheel. You can query the current button mapping via:

```
$ xinput get-button-map *device*

```

You can freely permutate the button numbers and write them back. Example:

```
$ xinput set-button-map *device* 1 6 3 4 5 0 7

```

In this example, we mapped button 6 to be the middle button and disabled the original middle button by assigning it to button 0.

**Tip:** You can use *xev* (from the [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) package) to find out which physical button is currently mapped to which ID.

Some devices occur several times under the same device name, with a different amount of buttons exposed. The following shell script is an example for reliably changing the button mapping for a Logitech Revolution MX mouse:

 `remap-revolution.sh` 
```
#!/usr/bin/bash
for i in `xinput list | grep "Logitech USB Receiver" | perl -n -e'/id=(\d+)/ && print "$1
"'`
	do if xinput get-button-map "$i" 2>/dev/null| grep -q 20; then
		xinput set-button-map "$i" 1 17 3 4 5 8 7 6 9 10 11 12 13 14 15 16 2 18 19 20
	fi
done
```

### Debugging

Some inputs require kernel support. The tool *evemu-describe* from the [evemu](https://www.archlinux.org/packages/?name=evemu) package can be used to check:

Compare the output of [software supported input trackpad driver](http://ix.io/m6b) with [a supported trackpad](https://github.com/whot/evemu-devices/blob/master/touchpads/SynPS2%20Synaptics%20TouchPad-with-scrollbuttons.events). i.e. a couple of ABS_ axes, a couple of ABS_MT axes and no REL_X/Y axis. For a clickpad the `INPUT_PROP_BUTTONPAD` property should also be set, if it is supported.

### Multitouch events

While the libinput driver already contains logic to process advanced multitouch events like swipe and pinch, the [Desktop environment](/index.php/Desktop_environment "Desktop environment") or [Window manager](/index.php/Window_manager "Window manager") might not have implemented actions for all of them yet.

For [EWMH](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints "w:Extended Window Manager Hints") (see also [wm-spec](https://www.freedesktop.org/wiki/Specifications/wm-spec/)) compliant window managers, the [libinput-gestures](https://github.com/bulletmark/libinput-gestures) utility can be used meanwhile.

The utility can be installed/configured/uninstalled as a user, If its [python](https://www.archlinux.org/packages/?name=python) and [xdotool](https://www.archlinux.org/packages/?name=xdotool) dependencies are installed on the system. It enables to define custom swipe and pinch actions via a `~/.config/libinput-events.conf` file. An [AUR](/index.php/AUR "AUR") package is not available yet.[[2]](https://github.com/bulletmark/libinput-gestures/issues/6)

## See also

*   [FOSDEM 2015 - libinput](https://archive.fosdem.org/2015/schedule/event/libinput/attachments/slides/591/export/events/attachments/libinput/slides/591/libinput_xorg.pdf) - Hans de Goede on goals and plans of the project
*   [Peter Hutterer's Blog](http://who-t.blogspot.com.au/) - numerous posts on libinput from one of the project's hackers