# pacman (正體中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**翻譯狀態：** 本文章是 [pacman](/index.php/Pacman "Pacman") 的翻譯版本。最近一次的翻譯時間：2013-12-22。點擊[本連結](https://wiki.archlinux.org/index.php?title=pacman&diff=0&oldid=289055)查看英文頁面之後的變更。

相關文章

*   [降級軟體包 (英)](/index.php/Downgrading_packages "Downgrading packages")
*   [增進 Pacman 效能 (英)](/index.php/Improve_pacman_performance "Improve pacman performance")
*   [Pacman GUI 前端 (英)](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")
*   [Pacman Rosetta (英)](/index.php/Pacman_Rosetta "Pacman Rosetta")
*   [Pacman 提示 (英)](/index.php/Pacman_tips "Pacman tips")
*   [Pacman 軟體包簽署 (英)](/index.php/Pacman_package_signing "Pacman package signing")
*   [常見問答#軟體包管理](/index.php/FAQ_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E8.BB.9F.E9.AB.94.E5.8C.85.E7.AE.A1.E7.90.86 "FAQ (正體中文)")
*   [pacman-key (英)](/index.php/Pacman-key "Pacman-key")
*   [Pacnew 和 Pacsave 檔案](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files")
*   [應用程式清單/工具#軟體包管理 (英)](/index.php/List_of_Applications/Utilities#Package_management "List of Applications/Utilities")
*   [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")
*   [官方軟體庫](/index.php/Official_Repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official Repositories (正體中文)")
*   [Arch 使用者倉庫](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")

**[Pacman](https://www.archlinux.org/pacman/)** [軟體包管理員](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system")是 Arch Linux 的主要特色工具，結合了二進位軟體包格式和容易使用的[組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")。輕鬆管理軟體是 Pacman 的目標，無論這些軟體包是來自[官方軟體庫](/index.php/Official_Repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official Repositories (正體中文)")還是由使用者自建。

Pacman 會和主要伺服器同步軟體包清單，來保持系統處於最新狀態。在主從式架構之下，使用者只要用簡單的指令就可以下載並安裝軟體包，並補足所有相依的軟體包。

Pacman 以 C 語言撰寫，使用 `.pkg.tar.xz` 軟體包格式。

**提示:** 官方的 [pacman](https://www.archlinux.org/packages/?name=pacman) 已提供了不少好用工具 (如 **makepkg**, **pactree**, **vercmp** 以及更多)：執行 `pacman -Ql pacman | grep bin` 可查看完整清單。

## Contents

*   [1 設定](#.E8.A8.AD.E5.AE.9A)
    *   [1.1 一般選項](#.E4.B8.80.E8.88.AC.E9.81.B8.E9.A0.85)
        *   [1.1.1 跳過特定軟體包的升級](#.E8.B7.B3.E9.81.8E.E7.89.B9.E5.AE.9A.E8.BB.9F.E9.AB.94.E5.8C.85.E7.9A.84.E5.8D.87.E7.B4.9A)
        *   [1.1.2 跳過特定軟體群組的升級](#.E8.B7.B3.E9.81.8E.E7.89.B9.E5.AE.9A.E8.BB.9F.E9.AB.94.E7.BE.A4.E7.B5.84.E7.9A.84.E5.8D.87.E7.B4.9A)
        *   [1.1.3 禁止特定檔案安裝至系統](#.E7.A6.81.E6.AD.A2.E7.89.B9.E5.AE.9A.E6.AA.94.E6.A1.88.E5.AE.89.E8.A3.9D.E8.87.B3.E7.B3.BB.E7.B5.B1)
    *   [1.2 軟體庫](#.E8.BB.9F.E9.AB.94.E5.BA.AB)
    *   [1.3 軟體包的安全性](#.E8.BB.9F.E9.AB.94.E5.8C.85.E7.9A.84.E5.AE.89.E5.85.A8.E6.80.A7)
*   [2 使用方式](#.E4.BD.BF.E7.94.A8.E6.96.B9.E5.BC.8F)
    *   [2.1 安裝軟體包](#.E5.AE.89.E8.A3.9D.E8.BB.9F.E9.AB.94.E5.8C.85)
        *   [2.1.1 安裝特定軟體包](#.E5.AE.89.E8.A3.9D.E7.89.B9.E5.AE.9A.E8.BB.9F.E9.AB.94.E5.8C.85)
        *   [2.1.2 安裝軟體群組](#.E5.AE.89.E8.A3.9D.E8.BB.9F.E9.AB.94.E7.BE.A4.E7.B5.84)
    *   [2.2 移除軟體包](#.E7.A7.BB.E9.99.A4.E8.BB.9F.E9.AB.94.E5.8C.85)
    *   [2.3 升級軟體包](#.E5.8D.87.E7.B4.9A.E8.BB.9F.E9.AB.94.E5.8C.85)
    *   [2.4 查詢軟體包資料庫](#.E6.9F.A5.E8.A9.A2.E8.BB.9F.E9.AB.94.E5.8C.85.E8.B3.87.E6.96.99.E5.BA.AB)
    *   [2.5 其他指令](#.E5.85.B6.E4.BB.96.E6.8C.87.E4.BB.A4)
    *   [2.6 不支援部分升級](#.E4.B8.8D.E6.94.AF.E6.8F.B4.E9.83.A8.E5.88.86.E5.8D.87.E7.B4.9A)
    *   [2.7 基本注意事項](#.E5.9F.BA.E6.9C.AC.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A0.85)
*   [3 疑難排解](#.E7.96.91.E9.9B.A3.E6.8E.92.E8.A7.A3)
    *   [3.1 升級某個軟體包後，我的系統故障了！](#.E5.8D.87.E7.B4.9A.E6.9F.90.E5.80.8B.E8.BB.9F.E9.AB.94.E5.8C.85.E5.BE.8C.EF.BC.8C.E6.88.91.E7.9A.84.E7.B3.BB.E7.B5.B1.E6.95.85.E9.9A.9C.E4.BA.86.EF.BC.81)
    *   [3.2 我知道某個軟體包升級已經釋出，但 Pacman 說我的系統已經是最新的！](#.E6.88.91.E7.9F.A5.E9.81.93.E6.9F.90.E5.80.8B.E8.BB.9F.E9.AB.94.E5.8C.85.E5.8D.87.E7.B4.9A.E5.B7.B2.E7.B6.93.E9.87.8B.E5.87.BA.EF.BC.8C.E4.BD.86_Pacman_.E8.AA.AA.E6.88.91.E7.9A.84.E7.B3.BB.E7.B5.B1.E5.B7.B2.E7.B6.93.E6.98.AF.E6.9C.80.E6.96.B0.E7.9A.84.EF.BC.81)
    *   [3.3 更新時發生錯誤: "file exists in filesystem"!](#.E6.9B.B4.E6.96.B0.E6.99.82.E7.99.BC.E7.94.9F.E9.8C.AF.E8.AA.A4:_.22file_exists_in_filesystem.22.21)
    *   [3.4 安裝軟體包時發生錯誤: "not found in sync db"](#.E5.AE.89.E8.A3.9D.E8.BB.9F.E9.AB.94.E5.8C.85.E6.99.82.E7.99.BC.E7.94.9F.E9.8C.AF.E8.AA.A4:_.22not_found_in_sync_db.22)
    *   [3.5 安裝軟體包時發生錯誤: "target not found"](#.E5.AE.89.E8.A3.9D.E8.BB.9F.E9.AB.94.E5.8C.85.E6.99.82.E7.99.BC.E7.94.9F.E9.8C.AF.E8.AA.A4:_.22target_not_found.22)
    *   [3.6 Pacman 一直重複更新同樣的軟體包！](#Pacman_.E4.B8.80.E7.9B.B4.E9.87.8D.E8.A4.87.E6.9B.B4.E6.96.B0.E5.90.8C.E6.A8.A3.E7.9A.84.E8.BB.9F.E9.AB.94.E5.8C.85.EF.BC.81)
    *   [3.7 Pacman 在更新的時候崩潰了！](#Pacman_.E5.9C.A8.E6.9B.B4.E6.96.B0.E7.9A.84.E6.99.82.E5.80.99.E5.B4.A9.E6.BD.B0.E4.BA.86.EF.BC.81)
    *   [3.8 我使用 "make install" 安裝軟體；這些檔案並不屬於任何軟體包！](#.E6.88.91.E4.BD.BF.E7.94.A8_.22make_install.22_.E5.AE.89.E8.A3.9D.E8.BB.9F.E9.AB.94.EF.BC.9B.E9.80.99.E4.BA.9B.E6.AA.94.E6.A1.88.E4.B8.A6.E4.B8.8D.E5.B1.AC.E6.96.BC.E4.BB.BB.E4.BD.95.E8.BB.9F.E9.AB.94.E5.8C.85.EF.BC.81)
    *   [3.9 我需要一個特定檔案。要怎麼知道是哪個軟體包提供它呢？](#.E6.88.91.E9.9C.80.E8.A6.81.E4.B8.80.E5.80.8B.E7.89.B9.E5.AE.9A.E6.AA.94.E6.A1.88.E3.80.82.E8.A6.81.E6.80.8E.E9.BA.BC.E7.9F.A5.E9.81.93.E6.98.AF.E5.93.AA.E5.80.8B.E8.BB.9F.E9.AB.94.E5.8C.85.E6.8F.90.E4.BE.9B.E5.AE.83.E5.91.A2.EF.BC.9F)
    *   [3.10 Pacman 整個壞掉了！我要如何將它重新安裝？](#Pacman_.E6.95.B4.E5.80.8B.E5.A3.9E.E6.8E.89.E4.BA.86.EF.BC.81.E6.88.91.E8.A6.81.E5.A6.82.E4.BD.95.E5.B0.87.E5.AE.83.E9.87.8D.E6.96.B0.E5.AE.89.E8.A3.9D.EF.BC.9F)
    *   [3.11 更新我的系統後，重新開機得到 "unable to find root device" 錯誤，之後我的系統就再也無法開機了](#.E6.9B.B4.E6.96.B0.E6.88.91.E7.9A.84.E7.B3.BB.E7.B5.B1.E5.BE.8C.EF.BC.8C.E9.87.8D.E6.96.B0.E9.96.8B.E6.A9.9F.E5.BE.97.E5.88.B0_.22unable_to_find_root_device.22_.E9.8C.AF.E8.AA.A4.EF.BC.8C.E4.B9.8B.E5.BE.8C.E6.88.91.E7.9A.84.E7.B3.BB.E7.B5.B1.E5.B0.B1.E5.86.8D.E4.B9.9F.E7.84.A1.E6.B3.95.E9.96.8B.E6.A9.9F.E4.BA.86)
    *   [3.12 來自 "User <email@gmail.com>" 的簽章為未知信任，安裝失敗](#.E4.BE.86.E8.87.AA_.22User_.3Cemail.40gmail.com.3E.22_.E7.9A.84.E7.B0.BD.E7.AB.A0.E7.82.BA.E6.9C.AA.E7.9F.A5.E4.BF.A1.E4.BB.BB.EF.BC.8C.E5.AE.89.E8.A3.9D.E5.A4.B1.E6.95.97)
    *   [3.13 我一直得到](#.E6.88.91.E4.B8.80.E7.9B.B4.E5.BE.97.E5.88.B0)
    *   [3.14 我一直得到 "failed to commit transaction (invalid or corrupted package)" 錯誤](#.E6.88.91.E4.B8.80.E7.9B.B4.E5.BE.97.E5.88.B0_.22failed_to_commit_transaction_.28invalid_or_corrupted_package.29.22_.E9.8C.AF.E8.AA.A4)
    *   [3.15 每次我使用 Pacman 時，都會出現錯誤 "warning: current locale is invalid; using default "C" locale" 我要怎麼做？](#.E6.AF.8F.E6.AC.A1.E6.88.91.E4.BD.BF.E7.94.A8_Pacman_.E6.99.82.EF.BC.8C.E9.83.BD.E6.9C.83.E5.87.BA.E7.8F.BE.E9.8C.AF.E8.AA.A4_.22warning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.22_.E6.88.91.E8.A6.81.E6.80.8E.E9.BA.BC.E5.81.9A.EF.BC.9F)
    *   [3.16 我要如何讓 Pacman 遵守我的代理伺服設定？](#.E6.88.91.E8.A6.81.E5.A6.82.E4.BD.95.E8.AE.93_Pacman_.E9.81.B5.E5.AE.88.E6.88.91.E7.9A.84.E4.BB.A3.E7.90.86.E4.BC.BA.E6.9C.8D.E8.A8.AD.E5.AE.9A.EF.BC.9F)
    *   [3.17 我要如何重新安裝所有軟體包，同時保留它們彼此之間的相依關係？](#.E6.88.91.E8.A6.81.E5.A6.82.E4.BD.95.E9.87.8D.E6.96.B0.E5.AE.89.E8.A3.9D.E6.89.80.E6.9C.89.E8.BB.9F.E9.AB.94.E5.8C.85.EF.BC.8C.E5.90.8C.E6.99.82.E4.BF.9D.E7.95.99.E5.AE.83.E5.80.91.E5.BD.BC.E6.AD.A4.E4.B9.8B.E9.96.93.E7.9A.84.E7.9B.B8.E4.BE.9D.E9.97.9C.E4.BF.82.EF.BC.9F)
*   [4 另請參閱](#.E5.8F.A6.E8.AB.8B.E5.8F.83.E9.96.B1)

## 設定

Pacman 的設定檔為 `/etc/pacman.conf`。使用者可以修改設定檔讓程式符合需求。該設定檔的進一步資訊可以在 [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html) 找到。

### 一般選項

一般選項的定義落在 `[options]` 區塊。閱讀 man 文件或查看預設 `pacman.conf` 以了解可調整的地方。

#### 跳過特定軟體包的升級

若要取消特定軟體包的升級，可如下指定：

```
IgnorePkg=linux

```

多種軟體包的取消升級，可用空白分隔各軟體包名稱，或是加入若干 `IgnorePkg` 行。

#### 跳過特定軟體群組的升級

取消軟體群組升級的作法跟單一軟體包相同：

```
IgnoreGroup=gnome

```

#### 禁止特定檔案安裝至系統

若要永遠禁止特定目錄的安裝，將它們列在 `NoExtract` 後面。例如以下禁止 [systemd](/index.php/Systemd "Systemd") 新元件的安裝：

```
NoExtract=usr/lib/systemd/system/*

```

### 軟體庫

這一部分定義了要使用哪些[軟體庫](/index.php/Official_Repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official Repositories (正體中文)")，如 `/etc/pacman.conf` 內所述。我們可以直接在檔案內宣告軟體庫的位置，或是從另一個檔案讀取(如 `/etc/pacman.d/mirrorlist`)，這樣就只需要維護一項清單。鏡像站的設定請參閱[這裡](/index.php/Mirrors "Mirrors")。

 `/etc/pacman.conf` 

```
#[testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[extra]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[community]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

#[multilib]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs
```

**警告:** 使用 _testing_ 軟體庫的人請留意！該庫的軟體處於密集開發的狀態，隨意更新可能有讓部分軟體無法運作的風險。我們鼓勵使用 _testing_ 軟體庫的人訂閱 [arch-dev-public 郵件論壇](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public)來了解目前開發的資訊。

### 軟體包的安全性

Pacman 4 支援軟體包簽章，為軟體包的安全性多添加一層保障。預設選項 `SigLevel = Required DatabaseOptional` 啟用對所有軟體包的簽章認証：軟體庫設定值的 `SigLevel` 行 (如上面所示) 設定可蓋過預設選項。更多相關資訊 (簽署軟體包、認證簽章) 請參閱 [pacman-key](/index.php/Pacman-key "Pacman-key")。

## 使用方式

以下將用一些簡單範例來說明 pacman 可執行的操作。[man pacman](https://www.archlinux.org/pacman/pacman.8.html) 有更多的範例可供參考。

### 安裝軟體包

#### 安裝特定軟體包

安裝一或多個軟體包 (包含相依軟體)：

```
# pacman -S **軟體包名稱1** **軟體包名稱2** ...

```

有時候不同的軟體庫下會存放同一種軟體包，只是版本不同而已 (如 [extra] 和 [testing])。此時必須在軟體包名稱前面定義軟體庫名：

```
# pacman -S extra/**軟體包名稱**

```

#### 安裝軟體群組

Pacman 可以同時安裝歸屬於同一群組下的軟體包，如下面範例指令：

```
# pacman -S gnome

```

Pacman 將提示您選擇 [gnome](https://www.archlinux.org/groups/x86_64/gnome/) 群組下要安裝那些軟體包。

某些軟體群組包含了數量眾多的軟體包，只有某一小部分的軟體包是您(不)要安裝的。您不需將所有需要的軟體包代碼一一輸入，用以下的語法可以快速選取某一範圍的軟體包，例如：

```
Enter a selection (default=all): 1-10 15

```

將會安裝從 1 到 10，以及 15 號軟體包，或者：

```
Enter a selection (default=all): ^5-8 ^2

```

除了 5 到 8、以及 2 號軟體包以外，其他軟體包將會被安裝。

執行以下指令查看哪些軟體包被歸類在 gnome 群組：

```
# pacman -Sg gnome

```

或者，到 [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) 網站查看有什麼軟體群組可用。

**註記:** 當指定安裝一項軟體包時，就算該軟體包已被安裝過，也還是會重新安裝一次。可以利用 `--needed` 選項略過已安裝且為最新版本的軟體包。

**警告:** 在系統尚未[升級](#.E5.8D.87.E7.B4.9A.E8.BB.9F.E9.AB.94.E5.8C.85)過的狀況下安裝軟體包時，千萬**不要**重新整理軟體包清單 (即 `pacman -Sy _軟體包名稱_`)；這可能會導致相依性出現問題。請參閱[#不支援部分升級](#.E4.B8.8D.E6.94.AF.E6.8F.B4.E9.83.A8.E5.88.86.E5.8D.87.E7.B4.9A)和 [https://bbs.archlinux.org/viewtopic.php?id=89328。](https://bbs.archlinux.org/viewtopic.php?id=89328。)

### 移除軟體包

移除單一軟體包，但不移除與其一同安裝的相依軟體包：

```
# pacman -R _軟體包名稱_

```

移除單一軟體包，以及與其相依且不再被其他軟體需要的軟體包：

```
# pacman -Rs _軟體包名稱_

```

移除單一軟體包，以及與其相依的軟體包；也一同移除其他受影響的軟體包：

**警告:** 這項操作具連帶性，進行之前必須確認不會刪掉您仍然需要的軟體包。

```
# pacman -Rsc _軟體包名稱_

```

移除單一軟體包，但不移除依賴該軟體包的其他軟體包：

```
# pacman -Rdd _軟體包名稱_

```

Pacman 在移除特定應用程式時，會儲存其重要設定檔，加上副檔名 `.pacsave`。使用 `-n` 選項避免這些備份檔案被建立：

```
# pacman -Rn _軟體包名稱_

```

**註記:** Pacman 不會移除應用程式自己建立的設定檔 (例如家目錄下的「隱藏檔案」)。

### 升級軟體包

Pacman 只需一個指令即可更新系統所有軟體包。根據系統的軟體包版本狀態，這項操作會花上一段時間。本指令會同步資料庫_並_更新系統的軟體包 (除了不在預定軟體庫內的「本機」軟體包)：

```
# pacman -Syu

```

**警告:** 並不是每當更新可用時就得馬上更新。使用者必須瞭解，基於 Arch 的「無縫更新」特性，每一次大更新都可能會導向無法預期的結果。打個比方而言，在您準備一場重要的演說前一刻更新系統是相當不智的行為。最好在閒暇時刻進行更新，並準備應付更新可能引發的任何問題。

Pacman 是相當強大的軟體包管理工具，但它並不是對付各式疑難雜症的萬靈丹。若這對您造成困擾，請回頭看看 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")是怎麼說的。使用者必須有警覺心，並負起維護自己系統的重責大任。**在執行系統更新時，要做好 Arch 使用者的基本功：閱讀 Pacman 輸出的所有資訊並動動腦筋。**當新軟體包的版本要更新一個被使用者修改過的設定檔時，為了避免蓋掉使用者自己的設定，會將新的預設設定檔改為 `.pacnew` 檔案。Pacman 會提醒使用者融合新舊兩檔。這些設定檔案需要使用者手動介入，而且最好在每次軟體包更新 / 移除之後就馬上處理。更多資訊請參閱 [Pacnew 與 Pacsave 檔案](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files")。

**提示:** Pacman 的輸出訊息會記錄在 `/var/log/pacman.log`。

升級系統之前，建議到 [Arch Linux 首頁](https://www.archlinux.org/)檢查最新消息 (或是訂閱 [RSS feed](https://www.archlinux.org/feeds/news/)、[arch-announce 郵件論壇](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)，或是追蹤 [@archlinux](https://twitter.com/archlinux) Arch 的推特)。當出現 Pacman 無法自行處理、使用者必須介入的狀況時 (雖然這種情況很少見)，我們會發送新的公告貼文。

要是您碰到的問題無法藉由以上的指示解決，記得到論壇搜尋看看，說不定也有其他人碰到跟您相同的問題，並提出解決辦法。

### 查詢軟體包資料庫

Pacman 使用 `-Q` 旗標查詢本機的軟體包資料庫；可參閱：

```
$ pacman -Q --help

```

並使用 `-S` 旗標查詢(軟體庫的)同步資料庫；可參閱：

```
$ pacman -S --help

```

Pacman 可以用來搜尋資料庫內記錄的軟體包，以軟體包名稱、描述來搜尋：

```
$ pacman -Ss **字串1** **字串2** ...

```

搜尋已安裝的軟體包：

```
$ pacman -Qs **字串1** **字串2** ...

```

顯示給定軟體包的詳細資料：

```
$ pacman -Si **軟體包名稱**

```

系統內安裝軟體包的詳細資料：

```
$ pacman -Qi **軟體包名稱**

```

傳入兩個 `-i` 旗標，會同時顯示備份檔案清單與它們的修改狀態：

```
$ pacman -Qii **軟體包名稱**

```

獲取軟體包所安裝的檔案清單：

```
$ pacman -Ql **軟體包名稱**

```

尚未安裝的軟體包則使用 [pkgfile](/index.php/Pkgfile "Pkgfile")。

您也可以向資料庫查詢系統內某個檔案是屬於哪一項軟體包：

```
$ pacman -Qo **檔案路徑**

```

根據相依性，列出所有不再需要的軟體包 (孤兒)：

```
$ pacman -Qdt

```

列出軟體包的相依性樹狀圖：

```
$ pactree **軟體包名稱**

```

使用 [pkgtools](/index.php/Pkgtools "Pkgtools") 下的 `whoneeds` ，列出需要某個_已安裝_軟體包的所有軟體包：

```
$ whoneeds **軟體包名稱**

```

### 其他指令

一行升級系統並安裝其他軟體包：

```
# pacman -Syu **軟體包名稱1** **軟體包名稱2** ...

```

下載軟體包但不要安裝：

```
# pacman -Sw **軟體包名稱**

```

安裝不是來自遠端軟體庫的「本機」軟體包 (如從 [AUR](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)") 建構的軟體包)：

```
# pacman -U /path/to/package/package_name-version.pkg.tar.xz

```

**提示:** 若要保存一份本機軟體包的副本到 Pacman 的快取，使用：

```
# pacman -U file://path/to/package/package_name-version.pkg.tar.xz

```

安裝非 Pacman 設定檔所指定軟體庫下的「遠端」軟體包：

```
# pacman -U http://www.example.com/repo/example.pkg.tar.xz

```

清理目前尚未安裝的軟體包快取 (`/var/cache/pacman/pkg`)：

**警告:** 這項操作將移除快取資料夾下所有軟體包的舊有版本，只留下目前已安裝的軟體包版本。只有在安裝的軟體包都穩定、不需要進行[降級](/index.php/Downgrading_packages "Downgrading packages")的情況下，再進行這項操作。萬一未來更新時出現任何問題，擁有的這些舊有版本就可以派上用場。

```
# pacman -Sc

```

清理整個軟體包快取：

**警告:** 這將會清掉整個軟體包快取。這不是一個好動作；這樣會失去直接從快取資料夾降級軟體包的機會。使用者會被迫使用毀損軟體包的替代來源，例如 [Arch Rollback Machine](/index.php/Downgrading_packages#ARM "Downgrading packages")。

```
# pacman -Scc

```

**提示:** 除了使用 `-Sc` 和 `-Scc` 這兩個選項以外，也可以考慮使用 [pacman](https://www.archlinux.org/packages/?name=pacman) 下的 `paccache`。此工具提供更多樣的控制，像是要刪除什麼軟體包快取、或刪除多少軟體包快取。執行 `paccache -h` 可獲得更多指示。

### 不支援部分升級

Arch Linux 採用無縫更新，[函式庫](https://en.wikipedia.org/wiki/Library_(computing) "wikipedia:Library (computing)")若有新的版本就會馬上推進軟體庫。開發人員與受信任的使用者會將庫內所有與函式庫相關的軟體包都重新建構過。若系統內有本機安裝的軟體包 (像 [AUR](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)") 軟體包) 碰到 [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") bump 時，使用者就必須重新建構它們。

此時部分升級將**不被支援**。不要使用 `pacman -Sy [軟體包]` 或其他相似指令如 `pacman -Sy` 加 `pacman -S [軟體包]`。在安裝軟體包記得先將系統升級 -- 特別是當 Pacman 重整同步軟體庫之後。基於相同的原因，使用 `IgnorePkg` 和 `IgnoreGroup` 時也請多留意。

若在部分升級的情況下，有函式庫因為找不到其他與其連結的函式庫而發生問題的話，**不要試著用軟連結「修復」問題**。函式庫在**未向後相容**的情況下會收到[soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") bump。只要 Pacman 還能正常運作，一個簡單的 `pacman -Syu`，加上與鏡像站適當地同步就可以解決此問題。

### 基本注意事項

**警告:** 使用 `--force` 開關時請小心，不正當的使用將導致重大問題。強烈建議**只有**在 Arch 新聞指定的情況下才使用這個選項。

## 疑難排解

### 升級某個軟體包後，我的系統故障了！

Arch Linux 屬於無縫發行的尖端發行版本。當軟體包的更新被認定在一般使用上有足夠的穩定度時就會立即釋出。但是，有時候更新需要使用者的介入，比如說設定檔案需要更新、選用相依性改變等等。

最重要的一點提示就是，不要「盲目」升級 Arch 系統。永遠記得先閱讀準備更新的軟體包清單。注意是否有「重要」的軟體包更新 (諸如 [linux](https://www.archlinux.org/packages/?name=linux), [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 等)。如果是的話，檢查 [https://www.archlinux.org/](https://www.archlinux.org/) 上是否有最新新聞，並爬一下最近的論壇貼文，看看是否有人在本次更新碰到任何問題。

若軟體包更新預期/已知會產生問題，打包人員會確認更新軟體包時 Pacman 會顯示適當訊息。若更新後碰到任何問題，到日誌檔 (`/var/log/pacman.log`) 檢查 Pacman 的輸出訊息。

到這個時候，**只有在確認 Pacman 沒有顯示任何可用訊息、[https://www.archlinux.org/](https://www.archlinux.org/) 上沒有相關新聞，論壇上也沒有和該次更新相關的貼文時**，再考慮到論壇、[IRC](/index.php/IRC_Channel "IRC Channel") 上求助，或是將[衝突的軟體包降級](/index.php/Downgrading_packages "Downgrading packages")。

### 我知道某個軟體包升級已經釋出，但 Pacman 說我的系統已經是最新的！

Pacman 鏡像站並非立即同步。大約要 24 小時過後您才會收到更新。唯一能做的就是耐心等候，或者使用其他鏡像站。[MirrorStatus](https://www.archlinux.org/mirrors/status/) 可以幫助您找出處於最新狀態的鏡像站。

### 更新時發生錯誤: "file exists in filesystem"!

ASIDE: **取自 [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) (作者 Misfit138)。**

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /path/to/file exists in filesystem
Errors occurred, no packages were upgraded.

```

為何有這種情況發生：pacman 偵測到檔案衝突，根據設計，它不會幫您蓋過舊有檔案。這是其中一項設計功能，而非失誤。

通常這種問題都很好解決。比較安全的方式是，首先檢查是否有其他軟體包擁有這份檔案 (`pacman -Qo **檔案路徑**`)。若有其他軟體包擁有這份檔案，[寄一份錯誤報告](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")。沒有的話，將「存在檔案系統」的這份檔案重新命名，並重新下達升級指令。若一切正常，檔案就會被移除。

若您使用手動的方式安裝程式，而非 pacman 或其它前端程式的話，先移除這個程式和所有相關檔案，再使用 pacman 重新安裝。

每份安裝的軟體包都會提供 `/var/lib/pacman/local/$package-$version/files` 檔案，其中包含了有關這份軟體包的元數據。如果這個檔案損壞 (變空或是遺失)，在嘗試升級軟體包時就會出現 "file exists in filesystem" (檔案已存在於檔案系統) 錯誤。通常這種錯誤只影響單一軟體包，除了手動重新命名並移除該軟體包所有檔案以外，您可以執行 `pacman -S --force $package` 強制 pacman 覆寫這些檔案。

**千萬不要**執行 `pacman -Syu --force`。

### 安裝軟體包時發生錯誤: "not found in sync db"

請先確認軟體包確實存在 (並檢查拼字正確)。若該軟體包確實存在，代表您的軟體包清單可能過期，或是您的軟體倉庫設定不正確。試著用 `pacman -Syyu` 重整所有軟體包清單後更新。

### 安裝軟體包時發生錯誤: "target not found"

請先確認軟體包確實存在 (並檢查拼字正確)。若該軟體包確實存在，代表您的軟體包清單可能過期，或是您的軟體倉庫設定不正確。試著用 `pacman -Syyu` 重整所有軟體包清單後更新。  
這也有可能是該軟體包所屬之軟體倉庫在您的系統上未被啟用，比如說軟體包在 _multilib_ 倉庫，但您的 _pacman.conf_沒有啟用 _multilib_。

### Pacman 一直重複更新同樣的軟體包！

這是因為 `/var/lib/pacman/local/` 出現了重複的項目，例如兩個 `linux` 項目。`pacman -Qi` 輸出了正確版本，但 `pacman -Qu` 偵測到舊有版本而嘗試更新。

解決方式：在 `/var/lib/pacman/local/` 刪除衝突的項目。

**註記:** Pacman 版本 3.4 應會顯示對應重複項目的錯誤，這則記事已經過期。

### Pacman 在更新的時候崩潰了！

在 Pacman 在移除軟體包時出現「資料庫寫入」錯誤而崩潰，重新安裝或升級軟體包也失敗的狀況下：

1.  使用 Arch 安裝媒體開機。
2.  掛載您的根檔案系統。
3.  更新 Pacman 資料庫並透過 `pacman -Syyu` 升級。
4.  透過 `pacman -r **根目錄路徑** -S **軟體包**` 重新安裝損毀的軟體包。

### 我使用 "make install" 安裝軟體；這些檔案並不屬於任何軟體包！

當收到 "conflicting files" (檔案衝突) 錯誤，若加上 `--force` (`pacman -S --force`)，Pacman 將覆寫手動安裝的軟體。參閱 [Pacman 提示#偵測不屬於任何軟體包的檔案](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips")，有一份搜尋檔案系統下是否有「無歸屬」檔案的腳本可供參考。

**警告:** 使用 `--force` 開關時請小心，不正當的使用將導致重大問題。強烈建議只在 Arch 新聞指定的情況下才使用這個選項。

### 我需要一個特定檔案。要怎麼知道是哪個軟體包提供它呢？

安裝 [pkgfile](/index.php/Pkgfile "Pkgfile")。這個程式使用一個分離資料庫，記錄著所有檔案和它們相關聯的軟體包。

### Pacman 整個壞掉了！我要如何將它重新安裝？

當 pacman 損壞且無法修復，手動下載必要的軟體包 ([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive) 以及 [pacman](https://www.archlinux.org/packages/?name=pacman))，在根目錄下將它們解壓縮，就可恢復 pacman 執行檔和其預設設定檔。之後用 pacman 重新安裝這些軟體包，以維持軟體包資料庫的正確性。更多資訊和一份自動化的範例 (過期) 腳本請參閱[這個](https://bbs.archlinux.org/viewtopic.php?id=95007)論壇貼文。

### 更新我的系統後，重新開機得到 "unable to find root device" 錯誤，之後我的系統就再也無法開機了

很有可能是核心升級時 initramfs 損壞了 (肇因之一為不正當的使用 pacman 的 `--force` 選項)。有兩條路可走：

**1.** 試試 _Fallback_ 項目。

**提示:** 如果這個項目被刪除，在開機載入程式的選單顯示之後，按 `Tab` 鍵 (Syslinux) 或 `e` (GRUB)，重新命名為 `initramfs-linux-fallback.img`，按 `Enter` 或 `b` (視開機載入程式而定) 以新參數開機。

當系統啟動就緒，在終端機或文字介面下執行這個指令 (對應 [linux](https://www.archlinux.org/packages/?name=linux) 核心)，重新建立一份 initramfs 映像：

 `# mkinitcpio -p linux` 

**2.** 若沒有任何作用，用 2012 年的 Arch 釋出媒體 (CD/DVD 或 USB 碟) 開機，並執行：

**註記:** 如果您沒有一份 2012 年的釋出版，或者已經被其他 Linux 發行版本的「live」環境覆蓋，可以使用比較老套的辦法：[chroot](/index.php/Chroot "Chroot")。當然，比起簡單執行 `arch-chroot` 腳本，這個辦法需要打的字會比較多。

```
# mount /dev/sdxY /mnt         # 您的根分割區
# mount /dev/sdxZ /mnt/boot    # 若您有使用分開的 /boot 分割區。
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux
```

重新安裝核心 ([linux](https://www.archlinux.org/packages/?name=linux) 軟體包) 將自動以 `mkinitcpio -p linux` 重新產生 initramfs 映像。該指令不需要另外特定執行。

接著，建議您執行 `exit`, `umount /mnt/{boot,}` 和 `reboot`。

**註記:** 如果您無法進入 arch-chroot 或 chroot 環境，但需要重新安裝軟體包，可以使用指令 `pacman -r /mnt -Syu **軟體包名稱**`，使用在您的根分割區之下的 Pacman。

### 來自 "User <email@gmail.com>" 的簽章為未知信任，安裝失敗

遵照 [pacman-key#重設所有鑰匙](/index.php/Pacman-key#Resetting_all_the_keys "Pacman-key")。或者您可以先嘗試手動更新 [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) 軟體包，即 `pacman -S archlinux-keyring`。

### 我一直得到

```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded. 

```

當系統時鐘錯誤時會出現這些錯誤。設定好[時間](/index.php/Time "Time")並執行： `# hwclock -w` ，再嘗試安裝/升級軟體包。

### 我一直得到 "failed to commit transaction (invalid or corrupted package)" 錯誤

檢查 `/var/cache/pacman/pkg` 下的 `*.part` 檔 (部分下載軟體包) 並移除它們 (通常肇因為使用 `pacman.conf` 的自訂 `XferCommand`)。

### 每次我使用 Pacman 時，都會出現錯誤 "warning: current locale is invalid; using default "C" locale" 我要怎麼做？

如該錯誤訊息所示，您的語系並未正確設定。請參閱[語系](/index.php/Locale "Locale")。

### 我要如何讓 Pacman 遵守我的代理伺服設定？

確認相關的環境變數 (`$http_proxy`, `$ftp_proxy` 等) 都已設定完成。若使用 [sudo](/index.php/Sudo "Sudo") 執行 Pacman，您需要設定讓 sudo [傳送這些環境變數給 Pacman](/index.php/Sudo#Environment_variables "Sudo")。

### 我要如何重新安裝所有軟體包，同時保留它們彼此之間的相依關係？

重新安裝所有原地軟體包：`pacman -S $(pacman -Qnq)` (`-S` 選項預設保留安裝緣由)。  
接著您必須重新安裝所有外部軟體包，用 `pacman -Qmq` 來列出它們。

## 另請參閱

*   [libalpm(3) 手冊頁面](https://www.archlinux.org/pacman/libalpm.3.html)
*   [pacman(8) 手冊頁面](https://www.archlinux.org/pacman/pacman.8.html)
*   [pacman.conf(5) 手冊頁面](https://www.archlinux.org/pacman/pacman.conf.5.html)
*   [repo-add(8) 手冊頁面](https://www.archlinux.org/pacman/repo-add.8.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacman_(正體中文)&oldid=411874](https://wiki.archlinux.org/index.php?title=Pacman_(正體中文)&oldid=411874)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [正體中文](/index.php/Category:%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87 "Category:正體中文")
*   [Package management (正體中文)](/index.php/Category:Package_management_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Category:Package management (正體中文)")