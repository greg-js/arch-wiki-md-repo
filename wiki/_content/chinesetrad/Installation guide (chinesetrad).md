**翻譯狀態：** 本文章是 [Installation_guide](/index.php/Installation_guide "Installation guide") 的翻譯版本。最近一次的翻譯時間：2016-08-27。點擊[本連結](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=000000)查看英文頁面之後的變更。

本文將指引您使用由官方安裝映像檔啟動的 live system 安裝 [Arch Linux](/index.php/Arch_Linux "Arch Linux")。安裝之前請先閱讀 [FAQ](/index.php/FAQ "FAQ")。For conventions used in this document, see [Help:Reading](/index.php/Help:Reading "Help:Reading")。

更詳細的資源，可以參考 [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") 文章（安裝過程中可以使用 [ELinks](/index.php/ELinks "ELinks") 瀏覽），或者閱讀該命令的 [man page](/index.php/Man_page "Man page") ，參考 [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) for an overview of the configuration. 如需要互動式幫助，可透過 [IRC channel](/index.php/IRC_channel "IRC channel") 及 [forums](https://bbs.archlinux.org/)。

## Contents

*   [1 Pre-installation (安裝前)](#Pre-installation_.28.E5.AE.89.E8.A3.9D.E5.89.8D.29)
    *   [1.1 Verify the boot mode (驗證開機模式)](#Verify_the_boot_mode_.28.E9.A9.97.E8.AD.89.E9.96.8B.E6.A9.9F.E6.A8.A1.E5.BC.8F.29)
    *   [1.2 Set the keyboard layout (設定鍵盤配置)](#Set_the_keyboard_layout_.28.E8.A8.AD.E5.AE.9A.E9.8D.B5.E7.9B.A4.E9.85.8D.E7.BD.AE.29)
    *   [1.3 Connect to the Internet (連接到網際網路)](#Connect_to_the_Internet_.28.E9.80.A3.E6.8E.A5.E5.88.B0.E7.B6.B2.E9.9A.9B.E7.B6.B2.E8.B7.AF.29)
    *   [1.4 Update the system clock (更新系統時間)](#Update_the_system_clock_.28.E6.9B.B4.E6.96.B0.E7.B3.BB.E7.B5.B1.E6.99.82.E9.96.93.29)
    *   [1.5 Partition the disks (分割磁碟)](#Partition_the_disks_.28.E5.88.86.E5.89.B2.E7.A3.81.E7.A2.9F.29)
    *   [1.6 Format the partitions (格式化磁碟)](#Format_the_partitions_.28.E6.A0.BC.E5.BC.8F.E5.8C.96.E7.A3.81.E7.A2.9F.29)
    *   [1.7 Mount the partitions (掛載磁碟)](#Mount_the_partitions_.28.E6.8E.9B.E8.BC.89.E7.A3.81.E7.A2.9F.29)
*   [2 Installation (安裝系統)](#Installation_.28.E5.AE.89.E8.A3.9D.E7.B3.BB.E7.B5.B1.29)
    *   [2.1 Select the mirrors (選擇映射站)](#Select_the_mirrors_.28.E9.81.B8.E6.93.87.E6.98.A0.E5.B0.84.E7.AB.99.29)
    *   [2.2 Install the base packages (安裝基本套件)](#Install_the_base_packages_.28.E5.AE.89.E8.A3.9D.E5.9F.BA.E6.9C.AC.E5.A5.97.E4.BB.B6.29)
*   [3 Configure the system (配置系統)](#Configure_the_system_.28.E9.85.8D.E7.BD.AE.E7.B3.BB.E7.B5.B1.29)
    *   [3.1 Fstab (檔案系統列表)](#Fstab_.28.E6.AA.94.E6.A1.88.E7.B3.BB.E7.B5.B1.E5.88.97.E8.A1.A8.29)
    *   [3.2 Chroot (改變根目錄)](#Chroot_.28.E6.94.B9.E8.AE.8A.E6.A0.B9.E7.9B.AE.E9.8C.84.29)
    *   [3.3 Time zone (時區)](#Time_zone_.28.E6.99.82.E5.8D.80.29)
    *   [3.4 Locale (語系)](#Locale_.28.E8.AA.9E.E7.B3.BB.29)
    *   [3.5 Hostname (主機名稱)](#Hostname_.28.E4.B8.BB.E6.A9.9F.E5.90.8D.E7.A8.B1.29)
    *   [3.6 Network configuration (網路設定)](#Network_configuration_.28.E7.B6.B2.E8.B7.AF.E8.A8.AD.E5.AE.9A.29)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Root password (Root 密碼)](#Root_password_.28Root_.E5.AF.86.E7.A2.BC.29)
    *   [3.9 Boot loader (開機管理程式)](#Boot_loader_.28.E9.96.8B.E6.A9.9F.E7.AE.A1.E7.90.86.E7.A8.8B.E5.BC.8F.29)
*   [4 Reboot (重新啟動)](#Reboot_.28.E9.87.8D.E6.96.B0.E5.95.9F.E5.8B.95.29)
*   [5 Post-installation (安裝後)](#Post-installation_.28.E5.AE.89.E8.A3.9D.E5.BE.8C.29)

## Pre-installation (安裝前)

Arch Linux 可以運行在任何記憶體不小於 256MB 的相容裝置上。最基本的 [base](https://www.archlinux.org/groups/x86_64/base/) 套件組需要至少 800MB 的磁碟空間。安裝過程需要從遠端的repo取得套件，因此必須確定網路正常運作。

[Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") 包含了下載並啟動安裝媒體的說明。啟動後您會以 root 的身份登入並進入 [Zsh](/index.php/Zsh "Zsh") 命令列，常見的指令例如 [systemctl(1)](http://man7.org/linux/man-pages/man1/systemctl.1.html) 可以使用 Tab 鍵自動補齊。

編輯配置文件可用 [nano](/index.php/Nano#Usage "Nano")，[vi](https://en.wikipedia.org/wiki/vi "w:vi") 或 [vim](/index.php/Vim#Usage "Vim")。

### Verify the boot mode (驗證開機模式)

As instructions differ for [UEFI](/index.php/UEFI "UEFI") systems，檢查 [efivars](/index.php/Efivars "Efivars") 檔案以確認開機模式：

```
# ls /sys/firmware/efi/efivars

```

### Set the keyboard layout (設定鍵盤配置)

默認的鍵盤配置([console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console"))為 [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")。`ls /usr/share/kbd/keymaps/**/*.map.gz` 可列出可用的键盘布局。

配置可用 [loadkeys(1)](http://man7.org/linux/man-pages/man1/loadkeys.1.html) 改變，加上檔案名稱（可以忽略路徑及副檔名）。例如：

```
# loadkeys *de-latin1*

```

[Console fonts](/index.php/Console_fonts "Console fonts") 位於 `/usr/share/kbd/consolefonts/`，設置方式請參考 [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html)。

### Connect to the Internet (連接到網際網路)

所有支援的有線網路在 live system 啟動後皆會啟用 [dhcpcd](/index.php/Dhcpcd "Dhcpcd")，可以用 [ping](/index.php/Ping "Ping") 等工具檢查網路連接。

如欲使用其他網路配置（[network configuration](/index.php/Network_configuration "Network configuration")）工具，可以使用 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")及[netctl](/index.php/Netctl "Netctl")。範例請參考[systemd.network(5)](http://man7.org/linux/man-pages/man5/systemd.network.5.html)和[netctl.profile(5)](https://git.archlinux.org/netctl.git/tree/docs/netctl.profile.5.txt)。

使用兩個網路服務（service）之一時，請先 [stop](/index.php/Stop "Stop") `dhcpcd@*interface*.service`。

### Update the system clock (更新系統時間)

用[timedatectl(1)](http://man7.org/linux/man-pages/man1/timedatectl.1.html)確保系統時間為正確的：

```
# timedatectl set-ntp true

```

他 用`timedatectl status`檢查服務狀態。

### Partition the disks (分割磁碟)

使用 [fdisk](/index.php/Fdisk "Fdisk") 和 [parted](/index.php/Parted "Parted") 製作 [MBR](/index.php/MBR "MBR") 或 [GPT](/index.php/GPT "GPT") 磁碟分割表(partition table)，或使用 [gdisk](/index.php/Gdisk "Gdisk") 製作 [GPT](/index.php/GPT "GPT") 磁碟分割表。

至建立一個 `/` 分割區。[UEFI](/index.php/UEFI "UEFI") 系統另外需要一個 EPS分割區([EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition"))。Other partitions may be needed, such as a [GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB").

If wanting to create any stacked block devices for [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") or [RAID](/index.php/RAID "RAID"), do it now.

### Format the partitions (格式化磁碟)

使用 [mkfs(8)](http://man7.org/linux/man-pages/man8/mkfs.8.html) 建立檔案系統([File systems](/index.php/File_systems "File systems"))，或者使用 [mkswap(8)](http://man7.org/linux/man-pages/man8/mkswap.8.html) 建立 [swap](/index.php/Swap "Swap") 區。詳細請參考 [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems")。

### Mount the partitions (掛載磁碟)

掛載([mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html)) root 分割區到 `/mnt`。例如：

```
# mount /dev/*sda1* /mnt 

```

之後請為其他分割區創建目錄(directory)並掛載他們 (`/mnt/boot`, `/mnt/home`, ...)，並用 [swapon(8)](http://man7.org/linux/man-pages/man8/swapon.8.html) 啟動 *swap* 分割區，如此才能被 *genfstab* 偵測到。

## Installation (安裝系統)

### Select the mirrors (選擇映射站)

編輯 `/etc/pacman.d/mirrorlist` 並選擇您的映射站(mirror)。Regional mirrors usually work best; however, other criteria may be necessary to discern, read more on [Mirrors](/index.php/Mirrors "Mirrors").

此檔案(mirror 列表)也會被*pacstrap*複製到新系統中，所以請確保設置正確。

### Install the base packages (安裝基本套件)

執行 [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 腳本安裝 [base](https://www.archlinux.org/groups/x86_64/base/) 套件組：

```
# pacstrap /mnt base

```

此套件組並無包含全部 live 安裝環境的中所有工具，例如 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) 或特定的無線韌體。[packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) 包含了他們的差異。

To [install](/index.php/Install "Install") other packages or groups to the new system, append their names to *pacstrap* (space separated) or to individual [pacman(8)](https://www.archlinux.org/pacman/pacman.8.html) commands after the [#Chroot](#Chroot) step.

## Configure the system (配置系統)

### Fstab (檔案系統列表)

建立 [fstab](/index.php/Fstab "Fstab") 檔案 (使用 `-U` 或 `-L` 選項設置 [UUID](/index.php/UUID "UUID") 或 labels)：

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

接下來請檢查生成的檔案 `/mnt/etc/fstab`，如有錯誤請更正。

### Chroot (改變根目錄)

[Change root](/index.php/Change_root "Change root") 進入新的系統：

```
# arch-chroot /mnt

```

### Time zone (時區)

設定 [time zone](/index.php/Time_zone "Time zone"):

```
# ln -s /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime

```

使用 [hwclock(8)](http://man7.org/linux/man-pages/man8/hwclock.8.html) 建立 `/etc/adjtime`。If the hardware clock is set to [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"), other operating systems should be [configured accordingly](/index.php/Time_standard "Time standard").

```
# hwclock --systohc --*utc*

```

### Locale (語系)

在 `/etc/locale.gen` 移除 `en_US.UTF-8 UTF-8` 及其他需要的 [localization](/index.php/Localization "Localization") 前的註釋符號(#)，接著生成 locale 訊息：

```
# locale-gen

```

创建 locale.conf 并提交您的本地化选项 在 [locale.conf(5)](http://man7.org/linux/man-pages/man5/locale.conf.5.html) 中設定您的語系選項。例如：

```
# echo LANG=*en_US.UTF-8* > /etc/locale.conf

```

If required, set the [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [font](/index.php/Fonts#Console_fonts "Fonts") in [vconsole.conf(5)](http://man7.org/linux/man-pages/man5/vconsole.conf.5.html).

### Hostname (主機名稱)

在 `/etc/hostname` 建立新的項目 [hostname](/index.php/Hostname "Hostname")：

```
# echo *myhostname* > /etc/hostname

```

Add a matching line to `/etc/hosts`:

```
127.0.1.1  *myhostname*.localdomain  *myhostname*

```

### Network configuration (網路設定)

需要對新安裝的系統設置網路配置請參考 [Network configuration](/index.php/Network_configuration "Network configuration")。

對於無線網路配置([Wireless configuration](/index.php/Wireless_configuration "Wireless configuration"))，安裝 [iw](https://www.archlinux.org/packages/?name=iw)， [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) 和 [dialog](https://www.archlinux.org/packages/?name=dialog) 以及需要的韌體套件([firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless"))。

### Initramfs

When making configuration changes to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), create a new initial RAM disk with:

```
# mkinitcpio -p linux

```

### Root password (Root 密碼)

設定 root [password](/index.php/Password "Password"):

```
# passwd

```

### Boot loader (開機管理程式)

可用的選擇和配置請參考 [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders")。例如，如果您的系統支援 UEFI，使用 [systemd-boot](/index.php/Systemd-boot "Systemd-boot") 建立開機管理，反之則用 [GRUB](/index.php/GRUB#BIOS_systems "GRUB")。

如果您與用 Intel CPU，請另外安裝 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) 並啟用 Intel microcode Updates([enable microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode"))。

## Reboot (重新啟動)

輸入 `exit` 或按下 `Ctrl+D` 以離開 chroot 環境。

Optionally manually unmount all the partitions with `umount -R /mnt`: this allows noticing any "busy" partitions, and finding the cause with [fuser(1)](http://man7.org/linux/man-pages/man1/fuser.1.html).

最後，輸入`reboot` 以重新啟動裝置，所有未卸載的磁碟分割區將會自動由 *systemd* 卸載。記得移除安裝媒體並以 root 身份登入新系統。

## Post-installation (安裝後)

系統管理和安裝後的相關教學（例如：圖形化使用者界面，聲音，觸控板）請參考 [General recommendations](/index.php/General_recommendations "General recommendations")。

感興趣的各類應用程式，請參考 [List of applications](/index.php/List_of_applications "List of applications")。