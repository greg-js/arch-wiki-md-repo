| **Device** | **Status** |
| Intel | Working |
| Nvidia | Working |
| HDMI | Working |
| Ethernet (USB cable) | Working |
| Wireless | Working |
| Audio | Working |
| Touchpad | Working |
| Camera | Working |
| Card Reader | Working |
| Bluetooth | Working |
| Function keys | Working |
| Face recognition sensor | working |
| Battery charge threshold | Not working |

ASUS [announced](https://www.asus.com/us/News/C8ew3iV9HQ6KqLnw) UX333, UX433 and UX533models. Since these models share almost the same hardware (the only difference is screen size and discrete NVidia GPU), this article covers hardware specific configuration for all ZenBook 13 (UX333), ZenBook 14 (UX433) and ZenBook 15 (UX533).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Secure Boot (option)](#Secure_Boot_(option))
    *   [1.2 Video](#Video)
    *   [1.3 Audio](#Audio)
    *   [1.4 Touchpad](#Touchpad)
    *   [1.5 Facerecognition login](#Facerecognition_login)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Microcode](#Microcode)
    *   [2.2 Nvidia issues with Bumblebee](#Nvidia_issues_with_Bumblebee)
    *   [2.3 Suspend](#Suspend)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Power saving and performance](#Power_saving_and_performance)
    *   [3.2 Extract Windows 10 license key](#Extract_Windows_10_license_key)

# Configuration

## Secure Boot (option)

In order to boot any Linux operating system, navigate to BIOS, then hit F7 or click on "Advanced Menu", then the "Security" tab and set "Secure Boot" to `Off`.

If the aforementioned "Secure Boot" option is a menu rather than an on-or-off option, click on "Secure Boot", "Key Management", then "Reset to Setup Mode" and confirm in the dialog.

## Video

See [Intel Graphics](/index.php/Intel_graphics#Installation "Intel graphics") and [Hardware Acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). For models with discrete Nvidia graphics card, also see [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus").

## Audio

See [PulseAudio](/index.php/PulseAudio "PulseAudio").

## Touchpad

See [Libinput](/index.php/Libinput "Libinput").

## Facerecognition login

This computer has built-in face recognition sensor. You can use it with the project Howdy [[1]](https://github.com/boltgolt/howdy). See the [howdy](/index.php/Howdy "Howdy") page for further informations.

# Troubleshooting

## Microcode

During boot you might get the message `[Firmware Bug]: TSC_DEADLINE disabled due to Errata; please update microcode to version: 0x52 (or later)`. See [Microcode](/index.php/Microcode "Microcode") to resolve it.

## Nvidia issues with Bumblebee

It is likely that it's one of these issues:

*   You used a power management application (especially [Powertop](/index.php/Powertop "Powertop")). See [bumblebee#Broken power management with kernel 4.8](/index.php/Bumblebee#Broken_power_management_with_kernel_4.8 "Bumblebee") for more information.
*   You suspended your laptop and resumed, and are now unable to start your GPU, see [Bumblebee#Failed to initialize the NVIDIA GPU at PCI:1:0:0 (Bumblebee daemon reported: error: [XORG] (EE) NVIDIA(GPU-0))](/index.php/Bumblebee#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_(Bumblebee_daemon_reported:_error:_[XORG]_(EE)_NVIDIA(GPU-0)) "Bumblebee").

## Suspend

Linux (4.17 at least) default to [suspend-to-idle](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html#suspend-to-idle) which isn't very power effective. This is probably due to this change in [4.14-rc1](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=e870c6c87cf9484090d28f2a68aa29e008960c93). For better power effective you can use [suspend-to-ram](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html#suspend-to-ram) by adding `mem_sleep_default=deep` to the kernel cmdline.

# Tips and tricks

## Power saving and performance

As advertised by ASUS, these laptops are capable to last up to 9 hours on battery. In order to achieve this, see:

*   BIOS update - It is generally recommended to update BIOS, as it usually brings performance, power-saving and security features.

*   [Power Saving](/index.php/Power_Saving "Power Saving") - List of general recommendations to increase battery life.

*   [Improving performance](/index.php/Improving_performance "Improving performance") - List of general recommendations to increase performance.

*   [SSD](/index.php/SSD "SSD") - Tips and tricks for Solid State Drives. These three laptops ship M.2 SSD by default.

*   [Undervolting CPU](/index.php/Undervolting_CPU "Undervolting CPU") - Decrease voltage for Intel CPU (reduce battery drain, reduce heat and therefore - reduce fan speed)

## Extract Windows 10 license key

The laptop comes with Windows 10 preinstalled and the activation key is hardcoded into the firmware. If you replace Windows with Linux, then hardcoded activation key is useless. You might want to extract it and use somewhere else (e.g. virtualized Windows 10):

```
# grep -aPo '[\w]{5}-[\w]{5}-[\w]{5}-[\w]{5}-[\w]{5}' /sys/firmware/acpi/tables/MSDM

```

**Note:** Microsoft online support confirmed that the code is valid, but because you are unable to activate it (Windows fails to activate and asks for another code), they offered 2 options - replace activation code with another one for 40$ or contact OEM (ASUS) about this issue.ASUS confirmed, that in order to "use" this activation key, you need to bring this laptop to repair service so they can "restore" system using ASUS OEM Windows 10 image. They do not provide this image for download.