| **Device** | **Status** |
| Intel | Working |
| Nvidia (UX430UQ only) | Working |
| HDMI (USB cable) | Working |
| Ethernet (USB cable) | Working |
| Wireless | Working |
| Audio | Working |
| Touchpad | Working |
| Camera | Working |
| Card Reader | Working |
| Bluetooth | Working |
| Function keys | Working |
| Ambient Light Sensor | Not working |
| Fingerprint Sensor | Not working |

Asus Zenbook UX430 comes in 2 versions - UX430UA and UX430UQ. The only difference is that [UX430UQ](https://www.asus.com/Laptops/ASUS-ZenBook-UX430UQ/) ships NVIDIA GeForce 940MX graphics card while [UX430UA](https://www.asus.com/Laptops/ASUS-ZenBook-UX430UA/) has integrated Intel graphics only.

**Note:** Asus [announced](https://www.asus.com/News/q0npwWGXCqpxoVf8) UX430 and UX530 (bigger display) laptops at the same time, so it is likely that everything below also applies to Asus Zenbook UX530UQ/UX models.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Secure Boot (option)](#Secure_Boot_.28option.29)
    *   [1.2 Video](#Video)
    *   [1.3 Audio](#Audio)
    *   [1.4 Touchpad](#Touchpad)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Headphones audio is too low](#Headphones_audio_is_too_low)
    *   [2.2 Fan spins all the time](#Fan_spins_all_the_time)
    *   [2.3 Microcode](#Microcode)
    *   [2.4 Nvidia issues with Bumblebee](#Nvidia_issues_with_Bumblebee)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Power saving and performance](#Power_saving_and_performance)
    *   [3.2 Extract Windows 10 license key](#Extract_Windows_10_license_key)

# Configuration

## Secure Boot (option)

In order to boot any Linux operating system, navigate to BIOS, then "Security Tab" and set "Secure Boot" to `Off`.

## Video

See [Intel Graphics](/index.php/Intel_graphics#Installation "Intel graphics") and [Hardware Acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). For UX430UQ, also see [Bumblebee](/index.php/Bumblebee "Bumblebee").

## Audio

See [Pulseaudio](/index.php/Pulseaudio "Pulseaudio").

## Touchpad

See [Libinput](/index.php/Libinput "Libinput").

# Troubleshooting

## Headphones audio is too low

The speakers on this ultrabook are loud and clear. However, you may notice that the audio through the headphones is noticeably low ([upstream bug](https://bugs.launchpad.net/ubuntu/+source/alsa-driver/+bug/1648183)).

In order to fix it, install [hda-verb](https://aur.archlinux.org/packages/hda-verb/) and create file:

 `/usr/local/bin/fix_headphones_audio.sh` 
```
#!/bin/sh
/usr/bin/hda-verb /dev/snd/hwC0D0 0x20 SET_COEF_INDEX 0x67
/usr/bin/hda-verb /dev/snd/hwC0D0 0x20 SET_PROC_COEF 0x3000

```

Then create a [systemd](/index.php/Systemd "Systemd") script with the following content:

 `/etc/systemd/system/fix_headphones_audio.service` 
```
[Unit]
Description=Fix headphones audio after boot & resume.
After=dev-snd-hwC0D0.device suspend.target hibernate.target

[Service]
Type=oneshot
ExecStart=/bin/sh '/usr/local/bin/fix_headphones_audio.sh'

[Install]
WantedBy=dev-sdn-hwC0D0.device suspend.target hibernate.target

```

And finally, [start and enable](/index.php/Systemd#Using_units "Systemd") `fix_headphones_audio.service`.

## Fan spins all the time

See [Fan_speed_control#NBFC](/index.php/Fan_speed_control#NBFC "Fan speed control") to fix fan behaviour.

## Microcode

During boot you might get message `[Firmware Bug]: TSC_DEADLINE disabled due to Errata; please update microcode to version: 0x52 (or later)`. See [Microcode](/index.php/Microcode "Microcode") to resolve it.

## Nvidia issues with Bumblebee

It is likelly that it's one of these issues:

*   You used power management application (especially [Powertop](/index.php/Powertop "Powertop")). See [bumblebee#Broken_power_management_with_kernel_4.8](/index.php/Bumblebee#Broken_power_management_with_kernel_4.8 "Bumblebee") for more information.
*   You suspended your laptop and resumed - unable to start GPU. The only fix seems to be full reboot in order to get it working back.

# Tips and tricks

## Power saving and performance

As advertised by ASUS, both laptops are capable to last up to 9 hours on battery. In order to achieve this, see:

*   BIOS update - It is generally recommended to update BIOS, as it usually brings performance, power-saving and security features. See [UX430UA](https://www.asus.com/Laptops/ASUS-ZenBook-UX430UA/HelpDesk_BIOS/) or [UX430UQ](https://www.asus.com/Laptops/ASUS-ZenBook-UX430UQ/HelpDesk_BIOS/) BIOS.

*   [Power Saving](/index.php/Power_Saving "Power Saving") - List of general recommendations to increase battery life.

*   [Improving performance](/index.php/Improving_performance "Improving performance") - List of general recommendations to increase performance.

*   [SSD](/index.php/SSD "SSD") - Tips and tricks for Solid State Drives. Both laptops ship M.2 SSD by default.

## Extract Windows 10 license key

The laptop comes with Windows 10 preinstalled and the activation key is hardcoded into the firmware. If you replace Windows with Linux, then hardcoded activation key is useless. You might want to extract it and use somewhere else (e.g. virtualized Windows 10):

```
# grep -aPo '[A-Z\d-]{29}' /sys/firmware/acpi/tables/MSDM

```

**Note:** Microsoft online support confirmed that the code is valid, but because you are unable to activate it (Windows fails to activate and asks for another code), they offered 2 options - replace code with another one for 40$ or contact OEM (Asus) about this issue and try to sort this out.