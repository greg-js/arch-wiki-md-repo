This article describes specific steps to configure hardware on the notebook model HP Compaq NX6325.

## Contents

*   [1 Wireless](#Wireless)
*   [2 Power management](#Power_management)
    *   [2.1 Troubleshooting](#Troubleshooting)
*   [3 Audio](#Audio)
    *   [3.1 Multimedia keys](#Multimedia_keys)
*   [4 Video](#Video)
    *   [4.1 Xorg.conf](#Xorg.conf)
*   [5 Fingerprint, card slots, etc.](#Fingerprint.2C_card_slots.2C_etc.)

# Wireless

The Compaq nx6325 has the BCM4311 or BCM4312 wireless chipset. The b43 drivers that come with the latest kernel will get these to work. The b43-firmware package **must** also be installed from the AUR. Details can be found [here](/index.php/Broadcom_wireless#b43.2Fb43legacy "Broadcom wireless")

# Power management

**NOTE**: All and any of these are optional. Laptop Mode Tools and Acpid are *highly* advised.

Laptop Mode tools with a combination of Cpufreq, acpi and pm-utils will work on this notebook. Thorough installation and configuration instructions for each tool can be found:

*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") (may not be required)
*   [Acpid](/index.php/Acpid "Acpid")
*   [Pm-utils](/index.php/Pm-utils "Pm-utils")

## Troubleshooting

On almost every kernel and distribution the CPU scaling doesnt work and it stays stuck at 800Mhz constantly. An easy fix is to append the linux line in [GRUB](/index.php/GRUB "GRUB") and add: "acpi=noirq" . To make it permanent you need to configure the GRUB_CMDLINE_LINUX argument.

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="acpi=noirq"` 

# Audio

Sound works fine, just follow the [ALSA](/index.php/ALSA "ALSA") how-to. For a more complete solution (with greater options) consider installing [PulseAudio](/index.php/PulseAudio "PulseAudio").

## Multimedia keys

A modern Desktop Environment will take care of this Automatically. However to manually enable the multimedia keys (volume up/down/mute), create a file *.Xmodmap* in your home directory, add the following lines:

```
keycode 160 = XF86AudioMute
keycode 176 = XF86AudioRaiseVolume
keycode 174 = XF86AudioLowerVolume

```

and restart X.

# Video

The free [xf86-video-driver](/index.php/ATI "ATI") driver works perfectly for the Radeon Xpress 200M that ships with the nx6325\. The proprietry [catalyst](/index.php/ATI#ATI_Catalyst_proprietary_driver "ATI") driver no longer works for this card, support has been dropped.

## Xorg.conf

Xorg now automatically takes care of the Xorg configuration. No xorg.conf is needed, however if one is presented it will attempt to load it.

For troubleshooting or setting up a complicated environment, refer to [Xorg](/index.php/Xorg "Xorg")

# Fingerprint, card slots, etc.

The multi-card reader work out-of-the-box with the latest kernel.

The Authentec fingerprint reader works with the installation and configuration of [fprint](/index.php/Fprint "Fprint")