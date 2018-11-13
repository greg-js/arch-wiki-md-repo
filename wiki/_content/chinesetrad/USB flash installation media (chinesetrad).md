相關文章

*   [CD 燒錄 (英)](/index.php/CD_Burning "CD Burning")
*   [Archiso (英)](/index.php/Archiso "Archiso")

**翻譯狀態：** 本文章是 [USB_Flash_Installation_Media](/index.php/USB_Flash_Installation_Media "USB Flash Installation Media") 的翻譯版本。最近一次的翻譯時間：2014-02-02。點擊[本連結](https://wiki.archlinux.org/index.php?title=USB_Flash_Installation_Media&diff=0&oldid=295276)查看英文頁面之後的變更。

本頁面將討論各種將 Arch Linux 映像寫入 USB 裝置 (又稱「快閃碟」、「USB 隨身碟」、「USB 鍵」等)，並在 BIOS 和 UEFI 系統上開機的跨平台方式。裝載進 USB 裝置的 LiveUSB (類似於 LiveCD) 系統可以用來安裝 Arch Linux，系統維護或救援資料，其本質為 [SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS") 系統，關機之後所有的變更都會消失無蹤。

如果要將 Arch Linux 完整的裝入 USB 裝置 (即所有更改皆永遠有效)，請參閱[安裝 Arch Linux 至 USB 碟](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")。如果要使用可開機的 Arch Linux USB 隨身碟當作救援用 USB，請參閱[更換根目錄 (chroot)](/index.php/Change_root "Change root")。

## Contents

*   [1 BIOS 和 UEFI 可開機 USB](#BIOS_和_UEFI_可開機_USB)
    *   [1.1 使用 dd](#使用_dd)
        *   [1.1.1 GNU/Linux](#GNU/Linux)
        *   [1.1.2 Windows](#Windows)
            *   [1.1.2.1 使用 Cygwin](#使用_Cygwin)
            *   [1.1.2.2 Windows 下使用 dd](#Windows_下使用_dd)
        *   [1.1.3 Mac OS X](#Mac_OS_X)
        *   [1.1.4 如何還原 USB 裝置](#如何還原_USB_裝置)
    *   [1.2 手動格式化](#手動格式化)
        *   [1.2.1 GNU/Linux](#GNU/Linux_2)
        *   [1.2.2 Windows](#Windows_2)
*   [2 適用於 BIOS 系統的其他方式](#適用於_BIOS_系統的其他方式)
    *   [2.1 GNU/Linux](#GNU/Linux_3)
        *   [2.1.1 使用 UNetbootin](#使用_UNetbootin)
    *   [2.2 Windows](#Windows_3)
        *   [2.2.1 Win32 Disk Imager](#Win32_Disk_Imager)
        *   [2.2.2 Windows 下的 USBWriter](#Windows_下的_USBWriter)
        *   [2.2.3 Flashnul 方式](#Flashnul_方式)
        *   [2.2.4 從 RAM 載入安裝媒體](#從_RAM_載入安裝媒體)
            *   [2.2.4.1 準備 USB 隨身碟](#準備_USB_隨身碟)
            *   [2.2.4.2 將所需檔案複製到 USB 隨身碟](#將所需檔案複製到_USB_隨身碟)
            *   [2.2.4.3 建立設定檔案](#建立設定檔案)
            *   [2.2.4.4 最後步驟](#最後步驟)
        *   [2.2.5 Universal USB Installer](#Universal_USB_Installer)
*   [3 疑難排解](#疑難排解)
*   [4 另請參閱](#另請參閱)

## BIOS 和 UEFI 可開機 USB

### 使用 dd

**註記:** 建議使用這個方式，因為比較簡單。如果沒有用，改用下一個方式：[#手動格式化](#手動格式化)。

**警告:** 這會摧毀 `/dev/sd**x**` 上所有的資料，無法還原！

#### GNU/Linux

**提示：** **不要**掛載 USB 碟安裝媒體，可以用 `lsblk` 檢查。

**註記:** 使用 `/dev/sd**x**` 而非 `/dev/sd**x1**`，調整 **x** 為您的目標裝置。

```
# dd bs=4M if=/path/to/archlinux.iso of=/dev/sd**x** && sync

```

#### Windows

##### 使用 Cygwin

確認您安裝的 [Cygwin](http://www.cygwin.com/) 有包含 `dd` 軟體包。

**提示：** 若您不想安裝 Cygwin，也可以從[這裡](http://www.chrysocome.net/dd)單獨下載 Windows 版的 `dd`。更多資訊請參閱下一節。

將映像檔放在您的使用者目錄下，例如：

```
C:\cygwin\home\John\

```

以系統管理員身分執行 cygwin (這樣 cygwin 才能存取硬體)。使用以下指令寫入 USB 碟：

```
dd if=image.iso of=\\.\[x]: bs=4M

```

image.iso 代表 `cygwin` 目錄下 ISO 映像檔的所在路徑。 `\\.\[**x**]:` 代表您的 USB 隨身碟，其中 **x** 是 Windows 為該 USB 裝置指定的代號取代，例如 `\\.\d:`。

在 Cygwin 6.0 下，找出正確的分割區：

```
cat /proc/partitions

```

並根據輸出的資訊，將 ISO 映像寫入指定地點。範例如下：

**警告:** 您的 USB 碟上的所有檔案都會被刪除且無法還原。繼續執行前，請確認隨身碟上面沒有任何重要檔案。

```
dd if=image.iso of=/dev/sdb bs=4M

```

##### Windows 下使用 dd

**註記:** 某些使用者用此方法製作的媒體開機時，碰到「isolinux.bin missing or corrupt」問題。

您可以從 [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd) 下載 dd 的 Windows 版本 (以 GPL 授權)。比起用 Cygwin，好處是下載量變小了。其餘請根據上述的 Cygwin 步驟。

下載最新版本的 Windows 版 dd。下載好之後，將壓縮檔的內容提取出來，放「下載」或其他地方都可。

現在用管理員身分開啟`命令提示字元`。接著用 `cd` 指令進入「下載」目錄。

若您的 your Arch Linux ISO 位在其他地方，將需要指定完整路徑，為了方便起見，將 Arch Linux ISO 放在與 dd 執行檔同一個目錄底下。指令的基本格式看起來像這樣。

 `dd if=archlinux-2013-XX-xx-dual.iso of=\\.\x: bs=4m` 
**警告:** 這個指令會將裝置的內容與格式替換為 ISO 的。若複製出了意外，很有可能無法復原原本的內容。執行以前請再三確認 dd 指向的是正確的裝置！

在空白的欄位 (以「x」指示) 補齊正確的日期與裝置字母。

以下為完整範例。

 `dd if=ISOs\archlinux-2013.08.01-dual.iso of=\\.\d: bs=4M` 

#### Mac OS X

在 Mac 底下，要使用 `dd` 修改 USB 裝置之前，您必須先作幾項修正。首先插入 USB 裝置，OS X 會自動掛載。接著在 `Terminal.app` (終端機) 中執行

```
$ diskutil list

```

用 `mount` 或 `sudo dmesg | tail` 找到您的 USB 裝置代號 (如 `/dev/disk1`)，並卸載裝置上的分割區 (就是 /dev/disk1s1)，同時保持裝置 (就是 /dev/disk1)：

```
$ diskutil unmountDisk /dev/disk1

```

現在我們可以照上述的指示進行 (若您使用的是 OS X 的 `dd`，請改使用 `bs=8192`，此數字來自於 `1024*8`)。

 `dd if=image.iso of=/dev/disk1 bs=8192` 
```
20480+0 records in
20480+0 records out
167772160 bytes transferred in 220.016918 secs (762542 bytes/sec)

```

在拔除您的裝置前，請先記得將它退出：

```
$ diskutil eject /dev/disk1

```

#### 如何還原 USB 裝置

ISO 映像是可以燒錄至光碟，也可以直接寫入 USB 裝置的混合文件系統，因此它並不需要包含正規的分割表。

Arch Linux 安裝完成後，若您確定不再使用裡面的安裝媒體，要恢復該 USB 碟原本的大小，必須清理它的前 512 位元組 **(也就是 MBR 內的開機碼與以及非正規分割表)**：

```
# dd count=1 bs=512 if=/dev/zero of=/dev/sd**x** && sync

```

接著用 [gparted](https://www.archlinux.org/packages/?name=gparted)，或是從終端機建立新的分割表 (如「msdos」) 以及檔案系統(如 EXT4、FAT32)：

*   EXT2/3/4 (依需求調整)：

```
# cfdisk /dev/sd**x**
# mkfs.ext4 /dev/sd**x1**
# e2label /dev/sd**x1** USB_STICK

```

*   FAT32，安裝 [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) 軟體包後執行：

```
# cfdisk /dev/sd**x**
# mkfs.vfat -F32 /dev/sd**x1**
# dosfslabel /dev/sd**x1** USB_STICK

```

### 手動格式化

#### GNU/Linux

比起直接用 `dd` 寫入映像，這種方式比較複雜，但好處是完成後裝置依然可以儲存資料。

*   確認系統上已經安裝最新的 *syslinux* 軟體包 (版本 6.02 以上)。

*   裝置使用 MBR (msdos) 分割表，並已存在至少一個分割區使用 FAT32 檔案系統。如果沒有，請先建立好分割區和檔案系統再繼續。

*   掛載 ISO 映像。

```
# mkdir -p /mnt/iso
# mount -o loop archlinux-2013.10.01-dual.iso /mnt/iso

```

**註記:** 將以下指令中的 `/dev/sd**X**1` 調整為您實際系統的對應部分。

*   掛載 USB 隨身碟上的 FAT32 檔案系統，並將 ISO 的內容複製到上面。

```
# mkdir -p /mnt/usb
# mount /dev/sd**X**1 /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/{usb,iso}

```

*   調整設定檔 archiso_sys32 與 archiso_sys64。 (非 [Archiso](/index.php/Archiso "Archiso")) 則跳過此步驟。這個指令會將兩個檔案中的 archisolabel 參數 (如 `archisolabel=ARCH_2014XX`) 替換成 archisodevice 參數 (如 `archiso**device**=/dev/disk/by-uuid/47FA-4071`)。

**警告:** 若硬碟的標記 `ARCH_2014XX` (釋出月份) 或 [UUID](/index.php/UUID "UUID") (視情況而定) 設錯，建立的媒體將無法用來開機。

```
$ sed -i "s|label=ARCH_.*|device=/dev/disk/by-uuid/$(blkid -o value -s UUID /dev/sd**X**1)|" archiso_sys{32,64}.cfg

```

**註記:** 記得按照實際狀況調整 `/dev/sd**X**1`。

*   根據 [Syslinux#手動安裝](/index.php/Syslinux#Manual_install "Syslinux")的步驟，為隨身碟安裝 Syslinux。將 USB (來源自 ISO) 底下存在的所有 syslinux 模組 (`*.c32` 檔案) 都用 syslinux 軟體包提供的檔案覆蓋過去。這可以有效避免因版本不同而觸發的開機失敗。

*   根據 [Syslinux#MBR 分割表](/index.php/Syslinux#MBR_partition_table "Syslinux")的步驟，將該分割區標記為 active。

#### Windows

**註記:**

*   不要用任何「可開機 USB 建立工具」建立 UEFI 可開機 USB。不要用「dd 的 Windows 版本」將 ISO 拷進 USB 隨身碟。

*   以下的指令中，**X:** 代表 Windows 給 USB 隨身碟的代號。

*   Windows 使用反斜線 `\` 表示路徑，如以下指令所示。

*   所有指令必須「以系統管理員身分」在 Windows 的命令列下執行。

*   `>` 這個符號代表 Windows 的命令提示字元。

*   使用 [Rufus USB partitioner](http://rufus.akeo.ie/) 分割並格式化 USB 隨身碟。選擇 **MBR for BIOS and UEFI** 分割計劃選項，檔案系統選擇 **FAT32**。取消勾選「Create a bootable disk using ISO image」和「Create extended label and icon files」選項。

*   將 USB 隨身碟 `X:` 的 **Volume Label** (標籤) 修改成 `<ISO>\loader\entries\archiso-x86_64.conf` 中 `archisolabel=` 部分的 LABEL 名稱。官方 ISO ([Archiso](/index.php/Archiso "Archiso")) 需要這項步驟，

*   將 ISO 解壓縮 (和解壓縮 ZIP 檔一樣) 到 USB 隨身碟 (使用 [7-Zip](http://7-zip.org/))。

*   從 [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) 下載官方最新 syslinux 6.xx 執行檔 (zip 檔)，將它解壓縮。

*   執行以下指令 (在 Windows 命令提示字元下，用系統管理員身分執行)：

*   執行以下指令將 Syslinux 安裝到 USB (64 位元版 Windows 得使用 `win64\syslinux64.exe`)：

**註記:** Archboot ISO 請使用 `/boot/syslinux`。

```
> cd bios\
> win32\syslinux.exe -d /arch/boot/syslinux -i -a -m X:

```

**註記:**

*   上述的步驟會安裝 Syslinux `ldlinux.sys` 到 USB 的分割區 VBR，在 MBR 分割表內設定分割區為 active/boot，並將 MBR 開機碼寫進 USB 最前面的 400 位元組內。

*   有 `-d` 選項，請使用斜線表示路徑，就跟 *unix 系統下的方式相同。

## 適用於 BIOS 系統的其他方式

### GNU/Linux

#### 使用 UNetbootin

UNetbootin 可以將 ISO 複製到 USB 裝置，可在任何 Linux 發行版或 Windows 上使用。不過 Unetbootin 會覆寫 syslinux.cfg，因此建立出來的 USB 裝置將無法正常啟動。基於這個原因，**我們並不推薦 Unetbootin** -- 請使用 `dd` 或本主題提出的任一種方式。

**警告:** UNetbootin 將覆寫預設的 `syslinux.cfg`；必須恢復才能讓 USB 裝置正確啟動。

編輯 `syslinux.cfg`：

 `sysconfig.cfg` 
```
default menu.c32
prompt 0
menu title Archlinux Installer
timeout 100

label unetbootindefault
menu label Archlinux_x86_64
kernel /arch/boot/x86_64/vmlinuz
append initrd=/arch/boot/x86_64/archiso.img archisodevice=/dev/sd**x1** ../../

label ubnentry0
menu label Archlinux_i686
kernel /arch/boot/i686/vmlinuz
append initrd=/arch/boot/i686/archiso.img archisodevice=/dev/sd**x1** ../../
```

根據要安裝 Arch Linux 的系統所用掉的字母，將 `/dev/sd**x1**` 中的 **x** 替換成第一個可用字母 (例如：有兩顆硬碟就使用 `c`)。您可以在開機的第一階段、顯示開機選單時再按 `Tab` 改變設定。

### Windows

#### Win32 Disk Imager

**警告:** 這會摧毀 USB 隨身碟上的所有資訊！

首先，從[這裡](http://sourceforge.net/projects/win32diskimager/)下載程式。接著解壓縮並執行可執行檔。現在，在 `Image File` (映像檔) 一區選擇 Arch Linux ISO，`Device` (裝置) 一區選擇 USB 裝置字母 (例如 [D:\])。最後，準備好之後點選 `Write` (寫入)。

**提示：** 預設 Win32 Disk Imager 的檔案瀏覽會認為映像檔的副檔名為 `.img`。您可以輕易將 `Files of type` (檔案類型) 下拉選單改為 `*.*`，再選擇 Arch Linux ISO。

**註記:** 安裝完成後，若需要還原 USB 裝置，請依照[這裡](#如何還原_USB_裝置)所寫的步驟進行。

#### Windows 下的 USBWriter

從 [http://sourceforge.net/projects/usbwriter/](http://sourceforge.net/projects/usbwriter/) 下載程式後執行。選擇 Arch 映像檔、目標 USB 碟，並點擊 `write` (寫入) 按鈕。您現在應該可以用 USB 碟開機並安裝 Arch Linux 了。

#### Flashnul 方式

[flashnul](http://shounen.ru/soft/flashnul/) 是一套檢驗快閃記憶體 (如 USB-Flash, IDE-Flash, SecureDigital, MMC, MemoryStick, SmartMedia, XD, CompactFlash) 功能與狀況的工具程式。

在指令列呼叫 flashnul 與 `-p` 選項，找出您的 USB 裝置是哪個代號。如下：

 `C:\>flashnul -p` 
```
Avaible physical drives:
Avaible logical disks:
C:\
D:\
E:\

```

決定好正確的裝置後，以裝置代號 `-L` 與映像路徑呼叫 flashnul，在該裝置上寫入映像，如下：

```
C:\>flashnul **E:** -L *path\to\arch.iso*

```

萬般確認後，輸入 yes 開始寫入資料，請稍待片刻等寫入動作完成。若發生「拒絕存取」錯誤，關掉所有開啟的檔案總管視窗。

Vista 或 Win7 的使用者，請以系統管理員的身分啟動終端機，否則 flashnul 會無法以區塊裝置的方式開啟隨身碟，只能經由 Windows 提供的驅動寫入。

**註記:** 請確認您使用的是裝置符號，而非數字。flashnul 1rc1, Windows 7 x64.

#### 從 RAM 載入安裝媒體

這個方式使用 [Syslinux](/index.php/Syslinux "Syslinux") 和 [Ramdisk](/index.php/Ramdisk "Ramdisk") ([MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)) 將整個 Arch Linux ISO 載入記憶體 (RAM)。整個 Live 環境將完全在系統記憶體上執行，因此您需要確定系統的記憶體容量足夠。以 MEMDISK 為基礎的 Arch Linux 安裝最低 RAM 需求大小為 500 MB 到 1 GB 之間。

更多 Arch Linux 與 MEMDISK 的系統要求，請參閱[新手教學](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' guide (正體中文)")以及[這裡](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries)。

**提示：** 一旦安裝程序徹底載入完畢，就可以移除 USB 隨身碟，將它插入不同機器後可以重新進行安裝步驟。可利用式 MEMDISK 也允許啟動並安裝 Arch Linux 到原本用來安裝的 USB 隨身碟上。

##### 準備 USB 隨身碟

一開始，將 USB 隨身碟格式化為 **FAT32**。接著，在新格式化的隨身碟上建立以下資料夾。

*   `Boot`
    *   `Boot/ISOs`
    *   `Boot/Settings`

##### 將所需檔案複製到 USB 隨身碟

下一步，將要啟動的 ISO 複製到 `Boot/ISOs` 資料夾。接著，從[這裡](http://www.kernel.org/pub/linux/utils/boot/syslinux/)下載最新版本的 [syslinux](https://www.archlinux.org/packages/?name=syslinux)，解開以下檔案後複製到以下資料夾。

*   `./win32/syslinux.exe` 放到系統的「桌面」或「下載」資料夾。
*   `./memdisk/memdisk` 放到 USB 隨身碟的 `Settings` 資料夾。

##### 建立設定檔案

複製好所需檔案之後，進入 USB 隨身碟的 /boot/Settings 並建立 `syslinux.cfg` 檔案。

**警告:** 在 `INITRD` 這一行，要使用複製進 `ISOs` 資料夾的 ISO 檔案名稱！
 `/Boot/Settings/syslinux.cfg` 
```
DEFAULT arch_iso

LABEL arch_iso
        MENU LABEL Arch Setup
        LINUX memdisk
        INITRD /Boot/ISOs/archlinux-2013.08.01-dual.iso
        APPEND iso
```

更多 Syslinux 的資訊請參閱 [Arch Wiki 文章](/index.php/Syslinux "Syslinux")。

##### 最後步驟

最後，在 `syslinux.exe` 所在位置建立 `*.bat` 檔案，並執行 (Vista 或 Windows 7 使用者請「以系統管理員身分執行」)：

 `C:\Documents and Settings\username\Desktop\install.bat` 
```
@echo off
syslinux.exe -m -a -d /Boot/Settings X:
```

#### Universal USB Installer

Windows 下有個工具 [[1]](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/) 可以快速建立內含多個 Linux 發行版安裝程式的 LiveUSB。另外，這些安裝程式可隨意新增、移除，不需要重新格式化 USB 隨身碟。

## 疑難排解

*   若您使用 [MEMDISK 方法](#從_RAM_載入安裝媒體)，在啟動 i686 版本時發生惡名昭彰的「30 秒」錯誤，在 `Boot Arch Linux (i686)` 選項上按下 `Tab` 鍵，在結尾加上 `vmalloc=448M`。也請參考：「若映像大於 128MiB 且使用 32 位元 OS，應增加 vmalloc 的最大記憶體用量」。[[2]](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

*   若「30 秒」錯誤是肇因於 `/dev/disk/by-label/ARCH_XXXXXX` 未被掛載，試著重新命名 USB 媒體為 `ARCH_XXXXXX` (如 `ARCH_201302`)。

## 另請參閱

*   [Gentoo wiki - LiveUSB/HOWTO](https://wiki.gentoo.org/wiki/LiveUSB/HOWTO)
*   [Fedora wiki - How to create and use Live USB](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)
*   [openSUSE wiki - SDB:Live USB stick](http://en.opensuse.org/SDB:Live_USB_stick)