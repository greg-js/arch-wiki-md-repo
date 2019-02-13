| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Backlight | Working with workaround, see notes |
| Touchscreen | Working |
| Stylus | Working | xf86-input-wacom |
| Wireless | Working with workaround, see notes | r8723bs |
| Audio | Working |
| Battery Status | Working |
| Camera | Not working |
| Bluetooth | Working | r8723bs |
| MicroSD Reader | Working |
| Power Management | Seems to work fine |
| Accelerometer | Working |
| Hardware Buttons | Working |

The Nuvision Solo 10 Draw is a [Tablet PC](/index.php/Tablet_PC "Tablet PC") device, equipped with a 10.1 inch touchscreen display that supports 1920 x 1200 pixels. It also has support for N-Trig Pens like the ones for Microsoft Surface.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 System Specifications](#System_Specifications)
*   [2 Installation](#Installation)
*   [3 On-Screen Keyboard](#On-Screen_Keyboard)
*   [4 Backlight](#Backlight)
*   [5 Wireless](#Wireless)
*   [6 Accelerometer](#Accelerometer)

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