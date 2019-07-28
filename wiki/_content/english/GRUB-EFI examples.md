It is well known that different motherboard manufactures implement UEFI differently. The purpose of this page is to show hardware-specific methods known to work when installing/restoring GRUB in EFI mode.

**Note:** In the entire article `*esp*` denotes the mountpoint of the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") aka ESP.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Apple Macs](#Apple_Macs)
*   [2 Asus](#Asus)
    *   [2.1 Z68 Family and U47 Family](#Z68_Family_and_U47_Family)
    *   [2.2 ux32vd](#ux32vd)
    *   [2.3 P8Z77 Family](#P8Z77_Family)
    *   [2.4 M5A97](#M5A97)
*   [3 Asrock](#Asrock)
    *   [3.1 Z97M Pro4](#Z97M_Pro4)
*   [4 Dell](#Dell)
    *   [4.1 PowerEdge T30](#PowerEdge_T30)
*   [5 MSI](#MSI)
    *   [5.1 B250M PRO-VH](#B250M_PRO-VH)
    *   [5.2 B150 PC MATE / B250 PC MATE / H110I PRO / Z370 GAMING PLUS](#B150_PC_MATE_/_B250_PC_MATE_/_H110I_PRO_/_Z370_GAMING_PLUS)
*   [6 HP](#HP)
    *   [6.1 EliteBook 840 G1](#EliteBook_840_G1)
*   [7 Intel](#Intel)
    *   [7.1 S5400 Family](#S5400_Family)
*   [8 Lenovo](#Lenovo)
    *   [8.1 K450 IdeaCentre](#K450_IdeaCentre)
    *   [8.2 M92p ThinkCentre](#M92p_ThinkCentre)
    *   [8.3 X270 Thinkpad](#X270_Thinkpad)

## Apple Macs

Use bless command from within macOS to set `grubx64.efi` as the default boot option. You can also boot from the macOS install disc and launch a Terminal there if you only have Linux installed. In the Terminal, create a directory and mount the [EFI system partition](/index.php/EFI_system_partition "EFI system partition"):

```
# cd /Volumes
# mkdir efi
# mount -t msdos /dev/disk0s1 /Volumes/efi

```

Then run bless on `grub.efi` and on the EFI system partition to set them as the default boot options.

```
# bless --folder=/Volumes/efi --file=/Volumes/efi/EFI/GRUB/grubx64.efi --setBoot
# bless --mount=/Volumes/efi --file=/Volumes/efi/EFI/GRUB/grubx64.efi --setBoot

```

More info at [https://help.ubuntu.com/community/UEFIBooting#Apple_Mac_EFI_systems_.28both_EFI_architecture.29](https://help.ubuntu.com/community/UEFIBooting#Apple_Mac_EFI_systems_.28both_EFI_architecture.29).

**Note:**

*   TODO: GRUB upstream Bazaar mactel branch [http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes](http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes). No further update from grub developers.
*   TODO: Experimental "bless" utility for Linux by Fedora developers - [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/). Requires more testing.

## Asus

### Z68 Family and U47 Family

```
# cp *esp*/EFI/GRUB/grubx64.efi *esp*/shellx64.efi

```

After this launch the UEFI Shell from the UEFI setup/menu (in ASUS UEFI BIOS, switch to advanced mode, press *Exit* in the top right corner and choose "Launch EFI shell from filesystem device"). The GRUB menu will show up and you can boot into your system. Afterwards you can use [efibootmgr](/index.php/Efibootmgr "Efibootmgr") to setup a menu entry, for example if you have the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") on `/dev/sda1`:

```
# efibootmgr --create --disk /dev/sda --part 1 --write-signature --loader /EFI/GRUB/grubx64.efi --label "GRUB" --verbose

```

If your motherboard has no such option (or even if it does), you can use [UEFI shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") to create a UEFI boot option for the Arch partition temporarily.

Once you boot into the UEFI shell, add a UEFI boot menu entry:

```
Shell> bcfg boot add 0 FS0:\EFI\GRUB\grubx64.efi "GRUB"

```

where `FS0:` is the mapping corresponding to the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") and `\EFI\GRUB\grubx64.efi` is the the from the `--bootloader-id` from the `grub-install` command above.

This will temporarily add a UEFI boot option for the next boot to get into Arch. Once in Arch, `modprobe efivars` and confirm that `efibootmgr` creates no errors (no errors meaning you successfully booted in UEFI mode). Then [GRUB installation](/index.php/GRUB#Installation_2 "GRUB") can be performed again and should successfully permanently add a boot entry in the UEFI menu.

### ux32vd

**Note:** The BIOS does not allow computer to boot from GPT disk if there is no properly set-up UEFI boot entry. The disk even may not be seen in BIOS in this case. The fix is to make a proper UEFI boot entry.

There is a caveat. If the machine was booted from MBR then `grub-install` (or [efibootmgr](/index.php/Efibootmgr "Efibootmgr")) will fail to create the UEFI boot entry with the following error:

```
EFI variables are not supported on this system

```

You first need to boot the machine with EFI and then create the boot entry. This can be done the way described for Z68 Family: by copying `*esp*/EFI/GRUB/grubx64.efi` into `*esp*/shellx64.efi` and selecting "Launch EFI shell from filesystem device". After successful boot it is possible to create a boot entry using [grub-install](/index.php/GRUB#Installation_2 "GRUB") or [efibootmgr](/index.php/Efibootmgr "Efibootmgr").

### P8Z77 Family

[Install GRUB](/index.php/GRUB#Installation_2 "GRUB") and copy the [modified UEFI Shell binary](/index.php/Unified_Extensible_Firmware_Interface#Obtaining_UEFI_Shell "Unified Extensible Firmware Interface") to [ESP](/index.php/ESP "ESP").

The [EFI system partition](/index.php/EFI_system_partition "EFI system partition") should contain just two files:

```
/Shell.efi
/EFI/GRUB/grubx64.efi

```

*   Reboot and enter the BIOS (the `Delete` key will do this).
*   Using the arrow keys, move to the *exit* menu and drop down to the *EFI shell*.
*   Add an entry for Arch to the menu. Below is an example, see the [Unified Extensible Firmware Interface#Launching UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#Launching_UEFI_Shell "Unified Extensible Firmware Interface") article for more.

**Within UEFI shell**

```
Shell> bcfg boot dump -v
Shell> bcfg boot add 1 FS0:\EFI\GRUB\grubx64.efi "GRUB"
Shell> exit

```

*   Reboot the machine and enter the BIOS.
*   Navigate to the *Boot* section and adjust the boot order to with the "GRUB" being the one on the SSD.
*   Boot to this entry and enjoy.

### M5A97

Finish the standard Arch install procedures, making sure that you partition your boot hard disk as GPT.

[Install GRUB](/index.php/GRUB#Installation_2 "GRUB") and copy the [modified UEFI Shell binary](/index.php/Unified_Extensible_Firmware_Interface#Obtaining_UEFI_Shell "Unified Extensible Firmware Interface") to [ESP](/index.php/ESP "ESP").

The reason that we need this shell application is that the `efibootmgr` command will fail silently during `grub-install`.

After this launch the UEFI Shell from the UEFI setup/menu (in ASUS UEFI BIOS, switch to advanced mode, press *Exit* in the top right corner and choose "Launch EFI shell from filesystem device"). The UEFI shell will show up. From here we need to add our GRUB entry to the NVRAM.

```
Shell> bcfg boot add 3 FS0:\EFI\GRUB\grubx64.efi "GRUB"

```

where `FS0:` is the mapping corresponding to the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") and `3` is the zero based boot entry index.

**Tip:** UEFI Shell commands usually support `-b` option which makes output pause after each page. `map` lists recognized filesystems (`fs0`, ...) and data storage devices (`blk0`, ...). Run `help -b` to list available commands. See [Unified Extensible Firmware Interface#Important UEFI Shell commands](/index.php/Unified_Extensible_Firmware_Interface#Important_UEFI_Shell_commands "Unified Extensible Firmware Interface") for more information.

To list the current boot entries you can run:

```
Shell> bcfg boot dump -v

```

## Asrock

### Z97M Pro4

This is a similar procedure to Asus Z68 Family. This was tested on a Z97M Pro4 BIOS P1.90.

```
# cp *esp*/EFI/GRUB/grubx64.efi *esp*/shellx64.efi

```

After this launch the UEFI Shell from the UEFI setup/menu (in ASROCK UEFI BIOS, goto *Exit* tab and choose "Launch EFI Shell From Filesystem Device"). The GRUB menu will show up and you can boot into your system. Afterwards you can use *efibootmgr* to setup a menu entry, for example if you have the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") on `/dev/sda1`:

```
# efibootmgr --create --disk /dev/sda --part 1 --write-signature --loader /EFI/GRUB/grubx64.efi --label "GRUB" --verbose

```

## Dell

### PowerEdge T30

The Dell UEFI implementation needs the [UEFI firmware workaround](/index.php/GRUB/Tips_and_tricks#UEFI_firmware_workaround "GRUB/Tips and tricks") to load grub. Otherwise it will drop into a "no OS found" screen.

## MSI

These MSI motherboards seem to want the EFI program to exist in a different location from where GRUB installs it. Do one of the following after following the instructions for installing [GRUB](/index.php/GRUB "GRUB"):

### B250M PRO-VH

```
# mkdir *esp*/EFI/BOOT
# cp *esp*/EFI/grub/grubx64.efi *esp*/EFI/BOOT/shellx64.efi

```

### B150 PC MATE / B250 PC MATE / H110I PRO / Z370 GAMING PLUS

Install GRUB to the [default/fallback boot path](/index.php/GRUB#Default/fallback_boot_path "GRUB").

**Note:** The procedures above probably also work for other MSI motherboards.

## HP

### EliteBook 840 G1

See [HP EliteBook 840 G1#UEFI Setup](/index.php/HP_EliteBook_840_G1#UEFI_Setup "HP EliteBook 840 G1") for details.

**Note:** The procedures in the link above probably also work for a range of other HP models.

## Intel

### S5400 Family

This board can run in BIOS or in EFI mode. BIOS mode requires an MBR partitioned hard drive, EFI - a GPT hard drive. Please note that this board operates on the Intel EFI v1.10 specification, and is IA32 (32-bit) only. The normal procedure for UEFI installation can be followed, with the exception of the following changes.

*   Instead of using the `grub-efi-x86_64` target, `grub-efi-i386` has to be used
*   The `bcfg` command is not available for pre-UEFI (v2.0) firmware. A `startup.nsh` file can be used on the root of the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") containing the path to the bootloader. For example: `FS0:\EFI\GRUB\grubia32.efi` has to be placed in the `startup.nsh` file on the root of the EFI system partition.
*   The `grub.cfg` file has to be placed in the same directory as the grub EFI binary, otherwise GRUB will not find it and enter the interactive shell.

## Lenovo

### K450 IdeaCentre

The EFI system partition requires the file `\EFI\BOOT\BOOTx64.efi` to be present in order to boot, otherwise you will receive "Error 1962: No operating system found. Boot sequence will automatically repeat."

Install GRUB to the [default/fallback boot path](/index.php/GRUB#Default/fallback_boot_path "GRUB").

This is a workaround for what is likely a bug in the UEFI implementation.

### M92p ThinkCentre

This system whitelists UEFI boot entries. It will only boot from a entry called "Red Hat Enterprise Linux". So specify the bootloader-id appropriately:

```
# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id="Red Hat Enterprise Linux" --recheck --debug

```

### X270 Thinkpad

Install GRUB to the [default/fallback boot path](/index.php/GRUB#Default/fallback_boot_path "GRUB").