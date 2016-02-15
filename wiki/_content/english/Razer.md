There are currently no official drivers for any Razer peripherals in Linux. However, Michael Buesch has created a tool called [razercfg](http://bues.ch/cms/hacking/razercfg.html) to configure Razer mice under Linux. There also exist scripts to enable macro keys of Razer keyboards.

## Contents

*   [1 Razer Peripherals](#Razer_Peripherals)
    *   [1.1 Compatibility](#Compatibility)
    *   [1.2 Installation](#Installation)
    *   [1.3 Using the Razer Configuration Tool](#Using_the_Razer_Configuration_Tool)
*   [2 Razer Blade](#Razer_Blade)
    *   [2.1 2014 version](#2014_version)
        *   [2.1.1 Problems](#Problems)
        *   [2.1.2 Possible trackpad solution](#Possible_trackpad_solution)
    *   [2.2 2013 version](#2013_version)
        *   [2.2.1 What works](#What_works)
        *   [2.2.2 Problems](#Problems_2)
        *   [2.2.3 Possible trackpad solution](#Possible_trackpad_solution_2)
*   [3 Razer Keyboards](#Razer_Keyboards)

## Razer Peripherals

### Compatibility

_razercfg_ lists the following mice models as stable:

*   Razer DeathAdder Classic
*   Razer DeathAdder 3500 DPI
*   Razer DeathAdder Black Edition
*   Razer DeathAdder 2013
*   Razer DeathAdder Chroma
*   Razer Krait
*   Razer Naga Classic
*   Razer Naga 2012
*   Razer Naga 2014
*   Razer Naga Hex
*   Razer Taipan

And the following as stable but missing minor features:

*   Razer Lachesis
*   Razer Copperhead
*   Razer Boomslang CE

### Installation

Download and install [razercfg](https://aur.archlinux.org/packages/razercfg/) or [razercfg-git](https://aur.archlinux.org/packages/razercfg-git/) for bleeding edge git releases from the [AUR](/index.php/AUR "AUR").

You also need to edit your `/etc/X11/xorg.conf` file to disable the current mouse settings by commenting them out as in the following example, where also some defaults are set as suggested by the author:

 `/etc/X11/xorg.conf` 

```
 Section "InputDevice"
    Identifier  "Mouse"
    Driver  "mouse"
    Option  "Device" "/dev/input/mice"
 EndSection
```

It is important to only have `Mouse` and not `Mouse#` listed in `xorg.conf`.

Restart the computer, then enter:

```
# udevadm control --reload-rules

```

Then [start](/index.php/Start "Start") the `razerd` daemon and possibly enable it.

### Using the Razer Configuration Tool

There are two commands you can use, one for the command line tool _razercfg_ or the Qt-based GUI tool _qrazercfg_.

From the tool you can use the 5 profiles, change the DPI, change mouse frequency, enable and disable the scroll and logo lights and configure the buttons.

## Razer Blade

Razer Blade is Razer's line of gaming laptops. There is currently a 14" model, and a 17" model. Due to the proprietary SBUI trackpad on the 17" model, it will be extremely difficult to get it to work without extensive USB protocol reversing.

### 2014 version

#### Problems

[Source](http://forum.notebookreview.com/razer/751074-2014-razer-blade-14-linux.html)

*   touchpad (multitouch, although this may be a kernel bug that has since been fixed)
*   keys to increase/decrease screen illumination not working
*   keys to increase/decrease keyboard illumination not working

#### Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone https://github.com/aduggan/hid-rmi.git -b rb14 # and then install it
depmod -a
sudo pacman -S synaptics

Feature still not working: pinch to zoom, 3rd mouse button

```

### 2013 version

#### What works

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356)

*   Wireless
*   Switchable graphics
*   Bluetooth
*   Keyboard light (HW controlled)
*   UEFI boot
*   Trackpad (only on Linux 4.0+ **without** libinput-based X.Org input driver (xf86-input-libinput) thanks to [Andrew Duggan's work](http://git.kernel.org/cgit/linux/kernel/git/jikos/hid.git/log/drivers/hid/hid-rmi.c?h=for-3.20/rmi)).

#### Problems

[Source](http://forum.notebookreview.com/razer/729380-razer-blade-pro-under-linux.html)

*   SwitchBlade UI doesn't work due to lack of drivers.
*   ~~Trackpad scrolling does not work.~~

#### Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone https://github.com/aduggan/hid-rmi.git -b rb14 # and then install it
depmod -a
sudo pacman -S synaptics

Feature still not working: pinch to zoom, 3rd mouse button

```

## Razer Keyboards

There are currently two Python scripts available to enable macro keys under Linux:

*   [blackwidowcontrol](https://aur.archlinux.org/packages/blackwidowcontrol/)
    *   Should work with regular BlackWidow and might work with BlackWidow Ultimate / 2013
    *   uses Python 3
    *   does not bundle any scripts to create macros (use hot key configuration tool from your desktop environment)
    *   allows to controls the status of the LED
*   [razer-blackwidow-macro-scripts](https://aur.archlinux.org/packages/razer-blackwidow-macro-scripts/)
    *   Should work with BlackWidow Ultimate 2013
    *   uses Python 2
    *   also bundles scripts to create and execute macros