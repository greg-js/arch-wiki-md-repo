| **Device** | **Status** | **Modules** |
| Intel UHD 630 Graphics | Working | i965 |
| Nvidia GTX 1050 Ti (Max-Q) | Working | nvidia |
| Intel I219-V Ethernet | Working | e1000e |
| Intel 9560 wireless | Working | iwlwifi |
| Realtek ALC285 audio | Working | snd_hda_intel |
| Synaptics touchpad | Working | synaptics + libinput |
| SunplusIT camera | Working | uvcvideo |
| Card reader | Working | xhci_hcd |
| Intel 9560 Bluetooth | Working | btusb |
| Intel JHL7540 Thunderbolt | Untested |
| Synaptics fingerprint reader | Not working |

The [ThinkPad X1 Extreme](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/ThinkPad-X1-Extreme/p/20MF000DUS) is a thin-and-light 15.6" workstation/multimedia laptop from Lenovo's 2018 ThinkPad X lineup.

This page specifically concerns the specifics of running Arch Linux on this laptop. See [Laptop](/index.php/Laptop "Laptop") for generic laptop-related information, or [ThinkPad](/index.php/ThinkPad "ThinkPad") for other ThinkPad laptops.

**Note:** The ThinkPad P1 is a workstation version of the same laptop, using extremely similar hardware. The information on this page should be applicable to P1 models as well, but that has not been confirmed.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 BIOS update](#BIOS_update)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Dolby Atmos Effect on Linux](#Dolby_Atmos_Effect_on_Linux)
    *   [1.4 TLP](#TLP)
    *   [1.5 CPU Undervolting](#CPU_Undervolting)
    *   [1.6 Other notes](#Other_notes)
*   [2 Specifications](#Specifications)

## Configuration

### BIOS update

Despite not being required for an Arch Linux install, a BIOS update is strongly recommended for general use of the laptop - the initial 1.13 version devices seem to ship with contains multiple bugs that can result in bricking the laptop: [Reddit thread discussing the issue](https://www.reddit.com/r/thinkpad/comments/a2g0k4/warning_do_not_change_from_hybrid_graphics_to/); [another Reddit thread discussing a different bricking issue](https://www.reddit.com/r/thinkpad/comments/9qreoj/psa_do_not_enable_bios_support_for_thunderbolt/).

BIOS updates are normally available via [fwupd](/index.php/Fwupd "Fwupd"), however, the latest BIOS update version 1.17 is only available from [Lenovo's website](https://pcsupport.lenovo.com/en/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme/downloads) as of late December 2018\. You can use the bootable version if you don't have access to a Windows install.

### Graphics

Text mode works out of the box. Starting X11 requires configuring the right card ID for the driver in [Xorg.conf](/index.php/Xorg.conf "Xorg.conf"), e.g.:

```
Section "Device"
       Identifier  "Card1"
       # pick between "modesetting" and "intel" here (intel requires xf86-video-intel)
       Driver      "modesetting"
       BusID       "PCI:0:2:0"
EndSection

```

Others have reported the display working out of the box with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), but this is not confirmed. modesetting Hybrid graphics works via [Bumblebee](/index.php/Bumblebee "Bumblebee"). The HDMI port is wired to the Nvidia chip, see [Bumblebee#Output_wired_to_the_NVIDIA_chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee") for details.

Nvidia-only mode has not been thoroughly tested, but seems to work fine with the default configuration produced by `nvidia-xconfig`, including HDMI output.

### Dolby Atmos Effect on Linux

In order to get the same speaker sound quality/effect as on Dolby Atmos with Windows install & configure [Pulseaudio](/index.php/Pulseaudio "Pulseaudio") and [pulseeffects](https://www.archlinux.org/packages/?name=pulseeffects).

You can then download the Dolby Atmos preset from [JackHack96's Github](https://github.com/JackHack96/PulseEffects-Presets/tree/master/irs).

Open the PulseEffects GUI and enable the preset in the "Convolver" tab.

### TLP

Currently the TLP module [tlp_smapi](https://www.archlinux.org/packages/?name=tlp_smapi) doesn't seem to load / work correctly. How ever, the package [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat) works and can read the battery charging start/stop limits.

To set battery start/stop thresholds with [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat) you need to edit /etc/default/tlp e.g.:

"START_CHARGE_THRESH_BAT0=80" and "STOP_CHARGE_THRESH_BAT0=90"

The available CPU governors on the X1E are "performance" and "powersave" (see output of "cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors").

### CPU Undervolting

Undervolting the CPU/Intel GPU works well with [intel-undervolt](https://aur.archlinux.org/packages/intel-undervolt/). The ArchWiki describes how to do it: [Undervolting_CPU#intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU").

Generally -150mV seems to be a safe choice on the i7-8750H and i7-8850H CPUs.

### Other notes

The webcam works out of the box, though it appears connected at all times, no matter the slider state (the camera appears "disconnected" in Windows when the protective slider is closed) - however, when the slider is closed, a completely black image is reported by the camera.

The fingerprint scanner is currently not supported in libfprint - a reverse engineering effort was ongoing [here](https://github.com/nmikhailov/Validity90), but seems to have stalled. Upstream libfprint bug is tracked [here](https://gitlab.freedesktop.org/libfprint/libfprint/issues/134).

The Thunderbolt port has been reported to work on other distributions, but has not been tested on Arch as of December 2018.

Everything else works correctly out of the box.

## Specifications

All information on this page has been tested on laptop part number 20MF000BUS and 20MFCTO1WW, with the following specifications:

*   CPU: Intel Core i7-8750H / i7-8850H
*   Graphics: Hybrid Intel UHD 630 + Nvidia GTX 1050 Ti Max-Q
*   Display: Innolux N156HCE-EN1 1920x1080/60Hz IPS (other vendors may be used)
*   RAM: 16GB / 32GB
*   SSD: Intel 7600p series 512GB NVMe / Samsung 970 Pro 1TB NVMe