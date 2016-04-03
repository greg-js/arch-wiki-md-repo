**翻译状态：** 本文是英文页面 [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-04-02，点击[and Arch Dual Boot&diff=0&oldid=308005 这里](https://wiki.archlinux.org/index.php?title=Windows)可以查看翻译后英文页面的改动。

This is a simple article detailing different methods of Arch/Windows coexistence.

## Contents

*   [1 Potential Data Loss](#Potential_Data_Loss)
    *   [1.1 Renaming Files on NTFS partitions](#Renaming_Files_on_NTFS_partitions)
    *   [1.2 Fast Start-Up](#Fast_Start-Up)
*   [2 Installation](#Installation)
    *   [2.1 BIOS Systems](#BIOS_Systems)
        *   [2.1.1 Using a Linux boot loader](#Using_a_Linux_boot_loader)
        *   [2.1.2 Using Windows boot loader](#Using_Windows_boot_loader)
            *   [2.1.2.1 Windows 7/8 boot loader](#Windows_7.2F8_boot_loader)
            *   [2.1.2.2 Windows 2000/XP boot loader](#Windows_2000.2FXP_boot_loader)
    *   [2.2 UEFI Systems](#UEFI_Systems)
*   [3 时间标准](#.E6.97.B6.E9.97.B4.E6.A0.87.E5.87.86)
*   [4 See also](#See_also)

## Potential Data Loss

### Renaming Files on NTFS partitions

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

These are limitations of Windows and not NTFS: any other OS using the NTFS partition will be fine. Windows will fail to detect these files and running `chkdsk` will most likely cause them to be deleted.

### Fast Start-Up

Fast Start-Up is a feature in Windows 8 that hibernates the computer rather than actually shutting it down to speed up boot times. Your system can lose data if Windows hibernates and you dual boot into another OS and make changes to files. Even if you don't intend to share filesystems, the EFI System Partition is likely to be damaged on an EFI system. Therefore, you should disable Fast Startup, as described [here](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html), before you install Linux on any computer that uses Windows 8.

[NTFS-3G added a safe-guard](http://sourceforge.net/p/ntfs-3g/ntfs-3g/ci/559270a8f67c77a7ce51246c23d2b2837bcff0c9/) to prevent read-write mounting of hibernated disks, but the NTFS driver within the Linux kernel has no such safeguard.

## Installation

The recommended way to setup a Linux/Windows dual booting system is to first install Windows, only using part of the disk for its partitions. When you have finished the Windows setup, boot into the Linux install environment where you can create additional partitions for Linux while leaving the existing Windows partitions untouched.

Some newer computers come pre-installed with Windows 8 which will be using Secure Boot. Arch Linux currently does not support Secure Boot, but some Windows 8 installations have been seen not to boot if Secure Boot is turned off in the BIOS. In some cases it is necessary to turn off both Secure Boot as well as Fastboot in the BIOS options in order to allow Windows 8 to boot without Secure Boot. However there are potential security risks in turning off Secure Boot for booting up Windows 8\. Therefore, it may be a better option to keep the Windows 8 install intact and have an independent hard drive for the Linux install - which can then be partitioned from scratch using a GPT partition table. Once that is done, creating several ext4/FAT32/swap partitions on the second drive may be a better way forward if the computer has two drives available. This is often not easy or possible on a small laptop. Currently, Secure Boot is still not in a fully stable state for reliable operation, even for Linux distributions that support it.

### BIOS Systems

#### Using a Linux boot loader

You may use [GRUB](/index.php/GRUB#Dual-booting "GRUB") or [Syslinux](/index.php/Syslinux#Chainloading "Syslinux").

#### Using Windows boot loader

With this setup the Windows bootloader loads GRUB which then boots Arch.

##### Windows 7/8 boot loader

The following section contains excerpts from [http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/](http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/).

The remainder of the setup is similar to a typical installation. Some documents state that the partition being loaded by the Windows boot loader must be a primary partition but I have used this without problem on an extended partition.

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

*   Boot to Windows and open up and you should be able to see the FAT32 partition. Copy the linux.bin file to `C:\`. Now run **cmd** with administrator privileges (navigate to *Start > All Programs > Accessories*, right-click on *Command Prompt* and select *Run as administrator*):

```
bcdedit /create /d “Linux” /application BOOTSECTOR

```

*   BCDEdit will return an alphanumeric identifier for this entry that I will refer to as {ID} in the remaining steps. You’ll need to replace {ID} by the actual returned identifier. An example of {ID} is {d7294d4e-9837-11de-99ac-f3f3a79e3e93}.

```
bcdedit /set {ID} device partition=c:
bcdedit /set {ID}  path \linux.bin
bcdedit /displayorder {ID} /addlast
bcdedit /timeout 30

```

Reboot and enjoy. In my case I'm using the Windows boot loader so that I can map my Dell Precision M4500's second power button to boot Linux instead of Windows.

##### Windows 2000/XP boot loader

For information on this method see [http://www.geocities.com/epark/linux/grub-w2k-HOWTO.html](http://www.geocities.com/epark/linux/grub-w2k-HOWTO.html). I do not believe there are any distinct advantages of this method over the Linux boot loader; you will still need a `/boot` partition, and this one is arguably more difficult to set up.

### UEFI Systems

Both [Gummiboot](/index.php/Gummiboot "Gummiboot") and [rEFInd](/index.php/REFInd "REFInd") autodetect **Windows Boot Manager** `\EFI\Microsoft\Boot\bootmgfw.efi` and show it in their boot menu, so there is no manual config required.

For [GRUB](/index.php/GRUB "GRUB")(2) follow [GRUB#Windows installed in UEFI-GPT Mode menu entry](/index.php/GRUB#Windows_installed_in_UEFI-GPT_Mode_menu_entry "GRUB").

Syslinux (as of version 6.01) and ELILO do not support chainloading other EFI applications, so they cannot be used to chainload `\EFI\Microsoft\Boot\bootmgfw.efi` .

Computers that come with newer versions of Windows often have [secure boot](/index.php/UEFI#Secure_Boot "UEFI") enabled. You will need to take extra steps to either disable secure boot or to make your installation media compatible with secure boot.

## 时间标准

*   建议：将 Arch Linux 和 Windows 皆设置为UTC。需要[修改Windows注册表](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Windows_.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8_UTC "Time (简体中文)")。另：记得关闭Windows的在线时间校准以防硬件时间被设为*localtime*。若需同步网络时间(NTP sync)，请在Arch Linux上安装[ntpd](/index.php/Ntpd "Ntpd")。

*   不建议：将Arch Linux的硬件时钟模式设为*localtime*并禁用任何时钟同步服务（如`ntpd.service`）。这将会使Windows检查硬件时间的正确性，并且你需要在一年中至少启动Windows两次(分别在春季与秋季)以正确应用[夏令时](https://en.wikipedia.org/wiki/Daylight_savings_time "wikipedia:Daylight savings time")。So please **don't** ask on the forums why the clock is one hour behind or ahead if you usually go for days or weeks without booting into Windows（所以请不要忘记启动Windows而在论坛问为什麼时钟会快/慢一个小时）。}}

## See also

*   [Booting Windows from a desktop shortcut](https://bbs.archlinux.org/viewtopic.php?id=140049)