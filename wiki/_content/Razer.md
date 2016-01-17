# Razer

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Various style issues, structure lacking (Discuss in [Talk:Razer#](https://wiki.archlinux.org/index.php/Talk:Razer))

There is currently no official driver for the Razer gaming mice in Linux. However, Michael Buesch has created a tool called [razercfg](http://bues.ch/cms/hacking/razercfg.html) to configure Razer mice under Linux.

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

Download and install [razercfg](https://aur.archlinux.org/packages/razercfg/)<sup><small>AUR</small></sup> or [razercfg-git](https://aur.archlinux.org/packages/razercfg-git/)<sup><small>AUR</small></sup> for bleeding edge git releases from the [AUR](/index.php/AUR "AUR").

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

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Why reboot? (Discuss in [Talk:Razer#](https://wiki.archlinux.org/index.php/Talk:Razer))

Restart the computer, then enter:

```
# udevadm control --reload-rules

```

Then [start](/index.php/Start "Start") the `razerd` daemon and possibly enable it.

### Using the Razer Configuration Tool

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Button configuration reported to not work (Discuss in [Talk:Razer#Button configuration in razercfg or qrazercfg](https://wiki.archlinux.org/index.php/Talk:Razer#Button_configuration_in_razercfg_or_qrazercfg))

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
*   <strike>Trackpad scrolling does not work.</strike>

#### Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone https://github.com/aduggan/hid-rmi.git -b rb14 # and then install it
depmod -a
sudo pacman -S synaptics

Feature still not working: pinch to zoom, 3rd mouse button

```

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The SBUI works as a trackpad, but no linux drivers currently exist. Does it even work for basic trackpad functionality? (Discuss in [Talk:Razer#](https://wiki.archlinux.org/index.php/Talk:Razer))

Retrieved from "[https://wiki.archlinux.org/index.php?title=Razer&oldid=415680](https://wiki.archlinux.org/index.php?title=Razer&oldid=415680)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mice](/index.php/Category:Mice "Category:Mice")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")