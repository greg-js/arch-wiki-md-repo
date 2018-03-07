This article covers the installation and configuration of Arch Linux on a Lenovo T440s laptop.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 UEFI vs BIOS](#UEFI_vs_BIOS)
    *   [1.2 Driver Selection](#Driver_Selection)
    *   [1.3 Tp_smapi](#Tp_smapi)
*   [2 Tweaks](#Tweaks)
    *   [2.1 Screen resolution and scaling](#Screen_resolution_and_scaling)
    *   [2.2 Backlight](#Backlight)
    *   [2.3 Touchpad](#Touchpad)
*   [3 Updating the BIOS](#Updating_the_BIOS)

## Installation

### UEFI vs BIOS

The T440S has Secure Boot and dual UEFI/BIOS boot enabled by default. Unless you are comfortable in attempting to set up UEFI boot, it's simpler to get an after-market operating system installed if the booting is switched to BIOS-only. In the BIOS/EFI menu, set booting to "Legacy Only" (which uses BIOS emulation instead of EFI).

If using UEFI for your installation, you may want to consider the following:

*   Secure Boot must be disabled in order to boot a non-Windows operating system. Go to *Security > Secure Boot* and set Secure Boot to Disabled. You may also want to put it into Setup/Custom Mode.
*   If the security chip is enabled, this can sometimes prevent your bootloader's bootx64.efi from being booted. Under *Security > Security Chip*, set Security Chip Selection to Discrete TPM and Security Chip to Disabled.

### Driver Selection

| Device | Driver Package |
| Video | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| ClickPad | [libinput](/index.php/Libinput "Libinput") |
| Wireless/Bluetooth | iwlwifi* |
| Finger Print Reader | [Fprint](/index.php/Fprint "Fprint") since V 0.6.0 |
| SD-Card Reader (Realtek RTS5227) | [rts5227-dkms](https://aur.archlinux.org/packages/rts5227-dkms/) |

Note*: Depending on what you picked when ordering the laptop, you might have a stock ThinkPad wireless card. Check [this page](http://www.thinkwiki.org/wiki/Drivers) for more information.

### Tp_smapi

See [tp_smapi](/index.php/Tp_smapi "Tp smapi") and a configuration for [ThinkPad T420](/index.php/Lenovo_ThinkPad_T420#Tp_smapi "Lenovo ThinkPad T420").

## Tweaks

### Screen resolution and scaling

In order to use the real dpi value create the file (`/etc/X11/xorg.conf.d/90-monitor.conf`):

```
Section "Monitor"
    Identifier             "<default monitor>"
    DisplaySize            309 173    # In millimeters
EndSection

```

Otherwise the defalut resolution is set to 96dpi.

If you have a 1920x1080 FHD panel installed and find that text and UI elements are too small, it may interest you to consider using [display scaling](/index.php/HiDPI "HiDPI") to adjust the size of UI elements to your preference. Integer HiDPI scaling is likely too excessive for a display of this resolution and size, so you will want to consider a fractional scaling solution.

### Backlight

See [Backlight](/index.php/Backlight "Backlight").

### Touchpad

Most responsive configuration is obtained through [xinput](/index.php/Xinput "Xinput").

Decent Synaptics configuration, utilizing sane settings for the X1-Carbon:

*   ["R's Circus" Synaptics configuration](http://rscircus.org/post/72978821261/t440s-clickpad-fix-which-feels-good)

## Updating the BIOS

**Warning:** Flashing motherboard BIOS is a dangerous activity that can render your motherboard inoperable!

See [Flashing BIOS from Linux#Bootable optical disk emulation](/index.php/Flashing_BIOS_from_Linux#Bootable_optical_disk_emulation "Flashing BIOS from Linux") and [Updating the BIOS on my ThinkPad T440](http://www.lenzg.net/archives/358-Updating-the-BIOS-on-my-ThinkPad-T440-without-Windows-or-a-DVD-Drive.html)