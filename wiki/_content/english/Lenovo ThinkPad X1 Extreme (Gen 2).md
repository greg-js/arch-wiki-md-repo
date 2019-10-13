| **Device** | **Status** | **Modules** |
| Intel UHD 630 Graphics | Working | i915 |
| NVIDIA GeForce GTX 1650 | Working | nvidia |
| Intel AX200 Wifi | Working | iwlwifi |
| Intel HDA | Working | snd_hda_intel |
| Synaptics touchpad | Working | libinput |
| Chicony Electronics | Working | uvcvideo |
| Card reader | Working | xhci_hcd |
| Intel AX200 Bluetooth | Working | btusb |
| Intel Thunderbolt | Working | thunderbolt |
| Synaptics fingerprint reader | Not working |

The [Thinkpad X1E Gen 2](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/X1-Extreme-Gen-2/p/22TP2TXX1E2) is a thin-and-light 15.6" workstation/multimedia laptop from Lenovo's 2019 ThinkPad X lineup.

This page specifically concerns the specifics of running Arch Linux on this laptop. See [Laptop](/index.php/Laptop "Laptop") for generic laptop-related information, or [ThinkPad](/index.php/ThinkPad "ThinkPad") for other ThinkPad laptops.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
    *   [1.1 Thunderbolt 3](#Thunderbolt_3)
    *   [1.2 Battery](#Battery)
        *   [1.2.1 Invalid stats workaround](#Invalid_stats_workaround)
        *   [1.2.2 Battery life and graphics](#Battery_life_and_graphics)
    *   [1.3 Graphics](#Graphics)
        *   [1.3.1 Nouveau](#Nouveau)
        *   [1.3.2 NVIDIA](#NVIDIA)
            *   [1.3.2.1 Beta driver features](#Beta_driver_features)
            *   [1.3.2.2 Optimus manager](#Optimus_manager)
    *   [1.4 Audio](#Audio)
        *   [1.4.1 Audio pop on shutdown and startup](#Audio_pop_on_shutdown_and_startup)
    *   [1.5 Fingerprint](#Fingerprint)
    *   [1.6 Webcam](#Webcam)
*   [2 Firmware](#Firmware)
*   [3 Software](#Software)
    *   [3.1 Throttling fix](#Throttling_fix)
    *   [3.2 CPU undervolting](#CPU_undervolting)

## Hardware

### Thunderbolt 3

To use Thunderbolt 3, ensure you are on the latest BIOS firmware (doing the following steps on older BIOSes may brick your device):

1\. Go into BIOS

2\. Enable BIOS Assist mode: (Thunderbolt 3 -> Enable BIOS assist mode) *Ensure you're on the latest BIOS!*

### Battery

#### Invalid stats workaround

As of writing, [a bug exists](https://bbs.archlinux.org/viewtopic.php?pid=1859876) where the battery data can appear corrupt, wildly incorrect, or seem to change drastically from boot to boot. To workaround this bug you should add battery to the `/etc/mkinitcpio.conf`.

```
MODULES=(**battery**)

```

Remember to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") for these changes to take effect.

**Note:** You can also build the battery module into your kernel.

#### Battery life and graphics

[bbswitch does not work](https://bbs.archlinux.org/viewtopic.php?id=238389) on this laptop to disable the NVIDIA card when not in use. To disable the NVIDIA card you can run:

```
# tee /sys/bus/pci/devices/0000\:01\:00.1/remove <<<1
# tee /sys/bus/pci/devices/0000\:01\:00.0/remove <<<1

```

### Graphics

#### Nouveau

Currently (5.2.9-arch1), the Nouveau driver can cause quite a lot of kernel panics when using the webcamera. You should blacklist this driver to prevent it from being loaded.

#### NVIDIA

##### Beta driver features

The NVIDIA beta video driver supports PRIME Offloading. [Following this guide](https://bbs.archlinux.org/viewtopic.php?pid=1859226#p1859226) you can try out this new mode. However, this means [your external display ports will not work](https://forum.manjaro.org/t/nvidia-render-offloading-help-getting-external-monitor-working/99430/22).

**Note:** Unlike the posters in the above thread. The graphics card that is on this laptop **will** shutdown.

##### Optimus manager

Currently, one of the easiest solutions for this laptop is to use [optimus-manager](https://github.com/Askannz/optimus-manager) with the bbswitch backend.

When using just the intel driver, disable the NVIDIA card manually:

```
# tee /sys/bus/pci/devices/0000\:01\:00.1/remove <<<1
# tee /sys/bus/pci/devices/0000\:01\:00.0/remove <<<1

```

This has been confirmed to work with the HDMI port.

### Audio

#### Audio pop on shutdown and startup

To work around the loud audio artifacts on startup/shutdown follow the guide for enabling the audio powersave: [Power management#Audio](/index.php/Power_management#Audio "Power management").

### Fingerprint

The 2.0 version of fprint [will support this device](https://gitlab.freedesktop.org/libfprint/libfprint/issues/181) after a firmware update.

### Webcam

The webcam in this laptop is capable of "Windows Hello" which has a Linux version called [Howdy](/index.php/Howdy "Howdy"). The device you should use to configure howdy on this laptop is `/dev/video0`.

## Firmware

BIOS and firmware updates are available via [fwupd](/index.php/Fwupd "Fwupd"), the Lenovo Vantage application on Windows, or from [Lenovo's website](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme-gen-2/downloads).

The latest BIOS version, v1.26, is highly recommended. All information on this page generally assumes the latest BIOS unless explicitly stated.

## Software

### Throttling fix

You will see a dmesg error that talks about CPU throttling. To fix this install [throttled](https://www.archlinux.org/packages/?name=throttled), then run

```
# systemctl enable --now lenovo_fix.service

```

### CPU undervolting

Undervolting the CPU/Intel GPU works well with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU").