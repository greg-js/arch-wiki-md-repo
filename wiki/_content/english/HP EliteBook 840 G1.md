| **Device** | **Status** | **Modules** |
| Intel graphics | **Working** | xf86-video-intel |
| AMD graphics ([PRIME](/index.php/PRIME "PRIME")) | **Working** | xf86-video-ati |
| HDMI | **Working** | xf86-video-intel |
| Ethernet | **Working** |
| Wireless | **Working** |
| Bluetooth | **Working** |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** | xf86-input-synaptics |
| Camera | **Working** | uvcvideo |
| Fingerprint reader | **Not working** |
| USB 3.0 | **Working** | xhci-hcd |
| Memory Card Reader | **Working** |
| Smart Card Reader | **Working** | ccid, pcsclite |
| Function Keys | **Working (except mic.)** |

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 UEFI Setup](#UEFI_Setup)
        *   [1.1.1 Using the "Customized Boot" path option (recommended)](#Using_the_.22Customized_Boot.22_path_option_.28recommended.29)
        *   [1.1.2 Change the OS boot loader path to match the hard coded path](#Change_the_OS_boot_loader_path_to_match_the_hard_coded_path)
    *   [1.2 Encryption](#Encryption)
    *   [1.3 Audio](#Audio)
    *   [1.4 Wireless](#Wireless)
    *   [1.5 Resume / wake on lid open](#Resume_.2F_wake_on_lid_open)
*   [2 See also](#See_also)

## Configuration

### UEFI Setup

**Note:** Make sure you have the latest HP [UEFI](/index.php/UEFI "UEFI") firmware installed.

Even if [UEFI](/index.php/UEFI "UEFI"), [Arch Linux](/index.php/Arch_Linux "Arch Linux") and (e.g.) [GRUB](/index.php/GRUB "GRUB") are correctly configured and with the correct UEFI NVRAM variables set, the system will not boot from the HDD/SSD. The problem is that HP hard coded the paths for the OS boot manager in their UEFI boot manager to `\EFI\Microsoft\Boot\bootmgfw.efi` to boot Microsoft Windows, regardless of how the UEFI NVRAM variables are changed. There are two workarounds:

#### Using the "Customized Boot" path option (recommended)

The latest HP firmware allows defining a “Customized Boot” path in the UEFI pre-boot graphical environment. Select the “Customized Boot” option in the UEFI pre-boot graphical environment under “Boot Options” and set the path to your OS boot loader on the ESP (see [UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI")), e.g.:

`\EFI\grub_archlinux\grubx64.efi`

Always verify the correct path to the .efi file. Also, adjust the device boot order (also in the UEFI pre-boot graphical environment) to boot this entry first.

#### Change the OS boot loader path to match the hard coded path

**Warning:** This method is not recommended, as it will create conflicts in a dual boot setup with Microsoft Windows. Also, everytime you install GRUB, you have to remember to copy it to the hard coded path.

Change the UEFI application path of the OS boot loader to that hard coded path. On your ESP (see [UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI"); e.g. with the $MOUNTPOINT `/boot/efi`), do (e.g. with [GRUB](/index.php/GRUB "GRUB") entry `grub_archlinux`):

```
 # mkdir -p $MOUNTPOINT/EFI/Microsoft/Boot
 # cp $MOUNTPOINT/EFI/grub_archlinux/grubx64.efi $MOUNTPOINT/EFI/Microsoft/Boot/bootmgfw.efi

```

or

```
 # mkdir -p $MOUNTPOINT/EFI/Boot
 # cp $MOUNTPOINT/EFI/grub_archlinux/grubx64.efi $MOUNTPOINT/EFI/Boot/Bootx64.efi

```

### Encryption

This notebook supports [HDD FDE (SED)](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption#Hard_disk_drive_FDE). The HDD/SSD can be locked by setting a password in the UEFI pre-boot graphical environment under the option "DriveLock" (this requires setting a password for the UEFI pre-boot graphical environment first). If you replace the HDD/SSD, make sure to get a compatible one to make use of this feature.

Otherwise, see [Disk encryption](/index.php/Disk_encryption "Disk encryption") for software-based encryption.

### Audio

For HDMI Audio you need `CONFIG_INTEL_IOMMU_DEFAULT_ON=n` in your kernel config (see [https://bugzilla.kernel.org/show_bug.cgi?id=61471](https://bugzilla.kernel.org/show_bug.cgi?id=61471)). In some cases, you will need `options snd-hda-intel enable=1,1,0` in `/etc/modprobe.d/snd-hda-intel.conf`. This will prevent freezes caused by hdmi audio cards conflicting.

### Wireless

Set `CONFIG_HP_WIRELESS=y` in your kernel config to enable the hardware button (Linux 3.14+).

### Resume / wake on lid open

This feature needs to be enabled in the bios / uefi setup: _Advanced > Built-in device options > Wake unit from sleep when lid is opened_

## See also

*   [UEFI, GNU/Linux and HP notebooks – problems and how to get it working](http://fomori.org/blog/?p=892)

*   [Changing Boot Order on Dual Boot Windows 8 and Ubuntu](http://h30434.www3.hp.com/t5/Notebook-Operating-Systems-and-Software/Changing-Boot-Order-on-Dual-Boot-Windows-8-and-Ubuntu/td-p/2503733)

*   [Setting GRUB as the default boot manager on a UEFI-based system](https://bbs.archlinux.org/viewtopic.php?id=168904&p=1)