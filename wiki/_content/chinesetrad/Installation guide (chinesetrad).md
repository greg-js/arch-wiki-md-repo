**翻譯狀態：** 本文章是 [Installation_guide](/index.php/Installation_guide "Installation guide") 的翻譯版本。最近一次的翻譯時間：2018-09-19。點擊[本連結](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid={{{3}}})查看英文頁面之後的變更。

This document is a guide for installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") from the live system booted with the official installation image. Before installing, it would be advised to view the [FAQ](/index.php/FAQ "FAQ"). For conventions used in this document, see [Help:Reading](/index.php/Help:Reading "Help:Reading"). In particular, code examples may contain placeholders (formatted in `*italics*`) that must be replaced manually.

此文件是個引導你透過官方安裝映像的 Live 系統安裝 [Arch Linux](/index.php/Arch_Linux "Arch Linux") 的教學。在安裝前，建議先閱讀 [FAQ](/index.php/FAQ "FAQ")。關於此文件使用的慣例，請閱讀 [Help:Reading](/index.php/Help:Reading "Help:Reading")。一些情況下，範例程式碼可能包含佔位符（以 `*italics*` 格式化），其需要手動替換。

For more detailed instructions, see the respective [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") articles or the various programs' [man pages](/index.php/Man_page "Man page"), both linked from this guide. For interactive help, the [IRC channel](/index.php/IRC_channel "IRC channel") and the [forums](https://bbs.archlinux.org/) are also available.

更詳細的資源，可以參考 [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") 文章，或者閱讀該命令的 [man page](/index.php/Man_page "Man page")。如需要互動式幫助，可透過 [IRC channel](/index.php/IRC_channel "IRC channel") 及 [forums](https://bbs.archlinux.org/)。

Arch Linux should run on any [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64")-compatible machine with a minimum of 512 MB RAM. A basic installation with all packages from the [base](https://www.archlinux.org/groups/x86_64/base/) group should take less than 800 MB of disk space. As the installation process needs to retrieve packages from a remote repository, this guide assumes a working internet connection is available.

Arch Linux 可在任何 RAM 不小於 512MB 的 [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") 相容機上運行。用 [base](https://www.archlinux.org/groups/x86_64/base/) 套件組內的所有套件進行基本安裝將占用小於 800MB 的硬碟空間。由於安裝過程中需要從遠程存儲庫獲取軟件包，機器需要連結到網際網路。

## Contents

*   [1 Pre-installation 安裝前的準備](#Pre-installation_.E5.AE.89.E8.A3.9D.E5.89.8D.E7.9A.84.E6.BA.96.E5.82.99)
    *   [1.1 Set the keyboard layout 設置鍵盤配置](#Set_the_keyboard_layout_.E8.A8.AD.E7.BD.AE.E9.8D.B5.E7.9B.A4.E9.85.8D.E7.BD.AE)
    *   [1.2 Verify the boot mode 確認啟動模式（待翻譯）](#Verify_the_boot_mode_.E7.A2.BA.E8.AA.8D.E5.95.9F.E5.8B.95.E6.A8.A1.E5.BC.8F.EF.BC.88.E5.BE.85.E7.BF.BB.E8.AD.AF.EF.BC.89)
    *   [1.3 Connect to the Internet 連接到網際網路（待翻譯）](#Connect_to_the_Internet_.E9.80.A3.E6.8E.A5.E5.88.B0.E7.B6.B2.E9.9A.9B.E7.B6.B2.E8.B7.AF.EF.BC.88.E5.BE.85.E7.BF.BB.E8.AD.AF.EF.BC.89)
    *   [1.4 Update the system clock 更新系統時間](#Update_the_system_clock_.E6.9B.B4.E6.96.B0.E7.B3.BB.E7.B5.B1.E6.99.82.E9.96.93)
    *   [1.5 Partition the disks 分割硬碟（待翻譯）](#Partition_the_disks_.E5.88.86.E5.89.B2.E7.A1.AC.E7.A2.9F.EF.BC.88.E5.BE.85.E7.BF.BB.E8.AD.AF.EF.BC.89)
    *   [1.6 Format the partitions 格式化分割](#Format_the_partitions_.E6.A0.BC.E5.BC.8F.E5.8C.96.E5.88.86.E5.89.B2)
    *   [1.7 Mount the file systems 掛載檔案系統](#Mount_the_file_systems_.E6.8E.9B.E8.BC.89.E6.AA.94.E6.A1.88.E7.B3.BB.E7.B5.B1)
*   [2 Installation 安裝](#Installation_.E5.AE.89.E8.A3.9D)
    *   [2.1 Select the mirrors 選擇鏡像站（待翻譯）](#Select_the_mirrors_.E9.81.B8.E6.93.87.E9.8F.A1.E5.83.8F.E7.AB.99.EF.BC.88.E5.BE.85.E7.BF.BB.E8.AD.AF.EF.BC.89)
    *   [2.2 Install the base packages 安裝系統基本套件](#Install_the_base_packages_.E5.AE.89.E8.A3.9D.E7.B3.BB.E7.B5.B1.E5.9F.BA.E6.9C.AC.E5.A5.97.E4.BB.B6)
*   [3 Configure the system 系統設置](#Configure_the_system_.E7.B3.BB.E7.B5.B1.E8.A8.AD.E7.BD.AE)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone 時區](#Time_zone_.E6.99.82.E5.8D.80)
    *   [3.4 Localization 語言環境](#Localization_.E8.AA.9E.E8.A8.80.E7.92.B0.E5.A2.83)
    *   [3.5 Network configuration 網路設置](#Network_configuration_.E7.B6.B2.E8.B7.AF.E8.A8.AD.E7.BD.AE)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root password Root 密碼](#Root_password_Root_.E5.AF.86.E7.A2.BC)
    *   [3.8 Boot loader 開機引導程式](#Boot_loader_.E9.96.8B.E6.A9.9F.E5.BC.95.E5.B0.8E.E7.A8.8B.E5.BC.8F)
*   [4 Reboot 重新啟動](#Reboot_.E9.87.8D.E6.96.B0.E5.95.9F.E5.8B.95)
*   [5 Post-installation 安裝後](#Post-installation_.E5.AE.89.E8.A3.9D.E5.BE.8C)

## Pre-installation 安裝前的準備

Download and boot the installation medium as explained in [Getting and installing Arch](/index.php/Getting_and_installing_Arch "Getting and installing Arch"). You will be logged in on the first [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") as the root user, and presented with a [Zsh](/index.php/Zsh "Zsh") shell prompt.

根據 [Getting and installing Arch](/index.php/Getting_and_installing_Arch "Getting and installing Arch") 中所述，下載並引導安裝媒介。啟動完成後將會自動以 root 身份登錄虛擬控制台（[virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console")）並進入 [Zsh](/index.php/Zsh "Zsh") 命令解譯器。

To switch to a different console—for example, to view this guide with [ELinks](/index.php/ELinks "ELinks") alongside the installation—use the `Alt+*arrow*` [shortcut](/index.php/Keyboard_shortcuts "Keyboard shortcuts"). To [edit](/index.php/Textedit "Textedit") configuration files, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") and [vim](/index.php/Vim#Usage "Vim") are available.

欲切換至其它的虛擬終端，例如使用 [ELinks](/index.php/ELinks "ELinks") 來查看本篇指南，使用 `Alt+*arrow*` 快捷鍵（[shortcut](/index.php/Keyboard_shortcuts "Keyboard shortcuts")）。可使用 [nano](/index.php/Nano#Usage "Nano")，[vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") 或 [vim](/index.php/Vim#Usage "Vim") 來編輯（[edit](/index.php/Textedit "Textedit")）配置文件。

### Set the keyboard layout 設置鍵盤配置

The default [console keymap](/index.php/Console_keymap "Console keymap") is [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Available layouts can be listed with:

預設的鍵盤配置（[console keymap](/index.php/Console_keymap "Console keymap")）為 [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")。執行以下命令以列出所有配置：

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

To modify the layout, append a corresponding file name to [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omitting path and file extension. For example, to set a [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") keyboard layout:

欲更改鍵盤配置，需將對應的文件名添加經 [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1)，並省略路徑和副檔名。例如，欲添加 [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") 鍵盤配置：

```
# loadkeys de-latin1

```

[Console fonts](/index.php/Console_fonts "Console fonts") are located in `/usr/share/kbd/consolefonts/` and can likewise be set with [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

[Console fonts](/index.php/Console_fonts "Console fonts") 位於 {{ic|/usr/share/kbd/consolefonts/}，設置方式請參考 [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8)。

### Verify the boot mode 確認啟動模式（待翻譯）

If UEFI mode is enabled on an [UEFI](/index.php/UEFI "UEFI") motherboard, [Archiso](/index.php/Archiso "Archiso") will [boot](/index.php/Boot "Boot") Arch Linux accordingly via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). To verify this, list the [efivars](/index.php/UEFI#UEFI_variables "UEFI") directory:

```
# ls /sys/firmware/efi/efivars

```

If the directory does not exist, the system may be booted in [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or CSM mode. Refer to your motherboard's manual for details.

### Connect to the Internet 連接到網際網路（待翻譯）

The installation image enables the [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon for [wired network devices](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) on boot. The connection may be verified with [ping](https://en.wikipedia.org/wiki/ping_(networking_utility) "wikipedia:ping (networking utility)"):

```
# ping archlinux.org

```

If no connection is available, [stop](/index.php/Stop "Stop") the *dhcpcd* service with `systemctl stop dhcpcd@*interface*` where the `*interface*` name can be [tab-completed](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Proceed to configure the network as described in [Network configuration](/index.php/Network_configuration "Network configuration").

### Update the system clock 更新系統時間

Use [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) to ensure the system clock is accurate:

執行 [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) 確保系統時間是準確的：

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`.

可以執行 `timedatectl status` 檢查系統時間的服務狀態。

### Partition the disks 分割硬碟（待翻譯）

When recognized by the live system, disks are assigned to a [block device](https://en.wikipedia.org/wiki/Device_file#Naming_conventions "wikipedia:Device file") such as `/dev/sda` or `/dev/nvme0n1`. To identify these devices, use [lsblk](/index.php/Lsblk "Lsblk") or *fdisk*.

```
# fdisk -l

```

Results ending in `rom`, `loop` or `airoot` may be ignored.

The following *partitions* are **required** for a chosen device:

*   One partition for the root directory `/`.
*   If [UEFI](/index.php/UEFI "UEFI") is enabled, an [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

**Note:** [Swap](/index.php/Swap "Swap") space can be set on a separate partition or a [swap file](/index.php/Swap_file "Swap file").

To modify *partition tables*, use [fdisk](/index.php/Fdisk "Fdisk") or [parted](/index.php/Parted "Parted").

```
# fdisk /dev/*sda*

```

See [Partitioning](/index.php/Partitioning "Partitioning") for more information.

**Note:** If you want to create any stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), do it now.

### Format the partitions 格式化分割

Once the partitions have been created, each must be formatted with an appropriate [file system](/index.php/File_system "File system"). For example, to format the root partition on `/dev/*sda1*` with `*ext4*`, run:

分區一旦建立，每個分區都要用適當的檔案系統（[file system](/index.php/File_system "File system")）進行格式化。例如，欲將 `/dev/*sda1*` 格式化成 `*ext4*`，可執行：

```
# mkfs.*ext4* /dev/*sda1*

```

If you created a partition for swap (for example `/dev/*sda3*`), initialize it with *mkswap*:

如果您創建了 swap 分割（例如 `/dev/*sda3*`），使用 *mkswap* 將其初始化：

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

See [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") for details.

詳情參見（[File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems")）。

### Mount the file systems 掛載檔案系統

[Mount](/index.php/Mount "Mount") the file system on the root partition to `/mnt`, for example:

首先將根分割掛載（[Mount](/index.php/Mount "Mount")）到 `/mnt`，例如：

```
# mount /dev/*sda1* /mnt

```

Create mount points for any remaining partitions and mount them accordingly:

為其它分割創建目錄並掛載它們：

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) will later detect mounted file systems and swap space.

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) 會自動檢測掛載的檔案系統和 swap 分割。

## Installation 安裝

### Select the mirrors 選擇鏡像站（待翻譯）

Packages to be installed must be downloaded from [mirror servers](/index.php/Mirrors "Mirrors"), which are defined in `/etc/pacman.d/mirrorlist`. On the live system, all mirrors are enabled, and sorted by their synchronization status and speed at the time the installation image was created.

The higher a mirror is placed in the list, the more priority it is given when downloading a package. You may want to edit the file accordingly, and move the geographically closest mirrors to the top of the list, although other criteria should be taken into account.

This file will later be copied to the new system by *pacstrap*, so it is worth getting right.

### Install the base packages 安裝系統基本套件

Use the [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) script to install the [base](https://www.archlinux.org/groups/x86_64/base/) package group:

使用 [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 腳本安裝 [base](https://www.archlinux.org/groups/x86_64/base/) 套件組：

```
# pacstrap /mnt base

```

This group does not include all tools from the live installation, such as [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) or specific wireless firmware; see [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) for comparison.

這個套件組沒有包含全部 Live 安裝環境中的工具，例如 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 或是特定的無線裝置的韌體。 差異請見 [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64)。

To [install](/index.php/Install "Install") packages and other groups such as [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), append the names to *pacstrap* (space separated) or to individual [pacman](/index.php/Pacman "Pacman") commands after the [#Chroot](#Chroot) step.

安裝（[install](/index.php/Install "Install")）其他套件或套件組例如 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)，請將它們的名稱添加到 *pacstrap* 之後並用空格隔開。也可以在 [#Chroot](#Chroot) 後使用 [pacman](/index.php/Pacman "Pacman") 個別安裝。

## Configure the system 系統設置

### Fstab

Generate an [fstab](/index.php/Fstab "Fstab") file (use `-U` or `-L` to define by [UUID](/index.php/UUID "UUID") or labels, respectively):

用以下命令生成 [fstab](/index.php/Fstab "Fstab") 文件（用 `-U` 或 `-L` 以使用 UUID 或分割標籤（Partition labels））：

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Check the resulting file in `/mnt/etc/fstab` afterwards, and edit it in case of errors.

執行完後檢查一下生成的 `/mnt/etc/fstab` 文件是否正確，如有錯需立即更正。

### Chroot

[Change root](/index.php/Change_root "Change root") into the new system:

[Change root](/index.php/Change_root "Change root") 到新系統：

```
# arch-chroot /mnt

```

### Time zone 時區

Set the [time zone](/index.php/Time_zone "Time zone"):

設置時區（[time zone](/index.php/Time_zone "Time zone")）:

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

Run [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) to generate `/etc/adjtime`:

執行 [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) 以生成 `/etc/adjtime`：

```
# hwclock --systohc

```

This command assumes the hardware clock is set to [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). See [Time#Time standard](/index.php/Time#Time_standard "Time") for details.

這個命令假定硬體時間已經被設置為 [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC") 時間。詳細資訊請看 [Time#Time standard](/index.php/Time#Time_standard "Time")。

### Localization 語言環境

Uncomment `en_US.UTF-8 UTF-8` and other needed [locales](/index.php/Locale "Locale") in `/etc/locale.gen`, and generate them with:

```
# locale-gen

```

Set the `LANG` [variable](/index.php/Variable "Variable") in [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) accordingly, for example:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

If you [set the keyboard layout](#Set_the_keyboard_layout), make the changes persistent in [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### Network configuration 網路設置

Create the [hostname](/index.php/Hostname "Hostname") file:

創建 [hostname](/index.php/Hostname "Hostname") 文件：

 `/etc/hostname` 
```
*myhostname*

```

Add matching entries to [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

並添加對應的項目到 [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)：

 `/etc/hosts` 
```
127.0.0.1      localhost
::1            localhost
127.0.1.1      *myhostname*.localdomain      *myhostname*

```

If the system has a permanent IP address, it should be used instead of `127.0.1.1`.

如果系統擁有一個永久的 IP 位址，請使用該 IP 位址而不是 `127.0.1.1`。

Complete the [network configuration](/index.php/Network_configuration "Network configuration") for the newly installed environment.

為新安裝的環境完成網路設置 ([network configuration](/index.php/Network_configuration "Network configuration"))。

### Initramfs

Creating a new *initramfs* is usually not required, because [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") was run on installation of the [linux](https://www.archlinux.org/packages/?name=linux) package with *pacstrap*.

你通常不需創建 *initramfs*，因為在執行 *pacstrap* 安裝 [linux](https://www.archlinux.org/packages/?name=linux) 套件時， [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") 即會被自動執行。

For special configurations, modify the [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) file and recreate the initramfs image:

如有特殊配置的需求，可更改 [mkinitcpoi.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpoi.conf.5) 並執行以下命令重新創建一個 Initramfs：

```
# mkinitcpio -p linux

```

### Root password Root 密碼

Set the root [password](/index.php/Password "Password"):

設置 root 密碼（[password](/index.php/Password "Password")）：

```
# passwd

```

### Boot loader 開機引導程式

A Linux-capable boot loader must be installed in order to boot Arch Linux. See [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") for available choices.

你需要安裝與 Linux 相容的開機引導程式（boot loader）以在安裝完成後啟動 Arch Linux。可用的開機程式請參考 [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders")。

If you have an Intel or AMD CPU, enable [microcode](/index.php/Microcode "Microcode") updates.

如果你使用的是 Intel 或 AMD 的 CPU，請開啟微碼（[Microcode](/index.php/Microcode "Microcode")）更新。

## Reboot 重新啟動

Exit the chroot environment by typing `exit` or pressing `Ctrl+D`.

執行 `exit` 或按 `Ctrl+D` 退出 chroot 環境。

Optionally manually unmount all the partitions with `umount -R /mnt`: this allows noticing any "busy" partitions, and finding the cause with [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

可以執行 `umount -R /mnt` 以手動卸載被掛載的分區：這有助於發現任何「繁忙」的分區，並通過 [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1) 查找原因。

Finally, restart the machine by typing `reboot`: any partitions still mounted will be automatically unmounted by *systemd*. Remember to remove the installation media and then login into the new system with the root account.

最后，通過執行 `reboot` 重新啓動系統，*systemd* 將自動卸載掛載中的任何分區。並記得移除安裝媒介，然後使用 root 帳戶登入新系統。

## Post-installation 安裝後

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials (like setting up a graphical user interface, sound or a touchpad).

系統管理引導，圖形使用者介面安裝、聲音管理、觸控板等後期工作參考 [General recommendations](/index.php/General_recommendations "General recommendations")。

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").

感興趣的各類程式，請參考 [List of applications](/index.php/List_of_applications "List of applications")。