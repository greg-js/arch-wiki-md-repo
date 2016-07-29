Apple uses a [Wikipedia:RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID") alternative called CoreStorage to merge the SSD and HDD into a single logical volume (sold as Fusion). We need to remove this volume, so we can reinstall OS X to the HDD without using the SSD.

## Contents

*   [1 Boot into recovery](#Boot_into_recovery)
*   [2 Destroy CoreStorage and prepare new volumes](#Destroy_CoreStorage_and_prepare_new_volumes)
*   [3 Install OS X on the HDD](#Install_OS_X_on_the_HDD)
*   [4 Proceed installing Arch Linux](#Proceed_installing_Arch_Linux)
*   [5 See also](#See_also)

## Boot into recovery

The iMacs that come with Fusion also come with a rescue partition that runs itself from RAM (a virtual disk2). This will allow you to play with the HDD and SDD without problems caused by mounted disks. Power on your iMac, holding down Command+R to enter the recovery environment.

When the recovery has started, start a terminal (in the Utilities menu).

## Destroy CoreStorage and prepare new volumes

Find the CoreStorage 'Logical volume group' ID, and take note of the SSD and larger disk (disk0 & 1)

```
diskutil cs list

```

Remove the CoreStorage volume

```
diskutil cs delete <VOLUMEID>

```

Sometimes you need to unmount a volume or try the above command twice for OS X to actually run it successfuly.

Zero the SSD (if you specify the correct disk this takes around 5 minutes) This will remove everything, including the partition table, so OS X doesn't see the disk and won't try to use it during installation.

```
diskutil zeroDisk disk1

```

Erase the HDD (this is faster then zeroDisk plus it creates a new HFS+ volume for OSx)

```
diskutil eraseDisk JHFS+ Macintosh disk0

```

## Install OS X on the HDD

Quit the terminal and start the OS X installer. **Do not use the GUI-based Disk Utility at this point**, it will show your disks as errored (red) and will want to fix them for you. This will actually screw things up as it will recreate the CoreStorage volume (even if you choose not to 'fix' anything). The OS X installer should show you 1 disk; which is the created Journaled HFS+ volume on the HDD.

Proceed by installing a fresh OS X version on the HDD. You can play around in OS X, for example use the **Disk Utility** to resize the OS X partition so you can allocate some space for Linux to use besides the SSD. Now boot the Arch Linux USB stick by holding the Option key while booting your iMac (you might need to use an Apple keyboard for this to work). This will show you a boot menu where you can select the USB drive for booting.

## Proceed installing Arch Linux

Installing Arch Linux requires no special tricks; follow the [Installation guide](/index.php/Installation_guide "Installation guide"); mount /dev/sda1 (the first partition of the HDD is the [UEFI](/index.php/UEFI "UEFI") partition) on /boot/efi; install grub-efi-x86_64 and you should be good to go! Since you will be installing on the [Solid State Drive](/index.php/Solid_State_Drives "Solid State Drives"), use parted and created aligned partitions. I use this scheme:

```
Model: ATA APPLE SSD SM128E (scsi)
Disk /dev/sdb: 121332826112B
Sector size (logical/physical): 512B/4096B
Partition Table: gpt
Disk Flags: 

Number  Start         End            Size           File system     Name  Flags
1      1048576B      16383999999B   16382951424B   linux-swap(v1)
2      16384000000B  121331777535B  104947777536B  ext4

```

Also, to use the internal network card you will need at least kernel 3.9! I use a Thunderbolt cable (which works in kernel 3.7+) to download the latest 3.9-rc

When rebooting, hold Option to show the internal bootloader so you can select your new install. To change the default boot option to Arch Linux, you need to 'bless' the earlier created UEFI file. It is best to rename the created 'EFI/arch_grub/grubx64_standalone.efi' to 'EFI/BOOT/BOOTX64.EFI', then run the following command from Mac OS X, after mounting the EFI partition:

```
sudo bless --device=/dev/disk1s2 --file=/Volumes/EFI/efi/BOOT/BOOTX64.EFI --setBoot

```

Make sure you specify a partition on the SSD as '--device'! Otherwise OS X will boot EFI from the partition, but GRUB will not find the SSD (where the actual install is) and you'll end up in rescue mode.

## See also

*   [IMac Aluminium](/index.php/IMac_Aluminium "IMac Aluminium")
*   [http://blog.fosketts.net/2011/08/05/undocumented-corestorage-commands/](http://blog.fosketts.net/2011/08/05/undocumented-corestorage-commands/)
*   [http://arstechnica.com/apple/2012/11/achieving-fusion-with-a-service-training-doc-ars-tears-open-apples-fusion-drive/2/](http://arstechnica.com/apple/2012/11/achieving-fusion-with-a-service-training-doc-ars-tears-open-apples-fusion-drive/2/)