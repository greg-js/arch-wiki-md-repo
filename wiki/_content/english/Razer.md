There are currently no official drivers for any Razer peripherals in Linux. However, Michael Buesch has created a tool called [razercfg](http://bues.ch/cms/hacking/razercfg.html) to configure Razer mice under Linux. There also exist scripts to enable macro keys of Razer keyboards.

## Contents

*   [1 Razer Peripherals](#Razer_Peripherals)
    *   [1.1 Compatibility](#Compatibility)
    *   [1.2 Installation](#Installation)
    *   [1.3 Using the Razer Configuration Tool](#Using_the_Razer_Configuration_Tool)
*   [2 Razer Blade](#Razer_Blade)
    *   [2.1 2016 version (Razer Blade & Razer Blade Stealth)](#2016_version_.28Razer_Blade_.26_Razer_Blade_Stealth.29)
        *   [2.1.1 Killer Wireless Network Adapter](#Killer_Wireless_Network_Adapter)
        *   [2.1.2 Touchpad](#Touchpad)
        *   [2.1.3 Graphics Drivers](#Graphics_Drivers)
        *   [2.1.4 Hybrid graphics](#Hybrid_graphics)
        *   [2.1.5 Suspend Loop](#Suspend_Loop)
        *   [2.1.6 Tweaking](#Tweaking)
        *   [2.1.7 Unresolved Issues](#Unresolved_Issues)
    *   [2.2 2014 version](#2014_version)
        *   [2.2.1 Problems](#Problems)
        *   [2.2.2 Possible trackpad solution](#Possible_trackpad_solution)
    *   [2.3 2013 version](#2013_version)
        *   [2.3.1 What works](#What_works)
        *   [2.3.2 Problems](#Problems_2)
        *   [2.3.3 Possible trackpad solution](#Possible_trackpad_solution_2)
*   [3 Razer keyboards](#Razer_keyboards)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Mouse randomly stops working](#Mouse_randomly_stops_working)

## Razer Peripherals

### Compatibility

*razercfg* lists the following mice models as stable:

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

## Razer Blade

Razer Blade is Razer's line of gaming laptops. There is currently a 14" model, and a 17" model. Due to the proprietary SBUI trackpad on the 17" model, it will be extremely difficult to get it to work without extensive USB protocol reversing.

### 2016 version (Razer Blade & Razer Blade Stealth)

The normal installation process works in general with the exceptions enumerated below.

#### Killer Wireless Network Adapter

The wireless adapter won't work without proprietary firmware. You will require a USB ethernet adapter to do the installation or an ISO with the proprietary driver installed. The wireless adapter presents itself as

```
01:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

It is a [Killer Wireless-AC 1535](http://www.killernetworking.com/product-support/knowledge-base/17-linux/20-killer-wireless-ac-in-linux-ubuntu-debian) which requires proprietary firmware for the board. The latest 4.4.1 kernel only requires the *board.bin* to be overwritten.

```
# wget -O /lib/firmware/ath10k/QCA6174/hw3.0/board.bin http://www.killernetworking.com/support/K1535_Debian/board.bin

```

Or use the [Installer Script](https://github.com/stuartwells4/razer-laptop/tree/master/stealth) at your own risk.

To improve WiFi stability, go into the BIOS and ENABLE WiFi Firmware loading. This loads the wireless firmware at boot, which prevents the WiFi from failing to initiate at boot.

#### Touchpad

[Install](/index.php/Install "Install") the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package. See [Libinput](/index.php/Libinput "Libinput") for more information on this driver.

Alternatively, if you prefer using the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") driver, [install](/index.php/Install "Install") the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package.

#### Graphics Drivers

The graphics card works OK with the standard intel drivers which you can [install](/index.php/Install "Install") with the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. See [Intel graphics](/index.php/Intel_graphics "Intel graphics") for more information on installation and configuration.

Issues with screen flickering seem to be resolved by changing *AccelMethod* to *uxa* as described in the [SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics") section.

```
# cat >/etc/X11/xorg.conf.d/20-intel.conf 
Section "Device"
  Identifier  "Intel Graphics"
  Driver      "intel"
  Option      "AccelMethod"  "uxa"
  #Option      "AccelMethod"  "sna"
EndSection

```

#### Hybrid graphics

If the discrete Nvidia GPU is switched off before starting Xorg or Wayland, then the system freezes. The only possible solution is to manually disable/enable the discrete card after starting the graphical session. However there is a ACPI DSDT fix available which fixes this problem. Check the [repository](https://github.com/m4ng0squ4sh/razer_blade_14_2016_acpi_dsdt) for more information.

#### Suspend Loop

Suspending (Close laptop lid) does not seem to work with a basic installation. You can suspend but once the system resumes it suffers from random suspends or the screen going blank for no apparent reason.

A temporary fix is to disable the automatic systemd suspend action by chaning the *HandleLidSwitch* value in the */etc/systemd/logind.conf* file:

```
HandleLidSwitch=ignore

```

#### Tweaking

If you are using [GNOME](/index.php/GNOME "GNOME"), the *gnome-tweak-tool* can be used to adjust the window and font scaling. A font scale of *1.25* puts the font sizes closer to how they are displayed by default in Windows 10.

If you are using an external monitor that is not [HiDPI](/index.php/HiDPI "HiDPI"), you can use *xrandr* to alter the scaling of the external monitor using the instructions for [Multiple Displays](/index.php/HiDPI#Multiple_displays "HiDPI"). You may have better results though running [GNOME](/index.php/GNOME "GNOME") on [Wayland](/index.php/Wayland "Wayland"). When installed, clicking the gear icon in [GDM](/index.php/GDM "GDM") will allow you to select *Gnome On Wayland* and will default to that in the future.

#### Unresolved Issues

*   the webcam does not seem to work with a basic installation. External webcams work fine. It seems to fail when the resolution is anything but 640x480\. [guvcview](https://www.archlinux.org/packages/?name=guvcview) works because it defaults to the resolution. [cheese](https://www.archlinux.org/packages/?name=cheese) and [Google Hangouts](https://hangouts.google.com) do not because they default to the max resolution.

### 2014 version

#### Problems

[Source](http://forum.notebookreview.com/razer/751074-2014-razer-blade-14-linux.html)

*   touchpad (multitouch, although this may be a kernel bug that has since been fixed)
*   keys to increase/decrease screen illumination not working
*   keys to increase/decrease keyboard illumination not working

#### Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone [https://github.com/aduggan/hid-rmi.git](https://github.com/aduggan/hid-rmi.git) -b rb14 # and then install it
depmod -a

```

Then [install](/index.php/Install "Install") the [synaptics](https://www.archlinux.org/packages/?name=synaptics) package.

Feature still not working: pinch to zoom, 3rd mouse button.

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

```

Then [install](/index.php/Install "Install") the [synaptics](https://www.archlinux.org/packages/?name=synaptics) packages.

Feature still not working: pinch to zoom, 3rd mouse button

## Razer keyboards

There are currently two Python scripts available to enable macro keys under Linux:

*   [blackwidowcontrol](https://aur.archlinux.org/packages/blackwidowcontrol/)
    *   works with regular BlackWidow and BlackWidow 2013
    *   might work with BlackWidow Ultimate (2013), too
    *   does not work with BlackWidow (Ultimate) 2016 yet
    *   uses Python 3
    *   does not bundle any scripts to create macros (use hot key configuration tool from your desktop environment)
    *   allows to control the status of the LED
*   [razer-blackwidow-macro-scripts](https://aur.archlinux.org/packages/razer-blackwidow-macro-scripts/)
    *   works with BlackWidow Ultimate 2013 (unknown whether it works with other versions)
    *   uses Python 2
    *   also bundles scripts to create and execute macros

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