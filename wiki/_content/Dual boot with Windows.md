# Dual boot with Windows

Related articles

*   [Dual boot with Windows/SafeBoot](/index.php/Dual_boot_with_Windows/SafeBoot "Dual boot with Windows/SafeBoot")

This is a simple article detailing different methods of Arch/Windows coexistence.

## Contents

*   [1 Important information](#Important_information)
    *   [1.1 Windows UEFI vs BIOS limitations](#Windows_UEFI_vs_BIOS_limitations)
    *   [1.2 Install media limitations](#Install_media_limitations)
    *   [1.3 Bootloader UEFI vs BIOS limitations](#Bootloader_UEFI_vs_BIOS_limitations)
    *   [1.4 UEFI Secure Boot](#UEFI_Secure_Boot)
    *   [1.5 Fast Start-Up](#Fast_Start-Up)
    *   [1.6 Windows filenames limitations](#Windows_filenames_limitations)
*   [2 Installation](#Installation)
    *   [2.1 BIOS systems](#BIOS_systems)
        *   [2.1.1 Using a Linux boot loader](#Using_a_Linux_boot_loader)
        *   [2.1.2 Using Windows boot loader](#Using_Windows_boot_loader)
            *   [2.1.2.1 Windows Vista/7/8/8.1 boot loader](#Windows_Vista.2F7.2F8.2F8.1_boot_loader)
    *   [2.2 UEFI systems](#UEFI_systems)
    *   [2.3 Troubleshooting](#Troubleshooting)
        *   [2.3.1 Couldn't create a new partition or locate an existing one](#Couldn.27t_create_a_new_partition_or_locate_an_existing_one)
*   [3 Time standard](#Time_standard)
*   [4 See also](#See_also)

## Important information

### Windows UEFI vs BIOS limitations

Microsoft imposes limitations on which firmware boot mode and partitioning style can be supported based on the version of Windows used:

*   **Windows XP** both **x86 32-bit** and **x86_64** (also called x64) (RTM and all Service Packs) versions do not support booting in UEFI mode (IA32 or x86_64) from any disk (MBR or GPT) OR in BIOS mode from GPT disk. They support only BIOS boot and only from MBR/msdos disk.
*   **Windows Vista** or **7** **x86 32-bit** (RTM and all Service Packs) versions support booting in BIOS mode from MBR/msdos disks only, not from GPT disks. They do not support x86_64 UEFI or IA32 (x86 32-bit) UEFI boot. They support only BIOS boot and only from MBR/msdos disk.
*   **Windows Vista RTM x86_64** (only RTM) version support booting in BIOS mode from MBR/msdos disks only, not from GPT disks. It does not support x86_64 UEFI or IA32 (x86 32-bit) UEFI boot. It supports only BIOS boot and only from MBR/msdos disk.
*   **Windows Vista** (SP1 and above, not RTM) and **Windows 7** **x86_64** versions support booting in x86_64 UEFI mode from GPT disk only, OR in BIOS mode from MBR/msdos disk only. They do not support IA32 (x86 32-bit) UEFI boot from GPT/MBR disk, x86_64 UEFI boot from MBR/msdos disk, or BIOS boot from GPT disk.
*   **Windows 8/8.1 x86 32-bit** support booting in IA32 UEFI mode from GPT disk only, OR in BIOS mode from MBR/msdos disk only. They do not support x86_64 UEFI boot from GPT/MBR disk, x86_64 UEFI boot from MBR/msdos disk, or BIOS boot from GPT disk. On market, the only systems known to ship with IA32 (U)EFI are some old Intel Macs (pre-2010 models?) and Intel Atom System-on-Chip (Clover trail and Bay Trail) Windows Tablets. in which it boots ONLY in IA32 UEFI mode and ONLY from GPT disk.
*   **Windows 8/8.1** **x86_64** versions support booting in x86_64 UEFI mode from GPT disk only, OR in BIOS mode from MBR/msdos disk only. They do not support IA32 UEFI boot, x86_64 UEFI boot from MBR/msdos disk, or BIOS boot from GPT disk.

In case of pre-installed Systems:

*   All systems pre-installed with Windows XP, Vista or 7 32-bit, irrespective of Service Pack level, bitness, edition (SKU)or presence of UEFI support in firmware, boot in BIOS-MBR mode by default.
*   MOST of the systems pre-installed with Windows 7 x86_64, irrespective of Service Pack level, bitness or edition (SKU), boot in BIOS-MBR mode by default. Very few recent systems pre-installed with Windows 7 are known to boot in x86_64 UEFI-GPT mode by default.
*   ALL systems pre-installed with Windows 8/8.1 boot in UEFI-GPT mode. The firmware bitness matches the bitness of Windows, ie. x86_64 Windows 8/8.1 boot in x86_64 UEFI mode and 32-bit Windows 8/8.1 boot in IA32 UEFI mode.

The best way to detect the boot mode of Windows is to do the following (info from [here](http://www.eightforums.com/tutorials/29504-bios-mode-see-if-windows-boot-uefi-legacy-mode.html)):

*   Boot into Windows
*   Press Win key and 'R' to start the Run dialog
*   In the Run dialog type "msinfo32" and press Enter
*   In the **System Information** windows, select **System Summary** on the left and check the value of **BIOS mode** item on the right
*   If the value is **UEFI**, Windows boots in UEFI-GPT mode. If the value is **Legacy**, Windows boots in BIOS-MBR mode.

In general, Windows forces type of partitioning depending on the firmware mode used, i.e. if Windows is booted in UEFI mode, it can be installed only to a GPT disk. If the Windows is booted in Legacy BIOS mode, it can be installed only to a MBR (also called **msdos** style partitioning) disk. This is a limitation enforced by Windows installer, and as of April 2014 there is no officially (Microsoft) supported way of installing Windows in UEFI-MBR or BIOS-GPT configuration. Thus Windows only supports either UEFI-GPT boot or BIOS-MBR configuration.

Such a limitation is not enforced by the Linux kernel, but can depend on which bootloader is used and/or how the bootloader is configured. The Windows limitation should be considered if the user wishes to boot Windows and Linux from the same disk, since installation procedure of bootloader depends on the firmware type and disk partitioning configuration. In case where Windows and Linux dual boot from the same disk, it is advisable to follow the method used by Windows, ie. either go for UEFI-GPT boot or BIOS-MBR boot. See [http://support.microsoft.com/kb/2581408](http://support.microsoft.com/kb/2581408) for more info.

### Install media limitations

Intel Atom System-on-Chip Tablets (Clover trail and Bay Trail) provide only IA32 UEFI firmware WITHOUT Legacy BIOS (CSM) support (unlike most of the x86_64 UEFI systems), due to Microsoft Connected Standby Guidelines for OEMs. Due to lack of Legacy BIOS support in these systems, and the lack of 32-bit UEFI boot in Arch Official Install ISO or the Archboot iso (as of April 2014), these install media cannot boot in Atom SoC tablets pre-installed with Windows 8/8.1 32-bit.

### Bootloader UEFI vs BIOS limitations

Most of the linux bootloaders installed for one firmware type cannot launch or chainload bootloaders of other firmware type. That is, if Arch is installed in UEFI-GPT or UEFI-MBR mode in one disk and Windows is installed in BIOS-MBR mode in another disk, the UEFI bootloader used by Arch cannot chainload the BIOS installed Windows in the other disk. Similarly if Arch is installed in BIOS-MBR or BIOS-GPT mode in one disk and Windows is installed in UEFI-GPT in another disk , the BIOS bootloader used by Arch cannot chainload UEFI installed Windows in the other disk.

The only exceptions to this are grub(2) in Apple Macs in which EFI installed grub(2) can boot BIOS installed OS via **appleloader** command (does not work in non-Apple systems), and rEFInd which technically supports booting legacy BIOS OS from UEFI systems, but [does not always work in non-Apple UEFI systems](http://rodsbooks.com/refind/using.html#legacy) as per its author Rod Smith.

However if Arch is installed in BIOS-GPT in one disk and Windows is installed in BIOS-MBR mode in another disk, then the BIOS bootloader used by Arch CAN boot the Windows in the other disk, if the bootloader itself has the ability to chainload from another disk.

**Note:** If Arch and Windows are dual-booting from same disk, then Arch SHOULD follow the same firmware boot mode and partitioning combination used by the installed Windows in the disk.

### UEFI Secure Boot

All pre-installed Windows 8/8.1 systems by default boot in UEFI-GPT mode and have UEFI Secure Boot enabled by default (which can be manually disabled by the user) and Legacy BIOS support (CSM) disabled by default (which can be manually enabled by the user, if the firmware supports it) in the firmware. This is mandated by Microsoft for all OEM pre-installed systems.

Arch Linux install media currently supports Secure Boot but it requires some manual steps by the user to [setup the HashTool while booting](/index.php/UEFI#Secure_Boot "UEFI"). There it is advisable to disable UEFI Secure Boot in the firmware setup before attempting to boot Arch Linux. Windows 8/8.1 SHOULD continue to boot fine even if Secure boot is disabled.

The only issue with regards to disabling UEFI Secure Boot support is that it requires physical access to the system to disable secure boot option in the firmware setup, as Microsoft has explicitly forbidden presence of any method to remotely or programmatically (from within OS) disable secure boot in all Windows 8/8.1 pre-installed systems

### Fast Start-Up

Fast Start-Up is a feature in Windows 8 that hibernates the computer rather than actually shutting it down to speed up boot times. Your system can lose data if Windows hibernates and you dual boot into another OS and make changes to files. Even if you do not intend to share filesystems, the EFI System Partition is likely to be damaged on an EFI system. Therefore, you should disable Fast Startup, as described [here](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html), before you install Linux on any computer that uses Windows 8.

[ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) added a [safe-guard](http://sourceforge.net/p/ntfs-3g/ntfs-3g/ci/559270a8f67c77a7ce51246c23d2b2837bcff0c9/) to prevent read-write mounting of hibernated disks, but the NTFS driver within the Linux kernel has no such safeguard.

### Windows filenames limitations

Windows is limited to filepaths being shorter than [260 characters](http://blogs.msdn.com/b/bclteam/archive/2007/02/13/long-paths-in-net-part-1-of-3-kim-hamilton.aspx).

Windows also puts [certain characters off limits](http://msdn.microsoft.com/en-us/library/aa365247(VS.85).aspx#naming_conventions) in filenames for reasons that run all the way back to DOS:

*   < (less than)
*   > (greater than)
*   : (colon)
*   " (double quote)
*   / (forward slash)
*   \ (backslash)
*   | (vertical bar or pipe)
*   ? (question mark)
*   * (asterisk)

These are limitations of Windows and not NTFS: any other OS using the NTFS partition will be fine. Windows will fail to detect these files and running `chkdsk` will most likely cause them to be deleted. This can lead to potential data-loss.

**NTFS-3G** applies Windows restrictions to new file names through the [windows_filenames](http://www.tuxera.com/community/ntfs-3g-manual/#4) option (see [fstab](/index.php/Fstab "Fstab")).

## Installation

The recommended way to setup a Linux/Windows dual booting system is to first install Windows, only using part of the disk for its partitions. When you have finished the Windows setup, boot into the Linux install environment where you can create additional partitions for Linux while leaving the existing Windows partitions untouched. The Windows installation will create the EFI System Partition which can be used by your Linux bootloader.

### BIOS systems

#### Using a Linux boot loader

You may use [GRUB](/index.php/GRUB#Dual-booting "GRUB") or [Syslinux](/index.php/Syslinux#Chainloading "Syslinux").

#### Using Windows boot loader

With this setup the Windows bootloader loads GRUB which then boots Arch.

##### Windows Vista/7/8/8.1 boot loader

The following section contains excerpts from [http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/](http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/).

In order to have the Windows boot loader see the Linux partition, one of the Linux partitions created needs to be FAT32 (in this case, `/dev/sda3`). The remainder of the setup is similar to a typical installation. Some documents state that the partition being loaded by the Windows boot loader must be a primary partition but I have used this without problem on an extended partition.

*   When installing the GRUB boot loader, install it on your `/boot` partition rather than the MBR.

    **Note:** For instance, my `/boot` partition is `/dev/sda5`. So I installed GRUB at `/dev/sda5` instead of `/dev/sda`. For help on doing this, see [GRUB#Install to partition or partitionless disk](/index.php/GRUB#Install_to_partition_or_partitionless_disk "GRUB")

*   Under Linux make a copy of the boot info by typing the following at the command shell:

```
my_windows_part=/dev/sda3
my_boot_part=/dev/sda5
mkdir /media/win
mount $my_windows_part /media/win
dd if=$my_boot_part of=/media/win/linux.bin bs=512 count=1

```

*   Boot to Windows and open up and you should be able to see the FAT32 partition. Copy the linux.bin file to `C:\`. Now run **cmd** with administrator privileges (navigate to _Start > All Programs > Accessories_, right-click on _Command Prompt_ and select _Run as administrator_):

```
bcdedit /create /d “Linux” /application BOOTSECTOR

```

*   BCDEdit will return an alphanumeric identifier for this entry that I will refer to as {ID} in the remaining steps. You will need to replace {ID} by the actual returned identifier. An example of {ID} is {d7294d4e-9837-11de-99ac-f3f3a79e3e93}.

```
bcdedit /set {ID} device partition=c:
bcdedit /set {ID}  path \linux.bin
bcdedit /displayorder {ID} /addlast
bcdedit /timeout 30

```

Reboot and enjoy. In my case I'm using the Windows boot loader so that I can map my Dell Precision M4500's second power button to boot Linux instead of Windows.

### UEFI systems

If you already have Windows installed, it will already have created some partitions (on a [GPT](/index.php/GPT "GPT")-formatted disk):

*   a partition of type `ef00 EFI System` and filesystem {{ic|FAT32},
*   a partition of type `0c01 Microsoft reserved`, generally of size `128 MiB`,
*   a partition of type `0700 Microsoft basic data` and of filesystem {{ic|NTFS}, which corresponds to `C:\`,
*   potentially system recovery and backup partitions and/or secondary data partitions (corresponding often to `D:\` and above).

Using the Disk Management utility in Windows, check how the partitions are labelled and which type gets reported. This will help you understand which partitions are essential to Windows, and which others you might repurpose: the first 3 bullets in the above list are essential, do not delete them.

You can then proceed with [partitioning](/index.php/Partitioning "Partitioning"), depending on your needs. Mind that there is no need to create an additional EFI System Partition, since it already exists (see above): when required, [mount](/index.php/Mount "Mount") this to `/boot`, install your [bootloader](/index.php/Bootloader "Bootloader") to it and save the entry in `/etc/[fstab](/index.php/Fstab "Fstab")`.

Concerning bootloaders, [systemd-boot](/index.php/Systemd-boot "Systemd-boot") and [rEFInd](/index.php/REFInd "REFInd") autodetect _Windows Boot Manager_ (`\EFI\Microsoft\Boot\bootmgfw.efi`) and show it in their boot menu automatically. For [GRUB](/index.php/GRUB "GRUB") follow [GRUB#Windows installed in UEFI-GPT Mode menu entry](/index.php/GRUB#Windows_installed_in_UEFI-GPT_Mode_menu_entry "GRUB"). Syslinux (as of version 6.02 and 6.03-pre9) and ELILO do not support chainloading other EFI applications, so they cannot be used to boot `\EFI\Microsoft\Boot\bootmgfw.efi`.

Computers that come with newer versions of Windows often have [secure boot](/index.php/UEFI#Secure_Boot "UEFI") enabled. You will need to take extra steps to either disable secure boot or to make your installation media compatible with secure boot (see above and in the linked page).

### Troubleshooting

#### Couldn't create a new partition or locate an existing one

The usb-stick for installing Windows 8.1 seems to need a MBR partition table (not GPT), otherwise the installation gets confused and prints something like "Couldn't create a new partition or locate an existing one", although the partitions were created.

## Time standard

*   Recommended: Set both Arch Linux and Windows to use UTC, following [Time#UTC in Windows](/index.php/Time#UTC_in_Windows "Time"). Also, be sure to prevent Windows from synchronizing the time on-line, because the hardware clock will default back to _localtime_.

*   Not recommended: Set Arch Linux to _localtime_ and disable any time-related services, like [NTPd](/index.php/NTPd "NTPd") . This will let Windows take care of hardware clock corrections and you will need to remember to boot into Windows at least two times a year (in Spring and Autumn) when [DST](https://en.wikipedia.org/wiki/Daylight_saving_time "wikipedia:Daylight saving time") kicks in. So please do not ask on the forums why the clock is one hour behind or ahead if you usually go for days or weeks without booting into Windows.

## See also

*   [Booting Windows from a desktop shortcut](https://bbs.archlinux.org/viewtopic.php?id=140049)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dual_boot_with_Windows&oldid=415619](https://wiki.archlinux.org/index.php?title=Dual_boot_with_Windows&oldid=415619)"