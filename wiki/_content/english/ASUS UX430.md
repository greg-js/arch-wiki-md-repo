## Contents

*   [1 Specifications](#Specifications)
*   [2 Booting from USB](#Booting_from_USB)
*   [3 Installing the system](#Installing_the_system)
*   [4 What Works and What Doesn't](#What_Works_and_What_Doesn.27t)
*   [5 Post Installation Steps and Microcode Updates](#Post_Installation_Steps_and_Microcode_Updates)
*   [6 Configuring Video](#Configuring_Video)
*   [7 Configuring Audio](#Configuring_Audio)
*   [8 Battery Life](#Battery_Life)
    *   [8.1 TLP](#TLP)
    *   [8.2 Powertop](#Powertop)
    *   [8.3 Power Saving](#Power_Saving)
*   [9 Input Devices](#Input_Devices)
*   [10 Hard Drive / SSD](#Hard_Drive_.2F_SSD)

## Specifications

The UX430UA that was used to write this article features the following:

```
- Corei5 - 7200U 2.5Ghz - 3.1Ghz Dual Core
- 8GB DDR3 RAM
- 256GB SATA3 M.2 SSD
- Intel HD 620 Graphics (64MB Allocated in Bios)
- No Backlit Keyboard nor Fingerprint Sensor

```

Asus released the UX430 Ultrabook in 2017\. Whilst it worked out of the box with Linux, there may be some customizations to make the system better. This page will be updated (bare with me, first page submission) as I find more issues and fixes.

## Booting from USB

Assuming you've already disabled SecureBoot, pressing Escape while booting the machine will show the boot menu with all devices that can be booted from, plus an option to Enter Setup

## Installing the system

Before installing Arch onto the UX430, It is highly recommended that the BIOS is updated. The laptop shipped with version 201, but there is an upgrade to version 300 via the ASUS website. Version 300 states that it optimizes performance of the device (for the UA model at least) and I have personally noticed that the fan and heat on the device is not as hot as on version 201.

```
[UX430UA BIOS](https://www.asus.com/Laptops/ASUS-ZenBook-UX430UA/HelpDesk_BIOS/)

```

```
[UX430UQ BIOS](https://www.asus.com/Laptops/ASUS-ZenBook-UX430UQ/HelpDesk_BIOS/)

```

Installation of Arch Linux worked without a hitch following the standard installation procedure. Before installation, you'll need to ensure that you disable SecureBoot as it won't allow Linux to load if it is on. CSM can stay on, and so can FastBoot as they do not affect installation or running of Linux.

```
- Boot Machine : Press Escape to Enter EUFI Bios - Security Tab: Secure Boot = Off

```

You can then boot in and install as per the Installation guide, or manually if you know how to. If you are using a distribution such as Antergos, the installation via GUI will work without issues as well.

Installation media has not been checked with USB-C but works with USB 3.1 and USB 2.0 ports.

## What Works and What Doesn't

**Works:**

*   Audio
*   Video
*   Touchpad
*   USB Ports (All)
*   MicroHDMI Port
*   WIFI
*   Bluetooth
*   Webcam
*   Function Keys

**Doesn't Work:**

*   Ambient Light Sensor

## Post Installation Steps and Microcode Updates

Depending on your distribution, you should find that Bluetooth works fine (tested with Bluez-* on KDE), sound works fine (more on that below), Graphics are working fine (more on that below), and Battery life is exceptional(again more on that below).

It is however recommended before continuing, to also update the [Microcode](/index.php/Microcode "Microcode") for your processor. Check the page for more details on how to apply this for Intel CPUs.

## Configuring Video

Configuring the Video is extremely easy on this device. Installing Xorg-Server will automatically detect that you have an Intel GPU (for the UA model) and install xf86-video-intel. I personally remove this and use the MODSET drivers as they are more reliable, but tests have not been done to see which is more reliable. There was no discernible difference using either.

Check out the [Intel Graphics](/index.php/Intel_graphics#Installation "Intel graphics") section for more information

Check out the [Hardware Acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") section for Video Acceleration

## Configuring Audio

When using Audio, the speakers on this Ultrabook are loud and ultra clear. You may notice though that the audio through the Headphones is extremely low. In order to combat this, simply add the following to /etc/modprobe.d/alsa-base.conf:

```
options snd-hda-intel mode=Laptop

```

The [ALSA](/index.php/ALSA "ALSA") page can help with this, and it is highly recommended to install [PulseAudio](/index.php/PulseAudio "PulseAudio") though Environments such as KDE come with this by default.

## Battery Life

This laptop is capable of presenting 6 - 9 hours of battery life, depending on the load on the machine. This is for the UX430UA with Intel HD 620 graphics. Battery may differ on the UQ which has the 940MX graphics card from NVidia.

### TLP

Using TLP the machine managed to push from 4hrs on average to 7hrs on average. See the [TLP](/index.php/TLP "TLP") Page for more information

### Powertop

Using Powertop also increased life by around 30 minutes though once TLP was enabled most of the tunable variables were set to "Good" automatically. More information here: [Powertop](/index.php/Powertop "Powertop")

### Power Saving

More information can be found under the [Power Saving](/index.php/Power_Saving "Power Saving") section

## Input Devices

By default (as expected) the Elan touchpad works but is far too sensitive. Depending on your Desktop Environment you may be able to edit these settings, or may need additional software. For myself on KDE , I had to install the KCM LibInput package from the AUR. More information can be found on the [Libinput](/index.php/Libinput "Libinput") page

## Hard Drive / SSD

Since this machine comes with an M.2 SSD by default, it's recommended to check out [SSD](/index.php/SSD "SSD") section too