**Note:** This page refers to Razer's mice and keyboards. If you were looking for the laptop, see [Razer Blade](/index.php/Razer_Blade "Razer Blade").

There are currently no official drivers for any Razer peripherals in Linux. However, Michael Buesch has created a tool called [razercfg](http://bues.ch/cms/hacking/razercfg.html) to configure Razer mice under Linux. There also exist scripts to enable macro keys of Razer keyboards.

Another package, [openrazer-meta](https://aur.archlinux.org/packages/openrazer-meta/) can be used to enable Razer support along with [polychromatic](https://aur.archlinux.org/packages/polychromatic/) or [razergenie](https://aur.archlinux.org/packages/razergenie/) for GUI configuration. Supported devices are [listed here](https://openrazer.github.io/#devices)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 razercfg](#razercfg)
    *   [1.1 Compatibility](#Compatibility)
    *   [1.2 Installation](#Installation)
    *   [1.3 Using the Razer Configuration Tool](#Using_the_Razer_Configuration_Tool)
*   [2 OpenRazer](#OpenRazer)
    *   [2.1 Compatibility](#Compatibility_2)
        *   [2.1.1 Headsets](#Headsets)
        *   [2.1.2 Keyboards](#Keyboards)
        *   [2.1.3 Mice](#Mice)
        *   [2.1.4 Mousemats](#Mousemats)
        *   [2.1.5 Other devices](#Other_devices)
    *   [2.2 Installation](#Installation_2)
    *   [2.3 How to use](#How_to_use)
    *   [2.4 Troubleshooting](#Troubleshooting)
*   [3 Razer keyboards](#Razer_keyboards)
    *   [3.1 Blackwidow Control](#Blackwidow_Control)
        *   [3.1.1 Features](#Features)
        *   [3.1.2 How to Use](#How_to_Use_2)
    *   [3.2 Blackwidow macro scripts](#Blackwidow_macro_scripts)
        *   [3.2.1 Features](#Features_2)
*   [4 Troubleshooting](#Troubleshooting_2)
    *   [4.1 Mouse randomly stops working](#Mouse_randomly_stops_working)

## razercfg

### Compatibility

*razercfg* lists the following mice models as stable:

*   Razer DeathAdder 2013
*   Razer DeathAdder 3500 DPI
*   Razer DeathAdder Black Edition
*   Razer DeathAdder Chroma
*   Razer DeathAdder Classic
*   Razer Krait
*   Razer Naga 2012
*   Razer Naga 2014
*   Razer Naga Classic
*   Razer Naga Hex
*   Razer Taipan

And the following as stable but missing minor features:

*   Razer Boomslang CE
*   Razer Copperhead
*   Razer Lachesis

### Installation

Download and install [razercfg](https://www.archlinux.org/packages/?name=razercfg) or [razercfg-git](https://aur.archlinux.org/packages/razercfg-git/) for bleeding edge git releases from the [AUR](/index.php/AUR "AUR").

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

There are two commands you can use, one for the command line tool *razercfg* or the Qt-based GUI tool *qrazercfg*.

From the tool you can use the 5 profiles, change the DPI, change mouse frequency, enable and disable the scroll and logo lights and configure the buttons.

If the colors reset on reboot edit the config file directly and test with another reboot:

 `/etc/razer.conf` 
```
# Configure LEDs
led=1:GlowingLogo:on
led=1:Scrollwheel:on
mode=1:Scrollwheel:static
color=1:Scrollwheel:0000FF
mode=1:GlowingLogo:static
color=1:GlowingLogo:FFFFFF

```

"static" can probably be changed to spectrum or breathing, and mode/color lines can be removed if led is set to "off".

## OpenRazer

### Compatibility

#### Headsets

*   Razer Kraken 7.1 Chroma
*   Razer Kraken 7.1 Classic
*   Razer Kraken 7.1 V2

#### Keyboards

*   Razer Anansi
*   Razer BlackWidow Chroma
*   Razer BlackWidow Chroma (Overwatch)
*   Razer BlackWidow Chroma V2
*   Razer BlackWidow Classic
*   Razer BlackWidow Classic (Alternate)
*   Razer BlackWidow Tournament Edition Chroma
*   Razer BlackWidow Ultimate 2012
*   Razer BlackWidow Ultimate 2013
*   Razer BlackWidow Ultimate 2016
*   Razer BlackWidow X Chroma
*   Razer BlackWidow X Tournament Edition Chroma
*   Razer BlackWidow X Ultimate
*   Razer Blade (Late 2016)
*   Razer Blade Pro (Late 2016)
*   Razer Blade QHD
*   Razer Blade Stealth
*   Razer Blade Stealth (Late 2016)
*   Razer Blade Stealth (Mid 2017)
*   Razer DeathStalker Chroma
*   Razer DeathStalker Expert
*   Razer Orbweaver Chroma
*   Razer Ornata
*   Razer Ornata Chroma

#### Mice

*   Razer Abyssus 2014
*   Razer Abyssus V2
*   Razer DeathAdder Chroma
*   Razer DeathAdder Elite
*   Razer Diamondback Chroma
*   Razer Imperator 2012
*   Razer Mamba 2012 (Wired)
*   Razer Mamba 2012 (Wireless)
*   Razer Mamba Tournament Edition
*   Razer Mamba (Wired)
*   Razer Mamba (Wireless)
*   Razer Naga 2014
*   Razer Naga Chroma
*   Razer Naga Hex
*   Razer Naga Hex (Red)
*   Razer Naga Hex V2
*   Razer Orochi 2011
*   Razer Orochi 2013
*   Razer Orochi (Wired)
*   Razer Ouroboros 2012
*   Razer Taipan

#### Mousemats

*   Razer Firefly

#### Other devices

*   Razer Chroma Mug Holder
*   Razer Core
*   Razer Nostromo
*   Razer Orbweaver
*   Razer Tartarus
*   Razer Tartarus Chroma

### Installation

[Install](/index.php/Install "Install") the [openrazer-meta](https://aur.archlinux.org/packages/openrazer-meta/) package. Don't forget to add your current user to the group `plugdev` with the command `sudo gpasswd -a $USER plugdev` and logging out and back in.

### How to use

The recommended way is to use a graphical front-end for interfacing with the drivers.

*   [polychromatic](https://aur.archlinux.org/packages/polychromatic/): A WebKit-based front-end featuring profiles
*   [razergenie](https://aur.archlinux.org/packages/razergenie/): A Qt-based front-end
*   [razercommander](https://aur.archlinux.org/packages/razercommander/): A GTK-based front-end

### Troubleshooting

Visit the [Troubleshooting page](https://github.com/openrazer/openrazer/wiki/Troubleshooting) in the OpenRazer wiki.

## Razer keyboards

There are currently two Python scripts available to enable the extra M1 - M5 macro keys, that certain Razers have, under Linux: Note that this does not allow to assign any content to Macro keys, it merely will enable the sending of keycodes. For Razers without M1 -M5 extra keys there is no point using this tool.

### Blackwidow Control

#### Features

*   confirmed to work with regular BlackWidow, BlackWidow 2013 and BlackWidow Ultimate Stealth 2014
*   should also work with BlackWidow Ultimate, BlackWidow Ultimate 2013 and BlackWidow 2014
*   does not work with BlackWidow (Ultimate) 2016 yet
*   uses Python 3
*   allows to control the status of the LED
*   contains a file with udev rule so macro keys will be enabled automatically when the keyboard is plugged in

#### How to Use

Install it from AUR [blackwidowcontrol](https://aur.archlinux.org/packages/blackwidowcontrol/) After install run as root

```
$ blackwidowcontrol -i

```

Then use the shortcut utility of your Desktop Enviroment to map the keys, i.e. to actually use the macro keys for something useful. For example, the "KDE global shortcuts" GUI (find it in system settings) can assign macros to a key on any keyboard, not just Razers.

### Blackwidow macro scripts

#### Features

*   Works with BlackWidow Ultimate and Stealth 2013 (unknown whether it works with other versions or keyboard models)
*   adding the "021e" ID for Ornata Chroma makes the Game-mode feature (white "G" LED) work on Ornata Chroma as well.
*   Uses Python 2
*   Bundles scripts to create and execute macros

## Troubleshooting

### Mouse randomly stops working

**Note:** This is tested on [ASUS N550JV](/index.php/ASUS_N550JV "ASUS N550JV") using mouse **Razer Orochi 2013**. Laptop probably has faulty charging port and therefore it sometimes directly affects connected mouse USB port and causes similar issues.

If your razer mouse stops working after some time, however, led flashes or lights up, but reboot and re-plugging does not help, try the following commands.

Unload `ehci_pci` and `ehci_hcd` modules:

```
# rmmod ehci_pci
# rmmod ehci_hcd

```

Disconnect the mouse, wait a few seconds and run the following commands to load modules back:

```
# modprobe ehci_hcd
# modprobe ehci_pci

```

Connect the mouse and it should be working.