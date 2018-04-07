[GRUB2](http://www.gnu.org/software/grub/) generasi berikutnya dari GRUB. GRUB2 adalah derivasi dari [PUPA](http://www.nongnu.org/pupa/) yang merupakan proyek pengembangand dari GRUB. GRUB 2 telah di tulis ulang untuk membersihkan segalanya dan memberikan modularitas dan portabilitas. [[1]](http://www.gnu.org/software/grub/grub-faq.en.html#q1).

Secara singkat, *bootloader* adalah program software pertama yang berjalan ketika komputer pertama dinyalakan. *Bootloader* bertanggung jawab sebagai pemicu dan pengirim kontrol ke Kernel Linux. Kernel, selanjutnya, menginisialisasi seluruh sistem operasi.

**Note:** grub2 dari 1.99 dan selanjutnya telah mendukung btrfs sebagai root (tanpa /boot filesistem yang terpisah), tetapi tingkat kompresinya terbatas pada zlib, tidak LZO. Dukungan kompresi LZO hanya terdapat pada repo bzr upstream.

## Contents

*   [1 Prefasi](#Prefasi)
    *   [1.1 Catatan untuk pengguna GRUB Legacy](#Catatan_untuk_pengguna_GRUB_Legacy)
    *   [1.2 Kebutuhan GRUB2](#Kebutuhan_GRUB2)
        *   [1.2.1 System BIOS](#System_BIOS)
            *   [1.2.1.1 Instruksi spesifik untuk GPT](#Instruksi_spesifik_untuk_GPT)
            *   [1.2.1.2 Instruksi spesifik MBR dikenal sebagai pemartisian msdos](#Instruksi_spesifik_MBR_dikenal_sebagai_pemartisian_msdos)
        *   [1.2.2 UEFI systems](#UEFI_systems)
            *   [1.2.2.1 Membuat dan the UEFI SYSTEM PARTITION](#Membuat_dan_the_UEFI_SYSTEM_PARTITION)
*   [2 Installation](#Installation)
    *   [2.1 During Arch Linux installation](#During_Arch_Linux_installation)
    *   [2.2 From a running Arch Linux](#From_a_running_Arch_Linux)
        *   [2.2.1 BIOS systems](#BIOS_systems)
            *   [2.2.1.1 Backup Important Data](#Backup_Important_Data)
            *   [2.2.1.2 Install grub2-bios package](#Install_grub2-bios_package)
            *   [2.2.1.3 Install grub2-bios boot files](#Install_grub2-bios_boot_files)
                *   [2.2.1.3.1 Install to 440-byte MBR boot code region](#Install_to_440-byte_MBR_boot_code_region)
                *   [2.2.1.3.2 Install to Partition or Partitionless Disk](#Install_to_Partition_or_Partitionless_Disk)
                *   [2.2.1.3.3 Generate core.img alone](#Generate_core.img_alone)
            *   [2.2.1.4 Generate GRUB2 BIOS Config file](#Generate_GRUB2_BIOS_Config_file)
            *   [2.2.1.5 Multiboot in BIOS](#Multiboot_in_BIOS)
                *   [2.2.1.5.1 Boot Microsoft Windows installed in BIOS-MBR mode](#Boot_Microsoft_Windows_installed_in_BIOS-MBR_mode)
        *   [2.2.2 UEFI systems](#UEFI_systems_2)
            *   [2.2.2.1 Install grub2-uefi package](#Install_grub2-uefi_package)
            *   [2.2.2.2 Install grub2-uefi boot files](#Install_grub2-uefi_boot_files)
                *   [2.2.2.2.1 Install to UEFI SYSTEM PARTITION](#Install_to_UEFI_SYSTEM_PARTITION)
            *   [2.2.2.3 Create GRUB2 entry in the Firmware Boot Manager](#Create_GRUB2_entry_in_the_Firmware_Boot_Manager)
                *   [2.2.2.3.1 Non-Mac UEFI systems](#Non-Mac_UEFI_systems)
                *   [2.2.2.3.2 Apple Mac EFI systems](#Apple_Mac_EFI_systems)
            *   [2.2.2.4 Generate GRUB2 UEFI Config file](#Generate_GRUB2_UEFI_Config_file)
            *   [2.2.2.5 Create GRUB2 Standalone UEFI Application](#Create_GRUB2_Standalone_UEFI_Application)
            *   [2.2.2.6 Multiboot in UEFI](#Multiboot_in_UEFI)
                *   [2.2.2.6.1 Chainload Microsoft Windows x86_64 UEFI-GPT](#Chainload_Microsoft_Windows_x86_64_UEFI-GPT)
*   [3 Configuration](#Configuration)
    *   [3.1 Automatically generating using grub-mkconfig (Recommended)](#Automatically_generating_using_grub-mkconfig_.28Recommended.29)
    *   [3.2 Manually creating grub.cfg](#Manually_creating_grub.cfg)
    *   [3.3 Dual-booting](#Dual-booting)
        *   [3.3.1 Using grub-mkconfig](#Using_grub-mkconfig)
            *   [3.3.1.1 With GNU/Linux](#With_GNU.2FLinux)
            *   [3.3.1.2 With FreeBSD](#With_FreeBSD)
            *   [3.3.1.3 With Windows](#With_Windows)
        *   [3.3.2 With Windows via EasyBCD and NeoGRUB](#With_Windows_via_EasyBCD_and_NeoGRUB)
    *   [3.4 Visual Configuration](#Visual_Configuration)
        *   [3.4.1 Setting the framebuffer resolution](#Setting_the_framebuffer_resolution)
        *   [3.4.2 915resolution hack](#915resolution_hack)
        *   [3.4.3 Background image and bitmap fonts](#Background_image_and_bitmap_fonts)
        *   [3.4.4 Menu colors](#Menu_colors)
        *   [3.4.5 Hidden menu](#Hidden_menu)
    *   [3.5 Other Options](#Other_Options)
        *   [3.5.1 LVM](#LVM)
        *   [3.5.2 Raid](#Raid)
        *   [3.5.3 Persistent block device naming](#Persistent_block_device_naming)
        *   [3.5.4 Using Labels](#Using_Labels)
        *   [3.5.5 Recall previous entry](#Recall_previous_entry)
        *   [3.5.6 Security](#Security)
        *   [3.5.7 Root Encryption](#Root_Encryption)
    *   [3.6 Booting an ISO Directly From Grub2](#Booting_an_ISO_Directly_From_Grub2)
        *   [3.6.1 Arch ISO](#Arch_ISO)
        *   [3.6.2 Ubuntu ISO](#Ubuntu_ISO)
*   [4 Using the command shell](#Using_the_command_shell)
    *   [4.1 Pager support](#Pager_support)
*   [5 GUI configuration tools](#GUI_configuration_tools)
*   [6 parttool or legacy hide/unhide](#parttool_or_legacy_hide.2Funhide)
*   [7 Using the rescue console](#Using_the_rescue_console)
*   [8 Combining the use of UUID's and basic scripting](#Combining_the_use_of_UUID.27s_and_basic_scripting)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Enable GRUB2 debug messages](#Enable_GRUB2_debug_messages)
    *   [9.2 Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error)
    *   [9.3 msdos-style error message](#msdos-style_error_message)
    *   [9.4 UEFI GRUB2 drops to shell](#UEFI_GRUB2_drops_to_shell)
    *   [9.5 UEFI GRUB2 not loaded](#UEFI_GRUB2_not_loaded)
    *   [9.6 Invalid signature](#Invalid_signature)
*   [10 References](#References)
*   [11 External Links](#External_Links)

## Prefasi

Walaupun, [GRUB](/index.php/GRUB "GRUB") (versi 0.9x) adalah bootloader standar Arch Linux, GRUB dapat diganti menjadi 'grub legacy' by upstream. Dimana telah menjadi GRUB2 dan [Syslinux](/index.php/Syslinux "Syslinux") di beberapa distribusi. Versi lanjutan merekomendasikan GRUB2 >=1.99 di atas versi grub-legacy.

### Catatan untuk pengguna GRUB Legacy

*   Ada perbedaan perinta dari GRUB dan GRUB2\. Perlu di lihat terlebih dahulu [GRUB2 commands](http://www.gnu.org/software/grub/manual/grub.html#Commands) sebelum melanjutkan (contoh : "find" telah di ganti dengan "search").

*   GRUB2 sekarang *modular* dan tidak lagi memerlukan "stage 1.5". Sebagai hasilnya, bootloader itu sendiri menjadi terbatas -- modul-modul diambil dari hard disk sebagai kebutuhan untuk meluaskan fungsionalitas. (contoh : dukungan untuk [LVM](/index.php/LVM "LVM") atau RAID).

*   Penamaan perangkat telah berubah antara GRUB dan GRUB2\. Partisi diurut dari nomor 1 dari pada 0 ketika disk masih bernomor 0\. Sebagai contoh, `/dev/sda1` akan menjadi `(hd0,msdos1)` (untuk MBR) atau `(hd0,gpt1)` (for GPT) ketika GRUB2 dipakai.

### Kebutuhan GRUB2

#### System BIOS

##### Instruksi spesifik untuk [GPT](/index.php/GPT "GPT")

GRUB2 di konfigurasi BIOS-GPT membutuhkan sebuah Partisi BIOS Boot yang terembed pada core.img di kehilangannya post-MBR di sistem yang terpartisi secara GPT (yang menyebabkan MBR diambil alih oleh GPT Primary Header dan Primary Partition table). Partisi ini digunakan oleh GRUB2 hanya pada pengaturan BIOS-GPT. Tidak ada partisi jenis ini dalam kasus partisi MBR (setidaknya tidak untuk GRUB2). Partisi ini juga tidak diperlukan jika sistem berbasiskan UEFI, kerana tidak ada bootsectors yang mengambil tempat dalam kasus ini. Syslinux tidak memerlukan partisi ini.

Untuk konfigurasi BIOS-GPT, buat sebuah partisi sebesar 2 MiB menggunaka cgdisk atau GNU Parted tanpa jenis filesistem. Lokasi partisi ini tidak menjadi masalah tetapi partisi ini haruslah berada diantara yang pertama dari area 2 TiB. Sangat disarankan untuk menempatkannya di awal disk sebelum partisi /boot. Atur jenis partisi menjadi "EF02" di cgdisk atau `set <BOOT_PART_NUM> bios_grub on` di GNU Parted.

**Note:** Partisi ini harus di buat sebelum grub_bios-install atau grub-setup dijalankan atau sebelum langka **Install Bootloader** dari penginstallan Archlinux (jika GRUB2 BIOS terpilih sebagai bootloader).

##### Instruksi spesifik [MBR](/index.php/MBR "MBR") dikenal sebagai pemartisian msdos

Biasa post-MBR (setelah 512 byte area MBR dan sebelum dimulainya partisi pertama) di banyak sistem pemartisian MBR (atau msdos disklabel) adalah 32 KiB ketika kompabilitas DOS telah terpenuhi. Akan tetapi sebuah post-MBR sejumlah 1 atau 2 MiB direkomendasikan untuk memberikan ruang yang cukup untuk core.img yang terembed ([FS#24103](https://bugs.archlinux.org/task/24103) ). Disarankan untuk menggunakan pemartisi yang mendukung alokasi partisi 1 MiB untuk mendapat ruang dalam memenuhi sektor non-512 byte. (yang tidak berelasi untuk embed core.img).

Jika anda tidak melakukan dual-boot dengan MS Windows (semua versi) di sistem BIOS, disarankan untuk menggunakan partisi GPT - [GUID Partition Table#Convert_from_MBR_to_GPT_without_data_loss](/index.php/GUID_Partition_Table#Convert_from_MBR_to_GPT_without_data_loss "GUID Partition Table")

**Catatan:** Membuat partisi 2MiB telah disebut diatas SEBELUM anda mengkonversi ke GPT. Jika tidak, gparted tidak akan merubah ukuran partisi boot untuk mengizinkan pembuatannya dan ketika anda reboot grub2 tidak tahu dimana untuk memulai.

#### UEFI systems

##### Membuat dan the UEFI SYSTEM PARTITION

Ikuti instruksi [Unified Extensible Firmware Interface#Create_an_UEFI_SYSTEM_PARTITION_in_Linux](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_SYSTEM_PARTITION_in_Linux "Unified Extensible Firmware Interface") dalam membuat sebuah UEFI SYSTEM PARTITION. Lalu mount UEFI SYSTEM PARTITION di `/boot/efi`. harus mempunya format FAT32 dan lebih besar dari >=200 MiB ukurannya. jika kamu telah mount partisi UEFISYS di mountpoint yang lain, ganti `/boot/efi` dengan command di bawah ini:

```
# mkdir -p /boot/efi
# mount -t vfat <UEFISYS_PART_DEVICE> /boot/efi

```

Buat direktori <UEFI_SYSTEM_PARTITION>/efi jika tidak ada:

```
# mkdir -p /boot/efi/efi

```

## Installation

### During Arch Linux installation

*   lEwati langkah **Install Bootloader** dan keluar dari penginstall.
*   Mengatur jaringan:

```
# aif -p partial-configure-network

```

Command ini memunculkan dialog; masukkan jenis perangkat yang digunakan, (contoh : eth0) dan gunakan DHCP untuk pengaturan yang lebih mudah.

*   Jika anda tidak mengkonfigurasi sistem `/etc/resolv.conf` dalam instalasi (anda merencanakan membiarkan DHCP mengatur otomatis), anda perlu mengkopi konfigurasi yang di buat oleh AIF ketika jaringan di konfigurasi otomatis:

```
# cp /etc/resolv.conf /mnt/etc/resolv.conf

```

*   Jika anda mengalami kegagalan jaringan saat update paket pacman, anda mungkin harus menginstall paket net-tools.
*   Cek dan liat apa modul dm_mod digunakan. Jika tidak load secara manual. (anda mungkin butuh grub2-bios; pasang jika diperlukan):

```
# lsmod | grep dm_mod
# modprobe dm-mod

```

**Note:** This is necessary at this point, and cannot be postponed after the chroot. If you try to use modprobe in a chroot environment that has a later kernel version from that of the installing device (at the time of writing, 2.6.33), modprobe will fail. This happens routinely using the Arch "net" installations.

*   From the installer's live shell, chroot to the installed system:

```
# mount -o bind /dev /mnt/dev
# mount -t proc /proc /mnt/proc/
# mount -t sysfs /sys /mnt/sys/
# chroot /mnt bash

```

*   Update database pacman :

```
# pacman-db-upgrade

```

*   Refresh daftar paket (dengan tambahan -y):

```
# pacman -Syy

```

*   Pasang paket GRUB2 sperti telah disebutkan di bagian [#From a running Arch Linux](#From_a_running_Arch_Linux). dm-mod module sudah di load tidak perlu di load lagi.

### From a running Arch Linux

#### BIOS systems

##### Backup Important Data

In general, a grub installation should run smoothly. Sometimes it could mess up your system. You're strongly advised to make a backup before installing grub2-bios.

*   copy grub modules and configuration

```
# cp -a /boot/grub /path/to/backup/

```

*   backup the MBR and GRUB-Legacy stage 1.5

```
# dd if=/dev/sdX of=/path/to/backup/first-sectors bs=512 count=63

```

Replace /dev/sdaX with you disk path (mostly /dev/sda).

**Note:** This command backs up the partition table too. Be careful while restoring if you've changed your partition setup in the meantime

To backup only the MBR boot code use:

```
# dd if=/dev/sdX of=/path/to/backup/mbr-boot-code bs=440 count=1

```

You could now lightly remove `/boot/grub` with:

```
# rm -rf /boot/grub

```

and follow the instructions below. You know that if things get nasty, you could reboot your system thanks to an installation media and:

*   move old grub-legacy or grub2 files out of the way

```
# mv /boot/grub /boot/grub.nonfunctional

```

*   copy grub back to /boot

```
# cp -a /path/to/backup/grub /boot/

```

*   replace MBR and next 62 sectors of sda with backed up copy (DANGEROUS!)

```
# dd if=/path/to/backup/first-sectors of=/dev/sdX bs=512 count=63

```

**Note:** This command also restores the partition table. Be careful.

To restore only the MBR boot code use:

```
# dd if=/path/to/backup/mbr-boot-code of=/dev/sdX bs=440 count=1

```

##### Install grub2-bios package

The GRUB2 package can be installed with pacman (and will replace [grub](https://www.archlinux.org/packages/?name=grub), if it is installed). Simply installing the package won't update the `/boot/grub/core.img` file and the grub2 modules in `/boot/grub`. You need to update them manually using grub_bios-install as explained below.

```
# pacman -S grub2-bios

```

**Note:** Installing grub2-common (a dependency of grub2-bios) 1.99~rc1 or later, may take forever in some systems since the post_install script runs grub-mkconfig and this script does not provide the option `--no-floppy`. For more details search this option in the article.

Also load the device-mapper kernel module without which grub-probe does not reliably detect disks and partitions:

```
# modprobe dm-mod

```

##### Install grub2-bios boot files

There are 3 ways to install grub2 boot files in BIOS booting：

*   [#Install to 440-byte MBR boot code region](#Install_to_440-byte_MBR_boot_code_region) (recommended) ,
*   [#Install to Partition or Partitionless Disk](#Install_to_Partition_or_Partitionless_Disk) (not recommended),
*   [#Generate core.img alone](#Generate_core.img_alone) (safest method, but requires another BIOS bootloader like [grub-legacy](/index.php/Grub-legacy "Grub-legacy") or [syslinux](/index.php/Syslinux "Syslinux") to be installed to chainload `/boot/grub/core.img` ).

###### Install to 440-byte MBR boot code region

To setup grub2-bios in the 440-byte Master Boot Record boot code region, populate the `/boot/grub` directory, generate the `/boot/grub/core.img` file, and embed it in the 32 KiB (minimum size - varies depending on partition alignment) post-MBR gap (MBR disks) or in BIOS Boot Partition (GPT disks), run:

```
# grub_bios-install --boot-directory=/boot --no-floppy --recheck --debug /dev/sda

```

where `/dev/sda` is the destination of the installation (in this case the MBR of the first SATA disk). If you use [LVM](/index.php/LVM "LVM") for your `/boot`, you can install GRUB2 on multiple physical disks.

The `--no-floppy` tells grub2-bios utilities not to search for any floppy devices which reduces the overall execution time of grub_bios-install on many systems (it will also prevent the issue below from occurring). Otherwise you get an error that looks like this:

```
grub-probe: error: Cannot get the real path of '/dev/fd0'
Auto-detection of a filesystem module failed.
Please specify the module with the option '--modules' explicitly.

```

**Warning:** Make sure that you check the `/boot` directory if you use the latter. Sometimes the `boot-directory` parameter creates another `/boot` folder inside of boot. A wrong install would look like this `/boot/boot/grub` !
.

###### Install to Partition or Partitionless Disk

**Note:** grub2-bios (any version - including upstream bzr repo) does not encourage installation to a partition boot sector or a partitionless disk like grub-legacy or syslinux does. Neither do the Arch devs.

To setup grub2-bios to a partition boot sector, to a partitionless disk (also called superfloppy) or to a floppy disk, run (using for example /dev/sda1 as the /boot partition)

```
# chattr -i /boot/grub/core.img
# grub_bios-install --boot-directory=/boot --no-floppy --recheck --force --debug /dev/sda1
# chattr +i /boot/grub/core.img

```

You need to use the `--force` option to allow usage of blocklists and should not use `--grub-setup=/bin/true` (which is similar to simply generating core.img).

grub_bios-install will give out warnings like which should give you the idea of what might go wrong with this approach.

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition.  This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible.  GRUB can only be installed in this setup by using blocklists.  
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

Without `--force` you may get the below error and grub-setup will not setup its boot code in the partition boot sector.

```
/sbin/grub-setup: error: will not proceed with blocklists

```

With `--force` you should get

```
Installation finished. No error reported.

```

The reason why grub-setup does not by default allow this is because in case of partition or a partitionless disk is that grub2-bios relies on embedded blocklists in the partition bootsector to locate the `/boot/grub/core.img` file and the prefix dir `/boot/grub`. The sector locations of `core.img` may change whenever the filesystem in the partition is being altered (files copied, deleted etc.). For more info see [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) and [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

The workaround for this is to set the immutable flag on `/boot/grub/core.img` (using chattr command as mentioned above) so that the sector locations of the `core.img` file in the disk is not altered. The immutable flag on `/boot/grub/core.img` needs to be set only if grub2-bios is installed to a partition boot sector or a partitionless disk, not in case of installation to MBR or simple generation of `core.img` without embedding any bootsector (mentioned above).

###### Generate core.img alone

To populate the `/boot/grub` directory and generate a `/boot/grub/core.img` file WITHOUT embedding any grub2-bios bootsector code in the MBR, post-MBR region, or the partition bootsector, add `--grub-setup=/bin/true` to grub_bios-install:

```
# grub_bios-install --grub-setup=/bin/true --boot-directory=/boot --no-floppy --recheck --debug /dev/sda

```

You can then chainload grub2's core.img from grub-legacy or syslinux as a Linux kernel or a multiboot kernel.

##### Generate GRUB2 BIOS Config file

Finally, generate a configuration for grub2 (this is explained in greater detail in the Configuration section):

```
# GRUB_PREFIX="/boot/grub" grub-mkconfig -o /boot/grub/grub.cfg

```

The GRUB_PREFIX env variable is supported in extra/grub2-common >=1:1.99-6 package.

If grub2 complains about "no suitable mode found" while booting, go to [#Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error).

If `grub-mkconfig` fails, convert your `/boot/grub/menu.lst` file to `/boot/grub/grub.cfg` using:

```
# grub-menulst2cfg /boot/grub/menu.lst /boot/grub/grub.cfg

```

For example:

 `/boot/grub/menu.lst` 
```
default=0
timeout=5

title  Arch Linux Stock Kernel
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux.img

title  Arch Linux Stock Kernel Fallback
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux-fallback.img

```
 `/boot/grub/grub.cfg` 
```
set default='0'; if [ x"$default" = xsaved ]; then load_env; set default="$saved_entry"; fi
set timeout=5

menuentry 'Arch Linux Stock Kernel' {
  set root='(hd0,1)'; set legacy_hdbias='0'
  legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
  legacy_initrd '/initramfs-linux.img' '/initramfs-linux.img'

}

menuentry 'Arch Linux Stock Kernel Fallback' {
  set root='(hd0,1)'; set legacy_hdbias='0'
  legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
  legacy_initrd '/initramfs-linux-fallback.img' '/initramfs-linux-fallback.img'
}

```

If you forgot to create a GRUB2 `/boot/grub/grub.cfg` configfile and simply rebooted into GRUB2 Command Shell, type:

```
sh:grub> insmod legacycfg
sh:grub> legacy_configfile ${prefix}/menu.lst

```

Boot into Arch and re-create the proper GRUB2 `/boot/grub/grub.cfg` configfile.

**Note:** This option works only in BIOS systems, not in UEFI systems.

##### Multiboot in BIOS

###### Boot Microsoft Windows installed in BIOS-MBR mode

**Note:** GRUB2 supports booting `bootmgr` directly and chainload of partition boot sector is no longer required to boot Windows in a BIOS-MBR setup.

Find the UUID of the NTFS filesystem of the Windows's SYSTEM PARTITION where the bootmgr and its files reside. For example, if Windows `bootmgr` exists at `/media/Windows/bootmgr`:

```
# grub-probe --target=fs_uuid /media/Windows/bootmgr
69B235F6749E84CE

```

Then, add the below code to `/etc/grub.d/40_custom` and regenerate grub.cfg with grub-mkconfig as explained above to chainload Windows (Vista, 7 or 8) installed in BIOS-MBR mode:

```
menuentry "Microsoft Windows 7 BIOS-MBR" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --no-floppy --set=root 69B235F6749E84CE
    ntldr (${root})/bootmgr
}

```

For Windows XP

```
menuentry "Microsoft Windows XP" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --no-floppy --set=root 69B235F6749E84CE
    ntldr (${root})/ntldr
}

```

#### [UEFI](/index.php/UEFI "UEFI") systems

##### Install grub2-uefi package

**Note:** Unless specified as EFI 1.x , EFI and UEFI terms are used interchangeably to denote UEFI 2.x firmware. Also unless stated explicitely, the instructions are general and not Mac specific. Some of them may not work or may be different in Macs. Apple's EFI implementation is neither a EFI 1.x version nor UEFI 2.x version but mixes up both. This kind of firmware does not fall under any one UEFI Specification version and is therefore not a standard UEFI firmware.

GRUB2 UEFI bootloader is available in Arch Linux only from version 1.99~rc1\. To install, first [Detect which UEFI firmware arch](/index.php/Unified_Extensible_Firmware_Interface#Detecting_UEFI_Firmware_Arch "Unified Extensible Firmware Interface") you have (either x86_64 or i386).

Depending on that, install the appropriate package

For 64-bit aka x86_64 UEFI firmware:

```
# pacman -S grub2-efi-x86_64

```

For 32-bit aka i386 UEFI firmware:

```
# pacman -S grub2-efi-i386

```

**Note:** Installing grub2-common (a dependency of grub2-bios) 1.99~rc1 or later, may take forever in some systems since the post_install script runs grub-mkconfig and this script does not provide the option `--no-floppy`. For more details search this option in the article.

**Note:** Simply installing the package won't update the grub.efi file and the grub2 modules in the UEFI System Partition. You need to update the grub.efi file and the grub2 modules in the UEFI System Partition manually using grub_efi_${UEFI_ARCH}-install as explained below.

Also load the device-mapper kernel module without which grub-probe does not reliably detect disks and partitions

```
# modprobe dm-mod

```

##### Install grub2-uefi boot files

###### Install to UEFI SYSTEM PARTITION

**Note:** The below commands assume you are using `grub2-efi-x86_64` (for `grub2-efi-i386` replace `x86_64` with `i386` in the below commands).

The UEFI system partition will need to be mounted at /boot/efi for the GRUB2 install script to detect it.

```
# mkdir -p /boot/efi
# mount -t vfat /dev/sdXY /boot/efi

```

Install GRUB UEFI application and its modules to `/boot/efi/efi/arch_grub` using

```
# grub_efi_x86_64-install --root-directory=/boot/efi --boot-directory=/boot/efi/efi --bootloader-id=arch_grub --no-floppy --recheck --debug

```

If you want to install grub2 modules and grub.cfg at the directory `/boot/grub` and only the grubx64.efi application at `/boot/efi/efi/arch_grub` use

```
# grub_efi_x86_64-install --root-directory=/boot/efi --boot-directory=/boot --bootloader-id=arch_grub --no-floppy --recheck --debug

```

In this case grub2-efi-x86_64 will be installed into /boot/grub, making the behavior consistent with the BIOS verion of GRUB2, but this is not recommended if you use both grub2-bios and grub2-efi-x86_64 in your system, as this will overwrite grub2-bios modules in /boot/grub .

The `--root-directory` option mentions the mountpoint of UEFI SYSTEM PARTITION , `--bootloader-id` mentions the name of the directory used to store the grubx64.efi file and `--boot-directory` mentions the directory wherein the actual modules will be installed (and into which grub.cfg should be created).

The actual paths are

```
<root-directory>/<efi or EFI>/<bootloader-id>/grubx64.efi

```

```
<boot-directory>/grub/<all modules, grub.efi, core.efi, grub.cfg>

```

Note the `--bootloader-id` option does not change `<boot-directory>/grub`, i.e. you cannot install the modules to `<boot-directory>/<bootloader-id>`, the path is hard-coded to <boot-directory>/grub .

In `--root-directory=/boot/efi --boot-directory=/boot/efi/efi --bootloader-id=grub`

```
<root-directory>/<efi or EFI>/<bootloader-id> == <boot-directory>/grub == /boot/efi/efi/grub

```

In `--root-directory=/boot/efi --boot-directory=/boot/efi/efi --bootloader-id=arch_grub`

```
<root-directory>/<efi or EFI>/<bootloader-id> == /boot/efi/efi/arch_grub
<boot-directory>/grub == /boot/efi/efi/grub

```

In `--root-directory=/boot/efi --boot-directory=/boot --bootloader-id=arch_grub`

```
<root-directory>/<efi or EFI>/<bootloader-id> == /boot/efi/efi/arch_grub
<boot-directory>/grub == /boot/grub

```

In `--root-directory=/boot/efi --boot-directory=/boot --bootloader-id=grub`

```
<root-directory>/<efi or EFI>/<bootloader-id> == /boot/efi/efi/grub
<boot-directory>/grub == /boot/grub

```

The `<root-directory>/<efi or EFI>/<bootloader-id>/grubx64.efi` is an exact copy of `<boot-directory>/grub/core.efi` .

**Note:** This behavior of --root-directory , --boot-directory , and --bootloader-id options are specific to UEFI systems and does not occur is BIOS mode. In grub_bios-install, --root-directory is deprecated and --bootloader-id option does not exist.

In all the cases the UEFI SYSTEM PARTITION should be mounted for grub_efi_x86_64-install to install grubx64.efi in it, which will be launched by the firmware (using th efibootmgr created boot entry in non-Mac systems).

If you notice carefully, there is no <device_path> option (Eg: `/dev/sda`) at the end of the `grub_efi_x86_64-install` command unlike the case of setting up grub2 for BIOS systems. Any <device_path> provided will be ignored by the install script as UEFI bootloaders do not use MBR or Partition boot sectors at all.

You may now be able to UEFI boot your system by creating a grub.cfg file by following [#Generate GRUB2 UEFI Config file](#Generate_GRUB2_UEFI_Config_file) and [#Create GRUB2 entry in the Firmware Boot Manager](#Create_GRUB2_entry_in_the_Firmware_Boot_Manager).

##### Create GRUB2 entry in the Firmware Boot Manager

###### Non-Mac UEFI systems

grub_efi_${UEFI_ARCH}-install will ensure that `/boot/efi/efi/arch_grub/grubx64.efi` is launched by default if it detects `efibootmgr` and if it is able to access UEFI Runtime Services. Follow [Unified Extensible Firmware Interface#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface#efibootmgr "Unified Extensible Firmware Interface") for more info.

If you have problems running GRUB2 in UEFI mode you can try the following (worked on an ASUS Z68 mainboard):

```
# cp /boot/efi/efi/arch_grub/grubx64.efi /boot/efi/shellx64.efi

```

or

```
# cp /boot/efi/efi/arch_grub/grubx64.efi /boot/efi/efi/shellx64.efi

```

or

```
# cp /boot/efi/efi/arch_grub/grubx64.efi /boot/efi/efi/shell/shellx64.efi

```

After this launch the UEFI Shell from the UEFI setup/menu (in ASUS UEFI BIOS, switch to advanced mode, press Exit in the top right corner and choose "Launch EFI shell from filesystem device"). The grub2 menu will show up and you can boot into your system. Afterwards you can use efibootmgr to setup a menu entry (see above).

###### Apple Mac EFI systems

**Note:** TODO: Grub upstream bzr mactel branch [http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes](http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes)

**Note:** TODO: Fedora's mactel-boot ( [https://bugzilla.redhat.com/show_bug.cgi?id=755093](https://bugzilla.redhat.com/show_bug.cgi?id=755093) )

Use bless command from within Mac OS X to set `grubx64.efi` as the default boot option. You can also boot from the Mac OS X install disc and launch a Terminal there if you only have Linux installed. In the Terminal, create a directory and mount the EFI System Partition:

```
# cd /Volumes
# mkdir efi
# mount -t msdos /dev/disk0s1 /Volumes/efi

```

Then run bless on `grub.efi` and on the EFI partition to set them as the default boot options.

```
# bless --folder=/Volumes/efi --file=/Volumes/efi/efi/arch_grub/grubx64.efi --setBoot
# bless --mount=/Volumes/efi --file=/Volumes/efi/efi/arch_grub/grubx64.efi --setBoot

```

More info at [https://help.ubuntu.com/community/UEFIBooting#Apple_Mac_EFI_systems_.28both_EFI_architecture.29](https://help.ubuntu.com/community/UEFIBooting#Apple_Mac_EFI_systems_.28both_EFI_architecture.29).

##### Generate GRUB2 UEFI Config file

Finally, generate a configuration for grub2 (this is explained in greater detail in the Configuration section):

```
# GRUB_PREFIX="<boot-directory>/grub" grub-mkconfig -o <boot-directory>/grub/grub.cfg

```

If you used `--boot-directory=/boot/efi/efi` :

```
# GRUB_PREFIX="/boot/efi/efi/grub" grub-mkconfig -o /boot/efi/efi/grub/grub.cfg

```

If you used `--boot-directory=/boot` :

```
# GRUB_PREFIX="/boot/grub" grub-mkconfig -o /boot/grub/grub.cfg

```

This is independent of the value of --bootloader-id option. The `GRUB_PREFIX` env variable is supported in extra/grub2-common >=1:1.99-6 package.

If grub2-uefi complains about "no suitable mode found" while booting, try [#Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error).

##### Create GRUB2 Standalone UEFI Application

It is possible to create a grubx64_standalone.efi application which has all the modules embeddded in a memdisk within the uefi application, thus removing the need for having a separate directory populated with all the grub2 uefi modules and other related files. This is done using the grub-mkstandalone command which is included in extra/grub2-common >= 1:1.99-6 package.

The easiest way to do this would be with the install command already mentioned before, but specifying the modules to include. For example:

```
# grub-mkstandlone --directory="/usr/lib/grub-x86_64-efi" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/efi/arch_grub/grubx64_standalone.efi" <any extra files you want to include>

```

The grubx64_standalone.efi file expects grub.cfg to be within its $prefix which is (memdisk)/boot/grub. The memdisk is embedded within the efi app. The grub-mkstandlone script allow passing files to be included in the memdisk image to be as the arguments to the script (in <any extra files you want to include>).

If you have the grub.cfg at `/home/user/Desktop/grub.cfg`, then create a temporary `/home/user/Desktop/boot/grub/` directory, copy the `/home/user/Desktop/grub.cfg` to `/home/user/Desktop/boot/grub/grub.cfg`, cd into `/home/user/Desktop/boot/grub/` and run

```
# grub-mkstandlone --directory="/usr/lib/grub-x86_64-efi" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/efi/arch_grub/grubx64_standalone.efi" "boot/grub/grub.cfg"

```

The reason to cd into `/home/user/Desktop/boot/grub/` and to pass the file path as `boot/grub/grub.cfg` (notice the lack of a leading slash - boot/ vs /boot/ ) is because `dir1/dir2/file` is included as `(memdisk)/dir1/dir2/file` by the grub-mkstandalone script.

If you pass `/home/user/Desktop/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/grub.cfg`. If you pass `/home/user/Desktop/boot/grub/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/boot/grub/grub.cfg` . That is the reason for cd'ing into `/home/user/Desktop/boot/grub/` and passing `boot/grub/grub.cfg`, to includ the file as `(memdisk)/boot/grub/grub.cfg`, which is what grub.efi expects the file to be.

You need to create an UEFI Boot Manager entry for `/boot/efi/efi/arch_grub/grubx64_standalone.efi` using `efibootmgr`. Follow [#Create GRUB2 entry in the Firmware Boot Manager](#Create_GRUB2_entry_in_the_Firmware_Boot_Manager).

##### Multiboot in UEFI

###### Chainload Microsoft Windows x86_64 UEFI-GPT

Find the UUID of the FAT32 filesystem in the UEFI SYSTEM PARTITION where the Windows UEFI Bootloader files reside. For example, if Windows `bootmgfw.efi` exists at `/boot/efi/efi/Microsoft/Boot/bootmgfw.efi` (ignore the upper-lower case differences since that is immaterial in FAT filesystem):

```
# grub-probe --target=fs_uuid /boot/efi/efi/Microsoft/Boot/bootmgfw.efi
1ce5-7f28

```

```
# grub-probe --target=hints_string /boot/efi/efi/Microsoft/Boot/bootmgfw.efi
--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1

```

Then, add this code to `/boot/grub/grub.cfg` OR `/boot/efi/efi/grub/grub.cfg` to chainload Windows x86_64 (Vista SP1+, 7 or 8) installed in UEFI-GPT mode:

```
menuentry "Microsoft Windows x86_64 UEFI-GPT" {
    insmod part_gpt
    insmod fat
    insmod search_fs_uuid
    insmod chain
    search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1 1ce5-7f28
    chainloader /efi/Microsoft/Boot/bootmgfw.efi
}

```

## Configuration

You can also choose to automatically generate or manually edit `grub.cfg`.

**Note:** If GRUB2 was installed with the `--boot-directory` option set, the `grub.cfg` file must be placed in the same directory as `grubx64.efi`. Otherwise, the `grub.cfg` file goes in `/boot/grub/`, just like in the BIOS version of GRUB2.

### Automatically generating using grub-mkconfig (Recommended)

The GRUB2 `menu.1st` equivalent configuration files are `/etc/default/grub` and `/etc/grub.d/*`. grub-mkconfig uses these files to generate `grub.cfg`. By default the script outputs to stdout. To generate a `grub.cfg` file run the command:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

`/etc/grub.d/10_linux` is set to automatically add menu items for Arch linux that work out of the box, to any generated configuration. Other operating systems may need to be added manually by editing `/etc/grub.d/40_custom`

### Manually creating grub.cfg

A basic grub file uses the following options

*   `(hdX,Y)` is the partition `Y` on disk `X`, partition numbers starting at 1, disk numbers starting at 0
*   `set default=N` is the default boot entry that is chosen after timeout for user action
*   `set timeout=M` is the time `M` to wait in seconds for a user selection before default is booted
*   `menuentry "title" {entry options}` is a boot entry titled `title`
*   `set root=(hdX,Y)` sets the boot partition, where the kernel and GRUB modules are stored (boot need not be a separate partition, and may simply be a directory under the "root" partition (`/`)

An example configuration:

```
/boot/grub/grub.cfg

```

```
# Config file for GRUB2 - The GNU GRand Unified Bootloader
# /boot/grub/grub.cfg

# DEVICE NAME CONVERSIONS
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,2)
#  /dev/sda3       (hd0,3)
#

# Timeout for menu
set timeout=5

# Set default boot entry as Entry 0
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
    set root=(hd0,1)
    linux /vmlinuz-linux root=/dev/sda3 ro
    initrd /initramfs-linux.img
}

## (1) Windows
#menuentry "Windows" {
#set root=(hd0,3)
#chainloader +1
#}

```

### Dual-booting

*NOTE: If you want GRUB2 to automatically search for other systems, for example as in Ubuntu. Then you may need to install [os-prober](https://www.archlinux.org/packages/?name=os-prober).*

#### Using grub-mkconfig

The best way to add other entries is editing the `/etc/grub.d/40_custom`. The entries in this file will be automatically added when running **grub-mkconfig**. After adding the new lines, run:

```
# grub-mkconfig -o /boot/grub/grub.cfg 

```

to generate an updated `grub.cfg`.

##### With GNU/Linux

Assuming that the other distro is on partition `sda2`:

```
menuentry "Other Linux" {
set root=(hd0,2)
linux /boot/vmlinuz (add other options here as required)
initrd /boot/initrd.img (if the other kernel uses/needs one)
}

```

##### With FreeBSD

Requires that FreeBSD is installed on a single partition with UFS. Assuming it is installed on `sda4`:

```
menuentry "FreeBSD" {
set root=(hd0,4)
chainloader +1
}

```

##### With Windows

This assumes that your Windows partition is `sda3`.

```
# (2) Windows XP
menuentry "Windows XP" {
    set root=(hd0,3)
    chainloader (hd0,3)+1
}

```

If the windows bootloader is on an entirely different harddrive than grub, it may be necessary to trick Windows into believing that it is in fact the first harddrive. This was possible in the old grub with `map` and is now done with `drivemap`. Assume grub is on `hd0` and windows on `hd2`, you need to add the following after `set root`:

```
drivemap -s hd0 hd2

```

#### With Windows via EasyBCD and NeoGRUB

Since EasyBCD's NeoGRUB currently does not understand the GRUB2 menu format, chainload to it by replacing the contents of your `C:\NST\menu.lst` file with lines similar to the following:

```
default 0
timeout 1

```

```
title       Chainload into GRUB v2
root        (hd0,7)
kernel      /boot/grub/core.img

```

### Visual Configuration

In GRUB2 it is possible, by default, to change the look of the menu. Make sure to initialize, if not done already, grub2 graphical terminal, gfxterm, with proper video mode, gfxmode, in grub2\. This can be seen in the section [#Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error). This video mode is passed by grub2 to the linux kernel via 'gfxpayload' so any visual configurations need this mode in order to be in effect.

#### Setting the framebuffer resolution

Grub2 can set the framebuffer for both grub2 itself and the kernel. The old *vga=* way is deprecated. The preferred method is editing `/etc/default/grub` as the following sample:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

To generate the changes, run:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

The `gfxpayload` property will make sure the kernel keeps the resolution.

**Note:** If this example does not work for you try to replace `gfxmode="1024x768x32"` by `vbemode="0x105"`. Remember to replace the specified resolution with one suitable for your screen.

**Note:** To show all the modes you can use `# hwinfo --framebuffer` (hwinfo is available in [community]), while at grub2 prompt you can use the `vbeinfo` command.

If this method does not work for you, the deprecated `vga=` method will still work. Just add it next to the `"GRUB_CMDLINE_LINUX_DEFAULT="` line in `/etc/default/grub` for eg: `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` will give you a `1024x768` resolution.

You can choose one of these resolutions: `640×480`, `800×600`, `1024×768`, `1280×1024`, `1600×1200`

#### 915resolution hack

Some times for Intel graphic adapters neither `# hwinfo --framebuffer` nor `vbeinfo` will show you the desired resolution. In this case you can use `915resolution` hack. This hack will temporarily modify video BIOS and add needed resolution. See [915resolution's home page](http://915resolution.mango-lang.org/)

In the following I will proceed with the example for my system. Please adjust the recipe for your needs. First you need to find a video mode which will be modified later. For that, run `915resolution` in GRUB2 command shell.

```
915resolution -l

```

The output will be something like:

```
Intel 800/900 Series VBIOS Hack : version 0.5.3
...
Mode 30 : 640x480, 8 bits/pixel
...

```

Next, our purpose is to overwrite mode 30\. (You can choose what ever mode you want.) In the file `/etc/grub.d/00_header` just before the `set gfxmode=${GRUB_GFXMODE}` line insert

```
915resolution 30 1440 900

```

Here we are overwriting the mode `30` with `1440x900` resolution. Lastly we need to set `GRUB_GFXMODE` as described earlier, regenerate grub configuration file and reboot to test changes.

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
sudo reboot

```

#### Background image and bitmap fonts

GRUB2 comes with support for background images and bitmap fonts in pf2 format. The unifont font is included in the grub2 package under the filename `unicode.pf2`, or, as only ascii characters under the name `ascii.pf2`.

Image formats supported include tga, png and jpeg, providing the correct modules are loaded. The maximum supported resolution depends on your hardware.

Make sure you have set up the proper [framebuffer resolution](/index.php/GRUB2#Setting_the_framebuffer_resolution "GRUB2").

Edit `/etc/default/grub` like this:

```
GRUB_BACKGROUND="/boot/grub/archlinux.tga"
#GRUB_THEME="/path/to/gfxtheme"

```

(archlinux.tga is a placeholder; put your file name there)

**Note:** If you have installed Grub on a separate partition, `/boot/grub/archlinux.tga` becomes `/grub/archlinux.tga`.

To generate the changes and add the information into grub.cfg, run:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

If adding the splash image was successful, the user will see "Found background image..." in the terminal as the command is executed. If this phrase is not seen, the image information was probably not incorporated into the grub.cfg file.

If the image is not displayed, check:

*   The path and the filename in /etc/default/grub are correct.
*   The image is of the proper size and format (tga, png, 8-bit jpg).
*   The image was saved in the RGB mode, and is not indexed.
*   The console mode is not enabled in /etc/default/grub.
*   The command grub-mkconfig must be executed to place the background image information into the /boot/grub/grub.cfg file.

#### Menu colors

As in Grub (0.9x), you can change the menu colors in Grub2\. The available colors for GRUB2 are at [http://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html#Theme-file-format](http://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html#Theme-file-format). Here is an example:

Edit `/etc/default/grub`:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

Generate the changes:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

#### Hidden menu

One of the unique features of Grub2 is hiding/skipping the menu and showing it by holding "Shift" when needed. You can also adjust whether you want to see the timeout counter.

Edit `/etc/default/grub` as you wish. Here is an example where the comments from the beginning of the two lines have been removed to enable the feature, the timeout has been set to five seconds and to be shown to the user:

```
GRUB_HIDDEN_TIMEOUT=5
GRUB_HIDDEN_TIMEOUT_QUIET=false

```

and run:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

### Other Options

#### LVM

If you use [LVM](/index.php/LVM "LVM") for your `/boot`, add the following before menuentry lines:

```
insmod lvm

```

and specify your root in the menuentry as:

```
set root=(*lvm_group_name*-*lvm_logical_boot_partition_name*)

```

Example:

```
# (0) Arch Linux
menuentry "Arch Linux" {
insmod lvm
set root=(VolumeGroup-lv_boot)
# you can only set following two lines
linux /vmlinuz-linux root=/dev/mapper/VolumeGroup-root ro
initrd /initramfs-linux.img
}

```

#### Raid

Grub2 provides convenient handling of raid-volumes. You need to add:

```
insmod raid

```

which allows you to address the volume natively. E.g. `/dev/md0` becomes:

```
set root=(md0)

```

whereas a partitioned raid-volume (e.g. `/dev/md0p1`) becomes:

```
set root=(md0,1)

```

#### Persistent block device naming

You can use UUIDs to detect partitions instead of the "old" `/dev/sd*` scheming. It has the advantage of detecting partitions by their unique UUIDs, which is needed by some people booting with complicated partition setups.

UUIDs are used by default in the recent versions of grub2 - there is no downside in it anyway except that you need to re-generate the `grub.cfg` file every time you resize or reformat your partitions. Remember this when modifying partitions with Live-CD.

The recent versions of grub2 use UUIDs by default. You can re-enable the use of UUIDS by simply commenting the UUID line (this is also what it looks like by default):

```
#GRUB_DISABLE_LINUX_UUID=true

```

you can also just set the value as `false` as shown here:

```
GRUB_DISABLE_LINUX_UUID=false

```

Either way, do not forget to generate the changes:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

#### Using Labels

It is possible to use labels, human-readable strings attached to filesystems, by using the `--label` option to `search`. First of all, label your existing partition:

```
# tune2fs -L a <LABEL> <PARTITION>

```

Then, add an entry using labels. An example of this:

```
menuentry "Arch Linux, session texte" {
    search --label --no-floppy --set=root archroot
    linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
    initrd /boot/initramfs-linux.img
}

```

#### Recall previous entry

Grub2 can remember the last entry you booted from and use this as the default entry to boot from next time. This is useful if you have multiple kernels (i.e., the current Arch one and the LTS kernel as a fallback option) or operating systems. To do this, edit `/etc/default/grub` and change the setting of `GRUB_DEFAULT`:

```
GRUB_DEFAULT=saved

```

This ensures that grub will default to the saved entry. To enable saving the selected entry, add the following line to `/etc/default/grub`:

```
GRUB_SAVEDEFAULT=true

```

Note that manually added menu items, eg Windows in `/etc/grub.d/40_custom`, will need `savedefault` added. Remember to regenerate your configuration file.

#### Security

If you want to secure GRUB2 so it is not possible for anyone to change boot parameters or use the command line, you can add a user/password combination to GRUB2's configuration files. To do this, run the command `grub-mkpasswd_pbkdf2`. Enter a password and confirm it. The output will look like this:

 `Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A` Then, add the following to `/etc/grub.d/00_header`:
```
cat << EOF

set superusers="username"
password_pbkdf2 username <password>

EOF
```

where <password> is the string generated by `grub-mkpasswd_pbkdf2`.

Regenerate your configuration file. Your GRUB2 command line and boot parameters are now protected.

#### Root Encryption

To let GRUB2 automatically add the kernel parameters for root encryption, add "cryptdevice=/dev/yourdevice:label" to GRUB_CMDLINE_LINUX in /etc/defaults/grub .

Example with root mapped to /dev/mapper/root :

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:root"

```

Also, disable the usage of UUIDs for the rootfs:

```
GRUB_DISABLE_LINUX_UUID=true

```

Regenerate the configuration.

### Booting an ISO Directly From Grub2

Edit `/etc/grub.d/40_custom` to add an entry for the target ISO. When finished, update the grub menu as with the usual `grub-mkconfig -o /boot/grub/grub.cfg` (as root).

#### Arch ISO

**Note:** Be sure to adjust the "hdX,Y" in the third line to point to the correct disk/partition number of the isofile. Also adjust the img_dev line to match this same location.

```
menuentry "Archlinux-2011.08.19-netinstall-x86_64.iso" {
set isofile="/archives/archlinux-2011.08.19-netinstall-x86_64.iso"
loopback loop (hd0,7)$isofile
linux (loop)/arch/boot/x86_64/vmlinuz archisolabel=ARCH_201108 img_dev=/dev/sda7 img_loop=$isofile earlymodules=loop
initrd (loop)/arch/boot/x86_64/archiso.img
}

```

#### Ubuntu ISO

**Note:** Be sure to adjust the "hdX,Y" in the third line to point to the correct disk/partition number of the isofile.

```
menuentry "ubuntu-11.04-desktop-amd64.iso" {
set isofile="/path/to/ubuntu-11.04-desktop-amd64.iso"
loopback loop (hdX,Y)$isofile
linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile quiet noeject noprompt splash --
initrd (loop)/casper/initrd.lz
}

```

## Using the command shell

Since the MBR is too small to store all GRUB2 modules, only the menu and a few basic commands reside there. The majority of GRUB2 functionality remains in modules in `/boot/grub`, which are inserted as needed. In error conditions (e.g. if the partition layout changes) GRUB2 may fail to boot. When this happens, a command shell may appear.

GRUB2 offers multiple shells/prompts. If there is a problem reading the menu but the bootloader is able to find the disk, you will likely be dropped to the "normal" shell:

```
sh:grub>

```

If there is a more serious problem (e.g. GRUB cannot find required files), you may instead be dropped to the "rescue" shell:

```
grub rescue>

```

The rescue shell is a restricted subset of the normal shell, offering much less functionality. If dumped to the rescue shell, first try inserting the "normal" module, then starting the "normal" shell:

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/normal.mod
rescue:grub> normal

```

### Pager support

GRUB2 supports pager for reading commands that provide long output (like the help command). This works only in normal shell mode and not in rescue mode. To enable pager, in GRUB2 command shell type:

```
sh:grub> set pager=1

```

## GUI configuration tools

Following package may be installed from [AUR](/index.php/AUR "AUR")

*   [grub-customizer](https://aur.archlinux.org/packages.php?ID=44020) (requires gettext gksu gtkmm hicolor-icon-theme openssl)

    	Customize the bootloader (GRUB2 or BURG)

*   [grub2-editor](http://kde-apps.org/content/show.php?content=139643) (requires kdelibs)

    	A KDE4 control module for configuring the GRUB2 bootloader

*   [kcm-grub2](http://kde-apps.org/content/show.php?content=137886) (requires kdelibs python2-qt kdebindings-python)

    	This Kcm module manages the most common settings of Grub2.

*   [startupmanager](http://sourceforge.net/projects/startup-manager/) (requires gnome-python imagemagick yelp python2 xorg-xrandr)

    	GUI app for changing the settings of GRUB, GRUB2, Usplash and Splashy

## parttool or legacy hide/unhide

If you have a win9x paradigm with hidden C disks GRUB legacy had the hide/unhide feature. In GRUB2 this has been replaced by parttool. For example, to boot the third C disk of three win9x installations on the CLI enter the CLI and:

```
parttool hd0,1 hidden+ boot-
parttool hd0,2 hidden+ boot-
parttool hd0,3 hidden- boot+
set root=hd0,3
chainloader +1
boot

```

## Using the rescue console

See [#Using the command shell](#Using_the_command_shell) first. If unable to activate the standard shell, one possible solution is to boot using a live CD or some other rescue disk to correct configuration errors and reinstall GRUB. However, such a boot disk is not always available (nor necessary); the rescue console is surprisingly robust.

The available commands in GRUB rescue include "insmod", "ls", "set", and "unset". This example uses "set" and "insmod". "set" modifies variables and "insmod" inserts new modules to add functionality.

Before starting, the user must know the location of their `/boot` partition (be it a separate partition, or a subdirectory under their root):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

where X is the physical drive number and Y is the partition number.

To expand console capabilities, insert the "linux" module:

```
grub rescue> insmod (hdX,Y)/boot/grub/linux.mod

```

**Note:** With a separate boot partition, omit `/boot` from the path, (i.e. type `set prefix=(hdX,Y)/grub` and `insmod (hdX,Y)/grub/linux.mod`).

This introduces the "linux" and "initrd" commands, which should be familiar (see [#Configuration](#Configuration)).

An example, booting Arch Linux:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot

```

With a separate boot partition, again change the lines accordingly:

```
set root=(hd0,5)
linux /vmlinuz-linux root=/dev/sda6
initrd /initramfs-linux.img
boot

```

After successfully booting the Arch Linux installation, users can correct `grub.cfg` as needed and then run:

```
# grub-install /dev/sda --no-floppy

```

to reinstall GRUB2 and fix the problem completely, changing `/dev/sda` if needed. See [#Bootloader installation](#Bootloader_installation) for details.

## Combining the use of UUID's and basic scripting

If you like the idea of using UUID's to avoid unreliable BIOS mappings or are struggling with Grub's syntax, here is an example boot menu item that uses UUID's and a small script to direct Grub to the proper disk partitions for your system. All you need to do is replace the UUID's in the sample with the correct UUID's for your system. (The example applies to a system with a boot and root partition. You will obviously need to modify the Grub configuration if you have additional partitions.)

```
 menuentry "Arch Linux 64" {
     # Set the UUIDs for your boot and root partition respectively
     set the_boot_uuid=ece0448f-bb08-486d-9864-ac3271bd8d07   
     set the_root_uuid=c55da16f-e2af-4603-9e0b-03f5f565ec4a

     # (Note: This may be the same as your boot partition)

     # Get the boot/root devices and set them in the root and grub_boot variables  
     search --fs-uuid --no-floppy --set=root $the_root_uuid      
     search --fs-uuid --no-floppy --set=grub_boot $the_boot_uuid

     # Check to see if boot and root are equal.
     # If they are, then append /boot to $grub_boot (Since $grub_boot is actually the root partition)
     if [ $the_boot_uuid == $the_root_uuid] ; then
         set grub_boot=$grub_boot/boot
     fi

     # $grub_boot now points to the correct location, so the following will properly find the kernel and initrd
     linux ($grub_boot)/vmlinuz-linux root=/dev/disk/by-uuid/$uuid_os_root ro
     initrd ($grub_boot)/initramfs-linux.img
 }

```

## Troubleshooting

Any troubleshooting should be added here.

### Enable GRUB2 debug messages

Add

```
set pager=1
set debug=all

```

to `grub.cfg`.

### Correct GRUB2 No Suitable Mode Found Error

If you get this error when booting any menuentry

```
error: no suitable mode found
Booting however

```

Then you need to initialize grub2 graphical terminal (gfxterm) with proper video mode (gfxmode) in grub2\. This video mode is passed by grub2 to the linux kernel via 'gfxpayload'. In case of UEFI systems, if the grub2 video mode is not initialized, no kernel boot messages will be shown in the terminal (atleast until KMS kicks in)

Copy `/usr/share/grub/unicode.pf2` to ${GRUB2_PREFIX_DIR} (`/boot/grub/` in case of BIOS and UEFI systems. If GRUB2 UEFI was installed with `--boot-directory=/boot/efi/efi` set, then the directory is `/boot/efi/efi/grub/`.

```
# cp /usr/share/grub/unicode.pf2 ${GRUB2_PREFIX_DIR}

```

If `/usr/share/grub/unicode.pf2` does not exist, install [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont), create the unifont.pf2 file and then copy it to ${GRUB2_PREFIX_DIR}.

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

Then, in the `grub.cfg` file, add the following lines to enable grub2 to pass the video mode correctly to the kernel, without of which you will only get a black screen (no output) but booting (actually) proceeds successfully without any system hang:

BIOS systems

```
insmod vbe

```

UEFI systems

```
insmod efi_gop
insmod efi_uga

```

After that add the following code (common to both BIOS and UEFI)

```
insmod font

```

```
if loadfont ${prefix}/unicode.pf2
then
    insmod gfxterm
    set gfxmode=auto
    set gfxpayload=keep
    terminal_output gfxterm
fi

```

As you can see for gfxterm (graphical terminal) to function properly, `unicode.pf2` font file should exist in ${GRUB2_PREFIX_DIR}.

### msdos-style error message

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding won't be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

This error may occur when you try installing GRUB2 in a VMware container. Read more about it [here](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). It happens when the first partition starts just after the MBR (block 63), without the usual space of 1 MiB (2048 blocks) before the first partition. Read [#MBR_aka_msdos_partitioning_specific_instructions](#MBR_aka_msdos_partitioning_specific_instructions)

### UEFI GRUB2 drops to shell

If grub loads but drop you into the rescue shell with no errors, it may be because of a missing or misplaced `grub.cfg`. This will happen if GRUB2 UEFI was installed with `--boot-directory` and `grub.cfg` is missing OR if the partition number of the boot partition changed (which is hard-coded into the `grubx64.efi` file).

### UEFI GRUB2 not loaded

In some cases the EFI may fail to load grub correctly. Provided everything is set up correctly, the output of

```
efibootmgr -v

```

might look something like this:

```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\efi\grub\grub.efi)
Boot0001* Shell	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EfiShell.efi)
Boot0002* Festplatte	BIOS(2,0,00)P0: SAMSUNG HD204UI

```

If everything works correctly, the EFI would now automatically load grub.
If the screen only goes black for a second and the next boot option is tried afterwards, according to [this post](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), moving grub to the partition root can help. The boot option has to be deleted and recreated afterwards. The entry for grub should look like this then:

```
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

### Invalid signature

If trying to boot windows results in an "invalid signature" error, e.g. after reconfiguring partitions or adding additional hard drives, (re)move grub's device configuration and let it reconfigure.

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

Grub-mkconfig should now mention all found boot options including windows. If it works, remove /boot/grub/device.map-old.

## References

1.  Official GRUB2 Manual - [http://www.gnu.org/software/grub/manual/grub.html](http://www.gnu.org/software/grub/manual/grub.html)
2.  Ubuntu wiki page for Grub2 - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
3.  GRUB2 wiki page describing steps to compile for UEFI systems - [https://help.ubuntu.com/community/UEFIBooting](https://help.ubuntu.com/community/UEFIBooting)
4.  Wikipedia's page on [BIOS Boot Partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")

## External Links

1.  [A Linux Bash Shell script to compile and install GRUB2 for BIOS from BZR Source](https://github.com/the-ridikulus-rat/My_Shell_Scripts/blob/master/grub2/grub2_bios.sh)
2.  [A Linux Bash Shell script to compile and install GRUB2 for UEFI from BZR Source](https://github.com/the-ridikulus-rat/My_Shell_Scripts/blob/master/grub2/grub2_uefi.sh)