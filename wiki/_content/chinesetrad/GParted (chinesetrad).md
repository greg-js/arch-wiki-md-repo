**翻譯狀態：** 本文章是 [GParted](/index.php/GParted "GParted") 的翻譯版本。最近一次的翻譯時間：2014-01-27。點擊[本連結](https://wiki.archlinux.org/index.php?title=GParted&diff=0&oldid=294554)查看英文頁面之後的變更。

[GParted](http://gparted.sourceforge.net/index.php) 是 GNU Parted 的 GTK+ 前端，也是 GNOME 官方指定的分割區編輯程式。它可以建立/刪除/縮放/檢查幾乎[所有檔案格式](http://gparted.sourceforge.net/features.php)的分割區，還可以管理硬碟標籤、旗標和複製/貼上整塊分割區。GParted 收錄於 extra 庫，還有 [Live CD](http://gparted.sourceforge.net/download.php) 版本。一個需要下載 Live CD 的場合是，調整平常無法卸載的根檔案系統所在分割區。

**警告:** GParted 可以讀寫您的硬碟分割區，因此若不慎使用會導致資料遺失。建議您在使用 GParted 之前先備份受影響的分割區。

## Contents

*   [1 安裝到 Arch](#.E5.AE.89.E8.A3.9D.E5.88.B0_Arch)
    *   [1.1 選用相依性](#.E9.81.B8.E7.94.A8.E7.9B.B8.E4.BE.9D.E6.80.A7)
        *   [1.1.1 檔案系統](#.E6.AA.94.E6.A1.88.E7.B3.BB.E7.B5.B1)
        *   [1.1.2 額外功能](#.E9.A1.8D.E5.A4.96.E5.8A.9F.E8.83.BD)
*   [2 GParted 支援](#GParted_.E6.94.AF.E6.8F.B4)
*   [3 提示與技巧](#.E6.8F.90.E7.A4.BA.E8.88.87.E6.8A.80.E5.B7.A7)
    *   [3.1 將 GParted-live 新增至您的 GRUB 選單](#.E5.B0.87_GParted-live_.E6.96.B0.E5.A2.9E.E8.87.B3.E6.82.A8.E7.9A.84_GRUB_.E9.81.B8.E5.96.AE)
    *   [3.2 與 Windows XP 雙重開機](#.E8.88.87_Windows_XP_.E9.9B.99.E9.87.8D.E9.96.8B.E6.A9.9F)
    *   [3.3 修復混亂的分割區順序](#.E4.BF.AE.E5.BE.A9.E6.B7.B7.E4.BA.82.E7.9A.84.E5.88.86.E5.89.B2.E5.8D.80.E9.A0.86.E5.BA.8F)
    *   [3.4 從選單啟動 GParted](#.E5.BE.9E.E9.81.B8.E5.96.AE.E5.95.9F.E5.8B.95_GParted)

## 安裝到 Arch

從[官方軟體庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")[安裝](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") [gparted](https://www.archlinux.org/packages/?name=gparted)。

### 選用相依性

#### 檔案系統

GParted 軟體包本身並不支援所有檔案系統。以下列舉了不同檔案系統支援所需安裝的軟體包：

| **Arch 軟體包** | **檔案系統** |
| [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | [Btrfs](/index.php/Btrfs "Btrfs") |
| [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | fat16/32 |
| [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | ext2/[ext3](/index.php/Ext3 "Ext3")/[ext4](/index.php/Ext4 "Ext4") (v1.41+) |
| [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | exfat |
| [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | [F2FS](/index.php/F2FS "F2FS") |
| [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | [JFS](/index.php/JFS "JFS") |
| [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | [NTFS](/index.php/NTFS "NTFS") |
| [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | [Reiser4](/index.php/Reiser4 "Reiser4") |
| [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Reiser3 |
| [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | [XFS](/index.php/XFS "XFS") |

#### 額外功能

| **Arch 軟體包** | **功能** |
| [mtools](https://www.archlinux.org/packages/?name=mtools) | MSDOS 硬碟適用的工具。如果您要更改 FAT 分割區的標籤，就需要這個。 |

若您透過 pacman 安裝 GParted，pacman 也會幫您列舉這些選用軟體包。

## GParted 支援

若您不確定某個指令的作用為何，可以參考[官方 GParted 論壇](http://gparted-forum.surf4.info/)。

## 提示與技巧

### 將 GParted-live 新增至您的 GRUB 選單

將 GParted-live 新增至您的 GRUB 選單的步驟，請參閱 [Gparted-Live](/index.php/Gparted-Live "Gparted-Live") wiki 文章。好處是您可以直接從 GRUB 啟動進 GParted-live CD 的 live 環境，不需要另外準備一片 CD！

### 與 Windows XP 雙重開機

如果您打算將一個同時屬於開機分割區的 Windows XP 分割區移動到另一顆硬碟，只要將以下的登錄機碼刪除，之後就可以用 GParted 輕易的進行，Windows 不會抱怨的：

```
HKEY_LOCAL_MACHINE\SYSTEM\MountedDevices

```

相關資料請參考[這裡](http://gparted-forum.surf4.info/viewtopic.php?pid=8347#p8347)。

### 修復混亂的分割區順序

如果您的硬碟上有邏輯分割區，刪除其中一個可能會導致分割區順序混亂。例如以下的範例：

```
/dev/sda1 (主要分割區)
/dev/sda2 (主要分割區)
/dev/sda3 (主要分割區)
/dev/sda4 (**延伸**分割區)
/dev/sda5 (邏輯分割區)
/dev/sda6 (邏輯分割區)
/dev/sda7 (邏輯分割區)

```

1-3 是主要分割區。5-6 是隸屬於延伸分割區 (4) 的邏輯分割區。假設您砍掉 `/dev/sda5`，並將 `/dev/sda2` 複製一份到釋出的空間上。現在您的硬碟會長得像這樣：

```
/dev/sda1 (主要分割區)
/dev/sda2 (主要分割區)
/dev/sda3 (主要分割區)
/dev/sda4 (**延伸**分割區)
/dev/sda7 (邏輯分割區)
/dev/sda5 (邏輯分割區)
/dev/sda6 (邏輯分割區)

```

注意到在刪除、複製/貼上分割區之後，分割區的順序被弄亂了。這可能會導致各種問題：無法順利掛載分割區、出現 GRUB 錯誤 17「無任何可開機系統」等等。解決這個小麻煩的方法相當簡單：

1.  用您的 Arch Live CD、GParted Live CD (或任何其他 live Linux CD) 啟動系統
2.  執行 fdisk，選擇硬碟，進入進階模式，修復分割區順序，並將變更寫回硬碟

範例 (假設使用 `/dev/sda`)：

```
# fdisk /dev/sda

```

1.  進入 fdisk 後，選擇 `x` 選項 (額外功能 (限進階使用)) 並按 enter
2.  接著選擇 `f` 選項 (修復分割區順序) 並按 enter
3.  接著選擇 `w` 選項 (寫入分割表到硬碟後離開) 並按 enter

**註記:** 您必須以 root 身分執行 **partprobe**，或是重新開機，這樣核心才能夠讀取新的分割表！

### 從選單啟動 GParted

如果您從選單 (例如 xfce 的應用程式選單) 載入 GParted 時發生任何問題，安裝 [polkit](https://www.archlinux.org/packages/?name=polkit) 軟體包，並設定為和作業階段一同啟動。