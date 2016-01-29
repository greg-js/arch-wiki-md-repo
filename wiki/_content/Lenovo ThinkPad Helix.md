# Lenovo ThinkPad Helix

<caption>Hardware Information</caption>
| Form Factor | Tablet/Ultrabook Convertible (detachable keyboard dock) |
| Display | 11.6" 1920x1080 LCD with Capacitive and Pen Digitizers |
| CPU | 3rd Generation (Ivy Bridge) Core i5-3427U or i7-3667U |
| RAM | 4GiB (i5) or 8GiB (i7) DDR3L RAM (dependent upon CPU) |
| Storage | 128/160/256GB mSATA SSD |
| WiFi | Intel Centrino Advanced-N 6205S mPCI WLAN |
| Bluetooth | Broadcom BCM20702 Bluetooth 4.0 (USB connected) |
| Camera | 5MP Rear and 2MP Front (also USB) |

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware Configuration](#Hardware_Configuration)
    *   [2.1 Bluetooth](#Bluetooth)
    *   [2.2 Digitizers](#Digitizers)
        *   [2.2.1 Udev Configuration](#Udev_Configuration)
        *   [2.2.2 Xorg Configuration](#Xorg_Configuration)
        *   [2.2.3 Touchscreen / Wacom Tips & Tricks](#Touchscreen_.2F_Wacom_Tips_.26_Tricks)
            *   [2.2.3.1 thinkpad-helix-utils: Toggle Touch](#thinkpad-helix-utils:_Toggle_Touch)
            *   [2.2.3.2 xnohands](#xnohands)
    *   [2.3 Screen Rotation](#Screen_Rotation)
    *   [2.4 Enable SSD TRIM](#Enable_SSD_TRIM)
*   [3 BIOS/Firmware Updates](#BIOS.2FFirmware_Updates)

## Installation

**Note:** As this model includes no physical recovery media, it's highly recommended to create a Windows reinstallation flash drive just in case using the recovery media creation tool included with your preinstalled Windows system.

Due to the fact that there is no optical drive, you need to [install Arch from USB stick](/index.php/USB_Installation_Media "USB Installation Media").

The Arch install media will happily boot under UEFI, so it is recommended to disable legacy boot in the system setup utility. If legacy boot is needed for some reason, it does work fine as well.

Booting using [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") works perfectly. Again, if legacy boot is needed, [GRUB](/index.php/GRUB "GRUB") is perfectly functional as well.

## Hardware Configuration

To fully support all hardware in X, one needs to ensure that the following driver packages are installed:

*   [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) (for the clickpad)
*   [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) (for the digitizers)
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) (for the GPU)

Nearly everything works fine with no special configuration. The sensors (accelerometer, gyroscope, magnetometer, ambient light sensor) don't seem to be recognized yet.

### Bluetooth

If the Broadcom USB device isn't showing up, you likely need to turn it on with `echo 1 > /sys/devices/platform/thinkpad_acpi/rfkill/rfkill0/state`

### Digitizers

The Lenovo Helix comes with the following input devices (the ids may not be the same on your system):

```
$ xinput list
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ Wacom ISDv4 EC Pen stylus               	id=15	[slave  pointer  (2)]
⎜   ↳ Atmel Atmel maXTouch Digitizer          	id=16	[slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad              	id=18	[slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                   	id=19	[slave  pointer  (2)]
⎜   ↳ Wacom ISDv4 EC Pen eraser               	id=21	[slave  pointer  (2)]

```

A Wacom USB device recognized by the [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) driver will create multiple X input devices from a single kernel device. In the Lenovo Helix's case, three such X input devices are created when properly configured:

*   Wacom ISDv4 EC Pen stylus
*   Wacom ISDv4 EC Pen eraser
*   Atmel Atmel maXTouch Digitizer

The **Wacom ISDv4 EC Pen stylus** xinput device is recognized by the [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) driver out of the box. However, additional [Udev](/index.php/Udev "Udev") and [Xorg](/index.php/Xorg "Xorg") configuration is required to recognize the **Atmel Atmel maXTouch Digitizer** touchscreen device as well as **Wacom ISDv4 EC Pen eraser** input if using a pen with an eraser function.

#### Udev Configuration

With an up-to-date Arch install, install the following packages:

*   [libwacom](https://www.archlinux.org/packages/?name=libwacom)
*   [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/)<sup><small>AUR</small></sup>

The [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/)<sup><small>AUR</small></sup> package installs the additional [Udev](/index.php/Udev "Udev") rules. The [libwacom](https://www.archlinux.org/packages/?name=libwacom) package is suggested by some graphics applications to see the additional inputs.

[Udev](/index.php/Udev "Udev") should automatically detect the changes if already running. But, you may want to reboot your system to verify the changes stick.

Additionally, you may want to read the [Wacom_Tablet#Dynamic_with_udev](/index.php/Wacom_Tablet#Dynamic_with_udev "Wacom Tablet") section to ensure the two wacom input devices are found. On this Helix system, it looks like this:

```
$ ls -l /dev/input/wacom* 
lrwxrwxrwx 1 root root 6 Jan 20 15:32 /dev/input/wacom -> event5
lrwxrwxrwx 1 root root 6 Jan 20 15:32 /dev/input/wacom- -> event5

```

These two inputs are the pen and eraser, respectfully.

You can also see if the touchscreen was detected properly:

```
$ ls -l /dev/input/tablet-*
lrwxrwxrwx 1 root root       6 Jan 20 15:32 tablet-tpc-ec- -> event5

```

With these three inputs, you can continue to the next section to configure Xorg.

#### Xorg Configuration

Next, you'll need to tell [Xorg](/index.php/Xorg "Xorg") to use the new inputs. The [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) driver package has an up-to-date list of devices that the Helix has. But, the package does not install the updated list by default. You'll need to link it for Xorg to see them:

```
# ln -s /usr/share/X11/xorg.conf.d/50-wacom.conf /etc/X11/xorg.conf.d/50-wacom.conf

```

Once done with all the above, reboot and you verify `xinput list` looks the same as the above.

#### Touchscreen / Wacom Tips & Tricks

If you find yourself frustrated by the capacitive digitizer while trying to use the pen, there are a few options as outlined below that can help.

##### thinkpad-helix-utils: Toggle Touch

The [thinkpad-helix-utils](https://aur.archlinux.org/packages/thinkpad-helix-utils/)<sup><small>AUR</small></sup> package contains a script located at `/usr/bin/helix-toggle-touch` that will toggle the capacitive digitizer on and off with a simple command using Xorg's **xinput** function. It also installs a `desktop` file called **Toggle Touch** that can be used to toggle xinput on and off with the pen.

Once activated, it disables the touchscreen xinput device until it is ran again to re-activate it.

##### xnohands

Another option that also uses Xorg's **xinput** is [xnohands](http://sourceforge.net/projects/xournal/files/xnohands/). This utility disables the touch device in a system when a stylus is detected (either pen or eraser) and re-enables the touchscreen once then stylus is pulled away from the screen. It does this by listening to the digitizer's "presence" event, which the Helix's Wacom ISDv4 EC input devices support. You'll need to download and extract it. Follow the README for instructions as it outlines how to set it up.

NOTE: You must have followed the udev and xorg configuration instructions earlier to have both the Pen and Eraser detected, as well as the touchscreen (all three must be detected); or else, this tool will not work.

If you want it always running, install the desktop file in your autostart to have it run on startup:

```
$ cp xnohands.desktop ~/.config/autostart/

```

Please note that you can have both the thinkpad-helix-utils **Toggle Touch** and **xnohands** installed; but, do not use both at the same time. **xnohands** will "re-activate" the touchscreen as soon as you pull the pen away from the screen, defeating the purpose of **Toggle Touch** to keep touch disabled at all times.

### Screen Rotation

If you have both digitizers configured through the xf86-input-wacom driver, they will automatically rotate with the display and you can use a simple command like `xrandr --output eDP1 --rotate left` to rotate the screen with ease.

If you want to use the bezel buttons (or some other hotkey) to cycle through orientations (or toggle between two specific ones), `helix-rotate`, also from from [thinkpad-helix-utils](https://aur.archlinux.org/packages/thinkpad-helix-utils/)<sup><small>AUR</small></sup>, provides an easy-to-bind command that may serve your needs well.

There is also [Magick Rotation](https://launchpad.net/magick-rotation/), which is supposed to automatically rotate the screen based on input events, but it only seems to respond to docking/undocking the tablet.

### Enable SSD TRIM

The built in 128 GB and 256 GB mSATA SSDs included with the Helix all support SSD TRIM functions.

Follow the [Solid_State_Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives") instructions to enable trim. For example, one could use **fstrim** and set it up weekly like so:

```
# systemctl enable fstrim.timer
# systemctl start fstrim.timer

```

## BIOS/Firmware Updates

Helpfully, Lenovo now provides [bootable ISO images](http://support.lenovo.com/en_US/downloads/detail.page?DocID=DS034628) for the purpose of installing BIOS updates. While it is not stated on their site, these bootable images also include updated firmware for the keyboard dock MPU. It is uncertain as to whether the USB hub firmware is also updated via this utility.

**Note:** While the update utility states that all expansion units should be disconnected, it is only referring to external (USB and DisplayPort) devices. Ensure that the tablet is in the dock and connected only to AC power and the utility boot media before starting the process.

If you do not have access to a USB optical drive and writable media, the information on [ThinkWiki](http://www.thinkwiki.org/wiki/BIOS_Upgrade/X_Series) is extremely helpful.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Helix&oldid=416940](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Helix&oldid=416940)"