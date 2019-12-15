Related articles

*   [Lenovo ThinkPad X1 Carbon (Gen 7)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_7) "Lenovo ThinkPad X1 Carbon (Gen 7)")

The Lenovo ThinkPad X1 Yoga, 4th generation is a 2-in-1 convertible laptop introduced in late 2019\. Its design is closely related to the [Lenovo ThinkPad X1 Carbon (Gen 7)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_7) "Lenovo ThinkPad X1 Carbon (Gen 7)"). It features a 14" screen, 8th-gen Intel Core processors and integrated [Intel UHD 620 graphics](/index.php/Intel_graphics "Intel graphics").

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# dmidecode -t system | grep Version
        Version: ThinkPad X1 Yoga 4th

```

| **Device** | **Working** | **Modules** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes | i915, (intel_agp) |
| [Wireless network](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes | iwlmvm |
| Native Ethernet with [included dongle](https://www3.lenovo.com/us/en/accessories-and-monitors/cables-and-adapters/adapters/CABLE-BO-TP-OneLink%2B-to-RJ45-Adapter/p/4X90K06975) | Yes | ? |
| Mobile broadband Fibocom | No¹ | ? |
| Audio | Yes | snd_hda_intel |
| Microphone | No⁴ | snd_sof, snd_sof_intel_hda |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes | psmouse, rmi_smbus, i2c_i801 |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes | psmouse, rmi_smbus, i2c_i801 |
| Camera | Yes | uvcvideo |
| [Fingerprint reader](/index.php/Fprint "Fprint") | No² | ? |
| [Power management](/index.php/Power_management "Power management") | Yes³ | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes | btusb |
| NFC | No | ? |
| Keyboard backlight | Yes | thinkpad_acpi |
| Function/Multimedia keys | Yes | ? |
| 

1.  No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.
2.  An official driver and a reverse engineered driver are in the works [[1]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181) (*06cb:00bd*). See [#Fingerprint sensor](#Fingerprint_sensor)
3.  S3 suspend requires changes to BIOS settings, see section on [enabling S3](#Enabling_S3).
4.  The internal microphone doesn't work on versions of the [linux](https://www.archlinux.org/packages/?name=linux) kernel before 5.3\. On version 5.3 and newer the SOF firmware can be enabled by installing [sof-firmware](https://www.archlinux.org/packages/?name=sof-firmware). However, the latest version of sof-fimrware requires Kernel 5.5 and additional udev rules. The X1 Carbon (Gen 7) seems to have the same issue. See the [Talkpage for X1 Carbon (Gen 7)](/index.php/Talk:Lenovo_ThinkPad_X1_Carbon_(Gen_7)#Microphone "Talk:Lenovo ThinkPad X1 Carbon (Gen 7)").

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BIOS](#BIOS)
    *   [1.1 Updates](#Updates)
        *   [1.1.1 Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service))
    *   [1.2 BIOS hanging, not booting into bootloader](#BIOS_hanging,_not_booting_into_bootloader)
    *   [1.3 Sleep/Suspend](#Sleep/Suspend)
    *   [1.4 S3 Suspend Bug with Bluetooth Devices](#S3_Suspend_Bug_with_Bluetooth_Devices)
    *   [1.5 Enabling S3](#Enabling_S3)
*   [2 Audio](#Audio)
    *   [2.1 Volume controls](#Volume_controls)
        *   [2.1.1 Persistent fix](#Persistent_fix)
*   [3 Tablet Functions](#Tablet_Functions)
    *   [3.1 Stylus](#Stylus)
    *   [3.2 Screen Rotation](#Screen_Rotation)
        *   [3.2.1 Automatic Screen Rotation in Gnome](#Automatic_Screen_Rotation_in_Gnome)
        *   [3.2.2 With Screen Rotator](#With_Screen_Rotator)
*   [4 Touchpad](#Touchpad)
*   [5 Fingerprint sensor](#Fingerprint_sensor)
*   [6 Configuration](#Configuration)

## BIOS

### Updates

#### Automatic (Linux Vendor Firmware Service)

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service (LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and possibly other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

### BIOS hanging, not booting into bootloader

Sometimes, the BIOS just "hangs" and you can't do anything but force-power off. This was fixed in the latest version of the Synaptics touchpad which you can install using fwupdmgr.

### Sleep/Suspend

The BIOS has two "Sleep State" options, Windows and Linux, which you can find in at `Config -> Power -> Sleep State`. The Linux option is the traditional S3 power state where all hardware components are turned off except for the RAM, and it should work normally. The Windows option is a newer software-based "modern standby" which works on Linux (despite the name). One possible benefit to the Windows sleep state is faster wake up time, and one possible drawback is increased power usage.

### S3 Suspend Bug with Bluetooth Devices

Occasionally your Thinkpad will wake up immediately after suspending with certain [bluetooth](/index.php/Bluetooth "Bluetooth") devices added. To prevent this, remove the devices or disable [bluetooth](/index.php/Bluetooth "Bluetooth") before suspending.

### Enabling S3

The BIOS has two "Sleep State" options, Windows and Linux, which you can find in at `Config -> Power -> Sleep State`. The Linux option is the traditional S3 power state where all hardware components are turned off except for the RAM, and it should work normally. The Windows option is a newer software-based "modern standby" which works on Linux (despite the name). One possible benefit to the Windows sleep state is faster wake up time, and one possible drawback is increased power usage.

Reboot and verify whether S3 is working by running:

```
 dmesg | grep -i "acpi: (supports"

```

You should now see something like this:

```
 [    0.230796] ACPI: (supports S0 S3 S4 S5)

```

## Audio

As there are physically four loudspeakers, you need to configure to 4.0 audio output. When using PulseAudio there are various [configuration utilities](/index.php/PulseAudio#Front-ends "PulseAudio").

### Volume controls

In order for volume controls to work correctly you must edit `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common` by adding the following above `[Element PCM]`:

```
[Element Master]
switch = mute
volume = ignore

```

A PulseAudio restart is required for this change to take affect. Make sure to increase the "*Master*" channel volume to 100% for the top-firing speakers to work (using amixer or alsamixer, found in [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)).

#### Persistent fix

Upgrading or reinstalling [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) will overwrite this file, and [PulseAudio doesn't appear to offer another way](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/PulseAudioStoleMyVolumes/) to make this configuration change. To prevent pacman from overwriting the file, add the following line under `[options]` in `/etc/pacman.conf`:

```
NoUpgrade = usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common

```

## Tablet Functions

For the most part, the touch screen and stylus work under Xorg after installing [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) package with no issues. See [Tablet PC](/index.php/Tablet_PC "Tablet PC") for further information.

### Stylus

The default stylus buttons are mapped by the wacom driver as follows:

| **Physical Button** | **Xorg mouse number** |
| Top | 2 |
| Bottom | "Eraser" |

These can be changed with xsetwacom. To set the top button of the stylus to the equivalent of a middle click or Xorg mouse button 3:

```
 xsetwacom --set "Wacom Pen and multitouch sensor Pen stylus" Button 2 3

```

To register the "eraser" as a right click use:

```
 xsetwacom --set "Wacom Pen and multitouch sensor Pen eraser" Button 1 2

```

### Screen Rotation

#### Automatic Screen Rotation in Gnome

The iio-sensor-proxy package provides automatic screen rotation for me in Gnome. The package is available in the community repo

```
sudo pacman -S iio-sensor-proxy 

```

No configuration was needed for my machine.

#### With Screen Rotator

Automatic screen rotation works well with ScreenRotator which has no configuration necessary. The touchscreen two finger swipe does not follow rotation at this time. Install [iio-sensor-proxy-git](https://aur.archlinux.org/packages/iio-sensor-proxy-git/) and [screenrotator-git](https://aur.archlinux.org/packages/screenrotator-git/). For KDE, there is [kded-rotation-git](https://aur.archlinux.org/packages/kded-rotation-git/).

**Note:** [ScreenRotator](https://github.com/GuLinux/screenrotator) is in early development stages.

## Touchpad

Sometimes after a boot, the touchpad doesn't work. This was fixed in the latest firmware for the Synaptics device which you can install using fwupdmgr.

## Fingerprint sensor

Warning : this is for testing only !

Solution was found for the next version v2.0 of libfprint in [this issue](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181).

## Configuration

Many of the configuration options can be found in [Lenovo ThinkPad X1 Carbon (Gen 7)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_7) "Lenovo ThinkPad X1 Carbon (Gen 7)"), as the X1 Carbon 7 has a very similar structure to the X1 Yoga 4.