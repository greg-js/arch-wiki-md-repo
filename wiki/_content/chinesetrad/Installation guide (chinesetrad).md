**翻譯狀態：** 本文章是 [Installation_guide](/index.php/Installation_guide "Installation guide") 的翻譯版本。最近一次的翻譯時間：2018-11-25。點擊[本連結](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid={{{3}}})查看英文頁面之後的變更。

此文件是個引導你透過官方安裝映像的 Live 系統安裝 [Arch Linux](/index.php/Arch_Linux "Arch Linux") 的教學。在安裝前，建議先閱讀 [FAQ](/index.php/FAQ "FAQ")。關於此文件使用的慣例字詞，請閱讀 [Help:Reading](/index.php/Help:Reading "Help:Reading")。一些情況下，範例程式碼可能包含佔位符（以`*斜體*`格式化），其需要手動替換。

更詳細的資源可以參考 [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") 文章，或者閱讀該命令的 [man page](/index.php/Man_page "Man page")。如需要互動式幫助，可以使用 [IRC channel](/index.php/IRC_channel "IRC channel") 及 [英文論壇](https://bbs.archlinux.org/)。

Arch Linux 可在任何 RAM 不小於 512MB 的 [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") 相容機器上運作。用 [base](https://www.archlinux.org/groups/x86_64/base/) 軟體包群組內的所有軟體包進行基本安裝將佔用小於 800MB 的硬碟空間。由於安裝過程中需要從遠端軟體庫取得軟體包，因此需要連線到網際網路。

## Contents

*   [1 安裝前的準備](#安裝前的準備)
    *   [1.1 設定鍵盤配置](#設定鍵盤配置)
    *   [1.2 確認啟動模式](#確認啟動模式)
    *   [1.3 連線到網際網路](#連線到網際網路)
    *   [1.4 更新系統時間](#更新系統時間)
    *   [1.5 Partition the disks 分割硬碟（待翻譯）](#Partition_the_disks_分割硬碟（待翻譯）)
    *   [1.6 Format the partitions 格式化分割](#Format_the_partitions_格式化分割)
    *   [1.7 Mount the file systems 掛載檔案系統](#Mount_the_file_systems_掛載檔案系統)
*   [2 Installation 安裝](#Installation_安裝)
    *   [2.1 Select the mirrors 選擇鏡像站（待翻譯）](#Select_the_mirrors_選擇鏡像站（待翻譯）)
    *   [2.2 Install the base packages 安裝系統基本套件](#Install_the_base_packages_安裝系統基本套件)
*   [3 Configure the system 系統設置](#Configure_the_system_系統設置)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone 時區](#Time_zone_時區)
    *   [3.4 Localization 語言環境](#Localization_語言環境)
    *   [3.5 Network configuration 網路設置](#Network_configuration_網路設置)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root password Root 密碼](#Root_password_Root_密碼)
    *   [3.8 Boot loader 開機引導程式](#Boot_loader_開機引導程式)
*   [4 Reboot 重新啟動](#Reboot_重新啟動)
*   [5 Post-installation 安裝後](#Post-installation_安裝後)

## 安裝前的準備

根據[取得並安裝 Arch *(英文)*](/index.php/Getting_and_installing_Arch "Getting and installing Arch")中所述，下載並引導安裝媒介。啟動完成後將會自動以 root 使用者身份登入虛擬終端器（[virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console")）並進入 [Zsh](/index.php/Zsh "Zsh") 命令解譯器。

欲切換至其它的虛擬終端器，例如在安裝過程使用 [ELinks](/index.php/ELinks "ELinks") 來查看本篇指南，使用 `Alt+*arrow*` 快捷鍵（[shortcut](/index.php/Keyboard_shortcuts "Keyboard shortcuts")）。可使用 [nano](/index.php/Nano#Usage "Nano")、[vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") 或 [vim](/index.php/Vim#Usage "Vim") 來編輯（[edit](/index.php/Textedit "Textedit")）設定檔案。

### 設定鍵盤配置

預設的鍵盤配置（[console keymap](/index.php/Console_keymap "Console keymap")）為 [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") 配置。可使用以下指令列出所有配置：

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

欲更改鍵盤配置，需將對應的檔案名稱，省略路徑和副檔名附加到 [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) 中。例如，要附加 [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") 鍵盤配置：

```
# loadkeys de-latin1

```

[終端字體](/index.php/Console_fonts "Console fonts")位於 `/usr/share/kbd/consolefonts/`，設定方式請參考 [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8)。

### 確認啟動模式

如果在 [UEFI](/index.php/UEFI "UEFI") 主機板上有啟用 UEFI 模式的話，[Archiso](/index.php/Archiso "Archiso") 將會根據 [systemd-boot](/index.php/Systemd-boot "Systemd-boot") 給出的設定[引導](/index.php/Boot "Boot") Arch Linux。若要驗證是否啟用，請使用 ls 指令列出 [efivars](/index.php/UEFI#UEFI_variables "UEFI") 資料夾：

```
# ls /sys/firmware/efi/efivars

```

如果資料夾不存在，系統可能將會以 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 或 CSM 模式啟動。參閱您的主機板說明了解詳細資訊。

### 連線到網際網路

安裝媒體啟用了 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 守護程序用來在開機時連線[有線網路裝置](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules)。若要確認是否連上網路，可使用 [ping](https://en.wikipedia.org/wiki/ping_(networking_utility) 檢查：

```
# ping archlinux.org

```

如果沒有網路，則請使用 `systemctl stop dhcpcd@*interface*` [停止](/index.php/Stop "Stop") *dhcpcd* 服務，`*interface*` 名稱可以[用 Tab 自動完成](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion")。

### 更新系統時間

執行 [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) 確保系統時間是準確的：

```
# timedatectl set-ntp true

```

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

This command assumes the hardware clock is set to [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). See [System time#Time standard](/index.php/System_time#Time_standard "System time") for details.

這個命令假定硬體時間已經被設置為 [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC") 時間。詳細資訊請看 [System time#Time standard](/index.php/System_time#Time_standard "System time")。

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