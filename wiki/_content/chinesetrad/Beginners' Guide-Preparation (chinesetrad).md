**翻譯狀態：** 本文章是 [Beginners'_Guide/Preparation](/index.php/Beginners%27_Guide/Preparation "Beginners' Guide/Preparation") 的翻譯版本。最近一次的翻譯時間：2014-01-26。點擊[本連結](https://wiki.archlinux.org/index.php?title=Beginners'_Guide/Preparation&diff=0&oldid=294181)查看英文頁面之後的變更。

**提示:** 本文是新手教學的多頁版本。若您希望閱讀完整的指南，請**[點擊這裡](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' guide (正體中文)")**。

本文件將指導您使用 [Arch 安裝腳本](https://projects.archlinux.org/arch-install-scripts.git/)完成 [Arch Linux](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)") 的安裝。開始之前建議您大略瀏覽一下 [FAQ](/index.php/FAQ_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "FAQ (正體中文)")。

若您碰到任何問題，社群維護的 [Arch 維基](/index.php/Main_page_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Main page (正體中文)")是主要的資料來源，請多加利用。若無法自行解決，也歡迎到 [IRC 頻道](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) 和[論壇](https://bbs.archlinux.org/)問問。根據 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")，我們鼓勵所有使用者在碰到任何不熟悉的指令時，先呼叫 `man **指令**` 查看 `man` 說明文件。

## Contents

*   [1 準備](#.E6.BA.96.E5.82.99)
    *   [1.1 系統需求](#.E7.B3.BB.E7.B5.B1.E9.9C.80.E6.B1.82)
    *   [1.2 準備最新的安裝媒體](#.E6.BA.96.E5.82.99.E6.9C.80.E6.96.B0.E7.9A.84.E5.AE.89.E8.A3.9D.E5.AA.92.E9.AB.94)
        *   [1.2.1 透過網路安裝](#.E9.80.8F.E9.81.8E.E7.B6.B2.E8.B7.AF.E5.AE.89.E8.A3.9D)
        *   [1.2.2 從既存的 Linux 系統安裝](#.E5.BE.9E.E6.97.A2.E5.AD.98.E7.9A.84_Linux_.E7.B3.BB.E7.B5.B1.E5.AE.89.E8.A3.9D)
        *   [1.2.3 在虛擬機器上安裝](#.E5.9C.A8.E8.99.9B.E6.93.AC.E6.A9.9F.E5.99.A8.E4.B8.8A.E5.AE.89.E8.A3.9D)
        *   [1.2.4 啟動安裝媒體](#.E5.95.9F.E5.8B.95.E5.AE.89.E8.A3.9D.E5.AA.92.E9.AB.94)
            *   [1.2.4.1 測試是否以 UEFI 模式開機](#.E6.B8.AC.E8.A9.A6.E6.98.AF.E5.90.A6.E4.BB.A5_UEFI_.E6.A8.A1.E5.BC.8F.E9.96.8B.E6.A9.9F)
        *   [1.2.5 開機疑難排解](#.E9.96.8B.E6.A9.9F.E7.96.91.E9.9B.A3.E6.8E.92.E8.A7.A3)

## 準備

**註記:** 如果您打算在既存的 GNU/Linux 發行版本下安裝 Arch，請參閱[這篇文章](/index.php/Install_from_existing_Linux "Install from existing Linux")，對透過 [VNC](/index.php/VNC "VNC") 或 [SSH](/index.php/SSH "SSH") 遠端安裝 Arch 的使用者而言會有幫助。欲透過 [SSH](/index.php/SSH "SSH") 連線遠端安裝 Arch Linux 的使用者，應閱讀[從 SSH 安裝](/index.php/Install_from_SSH "Install from SSH")提到的額外提示。

### 系統需求

Arch Linux 在任何 [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) 相容的機器上執行，最低需求 RAM 為 64 MB。一般而言將安裝 [base](https://www.archlinux.org/groups/x86_64/base/) 群組下所有軟體包，總共佔用約 500 MB 的硬碟空間。若您目前的空間不足，可以視狀況縮減安裝項目，但您必須真的瞭解自己在做什麼。

### 準備最新的安裝媒體

最新釋出的安裝媒體可以從官網的[下載](https://archlinux.org/download/)頁面取得。另外註明，單一 ISO 映像同時支援 32 和 64 位元的硬體架構。強烈建議您使用最新的 ISO 映像。

*   我們的安裝媒體都簽署過，強烈建議使用前先驗明正身。從下載頁面 (或任何一個表列的鏡像站) 將 *.sig* 檔下載到存放 *.iso* 檔的資料夾。在 Arch Linux 下以 root 身分使用 `pacman-key -v *iso-file*.sig`，其他環境下直接使用 gpg2，一樣用 root 身分執行：`gpg2 --verify *iso-file.sig*`。網站上也提供了 md5 和 sha1 校驗碼。

*   將 ISO 映像燒入 CD 或 DVD，用您習慣的燒錄軟體即可。Arch 下的燒錄程式請參考[光碟機#燒錄](/index.php/Optical_disc_drive#Burning "Optical disc drive")。

**註記:** 不同光碟機和 CD 本身的品質差異甚大。一般建議使用低速燒錄，以得到可靠的燒錄品質。若燒錄的 CD 發生任何異常狀況，請使用機器支援的最低速度再重新燒錄一遍。

*   也可以將 ISO 映像寫入 USB 碟。詳細的步驟請參閱 [USB 安裝媒體](/index.php/USB_Installation_Media_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "USB Installation Media (正體中文)")。

#### 透過網路安裝

除了光碟或隨身碟等方式之外，若您有一台可運作的伺服器，也可以選擇透過網路啟動 ISO 映像。請參閱 [PXE](/index.php/PXE "PXE") 文章了解更多資訊，並接續至[啟動安裝媒體](#.E5.95.9F.E5.8B.95.E5.AE.89.E8.A3.9D.E5.AA.92.E9.AB.94)。

#### 從既存的 Linux 系統安裝

在一個正在運行的 Linux 系統上安裝 Arch 是可行的。請參閱[從既存 Linux 安裝](/index.php/Install_from_existing_Linux "Install from existing Linux")。

#### 在虛擬機器上安裝

將 Arch Linux 安裝在[虛擬機器](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine")是熟悉 Arch Linux 的好方法：安裝時不必離開您現在的作業系統，也不會動到硬碟原本的分割區。此外，在安裝過程中也能夠開著瀏覽器查閱這份「新手教學」。對某些使用者而言，有一份獨立在虛擬機器上跑的 Arch Linux 作測試，好處多多。

常見的虛擬機器軟體有 [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels")。

準備虛擬機器的步驟因軟體而異，但一般跟以下的步驟相距不遠：

1.  建立虛擬硬碟映像檔，用來存放作業系統。
2.  正確設置虛擬機器的參數。
3.  使用虛擬光碟機，啟動下載的 ISO 映像。
4.  繼續按照[啟動安裝媒體](#.E5.95.9F.E5.8B.95.E5.AE.89.E8.A3.9D.E5.AA.92.E9.AB.94)的步驟安裝。

下面的文章可能對您有幫助：

*   [以 Arch Linux 作為 VirtualBox 客戶端](/index.php/VirtualBox#Arch_Linux_as_a_guest_in_a_Virtual_Machine "VirtualBox")
*   [以實體硬碟上的 Arch Linux 作為 VirtualBox 客戶端](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [以 Arch Linux 作為 VMware 客戶端](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [移動既存的安裝至/出虛擬機器](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

#### 啟動安裝媒體

首先，您可能需要更改電腦 BIOS 的開機順序。 在[開機自我測試 (POST)](https://en.wikipedia.org/wiki/Power-on_self_test "wikipedia:Power-on self test") 階段按下按鍵 (通常是 `Delete`, `F1`, `F2`, `F11` 或 `F12`)。您將進入 BIOS 設定視窗，在此設定系統搜尋開機裝置的次序。選擇「Save & Exit」(儲存並離開，或您 BIOS 下的相同選項)，此時電腦應完成它的正常開機程序。 在 Arch 選單顯示之後，選擇「Boot Arch Linux」(啟動 Arch Linux)，按下 `Enter` 進入 live 環境，我們將在這個環境下進行實際的安裝手續 (若使用 UEFI 開機，選項應為「Arch Linux archiso x86_64 UEFI」)。

開機進入 Live 環境後將使用 [Zsh](/index.php/Zsh "Zsh") 這個 shell，它提供了進階的 Tab 補齊，和其他 [grml config](http://grml.org/zsh/) 的部份功能。

##### 測試是否以 UEFI 模式開機

若您使用的是 [UEFI](/index.php/UEFI "UEFI") 主機板，且啟用 UEFI 開機模式 (優先於 BIOS/Legacy 模式)，CD/USB 將自動啟動 Arch Linux 核心 (透過 [Gummiboot](/index.php/Gummiboot "Gummiboot") 啟動核心 [EFISTUB](/index.php/EFISTUB "EFISTUB"))。檢查是否以 UEFI 模式開機：

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # 若自動掛載則略過
# efivar -l

```

如果 efivar 正確列出 uefi 變數，代表您已經以 UEFI 模式開機。若否，檢查是否都符合 [UEFI#正常運作所需要的 UEFI 變數支援](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_Variables_support_to_work_properly "Unified Extensible Firmware Interface")所列出的任何要求。

#### 開機疑難排解

*   若您使用 Intel 顯示晶片組，螢幕在開機過程中變成一片空白，問題可能跟[核心模式設定](/index.php/Kernel_mode_setting "Kernel mode setting")有關。請重新開機，在您要嘗試開機的項目 (i686 或 x86_64) 下按 `e`。在字串尾端加入 `nomodeset` 後按 `Enter`。另外一種方式是加上 `video=SVIDEO-1:d`，這樣就不必停用 KMS。您也可以試試 `i915.modeset=0`。更多資訊請參閱 [Intel](/index.php/Intel "Intel") 這篇文章。

*   若螢幕**並非**呈現一片空白，而是在嘗試載入核心的過程中卡住的話，則在選單項目上按 `Tab`，在字串尾端輸入 `acpi=off` 後按 `Enter`。

**[新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")**

* * *

**準備** >> [安裝](/index.php/Beginners%27_Guide/Installation_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide/Installation (正體中文)") >> [安裝完成後](/index.php/Beginners%27_Guide/Post-installation_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide/Post-installation (正體中文)")