| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| Nvidia | Working | bumblebee & nvidia |
| Ethernet | Working | r8169 |
| Wireless | Working | broadcom-wl-dkms |
| Audio | Working | snd_hda_codec_realtek |
| Touchpad | Working | xf86-input-synaptics |
| Camera | Working |

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 lsusb](#lsusb)
    *   [1.2 lspci](#lspci)
*   [2 Settings](#Settings)
    *   [2.1 Video](#Video)
    *   [2.2 Lan](#Lan)
    *   [2.3 Wifi](#Wifi)
    *   [2.4 Audio](#Audio)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Brightness](#Brightness)
    *   [2.7 Webcam](#Webcam)
    *   [2.8 Bluetooth & Card reader](#Bluetooth_.26_Card_reader)
*   [3 Problems](#Problems)
    *   [3.1 Led](#Led)

## Hardware

CPU: Intel BayTrail M Quad-Core 2940 | GPU: Intel HD | Nvidia: 820M | USB 3.0 | Ram: 4gb DDR3 | HDD: 500gb | HDMI

### lsusb

```
[punky@laptop ~]$ lsusb
Bus 001 Device 005: ID 0bda:57b4 Realtek Semiconductor Corp. 
Bus 001 Device 004: ID 04ca:2006 Lite-On Technology Corp. Broadcom BCM43142A0 Bluetooth Device
Bus 001 Device 002: ID 8087:07e6 Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### lspci

```
[punky@laptop ~]$ lspci
00:00.0 Host bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register (rev 0e)
00:02.0 VGA compatible controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display (rev 0e)
00:13.0 SATA controller: Intel Corporation Atom Processor E3800 Series SATA AHCI Controller (rev 0e)
00:1a.0 Encryption controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine (rev 0e)
00:1b.0 Audio device: Intel Corporation Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller (rev 0e)
00:1c.0 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 1 (rev 0e)
00:1c.2 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 3 (rev 0e)
00:1c.3 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 4 (rev 0e)
00:1d.0 USB controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series USB EHCI (rev 0e)
00:1f.0 ISA bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Power Control Unit (rev 0e)
00:1f.3 SMBus: Intel Corporation Atom Processor E3800 Series SMBus Controller (rev 0e)
01:00.0 3D controller: NVIDIA Corporation GF117M [GeForce 610M/710M/810M/820M / GT 620M/625M/630M/720M] (rev a1)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5286 PCI Express Card Reader (rev 01)
02:00.2 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 06)
03:00.0 Network controller: Broadcom Corporation BCM43142 802.11b/g/n (rev 01)

```

## Settings

**Warning:** Intel Baytrail CPU is known to provoque complete system freeze until [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=109051) is fixed in the kernel

#### Video

Laptop comes with two GPU's (main [INTEL](/index.php/Intel_graphics "Intel graphics") and dedicated [NVIDIA](/index.php/NVIDIA "NVIDIA")):

```
[punky@laptop ~]$ lspci | grep VGA
00:02.0 VGA compatible controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display (rev 0e)

```

For Intel HD install: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)

```
[punky@laptop ~]$ lspci | grep 3D
01:00.0 3D controller: NVIDIA Corporation GF117M [GeForce 610M/710M/810M/820M / GT 620M/625M/630M/720M] (rev a1)

```

For using Nvidia install [bumblebee along with Nvidia and Intel drivers](/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA "Bumblebee").

### Lan

Works fine with no configuration required.

### Wifi

Wifi does not work out of box, because you need to install driver from AUR:

```
broadcom-wl-dkms

```

Ethernet works good, so you can use cable for installing wifi driver.

**Warning:** Using the proprietary driver with KMS leads to sporadic OS freeze! I suppose that is problem with sporadic OS freezes.

### Audio

Install [PulseAudio](/index.php/PulseAudio "PulseAudio").

After installation, reboot the laptop to ensure all modules are loaded. Audio works well both with pure ALSA and with PulseAudio.

### Touchpad

Touchpad works with: [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)

### Brightness

Brightness does work out of box, but you can not change value with keyboard combo, buttons are not mapped at all (fn + F5 / fn + F6), untill you use the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_osi= acpi_backlight=native` to your bootloader. `acpi_osi=` it's indeed followed by a blank space + `acpi_backlight=native`. This is only way when backlight can be controled with keyboard combo keys.

### Webcam

Cheese works fine out of the box.

### Bluetooth & Card reader

I did not test bluetooth because I am not using it, also I did not test card reader, but I think that card reader works fine.

## Problems

### Led

I did not find a way to resolve problem with led for wifi. Every other led (battery, hdd, backlight) works good, but led for wifi does not work even keyboard combo (fn + F2) for enabling / disabling wifi works.