**翻譯狀態：** 本文章是 [Installation_guide](/index.php/Installation_guide "Installation guide") 的翻譯版本。最近一次的翻譯時間：2020-01-20。點擊[本連結](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid={{{3}}})查看英文頁面之後的變更。

此文件是個引導你透過官方安裝映像的 Live 系統安裝 [Arch Linux](/index.php/Arch_Linux "Arch Linux") 的教學。在安裝前，建議先閱讀 [FAQ](/index.php/FAQ "FAQ"). 關於此文件使用的慣例字詞，請閱讀 [Help:Reading](/index.php/Help:Reading "Help:Reading"). 一些情況下，範例程式碼可能包含佔位符（以`*斜體*`格式化），其需要手動替換。

更詳細的資源可以參考 [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") 文章，或者閱讀該程式的[手冊頁](/index.php/Man_page "Man page")。如需要互動式幫助，可以使用 [IRC channel](/index.php/IRC_channel "IRC channel") 及[英文論壇](https://bbs.archlinux.org/)。

Arch Linux 可在任何 RAM 不小於 512MiB 的 [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") 相容機器上運作。基本安裝將佔用小於 800MiB 的硬碟空間。由於安裝過程中需要從遠端軟體庫取得軟體包，因此需要連線到網際網路。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安裝前的準備](#安裝前的準備)
    *   [1.1 驗證簽章](#驗證簽章)
    *   [1.2 啓動 live 環境](#啓動_live_環境)
    *   [1.3 設定鍵盤配置](#設定鍵盤配置)
    *   [1.4 確認啟動模式](#確認啟動模式)
    *   [1.5 連線到網際網路](#連線到網際網路)
    *   [1.6 更新系統時間](#更新系統時間)
    *   [1.7 分割硬碟](#分割硬碟)
        *   [1.7.1 分割區示例](#分割區示例)
    *   [1.8 格式化分割](#格式化分割)
    *   [1.9 掛載檔案系統](#掛載檔案系統)
*   [2 安裝](#安裝)
    *   [2.1 選擇鏡像站](#選擇鏡像站)
    *   [2.2 安裝必要的軟體包](#安裝必要的軟體包)
*   [3 配置系統](#配置系統)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 時區](#時區)
    *   [3.4 在地化](#在地化)
    *   [3.5 配置網路](#配置網路)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root 密碼](#Root_密碼)
    *   [3.8 開機引導程式](#開機引導程式)
*   [4 重新啟動](#重新啟動)
*   [5 安裝後](#安裝後)

## 安裝前的準備

安裝媒介和它們的 [GnuPG](/index.php/GnuPG "GnuPG") 簽章可在[下載](https://archlinux.org/download/)頁獲取。

### 驗證簽章

推薦在使用鏡像前先驗證簽章，特別是從容易被攔截而[提供惡意鏡像](https://www2.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html)的 *HTTP 鏡像源*下載時。

在已經安裝 [GnuPG](/index.php/GnuPG "GnuPG") 的系統上，下載 *PGP 簽章*到 ISO 所在目錄，然後[進行驗證](/index.php/GnuPG#Verify_a_signature "GnuPG")：

```
$ gpg --keyserver-options auto-key-retrieve --verify archlinux-*version*-x86_64.iso.sig

```

或者，在已經安裝的 Arch Linux 作業系統上運行：

```
$ pacman-key -v archlinux-*version*-x86_64.iso.sig

```

**注意:**

*   如簽章是從鏡像源而非上文的 [archlinux.org](https://archlinux.org/download/) 下載，則其本身可被僞造。在這種情況下，確保用於解碼簽章的公鑰被另一可信任的金鑰簽名。`gpg` 指令會輸出公鑰的指紋。
*   另一種驗證簽章的方法是確保公鑰的指紋與簽署 ISO 檔案的 [Arch Linux 開發者](https://www.archlinux.org/people/developers/)相同。要獲取更多關於公鑰加密的訊息，請閱讀 [Wikipedia:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography").

### 啓動 live 環境

live 環境可從 [USB 隨身碟](/index.php/USB_flash_installation_media "USB flash installation media")，[光碟](/index.php/Optical_disc_drive#Burning "Optical disc drive")或含有 [PXE](/index.php/PXE "PXE") 的網路啓動。其它安裝方法參閱 [Category:Installation process](/index.php/Category:Installation_process "Category:Installation process").

*   通常通過在 [POST](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") 階段按下某個按鍵來選擇含有 Arch 安裝媒介的驅動器，熒幕上會出現提示。更多細節請閱讀主機板的手冊。
*   在 Arch 啓動選單出現時，選擇 *Boot Arch Linux* 並按下 `Enter` 來進入 live 環境。
*   閱讀 [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) 來獲取[啓動選項](/index.php/Kernel_parameters#Configuration "Kernel parameters")列表，以及 [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) 來獲取包含的軟體包列表。
*   你會作爲 root 使用者登入第一個 [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console")，並進入 [Zsh](/index.php/Zsh "Zsh") shell.

要切換至另一終端機——比如要在安裝的同時使用 [ELinks](/index.php/ELinks "ELinks") 閱讀本指南——使用 `Alt+*箭頭*` [快捷鍵](/index.php/Keyboard_shortcuts "Keyboard shortcuts")。要[編輯](/index.php/Textedit "Textedit")設定檔，可使用 [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") 和 [vim](/index.php/Vim#Usage "Vim").

### 設定鍵盤配置

預設的[鍵盤配置](/index.php/Console_keymap "Console keymap")為 [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") 配置。可使用以下指令列出所有配置：

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

欲更改鍵盤配置，需將對應的檔案名稱，省略路徑和副檔名附加到 [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) 中。例如，要附加 [German](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") 鍵盤配置：

```
# loadkeys de-latin1

```

[終端字體](/index.php/Console_fonts "Console fonts")位於 `/usr/share/kbd/consolefonts/`, 設定方式請參考 [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### 確認啟動模式

如果在 [UEFI](/index.php/UEFI "UEFI") 主機板上有啟用 UEFI 模式的話，[Archiso](/index.php/Archiso "Archiso") 將會根據 [systemd-boot](/index.php/Systemd-boot "Systemd-boot") 給出的設定[引導](/index.php/Boot "Boot") Arch Linux。若要驗證是否啟用，請使用 ls 指令列出 [efivars](/index.php/UEFI#UEFI_variables "UEFI") 目錄：

```
# ls /sys/firmware/efi/efivars

```

如果目錄不存在，系統可能以 [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") 或 CSM 模式啟動。參閱您的主機板說明了解詳細資訊。

### 連線到網際網路

按以下步驟連線到網際網路：

*   確認網路界面被列出且已被啓用，如使用 [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8): `# ip link` 
*   連線到忘記網路。插入乙太網路線或[連線到無線網路](/index.php/Wireless_network_configuration "Wireless network configuration")。
*   設定網路連線：
    *   [靜態 IP](/index.php/Network_configuration#Static_IP_address "Network configuration")
    *   動態 IP：使用 [DHCP](/index.php/DHCP "DHCP").

    **注意:** 在引導時，安裝鏡像會自動啓動 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*界面*.service`) 來設定[有線網路設備](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules)。

*   連線狀態可使用 [ping](https://en.wikipedia.org/wiki/ping "wikipedia:ping") 來確認： `# ping archlinux.org` 

### 更新系統時間

執行 [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) 確保系統時間是準確的：

```
# timedatectl set-ntp true

```

可以執行 `timedatectl status` 檢查時間同步服務的狀態。

### 分割硬碟

在被 live 系統識別後，硬碟會被分配爲[設備文件](/index.php/Block_device "Block device")，如 `/dev/sda` 或 `/dev/nvme0n1`. 可使用 [lsblk](/index.php/Lsblk "Lsblk") 或 *fdisk* 查看這些文件。

```
# fdisk -l

```

可忽略以 `rom`, `loop` 或 `airoot` 結尾的結果。

對於選中的設備，以下[分割區](/index.php/Partition "Partition")是**必需**的：

*   掛載在根目錄 `/` 的分割區。
*   如使用 [UEFI](/index.php/UEFI "UEFI")，一個 [EFI 系統分區](/index.php/EFI_system_partition "EFI system partition")。

如果想要使用 [LVM](/index.php/LVM "LVM"), [system encryption](/index.php/Dm-crypt "Dm-crypt") 或 [RAID](/index.php/RAID "RAID") 等建立多級儲存，請在此時完成。

#### 分割區示例

| BIOS 和 [MBR](/index.php/MBR "MBR") |
| 掛載點 | 分割區 | [分割區類型](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") | 建議的大小 |
| `/mnt` | `/dev/sd*X*1` | Linux | 剩餘的所有空間 |
| [SWAP] | `/dev/sd*X*2` | Linux swap | 大於 512 MiB |
| UEFI 和 [GPT](/index.php/GPT "GPT") |
| 掛載點 | 分割區 | [分割區類型](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") | 建議的大小 |
| `/mnt/boot` 或 `/mnt/efi` | `/dev/sd*X*1` | [EFI system partition](/index.php/EFI_system_partition "EFI system partition") | 260–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 root (/) | 剩餘的所有空間 |
| [SWAP] | `/dev/sd*X*3` | Linux swap | 大於 512 MiB |

參閱 [Partitioning#Example layouts](/index.php/Partitioning#Example_layouts "Partitioning").

**注意:**

*   使用 [fdisk](/index.php/Fdisk "Fdisk") 或 [parted](/index.php/Parted "Parted") 改動分區表，如 `fdisk /dev/sd*X*`.
*   在支援的檔案系統上可使用 [swap file](/index.php/Swap_file "Swap file") 設定 [Swap](/index.php/Swap "Swap") 空間。

### 格式化分割

一旦建立，每個分區都要用適當的[檔案系統](/index.php/File_system "File system")進行格式化。例如，根分區位於 `/dev/sd*X*1`, 且會包含 `*ext4*` 檔案系統，執行：

```
# mkfs.*ext4* /dev/sd*X1*

```

如果創建了 swap 分割，使用 *mkswap* 將其初始化：

```
# mkswap /dev/sd*X2*
# swapon /dev/sd*X2*

```

詳情參見 [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems").

### 掛載檔案系統

首先將根分區[掛載](/index.php/Mount "Mount")到 `/mnt`，例如：

```
# mount /dev/sd*X1* /mnt

```

創建剩餘的掛載點（如 `/mnt/efi`），然後掛載對應的分割區。

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) 稍後會自動檢測掛載的檔案系統和 swap 空間。

## 安裝

### 選擇鏡像站

要安裝的包必須從在 `/etc/pacman.d/mirrorlist` 中設定的[鏡像站](/index.php/Mirrors "Mirrors")下載。在 live 環境中，所有鏡像站都被預設啓用，且按照鏡像創建時的同步狀態和速度排序。

在下載時，列表中越靠前的鏡像站擁有越高的優先級。你可以按此編輯設定檔，並將地理位置最近的鏡像站移至頂端，同時也需要考慮其它標準。

*pacstrap* 稍後會將此文件複製到新系統中，所以請確保設定正確。

### 安裝必要的軟體包

使用 [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 腳本安裝 [base](https://www.archlinux.org/packages/?name=base) 軟體包，Linux [核心](/index.php/Kernel "Kernel")及常規硬體的韌體：

```
# pacstrap /mnt base linux linux-firmware

```

**提示：** 你可以將 [linux](https://www.archlinux.org/packages/?name=linux) 替換爲其它可選擇的[核心](/index.php/Kernel "Kernel")。如果知道自己的需求，可以不安裝核心或韌體。

[base](https://www.archlinux.org/packages/?name=base) 軟體包不包含所有 live 環境中的工具。要有一個完全可用的基本系統，你可能需要安裝其它軟體包。具體地說，考慮安裝：

*   管理所用[檔案系統](/index.php/File_systems "File systems")的工具;
*   訪問 [RAID](/index.php/RAID "RAID") 或 [LVM](/index.php/LVM "LVM") 分割區的工具;
*   未包含在 [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) 中的設備韌體;
*   [連線到網際網路](/index.php/Networking "Networking")需要的軟體;
*   [文本編輯器](/index.php/Text_editor "Text editor");
*   訪問 [man](/index.php/Man "Man") 和 [info](/index.php/Info "Info") 頁面的工具：[man-db](https://www.archlinux.org/packages/?name=man-db), [man-pages](https://www.archlinux.org/packages/?name=man-pages) 和 [texinfo](https://www.archlinux.org/packages/?name=texinfo).

要安裝其它軟體包/包組，將名字附加在上文的 *pacstrap* 指令之後（使用空格分隔），或在 [Chroot 進入新系統](#Chroot)後使用 [pacman](/index.php/Pacman "Pacman"). 可在 [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) 中找到 live 環境包含的所有軟體包列表。

## 配置系統

### Fstab

使用以下指令生成 [fstab](/index.php/Fstab "Fstab") 文件（使用 `-U` 或 `-L` 來選擇 [UUID](/index.php/UUID "UUID") 或檔案系統標籤（LABEL））：

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

檢查生成的 `/mnt/etc/fstab` 文件，如有錯誤請立即更正。

### Chroot

[Change root](/index.php/Change_root "Change root") 進入新系統：

```
# arch-chroot /mnt

```

### 時區

設定[時區](/index.php/Time_zone "Time zone")：

```
# ln -sf /usr/share/zoneinfo/*地區*/*城市* /etc/localtime

```

執行 [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) 以生成 `/etc/adjtime`:

```
# hwclock --systohc

```

這個命令假定硬體時間已經被設置為 [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC") 時間。詳細資訊參見 [System time#Time standard](/index.php/System_time#Time_standard "System time").

### 在地化

在 `/etc/locale.gen` 中取消註釋 `en_US.UTF-8 UTF-8` 和其它需要的 [locale](/index.php/Locale "Locale"), 然後生成它們：

```
# locale-gen

```

創建 [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) 文件，並按下方設定 `LANG` [變數](/index.php/Variable "Variable")：

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

如果[設定了鍵盤配置](#設定鍵盤配置)，編輯 [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) 以保留更改：

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### 配置網路

創建 [hostname](/index.php/Hostname "Hostname") 文件：

 `/etc/hostname` 
```
*myhostname*

```

並添加對應的項目到 [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*myhostname*.localdomain	*myhostname*

```

如果系統擁有一個永久的 IP 位址，請使用該 IP 位址替代 `127.0.1.1`。

為新安裝的環境[配置網路](/index.php/Network_configuration "Network configuration")，包含安裝想要使用的[網路管理](/index.php/Network_management "Network management")工具。

### Initramfs

一般不需要創建新的 *initramfs*, 因為在使用 *pacstrap* 安裝[核心](/index.php/Kernel "Kernel")時， [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") 已經被自動執行。

對於 [LVM](/index.php/LVM#Configure_mkinitcpio "LVM"), [system encryption](/index.php/Dm-crypt "Dm-crypt") 或 [RAID](/index.php/RAID#Configure_mkinitcpio "RAID"), 更改 [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) 並重新生成 initramfs:

```
# mkinitcpio -P

```

### Root 密碼

設置 root [密碼](/index.php/Password "Password")：

```
# passwd

```

### 開機引導程式

選擇並安裝一個與 Linux 相容的[開機引導程式](/index.php/Boot_loader "Boot loader")。如使用 Intel 或 AMD CPU, 需要額外地啓用 [microcode](/index.php/Microcode "Microcode") 更新。

## 重新啟動

執行 `exit` 或按 `Ctrl+d` 退出 chroot 環境。

可以手動執行 `umount -R /mnt` 以手動卸載所有分區：這有助於發現任何「繁忙」的分區，並通過 [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1) 查找原因。

最后，通過執行 `reboot` 重新啓動系統，*systemd* 將自動卸載所有掛載中的分區。記得移除安裝媒介，然後使用 root 帳戶登入新系統。

## 安裝後

系統管理與安裝後指南（如設定圖形使用者介面、聲音或觸控板）參見 [General recommendations](/index.php/General_recommendations "General recommendations").

要尋找可能感興趣的各類程式，參見 [List of applications](/index.php/List_of_applications "List of applications").