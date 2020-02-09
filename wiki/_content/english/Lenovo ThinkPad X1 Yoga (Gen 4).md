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
| Native Ethernet with [dongle](https://www.lenovo.com/us/en/accessories-and-monitors/cables-and-adapters/adapters/CABLE-BO-Ethernet-Extension-Adapter-2/p/4X90Q84427) (sometimes not included) | Yes | ? |
| Mobile broadband Fibocom | ? | ? |
| Audio | Yes | snd_hda_intel |
| Microphone | No³ | snd_sof, snd_sof_intel_hda |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes | psmouse, rmi_smbus, i2c_i801 |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes | psmouse, rmi_smbus, i2c_i801 |
| Camera | Yes | uvcvideo |
| [Fingerprint reader](/index.php/Fprint "Fprint") | No¹ | ? |
| [Power management](/index.php/Power_management "Power management") | Yes² | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes | btusb |
| NFC | ?⁴ | ? |
| Keyboard backlight | Yes | thinkpad_acpi |
| Function/Multimedia keys | Yes | ? |
| 

1.  An official driver and a reverse engineered driver are in the works [[1]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181) (*06cb:00bd*). See [#Fingerprint sensor](#Fingerprint_sensor)
2.  S3 suspend requires changes to BIOS settings, see section on [enabling S3](#Enabling_S3).
3.  The internal microphone doesn't work on versions of the [linux](https://www.archlinux.org/packages/?name=linux) kernel before 5.3\. On version 5.3 and newer the SOF firmware can be enabled by installing [sof-firmware](https://www.archlinux.org/packages/?name=sof-firmware). However, the latest version of sof-fimrware requires Kernel 5.5 and additional udev rules. The X1 Carbon (Gen 7) seems to have the same issue. See the [Talkpage for X1 Carbon (Gen 7)](/index.php/Talk:Lenovo_ThinkPad_X1_Carbon_(Gen_7)#Microphone "Talk:Lenovo ThinkPad X1 Carbon (Gen 7)").
4.  Using latest linux package and [neard](https://aur.archlinux.org/packages/neard/) nfctool detects the device nfc0 and shows supported protocols

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 BIOS](#BIOS)
    *   [2.1 Updates](#Updates)
        *   [2.1.1 Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service))
    *   [2.2 BIOS hanging, not booting into bootloader](#BIOS_hanging,_not_booting_into_bootloader)
    *   [2.3 Sleep/Suspend](#Sleep/Suspend)
    *   [2.4 S3 Suspend Bug with Bluetooth Devices](#S3_Suspend_Bug_with_Bluetooth_Devices)
    *   [2.5 Enabling S3](#Enabling_S3)
*   [3 Audio](#Audio)
*   [4 Tablet Functions](#Tablet_Functions)
    *   [4.1 Stylus](#Stylus)
    *   [4.2 Screen Rotation](#Screen_Rotation)
        *   [4.2.1 Automatic Screen Rotation in Gnome](#Automatic_Screen_Rotation_in_Gnome)
        *   [4.2.2 With Screen Rotator](#With_Screen_Rotator)
*   [5 Touchpad](#Touchpad)
*   [6 Fingerprint sensor](#Fingerprint_sensor)
*   [7 Configuration](#Configuration)

## Hardware

Additional hardware information from `lsusb` and `lspci` can be found below when using the [linux](https://www.archlinux.org/packages/?name=linux) kernel 5.5.1:

`lsusb`

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 04f2:b67c Chicony Electronics Co., Ltd Integrated Camera
Bus 001 Device 002: ID 056a:51b6 Wacom Co., Ltd Pen and multitouch sensor
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

`lspci`

```
00:00.0 Host bridge: Intel Corporation Coffee Lake HOST and DRAM Controller (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 11)
00:13.0 Serial controller: Intel Corporation Cannon Point-LP Integrated Sensor Hub (rev 11)
00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 11)
00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 11)
00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 11)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 11)
00:15.1 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #1 (rev 11)
00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 11)
00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 11)
00:1f.3 Audio device: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 11)
00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 11)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP SPI Controller (rev 11)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (6) I219-V (rev 11)
03:00.0 Non-Volatile memory controller: Sandisk Corp Device 5006
05:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:01.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:02.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
06:04.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:00.0 System peripheral: Intel Corporation JHL6540 Thunderbolt 3 NHI (C step) [Alpine Ridge 4C 2016] (rev 02)
2d:00.0 USB controller: Intel Corporation JHL6540 Thunderbolt 3 USB Controller (C step) [Alpine Ridge 4C 2016] (rev 02)

```

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

Install the latest [linux](https://www.archlinux.org/packages/?name=linux)-kernel and [sof-firmware](https://www.archlinux.org/packages/?name=sof-firmware).

Add to /etc/pulse/default.pa:

```
 load-module module-alsa-source device=hw:0,6 channels=4
 load-module module-alsa-sink device=hw:0,0

```

Add to /etc/modprobe.d/alsa.conf:

```
 options snd slots=,snd_usb_audio

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