| **Device** | **Status** |
| Intel | Working |
| Nvidia | Working |
| HDMI (USB cable) | Working |
| Ethernet (USB cable) | Working |
| Wireless | Working |
| Audio | Working |
| Touchpad | Working |
| Camera | Working |
| Card Reader | Working |
| Bluetooth | Working |
| Function keys | Working |
| Fingerprint Sensor | Partially working |
| Ambient Light Sensor | Not working |
| [Battery charge control](https://techinstyle.asus.com/asus-battery-health-charging-helps-you-get-the-most-out-of-your-zenbook/) | Not working |

ASUS [announced](https://www.asus.com/News/q0npwWGXCqpxoVf8) UX430 and UX530 models. Since these models share almost the same hardware (the only difference is screen size and discrete NVidia graphics card), this article covers hardware specific configuration for all UX430UA, UX430UQ, UX530UQ and UX530UX models.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Secure Boot (option)](#Secure_Boot_.28option.29)
    *   [1.2 Video](#Video)
    *   [1.3 Audio](#Audio)
    *   [1.4 Touchpad](#Touchpad)
    *   [1.5 Fingerprint sensor](#Fingerprint_sensor)
    *   [1.6 Suspend](#Suspend)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Linux kernel 4.13 issues](#Linux_kernel_4.13_issues)
    *   [2.2 Headphones audio is too low](#Headphones_audio_is_too_low)
    *   [2.3 Fan spins all the time](#Fan_spins_all_the_time)
    *   [2.4 Microcode](#Microcode)
    *   [2.5 Nvidia issues with Bumblebee](#Nvidia_issues_with_Bumblebee)
    *   [2.6 Headset Microphone](#Headset_Microphone)
    *   [2.7 No sound](#No_sound)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Power saving and performance](#Power_saving_and_performance)
    *   [3.2 Extract Windows 10 license key](#Extract_Windows_10_license_key)

# Configuration

## Secure Boot (option)

In order to boot any Linux operating system, navigate to BIOS, then hit F7 or click on "Advanced Menu", then the "Security" tab and set "Secure Boot" to `Off`.

If the aforementioned "Secure Boot" option is a menu rather than an on-or-off option, click on "Secure Boot", "Key Management", then "Reset to Setup Mode" and confirm in the dialog.

## Video

See [Intel Graphics](/index.php/Intel_graphics#Installation "Intel graphics") and [Hardware Acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). For models with discrete NVidia graphics card, also see [Bumblebee](/index.php/Bumblebee "Bumblebee").

## Audio

See [PulseAudio](/index.php/PulseAudio "PulseAudio").

## Touchpad

See [Libinput](/index.php/Libinput "Libinput").

## Fingerprint sensor

**Note:** This is likely not going to work at all. See [Talk:ASUS Zenbook UX430/UX530#Fingerprint Reader](/index.php/Talk:ASUS_Zenbook_UX430/UX530#Fingerprint_Reader "Talk:ASUS Zenbook UX430/UX530").

Install fingerprint sensor driver [libfprint-elantech-git](https://aur.archlinux.org/packages/libfprint-elantech-git/), then see [Fprint](/index.php/Fprint "Fprint") and you might be also interested in [Fingerprint GUI](/index.php/Fingerprint_GUI "Fingerprint GUI").

## Suspend

Linux (4.17 at least) default to [suspend-to-idle](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html#suspend-to-idle) which isn't very power effective. This is probably due to this change in [4.14-rc1](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=e870c6c87cf9484090d28f2a68aa29e008960c93). For better power effective you can use [suspend-to-ram](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html#suspend-to-ram) by adding `mem_sleep_default=deep` to the kernel cmdline.

# Troubleshooting

## Linux kernel 4.13 issues

**Bug references**: [197469](https://bugzilla.kernel.org/show_bug.cgi?id=197469) and [197449](https://bugzilla.kernel.org/show_bug.cgi?id=197449)

**Description**: Unstable CPU frequencies staying at minimum of 800Mhz-1600Mhz instead of 400-700Mhz. This wastes battery and generates heat, causing fan to spin more aggressively. Also KVM crashes running Windows 10 VM with all available VirtIO features.

**Fix**: Use kernel version 4.12.* (or earlier) or 4.14.4 (or further). Avoid any 4.13.* versions.

## Headphones audio is too low

Linux kernel version 4.14 and earlier has a bug, where you may notice that the audio through the headphones is too low ([upstream bug](https://bugs.launchpad.net/ubuntu/+source/alsa-driver/+bug/1648183)). In kernel version 4.15 you have to pull out and plug in back your headset after resume in order to fix the low audio.

In order to fix it, install [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools) or [hda-verb](https://aur.archlinux.org/packages/hda-verb/) and create the file:

 `/usr/local/bin/fix_headphones_audio.sh` 
```
#!/bin/bash
while true; do
	DEVICE=`ls /dev/snd/hwC[[:print:]]*D0 | head -n 1`
	if [ ! -z "$DEVICE" ]; then
		hda-verb "$DEVICE" 0x20 SET_COEF_INDEX 0x67
		hda-verb "$DEVICE" 0x20 SET_PROC_COEF 0x3000
		break
	fi
	sleep 1
done

```

Then create a [systemd](/index.php/Systemd "Systemd") script with the following content:

 `/etc/systemd/system/fix_headphones_audio.service` 
```
[Unit]
Description=Fix headphones audio after boot & resume.
After=multi-user.target suspend.target hibernate.target

[Service]
Type=oneshot
ExecStart=/bin/sh '/usr/local/bin/fix_headphones_audio.sh'

[Install]
WantedBy=multi-user.target suspend.target hibernate.target

```

And finally, [start and enable](/index.php/Systemd#Using_units "Systemd") `fix_headphones_audio.service`.

## Fan spins all the time

See [Fan speed control#NBFC](/index.php/Fan_speed_control#NBFC "Fan speed control"). Also see [#Linux kernel 4.13 issues](#Linux_kernel_4.13_issues)

## Microcode

During boot you might get the message `[Firmware Bug]: TSC_DEADLINE disabled due to Errata; please update microcode to version: 0x52 (or later)`. See [Microcode](/index.php/Microcode "Microcode") to resolve it.

## Nvidia issues with Bumblebee

It is likely that it's one of these issues:

*   You used a power management application (especially [Powertop](/index.php/Powertop "Powertop")). See [bumblebee#Broken power management with kernel 4.8](/index.php/Bumblebee#Broken_power_management_with_kernel_4.8 "Bumblebee") for more information.
*   You suspended your laptop and resumed, and are now unable to start your GPU, see [Bumblebee#Failed to initialize the NVIDIA GPU at PCI:1:0:0 (Bumblebee daemon reported: error: [XORG] (EE) NVIDIA(GPU-0))](/index.php/Bumblebee#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28Bumblebee_daemon_reported:_error:_.5BXORG.5D_.28EE.29_NVIDIA.28GPU-0.29.29 "Bumblebee").

## Headset Microphone

You may encounter an issue where your headset microphone is not being detected. To fix this, create this file and restart your system:

 `/etc/modprobe.d/fix_headset_microphone.conf` 
```
# Fix an issue where your headset microphone is not being detected:
options snd-hda-intel model=dell-headset-multi

```

## No sound

There seems to be a bug in the firmware that prevents the embedded sound card from working in Arch after Windows has been restarted. A complete shutdown of the laptop is required to get the sound card working again.

# Tips and tricks

## Power saving and performance

As advertised by ASUS, both laptops are capable to last up to 9 hours on battery. In order to achieve this, see:

*   BIOS update - It is generally recommended to update BIOS, as it usually brings performance, power-saving and security features.

*   [Power Saving](/index.php/Power_Saving "Power Saving") - List of general recommendations to increase battery life.

*   [Improving performance](/index.php/Improving_performance "Improving performance") - List of general recommendations to increase performance.

*   [SSD](/index.php/SSD "SSD") - Tips and tricks for Solid State Drives. Both laptops ship M.2 SSD by default.

*   [Undervolting CPU](/index.php/Undervolting_CPU "Undervolting CPU") - Decrease voltage for Intel CPU (reduce battery drain, reduce heat and therefore - reduce fan speed)

## Extract Windows 10 license key

The laptop comes with Windows 10 preinstalled and the activation key is hardcoded into the firmware. If you replace Windows with Linux, then hardcoded activation key is useless. You might want to extract it and use somewhere else (e.g. virtualized Windows 10):

```
# grep -aPo '[\w]{5}-[\w]{5}-[\w]{5}-[\w]{5}-[\w]{5}' /sys/firmware/acpi/tables/MSDM

```

**Note:** Microsoft online support confirmed that the code is valid, but because you are unable to activate it (Windows fails to activate and asks for another code), they offered 2 options - replace activation code with another one for 40$ or contact OEM (ASUS) about this issue.ASUS confirmed, that in order to "use" this activation key, you need to bring this laptop to repair service so they can "restore" system using ASUS OEM Windows 10 image. They do not provide this image for download.