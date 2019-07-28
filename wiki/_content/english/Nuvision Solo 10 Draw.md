| **Device** | **Status** | **Modules** |
| Accelerometer | Working |
| Audio | Working |
| Backlight | Working with workaround, see notes |
| Battery Status | Working |
| Bluetooth | Working | r8723bs |
| Cameras | Not working |
| Charging | Working with workaround, see notes | axp288_adc |
| Display | Working | xf86-video-intel |
| Hardware Buttons | Working |
| MicroSD Reader | Working |
| Power Management | Seems to work fine |
| OTG (On-The-Go) | Working with workaround, see notes | extcon-axp288 and intel_cht_int33fe |
| Stylus | Working | xf86-input-wacom |
| Touchscreen | Working |
| Wireless | Working with workaround, see notes | r8723bs |

The Nuvision Solo 10 Draw is a [Tablet PC](/index.php/Tablet_PC "Tablet PC") device, equipped with a 10.1 inch touchscreen display that supports 1920 x 1200 pixels. It also has support for N-Trig Pens like the ones for Microsoft Surface.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 System Specifications](#System_Specifications)
*   [2 Installation](#Installation)
*   [3 On-Screen Keyboard](#On-Screen_Keyboard)
*   [4 Backlight](#Backlight)
*   [5 Stylus](#Stylus)
*   [6 Wireless](#Wireless)
*   [7 Accelerometer](#Accelerometer)
*   [8 Charging](#Charging)
*   [9 OTG (On-The-Go)](#OTG_(On-The-Go))

## System Specifications

*   **CPU:** Intel Atom x5-Z8300 1.44GHz with Intel Burst Technology up to 1.84GHz
*   **GPU:** Intel HD Graphics (Cherry Trail)
*   **Display:** 10.1 inches, 1920x1200, IPS LCD
*   **Dimensions:** 10.25x6.25x0.33in (260.35x158.75x8.38mm), 1.15lbs (0.52kg)
*   **Camera:** 5MP rear, 2MP front
*   **Storage:** 32GB, expandable with Micro SD
*   **RAM:** 2GB
*   **Battery:** 6,800mAh
*   **Ports:** Micro-USB, micro-HDMI, 3.5mm headset

## Installation

**Before continuing make sure your tablet is fully charged!**

As of the 11th of February 2019 there is no known way to charge and have other peripherals attached to OTG at the same time for this particular tablet. This means your tablet will run off battery for the entire length of install time.

This device has a UEFI bootloader and BIOS settings menu but no keyboard included. In order to complete setup you will need a USB Hub, a wired usb keyboard, and a Micro-B OTG (On The Go) cable. But once fully set up you should be able to use the tablet without any extra peripherals.

**These are instructions for booting Arch Linux install environment or any operating system installed to a USB storage device for this particular device.**

Before starting, have your tablet in a powered off state, plug in your OTG cable, USB hub, your keyboard, and the USB storage device where you have Arch Linux install media on.

Power on your tablet and at the moment you see the "Nuvision" boot logo press and hold down the ESC key on your keyboard until you've reached the BIOS menu.

In the BIOS menu navigate right to the 'save & exit' section with the arrow keys. Under 'save & exit' navigate down and under 'boot overrides' find your USB device. Press the enter key to select and boot into the storage device.

At this point your tablet should boot into the Arch Linux install environment. You may continue with the standard [installation guide](/index.php/Installation_guide "Installation guide")

## On-Screen Keyboard

Depending on your preferred window manager, install [kvkbd](https://aur.archlinux.org/packages/kvkbd/) for [KDE](/index.php/KDE "KDE") or [cellwriter](https://www.archlinux.org/packages/?name=cellwriter) for [GNOME](/index.php/GNOME "GNOME"), see [Tablet PC](/index.php/Tablet_PC "Tablet PC")

## Backlight

Due to a bug the 'i915' graphics driver will fail to get control of the backlight with a similar error message to

```
[drm:pwm_setup_backlight [i915]] *ERROR* Failed to own the pwm chip

```

It is possibly the same bug as described here [https://bugs.freedesktop.org/show_bug.cgi?id=96571](https://bugs.freedesktop.org/show_bug.cgi?id=96571)

As a workaround, make sure that graphic module 'i915' is never added to the initramfs or to the 'modules' section of /etc/mkinitcpio.conf This delays the system long enough in finding the correct display driver.

The idea is that 'i915' is loaded too early into the system and 'i915' tries to obtain control over parts of the system that haven't fully loaded yet.

As of the 11th of February 2019, this workaround appears to work fine.

## Stylus

As of July 23, 2019 a patch has been merged fixing stylus support for a number of tablets including the Nuvision Solo 10 Draw. Styluses should now be fully working including styluses that have a eraser end. For [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)>=0.37.0

Until this is added into a new release you'll need to add this file as well. [https://github.com/linuxwacom/xf86-input-wacom/commit/030d272d5d605f9605ed44cdde4856737415a972](https://github.com/linuxwacom/xf86-input-wacom/commit/030d272d5d605f9605ed44cdde4856737415a972)

 `/etc/X11/xorg.conf.d/60-wacom.conf` 
```
Section "InputClass"
        Identifier "Nuvision Solo 10 Draw"
        MatchProduct "04F3200A:00 04F3:22F7"
        MatchDevicePath "/dev/input/event*"
        Driver "wacom"
EndSection
```

## Wireless

Included is a RTL8723BS chipset that supports Wifi and Bluetooth. It appears 2.4GHz is only supported for Wifi.

If you have any issues with connecting to wireless try this workaround. It's a settings change in the BIOS, you want to make sure 'SCC SDIO Support' is set to 'PCI Mode'.

To make that change follow the below guide.

From a powered off state, plug in a wired USB keyboard to a OTG cable and into your tablet.

Power on your tablet and at the moment you see the "Nuvision" boot logo press and hold down the ESC key on your keyboard until you've reached the BIOS menu.

In the BIOS navigate with the arrow keys.

Right to 'Chipset', down to 'South Bridge', down to 'LPSS & SCC Configuration', down to 'SCC SDIO Support' tap enter key and in the popup select 'PCI mode' and enter again.

Tap the ESC key to get back to the top menu and navigate to 'save & exit', then down to 'save changes and exit'.

Wifi should behave much better after this change.

As of the 11th of February 2019, this workaround appears to work fine.

## Accelerometer

Should be working out of the box with [systemd](https://www.archlinux.org/packages/?name=systemd)>=241

If you're running a older systemd you may need to add the following.

 `/etc/udev/hwdb.d/61-sensor-local.hwdb` 
```
sensor:modalias:acpi:KIOX000A*:dmi:*:svnTMAX:pnTM101W610L:*
 ACCEL_MOUNT_MATRIX=0, -1, 0; -1, 0, 0; 0, 0, 1
```

## Charging

As of July 23, 2019 there is a bug with the 'axp288_adc' module. It improperly handles the temperature sensor and sometimes triggers a temperature warning even when no temperature sensor is present. This leads the whole system to stop allowing a charge.

Bug reported at [https://bugzilla.redhat.com/show_bug.cgi?id=1610545](https://bugzilla.redhat.com/show_bug.cgi?id=1610545) there is a upstream patch but it doesn't appear to work correctly, patch at [https://github.com/torvalds/linux/commit/9bcf15f75cac3c6a00d8f8083a635de9c8537799#diff-8bdeb4777214fc30523f85b51c4a1851](https://github.com/torvalds/linux/commit/9bcf15f75cac3c6a00d8f8083a635de9c8537799#diff-8bdeb4777214fc30523f85b51c4a1851)

A workaround mentioned at the previous bug report link appears to help prevent any temperature warnings pertaining to the battery. However it's unclear if this will cause any damage to the battery, it shouldn't since it does not appear this tablet has a functioning temperature sensor for the battery.

Install [i2c-tools](https://www.archlinux.org/packages/?name=i2c-tools) and run the following commands as root. This disables the battery temperature sensor pin, preventing any issues with bogus temperature sensing that stops charging. This workaround appears to work as of July 23, 2019

 `Disable temperature pin` 
```
modprobe i2c-dev

i2cset -y -f 6 0x34 0x82 0xf0

i2cset -y -f 6 0x34 0x84 0xf0
```

You may want to make sure these commands run at boot, see [Autostarting](/index.php/Autostarting "Autostarting") for some ways you can run these commands at boot.

## OTG (On-The-Go)

The drivers and chipset used for this particular tablet do not have automatic switching of OTG modes. It's either in 'device' mode or 'host' mode. If you leave a OTG cable plugged in before booting up the system properly enables 'host' mode. But otherwise the system will be left in 'device' mode and OTG will not work unless it's switched.

However you can run these commands as root to switch the modes as needed.

 `To switch USB OTG port to device mode.`  `echo device > /sys/class/usb_role/intel_xhci_usb_sw-role-switch/role`  `To switch USB OTG port to host mode.`  `echo host > /sys/class/usb_role/intel_xhci_usb_sw-role-switch/role`