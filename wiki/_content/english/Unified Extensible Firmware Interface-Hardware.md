This is a subpage of the main article [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"). It provides information about the hardware compatibility with [UEFI](/index.php/UEFI "UEFI") under Arch Linux.

## Contents

*   [1 Required info](#Required_info)
*   [2 Lenovo ThinkPad t420s](#Lenovo_ThinkPad_t420s)
*   [3 Lenovo ThinkPad x121e](#Lenovo_ThinkPad_x121e)
    *   [3.1 Additional notes](#Additional_notes)
*   [4 Lenovo ThinkCenter M92z](#Lenovo_ThinkCenter_M92z)
*   [5 Intel DZ77GA-70K](#Intel_DZ77GA-70K)
    *   [5.1 Additional notes](#Additional_notes_2)
*   [6 Asus M5A99X EVO](#Asus_M5A99X_EVO)
*   [7 HP EliteBook 840 G1](#HP_EliteBook_840_G1)
*   [8 Lenovo Thinkpad Edge E430 3254-DAQ](#Lenovo_Thinkpad_Edge_E430_3254-DAQ)
    *   [8.1 System Info](#System_Info)
    *   [8.2 Observations](#Observations)
    *   [8.3 Important Info](#Important_Info)
        *   [8.3.1 From WonderWoofy](#From_WonderWoofy)
*   [9 System76 Galago UltraPro / TUXEDO Book BU1402](#System76_Galago_UltraPro_.2F_TUXEDO_Book_BU1402)
    *   [9.1 System Info](#System_Info_2)
    *   [9.2 Fix](#Fix)
*   [10 Intel Atom System-on-Chip](#Intel_Atom_System-on-Chip)
    *   [10.1 MinnowBoard](#MinnowBoard)
    *   [10.2 Intel Atom SoC Clover Trail](#Intel_Atom_SoC_Clover_Trail)
    *   [10.3 Intel Atom SoC Bay Trail](#Intel_Atom_SoC_Bay_Trail)

## Required info

1.  System OEM/Vendor (like Dell, HP, Lenovo etc.) and Model (like ThinkPad x121e etc.) - all info needed
2.  Processor with the model number (full info like Intel Core i7 xxxx 1.8 GHz - for eg.)
3.  Chipset info (Intel P67 or H67 etc.)
4.  Motherboard with full model number - required if desktop, optional for laptop
5.  BIOS/UEFI vendor - AMI Aptio, Phoenix SecureCore Tiano, Insyde H2O etc. (very important) with updated month/year (will be shown as copyright year in some firmwares)
6.  Were you able to create a working entry in UEFI Boot menu using efibootmgr? Any specific issues like black screen or something like [http://forum-en.msi.com/index.php?topic=153411.0](http://forum-en.msi.com/index.php?topic=153411.0) ?
7.  If you were able to launch the UEFI Shell in ways other than using `(USB)/efi/boot/bootx64.efi` or Archboot, how?
8.  Output of UEFI Shell "ver" command.
9.  If efibootmgr did not work for you and you were able to launch UEFI Shell, did you use bcfg command to create UEFI Boot Menu entry? Did bcfg created boot entry work for you?
10.  Filesystem of UEFI System Partition? FAT32 or FAT16? (Mostly it should be FAT32 but some firmwares have problems with it, which is a violation of UEFI Spec.)
11.  Any graphics/video card issues that occur in UEFI boot alone and not in BIOS boot? Like Nvidia closed-source driver's lack of Kernel Mode Setting etc.

**Note:** In any user discussion in irc , forum or mailing lists etc. regarding UEFI, add your system info here and link to this page in the discussion to help solve the issue(s) quickly.

Original Post: [https://bbs.archlinux.org/viewtopic.php?id=133074](https://bbs.archlinux.org/viewtopic.php?id=133074).

* * *

## Lenovo ThinkPad t420s

*   intel core i7 2640M 2.80GHz
*   Phoenix SecureCore Tiano, 2011
*   UEFI bios version 8CET51WW (1.31), dated 2011-11-29
*   efibootmgr can create entries in menu just fine. looks good.
*   FAT32

## Lenovo ThinkPad x121e

1.  Model: Lenovo ThinkPad x121e 3045CTO
2.  Processor: Intel(R) Core(TM) i3-2367M CPU @ 1.40GHz GenuineIntel
3.  BIOS/UEFI vendor: Phoenix SecureCore Tiano
4.  Could create a working entry in UEFI Boot menu using efibootmgr.
5.  Have not managed to launch UEFI shell.
6.  Filesystem of UEFI System Partition : FAT16 OR FAT32 with a sufficiently large ESP. FAT32 does *NOT* work with a smaller partition size. More info at [https://bbs.archlinux.org/viewtopic.php?id=131149](https://bbs.archlinux.org/viewtopic.php?id=131149).
7.  Stub loader does not work either directly or with a boot loader such as refind. EFI boot requires a boot manager such as grub.

### Additional notes

*   Works fine with MBR partition map in BIOS mode.
*   Also works fine with GPT partition map in UEFI mode but ONLY if the EFI partition is formatted as fat 16 OR the partition is large enough to officially support fat 32.
*   Cannot get it to boot from a GPT disk in BIOS mode.
*   I did not try archboot.

## Lenovo ThinkCenter M92z

1.  Intel(R) Pentium(R) CPU G2020 @ 2.90GHz
2.  Motherboard: Lenovo MAHOBAY
3.  Bios Version: American Megatrends, flashed with 9NKT60AUS Lenovo Bios Update, Release Date: 1/16/2014
4.  Use of efibootmgr: see just below
5.  UEFI V.2.3.1
6.  I did not try to create entries with bcfg
7.  Filesystem of UEFI System Partition? FAT32.

Notes: The main problem of this computer is that the entries created by efibootmgr sometimes disappear after the next reboot. Example after the reboot:

```
Boot0000* rEFInd Boot Manager	Vendor(99e275e7-75a0-4b37-a2e6-c5385e6c00cb,)
Boot0001* debian	HD(1,800,f3800,b500458e-3e0e-4299-bc41-48424508bced)File(\EFI\debian\grubx64.efi)

```

In this case after I installed the debian entry, a part of the entry for **rEFInd** disappeared. A step by step boot configuration with refind is available here: [https://gist.github.com/EmmanuelKasper/9590327](https://gist.github.com/EmmanuelKasper/9590327)

## Intel DZ77GA-70K

1.  System OEM/Vendor (like Dell, HP, Lenovo etc.) and Model (like ThinkPad x121e etc.) - all info needed
    *   Intel DZ77GA-70K
2.  Processor with the model number (full info like Intel Core i7 xxxx 1.8 GHz - for eg.)
    *   Intel Core i7 3770K
3.  Chipset info (Intel P67 or H67 etc.)
    *   Z77
4.  Motherboard with full model number - required if desktop, optional for laptop
    *   Intel DZ77GA-70K
5.  BIOS/UEFI vendor - AMI Aptio, Phoenix SecureCore Tiano, Insyde H2O etc. (very important) with updated month/year (will be shown as copyright year in some firmwares)
    *   (from hardinfo, under a bios boot)

```
 -BIOS-
  Date		: 07/13/2012
  Vendor		: Intel Corp. (www.intel.com)
  Version		: GAZ7711H.86A.0049.2012.0713.1518
 -Board-
  Name		: DZ77GA-70K
  Vendor		: Intel Corporation (www.intel.com)

```

1.  Were you able to create a working entry in UEFI Boot menu using efibootmgr? Any specific issues like black screen or something like [http://forum-en.msi.com/index.php?topic=153411.0](http://forum-en.msi.com/index.php?topic=153411.0) ?
    *   No. Linux cannot boot through uefi on this motherboard, with this bios revision.
2.  If you were able to launch the UEFI Shell in ways other than using `(USB)/efi/boot/bootx64.efi` or Archboot, how?
    *   No, however bootx64.efi works, archboot does not.
3.  Output of UEFI Shell "ver" command.

```
 UEFI Interactive Shell v2.0
 Copyright 2009-2011 Intel(r) Corporation. All rights reserved. Beta build 1.0
 UEFI v2.31 (American Megatrends, 0x0004028D)

```

1.  If efibootmgr did not work for you and you were able to launch UEFI Shell, did you use bcfg command to create UEFI Boot Menu entry? Did bcfg created boot entry work for you?
    *   booting through bcfg produced the same results as booting from the shell, didn't work.
2.  Filesystem of UEFI System Partition? FAT32 or FAT16? (Mostly it should be FAT32 but some firmwares have problems with it, which is a violation of UEFI Spec.)
    *   Both FAT32 and FAT16 do not work.
3.  Any graphics/video card issues that occur in UEFI boot alone and not in BIOS boot? Like Nvidia closed-source driver's lack of Kernel Mode Setting etc.
    *   Kernel hangs after attempting to boot, no graphics output after changing to the kernel. Graphics output before that is fine.

### Additional notes

More info at [archlinux forums](https://bbs.archlinux.org/viewtopic.php?id=146990) and [stack overflow](http://unix.stackexchange.com/questions/45312/how-can-i-tell-if-i-have-a-bug-with-my-kernel-or-with-my-bios-firmware). Similar problems with [a different motherboard](http://comments.gmane.org/gmane.linux.redhat.fedora.devel/167170). Seems to be a buggy uefi implementation by intel.

mihanson on **2013-07-21**: tried with latest BIOS, version 0066, and the results are the same as the above. No go in UEFI mode on the Intel DZ77GA-70K.

* * *

## Asus M5A99X EVO

1.  System OEM/Vendor
    *   Asus M5A99X EVO
2.  Processor with the model number
    *   AMD FX(tm)-8150 Eight-Core Processor
3.  Chipset info
    *   AMD 990X/SB950
4.  BIOS/UEFI vendor

```
  Vendor: American Megatrends Inc.
  Version: 0901
  Release Date: 12/02/2011

```

1.  Were you able to create a working entry in UEFI Boot menu using efibootmgr?
    *   Yes
2.  If you were able to launch the UEFI Shell in ways other than using `(USB)/efi/boot/bootx64.efi`
    *   Yes, option in the Exit menu of the UEFI BIOS "Launch UEFI from system partition"
3.  Output of UEFI Shell "ver" command.
    *   To be updated
4.  Filesystem of UEFI System Partition? FAT32 or FAT16?
    *   FAT32
5.  Any graphics/video card issues that occur in UEFI boot alone and not in BIOS boot? Like Nvidia closed-source driver's lack of Kernel Mode Setting etc.
    *   No

* * *

## HP EliteBook 840 G1

See [HP EliteBook 840 G1](/index.php/HP_EliteBook_840_G1 "HP EliteBook 840 G1") for details.

## Lenovo Thinkpad Edge E430 3254-DAQ

The below information was added by user [User:The.ridikulus.rat](/index.php/User:The.ridikulus.rat "User:The.ridikulus.rat") .

### System Info

1.  [Lenovo Thinkpad Edge E430](/index.php/Lenovo_ThinkPad_Edge_E430 "Lenovo ThinkPad Edge E430") 3254-DAQ (India)
2.  Intel Core i5 3210M 2.50 GHz (3rd Gen aka Ivy Bridge), 8 GB RAM
3.  Intel HM77 Express Chipset
4.  UEFI Firmware Vendor : Phoenix SecureCore Tiano
5.  UEFI/BIOS Version : 2.55
6.  Lenovo UEFI/BIOS Build Date : 27-FEB-2014
7.  External Ports: 3 USB 3.0, 1 USB 2.0, 1 VGA, 1 HDMI, 1 RJ45 Ethernet/LAN port (Realtek), 1 ExpressCard 34 port, 1 3.5mm Headphones jack
8.  1 Tray-Load CD/DVD Writer
9.  Switchable Graphics : Intel HD Graphics 4000 and Nvidia GeForce 610M (1GB Dedicated RAM)
10.  WiFi card : Intel Centrino Wireless-N 2230 (B/G/N + Bluetooth 4.0), no 802.11a and 802.11ac support

### Observations

1.  UEFI Secure Boot support is present in firmware, but I have currently disabled it. System came pre-installed with Windows 7 Pro x64 in BIOS-MBR mode, with BIOS version 1.14 (which did not include UEFI Secure Boot).
2.  Using a 1 GiB FAT32 UEFISYS partition (/dev/sda1) mounted at /boot/efi (i.e. separate from /boot). Kernel and initramfs files synced during update using [EFISTUB](/index.php/EFISTUB "EFISTUB").
3.  No issues with efibootmgr
4.  Currently using gummiboot (textonly mode) as main boot manager. No need for `/EFI/Microsoft/Boot/bootmgfw.efi` hack. Dual-booting Windows 8.1 Pro x64 UEFI-GPT. Windows boot files are stored in same EFISYS partition.
5.  Both UEFI Shell v2 and v1 work. No option in the firmware setup/menu to directly launch the shell.
6.  Currently using only intel and nouveau drivers. Haven't yet tried nvidia binary drivers or nvidia optimus graphics switching support. Kernel Mode Setting enabled.
7.  grub-bios works if the firmware is changed to boot "Legacy only" without any boot/active flag in 0xEE Protective MBR partition entry.
8.  Using only PARTUUID in /etc/fstab and in bootloader config files.

### Important Info

I didn't use Archiso or Archboot to install the system. I transferred the Arch installation from my old Sony Vaio laptop to my new Thinkpad E430 using an external USB HDD and rsync from within SystemRescueCD, after manually creating the partitions using GParted, and then manually setup fstab and rEFInd. After that I rebooted into Arch and installed grub-efi-x86_64 and grub-bios.

##### From WonderWoofy

On an E430-3254(CTO) I had the same issues as the.ridikulus.rat with efibootmgr and truncated kerl command line parameters. This usually lead to the inability of the kernel to find the initramfs. What I ended up doing is putting the kernel and intramfs in the root of the ESP, and from there the efibootmgr entries worked nicely. This does lead to an ESP that is not organized in the recommended way though.

Also, I did actually install via Archboot, and all worked fine. I have actually installed twice on this machine, once to a Momentus XT and once to a Samsung 830\. The first time I used a CD, and therefore selected the "UEFI First" preference in the bios. This supposedly will try UEFI (\EFI\boot\bootx64.efi) first, and if that fails it will look to the MBR. Unfortunately, it did not honor this setting for the optical drive, and I had to turn off legacy bios mode entirely to get it to boot in UEFI from the CD. Interestingly, this "UEFI First" setting works just fine for interal drives. USB flash drives are a whole different story though, and more information can be found [here](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface").

* * *

## System76 Galago UltraPro / TUXEDO Book BU1402

### System Info

*   System76 Galago UltraPro / TUXEDO Book BU1402 (Clevo W740SU)
*   intel core i7 4750HQ 2.0GHz
*   intel HM87 Chipset
*   Original firmware version unknown, but from American Megatrends Inc.
*   Boot in UEFI mode only possible by starting an UEFI shell via the BIOS setup (`$esp/shellx64.efi`)
*   UEFI menu entries could be created by using efibootmgr, but without them being shown in the bootup menu
*   ESP filesystem: FAT32
*   **Note:** UEFI boot is not officially supported by System76 or TUXEDO Computers. Currently TUXEDO Computers doesn't provide any BIOS updates. Create a backup if you want to be able to revert to original firmware.

### Fix

*   Download the Clevo W740SU firmware from [[1]](http://repo.palkeo.com/clevo-mirror/W740SU/).
*   Flash it using any FreeDOS live medium
*   The new firmware is from American Megatrends Inc. V.4.6.5 08/13/2013
*   The new firmware doesn't support mixed BIOS and UEFI support, so you have to manually switch if you want to boot from a medium that doesn't support UEFI.

* * *

## Intel Atom System-on-Chip

Intel Atom System-on-Chip (SoC) is the Intel's answer to ARM SoC, primarily targeting Smartphones and Tablets (not regular Desktop and Notebook PCs).

**Note:** This section was written based on information available online, not based on experience by an actual user of any Intel Atom SoC system.

**Note:** Intel Atom SoC systems that ship with Windows 8/8.1 32-bit provide 32-bit UEFI-only firmware with no BIOS compatibility option (no CSM). In UEFI terms these systems are called Class 3 systems (this term is not specific to 32-bit), ie. UEFI-only with no BIOS CSM. These Atom SoC systems are therefore called as 32-bit UEFI Class 3 systems, and these can be booted only using a 32-bit UEFI bootable USB, which is not provided by default in [Archiso](/index.php/Archiso "Archiso") (official install iso) and Archboot. These systems also come with UEFI Secure Boot enabled by default, but the firmware setup provides option(s) to disable Secure Boot as mandated by Microsoft for x86 systems.

**Related Links:**

*   [Wikipedia:Atom (system on chip)](https://en.wikipedia.org/wiki/Atom_(system_on_chip) "wikipedia:Atom (system on chip)")

### MinnowBoard

The MinnowBoard is an Intel Atom SoC based board similar to Raspberry Pi or BeagleBoard. It ships with [Tianocore UDK](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=Welcome) based 32-bit UEFI-only firmware which does not contain CSM support (no Legacy BIOS boot). The embedded Atom processor is supports only 32-bit, hence it is not possible to replace the 32-bit UEFI in the board with 64-bit (x86_64) UEFI. See below links for more info.

**Related Links:**

*   [http://www.minnowboard.org/](http://www.minnowboard.org/)
*   [http://www.elinux.org/MinnowBoard](http://www.elinux.org/MinnowBoard)
*   [http://uefidk.intel.com/content/minnowboard-uefi-firmware](http://uefidk.intel.com/content/minnowboard-uefi-firmware)

### Intel Atom SoC Clover Trail

Intel Atom SoC Clover Trail processors are 32-bit only, hence they contain only 32-bit UEFI firmware. Officially Intel has stated that Linux will not be supported in Clover Trail tablets. Apart from this, Intel has not released the Clover Trail power-management and (PowerVR based) graphics code for Linux. Hence these systems may not work reliably with Linux.

**Related Links:**

*   [http://download.lenovo.com/luc/dml/Tablet2_Imaging_considerations.pdf](http://download.lenovo.com/luc/dml/Tablet2_Imaging_considerations.pdf)
*   [http://arstechnica.com/information-technology/2012/09/intel-declares-clover-trail-atom-processor-a-no-linux-zone/](http://arstechnica.com/information-technology/2012/09/intel-declares-clover-trail-atom-processor-a-no-linux-zone/)

### Intel Atom SoC Bay Trail

Intel Atom SoC Bay Trail processors actually support 64-bit, but these tablets ship with only Windows 8/8.1 32-bit (not 64-bit) because of a feature called **Connected Standby** (also called **InstantGo**) which is mandated by Microsoft to be enabled, but currently supported only by Windows 8/8.1 32-bit version (not 64-bit, as of October 2013). **Connected Standby** requirements (by Microsoft) include tablets to support only UEFI boot (hence no BIOS CSM) and UEFI bitness to match the OS bitness (hence 32-bit UEFI for sake of Win 8/8.1 32-bit). With only 32-bit UEFI and lack of BIOS compatibility, even Windows XP/Vista/7 32-bit (no UEFI support) and 64-bit (cannot boot in 32-bit UEFI) cannot be installed in these systems. These systems are truly locked to Windows 8/8.1 32-bit (UEFI mode).

In these systems it should (theoretically) be possible to install 64-bit Linux provided the kernel is instructed to not access EFI runtime code using the **noefi** kernel parameter, due to the kernel/UEFI bitness mismatch. Unlike Clover Trail, Intel has stated that Bay Trail will support Android (which is based on Linux), and its graphics is based on Intel HD graphics (not PowerVR). Therefore, Bay Trail systems may work better with Linux compared to Clover Trail.

**Related Links:**

*   [Wikipedia:Connected Standby](https://en.wikipedia.org/wiki/Connected_Standby "wikipedia:Connected Standby")
*   [http://www.pcworld.com/article/2048599/windows-81-tablets-with-64bit-atom-chips-not-coming-until-q1.html](http://www.pcworld.com/article/2048599/windows-81-tablets-with-64bit-atom-chips-not-coming-until-q1.html)
*   [AnandTech: Windows 8.1 x64 Connected Standby Support](http://www.anandtech.com/show/8038/windows-81-x64-connected-standby-support)