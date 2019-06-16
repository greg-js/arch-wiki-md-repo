[Wacom](https://en.wikipedia.org/wiki/Wacom_(company) does not officially support Linux. Linux support is provided by the [Linux Wacom Project](https://linuxwacom.github.io/). Supported devices are listed on the [Device IDs](https://github.com/linuxwacom/input-wacom/wiki/Device-IDs) page with a version number in the *input-wacom* column.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Permanent configuration](#Permanent_configuration)
    *   [2.2 Remapping buttons](#Remapping_buttons)
        *   [2.2.1 Mapping pad buttons to function keys](#Mapping_pad_buttons_to_function_keys)
        *   [2.2.2 The syntax](#The_syntax)
        *   [2.2.3 Some examples](#Some_examples)
        *   [2.2.4 Execute custom commands](#Execute_custom_commands)
    *   [2.3 Adjusting aspect ratios](#Adjusting_aspect_ratios)
        *   [2.3.1 Reducing the drawing area height](#Reducing_the_drawing_area_height)
        *   [2.3.2 Reducing the screen area width](#Reducing_the_screen_area_width)
    *   [2.4 LEDs](#LEDs)
    *   [2.5 TwinView setup](#TwinView_setup)
        *   [2.5.1 Temporary TwinView setup](#Temporary_TwinView_setup)
    *   [2.6 xrandr setup](#xrandr_setup)
    *   [2.7 Pressure curve](#Pressure_curve)
*   [3 Application-specific configuration](#Application-specific_configuration)
    *   [3.1 Blender](#Blender)
    *   [3.2 GIMP](#GIMP)
    *   [3.3 Inkscape](#Inkscape)
    *   [3.4 Krita](#Krita)
    *   [3.5 VirtualBox](#VirtualBox)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Unknown device_type](#Unknown_device_type)
    *   [4.2 Tablet recognized but xsetwacom and similar tools do not display it](#Tablet_recognized_but_xsetwacom_and_similar_tools_do_not_display_it)
    *   [4.3 Manual setup](#Manual_setup)
        *   [4.3.1 Dynamic with udev](#Dynamic_with_udev)
            *   [4.3.1.1 USB-devices](#USB-devices)
            *   [4.3.1.2 Serial devices](#Serial_devices)
        *   [4.3.2 Static setup](#Static_setup)
        *   [4.3.3 Xorg configuration](#Xorg_configuration)
    *   [4.4 Mouse Moving Erratically due to Proximity Sensor](#Mouse_Moving_Erratically_due_to_Proximity_Sensor)
*   [5 See also](#See_also)

## Installation

The Arch Linux [kernels](/index.php/Kernels "Kernels") include the [input-wacom](https://github.com/linuxwacom/input-wacom) driver.

Ensure your kernel recognizes your tablet. Connect your tablet via USB or [Bluetooth](/index.php/Bluetooth "Bluetooth"). It should show up in `dmesg | grep -i wacom` and be listed in `/proc/bus/input/devices` (and if you use USB in the `lsusb` output). If it does not, your only chance is that your tablet is supported by a more recent driver than the one in your kernel. In that case [install](/index.php/Install "Install") the [input-wacom-dkms](https://aur.archlinux.org/packages/input-wacom-dkms/) package.

[Install](/index.php/Install "Install") the [X](/index.php/X "X") driver, [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom), and restart X so the new [udev](/index.php/Udev "Udev") rules take effect.

The command `xsetwacom list devices` should now list some devices. If it does not, see [#Manual setup](#Manual_setup).

The [kcm-wacomtablet](https://www.archlinux.org/packages/?name=kcm-wacomtablet) package provides a [KDE](/index.php/KDE "KDE") graphical user interface for tablet configuration and supports tablet-specific profiles and hotplugging.

Support for the following Wacom tablets is provided via [tuhi-git](https://aur.archlinux.org/packages/tuhi-git/):

*   Bamboo Spark
*   Bamboo Slate
*   Intuos Pro Paper

Consult README for the details of initial configuration. For setups with more than one monitor you'll probably want to fix aspect ratio using `Coordinate Transformation Matrix` as described at [dual and multimonitor set up](https://github.com/linuxwacom/xf86-input-wacom/wiki/Dual-and-Multi-Monitor-Set-Up).

## Configuration

The Xorg driver can be temporarily configured with `xsetwacom`, see [xsetwacom(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xsetwacom.1). Changes are lost after X server restarts or replugging your tablet.

List the available devices:

 `$ xsetwacom list devices` 
```
Wacom Bamboo 16FG 4x5 Finger touch	id: 12	type: TOUCH
Wacom Bamboo 16FG 4x5 Finger pad	id: 13	type: PAD       
Wacom Bamboo 16FG 4x5 Pen stylus	id: 17	type: STYLUS    
Wacom Bamboo 16FG 4x5 Pen eraser	id: 18	type: ERASER

```

For the `get` and `set` commands, devices can be specified by name or id. Scripts should use names because ids can change after X server restarts or replugging.

### Permanent configuration

**Note:** Because *xorg.conf* lacks options *xsetwacom* has and only lets you map buttons to mouse buttons, you may want to [autostart](/index.php/Autostart "Autostart") a script with *xsetwacom* commands instead of using *xorg.conf*.

Configuration can be made persistent in [xorg.conf](/index.php/Xorg.conf "Xorg.conf") and [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5).

You firstly need to find out your product names:

 `$ grep "Using input driver 'wacom'" /var/log/Xorg.0.log` 
```
[ 25059.351] (II) Using input driver 'wacom' for 'Wacom Intuos BT M Pen'
[ 25059.409] (II) Using input driver 'wacom' for 'Wacom Intuos BT M Pad'
[ 25059.428] (II) Using input driver 'wacom' for 'Wacom Intuos BT M Pen eraser'
[ 25059.429] (II) Using input driver 'wacom' for 'Wacom Intuos BT M Pen cursor'

```

For these product names the sections would be:

 `/etc/X11/xorg.conf.d/72-wacom-options.conf` 
```
Section "InputClass"
	Identifier "WACOM OPTIONS pen"
	MatchDriver "wacom"
	MatchProduct "Pen"
	NoMatchProduct "eraser"
	NoMatchProduct "cursor"
EndSection

Section "InputClass"
	Identifier "WACOM OPTIONS pad"
	MatchDriver "wacom"
	MatchProduct "Pad"
EndSection

Section "InputClass"
	Identifier "WACOM OPTIONS eraser"
	MatchDriver "wacom"
	MatchProduct "eraser"
EndSection

Section "InputClass"
	Identifier "WACOM OPTIONS cursor"
	MatchDriver "wacom"
	MatchProduct "cursor"
EndSection

```

*   The options described in [wacom(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wacom.4) can be added to sections.
*   The product name needs to contain the `MatchProduct` value in order for a section to match. Matching of parent devices requires negative matching.
*   The `Identifier` can be arbitrary and is printed into the Xorg log when the section matches. Giving your identifiers a common prefix lets you easily [grep](/index.php/Grep "Grep") for what sections were matched: `grep "WACOM OPT" /var/log/Xorg.0.log` 
*   Configuration changes require a X server restart to take effect.

**Note:** *xorg.conf* options can differ from *xsetwacom* options.

*xsetwacom* can try to print all current settings of a device in *xorg.conf* format with:

```
$ xsetwacom get *device* all

```

### Remapping buttons

The X driver lets you remap the buttons on tablets and pens. Buttons are identified by numbers. Tablet buttons start at 1, pen buttons start at 2 (1 is the tip contact event). By default the X driver maps button *M* to mouse button *M*. Because X uses buttons 4-7 as the four scrolling directions, physical buttons 4 and higher are mapped to mouse buttons 8 and higher by default. While *xorg.conf* uses the actual button numbers and only lets you map to mouse buttons, *xsetwacom* uses the translated mouse button numbers and allows mapping to multiple keycodes (but not keysyms).

If you have not yet remapped your buttons you can easily identify their ids with [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev), by running the following command, placing the mouse cursor on the created window and pressing a button:

 `$ xev -event button` 
```
Outer window is 0x1a00001, inner window is 0x1a00002

ButtonPress event, serial 25, synthetic NO, window 0x1a00001,
    root 0x2a0, subw 0x0, time 3390669, (404,422), root:(1047,444),
    state 0x0, button 8, same_screen YES

```

In this case the button number for *xsetwacom* is 8 and the actual button number for *xorg.conf* is 4.

Alternatively, if you want an overview of your tablet's button layout you can look at your tablet's layout SVG. Firstly, find out the filename with a recursive [grep](/index.php/Grep "Grep") search for the tablet name reported by `xsetwacom list devices`:

 `$ grep -rl 'Wacom Bamboo 16FG 4x5' /usr/share/libwacom/*.tablet`  `/usr/share/libwacom/bamboo-16fg-s-t.tablet` 

In this case the respective layout SVG is `/usr/share/libwacom/layouts/bamboo-16fg-s-t.svg`. The letters in the SVG correspond to the button numbers: A=1, B=2, C=3, ...

#### Mapping pad buttons to function keys

If you want to bind your tablet buttons to different shortcuts in different applications, you may want to map your tablet buttons to function keys because applications generally do not let you bind keyboard shortcuts to mouse buttons.

Firstly, map the pad buttons to mouse buttons 11 and higher so that you can distinguish them from regular mouse buttons. For example:

```
xsetwacom set *pad* Button 1 11
xsetwacom set *pad* Button 2 12
...

```

Then map the mouse buttons to the function keys. This can be done with [xbindkeys](/index.php/Xbindkeys "Xbindkeys") and [xdotool](/index.php/Xdotool "Xdotool") by adding an entry like the following for every pad to your `~/.xbindkeysrc`:

```
"xdotool key F21"
  b:11

"xdotool key F22"
  b:12
...

```

#### The syntax

The syntax of `xsetwacom` is flexible but not very well documented. The general mapping syntax (extracted from the source code) for xsetwacom 0.17.0 is the following.

```
 KEYWORD [ARGS...] [KEYWORD [ARGS...] ...]

 KEYWORD + ARGS:
   key [+,-]KEY [[+,-]KEY ...]  where +:key down, -:key up, no prefix:down and up
   button BUTTON [BUTTON ...]   (1=left,2=middle,3=right mouse button, 4/5 scroll mouse wheel)
   modetoggle                   toggle absolute/relative tablet mode 
   displaytoggle                toggle cursor movement among all displays which include individual screens
                                plus the whole desktop for the selected tool if it is not a pad.
                                When the tool is a pad, the function applies to all tools that are asssociated
                                with the tablet

 BUTTON: button ID as integer number

 KEY: MODIFIER, SPECIALKEY or ASCIIKEY
 MODIFIER: (each can be prefix with an **l** or an **r** for the left/right modifier (no prefix = left)
    ctrl=ctl=control, meta, alt, shift, super, hyper
 SPECIALKEY: f1-f35, esc=Esc, up,down,left,right, backspace=Backspace, tab, PgUp,PgDn
 ASCIIKEY: (usual characters the key produces, e.g. a,b,c,1,2,3 etc.)

```

#### Some examples

```
 $ xsetwacom set *pad* Button 1 3 # right mouse button
 $ xsetwacom set *pad* Button 1 "key +ctrl z -ctrl"
 $ xsetwacom get *pad* Button 1
 key +Control_L +z -z -Control_L
 $ xsetwacom set *pad* Button 1 "key +shift button 1 key -shift"

```

Even little macros are possible:

```
 $ xsetwacom set *pad* Button 1 "key +shift h -shift e l l o"

```

**Note:** If you try to run a script with `xsetwacom` commands from a udev rule, you might find that it will not work, as the Wacom input devices will not be ready at the time. A workaround is to add `sleep 1` at the beginning of your script.

#### Execute custom commands

Mapping custom commands to the buttons is a little bit tricky but actually very simple. First, install [xbindkeys](/index.php/Xbindkeys "Xbindkeys").

To get well defined button codes add the following to your permanent configuration file, e.g. `/etc/X11/xorg.conf.d/52-wacom-options.conf` in the InputClass section of your **pad** device. Map the tablet's buttons to some unused button ids.

```
 # Setting up buttons (preferably choose the correct button order, so the topmost key is mapped to 10 and so on)
 Option "Button1" "10"
 Option "Button2" "11"
 Option "Button3" "12"
 Option "Button4" "13"

```

Then restart your *Xorg* server and verify the buttons using `xev` or `xbindkeys -mk`.

Now set up your xbindkeys configuration, if you do not already have one you might want to create a default configuration

```
 $ xbindkeys --defaults > ~/.xbindkeysrc

```

Then add your custom key mapping to `~/.xbindkeysrc`, for example

```
 "firefox"
     m:0x10 + b:10   (mouse)
 "xterm"
     m:0x10 + b:11   (mouse)
 "xdotool key ctrl-z"
     m:0x10 + b:12   (mouse)
 "send-notify Test "No need for escaping the quotes""
     m:0x10 + b:13   (mouse)

```

### Adjusting aspect ratios

Drawing areas of tablets are generally more square than the usual widescreen display with a 16:9 aspect ratio, leading to a slight vertical compression of your input. To resolve such an aspect ratio mismatch you need to compromise by either reducing the drawing area height (called *Force Proportions* on Windows) or reducing the screen area width. The former wastes drawing area and the latter prevents you from reaching the right edge of your screen with your Stylus. It is probably still a compromise worth to be made because it prevents your strokes from being skewed.

Find out your tablet's resolution by running:

```
$ xsetwacom get *stylus* Area

```

#### Reducing the drawing area height

Run:

```
$ xsetwacom set *stylus* Area 0 0 *tablet_width* *height*

```

where *height* is *tablet_width * screen_height / screen_width*.

The tablet resolution can be reset back to the default using:

```
$ xsetwacom set *stylus* ResetArea

```

#### Reducing the screen area width

Run:

```
$ xsetwacom set *stylus* MapToOutput *WIDTH*x*SCREEN_HEIGHT*+0+0

```

where *WIDTH* is *screen_height * tablet_width / tablet_height*.

### LEDs

See the [sysfs-driver-wacom](https://www.kernel.org/doc/Documentation/ABI/testing/sysfs-driver-wacom) documentation. To make changes without requiring root permissions you will likely want to create a [udev](/index.php/Udev "Udev") rule like so:

 `/etc/udev/rules.d/99-wacom.rules` 
```
# Give the users group permissions to set Wacom device LEDs.
ACTION=="add", SUBSYSTEM=="hid", DRIVERS=="wacom", RUN+="/usr/bin/sh -c 'chown :users /sys/%p/wacom_led/*'"

```

Setting the Intuos OLEDs can be done using [i4oled](https://aur.archlinux.org/packages/i4oled/) from the AUR.

### TwinView setup

If you are going to use two monitors the aspect ratio while using the tablet might feel unnatural. In order to fix this you need to add:

```
Option "TwinView" "horizontal"

```

to all of your Wacom-InputDevice entries in the *xorg.conf* file. You may read more about that [here](http://ubuntuforums.org/showthread.php?t=640898).

#### Temporary TwinView setup

For temporary mapping of a Wacom device to a single display *while preserving the aspect ratio*, [this script](https://gist.github.com/Quackmatic/6c19fe907945d735c045) may be used. This will letter-box the surface area of the device as required to ensure the input is not stretched on the display. This script may be executed in your `.xinitrc` file for it to automatically run.

### xrandr setup

[xrandr](/index.php/Xrandr "Xrandr") sets two monitors as one big screen, mapping the tablet to the whole virtual screen and deforming aspect ratio. For a solution see this thread: [Arch Linux forum](https://bbs.archlinux.org/viewtopic.php?pid=797617).

If you just want to map the tablet to one of your screens, first find out what the screens are called:

```
$ xrandr
Screen 0: minimum 320 x 200, current 3840 x 1080, maximum 16384 x 16384
HDMI-0 disconnected (normal left inverted right x axis y axis)
DVI-0 connected 1920x1080+0+0 (normal left inverted right x axis y axis) 477mm x 268mm
  1920x1080      60.0*+
  1680x1050      60.0  
  ...
VGA-0 connected 1920x1080+1920+0 (normal left inverted right x axis y axis) 477mm x 268mm
  1920x1080      60.0*+
  1680x1050      60.0  
  ...

```

Then you need to know what is the ID of your tablet.

```
$ xsetwacom list devices
WALTOP International Corp. Slim Tablet stylus   id: 12  type: STYLUS

```

In my case I want to map the tablet (ID: 12) to the screen on the right, which is *VGA-0*. I can do that with this command

```
$ xsetwacom set 12 MapToOutput VGA-0

```

This should work immediately, no root necessary.

Should this fail when using the NVIDIA binary driver, using *HEAD-0*, *HEAD-1* and so on to refer to the monitors may work.

If xsetwacom replies with "Unable to find an output ..." an X11 geometry string of the form `WIDTHxHEIGHT+X+Y` can be specified instead of the screen identifier. In this example

```
$ xsetwacom set 12 MapToOutput 1920x1080+1920+0

```

should also map the tablet to the screen on the right.

Alternatively, you can use [this bash script](https://bitbucket.org/denilsonsa/small_scripts/src/3380435f92646190f860b87f566a39d0e215034c/xsetwacom_my_preferences.sh?at=default) to quickly map the tablet to one of your screens (or the entire desktop) and fix the aspect ratio.

In case *xsetwacom* does not work, you can try *xinput*.

First, you need to find your tablet's ID.

```
$ xinput list

```

In my case, the output is:

```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ Wacom Intuos PT S 2 Finger                id=11   [slave  pointer  (2)]
⎜   ↳ Wacom Intuos PT S 2 Pad                   id=12   [slave  pointer  (2)]
⎜   ↳ USB Keyboard                              id=14   [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=16   [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=17   [slave  pointer  (2)]
⎜   ↳ SteelSeries Kinzu V2 Gaming Mouse         id=9    [slave  pointer  (2)]
⎜   ↳ Wacom Intuos PT S 2 Pen Pen (0x6281780c)  id=20   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ Wacom Intuos PT S 2 Pen                   id=10   [slave  keyboard (3)]
    ↳ USB Keyboard                              id=13   [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=15   [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=18   [slave  keyboard (3)]
    ↳ USB Keyboard                              id=19   [slave  keyboard (3)]

```

This mean, my tablet's ID is *20*. Now we map it with *VGA-0* screen:

```
$ xinput map-to-output 20 VGA-0

```

### Pressure curve

Use the [Wacom Pressure Curve and Threshold Graph](https://linuxwacom.github.io/bezier.html) to find P1=red (eg. 50,0) and P2=purple (eg. 100,80) of your desired curve. The x-axis is the input pressure you apply to the pen; the y-axis is the output pressure the application is given.

You can change the pressure curve with:

```
$ xsetwacom set *stylus* PressureCurve *x1 y1 x2 y2*

```

## Application-specific configuration

### Blender

To enable pad buttons and extra pen buttons in [Blender](/index.php/Blender "Blender"), you can create a xsetwacom wrapper to temporarily remap buttons for your blender session.

Provided example (for Bamboo fun) adapted to *Sculpt* mode: [blender_sculpt.sh](http://pastebin.archlinux.fr/1887946)

It remaps:

*   Left tablet buttons to `Shift` and `Ctrl` *(pan/tilt/zoom/smooth/invert)*
*   Right tablet buttons to `F` *(brush size/strenght)* and `Ctrl-z` *(undo)*
*   Top pen button ton `m` *(mask control)*

### GIMP

To enable proper usage, and pressure sensitive painting in [GIMP](/index.php/GIMP "GIMP"), just go to *Edit > Input Devices*. Now for each of your *eraser*, *stylus*, and *cursor* *devices*, set the *mode* to *Screen*, and remember to save.

*   Please take note that if present, the *pad* *device* should be kept disabled as I do not think GIMP supports such things. Alternatively, to use such features of your tablet you should map them to keyboard commands with a program such as [Wacom ExpressKeys](http://hem.bredband.net/devel/wacom/).

*   You should also take note that the tool selected for the *stylus* is independent to that of the *eraser*. This can actually be quite handy, as you can have the *eraser* set to be used as any tool you like.

For more information checkout the *Setting up GIMP* section of [GIMP Talk - Community - Install Guide: Getting Wacom Drawing Tablets To Work In Gimp](http://www.gimptalk.com/forum/topic.php?t=17992&start=1).

If the above was not enough, you may want to try setting up the tablet's stylus (and eraser) as a second mouse pointer (separating it from your mouse) by using the `xinput create-master` and `xinput reattach` commands. It can help when GIMP does not start painting even if the stylus touches the tablet.

### Inkscape

Pressure sensitivity in [Inkscape](/index.php/Inkscape "Inkscape") is enabled the same way as in GIMP. Go to *Edit > Input Devices...*. Now for each of your *eraser*, *stylus*, and *cursor* *devices*, set the *mode* to *Screen*, and remember to save.

### Krita

If your tablet does not draw in Krita (clicks/pressure are not registered) but works in the brush selection dialog which has a small test area, try putting Krita in full-screen or canvas-only mode.

Krita only requires that Qt is able to use your tablet to function properly. If your tablet is not working in Krita, then make sure to check it is working in Qt first. The effect of tablet pressure can then be tweaked in the painttop configuration, for example by selecting opacity, then selecting pressure from the drop down and adjusting the curve to your preference.

### VirtualBox

First, make sure that your tablet works well under Arch. Then, download and install the last driver from [Wacom website](http://www.wacom.com/downloads/drivers.php) on the guest OS. Shutdown the virtual machine, go to *Settings > USB*. Select *Add Filter From Device* and select your tablet (e.g. WACOM CTE-440-U V4.0-3 [0403]). Select *Edit Filter*, and change the last item *Remote* to *Any*.

## Troubleshooting

Newer tablets' drivers might not be in the kernel yet, and additional manipulations might be needed. A notable example is the newer Intuos line of tablets (Draw/Comic/Photo).

### Unknown device_type

If your tablet does not get recognized by `xsetwacom` and `dmesg` complains about an unknown device_type, then you need to install a patched version of input-wacom.

Download and install the for-4.4 branch from [SourceForge](http://sourceforge.net/p/linuxwacom/input-wacom/ci/jiri/for-4.4/~/tarball). Your device should be recognized after you run

```
 # rmmod wacom
 # insmod /lib/modules/YOUR_KERNEL/kernel/drivers/hid/wacom.ko.gz

```

### Tablet recognized but xsetwacom and similar tools do not display it

Your logs indicate that the correct driver is selected, and the tablet works. However, when running `xsetwacom list devices` or use similar tools that depend on the correct driver, you get an empty list.

A reason might be the execution order of your xorg configuration. `/usr/share/X11/xorg.conf.d` gets executed first, then `/etc/X11/xorg.conf.d`. The package [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) contains the file `/usr/share/X11/xorg.conf.d/70-wacom.conf`. If there is a catchall for tablets, executed after this file, the previously selected `wacom` driver will be overwritten with a generic one that does not work with xsetwacom et. al.

To make sure, check the rules contained in the files executed after `/usr/share/X11/xorg.conf.d/70-wacom.conf` for anything that looks like graphics tablets.

### Manual setup

A manual configuration is done in `/etc/X11/xorg.conf` or in a separate file in the `/etc/X11/xorg.conf.d/` directory. The Wacom tablet device is accessed using a input event interface in `/dev/input/` which is provided by the kernel driver. The interface number `event??` is likely to change when unplugging and replugging into the same or especially a different *USB* port. Therefore it is wise to not refer to the device using its concrete `event??` interface (**static** configuration) but by letting *udev* dynamically create a symbolic link to the correct `event` file (**dynamic** configuration).

#### Dynamic with udev

**Note:** In AUR there is wacom-udev package, which includes udev-rules-file. You might skip this part and move on to the `xorg.conf` configuration if you are using the wacom-udev package from AUR.

Assuming *udev* is already installed you simply need to install [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/) from the [AUR](/index.php/AUR "AUR").

##### USB-devices

After (re-)plugging in your *USB*-tablet (or at least after rebooting) some symbolic links should appear in `/dev/input` referring to your tablet device.

```
 $ ls /dev/input/wacom* 
 /dev/input/wacom  /dev/input/wacom-stylus  /dev/input/wacom-touch

```

If not, your device is likely to be not yet included in the *udev* configuration from *wacom-udev* which resides in `/usr/lib/udev/rules.d/10-wacom.rules`. It is a good idea to copy the file e.g. to `10-my-wacom.rules` before modifying it, else it might be reverted by a package upgrade.

Add your device to the file by duplicating some line of another device and adapting *idVendor*,*idProduct* and the symlink name to your device. The two id's can be determined using

```
$ lsusb | grep -i wacom
Bus 002 Device 007: ID 056a:0062 Wacom Co., Ltd

```

In this example idVendor is 056a and idProduct 0062\. In case you have device with touch (e.g. Bamboo Pen&Touch) you might need to add a second line for the touch input interface. For details check the linuxwacom wiki [Fixed device files with udev](http://linuxwacom.sourceforge.net/wiki/index.php/Fixed_device_files_with_udev).

Save the file and reload udev's configuration profile using the command *udevadm control --reload-rules* Check again the content of */dev/input* to make sure that the *wacom* symlinks appeared. Note that you may need to plug-in the tablet again for the device to appear.

The files of further interest for the *Xorg* configuration are `/dev/input/wacom` and for a touch-device also `/dev/input/wacom_touch`.

##### Serial devices

The [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/) should also include support for serial devices. Users of serial tablets might be also interested in the inputattach tool from [linuxconsole](https://www.archlinux.org/packages/?name=linuxconsole) package. The inputattach command allows to bind serial device into /dev/input tree, for example with:

```
 # inputattach --w8001 /dev/ttyS0

```

See *man inputattach* for help about available options. As for USB devices one should end up with a file `/dev/input/wacom` and proceed with the *Xorg* configuration.

#### Static setup

Usually it is recommended to rely on [Xorg](/index.php/Xorg "Xorg")'s auto-detection or to use a **dynamic** setup. However for an *internal* tablet device one might consider a **static** Xorg setup in case autodetection does not work. A static [Xorg](/index.php/Xorg "Xorg") setup is usually not able to recognize your Wacom tablet when it is connected to a different *USB* port or even after unplugging and replugging it into the same port, and as such it should be considered as deprecated.

If you insist in using a static setup just refer to your tablet in the *Xorg* configuration in the next section using the correct `/dev/input/event??` files as one can find out by looking into `/proc/bus/input/devices`.

#### Xorg configuration

In either case, dynamic or static setup you got now one or two files in `/dev/input/` which refer to the correct input event devices of your tablet. All that is left to do is add the relevant information to `/etc/X11/xorg.conf`, or a dedicated file under `/etc/X11/xorg.conf.d/`. The exact configuration depends on your tablet's features of course. `xsetwacom list devices` might give helpful information on what *InputDevice* sections are needed for your tablet.

An example configuration for a *Volito2* might look like this

```
Section "InputDevice"
    Driver        "wacom"
    Identifier    "stylus"
    Option        "Device"       "/dev/input/wacom"   # or the corresponding event?? for a static setup
    Option        "Type"         "stylus"
    Option        "USB"          "on"                 # USB ONLY
    Option        "Mode"         "Relative"           # other option: "Absolute"
    Option        "Vendor"       "WACOM"
    Option        "tilt"         "on"  # add this if your tablet supports tilt
    Option        "Threshold"    "5"   # the official linuxwacom howto advises this line
EndSection
Section "InputDevice"
    Driver        "wacom"
    Identifier    "eraser"
    Option        "Device"       "/dev/input/wacom"   # or the corresponding event?? for a static setup
    Option        "Type"         "eraser"
    Option        "USB"          "on"                  # USB ONLY
    Option        "Mode"         "Relative"            # other option: "Absolute"
    Option        "Vendor"       "WACOM"
    Option        "tilt"         "on"  # add this if your tablet supports tilt
    Option        "Threshold"    "5"   # the official linuxwacom howto advises this line
EndSection
Section "InputDevice"
    Driver        "wacom"
    Identifier    "cursor"
    Option        "Device"       "/dev/input/wacom"   # or the corresponding event?? for a static setup
    Option        "Type"         "cursor"
    Option        "USB"          "on"                  # USB ONLY
    Option        "Mode"         "Relative"            # other option: "Absolute"
    Option        "Vendor"       "WACOM"
EndSection

```

Make sure that you also change the path (`"Device"`) to your mouse, as it will be `/dev/input/mouse_udev` now.

```
Section "InputDevice"
    Identifier  "Mouse1"
    Driver      "mouse"
    Option      "CorePointer"
    Option      "Device"             "/dev/input/mouse_udev"
    Option      "SendCoreEvents"     "true"
    Option      "Protocol"           "IMPS/2"
    Option      "ZAxisMapping"       "4 5"
    Option      "Buttons"            "5"
EndSection

```

Add this to the *ServerLayout* section

```
InputDevice "cursor" "SendCoreEvents" 
InputDevice "stylus" "SendCoreEvents"
InputDevice "eraser" "SendCoreEvents"

```

And finally make sure to update the identifier of your mouse in the *ServerLayout* section – as mine went from

```
InputDevice    "Mouse0" "CorePointer"

```

to

```
InputDevice    "Mouse1" "CorePointer"

```

### Mouse Moving Erratically due to Proximity Sensor

You can disable the mouse jumping due to a proximity sensor detecting a non-existing stylus. You can find your device with xinput --list, and after seeing the Stylus, disable it with: xinput disable "Your Device Name". This only works if you are not currently using a stylus.

## See also

*   [List of applications/Documents#Stylus note-taking](/index.php/List_of_applications/Documents#Stylus_note-taking "List of applications/Documents")
*   [input-wacom Wiki](https://github.com/linuxwacom/input-wacom/wiki)
*   [xf86-input-wacom Wiki](https://github.com/linuxwacom/xf86-input-wacom/wiki) (out of date)
*   [GIMP Talk - Community - Install Guide: Getting Wacom Drawing Tablets To Work In Gimp](http://www.gimptalk.com/forum/topic.php?t=17992&start=1)
*   [Ubuntu Help: Wacom](https://help.ubuntu.com/community/Wacom)
*   [Ubuntu Forums - Install a LinuxWacom Kernel Driver for Tablet PC's](http://ubuntuforums.org/showthread.php?t=1038949)