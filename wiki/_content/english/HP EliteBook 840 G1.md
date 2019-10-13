| **Device** | **Status** | **Modules** |
| Intel graphics | **Working** | xf86-video-intel |
| AMD graphics ([PRIME](/index.php/PRIME "PRIME")) | **Working** | xf86-video-amdgpu |
| HDMI | **Working** | xf86-video-intel |
| Ethernet | **Working** |
| Wireless | **Working** |
| Bluetooth | **Working** |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** | xf86-input-synaptics |
| Camera | **Working** | uvcvideo |
| Fingerprint reader | **Working** | fprintd-vfs_proprietary |
| USB 3.0 | **Working** | xhci-hcd |
| Memory Card Reader | **Working** |
| Smart Card Reader | **Working** | ccid, pcsclite |
| Function Keys | **Working** |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 UEFI Setup](#UEFI_Setup)
        *   [1.1.1 Using the "Customized Boot" path option (recommended)](#Using_the_"Customized_Boot"_path_option_(recommended))
        *   [1.1.2 Change the OS boot loader path to match the hard coded path](#Change_the_OS_boot_loader_path_to_match_the_hard_coded_path)
    *   [1.2 Encryption](#Encryption)
    *   [1.3 AMD Graphics](#AMD_Graphics)
    *   [1.4 Audio](#Audio)
    *   [1.5 Wireless](#Wireless)
    *   [1.6 Resume / wake on lid open](#Resume_/_wake_on_lid_open)
    *   [1.7 Enable the microphone muting key](#Enable_the_microphone_muting_key)
*   [2 See also](#See_also)

## Configuration

### UEFI Setup

**Note:** Make sure you have the latest HP [UEFI](/index.php/UEFI "UEFI") firmware installed.

Even if [UEFI](/index.php/UEFI "UEFI"), [Arch Linux](/index.php/Arch_Linux "Arch Linux") and (e.g.) [GRUB](/index.php/GRUB "GRUB") are correctly configured and with the correct UEFI NVRAM variables set, the system will not boot from the HDD/SSD. The problem is that HP hard coded the paths for the OS boot manager in their UEFI boot manager to `\EFI\Microsoft\Boot\bootmgfw.efi` to boot Microsoft Windows, regardless of how the UEFI NVRAM variables are changed. There are two workarounds:

#### Using the "Customized Boot" path option (recommended)

The latest HP firmware allows defining a “Customized Boot” path in the UEFI pre-boot graphical environment. Select the “Customized Boot” option in the UEFI pre-boot graphical environment under “Boot Options” and set the path to your OS boot loader on the ESP (see [UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI")), e.g.:

`\EFI\grub\grubx64.efi`

Always verify the correct path to the .efi file. Also, adjust the device boot order (also in the UEFI pre-boot graphical environment) to boot this entry first.

#### Change the OS boot loader path to match the hard coded path

**Warning:** If you are trying to boot on a the mSATA port (m.2 SSD), this is the only working method.

**Warning:** This method is not recommended, as it will create conflicts in a dual boot setup with Microsoft Windows. Also, everytime you install GRUB, you have to remember to copy it to the hard coded path.

Change the UEFI application path of the OS boot loader to that hard coded path. On your ESP (see [UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI"); e.g. with the $MOUNTPOINT `/boot/efi`), do (e.g. with [GRUB](/index.php/GRUB "GRUB") entry `grub_archlinux`):

```
 # mkdir -p $MOUNTPOINT/EFI/Microsoft/Boot
 # cp $MOUNTPOINT/EFI/grub/grubx64.efi $MOUNTPOINT/EFI/Microsoft/Boot/bootmgfw.efi

```

or

```
 # mkdir -p $MOUNTPOINT/EFI/Boot
 # cp $MOUNTPOINT/EFI/grub/grubx64.efi $MOUNTPOINT/EFI/Boot/Bootx64.efi

```

### Encryption

This notebook supports [HDD FDE (SED)](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption#Hard_disk_drive_FDE "wikipedia:Hardware-based full disk encryption"). The HDD/SSD can be locked by setting a password in the UEFI pre-boot graphical environment under the option "DriveLock" (this requires setting a password for the UEFI pre-boot graphical environment first). If you replace the HDD/SSD, make sure to get a compatible one to make use of this feature.

Otherwise, see [Disk encryption](/index.php/Disk_encryption "Disk encryption") for software-based encryption.

### AMD Graphics

In order to get the dedicated AMD graphics card to function properly, install [AMDGPU](/index.php/AMDGPU "AMDGPU") first. Set the following kernel parameters: `amdgpu.si_support=1 radeon.si_support=0`.

Now, any application run with `DRI_PRIME=1` (as described for using [PRIME](/index.php/PRIME "PRIME")) is using the dedicated GPU.

### Audio

For HDMI Audio you need `CONFIG_INTEL_IOMMU_DEFAULT_ON=n` in your kernel config (see [https://bugzilla.kernel.org/show_bug.cgi?id=61471](https://bugzilla.kernel.org/show_bug.cgi?id=61471)). In some cases, you will need `options snd-hda-intel enable=1,1,0` in `/etc/modprobe.d/snd-hda-intel.conf`. This will prevent freezes caused by hdmi audio cards conflicting.

### Wireless

Set `CONFIG_HP_WIRELESS=y` in your kernel config to enable the hardware button (Linux 3.14+).

### Resume / wake on lid open

This feature needs to be enabled in the bios / uefi setup: *Advanced > Built-in device options > Wake unit from sleep when lid is opened*

### Enable the microphone muting key

If your mute mic key (fn+F8) does not work, you actually just need to remap this key manually.

Here is an example of how you can do this by adding a custom mapping file:

 `/etc/udev/hwdb.d/61-hp-mic-mute-hotkey.hwdb` 
```
evdev:atkbd:dmi:bvn*:bvr*:bd*:svnHewlett-Packard*:pn*EliteBook*:pvr*
 KEYBOARD_KEY_81=f20                          # Fn+F8 on Elitebook, map to F20

```

**Warning:** It is strongly recommanded to understand [scancodes to keycodes mapping](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes") before doing this.

Then, you just need to regenerate and reload your `hwdb.bin` file:

```
# systemd-hwdb update
# udevadm trigger

```

**Note:** This also work for the HP EliteBook 840 G2 and the EliteBook 820 series.

## See also

*   [UEFI, GNU/Linux and HP notebooks – problems and how to get it working](http://fomori.org/blog/?p=892)

*   [Changing Boot Order on Dual Boot Windows 8 and Ubuntu](http://h30434.www3.hp.com/t5/Notebook-Operating-Systems-and-Software/Changing-Boot-Order-on-Dual-Boot-Windows-8-and-Ubuntu/td-p/2503733)

*   [Setting GRUB as the default boot manager on a UEFI-based system](https://bbs.archlinux.org/viewtopic.php?id=168904&p=1)

*   [Activate mic mute function key, ubuntu 18.04, HP Elitebook 820](https://gist.github.com/HappyCodingRobot/df400e16d0615e98e2c1eee738925d0b)