Related articles

*   [Calibrating Touchscreen](/index.php/Calibrating_Touchscreen "Calibrating Touchscreen")

If you ever tried to set up a touchscreen device in linux, you might have noticed that it's either working out of the box (besides some calibration) or is very tedious, especially when it is not supported by the kernel.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Available X11 drivers](#Available_X11_drivers)
*   [3 evdev drivers](#evdev_drivers)
    *   [3.1 Calibration](#Calibration)
*   [4 Using a touchscreen in a multi-head setup](#Using_a_touchscreen_in_a_multi-head_setup)
*   [5 Touchegg](#Touchegg)

## Introduction

This article assumes that your touchscreen device is supported by the kernel (e.g. by the usbtouchscreen module). That means there exists a `/dev/input/event*` node for your device. Check out

```
less /proc/bus/input/devices

```

to see if your device is listed or try

```
cat /dev/input/event? # replace ? with the event numbers

```

for every of your event nodes while touching the display. If you found the corresponding node, it's likely that you will be able to get the device working.

## Available X11 drivers

There are a lot of touchscreen input drivers for X11 out there. The most common ones are in the *extra* repository:

*   [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) (likely the default driver if you plug in your touchscreen and it "just works")
*   [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput); see also [libinput](/index.php/Libinput "Libinput")
*   [xf86-input-elographics](https://www.archlinux.org/packages/?name=xf86-input-elographics)

Less common drivers, not contained in the repository, are:

*   xf86-input-magictouch
*   xf86-input-mutouch
*   xf86-input-plpevtch
*   xf86-input-palmax

Proprietary drivers exist for some devices (e.g.: [xf86-input-egalax](https://aur.archlinux.org/packages/xf86-input-egalax/)), but it's recommended to try the open source drivers first.

Depending on your touchscreen device choose an appropriate driver. Again, evdev is likely to be the default if your touchscreen "just works."

## evdev drivers

### Calibration

Install [xinput_calibrator](https://aur.archlinux.org/packages/xinput_calibrator/) (AUR). Then, run xinput_calibrator and follow the instructions.

## Using a touchscreen in a multi-head setup

To use multiple displays (some of which are touchscreens), you need to tell Xorg the mapping between the touch surface and the screen. This can be achieved with *xinput* as follows.

Take for example the setup of having a wacom tablet and an external monitor; *xrandr* shows both displays:

```
$ xrandr
Screen 0: minimum 320 x 200, current 2944 x 1080, maximum 8192 x 8192
LVDS1 connected 1024x768+0+0 (normal left inverted right x axis y axis) 0mm x 0mm
   1024x768       60.0*+
   800x600        60.3     56.2  
   640x480        59.9  
VGA1 connected 1920x1080+1024+0 (normal left inverted right x axis y axis) 477mm x 268mm
   1920x1080      60.0*+
   1600x1200      60.0  
   1680x1050      60.0  
   1680x945       60.0  

```

You see we have two displays here. LVDS1 and VGA1\. LVDS1 is the display internal to the tablet, and VGA1 is the external monitor. We wish to map our stylus input to LVDS1\. So we have to find the ID of the stylus input:

```
 $ xinput --list
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ QUANTA OpticalTouchScreen               	id=9	[slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                   	id=11	[slave  pointer  (2)]
⎜   ↳ Serial Wacom Tablet WACf004 stylus      	id=13	[slave  pointer  (2)]
⎜   ↳ Serial Wacom Tablet WACf004 eraser      	id=14	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Sleep Button                            	id=8	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=10	[slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                  	id=12	[slave  keyboard (3)]

```

We see that we have two stylus inputs who's ID's are `13` and `14`. We now need to simply map our inputs to our output like so:

```
xinput --map-to-output 13 LVDS1
xinput --map-to-output 14 LVDS1

```

You can automate this by putting these commands in your `~/.xinitrc` or similar. ID numbers are not guaranteed to persist between boots, but you can extract that info from xinput itself.

```
xinput --map-to-output $(xinput list --id-only "Serial Wacom Tablet WACf004 stylus") LVDS1
xinput --map-to-output $(xinput list --id-only "Serial Wacom Tablet WACf004 eraser") LVDS1

```

Also, the mapping will be lost if the touchscreen is disconnected and re-connected, for example, when switching monitors via a KVM. In that case it is better to use a udev rule. The [Calibrating Touchscreen](/index.php/Calibrating_Touchscreen "Calibrating Touchscreen") page has an example udev rule for the case when a transformation matrix has been calculated manually and needs to be applied automatically.

## Touchegg

[Touchegg](/index.php/Touchegg "Touchegg") is a multitouch gesture program, that runs as a user in the background, recognizes gestures, and translates them to more conventional events such as mouse wheel movements, so that you can for example use two fingers to scroll. But it also interferes with applications or window managers which already do their own gesture recognition. If you have both a touchpad and a touchscreen, and if the touchpad driver (such as synaptics or libinput) has been configured not to recognize gestures itself, but to pass through the multi-touch events, then Touchegg will recognize gestures on both: this cannot be configured. In fact it does a better job of recognizing gestures than either the synaptics or libinput touchpad drivers; but on the touchscreen, it's generally better for applications to respond to touch in their own unique ways. Some Qt and GTK applications do that, but they will not be able to if you have Touchegg "eating" the touch events. So, Touchegg is useful when you are running mainly legacy applications which do not make their own use of touch events.