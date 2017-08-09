[GRUB2](http://www.gnu.org/software/grub/) 是新一代的 GRand Unified Bootloader (GRUB/開機引導程式). GRUB2 來自於 [PUPA](http://www.nongnu.org/pupa/) 這個探討下一代 GRUB 的研究專案 。GRUB 2 被重新編寫，擁有模組化和可移植性。[[1]](http://www.gnu.org/software/grub/grub-faq.html#q1)

簡單地說，*開機引導程式* 是當電腦開機時第一個執行的程式（在此請自動忽略BIOS）。它負責載入並移交控制權給 Linux 核心。而核心載入後，則反過來啟動作業系統內的其它部份。

## Contents

*   [1 前言](#.E5.89.8D.E8.A8.80)
    *   [1.1 給 GRUB 舊版的使用者](#.E7.B5.A6_GRUB_.E8.88.8A.E7.89.88.E7.9A.84.E4.BD.BF.E7.94.A8.E8.80.85)
    *   [1.2 Preliminary Requirements for GRUB2](#Preliminary_Requirements_for_GRUB2)
        *   [1.2.1 BIOS 系統](#BIOS_.E7.B3.BB.E7.B5.B1)
            *   [1.2.1.1 GPT specific instructions](#GPT_specific_instructions)
            *   [1.2.1.2 MBR aka msdos partitioning specific instructions](#MBR_aka_msdos_partitioning_specific_instructions)
        *   [1.2.2 UEFI 系統](#UEFI_.E7.B3.BB.E7.B5.B1)
            *   [1.2.2.1 創建並掛載到UEFI系統分割區(Create and Mount the UEFI SYSTEM PARTITION)](#.E5.89.B5.E5.BB.BA.E4.B8.A6.E6.8E.9B.E8.BC.89.E5.88.B0UEFI.E7.B3.BB.E7.B5.B1.E5.88.86.E5.89.B2.E5.8D.80.28Create_and_Mount_the_UEFI_SYSTEM_PARTITION.29)
*   [2 安裝](#.E5.AE.89.E8.A3.9D)
    *   [2.1 BIOS 系統](#BIOS_.E7.B3.BB.E7.B5.B1_2)
        *   [2.1.1 備份重要資料(Backup Important Data)](#.E5.82.99.E4.BB.BD.E9.87.8D.E8.A6.81.E8.B3.87.E6.96.99.28Backup_Important_Data.29)
        *   [2.1.2 安裝grub-bios套件(Install grub-bios package)](#.E5.AE.89.E8.A3.9Dgrub-bios.E5.A5.97.E4.BB.B6.28Install_grub-bios_package.29)
        *   [2.1.3 安裝grub-bios啟動檔案(Install grub-bios boot files)](#.E5.AE.89.E8.A3.9Dgrub-bios.E5.95.9F.E5.8B.95.E6.AA.94.E6.A1.88.28Install_grub-bios_boot_files.29)
            *   [2.1.3.1 安裝到440位元組MBR啟動區(Install to 440-byte MBR boot code region)](#.E5.AE.89.E8.A3.9D.E5.88.B0440.E4.BD.8D.E5.85.83.E7.B5.84MBR.E5.95.9F.E5.8B.95.E5.8D.80.28Install_to_440-byte_MBR_boot_code_region.29)
            *   [2.1.3.2 Install to Partition or Partitionless Disk](#Install_to_Partition_or_Partitionless_Disk)
            *   [2.1.3.3 單獨產生core.img(Generate core.img alone)](#.E5.96.AE.E7.8D.A8.E7.94.A2.E7.94.9Fcore.img.28Generate_core.img_alone.29)
        *   [2.1.4 產生GRUB2 BOIS設置檔案(Generate GRUB2 BIOS Config file)](#.E7.94.A2.E7.94.9FGRUB2_BOIS.E8.A8.AD.E7.BD.AE.E6.AA.94.E6.A1.88.28Generate_GRUB2_BIOS_Config_file.29)
        *   [2.1.5 在BIOS多重啟動(Multiboot in BIOS)](#.E5.9C.A8BIOS.E5.A4.9A.E9.87.8D.E5.95.9F.E5.8B.95.28Multiboot_in_BIOS.29)
            *   [2.1.5.1 在BIOS-MBR模式中啟動已安裝的Microsoft Windows(Boot Microsoft Windows installed in BIOS-MBR mode)](#.E5.9C.A8BIOS-MBR.E6.A8.A1.E5.BC.8F.E4.B8.AD.E5.95.9F.E5.8B.95.E5.B7.B2.E5.AE.89.E8.A3.9D.E7.9A.84Microsoft_Windows.28Boot_Microsoft_Windows_installed_in_BIOS-MBR_mode.29)
    *   [2.2 UEFI系統(UEFI systems)](#UEFI.E7.B3.BB.E7.B5.B1.28UEFI_systems.29)
        *   [2.2.1 安裝grub-uefi套件(Install grub-uefi package)](#.E5.AE.89.E8.A3.9Dgrub-uefi.E5.A5.97.E4.BB.B6.28Install_grub-uefi_package.29)
        *   [2.2.2 安裝grub-uefi啟動檔案(Install grub-uefi boot files)](#.E5.AE.89.E8.A3.9Dgrub-uefi.E5.95.9F.E5.8B.95.E6.AA.94.E6.A1.88.28Install_grub-uefi_boot_files.29)
            *   [2.2.2.1 Install to UEFI SYSTEM PARTITION](#Install_to_UEFI_SYSTEM_PARTITION)
        *   [2.2.3 Create GRUB2 entry in the Firmware Boot Manager](#Create_GRUB2_entry_in_the_Firmware_Boot_Manager)
            *   [2.2.3.1 Non-Mac UEFI systems](#Non-Mac_UEFI_systems)
            *   [2.2.3.2 Apple Mac EFI systems](#Apple_Mac_EFI_systems)
        *   [2.2.4 產生GRUB2 UEFI設置檔案(Generate GRUB2 UEFI Config file)](#.E7.94.A2.E7.94.9FGRUB2_UEFI.E8.A8.AD.E7.BD.AE.E6.AA.94.E6.A1.88.28Generate_GRUB2_UEFI_Config_file.29)
        *   [2.2.5 Create GRUB2 Standalone UEFI Application](#Create_GRUB2_Standalone_UEFI_Application)
        *   [2.2.6 Multiboot in UEFI](#Multiboot_in_UEFI)
            *   [2.2.6.1 Chainload Microsoft Windows x86_64 UEFI-GPT](#Chainload_Microsoft_Windows_x86_64_UEFI-GPT)
*   [3 設置(Configuration)](#.E8.A8.AD.E7.BD.AE.28Configuration.29)
    *   [3.1 使用grub-mkconfig自動產生(Automatically generating using grub-mkconfig) (Recommended)](#.E4.BD.BF.E7.94.A8grub-mkconfig.E8.87.AA.E5.8B.95.E7.94.A2.E7.94.9F.28Automatically_generating_using_grub-mkconfig.29_.28Recommended.29)
        *   [3.1.1 Additional arguments](#Additional_arguments)
    *   [3.2 手動創建grub.cfg( Manually creating grub.cfg)](#.E6.89.8B.E5.8B.95.E5.89.B5.E5.BB.BAgrub.cfg.28_Manually_creating_grub.cfg.29)
    *   [3.3 雙啟動(dual-boot)](#.E9.9B.99.E5.95.9F.E5.8B.95.28dual-boot.29)
        *   [3.3.1 使用 grub-mkconfig](#.E4.BD.BF.E7.94.A8_grub-mkconfig)
            *   [3.3.1.1 與 GNU/Linux](#.E8.88.87_GNU.2FLinux)
            *   [3.3.1.2 與 FreeBSD](#.E8.88.87_FreeBSD)
            *   [3.3.1.3 與 Windows](#.E8.88.87_Windows)
        *   [3.3.2 With Windows via EasyBCD and NeoGRUB](#With_Windows_via_EasyBCD_and_NeoGRUB)
    *   [3.4 Visual Configuration](#Visual_Configuration)
        *   [3.4.1 Setting the framebuffer resolution](#Setting_the_framebuffer_resolution)
        *   [3.4.2 915resolution hack](#915resolution_hack)
        *   [3.4.3 背景圖片和字體(Background image and bitmap fonts)](#.E8.83.8C.E6.99.AF.E5.9C.96.E7.89.87.E5.92.8C.E5.AD.97.E9.AB.94.28Background_image_and_bitmap_fonts.29)
        *   [3.4.4 佈景主題(Theme)](#.E4.BD.88.E6.99.AF.E4.B8.BB.E9.A1.8C.28Theme.29)
        *   [3.4.5 選單顏色(Menu colors)](#.E9.81.B8.E5.96.AE.E9.A1.8F.E8.89.B2.28Menu_colors.29)
        *   [3.4.6 隱藏選單(Hidden menu)](#.E9.9A.B1.E8.97.8F.E9.81.B8.E5.96.AE.28Hidden_menu.29)
        *   [3.4.7 關閉幀緩衝(Disable framebuffer)](#.E9.97.9C.E9.96.89.E5.B9.80.E7.B7.A9.E8.A1.9D.28Disable_framebuffer.29)
    *   [3.5 其他選項(Other Options)](#.E5.85.B6.E4.BB.96.E9.81.B8.E9.A0.85.28Other_Options.29)
        *   [3.5.1 LVM](#LVM)
        *   [3.5.2 RAID](#RAID)
        *   [3.5.3 Persistent block device naming](#Persistent_block_device_naming)
        *   [3.5.4 Using Labels](#Using_Labels)
        *   [3.5.5 Recall previous entry](#Recall_previous_entry)
        *   [3.5.6 安全(Security)](#.E5.AE.89.E5.85.A8.28Security.29)
        *   [3.5.7 Root Encryption](#Root_Encryption)
    *   [3.6 在GRUB2啟動(ISOBooting an ISO Directly From GRUB2)](#.E5.9C.A8GRUB2.E5.95.9F.E5.8B.95.28ISOBooting_an_ISO_Directly_From_GRUB2.29)
        *   [3.6.1 Arch ISO](#Arch_ISO)
        *   [3.6.2 Ubuntu ISO](#Ubuntu_ISO)
*   [4 Using the command shell](#Using_the_command_shell)
    *   [4.1 Pager support](#Pager_support)
*   [5 GUI configuration tools](#GUI_configuration_tools)
*   [6 parttool or legacy hide/unhide](#parttool_or_legacy_hide.2Funhide)
*   [7 Using the rescue console](#Using_the_rescue_console)
*   [8 Combining the use of UUIDs and basic scripting](#Combining_the_use_of_UUIDs_and_basic_scripting)
*   [9 疑難排解(Troubleshooting)](#.E7.96.91.E9.9B.A3.E6.8E.92.E8.A7.A3.28Troubleshooting.29)
    *   [9.1 Enable GRUB2 debug messages](#Enable_GRUB2_debug_messages)
    *   [9.2 Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error)
    *   [9.3 msdos-style error message](#msdos-style_error_message)
    *   [9.4 UEFI GRUB2 drops to shell](#UEFI_GRUB2_drops_to_shell)
    *   [9.5 UEFI GRUB2 not loaded](#UEFI_GRUB2_not_loaded)
    *   [9.6 Invalid signature](#Invalid_signature)
    *   [9.7 Restore GRUB Legacy](#Restore_GRUB_Legacy)
*   [10 參考資料(References)](#.E5.8F.83.E8.80.83.E8.B3.87.E6.96.99.28References.29)
*   [11 外部連結(External Links)](#.E5.A4.96.E9.83.A8.E9.80.A3.E7.B5.90.28External_Links.29)

## 前言

有些資訊必須先予以澄清:

*   The name *GRUB* officially refers to version *2* of the software, see [[2]](https://www.gnu.org/software/grub/). If you are looking for the article on the legacy version, see [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") (i.e. version 0.9x) 已被開發者們認為是舊作，在 Arch Linux已經被GRUB2取代 . 參閱最新消息 [here](https://www.archlinux.org/news/grub-legacy-no-longer-supported/). Upstream recommends GRUB2 >=1.99 over GRUB Legacy, even for current GRUB Legacy users.

*   The [Archboot](/index.php/Archboot "Archboot") ISO的安裝script支援 [grub-bios](https://www.archlinux.org/packages/?name=grub-bios) 和 [grub-efi-x86_64](https://www.archlinux.org/packages/?name=grub-efi-x86_64)的安裝. 舊版官方的安裝script-AIF (Arch Installation Framework)還未支援 GRUB(2)。

*   從 1.99-6版起, GRUB2 支援 [Btrfs](/index.php/Btrfs "Btrfs") as root (without a separate `/boot` filesystem) compressed with either zlib or LZO.

*   For GRUB2 UEFI info, it is recommended to read the [UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") pages before reading this page.

### 給 GRUB 舊版的使用者

*   GRUB 舊版將從您的系統中移除, 您可以考慮將 GRUB更新到版本 2.x, 或者其他開機程式.

*   Upgrade from [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") to [GRUB](/index.php/GRUB "GRUB")(2) is the much same as fresh installing GRUB(2)which is covered [below](#Installation).

*   GRUB and GRUB2 的指令是有差別的. 請在進行下一步之前自己熟悉一下 [GRUB2 commands](http://grub.enbug.org/CommandList) (例如， "find" 就被更換為 "search").

*   GRUB2 現在己經 *模組化* 且不再需要 "stage 1.5"。因此，引導程式本身是有限的 - 當需要擴充功能時模組才從硬碟內被載入（例如，[LVM](/index.php/LVM "LVM") 或 RAID支援）

*   GRUB2 設備命名也改得和 GRUB 不同。磁區 Partitions 由數字 1 起算，而硬碟仍然由 0 起算，舉例來說，`/dev/sda1` 被 GRUB2 指引為 `(hd0,1)`等 。

### Preliminary Requirements for GRUB2

#### BIOS 系統

##### [GPT](/index.php/GPT "GPT") specific instructions

GRUB2 in BIOS-GPT configuration requires a [BIOS Boot Partition](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html#BIOS-installation) to embed its `core.img` in the absence of post-MBR gap in GPT partitioned systems (which is taken over by the GPT Primary Header and Primary Partition table). This partition is used by GRUB2 only in BIOS-GPT setups. No such partition type exists in case of MBR partitioning (at least not for GRUB2). This partition is also not required if the system is UEFI based, as no embedding of bootsectors takes place in that case. Syslinux does not require this partition.

For a BIOS-GPT configuration, create a 2 MiB partition using cgdisk or GNU Parted with no filesystem. The location of the partition in the partition table does not matter but it should be within the first 2 TiB region of the disk. It is advisable to put it somewhere in the beginning of the disk before the `/boot` partition. Set the partition type to "EF02" in cgdisk or `set <BOOT_PART_NUM> bios_grub on` in GNU Parted.

**Note:** This partition should be created before `grub-install` or `grub-setup` is run or before the **Install Bootloader** step of the Archlinux installer (if GRUB2 BIOS is selected as bootloader).

##### [MBR](/index.php/MBR "MBR") aka msdos partitioning specific instructions

Usually the post-MBR gap (after the 512 byte MBR region and before the start of the 1st partition) in many MBR (or msdos disklabel) partitioned systems is 31 KiB when DOS compatibility cylinder alignment issues are satisfied in the partition table. However a post-MBR gap of about 1 to 2 MiB is recommended to provide sufficient room for embedding GRUB2's `core.img` ([FS#24103](https://bugs.archlinux.org/task/24103)). It is advisable to use a partitioner which supports 1 MiB partition alignment to obtain this space as well as satisfy other non-512 byte sector issues (which are unrelated to embedding of `core.img`).

如果你沒有在BIOS系統中雙啟動到MS Windows (any version), 轉換到 GPT partitioning - [GUID Partition Table#Convert_from_MBR_to_GPT](/index.php/GUID_Partition_Table#Convert_from_MBR_to_GPT "GUID Partition Table")是很適合的。

**Warning:** Create the 2MiB partition mentioned above BEFORE you convert to GPT. If you do not, gparted will not resize your boot partition to allow its creation, and when you reboot GRUB2 will not know where to look.

#### UEFI 系統

##### 創建並掛載到UEFI系統分割區(Create and Mount the UEFI SYSTEM PARTITION)

**注意:** 建議先閱讀 [UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") 頁面

遵循 [Unified Extensible Firmware Interface#Create_an_UEFI_System_Partition_in_Linux](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface") 中創建 UEFI SYSTEM PARTITION的指引. 接在將 UEFI SYSTEM PARTITION（也就是ESP分割區） 掛載在 `/boot/efi`. 如果您已經將 UEFI System Partition 掛載在其他掛載點, 以此掛載點置換在下面指引中的 {ic|/boot/efi}} :

```
# mkdir -p /boot/efi
# mount -t vfat <UEFISYS_PART_DEVICE> /boot/efi

```

如果<UEFI_系統分割區>`/EFI`不存在，請創建它的路徑(如：/boot/efi/EFI)

```
# mkdir -p /boot/efi/EFI

```

## 安裝

### BIOS 系統

#### 備份重要資料(Backup Important Data)

雖然 GRUB(2) 的安裝應該會是相當平穩的,仍然強烈建議安裝 [grub-bios](https://www.archlinux.org/packages/?name=grub-bios)前保留舊版的 GRUB資料。

```
# mv /boot/grub /boot/grub-legacy

```

備份內含啟動碼(boot code)跟分區對映表(partition table)的 MBR (根據您的實際硬碟分割情形，置換 `/dev/sd**X**` )

```
# dd if=/dev/sdX of=/path/to/backup/mbr_backup bs=512 count=1

```

只有 MBR中的446 位元組包含啟動碼, 接者的 64 位元組包含分區對映表. 如果您不想在將來回存到MBR時覆蓋掉你新設置的分區對映表，強烈建議此時只備份MBR啟動碼就好:

```
# dd if=/dev/sdX of=/path/to/backup/bootcode_backup bs=446 count=1

```

如果無法正確安裝 GRUB2 , 參閱 [GRUB2#Restore_GRUB_Legacy](/index.php/GRUB2#Restore_GRUB_Legacy "GRUB2").

#### 安裝grub-bios套件(Install grub-bios package)

```
GRUB(2)套件可以用pacman安裝 (安裝完將會取代 [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/) or [grub](https://www.archlinux.org/packages/?name=grub)):

# pacman -S grub-bios

```

**Note:** 僅安裝套件並不會更新 `/boot/grub/i386-pc/core.img` 檔案和 GRUB(2) 在 `/boot/grub/i386-pc`的模組. 你必須如下解釋般使用 `grub-install`來更新他們

#### 安裝grub-bios啟動檔案(Install grub-bios boot files)

要達到BIOS啟動有三種安裝 GRUB(2)方法:

*   [#安裝到440位元組MBR啟動區(Install to 440-byte MBR boot code region)](#.E5.AE.89.E8.A3.9D.E5.88.B0440.E4.BD.8D.E5.85.83.E7.B5.84MBR.E5.95.9F.E5.8B.95.E5.8D.80.28Install_to_440-byte_MBR_boot_code_region.29) (建議) ,
*   [#Install to Partition or Partitionless Disk](#Install_to_Partition_or_Partitionless_Disk) (不建議),
*   [#Generate_core.img_alone](#Generate_core.img_alone) (最安全的方法,但需要安裝其他的BIOS引導程式像是 [grub-legacy](/index.php/Grub-legacy "Grub-legacy") 或 [syslinux](/index.php/Syslinux "Syslinux") 來連鎖啟動 (chainload) `/boot/grub/i386-pc/core.img`).

##### 安裝到440位元組MBR啟動區(Install to 440-byte MBR boot code region)

To setup `grub-bios` in the 440-byte Master Boot Record boot code region, populate the `/boot/grub` directory, generate the `/boot/grub/i386-pc/core.img` file, and embed it in the 31 KiB (minimum size - varies depending on partition alignment) post-MBR gap (MBR disks) or in BIOS Boot Partition (GPT disks), run:

```
# modprobe dm-mod
# grub-install --target=i386-pc --recheck --debug /dev/sda
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

where `/dev/sda` is the destination of the installation (in this case the MBR of the first SATA disk). If you use [LVM](/index.php/LVM "LVM") for your `/boot`, you can install GRUB2 on multiple physical disks.

**Note:** Without `--target` or `--directory` option, grub-install cannot determine for which firmware grub(2) is being installed. In such cases grub-install will show `source_dir doesn't exist. Please specify --target or --directory` message.

The `--no-floppy` tells `grub-bios` utilities not to search for any floppy devices which reduces the overall execution time of `grub-install` on many systems (it will also prevent the issue below from occurring). Otherwise you get an error that looks like this:

```
grub-probe: error: Cannot get the real path of '/dev/fd0'
Auto-detection of a filesystem module failed.
Please specify the module with the option '--modules' explicitly.

```

**Note:** `--no-floppy` has been removed from `grub-install` in 2.00~beta2 upstream release, and replaced with `--allow-floppy`.

**Warning:** Make sure to check the `/boot` directory if you use the latter. Sometimes the `boot-directory` parameter creates another `/boot` folder inside of `/boot`. A wrong install would look like: `/boot/boot/grub/`.

##### Install to Partition or Partitionless Disk

**Note:** `grub-bios` (any version - including upstream Bazaar repo) does not encourage installation to a partition boot sector or a partitionless disk like GRUB Legacy or syslinux does. This kind of setup is prone to breakage, especially during updates, and is not supported by Arch devs.

To set up `grub-bios` to a partition boot sector, to a partitionless disk (also called superfloppy) or to a floppy disk, run (using for example `/dev/sdaX` as the `/boot` partition):

```
# modprobe dm-mod 
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --recheck --debug --force /dev/sdaX
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
# chattr +i /boot/grub/i386-pc/core.img

```

You need to use the `--force` option to allow usage of blocklists and should not use `--grub-setup=/bin/true` (which is similar to simply generating `core.img`).

`grub-install` will give out warnings like which should give you the idea of what might go wrong with this approach:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists. 
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

Without `--force` you may get the below error and `grub-setup` will not setup its boot code in the partition boot sector:

```
/sbin/grub-setup: error: will not proceed with blocklists

```

With `--force` you should get:

```
Installation finished. No error reported.

```

The reason why `grub-setup` does not by default allow this is because in case of partition or a partitionless disk is that `grub-bios` relies on embedded blocklists in the partition bootsector to locate the `/boot/grub/i386-pc/core.img` file and the prefix dir `/boot/grub`. The sector locations of `core.img` may change whenever the filesystem in the partition is being altered (files copied, deleted etc.). For more info see [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) and [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

The workaround for this is to set the immutable flag on `/boot/grub/i386-pc/core.img` (using chattr command as mentioned above) so that the sector locations of the `core.img` file in the disk is not altered. The immutable flag on `/boot/grub/i386-pc/core.img` needs to be set only if `grub-bios` is installed to a partition boot sector or a partitionless disk, not in case of installation to MBR or simple generation of `core.img` without embedding any bootsector (mentioned above).

##### 單獨產生core.img(Generate core.img alone)

To populate the `/boot/grub` directory and generate a `/boot/grub/i386-pc/core.img` file **without** embedding any `grub-bios` bootsector code in the MBR, post-MBR region, or the partition bootsector, add `--grub-setup=/bin/true` to `grub-install`:

```
# modprobe dm-mod
# grub-install --target=i386-pc --grub-setup=/bin/true --recheck --debug /dev/sda
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

You can then chainload GRUB2's `core.img` from GRUB Legacy or syslinux as a Linux kernel or a multiboot kernel.

#### 產生GRUB2 BOIS設置檔案(Generate GRUB2 BIOS Config file)

最後產生一個GRUB2的設定檔 (this is explained in greater detail in the Configuration section):

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**注意:** 檔案路徑是 `/boot/grub/grub.cfg`, **不是** `/boot/grub/i386-pc/grub.cfg`.

如果 grub(2) 在啟動是出現 "no suitable mode found" 訊息, 前往到 [#Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error). 如果 `grub-mkconfig` 失敗了, 使用下列指令將你的 `/boot/grub/menu.lst` 轉換成 `/boot/grub/grub.cfg` :

```
# grub-menulst2cfg /boot/grub/menu.lst /boot/grub/grub.cfg

```

範例:

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

如果你忘了創建 `/boot/grub/grub.cfg` 這個GRUB2的設定檔，那麼重啟到 GRUB2 選單，按C進入命令列, 輸入:

```
sh:grub> insmod legacycfg
sh:grub> legacy_configfile ${prefix}/menu.lst

```

啟動到Archlinux且重新創建正確的 `/boot/grub/grub.cfg` 。

**注意:** 這個選項只有在 BIOS 系統管用, 在 UEFI 系統不行.

#### 在BIOS多重啟動(Multiboot in BIOS)

##### 在BIOS-MBR模式中啟動已安裝的Microsoft Windows(Boot Microsoft Windows installed in BIOS-MBR mode)

**注意:** GRUB(2) 支援直接啟動 `bootmgr`檔案和分割區啟動區的連鎖載入 (chainload of partition boot sector)，因此不需要BIOS-MBR設定來啟動Windows

**警告:** 需要注意是具有bootmgr檔案的系統分割區, 而不一定是安裝有Windows的分割區, 也就是說:當你用blkid這個指令顯示出所有UUID's，他將是有著 LABEL="SYSTEM RESERVED" 且大小約為 100 mb-200 mb，更像是Arch的 /boot 分割區. 觀看 [wikipedia:System_partition_and_boot_partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") for some more info.

找到放置著`bootmgr`的NTFS格式Windows系統分割區的UUID . 舉例來說, 如果 Windows `bootmgr` 置放在 `/media/Windows/bootmgr`:

```
# grub-probe --target=fs_uuid /media/Windows/bootmgr
69B235F6749E84CE

```

然後, 把下面的幾行敘述加到 `/etc/grub.d/40_custom` 或 `/boot/grub/custom.cfg` 接者用前述的`grub-mkconfig`產生 `grub.cfg`來啟動安裝在BIOS-MBR模式的 Windows (Vista, 7 or 8):

```
menuentry "Microsoft Windows 7 BIOS-MBR" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --no-floppy --set=root 69B235F6749E84CE
    ntldr /bootmgr
}
```

For Windows XP:

```
menuentry "Microsoft Windows XP" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --no-floppy --set=root 69B235F6749E84CE
    ntldr /ntldr
}

```

### UEFI系統(UEFI systems)

**Note:** 在閱讀這個部份前，建議先閱讀 [UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") 頁面

#### 安裝grub-uefi套件(Install grub-uefi package)

**Note:** Unless specified as EFI 1.x , EFI and UEFI terms are used interchangeably to denote UEFI 2.x firmware. Also unless stated explicitely, the instructions are general and not Mac specific. Some of them may not work or may be different in Macs. Apple's EFI implementation is neither a EFI 1.x version nor UEFI 2.x version but mixes up both. This kind of firmware does not fall under any one UEFI Specification version and is therefore not a standard UEFI firmware.

GRUB(2) UEFI bootloader is available in Arch Linux only from version 1.99~rc1\. To install, first [detect which UEFI firmware arch](/index.php/Unified_Extensible_Firmware_Interface#Detecting_UEFI_Firmware_Arch "Unified Extensible Firmware Interface") you have (either x86_64 or i386).

Depending on that, install the appropriate package

For 64-bit aka x86_64 UEFI firmware:

```
# pacman -S grub-efi-x86_64

```

For 32-bit aka i386 UEFI firmware:

```
# pacman -S grub-efi-i386

```

**Note:** Simply installing the package will not update the `core.efi` file and the GRUB(2) modules in the UEFI System Partition. You need to do this manually using `grub-install` as explained below.

#### 安裝grub-uefi啟動檔案(Install grub-uefi boot files)

##### Install to UEFI SYSTEM PARTITION

**Note:** The below commands assume you are using `grub-efi-x86_64` (for `grub-efi-i386` replace `x86_64` with `i386` in the below commands).

**Note:** To do this, you need to boot using UEFI and not the BIOS. If you booted by just copying the ISO file to the USB drive, you will need to follow [this guide](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI") or grub-install will show errors.

The UEFI system partition will need to be mounted at `/boot/efi/` for the GRUB(2) install script to detect it:

```
# mkdir -p /boot/efi
# mount -t vfat /dev/sdXY /boot/efi

```

Install GRUB UEFI application to `/boot/efi/EFI/arch_grub` and its modules to `/boot/grub/x86_64-efi` (recommended) using:

```
# modprobe dm-mod
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

**Note:** Without `--target` or `--directory` option, grub-install cannot determine for which firmware grub(2) is being installed. In such cases grub-install will show `source_dir doesn't exist. Please specify --target or --directory` message.

If you want to install grub(2) modules and `grub.cfg` at the directory `/boot/efi/EFI/grub` and the `grubx64.efi` application at `/boot/efi/EFI/arch_grub` (ie. all the grub(2) uefi files inside the UEFISYS partition itself) use:

```
# modprobe dm-mod 
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --boot-directory=/boot/efi/EFI --recheck --debug
# mkdir -p /boot/efi/EFI/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/efi/EFI/grub/locale/en.mo

```

The `--efi-directory` option mentions the mountpoint of UEFI SYSTEM PARTITION , `--bootloader-id` mentions the name of the directory used to store the `grubx64.efi` file and `--boot-directory` mentions the directory wherein the actual modules will be installed (and into which `grub.cfg` should be created).

The actual paths are:

```
<efi-directory>/<EFI or efi>/<bootloader-id>/grubx64.efi

```

```
<boot-directory>/grub/x86_64-efi/<all modules, grub.efi, core.efi, grub.cfg>

```

**Note:** the `--bootloader-id` option does not change `<boot-directory>/grub`, i.e. you cannot install the modules to `<boot-directory>/<bootloader-id>`, the path is hard-coded to be `<boot-directory>/grub`.

In `--efi-directory=/boot/efi --boot-directory=/boot/efi/EFI --bootloader-id=grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == <boot-directory>/grub == /boot/efi/EFI/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot/efi/EFI --bootloader-id=arch_grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/arch_grub
<boot-directory>/grub == /boot/efi/EFI/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot --bootloader-id=arch_grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/arch_grub
<boot-directory>/grub == /boot/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot --bootloader-id=grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/grub
<boot-directory>/grub == /boot/grub

```

The `<efi-directory>/<EFI or efi>/<bootloader-id>/grubx64.efi` is an exact copy of `<boot-directory>/grub/x86_64-efi/core.efi`.

**Note:** In GRUB2 2.00~beta4, the `grub-install` option `--efi-directory` replaces `--root-directory` and the latter is deprecated.

**Note:** The options `--efi-directory` and `--bootloader-id` are specific to GRUB(2) UEFI.

In all the cases the UEFI SYSTEM PARTITION should be mounted for `grub-install` to install `grubx64.efi` in it, which will be launched by the firmware (using the `efibootmgr` created boot entry in non-Mac systems).

If you notice carefully, there is no <device_path> option (Eg: `/dev/sda`) at the end of the `grub-install` command unlike the case of setting up GRUB(2) for BIOS systems. Any <device_path> provided will be ignored by the install script as UEFI bootloaders do not use MBR or Partition boot sectors at all.

You may now be able to UEFI boot your system by creating a `grub.cfg` file by following [#Generate_GRUB2_UEFI_Config_file](#Generate_GRUB2_UEFI_Config_file) and [#Create GRUB2 entry in the Firmware Boot Manager](#Create_GRUB2_entry_in_the_Firmware_Boot_Manager).

#### Create GRUB2 entry in the Firmware Boot Manager

##### Non-Mac UEFI systems

`grub-install` will ensure that `/boot/efi/EFI/arch_grub/grubx64.efi` is launched by default if it detects `efibootmgr` and if it is able to access UEFI Runtime Services. Follow [Unified Extensible Firmware Interface#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface#efibootmgr "Unified Extensible Firmware Interface") for more info.(Before trying these steps, be sure to create a grub.cfg ([Grub2#Generate_GRUB2_UEFI_Config_file](/index.php/Grub2#Generate_GRUB2_UEFI_Config_file "Grub2")) because you will need it to boot into Arch after grub is loaded)

If you have problems running GRUB2 in UEFI mode you can try the following (worked on an ASUS Z68 mainboard):

```
# cp /boot/efi/EFI/arch_grub/grubx64.efi /boot/efi/shellx64.efi

```

or

```
# cp /boot/efi/EFI/arch_grub/grubx64.efi /boot/efi/EFI/shellx64.efi

```

or

```
# cp /boot/efi/EFI/arch_grub/grubx64.efi /boot/efi/EFI/tools/shellx64.efi

```

After this launch the UEFI Shell from the UEFI setup/menu (in ASUS UEFI BIOS, switch to advanced mode, press Exit in the top right corner and choose "Launch EFI shell from filesystem device"). The GRUB2 menu will show up and you can boot into your system. Afterwards you can use efibootmgr to setup a menu entry (see above).

If your motherboard has no such option (or even if it does), you can use UEFI shell ([Unified Extensible Firmware Interface#UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface")) to create a UEFI boot option for the Arch partition temporarily.

Once you boot into the EFI shell, add a UEFI boot menu entry:

```
Shell> bcfg boot add 0 fs1:\EFI\arch_grub\grubx64.efi "Arch Linux (GRUB2)"

```

where `fs1` is the mapping corresponding to the UEFI System Partition and `\EFI\arch_grub\grubx64.efi` is the the from the `--bootloader-id` from the `grub-install` command above.

This will temporarily add a UEFI boot option for the next boot to get into Arch.

Once in Arch, modprobe `efivars` and confirm that `efibootmgr` creates no errors (no errors meaning you successfully booted in UEFI mode).

Then [Grub2#Install_to_UEFI_SYSTEM_PARTITION](/index.php/Grub2#Install_to_UEFI_SYSTEM_PARTITION "Grub2") can be performed again and should successfully permanently add a boot entry in the UEFI menu.

##### Apple Mac EFI systems

**Note:** TODO: GRUB upstream Bazaar mactel branch [http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes](http://bzr.savannah.gnu.org/lh/grub/branches/mactel/changes). No further update from grub developers.

**Note:** TODO: Experimental "bless" utility for Linux by Fedora developers - [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/). Requires more testing.

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

#### 產生GRUB2 UEFI設置檔案(Generate GRUB2 UEFI Config file)

Finally, generate a configuration for GRUB(2) (this is explained in greater detail in the Configuration section):

```
# grub-mkconfig -o <boot-directory>/grub/grub.cfg

```

**Note:** The file path is `<boot-directory>/grub/grub.cfg`, NOT `<boot-directory>/grub/x86_64-efi/grub.cfg`.

If you used `--boot-directory=/boot`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

If you used `--boot-directory=/boot/efi/EFI`:

```
# grub-mkconfig -o /boot/efi/EFI/grub/grub.cfg

```

This is independent of the value of `--bootloader-id` option.

If GRUB2 complains about "no suitable mode found" while booting, try [#Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error).

#### Create GRUB2 Standalone UEFI Application

It is possible to create a `grubx64_standalone.efi` application which has all the modules embeddded in a memdisk within the uefi application, thus removing the need for having a separate directory populated with all the GRUB2 uefi modules and other related files. This is done using the `grub-mkstandalone` command which is included in [grub-common](https://www.archlinux.org/packages/?name=grub-common) >= 1:1.99-6 package.

The easiest way to do this would be with the install command already mentioned before, but specifying the modules to include. For example:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/EFI/arch_grub/grubx64_standalone.efi" <any extra files you want to include>

```

The `grubx64_standalone.efi` file expects `grub.cfg` to be within its $prefix which is `(memdisk)/boot/grub`. The memdisk is embedded within the efi app. The `grub-mkstandlone` script allow passing files to be included in the memdisk image to be as the arguments to the script (in <any extra files you want to include>).

If you have the `grub.cfg` at `/home/user/Desktop/grub.cfg`, then create a temporary `/home/user/Desktop/boot/grub/` directory, copy the `/home/user/Desktop/grub.cfg` to `/home/user/Desktop/boot/grub/grub.cfg`, cd into `/home/user/Desktop/boot/grub/` and run:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/EFI/arch_grub/grubx64_standalone.efi" "boot/grub/grub.cfg"

```

The reason to cd into `/home/user/Desktop/boot/grub/` and to pass the file path as `boot/grub/grub.cfg` (notice the lack of a leading slash - boot/ vs /boot/ ) is because `dir1/dir2/file` is included as `(memdisk)/dir1/dir2/file` by the `grub-mkstandalone` script.

If you pass `/home/user/Desktop/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/grub.cfg`. If you pass `/home/user/Desktop/boot/grub/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/boot/grub/grub.cfg`. That is the reason for cd'ing into `/home/user/Desktop/boot/grub/` and passing `boot/grub/grub.cfg`, to include the file as `(memdisk)/boot/grub/grub.cfg`, which is what `grub.efi` expects the file to be.

You need to create an UEFI Boot Manager entry for `/boot/efi/EFI/arch_grub/grubx64_standalone.efi` using `efibootmgr`. Follow [#Create GRUB2 entry in the Firmware Boot Manager](#Create_GRUB2_entry_in_the_Firmware_Boot_Manager).

#### Multiboot in UEFI

##### Chainload Microsoft Windows x86_64 UEFI-GPT

Find the UUID of the FAT32 filesystem in the UEFI SYSTEM PARTITION where the Windows UEFI Bootloader files reside. For example, if Windows `bootmgfw.efi` exists at `/boot/efi/EFI/Microsoft/Boot/bootmgfw.efi` (ignore the upper-lower case differences since that is immaterial in FAT filesystem):

```
# grub-probe --target=fs_uuid /boot/efi/EFI/Microsoft/Boot/bootmgfw.efi
1ce5-7f28

```

```
# grub-probe --target=hints_string /boot/efi/EFI/Microsoft/Boot/bootmgfw.efi
--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1

```

Then, add this code to `/boot/grub/grub.cfg` OR `/boot/efi/EFI/grub/grub.cfg` to chainload Windows x86_64 (Vista SP1+, 7 or 8) installed in UEFI-GPT mode:

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

## 設置(Configuration)

你可以選擇自動產生或手動編輯 `grub.cfg`.

**注意:** 對 EFI 系統, 如果 GRUB2 是以 `--boot-directory` 參數安裝, `grub.cfg` 檔案將被放在跟 `grubx64.efi`相同的路徑. 否則, `grub.cfg` 這檔案將會放在 `/boot/grub/`, 這點跟 GRUB2的BIOS版本是一樣的.

**注意:** 這裡對於如何配置GRUB2有相當完整的敘述: [http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html)

### 使用grub-mkconfig自動產生(Automatically generating using grub-mkconfig) (Recommended)

在 GRUB2中`/etc/default/grub` 和 `/etc/grub.d/*`，與舊版的GRUB的 `menu.lst` 有相似的設置效果， `grub-mkconfig` 預設利用這些檔案產生標準的`grub.cfg`輸出. 產生 `grub.cfg` 檔案可以執行指令:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

`/etc/grub.d/10_linux` is set to automatically add menu items for Arch linux that work out of the box, to any generated configuration. 其他的作業系統也許需要手動配置到 `/etc/grub.d/40_custom` 或 `/boot/grub/custom.cfg`

#### Additional arguments

To pass custom additional arguments to the Linux image, you can set the `GRUB_CMDLINE_LINUX` variable in `/etc/default/grub`. This is analogous to adding commands to the kernel line in GRUB Legacy.

For example, use `GRUB_CMDLINE_LINUX="resume=/dev/sdaX"` where `sda**X**` is your swap partition to enable resume after hibernation.

You can also use `GRUB_CMDLINE_LINUX="resume=/dev/disk/by-uuid/${swap_uuid}"`, where `${swap_uuid}` is the [UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") of your swap partition.

Users who have replaced the default SysV init with [systemd](/index.php/Systemd "Systemd") will want to add `init=/bin/systemd` to their `GRUB_CMDLINE_LINUX`.

Multiple entries are separated by spaces within the double quotes. So, for users who want both resume and systemd it would look like this: `GRUB_CMDLINE_LINUX="resume=/dev/sdaX init=/bin/systemd"`

### 手動創建grub.cfg( Manually creating grub.cfg)

**警告:** 直接對這個檔案進行編輯是不建議的事.這個檔案是用 `grub-mkconfig` 產生,所以最好是編輯你的 `/etc/default/grub` 或其他在 `/etc/grub.d` 資料夾的script.

一個基本的 GRUB 設置檔使用下列的選項

*   `(hdX,Y)` 意味在硬碟`X`中的分割區 `Y` , 分割區的編號從1開始，硬碟編號從0開始。
*   `set default=N` is the default boot entry that is chosen after timeout for user action
*   `set timeout=M` 意謂用 `M`秒鐘的時間等待使用者動作，否則啟動預設選項。
*   `menuentry "title" {entry options}` 是啟動項目名稱 `title`
*   `set root=(hdX,Y)` 設置啟動分割區, 此分割區應有核心和GRUB模組 (boot need not be a separate partition, and may simply be a directory under the "root" partition (`/`)

一個設置範例:

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

### 雙啟動(dual-boot)

*注意: 如果你希望 GRUB2 自動尋找其他的作業系統(舉例來說，像是ubuntu).那麼你可能需要從[AUR](/index.php/AUR "AUR")下載並安裝 [os-prober](https://www.archlinux.org/packages/?name=os-prober)*

#### 使用 grub-mkconfig

想增加其他啟動項目，最好的方法是編輯 `/etc/grub.d/40_custom`或{ic|/boot/grub/custom.cfg}} . 如此一來，項目將在你執行 **grub-mkconfig**後自動加入。 加入新的內容,執行

```
# grub-mkconfig -o /boot/grub/grub.cfg 

```

以產生一個新的 `grub.cfg`和grub選單。

##### 與 GNU/Linux

假設其他的 distro 在分割區 `sda2`:

```
menuentry "Other Linux" {
set root=(hd0,2)
linux /boot/vmlinuz (add other options here as required)
initrd /boot/initrd.img (if the other kernel uses/needs one)
}

```

##### 與 FreeBSD

Requires that FreeBSD is installed on a single partition with UFS. 假如安裝在`sda4`:

```
menuentry "FreeBSD" {
set root=(hd0,4)
chainloader +1
}

```

##### 與 Windows

假設你的 Windows 分割區是 `sda3`Remember you need to point set root and chainloader to the system reserve partition that windows made when it installed, not the actual partition windows is on..在{{ic|/etc/grub.d/40_custom})加入

```
# (2) Windows XP
menuentry "Windows XP" {
    set root=(hd0,3)
    chainloader (hd0,3)+1
}

```

執行

```
# grub-mkconfig -o /boot/grub/grub.cfg 

```

以產生一個新的 `grub.cfg`和grub選單。

If the Windows bootloader is on an entirely different hard drive than GRUB, it may be necessary to trick Windows into believing that it is the first hard drive. This was possible in GRUB Legacy with `map` and is now done with `drivemap`. Assuming GRUB is on `hd0` and Windows is on `hd2`, you need to add the following after `set root`:

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
kernel      /boot/grub/i386-pc/core.img

```

### Visual Configuration

In GRUB2 it is possible, by default, to change the look of the menu. Make sure to initialize, if not done already, GRUB2 graphical terminal, gfxterm, with proper video mode, gfxmode, in GRUB2\. This can be seen in the section [#Correct GRUB2 No Suitable Mode Found Error](#Correct_GRUB2_No_Suitable_Mode_Found_Error). This video mode is passed by GRUB2 to the linux kernel via 'gfxpayload' so any visual configurations need this mode in order to be in effect.

#### Setting the framebuffer resolution

GRUB2 can set the framebuffer for both GRUB2 itself and the kernel. The old `vga=` way is deprecated. The preferred method is editing `/etc/default/grub` as the following sample:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

套用改變, 執行:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

The `gfxpayload` property will make sure the kernel keeps the resolution.

**注意:** 如果這個例子對你以`vbemode="0x105"`置換`gfxmode="1024x768x32"`沒有成功. Remember to replace the specified resolution with one suitable for your screen.

**注意:** 你可以使用 `# hwinfo --framebuffer`來顯示出所有的模式 (hwinfo is available in [community]), while at GRUB2 prompt you can use the `vbeinfo` command.

If this method does not work for you, the deprecated `vga=` method will still work. Just add it next to the `"GRUB_CMDLINE_LINUX_DEFAULT="` line in `/etc/default/grub` for eg: `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` will give you a `1024x768` resolution.

You can choose one of these resolutions: `640×480`, `800×600`, `1024×768`, `1280×1024`,`1600×1200`, `1920×1200`

#### 915resolution hack

Some times for Intel graphic adapters neither `# hwinfo --framebuffer` nor `vbeinfo` will show you the desired resolution. In this case you can use `915resolution` hack. This hack will temporarily modify video BIOS and add needed resolution. See [915resolution's home page](http://915resolution.mango-lang.org/)

In the following I will proceed with the example for my system. Please adjust the recipe for your needs. First you need to find a video mode which will be modified later. For that, run `915resolution` in GRUB2 command shell:

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

Next, our purpose is to overwrite mode 30\. (You can choose what ever mode you want.) In the file `/etc/grub.d/00_header` just before the `set gfxmode=${GRUB_GFXMODE`} line insert:

```
915resolution 30 1440 900

```

Here we are overwriting the mode `30` with `1440x900` resolution. Lastly we need to set `GRUB_GFXMODE` as described earlier, regenerate GRUB2 configuration file and reboot to test changes:

```
# grub-mkconfig -o /boot/grub/grub.cfg
# reboot

```

#### 背景圖片和字體(Background image and bitmap fonts)

GRUB2 comes with support for background images and bitmap fonts in `pf2` format. The unifont font is included in the [grub-common](https://www.archlinux.org/packages/?name=grub-common) package under the filename `unicode.pf2`, or, as only ASCII characters under the name `ascii.pf2`.

圖像支援格式有 tga, png and jpeg. 解析度最大支援取決於您的硬體.

Make sure you have set up the proper [framebuffer resolution](/index.php/GRUB2#Setting_the_framebuffer_resolution "GRUB2").

編輯 `/etc/default/grub` :

```
GRUB_BACKGROUND="/boot/grub/myimage"
#GRUB_THEME="/path/to/gfxtheme"
GRUB_FONT="/path/to/font.pf2"

```

**注意:** 如果你將GRUB裝在分開的分割區, `/boot/grub/myimage` 會變成 `/grub/myimage`.

套用改變且將新資訊加到 `grub.cfg`, 執行:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

如果成功加入背景圖, 使用者將在終端機看到 `"Found background image..."` . 如果沒看到這段敘述, 圖像資訊可能沒有成功加到 `grub.cfg` 裡.

如果圖片沒有顯示, 進行確認:

*   在 `/etc/default/grub`的圖片路徑跟檔名都是正確的.
*   圖片的格式跟大小是正確的 (tga, png, 8-bit jpg).
*   The image was saved in the RGB mode, and is not indexed.
*   console mode 沒有啟用在 `/etc/default/grub`裡.
*   `grub-mkconfig` 確實執行並將背景圖片資訊放到 `/boot/grub/grub.cfg` 裡.

#### 佈景主題(Theme)

Here is an example for configuring Starfield theme which was included in GRUB2 package.

Edit `/etc/default/grub`

```
GRUB_THEME="/usr/share/grub/themes/starfield/theme.txt"

```

Generate the changes:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

如果主題設定成功, 您將會在終端機看到 `Found theme: /usr/share/grub/themes/starfield/theme.txt` 使用主題時，你原先設定的 splash image 將不會被顯示出來

#### 選單顏色(Menu colors)

如同 GRUB 舊版 (0.9x), 在 GRUB2你可以更改選單顏色. 目前可用的顏色 GRUB2 參照 [https://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html#Theme-file-format](https://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html#Theme-file-format). 這裡有個範例:

編輯 `/etc/default/grub`:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

套用變更:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

#### 隱藏選單(Hidden menu)

One of the unique features of GRUB2 is hiding/skipping the menu and showing it by holding `Esc` when needed. You can also adjust whether you want to see the timeout counter.

Edit `/etc/default/grub` as you wish. Here is an example where the comments from the beginning of the two lines have been removed to enable the feature, the timeout has been set to five seconds and to be shown to the user:

```
GRUB_HIDDEN_TIMEOUT=5
GRUB_HIDDEN_TIMEOUT_QUIET=false

```

接者執行:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

#### 關閉幀緩衝(Disable framebuffer)

Users who use NVIDIA proprietary driver might wish to disable GRUB2's framebuffer as it can cause problems with the binary driver.

要關閉幀緩衝, 編輯 `/etc/default/grub` 並將下行取消註解:

```
GRUB_TERMINAL_OUTPUT=console

```

接著執行:

```
grub-mkconfig -o /boot/grub/grub.cfg

```

### 其他選項(Other Options)

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

#### RAID

GRUB2 provides convenient handling of RAID volumes. You need to add `insmod raid` which allows you to address the volume natively. For example, `/dev/md0` becomes:

```
set root=(md0)

```

whereas a partitioned RAID volume (e.g. `/dev/md0p1`) becomes:

```
set root=(md0,1)

```

#### Persistent block device naming

You can use UUIDs to detect partitions instead of the "old" `/dev/sd*` and `/dev/hd*` scheming. It has the advantage of detecting partitions by their unique UUIDs, which is needed by some people booting with complicated partition setups.

UUIDs are used by default in the recent versions of GRUB2 - there is no downside in it anyway except that you need to re-generate the `grub.cfg` file every time you resize or reformat your partitions. Remember this when modifying partitions with Live-CD.

Recent versions of GRUB2 use UUIDs by default. You can enable the use of UUIDs by simply commenting the UUID line (which is the default):

```
#GRUB_DISABLE_LINUX_UUID=true

```

Or you can uncomment it and set the value to `false`:

```
GRUB_DISABLE_LINUX_UUID=false

```

Either way, do not forget to generate the changes:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

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

GRUB2 can remember the last entry you booted from and use this as the default entry to boot from next time. This is useful if you have multiple kernels (i.e., the current Arch one and the LTS kernel as a fallback option) or operating systems. To do this, edit `/etc/default/grub` and change the setting of `GRUB_DEFAULT`:

```
GRUB_DEFAULT=saved

```

This ensures that GRUB will default to the saved entry. To enable saving the selected entry, add the following line to `/etc/default/grub`:

```
GRUB_SAVEDEFAULT=true

```

**Note:** Manually added menu items, eg Windows in `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg` , will need `savedefault` added. Remember to regenerate your configuration file.

#### 安全(Security)

如果你想增加 GRUB2的安全性，使其他人不能改變啟動參數跟使用命令列,你可以加上一個 user/password 組合到 GRUB2的設置檔案. 如果像這樣做的話, 執行指令 `grub-mkpasswd-pbkdf2`. 輸入密碼且確認它. 螢幕輸入將會像是這樣:

 `Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A` Then, add the following to `/etc/grub.d/00_header`:
```
cat << EOF

set superusers="username"
password_pbkdf2 username <password>

EOF
```

這裡的 `<password>` 是由 `grub-mkpasswd_pbkdf2`產生的字串.

再次產生你的設置檔案， 您的 GRUB2 命令列, 啟動參數和所有的啟動項目都將被保護。

This can be relaxed and further customized with more users as described in the "Security" part of [the GRUB manual](https://www.gnu.org/software/grub/manual/grub.html#Security).

#### Root Encryption

To let GRUB2 automatically add the kernel parameters for root encryption, add `cryptdevice=/dev/yourdevice:label` to `GRUB_CMDLINE_LINUX` in `/etc/default/grub`.

Example with root mapped to `/dev/mapper/root`:

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:root"

```

Also, disable the usage of UUIDs for the rootfs:

```
GRUB_DISABLE_LINUX_UUID=true

```

Regenerate the configuration.

### 在GRUB2啟動(ISOBooting an ISO Directly From GRUB2)

編輯 `/etc/grub.d/40_custom` 或 `/boot/grub/custom.cfg` 為目標ISO增加項目。完成後`grub-mkconfig -o /boot/grub/grub.cfg` (as root)更新選單。

#### Arch ISO

**注意:** 一定要調整第3行的 `hdX,Y` ，才能指向ISO檔正確所在的硬碟/分割區。 同時調整 `img_dev` 行來對應到相同的位置。 像是, 如果電腦裡已有一個內置硬碟，此時想從隨身碟開啟ISO檔，那麼用`sdbY`取代 `sdaY`.

```
menuentry "Archlinux-2011.08.19-netinstall-x86_64.iso" {
    set isofile="/archives/archlinux-2011.08.19-netinstall-x86_64.iso"
    loopback loop (hd0,7)$isofile
    linux (loop)/arch/boot/x86_64/vmlinuz archisolabel=ARCH_201108 img_dev=/dev/sda7 img_loop=$isofile earlymodules=loop
    initrd (loop)/arch/boot/x86_64/archiso.img
}

```

```
menuentry "Archlinux-2012.07.15-netinstall-dual.iso" {
    set isofile="/archives/archlinux-2012.07.15-netinstall-dual.iso"
    loopback loop (hd0,7)$isofile
    linux (loop)/arch/boot/x86_64/vmlinuz archisolabel=ARCH_201207 img_dev=/dev/sda7 img_loop=$isofile
    initrd (loop)/arch/boot/x86_64/archiso.img
}

```

**Tip:** For thumbdrives, use [Persistent block device names](/index.php/Persistent_block_device_naming "Persistent block device naming") for the "img_dev" kernel parameter. **Ex:** img_dev=/dev/disk/by-label/CORSAIR

#### Ubuntu ISO

**注意:** 一定要調整第3行的 `hdX,Y` ，才能指向ISO檔正確所在的硬碟/分割區。 同時調整 `img_dev` 行來對應到相同的位置。

```
menuentry "ubuntu-12.04-desktop-amd64.iso" {
    set isofile="/path/to/ubuntu-12.04-desktop-amd64.iso"
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
grub rescue> insmod (hdX,Y)/boot/grub/i386-pc/normal.mod
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

If you have a Windows 9x paradigm with hidden C:\ disks GRUB Legacy had the hide/unhide feature. In GRUB2 this has been replaced by `parttool`. For example, to boot the third C:\ disk of three Windows 9x installations on the CLI enter the CLI and:

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

The available commands in GRUB rescue include `insmod`, `ls`, `set`, and `unset`. This example uses `set` and `insmod`. `set` modifies variables and `insmod` inserts new modules to add functionality.

Before starting, the user must know the location of their `/boot` partition (be it a separate partition, or a subdirectory under their root):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

where X is the physical drive number and Y is the partition number.

To expand console capabilities, insert the `linux` module:

```
grub rescue> insmod (hdX,Y)/boot/grub/linux.mod

```

**Note:** With a separate boot partition, omit `/boot` from the path, (i.e. type `set prefix=(hdX,Y)/grub` and `insmod (hdX,Y)/grub/linux.mod`).

This introduces the `linux` and `initrd` commands, which should be familiar (see [#Configuration](#Configuration)).

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

After successfully booting the Arch Linux installation, users can correct `grub.cfg` as needed and then reinstall GRUB2.

to reinstall GRUB2 and fix the problem completely, changing `/dev/sda` if needed. See [#Bootloader installation](#Bootloader_installation) for details.

## Combining the use of UUIDs and basic scripting

If you like the idea of using UUIDs to avoid unreliable BIOS mappings or are struggling with GRUB's syntax, here is an example boot menu item that uses UUIDs and a small script to direct GRUB to the proper disk partitions for your system. All you need to do is replace the UUIDs in the sample with the correct UUIDs for your system. The example applies to a system with a boot and root partition. You will obviously need to modify the GRUB configuration if you have additional partitions:

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

## 疑難排解(Troubleshooting)

Any troubleshooting should be added here.

### Enable GRUB2 debug messages

Add:

```
set pager=1
set debug=all

```

to `grub.cfg`.

### Correct GRUB2 No Suitable Mode Found Error

If you get this error when booting any menuentry:

```
error: no suitable mode found
Booting however

```

Then you need to initialize GRUB2 graphical terminal (`gfxterm`) with proper video mode (`gfxmode`) in GRUB2\. This video mode is passed by GRUB2 to the linux kernel via 'gfxpayload'. In case of UEFI systems, if the GRUB2 video mode is not initialized, no kernel boot messages will be shown in the terminal (atleast until KMS kicks in).

Copy `/usr/share/grub/unicode.pf2` to ${GRUB2_PREFIX_DIR} (`/boot/grub/` in case of BIOS and UEFI systems). If GRUB2 UEFI was installed with `--boot-directory=/boot/efi/EFI` set, then the directory is `/boot/efi/EFI/grub/`:

```
# cp /usr/share/grub/unicode.pf2 ${GRUB2_PREFIX_DIR}

```

If `/usr/share/grub/unicode.pf2` does not exist, install [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont), create the `unifont.pf2` file and then copy it to `${GRUB2_PREFIX_DIR}`:

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

Then, in the `grub.cfg` file, add the following lines to enable GRUB2 to pass the video mode correctly to the kernel, without of which you will only get a black screen (no output) but booting (actually) proceeds successfully without any system hang.

BIOS systems:

```
insmod vbe

```

UEFI systems:

```
insmod efi_gop
insmod efi_uga

```

After that add the following code (common to both BIOS and UEFI):

```
insmod font

```

```
if loadfont ${prefix}/fonts/unicode.pf2
then
    insmod gfxterm
    set gfxmode=auto
    set gfxpayload=keep
    terminal_output gfxterm
fi

```

As you can see for gfxterm (graphical terminal) to function properly, `unicode.pf2` font file should exist in `${GRUB2_PREFIX_DIR}`.

### msdos-style error message

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding won't be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

This error may occur when you try installing GRUB2 in a VMware container. Read more about it [here](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). It happens when the first partition starts just after the MBR (block 63), without the usual space of 1 MiB (2048 blocks) before the first partition. Read [#MBR aka msdos partitioning specific instructions](#MBR_aka_msdos_partitioning_specific_instructions)

### UEFI GRUB2 drops to shell

If GRUB loads but drops you into the rescue shell with no errors, it may be because of a missing or misplaced `grub.cfg`. This will happen if GRUB2 UEFI was installed with `--boot-directory` and `grub.cfg` is missing OR if the partition number of the boot partition changed (which is hard-coded into the `grubx64.efi` file).

### UEFI GRUB2 not loaded

In some cases the EFI may fail to load GRUB correctly. Provided everything is set up correctly, the output of:

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

If everything works correctly, the EFI would now automatically load GRUB.

If the screen only goes black for a second and the next boot option is tried afterwards, according to [this post](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), moving GRUB to the partition root can help. The boot option has to be deleted and recreated afterwards. The entry for GRUB should look like this then:

```
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

### Invalid signature

If trying to boot Windows results in an "invalid signature" error, e.g. after reconfiguring partitions or adding additional hard drives, (re)move GRUB's device configuration and let it reconfigure:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig` should now mention all found boot options, including Windows. If it works, remove `/boot/grub/device.map-old`.

### Restore GRUB Legacy

*   將 GRUB2 檔案先移除:

```
# mv /boot/grub /boot/grub.nonfunctional

```

*   把舊版GRUB( GRUB Legacy )放回 `/boot`:

```
# cp -af /boot/grub-legacy /boot/grub

```

*   將sda的MBR加上後面62個sectors的區塊用備份好的資料取代

**注意:** 這指令同時也回存舊的分割區對應表(partition table)，這可能會弄亂你的系統

```
# dd if=/path/to/backup/first-sectors of=/dev/sdX bs=512 count=1

```

比較安全的方法是僅回存MBR的啟動碼:

```
# dd if=/path/to/backup/mbr-boot-code of=/dev/sdX bs=446 count=1

```

## 參考資料(References)

1.  Official GRUB2 Manual - [https://www.gnu.org/software/grub/manual/grub.html](https://www.gnu.org/software/grub/manual/grub.html)
2.  Ubuntu wiki page for GRUB2 - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
3.  GRUB2 wiki page describing steps to compile for UEFI systems - [https://help.ubuntu.com/community/UEFIBooting](https://help.ubuntu.com/community/UEFIBooting)
4.  Wikipedia's page on [BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")

## 外部連結(External Links)

1.  [A Linux Bash Shell script to compile and install GRUB(2) for BIOS from BZR Source](https://github.com/the-ridikulus-rat/My_Shell_Scripts/blob/master/grub/grub_bios.sh)
2.  [A Linux Bash Shell script to compile and install GRUB(2) for UEFI from BZR Source](https://github.com/the-ridikulus-rat/My_Shell_Scripts/blob/master/grub/grub_uefi.sh)