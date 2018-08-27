**翻譯狀態：** 本文章是 [Installation_guide](/index.php/Installation_guide "Installation guide") 的翻譯版本。最近一次的翻譯時間：2018-08-26。點擊[本連結](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid={{{3}}})查看英文頁面之後的變更。

此文件是個引導你透過官方安裝映像的 Live 系統安裝 [Arch Linux](/index.php/Arch_Linux "Arch Linux") 的教學。在安裝前，建議先閱讀 [FAQ](/index.php/FAQ "FAQ")。關於此文件使用的慣例，請閱讀 [Help:Reading](/index.php/Help:Reading "Help:Reading")。一些情況下，範例程式碼可能包含佔位符（以 `*italics*` 格式化），其需要手動替換。

若要更多詳細指引，請閱讀 [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") 的分別文章或個別程式的 [man 頁面](/index.php/Man_page "Man page")，這兩個地方都跟此教學相關聯。若要互動型的說明，也可以使用 [IRC channel](/index.php/IRC_channel "IRC channel") 和 [論壇](https://bbs.archlinux.org/)。

Arch Linux 應該可以在任何 [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") 相容與至少 512MB 記憶體上的機器上運作，一個包含所有來自 [base](https://www.archlinux.org/groups/x86_64/base/) 群組的基礎安裝，需要至少 800MB 的硬碟空間。而安裝過程也需要從遠端軟體庫接收軟體包，因此這個教學也假設可以使用網路連線。

## Contents

*   [1 前置作業](#.E5.89.8D.E7.BD.AE.E4.BD.9C.E6.A5.AD)
    *   [1.1 設定鍵盤配置](#.E8.A8.AD.E5.AE.9A.E9.8D.B5.E7.9B.A4.E9.85.8D.E7.BD.AE)
    *   [1.2 Verify the boot mode](#Verify_the_boot_mode)
    *   [1.3 Connect to the Internet](#Connect_to_the_Internet)
    *   [1.4 Update the system clock](#Update_the_system_clock)
    *   [1.5 Partition the disks](#Partition_the_disks)
    *   [1.6 Format the partitions](#Format_the_partitions)
    *   [1.7 Mount the file systems](#Mount_the_file_systems)
*   [2 Installation](#Installation)
    *   [2.1 Select the mirrors](#Select_the_mirrors)
    *   [2.2 Install the base packages](#Install_the_base_packages)
*   [3 Configure the system](#Configure_the_system)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Time zone](#Time_zone)
    *   [3.4 Localization](#Localization)
    *   [3.5 Network configuration](#Network_configuration)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root password](#Root_password)
    *   [3.8 Boot loader](#Boot_loader)
*   [4 Reboot](#Reboot)
*   [5 Post-installation](#Post-installation)

## 前置作業

下載並啟動在 [取得並安裝 Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") 解釋的安裝介質，您將會在第一個 [虛擬終端控制臺](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") 以 root 使用者身份登入，並且以 [Zsh](/index.php/Zsh "Zsh") Shell 提示呈現環境。

假設要切換到不同的終端控制臺，以透過 [ELinks](/index.php/ELinks "ELinks") 在安裝過程中閱讀這個教學 -- 使用 `Alt+*arrow*` [鍵盤快捷鍵](/index.php/Keyboard_shortcuts "Keyboard shortcuts")。若要 [編輯](/index.php/Textedit "Textedit") 配置檔案，可以使用 [nano](/index.php/Nano#Usage "Nano")、[vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") 和 [vim](/index.php/Vim#Usage "Vim")。

### 設定鍵盤配置

預設的 [|終端按鍵映射](/index.php/Console_keymap "Console keymap") 為 [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")。可以透過以下指令列出可用的鍵盤配置：

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

若要修改配置，加入相對應的檔案名稱至 [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omitting path and file extension. For example, to set a [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") keyboard layout:

```
# loadkeys de-latin1

```

[Console fonts](/index.php/Console_fonts "Console fonts") are located in `/usr/share/kbd/consolefonts/` and can likewise be set with [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Verify the boot mode

If UEFI mode is enabled on an [UEFI](/index.php/UEFI "UEFI") motherboard, [Archiso](/index.php/Archiso "Archiso") will [boot](/index.php/Boot "Boot") Arch Linux accordingly via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). To verify this, list the [efivars](/index.php/UEFI#UEFI_variables "UEFI") directory:

```
# ls /sys/firmware/efi/efivars

```

If the directory does not exist, the system may be booted in [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or CSM mode. Refer to your motherboard's manual for details.

### Connect to the Internet

The installation image enables the [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon for [wired network devices](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) on boot. The connection may be verified with [ping](https://en.wikipedia.org/wiki/ping_(networking_utility) "wikipedia:ping (networking utility)"):

```
# ping archlinux.org

```

If no connection is available, [stop](/index.php/Stop "Stop") the *dhcpcd* service with `systemctl stop dhcpcd@*interface*` where the `*interface*` name can be [tab-completed](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Proceed to configure the network as described in [Network configuration](/index.php/Network_configuration "Network configuration").

### Update the system clock

Use [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) to ensure the system clock is accurate:

```
# timedatectl set-ntp true

```

To check the service status, use `timedatectl status`.

### Partition the disks

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

### Format the partitions

Once the partitions have been created, each must be formatted with an appropriate [file system](/index.php/File_system "File system"). For example, to format the root partition on `/dev/*sda1*` with `*ext4*`, run:

```
# mkfs.*ext4* /dev/*sda1*

```

If you created a partition for swap (for example `/dev/*sda3*`), initialize it with *mkswap*:

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

See [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") for details.

### Mount the file systems

[Mount](/index.php/Mount "Mount") the file system on the root partition to `/mnt`, for example:

```
# mount /dev/*sda1* /mnt

```

Create mount points for any remaining partitions and mount them accordingly:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) will later detect mounted file systems and swap space.

## Installation

### Select the mirrors

Packages to be installed must be downloaded from [mirror servers](/index.php/Mirrors "Mirrors"), which are defined in `/etc/pacman.d/mirrorlist`. On the live system, all mirrors are enabled, and sorted by their synchronization status and speed at the time the installation image was created.

The higher a mirror is placed in the list, the more priority it is given when downloading a package. You may want to edit the file accordingly, and move the geographically closest mirrors to the top of the list, although other criteria should be taken into account.

This file will later be copied to the new system by *pacstrap*, so it is worth getting right.

### Install the base packages

Use the [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) script to install the [base](https://www.archlinux.org/groups/x86_64/base/) package group:

```
# pacstrap /mnt base

```

This group does not include all tools from the live installation, such as [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) or specific wireless firmware; see [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) for comparison.

To [install](/index.php/Install "Install") packages and other groups such as [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), append the names to *pacstrap* (space separated) or to individual [pacman](/index.php/Pacman "Pacman") commands after the [#Chroot](#Chroot) step.

## Configure the system

### Fstab

Generate an [fstab](/index.php/Fstab "Fstab") file (use `-U` or `-L` to define by [UUID](/index.php/UUID "UUID") or labels, respectively):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Check the resulting file in `/mnt/etc/fstab` afterwards, and edit it in case of errors.

### Chroot

[Change root](/index.php/Change_root "Change root") into the new system:

```
# arch-chroot /mnt

```

### Time zone

Set the [time zone](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

Run [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) to generate `/etc/adjtime`:

```
# hwclock --systohc

```

This command assumes the hardware clock is set to [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). See [Time#Time standard](/index.php/Time#Time_standard "Time") for details.

### Localization

Uncomment `en_US.UTF-8 UTF-8` and other needed [locales](/index.php/Locale "Locale") in `/etc/locale.gen`, and generate them with:

```
# locale-gen

```

Set the `LANG` [variable](/index.php/Variable "Variable") in [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) accordingly, for example:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

If you [set the keyboard layout](#Set_the_keyboard_layout), make the changes persistent in [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### Network configuration

Create the [hostname](/index.php/Hostname "Hostname") file:

 `/etc/hostname` 
```
*myhostname*

```

Add matching entries to [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*myhostname*.localdomain	*myhostname*

```

If the system has a permanent IP address, it should be used instead of `127.0.1.1`.

Complete the [network configuration](/index.php/Network_configuration "Network configuration") for the newly installed environment.

### Initramfs

Creating a new *initramfs* is usually not required, because [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") was run on installation of the [linux](https://www.archlinux.org/packages/?name=linux) package with *pacstrap*.

For special configurations, modify the [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) file and recreate the initramfs image:

```
# mkinitcpio -p linux

```

### Root password

Set the root [password](/index.php/Password "Password"):

```
# passwd

```

### Boot loader

A Linux-capable boot loader must be installed in order to boot Arch Linux. See [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") for available choices.

If you have an Intel CPU, install the [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) package in addition, and [enable microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Reboot

Exit the chroot environment by typing `exit` or pressing `Ctrl+D`.

Optionally manually unmount all the partitions with `umount -R /mnt`: this allows noticing any "busy" partitions, and finding the cause with [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Finally, restart the machine by typing `reboot`: any partitions still mounted will be automatically unmounted by *systemd*. Remember to remove the installation media and then login into the new system with the root account.

## Post-installation

See [General recommendations](/index.php/General_recommendations "General recommendations") for system management directions and post-installation tutorials (like setting up a graphical user interface, sound or a touchpad).

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").