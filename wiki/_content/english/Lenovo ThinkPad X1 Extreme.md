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

This page specifically concerns the specifics of running Arch Linux on this laptop. See [Laptop](/index.php/Laptop "Laptop") for generic laptop-related information, or [ThinkPad](/index.php/ThinkPad "ThinkPad") for other ThinkPad laptops. The [Ubuntu certification page](https://certification.ubuntu.com/certification/hardware/201809-26479/) may also be useful.

**Note:** The [Lenovo ThinkPad P1](/index.php/Lenovo_ThinkPad_P1 "Lenovo ThinkPad P1") is a workstation version of the same laptop which uses extremely similar hardware. Most of the information on this page should be applicable to P1 models as well.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware compatibility](#Hardware_compatibility)
    *   [1.1 BIOS update](#BIOS_update)
    *   [1.2 Hybrid graphics](#Hybrid_graphics)
        *   [1.2.1 Bumblebee](#Bumblebee)
        *   [1.2.2 optimus-manager](#optimus-manager)
        *   [1.2.3 Using external graphics exclusively](#Using_external_graphics_exclusively)
    *   [1.3 Thunderbolt](#Thunderbolt)
    *   [1.4 Fan control](#Fan_control)
    *   [1.5 Other hardware](#Other_hardware)
*   [2 Software tweaks](#Software_tweaks)
    *   [2.1 Dolby Atmos Effect on Linux](#Dolby_Atmos_Effect_on_Linux)
    *   [2.2 Battery charge thresholds](#Battery_charge_thresholds)
    *   [2.3 CPU throttling workaround](#CPU_throttling_workaround)
    *   [2.4 CPU undervolting](#CPU_undervolting)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Some graphical applications not responsive](#Some_graphical_applications_not_responsive)
*   [4 Specifications](#Specifications)

## Hardware compatibility

### BIOS update

Despite not being strictly required for an Arch Linux install, a BIOS update is strongly recommended for general use of the laptop - the initial 1.13 version devices seem to ship with contains multiple bugs that can result in bricking the laptop: [Reddit thread discussing the issue](https://www.reddit.com/r/thinkpad/comments/a2g0k4/warning_do_not_change_from_hybrid_graphics_to/); [another Reddit thread discussing a different bricking issue](https://www.reddit.com/r/thinkpad/comments/9qreoj/psa_do_not_enable_bios_support_for_thunderbolt/).

BIOS updates are available via [fwupd](/index.php/Fwupd "Fwupd"), the Lenovo Vantage application on Windows, or from [Lenovo's website](https://pcsupport.lenovo.com/en/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme/downloads).

The latest version, v1.24, is highly recommended. All information on this page generally assumes the latest BIOS unless explicitly stated.

### Hybrid graphics

Hybrid mode works via [Bumblebee](/index.php/Bumblebee "Bumblebee"), [nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun") or [optimus-manager](/index.php/NVIDIA_Optimus#Using_optimus-manager "NVIDIA Optimus"). Both the HDMI port and DisplayPort outputs created when using either a USB-C adapter or Thunderbolt dock are wired to the Nvidia dGPU.

#### Bumblebee

After installing Bumblebee, the HDMI port works after modifying the following files, rebooting, and executing `intel-virtual-output -f` from an X server running on the iGPU. See [Bumblebee#Output wired to the NVIDIA chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee") for details.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
    Identifier "intelgpu0"
    Driver "intel"
EndSection

```
 `/etc/bumblebee/xorg.conf.nvidia` 
```
Section "ServerLayout"
    Identifier  "Layout0"
    Option      "AutoAddDevices" "true"
    Option      "AutoAddGPU" "false"
EndSection

Section "Device"
    Identifier  "DiscreteNvidia"
    Driver      "nvidia"
    VendorName  "NVIDIA Corporation"
    Option "ProbeAllGpus" "false"
    Option "AllowEmptyInitialConfiguration"
EndSection

Section "Screen"
    Identifier "Screen0"
    Device "DiscreteNVidia"
EndSection

```

#### optimus-manager

While optimus-manager requires logging out to switch graphics, it provides better performance and more stable external display support. The following configuration has been found to work well:

 `/etc/optimus-manager/optimus-manager.conf` 
```

[intel]
driver=intel
modeset=yes

[nvidia]
modeset=yes

[optimus]
switching=bbswitch

```

#### Using external graphics exclusively

Works fine with the default configuration produced by `nvidia-xconfig`, including HDMI output.

### Thunderbolt

Thunderbolt works out of the box (tested with ThinkPad Thunderbolt 3 Dock); see [Thunderbolt](/index.php/Thunderbolt "Thunderbolt") for details on security.

### Fan control

The fan on the right side of the laptop can be controlled by [thinkpad_acpi](/index.php/Fan_speed_control#ThinkPad_laptops "Fan speed control"). It seems that the fan on the left side can't be controlled yet; see [this Nvidia forum post](https://devtalk.nvidia.com/default/topic/1052110/linux/can-t-control-gtx-1050-ti-max-q-fan-on-thinkpad-x1-extreme-laptop/post/5340658/#5340658). If noise is an issue, the fan can be turned off manually by unplugging it from the motherboard, or [the dust mesh can be removed](https://www.reddit.com/r/thinkpad/comments/acesmt/x1_extremes_jet_engine_noise_reduced_after_mesh/).

### Other hardware

The touchpad experience can be greatly improved by enabling "intertouch" as hinted by kernel messages. This can be done by either adding `psmouse.synaptics_intertouch=1` to the kernel command line or by creating a modprobe entry like:

 `/etc/modprobe.d/psmouse.conf`  `options psmouse synaptics_intertouch=1` 

The webcam works out of the box, though it reports a completely black image instead of the "disconnected" placeholder when the protective slider is closed.

The fingerprint scanner is currently not supported in libfprint - a reverse engineering effort was ongoing [here](https://github.com/nmikhailov/Validity90), but seems to have stalled. Upstream libfprint bug is tracked [here](https://gitlab.freedesktop.org/libfprint/libfprint/issues/134).

Everything else works correctly out of the box.

## Software tweaks

### Dolby Atmos Effect on Linux

In order to get the same speaker sound quality/effect as on Dolby Atmos with Windows install & configure [PulseAudio](/index.php/PulseAudio "PulseAudio") and [pulseeffects](https://www.archlinux.org/packages/?name=pulseeffects). You can then download the Dolby Atmos preset from [JackHack96's Github](https://github.com/JackHack96/PulseEffects-Presets/tree/master/irs) and enable it in the "Convolver" tab of the PulseEffects GUI.

### Battery charge thresholds

Battery charging thresholds can be configured via sysfs nodes `/sys/class/power_supply/BAT0/charge_start_threshold` and `/sys/class/power_supply/BAT0/charge_stop_threshold`, or using [TLP](/index.php/TLP "TLP").

### CPU throttling workaround

**Warning:** As of BIOS v1.24, overriding thermal limits will result in your laptop running out of spec under certain conditions. A proper firmware level solution [is being worked on](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1C6-T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489) by Lenovo, and should be available eventually.

A stress test using [s-tui](https://www.archlinux.org/packages/?name=s-tui) indicates that the CPU is limited to 38W/80C, resulting in maximum sustained frequency of around 2850 MHz on i7-8750H under heavy loads.

This can be worked around by using [throttled](https://www.archlinux.org/packages/?name=throttled) or `intel-undervolt` (see below). It raises the power limit to 44W, which, combined with the `performance` [CPU frequency scaling governor](/index.php/CPU_frequency_scaling#Scaling_governors "CPU frequency scaling"), allows the CPU to run at 3100 MHz with the temperature of 95C.

### CPU undervolting

**Warning:** While generally not directly dangerous to the hardware, undervolting is not supported by Lenovo or Intel. If you experience any issues whatsoever while your hardware is undervolted, reset to stock voltages and verify the issue is still present.

Undervolting the CPU/Intel GPU works well with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU"). Generally -150mV seems to be a safe choice on the i7-8750H and i7-8850H CPUs, but your mileage may vary.

The effects of undervolting on system stability will vary depending on individual hardware (a.k.a. "the silicon lottery").

## Troubleshooting

### Some graphical applications not responsive

Some applications like Firefox or Telegram can experience periodic drawing lag for less than second every several seconds.

It may be the Intel driver [SNA Issue](/index.php/Intel_graphics#SNA_issues "Intel graphics").

## Specifications

All information on this page has been tested on laptop part number 20MF000BUS and 20MFCTO1WW, with the following specifications:

*   CPU: Intel Core i7-8750H / i7-8850H
*   Graphics: Hybrid Intel UHD 630 + Nvidia GTX 1050 Ti Max-Q
*   Display: Innolux N156HCE-EN1 1920x1080/60Hz IPS (other vendors may be used)
*   RAM: 16GB / 32GB
*   SSD: Intel 7600p series 512GB NVMe / Samsung 970 Pro 1TB NVMe