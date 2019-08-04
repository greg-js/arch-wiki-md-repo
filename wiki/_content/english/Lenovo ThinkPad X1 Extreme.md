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
    *   [1.3 Thunderbolt](#Thunderbolt)
    *   [1.4 Fan control](#Fan_control)
    *   [1.5 Other hardware](#Other_hardware)
*   [2 Software tweaks](#Software_tweaks)
    *   [2.1 Dolby Atmos Effect on Linux](#Dolby_Atmos_Effect_on_Linux)
    *   [2.2 Battery charge thresholds](#Battery_charge_thresholds)
    *   [2.3 CPU throttling workaround](#CPU_throttling_workaround)
    *   [2.4 CPU undervolting](#CPU_undervolting)
    *   [2.5 Kernel parameters](#Kernel_parameters)
*   [3 Specifications](#Specifications)

## Hardware compatibility

### BIOS update

Despite not being strictly required for an Arch Linux install, a BIOS update is strongly recommended for general use of the laptop - the initial 1.13 version devices seem to ship with contains multiple bugs that can result in bricking the laptop: [Reddit thread discussing the issue](https://www.reddit.com/r/thinkpad/comments/a2g0k4/warning_do_not_change_from_hybrid_graphics_to/); [another Reddit thread discussing a different bricking issue](https://www.reddit.com/r/thinkpad/comments/9qreoj/psa_do_not_enable_bios_support_for_thunderbolt/).

BIOS updates are available via [fwupd](/index.php/Fwupd "Fwupd"), the Lenovo Vantage application on Windows, or from [Lenovo's website](https://pcsupport.lenovo.com/en/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme/downloads).

The latest version, v1.23, is highly recommended. All information on this page generally assumes the latest BIOS unless explicitly stated.

### Hybrid graphics

Hybrid mode works via [Bumblebee](/index.php/Bumblebee "Bumblebee") or [nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun"). Both the HDMI port and DisplayPort outputs created when using either a USB-C adapter or Thunderbolt dock are wired to the Nvidia dGPU. After installing bumblebee, the HDMI port works after modifying the following files, rebooting, and executing `intel-virtual-output -f` from an X server running on the iGPU. See [Bumblebee#Output wired to the NVIDIA chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee") for details.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
    Identifier "intelgpu0"
    # pick between "modesetting" and "intel" here (intel requires xf86-video-intel)
    #Driver "modesetting"
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

Nvidia-only mode works fine with the default configuration produced by `nvidia-xconfig`, including HDMI output.

### Thunderbolt

Thunderbolt works out of the box (tested with ThinkPad Thunderbolt 3 Dock); see [Thunderbolt](/index.php/Thunderbolt "Thunderbolt") for details on security. DisplayPort/HDMI port seems to be attached to the NVIDIA GPU only.

### Fan control

The fan on the right side of the laptop can be controlled by [thinkpad_acpi](/index.php/Fan_speed_control#ThinkPad_laptops "Fan speed control"). It seems that the fan on the left side can't be controlled yet; see [this Nvidia forum post](https://devtalk.nvidia.com/default/topic/1052110/linux/can-t-control-gtx-1050-ti-max-q-fan-on-thinkpad-x1-extreme-laptop/post/5340658/#5340658). If noise is an issue, the fan can be turned off manually by unplugging it from the motherboard, or [the dust mesh can be removed](https://www.reddit.com/r/thinkpad/comments/acesmt/x1_extremes_jet_engine_noise_reduced_after_mesh/).

### Other hardware

The webcam works out of the box, though it appears connected at all times, no matter the slider state (the camera reports a "disconnected" placeholder image in Windows when the protective slider is closed) - however, when the slider is closed, a completely black image is reported by the camera.

The fingerprint scanner is currently not supported in libfprint - a reverse engineering effort was ongoing [here](https://github.com/nmikhailov/Validity90), but seems to have stalled. Upstream libfprint bug is tracked [here](https://gitlab.freedesktop.org/libfprint/libfprint/issues/134).

Everything else works correctly out of the box.

## Software tweaks

### Dolby Atmos Effect on Linux

In order to get the same speaker sound quality/effect as on Dolby Atmos with Windows install & configure [PulseAudio](/index.php/PulseAudio "PulseAudio") and [pulseeffects](https://www.archlinux.org/packages/?name=pulseeffects). You can then download the Dolby Atmos preset from [JackHack96's Github](https://github.com/JackHack96/PulseEffects-Presets/tree/master/irs) and enable it in the "Convolver" tab of the PulseEffects GUI.

### Battery charge thresholds

Battery charging thresholds can be configured via sysfs nodes `/sys/class/power_supply/BAT0/charge_start_threshold` and `/sys/class/power_supply/BAT0/charge_stop_threshold`, or using [TLP](/index.php/TLP "TLP").

### CPU throttling workaround

**Warning:** The safety of the settings mentioned in this section is still being investigated. The firmware limits the temperature to 80C maximum, even with the correct DPTF policy applied. This may or may not be a bug. Please don't use these settings unless you're confident you know what you're doing or the behavior is validated more.

A stress test using [s-tui](https://aur.archlinux.org/packages/s-tui/) indicates that CPU power limit is capped at 38W, keeping CPU temperature at 81C and resulting in maximum sustained frequency around 2850 MHz on i7-8750H.

It should be possible to modify those settings by [applying the correct DPTF policy](https://lkml.org/lkml/2018/10/10/328), however, as of BIOS 1.21, the policies seem to be ignored by the firmware.

This can be worked around by using [throttled](https://www.archlinux.org/packages/?name=throttled) (previously known as [lenovo-throttling-fix-git](https://aur.archlinux.org/packages/lenovo-throttling-fix-git/)) or `intel-undervolt` (see below). It raises the power limit to 44W, which, combined with the `performance` [CPU frequency scaling governor](/index.php/CPU_frequency_scaling#Scaling_governors "CPU frequency scaling"), allows the CPU to run at 3100 MHz with the temperature of 95C.

### CPU undervolting

Undervolting the CPU/Intel GPU works well with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU"). Generally -150mV seems to be a safe choice on the i7-8750H and i7-8850H CPUs, but your mileage may vary.

### Kernel parameters

As of March 2019, the following commonly used kernel parameters are known to work:

*   `i915.enable_guc=2` - enables [GuC/HuC firmware loading](/index.php/Intel_graphics#Enable_GuC_/_HuC_firmware_loading "Intel graphics"), allowing additional hardware acceleration for some video encoding configurations

## Specifications

All information on this page has been tested on laptop part number 20MF000BUS and 20MFCTO1WW, with the following specifications:

*   CPU: Intel Core i7-8750H / i7-8850H
*   Graphics: Hybrid Intel UHD 630 + Nvidia GTX 1050 Ti Max-Q
*   Display: Innolux N156HCE-EN1 1920x1080/60Hz IPS (other vendors may be used)
*   RAM: 16GB / 32GB
*   SSD: Intel 7600p series 512GB NVMe / Samsung 970 Pro 1TB NVMe