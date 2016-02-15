This page outlines installation tips for Archlinux on the Lenovo Thinkpad S540, and tips on getting the best setup, and known cavaets.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Before Installation](#Before_Installation)
    *   [1.2 During Installation](#During_Installation)
*   [2 Known issues](#Known_issues)

## Installation

### Before Installation

In the BIOS (press enter when the Lenovo Logo appears on screen):

*   Disable Secure Boot
*   Set Boot type to either Both (Legacy First) or Legacy Only (UEFI Installation has yet to be successful - but see comment below by a second S540 owner))
*   With Windows 8.1 already on the system a dual boot uefi system with Windows 8.1 and ArchLinux works fine - tested with rEFInd as the boot manager. Not only must Secure Boot be switched off but Fastboot must be turned off from within Windows 8.1 prior to the installation of ArchLinux otherwise a hybrid sleep mode is entered when Windows shuts down. Care is needed during the installation of Archlinux to add the necessary boot files to the existing ESP which needs to be included in the fstab partitions.

### During Installation

By default the system won't boot due to issues with the intel video chip.

Edit `/etc/default/grub` and change `GRUB_CMDLINE_LINUX` to the value `"intel.modeset=0"` and re-run `grub-mkconfig`. This will fix the video bug.

## Known issues

Currently known cavets with Arch Linux on the s540 are:

*   Touch screen sometimes doesn't re-activate after system is placed in sleep mode (requires reboot)
*   Default soft-buttons on the touch pad don't match the markings.This page outlines installation tips for Archlinux on the Lenovo Thinkpad S540, and tips on getting the best setup, and known cavaets.