<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
    *   [2.1 Booting the install USB](#Booting_the_install_USB)
*   [3 Configuration](#Configuration)
    *   [3.1 TrackPad](#TrackPad)
    *   [3.2 TouchScreen and Stylus](#TouchScreen_and_Stylus)
    *   [3.3 Video](#Video)
    *   [3.4 Audio](#Audio)
        *   [3.4.1 Microphone](#Microphone)
        *   [3.4.2 Speakers](#Speakers)
    *   [3.5 Bluetooth](#Bluetooth)
    *   [3.6 Screen Rotation](#Screen_Rotation)
*   [4 ACPI](#ACPI)
*   [5 Hardware information](#Hardware_information)
*   [6 Troubleshooting](#Troubleshooting)

## Overview

Most functionality works out of the box, a kernel of version 5.4 is recommended due to Ice Lake's new Thunderbolt.

| **Device** | **Status** | **Modules** |
| Graphics | **Working** | i915 |
| Wireless | **Working** | iwlwifi |
| Audio | **Partially Working** | snd_hda_intel |
| Touchscreen | **Working** | wacom |
| Stylus | **Working** ¹ | wacom,usbhid |
| Accelerometer | **Working** | hid_sensor_accel_3d |
| Touchpad | **Working** | psmouse |
| Camera | **Working** | uvcvideo |
| Bluetooth | **Working** | btintel |
| Fingerprint Reader | **Not Working** |

## Installation

Newer kernels boot without problems and the wifi should be available. If you get a blank screen after booting, the power modes are not supported by your kernel; refer to Troubleshooting.

### Booting the install USB

To access the boot menu and BIOS, use "F1". Disable secure boot from the BIOS. UEFI boot mode works fine.

## Configuration

### TrackPad

TrackPad works fine with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

### TouchScreen and Stylus

Touchscreen works with the Wacom driver (package: [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)). Also using the Stylus, the bottom button of the pen is defined as the eraser and the top button works as a middle mouse button

**Note:** See [Tablet PC](/index.php/Tablet_PC "Tablet PC") for more info on optimizing the touchscreen experience.

### Video

The kernel supports Iris Plus Gen11 from version 5.3\. With default configuration, tearing is apparent when playing videos. To fix tearing, create the file `/etc/X11/xorg.conf.d/20-intel.conf` with the following content:

```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "TearFree"    "true"
EndSection

```

That said there seems to be issues with Chromium based GPU acceleration, so either disabling that via Chromium flags, or removing [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Although you will face some tearing unless using [compton](https://www.archlinux.org/packages/?name=compton) or [picom](https://www.archlinux.org/packages/?name=picom).

### Audio

Audio works when using the snd_hda_intel driver, so make a file in `/etc/modprobe.d/alsa-base.conf` with

```
options snd_hda_intel enable=1 index=1

```

However Audio is partially working as there are some limitations.

#### Microphone

Microphone requires the new SOF firmware, I've not experimented with this so I can't really say anything to that.

Bug reports for Microphone

*   [https://bugzilla.kernel.org/show_bug.cgi?id=201251](https://bugzilla.kernel.org/show_bug.cgi?id=201251)
*   [https://github.com/thesofproject/sof/issues/2134](https://github.com/thesofproject/sof/issues/2134)

#### Speakers

Audio is OK, there are 5.1 speakers, 2.1 in the soundbar, and 2 under the palmrest on either side of the laptop. Only the 2 speakers in the soundbar works, and not the subwoofer. This isn't optimal, but Alsa/Pulseaudio report that its a 2 channel audio device. I have read in other articles from other Lenovo devices, like the X1 Yoga that they solve this by making the alsa/pulseaudio use 4 channels instead of 2.. I haven't tried this so I cannot report on it.

Thread on Alsa-devel about 5.1 speakers [https://mailman.alsa-project.org/pipermail/alsa-devel/2018-November/142369.html](https://mailman.alsa-project.org/pipermail/alsa-devel/2018-November/142369.html)

### Bluetooth

The Bluetooth adapter works out of the box.

### Screen Rotation

I personally use [bspwm](https://www.archlinux.org/packages/?name=bspwm) and for that I use [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) and [screenrotator-git](https://aur.archlinux.org/packages/screenrotator-git/). But theres a whole article on this in [Tablet_PC](/index.php/Tablet_PC "Tablet PC").

## ACPI

Suspend on lid works.

Manual fan control does not work at all.

## Hardware information

The output of *lspci* is

```
00:00.0 Host bridge: Intel Corporation Device 8a12 (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Iris Plus Graphics G7 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Device 8a03 (rev 03)
00:07.0 PCI bridge: Intel Corporation Ice Lake Thunderbolt 3 PCI Express Root Port #0 (rev 03)
00:07.1 PCI bridge: Intel Corporation Ice Lake Thunderbolt 3 PCI Express Root Port #1 (rev 03)
00:0d.0 USB controller: Intel Corporation Ice Lake Thunderbolt 3 USB Controller (rev 03)
00:0d.2 System peripheral: Intel Corporation Ice Lake Thunderbolt 3 NHI #0 (rev 03)
00:12.0 Serial controller: Intel Corporation Device 34fc (rev 30)
00:14.0 USB controller: Intel Corporation Ice Lake-LP USB 3.1 xHCI Host Controller (rev 30)
00:14.2 RAM memory: Intel Corporation Device 34ef (rev 30)
00:14.3 Network controller: Intel Corporation Killer Wi-Fi 6 AX1650i 160MHz Wireless Network Adapter (201NGW) (rev 30)
00:15.0 Serial bus controller [0c80]: Intel Corporation Ice Lake-LP Serial IO I2C Controller #0 (rev 30)
00:15.1 Serial bus controller [0c80]: Intel Corporation Ice Lake-LP Serial IO I2C Controller #1 (rev 30)
00:15.2 Serial bus controller [0c80]: Intel Corporation Ice Lake-LP Serial IO I2C Controller #2 (rev 30)
00:16.0 Communication controller: Intel Corporation Management Engine Interface (rev 30)
00:1d.0 PCI bridge: Intel Corporation Ice Lake-LP PCI Express Root Port #9 (rev 30)
00:1f.0 ISA bridge: Intel Corporation Ice Lake-LP LPC Controller (rev 30)
00:1f.3 Multimedia audio controller: Intel Corporation Smart Sound Technology Audio Controller (rev 30)
00:1f.4 SMBus: Intel Corporation Ice Lake-LP SMBus Controller (rev 30)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Ice Lake-LP SPI Controller (rev 30)
55:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981/PM983

```

The output of *lsusb* is

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 003: ID 06cb:00be Synaptics, Inc. 
Bus 003 Device 004: ID 8087:0026 Intel Corp. 
Bus 003 Device 002: ID 13d3:56b2 IMC Networks Integrated Camera
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Troubleshooting

Most of the difficulty is getting screen rotation, sound, and the microphone to work. Other issues like Chromium/Electron apps being slow, or graphics weirdness can be solved by uninstalling the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package