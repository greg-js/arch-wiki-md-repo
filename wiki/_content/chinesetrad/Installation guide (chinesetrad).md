**翻譯狀態：** 本文章是 [Installation_guide](/index.php/Installation_guide "Installation guide") 的翻譯版本。最近一次的翻譯時間：2015-05-13。點擊[本連結](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=310158)查看英文頁面之後的變更。

這份文件是[Arch Linux](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)")從官方安裝映像檔啟動Live系統後的安裝指南。 開始之前建議您大略瀏覽一下 [FAQ](/index.php/FAQ_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "FAQ (正體中文)") 。 如果需要更詳細、更清楚的安裝指南，可以參考[新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)") 。 [獲取並安裝 Arch](/index.php/Category:Getting_and_installing_Arch_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Category:Getting and installing Arch (正體中文)") 分類下也有幾份針對特殊狀況的安裝指南。

若您碰到任何問題，社群維護的 [Arch 維基](/index.php/Main_Page_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Main Page (正體中文)")是主要的資料來源，請多加利用。若無法自行解決，也歡迎到 [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") 頻道 ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) 和[論壇](https://bbs.archlinux.org/) 還有 [Arch Linux 臺灣社群](http://archlinux.tw/) 問問。 若您碰到不熟悉的指令，可以呼叫 `man **指令**` 查看該指令的 `man` 說明文件。

## Contents

*   [1 下載](#.E4.B8.8B.E8.BC.89)
*   [2 前期安裝流程](#.E5.89.8D.E6.9C.9F.E5.AE.89.E8.A3.9D.E6.B5.81.E7.A8.8B)
    *   [2.1 鍵盤配置](#.E9.8D.B5.E7.9B.A4.E9.85.8D.E7.BD.AE)
    *   [2.2 分割硬碟](#.E5.88.86.E5.89.B2.E7.A1.AC.E7.A2.9F)
    *   [2.3 格式化分割區](#.E6.A0.BC.E5.BC.8F.E5.8C.96.E5.88.86.E5.89.B2.E5.8D.80)
    *   [2.4 掛載分割區](#.E6.8E.9B.E8.BC.89.E5.88.86.E5.89.B2.E5.8D.80)
    *   [2.5 連接網路](#.E9.80.A3.E6.8E.A5.E7.B6.B2.E8.B7.AF)
    *   [2.6 無線網路](#.E7.84.A1.E7.B7.9A.E7.B6.B2.E8.B7.AF)
    *   [2.7 安裝基本系統](#.E5.AE.89.E8.A3.9D.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.B5.B1)
    *   [2.8 設定系統](#.E8.A8.AD.E5.AE.9A.E7.B3.BB.E7.B5.B1)
    *   [2.9 安裝並設定開機載入程式](#.E5.AE.89.E8.A3.9D.E4.B8.A6.E8.A8.AD.E5.AE.9A.E9.96.8B.E6.A9.9F.E8.BC.89.E5.85.A5.E7.A8.8B.E5.BC.8F)
    *   [2.10 卸載並重啟系統](#.E5.8D.B8.E8.BC.89.E4.B8.A6.E9.87.8D.E5.95.9F.E7.B3.BB.E7.B5.B1)
*   [3 安裝完成後](#.E5.AE.89.E8.A3.9D.E5.AE.8C.E6.88.90.E5.BE.8C)

## 下載

在 [Arch Linux 下載頁面](https://www.archlinux.org/download/)，下載最新的 Arch Linux ISO：這是可以依系統架構和使用者選擇啟動於 i686 和 x86_64 模式的混合映象檔。 請注意映象檔內不包含任何套件包：安裝程序必須從套件庫取得套件包，所以必須擁有能夠運行的網路環境。 下載後，用下載頁提供的 PGP 或 CHECKSUM 簽證碼 檢驗映像檔 (例如 `pacman-key -v *inst-image.iso*.sig`、`md5sum *inst-image.iso*`) 。 最後映像檔可以燒製成 CD、以 ISO 檔型式掛載，或是[直接寫入 USB 碟](/index.php/USB_Installation_Media_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "USB Installation Media (正體中文)")。

## 前期安裝流程

啟動安裝映象後，必須執行下列步驟來初始化安裝程序。

### 鍵盤配置

預設鍵盤配置是 US. 其它的鍵盤配置可以 `loadkeys *keymap_file*` 改變: keymap 檔存放在 `/usr/share/kbd/keymaps/` (路徑和副檔名可以省略)。

### 分割硬碟

詳情請參閱[硬碟分割](/index.php/Partitioning "Partitioning")。

如果您想要建立給 [LVM](/index.php/LVM "LVM")、[硬碟加密](/index.php/Disk_encryption "Disk encryption")或 [RAID](/index.php/RAID "RAID") 的堆疊區塊設備，請先完成它。

若您使用的是 (U)EFI，很可能需要另一個 UEFI 系統分割區。請參閱 [Linux 下建立 UEFI 系統分割區](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface")。

### 格式化分割區

詳情請參閱[檔案系統](/index.php/File_systems#Step_2:_create_the_new_file_system "File systems")。

### 掛載分割區

現在您必須將根目錄分割區掛載至 `/mnt`。接著，您也需要為其他分割區 (`/mnt/boot`, `/mnt/home`, ...) 建立目錄並掛載，並記得掛載您的 "swap" 分割區，如此一來 "genfstab" 才偵測得到它們。

### 連接網路

預設對所有可用的裝置啟用了 DHCP 服務。若您需要設定固定 IP，或是使用 [Netctl](/index.php/Netctl "Netctl") ，都應該先暫停此服務：`systemctl stop dhcpcd.service`。更多資訊請參閱[網路設定](/index.php/Network_Configuration_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Network Configuration (正體中文)")。

### 無線網路

執行 `wifi-menu` 以設定無線網路。詳情請參閱[無線網路設定](/index.php/Wireless_Setup "Wireless Setup")與 [Netctl](/index.php/Netctl "Netctl")。

### 安裝基本系統

在安裝之前，請先編輯 `/etc/pacman.d/mirrorlist` ，將適當的[鏡像站](/index.php/Mirrors "Mirrors")放在檔案的最前面。`pacstrap` 會在安裝過程中複製一份 mirrorlist 文件到新系統內，所以最好現在就把它設定好。

我們將使用 [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) 這支腳本來安裝基本系統。

```
# pacstrap /mnt base

```

在上述的指令後面加上其他軟體包的名稱來安裝 (用空白分隔)，例如開機載入程式。

### 設定系統

*   使用以下指令產生 [fstab](/index.php/Fstab "Fstab") (若您偏好使用 UUID 或標籤，請分別加上 `-U` 或 `-L` 選項，擇一即可)：

	 `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   用 [chroot](/index.php/Chroot "Chroot") 切換至全新安裝的系統：

	 `# arch-chroot /mnt` 

*   在 `/etc/hostname` 裡寫入指定的主機名稱。

*   建立軟連結 `/etc/localtime`，連向 `/usr/share/zoneinfo/Zone/SubZone`。將 `Zone` 和 `Subzone` 換成您所在的時區。例如：

	 `# ln -s /usr/share/zoneinfo/Asia/Taipei /etc/localtime` 

*   取消 `/etc/locale.gen` 內的註解以選擇語系，並使用 `locale-gen` 產生它們。
*   在 `/etc/locale.conf` 內設定[本地化](/index.php/Locale#Setting_system-wide_locale "Locale")。
*   在 `/etc/vconsole.conf` 內新增[終端機鍵盤布局](/index.php/KEYMAP "KEYMAP")與[終端機字型](/index.php/Fonts_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E7.B5.82.E7.AB.AF.E6.A9.9F.E5.AD.97.E5.9E.8B "Fonts (正體中文)")的偏好設定。
*   依需求設定 `/etc/mkinitcpio.conf` (參閱 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") )，並建立一個初始 RAM 碟：

	 `# mkinitcpio -p linux` 

*   用 `passwd` 設定 root 帳號的密碼。
*   為新安裝的系統設定網路。參閱[網路設定](/index.php/Network_Configuration_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Network Configuration (正體中文)")和[無線網路設定](/index.php/Wireless_Setup "Wireless Setup")。

### 安裝並設定開機載入程式

有數種選擇可供使用；參閱[開機載入程式](/index.php/Boot_loaders "Boot loaders")。

### 卸載並重啟系統

如果您還在 chroot 的環境內，請先輸入 `exit` 或按下 `Ctrl+D` 來離開 chroot 環境。 為了卸載先前我們在 `/mnt` 下所掛載的分割區。透過以下步驟來卸載它們：

```
# umount -R /mnt

```

現在請重啟系統，並使用 root 帳號來登入新的系統。

## 安裝完成後

安裝好 Arch 以後，也請參考[一般建議](/index.php/General_Recommendations_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "General Recommendations (正體中文)")內的設定教學，例如設定圖形界面、音效、觸控板等等。

好奇 Arch 下有什麼吸引人的應用程式嗎？請參考[應用程式清單](/index.php/List_of_applications "List of applications")。