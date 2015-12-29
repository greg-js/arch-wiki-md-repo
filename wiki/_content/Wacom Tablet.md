# Wacom Tablet

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This guide was started for _USB_ based Wacom tablets, so much of the info in here focuses on that. Usually it is recommended to rely on [Xorg](/index.php/Xorg "Xorg")'s auto-detection or to use a **dynamic** setup. However for an _internal_ tablet device one might consider a **static** Xorg setup in case autodetection does not work. A static [Xorg](/index.php/Xorg "Xorg") setup is usually not able to recognize your Wacom tablet when it is connected to a different _USB_ port or even after unplugging and replugging it into the same port, and as such it should be considered as deprecated.

## Contents

*   [1 Installing](#Installing)
    *   [1.1 Check if kernel drivers needed (usually not)](#Check_if_kernel_drivers_needed_.28usually_not.29)
    *   [1.2 Install Wacom drivers](#Install_Wacom_drivers)
    *   [1.3 Automatic setup](#Automatic_setup)
    *   [1.4 Manual setup](#Manual_setup)
        *   [1.4.1 Dynamic with udev](#Dynamic_with_udev)
            *   [1.4.1.1 USB-devices](#USB-devices)
            *   [1.4.1.2 Serial devices](#Serial_devices)
        *   [1.4.2 Static setup](#Static_setup)
        *   [1.4.3 Xorg configuration](#Xorg_configuration)
*   [2 Configuration](#Configuration)
    *   [2.1 General concepts](#General_concepts)
        *   [2.1.1 Temporary configuration](#Temporary_configuration)
        *   [2.1.2 Permanent configuration](#Permanent_configuration)
        *   [2.1.3 Changing orientation](#Changing_orientation)
        *   [2.1.4 Remapping Buttons](#Remapping_Buttons)
            *   [2.1.4.1 Finding out the button IDs](#Finding_out_the_button_IDs)
            *   [2.1.4.2 The syntax](#The_syntax)
            *   [2.1.4.3 Some examples](#Some_examples)
            *   [2.1.4.4 Execute custom commands](#Execute_custom_commands)
        *   [2.1.5 LEDs](#LEDs)
        *   [2.1.6 TwinView Setup](#TwinView_Setup)
            *   [2.1.6.1 Temporary TwinView Setup](#Temporary_TwinView_Setup)
        *   [2.1.7 Xrandr Setup](#Xrandr_Setup)
    *   [2.2 Pressure curves](#Pressure_curves)
    *   [2.3 Force Proportions](#Force_Proportions)
    *   [2.4 Using kcm-wacomtablet](#Using_kcm-wacomtablet)
*   [3 Application-specific configuration](#Application-specific_configuration)
    *   [3.1 GIMP](#GIMP)
    *   [3.2 Inkscape](#Inkscape)
    *   [3.3 Krita](#Krita)
    *   [3.4 VirtualBox](#VirtualBox)
    *   [3.5 Web Browser Plugin](#Web_Browser_Plugin)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Unknown device_type](#Unknown_device_type)
    *   [4.2 System freeze](#System_freeze)
*   [5 References](#References)

## Installing

### Check if kernel drivers needed (usually not)

After plugging in the tablet (in case of a USB device) check `lsusb` and/or `dmesg | grep -i wacom` to see if the kernel recognizes your tablet. It should also be listed in `/proc/bus/input/devices`.

In case it is not recognized, it might happen for new devices not to be supported by the current kernel. Sometimes the tablet has already support by a more recent driver than the one that comes with the kernel. In that case you may try to install [input-wacom-dkms](https://aur.archlinux.org/packages/input-wacom-dkms/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

### Install Wacom drivers

Thanks to [The Linux Wacom Project](http://linuxwacom.sourceforge.net), you only need to install the [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) package, which contains everything needed to use a Wacom tablet on Linux.

**Note:** There is also [xf86-input-wacom-git](https://aur.archlinux.org/packages/xf86-input-wacom-git/)<sup><small>AUR</small></sup> in AUR which provides git version of _xf86-input-wacom_, but you might encounter some troubles. For me the buttons for example did only work with the stable release, not with the git version. So it is recommended to try _xf86-input-wacom_ first.

### Automatic setup

Newer versions of X should be able to automatically detect and configure your device. Before going any further, restart X so the new udev rules take effect. Test if your device was recognized completely (i.e., that both pen and eraser work, if applicable), by issuing command

```
 $ xsetwacom --list devices

```

which should detect all devices with type, for example

```
 Wacom Bamboo 2FG 4x5 Pen stylus 	id: 8	type: STYLUS    
 Wacom Bamboo 2FG 4x5 Pen eraser 	id: 9	type: ERASER    
 Wacom Bamboo 2FG 4x5 Finger touch	id: 13	type: TOUCH     
 Wacom Bamboo 2FG 4x5 Finger pad 	id: 14	type: PAD       

```

You can also test it by opening [gimp](https://www.archlinux.org/packages/?name=gimp) or [xournal](https://www.archlinux.org/packages/?name=xournal) and checking the extended input devices section, or whatever tablet-related configuration is supported by the software of your choice.

For this to work you do not need any `xorg.conf` file, any configurations are made in files in the `/etc/X11/xorg.conf.d/` folder. If everything is working you can skip the manual configuration and **proceed** to the configuration section to learn how to further customize your tablet.

With the arrival of Xorg 1.8 support for HAL was dropped in favor of [udev](/index.php/Udev "Udev") which might break auto-detection for some tablets as fitting udev rules might not exist yet, so you may need to write your own.

If you have installed [libwacom](https://www.archlinux.org/packages/?name=libwacom) or associated packages like [libwacom-fedora](https://aur.archlinux.org/packages/libwacom-fedora/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libwacom-fedora)]</sup> remove those packages first. They are known to cause problems with newer version of X. _xf86-input-wacom_ is the only package you need to install the X11 drivers.

### Manual setup

A manual configuration is done in `/etc/X11/xorg.conf` or in a separate file in the `/etc/X11/xorg.conf.d/` directory. The Wacom tablet device is accessed using a input event interface in `/dev/input/` which is provided by the kernel driver. The interface number `event??` is likely to change when unplugging and replugging into the same or especially a different _USB_ port. Therefore it is wise to not refer to the device using its concrete `event??` interface (**static** configuration) but by letting _udev_ dynamically create a symbolic link to the correct `event` file (**dynamic** configuration).

#### Dynamic with udev

**Note:** In AUR there is wacom-udev package, which includes udev-rules-file. You might skip this part and move on to the `xorg.conf` configuration if you are using the wacom-udev package from AUR.

Assuming _udev_ is already installed you simply need to install [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

##### USB-devices

After (re-)plugging in your _USB_-tablet (or at least after rebooting) some symbolic links should appear in `/dev/input` referring to your tablet device.

```
 $ ls /dev/input/wacom* 
 /dev/input/wacom  /dev/input/wacom-stylus  /dev/input/wacom-touch

```

If not, your device is likely to be not yet included in the _udev_ configuration from _wacom-udev_ which resides in `/usr/lib/udev/rules.d/10-wacom.rules`. It is a good idea to copy the file e.g. to `10-my-wacom.rules` before modifying it, else it might be reverted by a package upgrade.

Add your device to the file by duplicating some line of another device and adapting _idVendor_,_idProduct_ and the symlink name to your device. The two id's can by determined using

```
$ lsusb | grep -i wacom
Bus 002 Device 007: ID 056a:0062 Wacom Co., Ltd

```

In this example idVendor is 056a and idProduct 0062. In case you have device with touch (e.g. Bamboo Pen&Touch) you might need to add a second line for the touch input interface. For details check the linuxwacom wiki [Fixed device files with udev](http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Fixed_device_files_with_udev).

Save the file and reload udev's configuration profile using the command _udevadm control --reload-rules_ Check again the content of _/dev/input_ to make sure that the _wacom_ symlinks appeared. Note that you may need to plug-in the tablet again for the device to appear.

The files of further interest for the _Xorg_ configuration are `/dev/input/wacom` and for a touch-device also `/dev/input/wacom_touch`.

##### Serial devices

The [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/)<sup><small>AUR</small></sup> should also include support for serial devices. Users of serial tablets might be also interested in the inputattach tool from [linuxconsole](https://www.archlinux.org/packages/?name=linuxconsole) package. The inputattach command allows to bind serial device into /dev/input tree, for example with:

```
 # inputattach --w8001 /dev/ttyS0

```

See _man inputattach_ for help about available options. As for USB devices one should end up with a file `/dev/input/wacom` and proceed with the _Xorg_ configuration.

#### Static setup

If you insist in using a static setup just refer to your tablet in the _Xorg_ configuration in the next section using the correct `/dev/input/event??` files as one can find out by looking into `/proc/bus/input/devices`.

#### Xorg configuration

In either case, dynamic or static setup you got now one or two files in `/dev/input/` which refer to the correct input event devices of your tablet. All that is left to do is add the relevant information to `/etc/X11/xorg.conf`, or a dedicated file under `/etc/X11/xorg.conf.d/`. The exact configuration depends on your tablet's features of course. `xsetwacom --list devices` might give helpful information on what _InputDevice_ sections are needed for your tablet.

An example configuration for a _Volito2_ might look like this

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

Add this to the _ServerLayout_ section

```
InputDevice "cursor" "SendCoreEvents" 
InputDevice "stylus" "SendCoreEvents"
InputDevice "eraser" "SendCoreEvents"

```

And finally make sure to update the identifier of your mouse in the _ServerLayout_ section – as mine went from

```
InputDevice    "Mouse0" "CorePointer"

```

to

```
InputDevice    "Mouse1" "CorePointer"

```

## Configuration

### General concepts

The configuration can be done in two ways temporary using the `xsetwacom` tool, which is included in _xf86-input-wacom_ or permanent in `xorg.conf` or better in a extra file in `/etc/X11/xorg.conf.d`. The possible options are identical so it is recommended to first use `xsetwacom` for testing and later add the final config to the _Xorg_ configuration files.

#### Temporary configuration

For the beginning it is a good idea to inspect the default configuration and all possible options using the following commands.

```
 $ xsetwacom --list devices                    # list the available devices for the get/set commands
 Wacom Bamboo 16FG 4x5 Finger touch	id: 12	type: TOUCH
 Wacom Bamboo 16FG 4x5 Finger pad	id: 13	type: PAD       
 Wacom Bamboo 16FG 4x5 Pen stylus	id: 17	type: STYLUS    
 Wacom Bamboo 16FG 4x5 Pen eraser	id: 18	type: ERASER
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5" all # using the device name
 $ xsetwacom --get 17 all                      # or equivalently use the device id
 $ xsetwacom --list parameters                 # to get an explanation of the Options
 $ man wacom                                   # get even more details

```

**Caution**, do not use the device id when writing shell scripts to set some options as the ids might change after an hotplug.

Options can be changed with the `--set` flag. Some useful examples are

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger touch" ScrollDistance 50  # change scrolling speed
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger touch" Gesture off        # disable multitouch gestures
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger touch" Touch off          # disable touch

```

For further configuration tips and tricks see below in [#Specific configuration tips](#Specific_configuration_tips).

**Note:** You can reset your temporary configuration at any time by unplugging and replugging in your tablet.

#### Permanent configuration

To make a permanent configuration the preferred way for _Xorg_>1.8 is to create a new file in `/etc/X11/xorg.conf.d` e.g. `52-wacom-options.conf` with the following content.

 `/etc/X11/xorg.conf.d/52-wacom-options.conf` 

```
Section "InputClass"
    Identifier "Wacom Bamboo stylus options"
    MatchDriver "wacom"
    MatchProduct "Pen"

    # Apply custom Options to this device below.
    Option "Rotate" "none"
    Option "RawSample" "20"
    Option "PressCurve" "0,10,90,100"
EndSection

Section "InputClass"
    Identifier "Wacom Bamboo eraser options"
    MatchDriver "wacom"
    MatchProduct "eraser"

    # Apply custom Options to this device below.
    Option "Rotate" "none"
    Option "RawSample" "20"
    Option "PressCurve" "5,0,100,95"
EndSection

Section "InputClass"
    Identifier "Wacom Bamboo touch options"
    MatchDriver "wacom"
    MatchProduct "Finger"

    # Apply custom Options to this device below.
    Option "Rotate" "none"
    Option "ScrollDistance" "18"
    Option "TapTime" "220"
EndSection

Section "InputClass"
    Identifier "Wacom Bamboo pad options"
    MatchDriver "wacom"
    MatchProduct "pad"

    # Apply custom Options to this device below.
    Option "Rotate" "none"

    # Setting up buttons
    Option "Button1" "1"
    Option "Button2" "2"
    Option "Button3" "3"
    Option "Button4" "0"
EndSection

```

The identifiers can be set arbitrarily. The option names are (except for the buttons) identical to the ones listed by `xsetwacom --list parameters` and especially also in `man wacom`. As noted in [#Remapping Buttons](#Remapping_Buttons) the button ids seem to be different than the ones for `xsetwacom`.

#### Changing orientation

If you want to use your tablet in a different orientation you have to tell this to the driver, else the movements do not cause the expected results. This is done by setting the **Rotate** option for all devices. Possible orientations are **none**,**cw**,**ccw** and **half**. A quick way is e.g.

```
 $ for i in 12 13 17 18; do xsetwacom --set $i Rotate half; done   # remember the ids might change when hotplugging

```

or use the following script like this `./wacomrot.sh half`

 `wacomrot.sh` 

```
#!/bin/bash
device="Wacom Bamboo 16FG 4x5"
stylus="$device Pen stylus"
eraser="$device Pen eraser"
touch="$device Finger touch"
pad="$device Finger pad"

xsetwacom --set "$stylus" Rotate $1
xsetwacom --set "$eraser" Rotate $1
xsetwacom --set "$touch"  Rotate $1
xsetwacom --set "$pad"    Rotate $1
```

#### Remapping Buttons

It is possible to remap the buttons with hotkeys.

##### Finding out the button IDs

Sometimes it needs some trial&error to find the correct button IDs. For me they even differ for `xsetwacom` and the `xorg.conf` configuration. Very helpful tools are `xev` or `xbindkeys -mk`. An easy way to proceed is the following

```
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 1
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5 Finger pad" Button 2 2
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5 Finger pad" Button 3 3
 $ # and so on

```

Then fire up `xev` from a terminal window, place your mouse cursor above the window and hit the buttons and write down the ids.

##### The syntax

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

##### Some examples

```
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 3 # right mouse button
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key +ctrl z -ctrl"
 $ xsetwacom --get "Wacom Bamboo 16FG 4x5 Finger pad" Button 1
 key +Control_L +z -z -Control_L
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key +shift button 1 key -shift"

```

even little macros are possible

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key +shift h -shift e l l o"

```

**Note:** There seems to be a bug in the _xf86-input-wacom_ driver version 0.17.0, at least for my _Wacom Bamboo Pen & Touch_, but I guess this holds in general. It causes the keystrokes not to be overwritten correctly.

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key a b c" # press button 1 -> abc
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key d"     # press button 1 -> dbc  WRONG!

```

A simple workaround is to reset the mapping by mapping to "":

```
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 ""          # to reset the mapping
 $ xsetwacom --set "Wacom Bamboo 16FG 4x5 Finger pad" Button 1 "key d"     # press button 1 -> d

```

**Note:** If you try to run a script with `xsetwacom` commands from a udev rule, you might find that it will not work, as the wacom input devices will not be ready at the time. A workaround is to add `sleep 1` at the beginning of your script.

##### Execute custom commands

Mapping custom commands to the buttons is a little bit tricky but actually very simple. First, install [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

To get well defined button codes add the following to your permanent configuration file, e.g. `/etc/X11/xorg.conf.d/52-wacom-options.conf` in the InputClass section of your **pad** device. Map the tablet's buttons to some unused button ids.

```
 # Setting up buttons (preferably choose the correct button order, so the topmost key is mapped to 10 and so on)
 Option "Button1" "10"
 Option "Button2" "11"
 Option "Button3" "12"
 Option "Button4" "13"

```

Then restart your _Xorg_ server and verify the buttons using `xev` or `xbindkeys -mk`.

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

#### LEDs

See the [sysfs-driver-wacom](https://www.kernel.org/doc/Documentation/ABI/testing/sysfs-driver-wacom) documentation. To make changes without requiring root permissions you will likely want to create a [udev](/index.php/Udev "Udev") rule like so:

 `/etc/udev/rules.d/99-wacom.rules` 

```
# Give the users group permissions to set Wacom device LEDs.
ACTION=="add", SUBSYSTEM=="hid", DRIVERS=="wacom", RUN+="/usr/bin/sh -c 'chown :users /sys/%p/wacom_led/*'"

```

Setting the Intuos OLEDs can be done using [i4oled](https://aur.archlinux.org/packages/i4oled/) from the AUR.

#### TwinView Setup

If you are going to use two Monitors the aspect ratio while using the Tablet might feel unnatural. In order to fix this you need to add

```
Option "TwinView" "horizontal"

```

To all of your Wacom-InputDevice entries in the `xorg.conf` file. You may read more about that [HERE](http://ubuntuforums.org/showthread.php?t=640898)

##### Temporary TwinView Setup

For temporary mapping of a Wacom device to a single display **while preserving the aspect ratio**, [this script](https://gist.github.com/Quackmatic/6c19fe907945d735c045) may be used. This will letter-box the surface area of the device as required to ensure the input is not stretched on the display. This script may be executed in your `.xinitrc` file for it to automatically run.

#### Xrandr Setup

xrandr sets two monitors as one big screen, mapping the tablet to the whole virtual screen and deforming aspect ratio. For a solution see this thread: [archlinux forum](https://bbs.archlinux.org/viewtopic.php?pid=797617).

If you just want to map the tablet to one of your screens, first find out what the screens are called

```
$ xrandr
Screen 0: minimum 320 x 200, current 3840 x 1080, maximum 16384 x 16384
**HDMI-0** disconnected (normal left inverted right x axis y axis)
**DVI-0** connected 1920x1080+0+0 (normal left inverted right x axis y axis) 477mm x 268mm
  1920x1080      60.0*+
  1680x1050      60.0  
  ...
**VGA-0** connected 1920x1080+1920+0 (normal left inverted right x axis y axis) 477mm x 268mm
  1920x1080      60.0*+
  1680x1050      60.0  
  ...

```

Then you need to know what is the ID of your tablet.

```
$ xsetwacom --list devices
WALTOP International Corp. Slim Tablet stylus   id: **12**  type: STYLUS

```

In my case I want to map the tablet (ID: **12**) to the screen on the right, which is **VGA-0**. I can do that with this command

```
$ xsetwacom --set **12** MapToOutput **"VGA-0"**

```

This should immediately work, no root necessary.

If xsetwacom replies with "Unable to find an output ..." an X11 geometry string of the form **WIDTHxHEIGHT+X+Y** can be specified instead of the screen identifier. In this example

```
$ xsetwacom --set **12** MapToOutput **"1920x1080+1920+0"**

```

should also map the tablet to the screen on the right.

Alternatively, you can use [this bash script](https://bitbucket.org/denilsonsa/small_scripts/src/3380435f92646190f860b87f566a39d0e215034c/xsetwacom_my_preferences.sh?at=default) to quickly map the tablet to one of your screens (or the entire desktop) and fix the aspect ratio.

### Pressure curves

Use [Wacom Pressure Demo](http://linuxwacom.sourceforge.net/misc/bezier.html) to find P1=red (eg. 50,0), P2=purple (eg. 100,80) and Threshold=green (eg. 27) of your desired curve. The x-axis is the input pressure you apply to the pen; the y-axis is the output pressure the application is given. ([example curve](http://250kb.de/u/150207/p/FoS1SiXuZQRP.png))

You can immediately test your desired values for your device (eg. "Wacom Intuos4 6x9 stylus") with

```
 xsetwacom --set "Wacom Intuos4 6x9 stylus" PressureCurve "50" "0" "100" "80"
 xsetwacom --set "Wacom Intuos4 6x9 stylus" Threshold "27"

```

Later you can apply them in `/etc/X11/xorg.conf` as shown below or you use the above shell commands in any startup script

 `/etc/X11/xorg.conf` 

```
  Option        "PressCurve"    "50,0,100,80"         # Custom preference
  Option        "Threshold"     "27"                  # sensitivity to do a "click"

```

### Force Proportions

For standard (**16:9**) widescreen monitors with Wacom tablets it is a typical problem that your strokes are slightly more horizontally oriented than they physically were (so for example a perfectly drawn circle with the pen will turn into a horizontal ellipse in the computer) because the tablet drawing surface proportions are larger on the vertical axis by default (**16:10**) than your monitors aspect ratio and this inconsistency will subtly distort your strokes. It is possible to force the proportions of the drawing surface to match the aspect ratio of your monitor to solve this problem by cutting off the bottom of the drawing surface to accommodate for the differences in vertical resolution with the below options. This is an alternative to the "Force Proportions" option in the Windows driver settings. It is generally recommended to do this to ensure maximum accuracy of your tablet input.

To get the tablets default values run the following command (where "device name or ID" would be for your stylus):

```
   xsetwacom --get "device name or ID" Area

```

After this you can figure out your tablet's resolution by dividing the values with the ratio **11.25** (so **21600/11.25=1920** and **13500/11.25=1200**), so to convert this to **1920x1080** (**16:9**) resolution, do **1080*11.25=12150** then to set the proportions with xsetwacom:

```
   xsetwacom --set "device name or ID" Area 0 0 21600 12150

```

Here is how to do the same in the xorg configuration file:

```
   Option "BottomX" "21600"
   Option "BottomY" "12150"

```

(An alternative formula would would be aspect ratio multiplied by **1350**. So **16:9** is **16*1350=21600** and **9*1350=12150**)

**Note:** There is also a KeepShape option which reportedly should do this automatically but it does not seem to work, which is why we have to do it the hard way. I do not know whether these values should be kept the same or increased on a bigger resolution monitor, but I highly suspect that they should be kept the same (e.g. the values are relative to the tablet's resolution, not the monitor's resolution; the important part is that the aspect ratio is correct, not that the resolution is a match)

### Using kcm-wacomtablet

The KDE configuration module [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)<sup><small>AUR</small></sup> (or if you're on Plasma 5, [kcm-wacomtablet-frameworks-git](https://aur.archlinux.org/packages/kcm-wacomtablet-frameworks-git/)<sup><small>AUR</small></sup>) supports easy configuration of the tablet through a graphical user interface, allowing for different profiles and proper hotplugging support. It will auto-detect the type of your tablet, and load your configuration profile automatically when the tablet is plugged in.

## Application-specific configuration

### GIMP

To enabled proper usage, and pressure sensitive painting in [GIMP](http://www.gimp.org), just go to _Edit → Input Devices_. Now for each of your _eraser_, _stylus_, and _cursor_ **devices**, set the **mode** to _Screen_, and remember to save.

*   Please take note that if present, the _pad_ **device** should be kept disabled as I do not think The GIMP supports such things. Alternatively, to use such features of your tablet you should map them to keyboard commands with a program such as [Wacom ExpressKeys](http://hem.bredband.net/devel/wacom/).

*   You should also take note that the tool selected for the _stylus_ is independent to that of the _eraser_. This can actually be quite handy, as you can have the _eraser_ set to be used as any tool you like.

For more information checkout the _Setting up GIMP_ section of [GIMP Talk - Community - Install Guide: Getting Wacom Drawing Tablets To Work In Gimp](http://www.gimptalk.com/forum/topic.php?t=17992&start=1).

If the above was not enough, you may want to try setting up the tablet's stylus (and eraser) as a second mouse pointer (separating it from your mouse) by using the `xinput create-master` and `xinput reattach` commands. It can help when GIMP does not start painting even if the stylus touches the tablet.

### Inkscape

As in GIMP, to do the same simply got to _Edit → Input Devices..._. Now for each of your _eraser_, _stylus_, and _cursor_ **devices**, set the **mode** to _Screen_, and remember to save.

### Krita

If your tablet does not draw in Krita (clicks/pressure are not registered) but works in the brush selection dialog which has a small test area, try putting Krita in full-screen or canvas-only mode.

Krita only requires that Qt is able to use your tablet to function properly. If your tablet is not working in Krita, then make sure to check it is working in Qt first. The effect of tablet pressure can then be tweaked in the painttop configuration, for example by selecting opacity, then selecting pressure from the drop down and adjusting the curve to your preference.

### VirtualBox

First, make sure that your tablet works well under Arch. Then, download and install the last driver from [Wacom website](http://www.wacom.com/downloads/drivers.php) on the guest OS. Shutdown the virtual machine, go to **Settings > USB**. Select **Add Filter From Device** and select your tablet (e.g. WACOM CTE-440-U V4.0-3 [0403]). Select **Edit Filter**, and change the last item **Remote** to **Any**.

### Web Browser Plugin

A plugin that imitates the official Wacom web plugin can be found on the AUR as [wacomwebplugin](https://aur.archlinux.org/packages/wacomwebplugin/). It has been tested successfully using Chromium and Firefox.

With this plugin it is possible to make use of online tools such as [deviantART's Muro](http://sta.sh/muro/). This plugin is in early stages so as always, your mileage may vary.

## Troubleshooting

Newer tablets' drivers might not be in the kernel yet, and additional manipulations might be needed. A notable example is the newer Intuos line of tablets (Draw/Comic/Photo).

### Unknown device_type

If your tablet does not get recognized by `xsetwacom` and `dmesg` complains about an unknown device_type, then you need to install a patched version of input-wacom.

Download and install the for-4.4 branch from [SourceForge](http://sourceforge.net/p/linuxwacom/input-wacom/ci/jiri/for-4.4/~/tarball). Your device should be recognized after you run

```
 # rmmod wacom
 # insmod /lib/modules/YOUR_KERNEL/extra/wacom.ko.gz

```

### System freeze

If your system freezes when your tablet gets activated by the stylus, then you will need to [patch](/index.php/Patch "Patch") your kernel with the patch from [LKML](https://lkml.org/lkml/2015/11/20/690).

## References

*   [Linux Wacom Project Wiki](http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Main_Page)
*   [GIMP Talk - Community - Install Guide: Getting Wacom Drawing Tablets To Work In Gimp](http://www.gimptalk.com/forum/topic.php?t=17992&start=1)
*   [Ubuntu Help: Wacom](https://help.ubuntu.com/community/Wacom)
*   [Ubuntu Forums - Install a LinuxWacom Kernel Driver for Tablet PC's](http://ubuntuforums.org/showthread.php?t=1038949)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wacom_Tablet&oldid=413737](https://wiki.archlinux.org/index.php?title=Wacom_Tablet&oldid=413737)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Graphics tablet](/index.php/Category:Graphics_tablet "Category:Graphics tablet")