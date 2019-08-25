| **Device** | **Status** | **Modules** |
| Intel UHD 630 Graphics | Working | i915 |
| NVIDIA GeForce GTX 1650 | Working | nvidia |
| Intel AX200 Wifi | Working | iwlwifi |
| Intel HDA | Working | snd_hda_intel |
| Synaptics touchpad | Working | libinput |
| Chicony Electronics | Working | uvcvideo |
| Card reader | Working | xhci_hcd |
| Intel AX200 Bluetooth | Working | btusb |
| Intel Thunderbolt | Unknown | thunderbolt |
| Synaptics fingerprint reader | Not working |

The [Thinkpad X1E Gen 2](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/X1-Extreme-Gen-2/p/22TP2TXX1E2) is a thin-and-light 15.6" workstation/multimedia laptop from Lenovo's 2019 ThinkPad X lineup.

This page specifically concerns the specifics of running Arch Linux on this laptop. See [Laptop](/index.php/Laptop "Laptop") for generic laptop-related information, or [ThinkPad](/index.php/ThinkPad "ThinkPad") for other ThinkPad laptops.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
    *   [1.1 Battery](#Battery)
        *   [1.1.1 Invalid Stats Workaround](#Invalid_Stats_Workaround)
        *   [1.1.2 Battery Life & Graphics](#Battery_Life_&_Graphics)
    *   [1.2 Graphics](#Graphics)
        *   [1.2.1 Nouveau](#Nouveau)
        *   [1.2.2 NVIDIA](#NVIDIA)
            *   [1.2.2.1 Beta Driver Features](#Beta_Driver_Features)
            *   [1.2.2.2 Optimus Manager](#Optimus_Manager)
    *   [1.3 Audio](#Audio)
        *   [1.3.1 Audio Pop on Shutdown/Startup](#Audio_Pop_on_Shutdown/Startup)
    *   [1.4 Fingerprint](#Fingerprint)
    *   [1.5 Webcam](#Webcam)
*   [2 Firmware](#Firmware)
*   [3 Software](#Software)
    *   [3.1 Throttling fix](#Throttling_fix)
    *   [3.2 CPU undervolting](#CPU_undervolting)

## Hardware

### Battery

#### Invalid Stats Workaround

As of writing, [a bug exists](https://bbs.archlinux.org/viewtopic.php?pid=1859876) where the battery data can appear corrupt, wildly incorrect, or seem to change drastically from boot to boot. To workaround this bug you should add battery to the `/etc/mkinitcpio.conf`.

	 `MODULES=(**battery**)` 

Remember to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") for these changes to take effect.

```
**NOTE:** You can also build the battery module into your kernel

```

#### Battery Life & Graphics

[bbswitch does not work](https://bbs.archlinux.org/viewtopic.php?id=238389) on this laptop to disable the NVIDIA card when not in use. To disable the NVIDIA card you can run:

```
# tee /sys/bus/pci/devices/0000\:01\:00.1/remove <<<1
# tee /sys/bus/pci/devices/0000\:01\:00.0/remove <<<1

```

### Graphics

#### Nouveau

Currently (5.2.9-arch1), the Nouveau driver can cause quite a lot of kernel panics when using the webcamera. You should blacklist this driver to prevent it from being loaded.

#### NVIDIA

##### Beta Driver Features

The NVIDIA beta video driver supports PRIME Offloading. [Following this guide](https://bbs.archlinux.org/viewtopic.php?pid=1859226#p1859226) you can try out this new mode. However, this means [your external display ports will not work](https://forum.manjaro.org/t/nvidia-render-offloading-help-getting-external-monitor-working/99430/22).

```
NOTE: Unlike the posters in the above thread. The graphics card that is on this laptop **will** shutdown. 

```

##### Optimus Manager

Currently, one of the easiest solutions for this laptop is to use [optimus-manager](https://github.com/Askannz/optimus-manager) with the bbswitch backend.

When using just the intel driver, disable the NVIDIA card manually:

```
# tee /sys/bus/pci/devices/0000\:01\:00.1/remove <<<1
# tee /sys/bus/pci/devices/0000\:01\:00.0/remove <<<1

```

This has been confirmed to work with the HDMI port.

### Audio

#### Audio Pop on Shutdown/Startup

To workaround the loud audio artifacts on startup/shutdown follow the guide for enabling the audio powersave [power_management#Audio](/index.php/Power_management#Audio "Power management")

### Fingerprint

The 2.0 version of fprint [will support this device](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181) after a firmware update.

### Webcam

The webcam in this laptop is capable of "Windows Hello" which has a Linux version called [Howdy](/index.php/Howdy "Howdy")

The device you should use to configure howdy on this laptop is:

```
/dev/video0

```

## Firmware

BIOS and firmware updates are available via [fwupd](/index.php/Fwupd "Fwupd"), the Lenovo Vantage application on Windows, or from [Lenovo's website](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme-gen-2/downloads).

The latest BIOS version, v1.08, is highly recommended. All information on this page generally assumes the latest BIOS unless explicitly stated.

## Software

### Throttling fix

You'll see a dmesg error that talks about CPU throttling. To fix this install [throttled](https://www.archlinux.org/packages/?name=throttled), then run

```
# systemctl enable --now lenovo_fix.service

```

### CPU undervolting

Undervolting the CPU/Intel GPU works well with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU").