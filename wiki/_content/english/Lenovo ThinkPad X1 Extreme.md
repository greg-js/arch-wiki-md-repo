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
| Intel JHL7540 Thunderbolt | Working | thunderbolt |
| Synaptics fingerprint reader | Not working |

The [ThinkPad X1 Extreme](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/ThinkPad-X1-Extreme/p/20MF000DUS) is a thin-and-light 15.6" workstation/multimedia laptop from Lenovo's 2018 ThinkPad X lineup.

This page specifically concerns the specifics of running Arch Linux on this laptop. See [Laptop](/index.php/Laptop "Laptop") for generic laptop-related information, or [ThinkPad](/index.php/ThinkPad "ThinkPad") for other ThinkPad laptops.

**Note:** The ThinkPad P1 is a workstation version of the same laptop which uses extremely similar hardware. Most of the information on this page should be applicable to P1 models as well.

## Contents

*   [1 Hardware compatibility](#Hardware_compatibility)
    *   [1.1 BIOS update](#BIOS_update)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Thunderbolt](#Thunderbolt)
    *   [1.4 Other hardware](#Other_hardware)
*   [2 Software tweaks](#Software_tweaks)
    *   [2.1 Dolby Atmos Effect on Linux](#Dolby_Atmos_Effect_on_Linux)
    *   [2.2 TLP](#TLP)
    *   [2.3 CPU throttling workaround](#CPU_throttling_workaround)
    *   [2.4 CPU undervolting](#CPU_undervolting)
    *   [2.5 Kernel parameters](#Kernel_parameters)
*   [3 Specifications](#Specifications)

## Hardware compatibility

### BIOS update

Despite not being required for an Arch Linux install, a BIOS update is strongly recommended for general use of the laptop - the initial 1.13 version devices seem to ship with contains multiple bugs that can result in bricking the laptop: [Reddit thread discussing the issue](https://www.reddit.com/r/thinkpad/comments/a2g0k4/warning_do_not_change_from_hybrid_graphics_to/); [another Reddit thread discussing a different bricking issue](https://www.reddit.com/r/thinkpad/comments/9qreoj/psa_do_not_enable_bios_support_for_thunderbolt/).

BIOS updates are available via [fwupd](/index.php/Fwupd "Fwupd"), the Lenovo Vantage application on Windows, or from [Lenovo's website](https://pcsupport.lenovo.com/en/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme/downloads).

The recommended minimum BIOS version is v1.17 (listed as 0.1.17 on LVFS); the latest version, v1.18, contains additional fixes, but is only available from Lenovo's website as of late January 2019.

### Graphics

Text mode works out of the box.

Starting X11 requires configuring the right card ID for the driver in [Xorg.conf](/index.php/Xorg.conf "Xorg.conf"), e.g.:

```
Section "Device"
       Identifier  "Card1"
       # pick between "modesetting" and "intel" here (intel requires xf86-video-intel)
       Driver      "modesetting"
       BusID       "PCI:0:2:0"
EndSection

```

Wayland compositors generally don't require additional configuration (tested with Plasma and Sway).

Hybrid graphics works via [Bumblebee](/index.php/Bumblebee "Bumblebee"). The HDMI port is wired to the Nvidia chip, see [Bumblebee#Output wired to the NVIDIA chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee") for details.

Nvidia-only mode has not been thoroughly tested, but seems to work fine with the default configuration produced by `nvidia-xconfig`, including HDMI output.

### Thunderbolt

Thunderbolt works out of the box (tested with ThinkPad Thunderbolt 3 Dock); see [Thunderbolt](/index.php/Thunderbolt "Thunderbolt") for details on security. DisplayPort/HDMI port seems to be attached to the NVIDIA GPU only.

### Other hardware

The webcam works out of the box, though it appears connected at all times, no matter the slider state (the camera reports a "disconnected" placeholder image in Windows when the protective slider is closed) - however, when the slider is closed, a completely black image is reported by the camera.

The fingerprint scanner is currently not supported in libfprint - a reverse engineering effort was ongoing [here](https://github.com/nmikhailov/Validity90), but seems to have stalled. Upstream libfprint bug is tracked [here](https://gitlab.freedesktop.org/libfprint/libfprint/issues/134).

Everything else works correctly out of the box.

## Software tweaks

### Dolby Atmos Effect on Linux

In order to get the same speaker sound quality/effect as on Dolby Atmos with Windows install & configure [PulseAudio](/index.php/PulseAudio "PulseAudio") and [pulseeffects](https://www.archlinux.org/packages/?name=pulseeffects). You can then download the Dolby Atmos preset from [JackHack96's Github](https://github.com/JackHack96/PulseEffects-Presets/tree/master/irs) and enable it in the "Convolver" tab of the PulseEffects GUI.

### TLP

To set battery start/stop thresholds with [TLP](/index.php/TLP "TLP"), install [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) and edit `/etc/default/tlp`:

```
START_CHARGE_THRESH_BAT0=80
STOP_CHARGE_THRESH_BAT0=90

```

### CPU throttling workaround

A stress test using [s-tui](https://aur.archlinux.org/packages/s-tui/) indicates that CPU power limit is capped at 38W, keeping CPU temperature at 81C and resulting in maximum sustained frequency around 2850 MHz on i7-8750H. Similar to other modern Thinkpad laptops, this can be worked around by using [lenovo-throttling-fix-git](https://aur.archlinux.org/packages/lenovo-throttling-fix-git/). It raises the power limit to 44W, which, combined with the `performance` [CPU frequency scaling governor](/index.php/CPU_frequency_scaling#Scaling_governors "CPU frequency scaling"), allows the same CPU to run at 3100 MHz with the temperature of 95C.

See the [lenovo-throttling-fix homepage](https://github.com/erpalma/lenovo-throttling-fix) for more info about the temporary fix; a [proper solution](https://git.kernel.org/pub/scm/linux/kernel/git/rzhang/linux.git/commit/?h=next&id=bcd8aa670b74c026759cd6c06019d98b7b28bfd6) is incoming, and likely to appear in Linux 5.0 or 5.1.

### CPU undervolting

Undervolting the CPU/Intel GPU works well with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU"). Generally -150mV seems to be a safe choice on the i7-8750H and i7-8850H CPUs, but your mileage may vary.

### Kernel parameters

As of January 2019, the following commonly used kernel parameters are known to work:

*   `i915.enable_psr=1` - enables panel self-refresh on Intel graphics, likely power savings
*   `i915.fastboot=1` - skips mode setting on startup, prevents flickering on compatible boot loaders (rEFInd, GRUB2 with resolution set, etc.)
*   `i915.enable_guc=2` - enables [GuC/HuC firmware loading](/index.php/Intel_graphics#Enable_GuC_/_HuC_firmware_loading "Intel graphics"), allowing additional hardware acceleration for some video encoding configurations

## Specifications

All information on this page has been tested on laptop part number 20MF000BUS and 20MFCTO1WW, with the following specifications:

*   CPU: Intel Core i7-8750H / i7-8850H
*   Graphics: Hybrid Intel UHD 630 + Nvidia GTX 1050 Ti Max-Q
*   Display: Innolux N156HCE-EN1 1920x1080/60Hz IPS (other vendors may be used)
*   RAM: 16GB / 32GB
*   SSD: Intel 7600p series 512GB NVMe / Samsung 970 Pro 1TB NVMe