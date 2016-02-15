**提示:** 這份教學有一份多頁版本。若您不習慣看太長的文章，可以從**[這裡](/index.php/Beginners%27_Guide/Preparation_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide/Preparation (正體中文)")**開始。

本文件將指導您使用 [Arch 安裝腳本](https://projects.archlinux.org/arch-install-scripts.git/)完成 [Arch Linux](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)") 的安裝。開始之前建議您大略瀏覽一下 [FAQ](/index.php/FAQ_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "FAQ (正體中文)")。

若您碰到任何問題，社群維護的 [Arch 維基](/index.php/Main_Page_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Main Page (正體中文)")是主要的資料來源，請多加利用。若無法自行解決，也歡迎到 [IRC 頻道](/index.php/IRC_channel "IRC channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) 和[論壇](https://bbs.archlinux.org/)問問。根據 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")，我們鼓勵所有使用者在碰到任何不熟悉的指令時，先呼叫 `man **指令**` 查看 `man` 說明文件。

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
*   [2 安裝](#.E5.AE.89.E8.A3.9D)
    *   [2.1 更改語言](#.E6.9B.B4.E6.94.B9.E8.AA.9E.E8.A8.80)
    *   [2.2 啟用網路連線](#.E5.95.9F.E7.94.A8.E7.B6.B2.E8.B7.AF.E9.80.A3.E7.B7.9A)
        *   [2.2.1 有線網路](#.E6.9C.89.E7.B7.9A.E7.B6.B2.E8.B7.AF)
        *   [2.2.2 無線網路](#.E7.84.A1.E7.B7.9A.E7.B6.B2.E8.B7.AF)
            *   [2.2.2.1 不使用 wifi-menu](#.E4.B8.8D.E4.BD.BF.E7.94.A8_wifi-menu)
        *   [2.2.3 類比式數據機、ISDN 或 PPPoE DSL](#.E9.A1.9E.E6.AF.94.E5.BC.8F.E6.95.B8.E6.93.9A.E6.A9.9F.E3.80.81ISDN_.E6.88.96_PPPoE_DSL)
        *   [2.2.4 代理伺服器背後](#.E4.BB.A3.E7.90.86.E4.BC.BA.E6.9C.8D.E5.99.A8.E8.83.8C.E5.BE.8C)
    *   [2.3 準備儲存裝置](#.E6.BA.96.E5.82.99.E5.84.B2.E5.AD.98.E8.A3.9D.E7.BD.AE)
        *   [2.3.1 選擇分割表類型](#.E9.81.B8.E6.93.87.E5.88.86.E5.89.B2.E8.A1.A8.E9.A1.9E.E5.9E.8B)
        *   [2.3.2 分割工具](#.E5.88.86.E5.89.B2.E5.B7.A5.E5.85.B7)
        *   [2.3.3 分割計畫](#.E5.88.86.E5.89.B2.E8.A8.88.E7.95.AB)
        *   [2.3.4 與 Windows 雙重開機的考量](#.E8.88.87_Windows_.E9.9B.99.E9.87.8D.E9.96.8B.E6.A9.9F.E7.9A.84.E8.80.83.E9.87.8F)
        *   [2.3.5 範例](#.E7.AF.84.E4.BE.8B)
            *   [2.3.5.1 使用 cgdisk 建立 GPT 分割區](#.E4.BD.BF.E7.94.A8_cgdisk_.E5.BB.BA.E7.AB.8B_GPT_.E5.88.86.E5.89.B2.E5.8D.80)
            *   [2.3.5.2 使用 fdisk 建立 MBR 分割區](#.E4.BD.BF.E7.94.A8_fdisk_.E5.BB.BA.E7.AB.8B_MBR_.E5.88.86.E5.89.B2.E5.8D.80)
        *   [2.3.6 建立檔案系統](#.E5.BB.BA.E7.AB.8B.E6.AA.94.E6.A1.88.E7.B3.BB.E7.B5.B1)
    *   [2.4 掛載分割區](#.E6.8E.9B.E8.BC.89.E5.88.86.E5.89.B2.E5.8D.80)
    *   [2.5 選擇鏡像站](#.E9.81.B8.E6.93.87.E9.8F.A1.E5.83.8F.E7.AB.99)
    *   [2.6 安裝基礎系統](#.E5.AE.89.E8.A3.9D.E5.9F.BA.E7.A4.8E.E7.B3.BB.E7.B5.B1)
    *   [2.7 產生 fstab](#.E7.94.A2.E7.94.9F_fstab)
    *   [2.8 Chroot 並設定基礎系統](#Chroot_.E4.B8.A6.E8.A8.AD.E5.AE.9A.E5.9F.BA.E7.A4.8E.E7.B3.BB.E7.B5.B1)
        *   [2.8.1 本地化](#.E6.9C.AC.E5.9C.B0.E5.8C.96)
        *   [2.8.2 終端機字型與鍵盤布局](#.E7.B5.82.E7.AB.AF.E6.A9.9F.E5.AD.97.E5.9E.8B.E8.88.87.E9.8D.B5.E7.9B.A4.E5.B8.83.E5.B1.80)
        *   [2.8.3 時區](#.E6.99.82.E5.8D.80)
        *   [2.8.4 硬體時鐘](#.E7.A1.AC.E9.AB.94.E6.99.82.E9.90.98)
        *   [2.8.5 核心模組](#.E6.A0.B8.E5.BF.83.E6.A8.A1.E7.B5.84)
        *   [2.8.6 主機名稱](#.E4.B8.BB.E6.A9.9F.E5.90.8D.E7.A8.B1)
    *   [2.9 設定網路](#.E8.A8.AD.E5.AE.9A.E7.B6.B2.E8.B7.AF)
        *   [2.9.1 有線網路](#.E6.9C.89.E7.B7.9A.E7.B6.B2.E8.B7.AF_2)
            *   [2.9.1.1 動態 IP](#.E5.8B.95.E6.85.8B_IP)
            *   [2.9.1.2 固定 IP](#.E5.9B.BA.E5.AE.9A_IP)
        *   [2.9.2 無線網路](#.E7.84.A1.E7.B7.9A.E7.B6.B2.E8.B7.AF_2)
            *   [2.9.2.1 新增無線網路](#.E6.96.B0.E5.A2.9E.E7.84.A1.E7.B7.9A.E7.B6.B2.E8.B7.AF)
            *   [2.9.2.2 自動連上已知網路](#.E8.87.AA.E5.8B.95.E9.80.A3.E4.B8.8A.E5.B7.B2.E7.9F.A5.E7.B6.B2.E8.B7.AF)
        *   [2.9.3 類比式數據機、ISDN 或 PPPoE DSL](#.E9.A1.9E.E6.AF.94.E5.BC.8F.E6.95.B8.E6.93.9A.E6.A9.9F.E3.80.81ISDN_.E6.88.96_PPPoE_DSL_2)
    *   [2.10 建立初始 ramdisk 環境](#.E5.BB.BA.E7.AB.8B.E5.88.9D.E5.A7.8B_ramdisk_.E7.92.B0.E5.A2.83)
    *   [2.11 設定 root 密碼](#.E8.A8.AD.E5.AE.9A_root_.E5.AF.86.E7.A2.BC)
    *   [2.12 安裝並設定開機載入程式](#.E5.AE.89.E8.A3.9D.E4.B8.A6.E8.A8.AD.E5.AE.9A.E9.96.8B.E6.A9.9F.E8.BC.89.E5.85.A5.E7.A8.8B.E5.BC.8F)
        *   [2.12.1 BIOS 主機板](#BIOS_.E4.B8.BB.E6.A9.9F.E6.9D.BF)
            *   [2.12.1.1 Syslinux](#Syslinux)
            *   [2.12.1.2 GRUB](#GRUB)
        *   [2.12.2 UEFI 主機板](#UEFI_.E4.B8.BB.E6.A9.9F.E6.9D.BF)
            *   [2.12.2.1 Gummiboot](#Gummiboot)
            *   [2.12.2.2 GRUB](#GRUB_2)
    *   [2.13 卸載分割區並重啟系統](#.E5.8D.B8.E8.BC.89.E5.88.86.E5.89.B2.E5.8D.80.E4.B8.A6.E9.87.8D.E5.95.9F.E7.B3.BB.E7.B5.B1)
*   [3 安裝完成後](#.E5.AE.89.E8.A3.9D.E5.AE.8C.E6.88.90.E5.BE.8C)
    *   [3.1 使用者管理](#.E4.BD.BF.E7.94.A8.E8.80.85.E7.AE.A1.E7.90.86)
    *   [3.2 軟體包管理](#.E8.BB.9F.E9.AB.94.E5.8C.85.E7.AE.A1.E7.90.86)
    *   [3.3 服務管理](#.E6.9C.8D.E5.8B.99.E7.AE.A1.E7.90.86)
    *   [3.4 音效](#.E9.9F.B3.E6.95.88)
    *   [3.5 圖形使用者介面(GUI)](#.E5.9C.96.E5.BD.A2.E4.BD.BF.E7.94.A8.E8.80.85.E4.BB.8B.E9.9D.A2.28GUI.29)
        *   [3.5.1 安裝 X](#.E5.AE.89.E8.A3.9D_X)
        *   [3.5.2 安裝影像驅動](#.E5.AE.89.E8.A3.9D.E5.BD.B1.E5.83.8F.E9.A9.85.E5.8B.95)
        *   [3.5.3 安裝輸入驅動程式](#.E5.AE.89.E8.A3.9D.E8.BC.B8.E5.85.A5.E9.A9.85.E5.8B.95.E7.A8.8B.E5.BC.8F)
        *   [3.5.4 設定 X](#.E8.A8.AD.E5.AE.9A_X)
        *   [3.5.5 測試 X](#.E6.B8.AC.E8.A9.A6_X)
            *   [3.5.5.1 疑難排解](#.E7.96.91.E9.9B.A3.E6.8E.92.E8.A7.A3)
        *   [3.5.6 字型](#.E5.AD.97.E5.9E.8B)
        *   [3.5.7 選擇/安裝圖形介面](#.E9.81.B8.E6.93.87.2F.E5.AE.89.E8.A3.9D.E5.9C.96.E5.BD.A2.E4.BB.8B.E9.9D.A2)
*   [4 附錄](#.E9.99.84.E9.8C.84)

## 準備

**註記:** 如果您打算在既存的 GNU/Linux 發行版本下安裝 Arch，請參閱[這篇文章](/index.php/Install_from_Existing_Linux "Install from Existing Linux")，對透過 [VNC](/index.php/VNC "VNC") 或 [SSH](/index.php/SSH "SSH") 遠端安裝 Arch 的使用者而言會有幫助。欲透過 [SSH](/index.php/SSH "SSH") 連線遠端安裝 Arch Linux 的使用者，應閱讀[從 SSH 安裝](/index.php/Install_from_SSH "Install from SSH")提到的額外提示。

### 系統需求

Arch Linux 在任何 [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") 相容的機器上執行，最低需求 RAM 為 64 MB。一般而言將安裝 [base](https://www.archlinux.org/groups/x86_64/base/) 群組下所有軟體包，總共佔用約 500 MB 的硬碟空間。若您目前的空間不足，可以視狀況縮減安裝項目，但您必須真的瞭解自己在做什麼。

### 準備最新的安裝媒體

最新釋出的安裝媒體可以從官網的[下載](https://archlinux.org/download/)頁面取得。另外註明，單一 ISO 映像同時支援 32 和 64 位元的硬體架構。強烈建議您使用最新的 ISO 映像。

*   我們的安裝媒體都簽署過，強烈建議使用前先驗明正身。從下載頁面 (或任何一個表列的鏡像站) 將 _.sig_ 檔下載到存放 _.iso_ 檔的資料夾。在 Arch Linux 下以 root 身分使用 `pacman-key -v _iso-file_.sig`，其他環境下直接使用 gpg2，一樣用 root 身分執行：`gpg2 --verify _iso-file.sig_`。網站上也提供了 md5 和 sha1 校驗碼。

*   將 ISO 映像燒入 CD 或 DVD，用您習慣的燒錄軟體即可。Arch 下的燒錄程式請參考[光碟機#燒錄](/index.php/Optical_disc_drive#Burning "Optical disc drive")。

**註記:** 不同光碟機和 CD 本身的品質差異甚大。一般建議使用低速燒錄，以得到可靠的燒錄品質。若燒錄的 CD 發生任何異常狀況，請使用機器支援的最低速度再重新燒錄一遍。

*   也可以將 ISO 映像寫入 USB 碟。詳細的步驟請參閱 [USB 安裝媒體](/index.php/USB_Installation_Media_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "USB Installation Media (正體中文)")。

#### 透過網路安裝

除了光碟或隨身碟等方式之外，若您有一台可運作的伺服器，也可以選擇透過網路啟動 ISO 映像。請參閱 [PXE](/index.php/PXE "PXE") 文章了解更多資訊，並接續至[啟動安裝媒體](#.E5.95.9F.E5.8B.95.E5.AE.89.E8.A3.9D.E5.AA.92.E9.AB.94)。

#### 從既存的 Linux 系統安裝

在一個正在運行的 Linux 系統上安裝 Arch 是可行的。請參閱[從既存 Linux 安裝](/index.php/Install_from_Existing_Linux "Install from Existing Linux")。

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

## 安裝

您現在可以看到 Shell 的提示輸入畫面，自動以 root 的身分登入。 終端機下若需要編輯文字檔案，建議使用 nano。若不熟悉這個編輯器，參閱 [nano#nano 用法](/index.php/Nano#nano_usage "Nano")。

### 更改語言

**提示:** 對多數使用者而言此步驟可略過。若您打算在設定檔內寫入母語的話本步驟便能派上用場。例如：在 Wi-Fi 密碼內使用變音符號、以母語顯示系統訊息 (如可能的錯誤) 等。這裡的變更**只會**影響安裝程序。

預設的鍵盤布局為 `us` (美式鍵盤)。 如果您使用的是非[美式](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")的鍵盤布局，請執行：

```
# loadkeys **布局**

```

...「布局」可以是 `fr`, `uk`, `dvorak`, `be-latin1` 等鍵盤布局。雙字母的國家代碼清單可參閱[這裡](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2")。使用指令 `localectl list-keymaps` 列出所有可用鍵盤布局。

字型也需要作更改，因為大多數語言使用的字母數超過 26 個[英文字母](https://en.wikipedia.org/wiki/English_alphabet "wikipedia:English alphabet")，某些非英文字母會顯示為白框或其他錯誤符號。注意，字型名稱有分大小寫，請**確實**按照名稱鍵入：

```
# setfont Lat2-Terminus16

```

預設的語系為「英文(美國)」。若您想要更改安裝程序語系 (以下範例為德文)，在 `/etc/locale.gen` 移除您需要[語系](/index.php/Locale "Locale")前面的井字符號 `#`，也請保留「英文(美國)」以備不時之需。請選擇 `UTF-8` 項目。

 `# nano /etc/locale.gen` 

```
en_US.UTF-8 UTF-8
de_DE.UTF-8 UTF-8
```

```
# locale-gen
# export LANG=de_DE.UTF-8

```

(譯註：以上舉例僅供示範。在安裝期間設定中文語系將發生無法正常顯示中文的問題，建議忽略此步驟。)

### 啟用網路連線

**警告:** udev 自版本 197 開始不再按照以往 wlanX、ethX 的方式分配網路介面的名稱。如果您是從其他發行版本轉來的玩家，還是準備重灌但還不知道新的介面命名方案的 Arch 玩家，先不要急著認為無線裝置就是 wlan0、有線裝置就是 eth0。您可以使用 `ip link` 指令找出介面名稱。

開機過程中會自動啟動 `dhcpcd` 網路守護程序，並嘗試建立有線網路連線。試著 ping 向任何一個伺服器檢查連線是否已建立，下面例子使用 Google 的伺服器：

 `# ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

若出現 `ping: unknown host` 錯誤，首先檢查網路線有沒有接好，無線網路訊號強度夠不夠。若否，您將得照下面的步驟來手動設定網路。成功連上網路的話就跳至[準備儲存裝置](#.E6.BA.96.E5.82.99.E5.84.B2.E5.AD.98.E8.A3.9D.E7.BD.AE)。

#### 有線網路

如果您使用固定 IP 位址的有線網路連線，請依照以下的步驟。

首先，將開機時自動開始的 dhcpcd 服務停用：

```
# systemctl stop dhcpcd.service

```

確認網路卡的介面名稱。

 `# ip link` 

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp2s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT qlen 1000
    link/ether 00:11:25:31:69:20 brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT qlen 1000
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
```

本範例中，網路卡的介面為 `enp2s0f0`。有線網路卡的介面名稱通常會以字母「e」當開頭，不應該是「lo」或其他以「w」 開頭的名稱。

您也必須了解以下的設定資料：

*   固定 IP 位址。
*   子網路遮罩。
*   通信閘的 IP 位址。
*   名稱伺服器 (DNS) 的 IP 位址。
*   網域名稱(單一區域網路內請隨意)。

啟用裝載的有線網路介面 (例如 `enp2s0f0`)：

```
# ip link set enp2s0f0 up

```

加入位址：

```
# ip addr add **IP 位址**/**遮罩位元數** dev **介面名**

```

例如：

```
# ip addr add 192.168.1.2/24 dev enp2s0f0

```

需要更多選項的話，執行 `man ip` 查詢。

加入您的網路通訊閘 IP 位址:

```
# ip route add default via **IP 位址**

```

例如：

```
# ip route add default via 192.168.1.1

```

編輯 `resolv.conf`，改成您的名稱伺服器 IP 位置，以及本機域名：

 `# nano /etc/resolv.conf` 

```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com
```

**註記:** 目前最多只能加入三行 `nameserver` 字串。若要克服此限制，您可以使用本地快取名稱伺服器，如 [Dnsmasq](/index.php/Dnsmasq "Dnsmasq")。

到這裡，您的網路連線應該可以使用了。若還是不行，請參閱更詳細的[網路設定](/index.php/Network_Configuration_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Network Configuration (正體中文)")。

#### 無線網路

若您在安裝過程中需要無線網路連線 (Wi-Fi)，請依照以下的步驟進行。

首先，偵測無線網路介面的名稱。

 `# iw dev` 

```
phy#0
        Interface wlp3s0
                ifindex 3
                wdev 0x1
                addr 00:11:22:33:44:55
                type managed
```

在本範例中，`wlp3s0` 為可用的無線網路介面。無線網路的介面名稱通常會以字母「w」當開頭，不應該是「lo」或以「e」開頭的名稱。

**註記:** 若您沒有看到相似的輸出，代表尚未載入無線網路驅動。在此情況下您必須手動將驅動載入。更細節的資訊請參閱[無線網路設定](/index.php/Wireless_Setup "Wireless Setup")。

啟用介面：

```
# ip link set wlp3s0 up

```

觀察以下指令輸出，驗證介面是否啟用：

 `# ip link show wlp3s0` 

```
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000
    link/ether 00:11:22:33:44:55 brd ff:ff:ff:ff:ff:ff

```

`<BROADCAST,MULTICAST,UP,LOWER_UP>` 的 `UP` 代表介面已經啟用，不用理會 `state DOWN`。

大多數無線網路晶片組需要韌體以及對應的驅動。核心會嘗試偵測這兩者並自動載入。若您得到 `SIOCSIFFLAGS: No such file or directory` 之類的輸出訊息，代表您需要手動載入韌體。不確定的話，呼叫 `dmesg` 檢查核心日誌內是否有無線網路晶片組的韌體請求。假設您有一個 Intel 晶片組，它在開機時曾向核心請求韌體的話：

 `# dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

若沒有任何輸出，或許系統的無線網路晶片組並不需要韌體。

**警告:** (某些卡片需要的) 無線網路晶片組的韌體軟體包已預先安裝在 (CD/USB 碟上) Live 環境的 `/usr/lib/firmware` 資料夾，**但您必須將其安裝在實際的系統上，才能在重啟系統後提供無線網路功能！**如何安裝軟體包將在本教學的後面提及。請在重新啟動前確認無線網路的模組與韌體皆安裝完成！若不確定您的晶片組是否需安裝相關韌體，請參閱[無線網路設定](/index.php/Wireless_Setup "Wireless Setup")。

接下來使用 [netctl](/index.php/Netctl "Netctl") 的 `wifi-menu` 連上網路：

```
# wifi-menu wlp3s0

```

到這裡，您的網路連線應該可以使用了。沒有的話，請參閱更詳細的[無線網路設定](/index.php/Wireless_Setup "Wireless Setup")頁面。

##### 不使用 wifi-menu

您也可以使用 `iw dev wlp3s0 scan | grep SSID` 掃描可用網路並連接：

```
# wpa_supplicant -B -i wlp3s0 -c <(wpa_passphrase "_ssid_" "_psk_")

```

您需要將 _ssid_ 改為您的網路名稱 (例如「Linksys etc...」)，_psk_ 改為您的無線網路密碼。**記得保留網路名稱與密碼兩旁的引號。**

最後您需要給介面一個 IP 位址。您可以手動設定或使用 DHCP：

```
# dhcpcd wlp3s0

```

失敗的話請使用以下指令：

```
# echo 'ctrl_interface=DIR=/run/wpa_supplicant' > /etc/wpa_supplicant.conf
# wpa_passphrase <SSID> <密語> >> /etc/wpa_supplicant.conf
# ip link set <介面> up # 可能不需要，但不會造成任何傷害
# wpa_supplicant -B -D nl80211 -c /foobar.conf -i <介面名稱>
# dhcpcd -A <介面名稱>

```

#### 類比式數據機、ISDN 或 PPPoE DSL

xDSL、撥號和 ISDN 連線的使用者請參閱[以數據機直接連線](/index.php/Direct_Modem_Connection "Direct Modem Connection")。

#### 代理伺服器背後

若您在代理伺服器的背後上網，必須匯出 `http_proxy` 和 `ftp_proxy` 這兩個環境變數。更多資訊請參閱[代理伺服器設定](/index.php/Proxy_settings "Proxy settings")。

### 準備儲存裝置

**警告:** 分割硬碟會破壞內部資料。您得**非常**小心，建議在繼續之前先備份所有重要資料。

#### 選擇分割表類型

您需要在 [GUID 分割表](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) 和[主開機記錄](/index.php/Master_Boot_Record "Master Boot Record") (MBR) 中擇一使用。全新安裝的場合下建議使用比較先進的 GPT。

*   若您要設定一台與 Windows 雙重開機的系統，必須考慮這個問題：[硬碟分割#在 GPT 與 MBR 間選擇](/index.php/Partitioning#Choosing_between_GPT_and_MBR "Partitioning")。
*   建議在 UEFI 開機的環境下使用 GPT，某些 UEFI 韌體不支援 UEFI-MBR 開機。
*   某些 BIOS 系統可能有採用 GPT 的問題。更多資訊與可能解決方案請參閱 [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) 和 [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) 。

**註記:** 若您打算安裝在 USB 隨身碟，請參閱[將 Arch Linux 安裝在 USB 碟](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")。

#### 分割工具

完完全全的新手可以先嘗試使用圖形化的分割工具。例如以 [「Live」 CD 提供](http://gparted.sourceforge.net/livecd.php)的 [GParted](http://gparted.sourceforge.net/download.php)。GParted 也包含在大多數 Linux 發行版本的 Live CD 內，例如 [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu_(operating_system) "wikipedia:Ubuntu (operating system)") 跟 [Linux Mint](https://en.wikipedia.org/wiki/Linux_Mint "wikipedia:Linux Mint")。硬碟必須先進行[分割](/index.php/Partitioning "Partitioning")，接著格式化為[檔案系統](/index.php/File_systems "File systems")。

**提示:** 當使用 Gparted，選擇建立新分割表的選項時，預設會採用「msdos」分割表。若您打算跟隨提議建立 GPT 分割表，您需要選擇「進階」並在下拉選單中選擇「gpt」。

Gparted 比較容易使用，但若您只是想要在新硬碟上建立幾個分割區，只要使用安裝媒體中包含的 [fdisk 相關軟體](/index.php/Partitioning#Partitioning_tools "Partitioning")之一即可快速完成工作。下面的章節會提供 [gdisk](/index.php/Partitioning#Gdisk_usage_summary "Partitioning") 和 [fdisk](/index.php/Partitioning#Fdisk_usage_summary "Partitioning") 的簡短使用步驟。

#### 分割計畫

您可以決定一顆硬碟要分多少塊分割區，每個分割區所歸屬的系統目錄為何。從分割區到目錄的映射 (通常被稱為「掛載點」) 叫做[分割計畫](/index.php/Partitioning#Partition_scheme "Partitioning")。最簡單也不草率的方式是只建立一大塊 `/` 分割區。另一個常見的選擇是分一塊 `/` 和一塊 `/home` 分割區出來。

**額外需要的分割區：**

*   若您使用的是 [UEFI](/index.php/UEFI "UEFI") 主機板，將需要建立一塊額外的 [EFI 系統分割區](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface")。
*   若您使用的是 BIOS 主機板 (或計畫以 BIOS 相容模式開機)，且想要在以 GPT 分割的硬碟上設定 GRUB，將需要建立一塊額外的 [BIOS 開機分割區](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")，大小為 1 或 2 MiB，類型代碼為 `EF02`。Syslinux 則不需要此分割區。
*   若您有系統自我[硬碟加密](/index.php/Disk_encryption "Disk encryption")的需求，必須反應在分割計畫內。系統安裝好以後，新增加密的資料夾、容器或家目錄都沒有問題。
*   若您計劃讓根檔案系統使用 ext4 (-3,-2) 以外的檔案系統，得先檢查 GRUB 是否支援。若否，您需要再建立一個與 GRUB 相容的分割區 (例如 [ext4](/index.php/Ext4 "Ext4")) 給 `/boot` 使用。

若您希望設定一個置換分割區或置換檔案，詳情請參閱 [Swap](/index.php/Swap "Swap")。置換檔案比分割區還容易調整大小，也可以在安裝之後的任何時間建立，但無法在 Btrfs 檔案系統中使用。

#### 與 Windows 雙重開機的考量

若您已經有存在的作業系統安裝在硬碟內，請特別注意：在硬碟上寫入一個全新分割表，之前硬碟內所有資料都會遺失。

設定一個 Linux/Windows 雙重開機系統的建議方式是：先安裝好 Windows，只使用部分硬碟作為它的分割區使用。結束 Windows 安裝後，開機進入 Linux 安裝環境，建立給 Linux 使用的額外分割區，同時保持既存的 Windows 分割區不被改動。

某些新電腦預先搭載 Windows 8，它們有使用「安全開機」(Secure Boot)。Arch Linux 目前不支援「安全開機」，但某些安裝的 Windows 8 在 BIOS 關閉「安全開機」的情況下會無法開機。某些情況下，同時將「安全開機」與「快速開機」(Fastboot) 關閉，可以讓 Windows 8 不須「安全開機」即可開機。但是在關掉「安全開機」的情況下，Windows 8 開機有潛在的安全風險。因此，一個更好的選項是，保持 Windows 8 安裝的硬碟不動，用另一顆獨立硬碟給 Linux 安裝使用 - 可完全使用 GPT 分割表分割。完成之後，在電腦有兩顆硬碟的情況下，當要建立數個 ext4/FAT32/swap 分割區時最好選擇第二顆硬碟。此方式對小筆電而言通常不容易/不可能實踐。目前即使是支援「安全開機」的 Linux 發行版本，也無法同時在可靠的操作下達到完全穩定的狀態。

**警告:** Windows 8 包含一個新功能「快速開機」(Fast Startup)，就是將「關機」換成「休眠至硬碟」。大部分的情況下，該功能將導致 Windows 8 與任何其他 OS 共享的檔案系統在兩者輪流切換開機時損壞。就算您不打算分享檔案系統，EFI 系統上的 EFI 系統分割區也很有可能遭受到池魚之殃。因此，在使用 Windows 8 的電腦上安裝 Linux 之前，您應該根據[這裡](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html)的指示停用「快速開機」。

若您已經建立好分割區，請接續至[建立檔案系統](#.E5.BB.BA.E7.AB.8B.E6.AA.94.E6.A1.88.E7.B3.BB.E7.B5.B1)。

否則請看以下的範例。

#### 範例

Arch Linux 安裝媒介包含了以下的硬碟分割工具：`fdisk`, `gdisk`, `cfdisk`, `cgdisk`, `parted`。

**提示:** 使用 `lsblk` 指令列出與系統連接的硬碟，以及其存在分割區的大小。這能幫您確認分割的硬碟是否正確，添點信心。

以下的範例系統將包含 15 GB 的根目錄區，以及占用其他空間的[家目錄](/index.php/Partitioning#.2Fhome "Partitioning")區。請從 [MBR](/index.php/MBR "MBR") 或 [GPT](/index.php/GPT "GPT") 任選一項進行，不要同時選擇它們！

再次提醒，使用者可自行任意決定如何分割硬碟。本範例僅為讀者提供示範而已。也請參閱[硬碟分割](/index.php/Partitioning "Partitioning")。

##### 使用 cgdisk 建立 GPT 分割區

```
# cgdisk /dev/sda

```

	根目錄：

*   選擇 _New_ (或按 `N`) – `Enter` 默認第一個磁區 (2048) – 輸入 `15G` – `Enter` 默認預設十六進位代碼 (8300) – `Enter` 默認空白分割區名稱。

	家目錄：

*   按數次下鍵，將光標移動至較大的可用空間。
*   選擇 _New_ (或按 `N`) – `Enter` 默認第一個磁區 – `Enter` 使用剩餘的硬碟空間 (或是輸入想要的大小：例如 `30G`) – `Enter` 默認預設十六進位代碼 (8300) – `Enter` 默認空白分割區名稱。

畫面應該長的像這樣：

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

再三檢查，確認您對分割區的大小、分割表的配置滿意之後再繼續。

若您要從頭開始，直接選擇 _Quit_ (或按 `Q`) 不儲存任何變更離開，接著重新啟動 _cgdisk_。

滿意的話就選擇 _Write_ (或按 `Shift+W`) 結束，將分割表寫入硬碟。輸入 `yes` 並選擇 _Quit_ (或按 `Q`) 離開，不做任何額外變更。

##### 使用 fdisk 建立 MBR 分割區

**註記:** 另外一種工具 _cfdisk_ 的操作介面與 _cgdisk_ 類似，但目前它無法正確自動對齊第一個分割區。因此我們在這裡使用經典的 _fdisk_ 工具。

啟動 _fdisk_：

```
# fdisk /dev/sda

```

建立分割表：

*   `Command (m for help):` 輸入 `o` 並按 `Enter`

接著建立第一個分割區：

1.  `Command (m for help):` 輸入 `n` 並按 `Enter`
2.  分割區類型：`Select (default p):` 按 `Enter`
3.  `Partition number (1-4, default 1):` 按 `Enter`
4.  `First sector (2048-209715199, default 2048):` 按 `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (2048-209715199....., default 209715199):` 輸入 `+15G` 並按 `Enter`

接著建立第二個分割區：

1.  `Command (m for help):` 輸入 `n` 並按 `Enter`
2.  分割區類型：`Select (default p):` 按 `Enter`
3.  `Partition number (1-4, default 2):` 按 `Enter`
4.  `First sector (31459328-209715199, default 31459328):` 按 `Enter`
5.  `Last sector, +sectors or +size{K,M,G} (31459328-209715199....., default 209715199):` 按 `Enter`

現在預覽新的分割表：

*   `Command (m for help):` 輸入 `p` 並按 `Enter`

```
Disk /dev/sda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x5698d902

   Device Boot     Start         End     Blocks   Id  System
/dev/sda1           2048    31459327   15728640   83   Linux
/dev/sda2       31459328   209715199   89127936   83   Linux

```

接著將變更寫入硬碟：

*   `Command (m for help):` 輸入 `w` 並按 `Enter`

若一切順利，fdisk 將會顯示以下訊息並退出：

```
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks. 

```

碰到 _fdisk_ 遭遇錯誤而無法工作的狀況時，您可以使用 `q` 指令離開。

#### 建立檔案系統

只有作硬碟分割是不夠的；它們還需要一個[檔案系統](/index.php/File_systems "File systems")。將分割區格式化為 ext4 檔案系統：

**警告:** 再三檢查要格式化的分割區是否為 `/dev/sda1` 和 `/dev/sda2`。您可以使用 `lsblk` 幫助判斷。

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda2

```

若您有分割區要以 swap (代碼 82) 使用，別忘了將它格式化後啟用：

```
# mkswap /dev/sda_X_
# swapon /dev/sda_X_

```

UEFI 的使用者應該將 EFI 系統分割區格式化 (以下範例為 /dev/sd_XY_)：

```
# mkfs.fat -F32 /dev/sd_XY_

```

### 掛載分割區

每個分割區都有一個分別用的數字後綴。舉例來說，`sda1` 代表硬碟的**第一個**分割區，至於 `sda` 則代表**整顆**硬碟。

顯示目前的分割區配置：

```
# lsblk /dev/sda

```

**註記:** 不要在同一個目錄掛載兩個以上的分割區。另外，掛載的順序十分重要，請保持謹慎。

首先，在 `/mnt` 掛載根目錄的分割區。這裡將沿用上面的範例 (根據您的配置可能有所不同)：

```
# mount /dev/sda1 /mnt

```

接著將 home 以及其他的分割區 (`/boot`, `/var` 等等) 一起掛載上來：

```
# mkdir /mnt/home
# mount /dev/sda2 /mnt/home

```

UEFI 主機版的使用者，請掛載 EFI 系統分割區至指定的掛載點 (範例為 `/boot`)：

```
# mkdir -p /mnt/boot
# mount /dev/sd_XY_ /mnt/boot

```

### 選擇鏡像站

安裝之前先編輯 `mirrorlist`，把最想使用的鏡像站擺在最前面。這份 mirrorlist 文件，`pacstrap`會複製一份並安裝到新系統內，所以最好現在就設定完成。

 `# nano /etc/pacman.d/mirrorlist` 

```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on 2012-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

您可以選定一個鏡像站為**唯一**可用的鏡像站，並刪掉其他行。不過，建議保留其他兩、三個站點，以防第一個站點掛掉導致無法更新。

**提示:**

*   使用[鏡像站清單產生器](https://www.archlinux.org/mirrorlist/)獲取您所在國家的最新鏡像站清單。HTTP 鏡像站因為其[持久連接](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive") (keepalive) 的特性而比 FTP 鏡像站快速。在 FTP 協定下，Pacman 每下載一個軟體包就需要送一次訊號，導致短暫停頓。其他產生鏡像站清單的方式請參閱[分類鏡像站點](/index.php/Mirrors#Sorting_mirrors "Mirrors")和 [Reflector](/index.php/Reflector "Reflector")。
*   [Arch Linux 鏡像站狀態](https://archlinux.org/mirrors/status/)報告列出了鏡像站點的各種相關資料，如網路問題、資料收集問題、上一次同步時間等等。

**註記:**

*   之後每當您更改了鏡像站的清單，記得使用 `pacman -Syy` 重整軟體包清單，使它們能一致地更新。更多資訊請參閱[鏡像站點](/index.php/Mirrors "Mirrors")。
*   若您使用的安裝媒體版本較舊，裡面的鏡像站清單可能已經過期，更新 Arch Linux 時可能會導致問題 (詳見 [FS#22510](https://bugs.archlinux.org/task/22510))。建議如上面所述，趕快取得最新的鏡像站資訊。
*   [Arch Linux 論壇](https://bbs.archlinux.org/)上出現了阻擋 Pacman 更新/與軟體倉庫同步的網路問題回報 (詳見 [[1]](https://bbs.archlinux.org/viewtopic.php?id=68944) 以及 [[2]](https://bbs.archlinux.org/viewtopic.php?id=65728))。若您是原生安裝 Arch Linux，用其他替代品取代 Pacman 預設的檔案下載程式可以解決問題 (更多資訊請參閱[增進 Pacman 表現](/index.php/Improve_pacman_performance "Improve pacman performance"))。若您在 [VirtualBox](/index.php/VirtualBox "VirtualBox") 上安裝 Arch Linux 為客體 OS，在機器屬性內使用 「主機介面」(Host Interface) 取代「NAT」也可以解決問題。

### 安裝基礎系統

我們將使用 _pacstrap_ 腳本安裝基礎系統。省略 `-i` 選項可跳過提示，直接安裝 [base](https://www.archlinux.org/groups/x86_64/base/) 群組內所有軟體包。

```
# pacstrap -i /mnt base

```

**註記:**

*   如果 Pacman 在驗證軟體包時失敗，請用 `Ctrl+C` 停止安裝程序，並使用 `cal` 檢查系統時間。假如系統時間無效 (如老早之前的 2010 年)，簽署金鑰會被認定為過期 (或無效)，軟體包的簽署檢查失敗，安裝程序就會被中斷。請使用指令 `ntpd -qg` 確保系統時間是否正確，再重新執行 pacstrap 指令。更多校正系統時間的資訊請參閱[時間](/index.php/Time "Time")頁面。
*   若 Pacman 抱怨 `error: failed to commit transaction (invalid or corrupted package)`，請執行下面的指令：

```
# pacman-key --init && pacman-key --populate archlinux

```

這樣就完成一個基本的 Arch 系統了。其他軟體包之後可以使用 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 安裝。

### 產生 fstab

用以下指令產生 [fstab](/index.php/Fstab "Fstab") 檔案。我們將使用 UUID，因為它有一定的優點 (請參閱 [fstab#偵測檔案系統](/index.php/Fstab#Identifying_filesystems "Fstab"))。若您想改用硬碟標籤，將 `-U` 選項改為 `-L`。

```
# genfstab -U -p /mnt >> /mnt/etc/fstab
# nano /mnt/etc/fstab

```

**警告:** fstab 檔案在產生之後一定要檢查。若執行 genfstab 或之後的安裝過程中遇到任何錯誤，**不要**再執行一次 genfstab；直接編輯 fstab 檔案即可。

另外一些考量如下：

*   最後一個欄位決定了系統啟動時檢查分割區的順序：`1` 給需要最先檢查的 (非 `btrfs`) 根目錄分割區；`2` 則給其他在啟動時要檢查的分割區；`0` 代表「不檢查」(參閱 [fstab#欄位定義](/index.php/Fstab#Field_definitions "Fstab"))。
*   所有 [btrfs](/index.php/Btrfs "Btrfs") 分割區的該欄位應該填 `0`。正常情況下，您也會希望自己的**置換** (swap) 分割區填 `0`。

### Chroot 並設定基礎系統

接下來，[chroot](/index.php/Chroot "Chroot") 進入全新安裝的系統：

```
# arch-chroot /mnt /bin/bash

```

**註記:** 省略 `/bin/bash` 將以 sh shell 進入。

這個階段將為您的 Arch Linux 基礎系統設定主要的設置檔。若您想要改變預設值，可以編輯或建立 (若檔案不存在) 這些檔案。

為了確保系統設置正確，請遵循以下步驟，並盡可能瞭解其中用處。

#### 本地化

**glibc** 與其他支援本地化的程式/函式庫會使用本地化設定，來渲染文字、顯示正確的地區貨幣、時間與日期格式、字母順序以及其他本地標準。

在這裡需要編輯兩個檔案：`locale.gen` 和 `locale.conf`。

將您需要用到的語系都取消註解，只要移除該行前面的 `#` 即可。非常建議只使用 `UTF-8` 項目：

 `# nano /etc/locale.gen` 

```
...
en_US.UTF-8 UTF-8
#en_US ISO-8859-1
...
#zh_TW.EUC-TW EUC-TW
zh_TW.UTF-8 UTF-8
#zh_TW BIG5

```

**註記:** `locale.gen` 檔案預設註解掉所有語系。

產生 `locale.gen` 內指定的語系：

```
# locale-gen

```

**註記:** 這個指令在每次 **glibc** 升級時都會執行。

為您選擇的語系建立 `/etc/locale.conf` 檔案：

```
# echo LANG=en_US.UTF-8 > /etc/locale.conf

```

**註記:** 指定給 `LANG` 變數的語系必須已經在 `/etc/locale.gen`取消註解。 `locale.conf` 檔案預設並不存在。只要設定 `LANG` 就夠了，其他變數將會以此當作預設值使用。

將您選擇的語系匯出：

```
# export LANG=en_US.UTF-8

```

**提示:** 若要設定其他 `LC_*` 變數為其他語系，執行 `locale` 檢查可用選項後，將它們加入 `locale.conf`。我們不建議設定 `LC_ALL` 變數。詳情請參閱[語系#設定全系統語系](/index.php/Locale#Setting_system-wide_locale "Locale")。

#### 終端機字型與鍵盤布局

若您在安裝過程的[一開始](#.E6.9B.B4.E6.94.B9.E8.AA.9E.E8.A8.80)設定過鍵盤布局的話，由於我們已經換到新安裝的系統環境，請現在再載入一遍。例如：

```
# loadkeys _us_
# setfont Lat2-Terminus16

```

要使設定在重啟系統後依然生效，編輯 `vconsole.conf` (若檔案不存在則新建一個)：

 `# nano /etc/vconsole.conf` 

```
KEYMAP=us
FONT=Lat2-Terminus16
```

*   `KEYMAP` – 請注意這裡的設定值只對 TTY (文字介面) 有用，不適用於 Xorg 或任何圖形視窗管理員。

*   `FONT` – `/usr/share/kbd/consolefonts/` 內可用的替代字型。預設 (留空) 是安全的，但某些非英文字母可能會變成白框或亂碼。建議您更改為 `Lat2-Terminus16`，因為 `/usr/share/kbd/consolefonts/README.Lat2-Terminus16` 號稱支援了「近 110 種語言」。

*   `FONT_MAP` 的可用選項 – 定義開機時載入的終端機布局。請閱讀 `man setfont`。將它移除或留空都沒關係。

更多資訊請參閱[字型#終端機字型](/index.php/Fonts_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E7.B5.82.E7.AB.AF.E6.A9.9F.E5.AD.97.E5.9E.8B "Fonts (正體中文)")或呼叫 `man vconsole.conf`。

#### 時區

各地區以及子分區可以在 `/usr/share/zoneinfo/<地區>/<子分區>` 目錄下找到。

檢查目錄 `/usr/share/zoneinfo/` 尋找可使用的**地區**：

```
# ls /usr/share/zoneinfo/

```

以同樣方式檢查是否有可用的**子分區**：

```
# ls /usr/share/zoneinfo/Asia

```

使用以下指令，建立軟連結 `/etc/localtime`，連結至您所屬的時區檔 `/usr/share/zoneinfo/<地區>/<子分區>`：

```
# ln -s /usr/share/zoneinfo/<地區>/<子分區> /etc/localtime

```

**範例：**

```
# ln -s /usr/share/zoneinfo/Asia/Taipei /etc/localtime

```

#### 硬體時鐘

請統一您所有作業系統的硬體時鐘模式。否則它們可能會覆寫硬體時鐘，造成時間偏移。

使用以下任一指令，自動產生 `/etc/adjtime`：

*   **UTC** (建議使用)

**註記:** 硬體時鐘使用 [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time")，不代表軟體會以 UTC 的方式顯示時間。

	 `# hwclock --systohc --utc` 

*   **localtime** (不建議；Windows 預設使用)

**警告:** 使用 _localtime_ 可能引發數個已知且無法修復的臭蟲。但目前沒有放棄 _localtime_ 支援的計劃。

	 `# hwclock --systohc --localtime` 

**提示:** 若您有 (或打算建立) Linux 與 Windows 的雙重開機系統：

*   建議：將 Arch Linux 和 Windows 設定為使用 UTC。Windows 需要加入一個[修正註冊碼](/index.php/Time#UTC_in_Windows "Time")。另外確保停用 Windows 的線上同步時間功能，否則硬體時鐘又會回復成 _localtime_ 的預設值。

*   不建議：將 Arch Linux 設定為 _localtime_，並取消任何時間服務如 [NTPd](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")。硬體時鐘將交由 Windows 處理，若您的所在地區有實施[日光節約時間](https://en.wikipedia.org/wiki/Daylight_saving_time "wikipedia:Daylight saving time")，要記得每年最少要啟動 Windows 兩次 (春季與秋季)。要是長久未打開 Windows，Arch 可能會出現比實際時間少/多一個小時的狀況，這已經成為 Arch 論壇的老問題了。

#### 核心模組

**提示:** 這裡僅做示例，您不需要作任何設定。所有需要的模組都會自動被 udev 載入，只有在少數情況下才需要加東西。只需加入據您所知缺漏的模組即可。

若要在開機時載入核心模組，在 `/etc/modules-load.d/` 底下放入 `*.conf` 檔案，檔名以模組名稱命名。

 `# nano /etc/modules-load.d/virtio-net.conf` 

```
# 開機時載入 'virtio-net.ko'

virtio-net
```

若 `*.conf` 內包含多個模組，一行只能寫一個模組名稱。這裡有個良好的範例可供參考：[VirtualBox Guest Additions](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox")。

空行、以 `#` 或 `;` 開頭的行將會被忽略。

#### 主機名稱

設定您喜歡的[主機名稱](https://en.wikipedia.org/wiki/hostname "wikipedia:hostname") (例如 _arch_)：

```
# echo _arch_ > /etc/hostname

```

**註記:** 您不需要編輯 `/etc/hosts`。

### 設定網路

現在，您需要為全新安裝的環境再設定一次網路。步驟與要求跟[上面](#.E5.95.9F.E7.94.A8.E7.B6.B2.E8.B7.AF.E9.80.A3.E7.B7.9A)十分類似，不同的是我們要將網路連線設定為開機時自動執行。

**註記:**

*   更多深入的網路設定資訊請參閱[設定網路](/index.php/Network_Configuration_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Network Configuration (正體中文)")和[無線網路設定](/index.php/Wireless_Setup "Wireless Setup")。
*   若您要使用舊的介面命名模式 (如 eth* 和 wlan*)，在 `/etc/udev/rules.d/80-net-name-slot.rules` 建立一個空白檔案，將會遮蓋 `/usr/lib/udev/rules.d` 底下相同名稱的檔案 (或者不使用空白檔案，建立指向 `/dev/null` 的軟連結也是可接受的遮蓋方式)

#### 有線網路

##### 動態 IP

	使用 dhcpcd

若您只有使用單一固定的有線網路，並不需要一個專門的網路管理服務，只要啟用 `dhcpcd` 服務即可

```
# systemctl enable dhcpcd.service

```

**註記:** 若無法作用，使用：`# systemctl enable dhcpcd@**介面名稱**.service`

	使用 netctl

從 `/etc/netctl/examples` 複製一份樣本設定檔到 `/etc/netctl`：

```
# cd /etc/netctl
# cp examples/ethernet-dhcp my_network

```

根據需求編輯設定檔 (將 `Interface` 原本填的 `eth0` 更新為網路配接器的 ID，可執行 `ip link` 查詢)：

```
# nano my_network

```

啟用 `my_network` 設定檔：

```
# netctl enable my_network

```

**註記:** 您會得到一個訊息："Running in chroot, ignoring request." (在 chroot 下執行，忽略請求)。目前該訊息可以忽略。

	使用 netctl-ifplugd

**警告:** 在明確啟用設定檔 (如 `netctl enable <設定檔>`) 的同時不能使用這個方式。

或者您也可以使用 `netctl-ifplugd`，可以有效處理新網路的動態連線：

安裝 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) (`netctl-ifplugd` 軟體包需要)：

```
# pacman -S ifplugd

```

接著啟用您需要的介面：

```
# systemctl enable netctl-ifplugd@<介面>.service

```

**提示:** [Netctl](/index.php/Netctl "Netctl") 也提供 `netctl-auto`，可和 `netctl-ifplugd` 配合一同處理有線網路連線設定檔。

##### 固定 IP

	使用 netctl 在開機時連線

從 `/etc/netctl/examples` 複製一份樣本設定檔至 `/etc/netctl`：

```
# cd /etc/netctl
# cp examples/ethernet-static my_network

```

依需求編輯設定檔 (修改 `Interface`、`Address`、`Gateway` 和 `DNS`)：

```
# nano my_network

```

*   注意 `Address` 下的 `/24` 代表 [CIDR 表示法](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing")：表示 `255.255.255.0` 子網路遮罩

啟用上面建立的設定檔，在每次開機時啟動：

```
# netctl enable my_network

```

	使用 systemd 在開機時連線

參閱[網路設定#於啟動時通過 systemd 手動連線](/index.php/Network_Configuration_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E6.96.BC.E5.95.9F.E5.8B.95.E6.99.82.E9.80.9A.E9.81.8E_systemd_.E6.89.8B.E5.8B.95.E9.80.A3.E7.B7.9A "Network Configuration (正體中文)")。

#### 無線網路

**註記:** 若您的無線網路配接器需要韌體 (如上面所述的[啟用網路連線](#.E7.84.A1.E7.B7.9A.E7.B6.B2.E8.B7.AF)小節，以及[這裡](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration"))，請安裝包含該韌體的軟體包。大多時候 [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) 軟體包會包含需要的韌體。但對某些裝置而言，需要的韌體會落在自己的軟體包內。例如： `# pacman -S zd1211-firmware` 更多資訊請參閱[設定無線網路#安裝驅動/韌體](/index.php/Wireless_network_configuration#Installing_driver.2Ffirmware "Wireless network configuration")。

安裝連上無線網路所需的 [iw](https://www.archlinux.org/packages/?name=iw) 和 [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)：

```
# pacman -S iw wpa_supplicant

```

##### 新增無線網路

	使用 wifi-menu

安裝 [dialog](https://www.archlinux.org/packages/?name=dialog) (`wifi-menu` 軟體包需要)：

```
# pacman -S dialog

```

完成剩餘的安裝步驟後重啟系統，就可以使用 `wifi-menu **介面名稱**` 連上網路 (`**介面名稱**`代表您的無線網路晶片組的介面)。

```
# wifi-menu **介面名稱**

```

**警告:** 若您已經離開 chroot 環境，必須在重啟系統**之後**才能進行本操作。本指令產生的程序將和 chroot 環境外執行的網路程序相牴觸。要不然您可以使用之前提到的模板，只手動調整網路設定檔，就完全不須擔心使用 `wifi-menu` 的問題。

	使用手動 netctl 設定檔

從 `/etc/netctl/examples` 複製一份網路設定檔至 `/etc/netctl`：

```
# cd /etc/netctl
# cp examples/wireless-wpa my-network

```

依需求編輯設定檔 (修改 `Interface`、`ESSID` 和 `Key`)：

```
# nano my-network

```

啟用上面建立的設定檔，在每次開機時開始使用：

```
# netctl enable my-network

```

##### 自動連上已知網路

**警告:** 在明確啟用設定檔 (如 `netctl enable <設定檔>`) 的同時不能使用這個方式。

安裝 [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond) (`netctl-auto` 軟體包需要)：

```
# pacman -S wpa_actiond

```

啟用 `netctl-auto` 服務，連上已知的網路並有效處理漫遊與斷線問題：

```
# systemctl enable netctl-auto@**介面名稱**.service

```

**提示:** [Netctl](/index.php/Netctl "Netctl") 也提供 `netctl-ifplugd`，可和 `netctl-auto` 配合一同處理有線網路連線設定檔。

#### 類比式數據機、ISDN 或 PPPoE DSL

xDSL、撥接與 ISDN 連線請參閱[以數據機直接連線](/index.php/Direct_Modem_Connection "Direct Modem Connection")。

### 建立初始 ramdisk 環境

**提示:** 多數使用者可以跳過此步，使用 `mkinitcpio.conf` 所提供的預設值。之前在使用 `pacstrap` 安裝 [linux](https://www.archlinux.org/packages/?name=linux) 軟體包 (Linux 核心) 時，就已經根據 `mkinitcpio.conf` 產生 initramfs 映像 (在 `/boot` 資料夾下 )。

若您將系統的根目錄安裝在 USB 碟，或是使用了 RAID/LVM，還是將 `/usr` 放在額外的分割區內，都需要設定好正確的[鉤子](/index.php/Mkinitcpio#HOOKS "Mkinitcpio")。

根據您的需求編輯 `/etc/mkinitcpio.conf`，並重新產生 initramfs 映像：

```
# mkinitcpio -p linux

```

**註記:** Arch 在 QEMU 上的 VPS 安裝 (如，使用 `virt-manager`)，可能需要 `mkinitcpio.conf` 內的 `virtio` 模組，才能啟動系統。 `# nano /etc/mkinitcpio.conf`  `MODULES="virtio virtio_blk virtio_pci virtio_net"` 

### 設定 root 密碼

設定 root 密碼：

```
# passwd

```

### 安裝並設定開機載入程式

#### BIOS 主機板

BIOS 系統有數種開機載入程式可以使用，完整清單請參閱[開機載入程式](/index.php/Boot_loaders "Boot loaders")。請選擇對您而言最方便的一套。這裡我們舉出兩種作為範例：

*   Syslinux (目前) 限制只能從安裝系統的分割區內載入檔案。設定檔比較淺顯易懂。[這裡](https://bbs.archlinux.org/viewtopic.php?pid=1109328#p1109328)有一份範例設定檔可供參考。

*   GRUB 的功能較為豐富，且支援更複雜的系統狀況。設定檔與 sh 腳本語言接近，對新手而言較難以手動編寫。建議自動產生一份設定檔。

##### Syslinux

若您之前選擇讓硬碟使用 GUID 分割表 (GPT)，需要安裝 [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) 軟體包才能使 syslinux 正常運作。

```
# pacman -S gptfdisk

```

安裝 [syslinux](https://www.archlinux.org/packages/?name=syslinux) 軟體包，並使用 `syslinux-install_update` 腳本自動**安裝**檔案 (`-i`)、設定開機旗標以**啟用**分割區 (`-a`)，並安裝 _MBR_ 開機碼 (`-m`)：

```
# pacman -S syslinux
# syslinux-install_update -i -a -m

```

設定 `syslinux.cfg` 以指向正確的根目錄分割區。這個步驟相當重要。指向錯誤的分割區將無法啟動 Arch Linux。將下面的 `/dev/sda3` 改為您的根目錄分割區所在地 **(若您依照[這個範例](#.E6.BA.96.E5.82.99.E5.84.B2.E5.AD.98.E8.A3.9D.E7.BD.AE)分割硬碟，您的根目錄分割區是 `/dev/sda1`)**。fallback 項目也如法炮製。

 `# nano /boot/syslinux/syslinux.cfg` 

```
...
LABEL arch
        ...
        APPEND root=**/dev/sda3** rw
        ...
```

更多設定、使用 Syslinux 的資訊請參閱 [Syslinux](/index.php/Syslinux "Syslinux")。

##### GRUB

安裝 [grub](https://www.archlinux.org/packages/?name=grub) 軟體包，接著執行 `grub-install` 安裝開機載入程式：

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

**註記:**

*   將 `/dev/sda` 改成您安裝 Arch 的硬碟代號。不要加上分割區號碼 (不要使用 `sda_X_`)。
*   使用 BIOS 主機板與 GPT 分割硬碟的使用者，還需要一個「BIOS 開機分割區」。請參閱 GRUB 頁面的 [GPT 特定步驟](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")。
*   grub 軟體包會連帶安裝一個 `/boot/grub/grub.cfg` 樣本，隨後的 `grub-*` 指令可能無法覆寫它。確認您是否有改變到 `grub.cfg`，而非將變更寫進 `grub.cfg.new` 或某些類似檔案。

雖然 `grub.cfg` 可以手動建立，但建議新手選擇讓程式自動產生：

**提示:** 若要自動搜尋電腦上安裝的其他作業系統，在執行以下指令前請先安裝 [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`)。

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

更多設定、使用 GRUB 的資訊請參閱 [GRUB](/index.php/GRUB "GRUB")。

#### UEFI 主機板

UEFI 系統有數個開機載入程式可以使用。完整清單請參閱[開機載入程式](/index.php/Boot_loaders "Boot loaders")。請選擇對您而言最方便的一套。這裡我們舉出兩種作為範例：

*   [gummiboot](/index.php/Gummiboot "Gummiboot") 是一套迷你 UEFI 開機管理員，基本上為 [EFISTUB](/index.php/EFISTUB "EFISTUB") 核心與其他 UEFI 應用程式提供選單。這是建議的 UEFI 開機方案。
*   GRUB 是個更為完整的開機載入程式，若 Gummiboot 發生問題，就使用這個。

**註記:** 要以 UEFI 開機，硬碟需要以 GPT 方式分割，且必須存在一個 [EFI 系統分割區](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (512 MiB 或更大，gdisk 類型 `EF00`，並以 FAT32 格式化)。在以下的範例中假設該分割區掛載為 `/boot`。若您有從頭照著教學一步一步進行，應該已經完成這些工作了。

##### Gummiboot

首先安裝 [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) 軟體包，接著執行 `gummiboot install`，將開機管理員安裝至 EFI 系統分割區：

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars              # 若已經掛載則略過
# pacman -S gummiboot
# gummiboot install

```

您將必須手動建立設定檔案，將 Arch Linux 項目加入 gummiboot 管理員。建立 `/boot/loader/entries/arch.conf` 並新增以下內容，將 `/dev/sdaX` 改成您的根目錄分割區，通常為 `/dev/sda2`：

 `# nano /boot/loader/entries/arch.conf` 

```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

更多設定、使用 gummiboot 的資訊請參閱 [gummiboot](/index.php/Gummiboot "Gummiboot")。

##### GRUB

安裝 [grub](https://www.archlinux.org/packages/?name=grub) 和 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) 軟體包，接著執行 `grub-install` 安裝開機載入程式：

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars             # 若已經掛載則略過
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

接下來，雖然 `grub.cfg` 可以手動建立，但建議新手選擇讓程式自動產生：

**提示:** 若要自動搜尋電腦上安裝的其他作業系統，在執行以下指令前請先安裝 [os-prober](https://www.archlinux.org/packages/?name=os-prober)。但目前並不肯定 os-prober 能正確偵測 UEFI 的作業系統。

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

更多設定、使用 GRUB 的資訊請參閱 [GRUB](/index.php/GRUB "GRUB")。

### 卸載分割區並重啟系統

離開 chroot 環境：

```
# exit

```

所有的分割區都掛載在 `/mnt`，使用以下指令卸載：

```
# umount -R /mnt

```

重新啟動電腦：

```
# reboot

```

**提示:** 請確認是否已移除安裝媒體，以免開機後再度跑回安裝環境。

## 安裝完成後

現在，您全新的 Arch Linux 基本系統已經是可以工作的 GNU/Linux 環境了，剩下就有待您的巧手了。若您剛使用 Linux 不久，參考一下新系統包含的[核心工具](/index.php/Core_Utilities_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Core Utilities (正體中文)")會很有幫助。

### 使用者管理

根據[使用者管理](/index.php/Users_and_Groups_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E8.80.85.E7.AE.A1.E7.90.86 "Users and Groups (正體中文)")的說明新增任何 root 以外您需要的使用者帳號。以 root 帳號作為日常使用、或透過 [SSH](/index.php/SSH "SSH") 連接伺服器都不是好的習慣。您應該只在進行管理任務時才使用 root 帳號。

### 軟體包管理

Pacman 是 Arch Linux 的「軟體包管理員」(**pac**kage **man**ager)。請參閱 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 和 [FAQ#軟體包管理](/index.php/FAQ_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E8.BB.9F.E9.AB.94.E5.8C.85.E7.AE.A1.E7.90.86 "FAQ (正體中文)")瞭解如何安裝、升級並管理軟體包。 由於 [Arch 的設計哲學#正確的程式碼勝過一時的便利](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E6.AD.A3.E7.A2.BA.E7.9A.84.E7.A8.8B.E5.BC.8F.E7.A2.BC.E5.8B.9D.E9.81.8E.E4.B8.80.E6.99.82.E7.9A.84.E4.BE.BF.E5.88.A9 "The Arch Way (正體中文)")，隨著 Arch Linux 的改變，更新系統**之前**需手動介入的狀況是免不了的。 訂閱 [arch-announce 郵遞清單](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)，或在每次更新前檢查首頁的 [Arch 新聞](https://www.archlinux.org/)。您也可以訂閱[這個 RSS 消息源](https://www.archlinux.org/feeds/news/)，或是追蹤 Twitter 上的 [@archlinux](https://twitter.com/archlinux)，都能對您有所幫助。

若您安裝了 Arch Linux x86_64 版本，且打算使用 32 位元的應用程式，或許會想[啟用 [multilib] 倉庫](/index.php/Multilib "Multilib")。

各個倉庫的用途詳情請參閱[官方倉庫](/index.php/Official_Repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official Repositories (正體中文)")。

### 服務管理

Arch Linux 使用 [systemd](/index.php/Systemd "Systemd") 這套 Linux 下的系統服務管理程式來初始化系統。為了維護您的 Arch Linux，請稍微了解一下它的基本概念與操作。所有和 systemd 的互動都可由 `systemctl` 指令完成。更多資訊請詳閱 [systemd#systemctl 基本用法](/index.php/Systemd#Basic_systemctl_usage "Systemd")。

### 音效

[ALSA](/index.php/ALSA "ALSA") 通常一裝完就可使用，通常只需要取消靜音即可。安裝 [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (已包含 `alsamixer`) 並依照[這裡](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")的指示進行。

ALSA 是核心的組件之一，建議使用。若無法使用，[OSS](/index.php/OSS "OSS") 會是個不錯的替代品。若您有進階的音效需求，請參閱[聲音系統](/index.php/Sound_system "Sound system")。

### 圖形使用者介面(GUI)

#### 安裝 X

[X 視窗系統](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (又稱之為 **X11** 或 **X**) 是套網路與顯示通訊協定，提供了以點陣圖顯示的視窗功能，包含了建立「圖形使用介面」 (GUI) 的標準工具集和協定。

安裝 [Xorg](/index.php/Xorg "Xorg") 基本軟體包：

```
# pacman -S xorg-server xorg-server-utils xorg-xinit

```

安裝 [mesa](https://en.wikipedia.org/wiki/Mesa_(computer_graphics) "wikipedia:Mesa (computer graphics)") (提供 3D 支援)：

```
# pacman -S mesa

```

#### 安裝影像驅動

**註記:** 若您是以 VirtualBox 安裝 Arch 為客體，就不需安裝影像驅動。請參閱 [Arch Linux 客體](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox")了解安裝與設定「客體附屬工具」(Guest Additions)，並跳到之後的[設定](#.E8.A8.AD.E5.AE.9A_X)部分。

Linux 核心包含了開源影像驅動，支援硬體加速幀緩衝。不過，X11 下 OpenGL 與 2D 加速皆需要使用者區的支援。

若您不曉得您的機器使用什麼顯示晶片組，請執行：

```
$ lspci | grep VGA

```

完整的開源影像驅動清單可從軟體包資料庫中搜尋：

```
$ pacman -Ss xf86-video | less

```

`vesa` 驅動是一般性的模式設定驅動，幾乎在所有 GPU 上都可以運作，但不提供任何 2D 或 3D 加速功能。若更好的驅動沒有找到或載入失敗，Xorg 會退而求其次使用 vesa。安裝 vesa：

```
# pacman -S xf86-video-vesa

```

為了讓影像加速可以運作，並使用 GPU 可設置的所有模式，您需要一個適當的影像驅動程式。請參閱 [Xorg#驅動安裝](/index.php/Xorg#Driver_installation "Xorg")中常見影像驅動表。

#### 安裝輸入驅動程式

Udev 可以毫無問題地偵測您的硬體。`evdev` 驅動 ([xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)) 是目前的熱插拔輸入驅動，幾乎適用於所有裝置，所以多數情況下您並不需要安裝輸入驅動。`evdev` 已因為 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 軟體包的相依性而被安裝好了。

筆記型電腦 (或觸控螢幕) 的使用者會需要 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) 軟體包，以讓觸控板/觸控螢幕作用：

```
# pacman -S xf86-input-synaptics

```

若需要微調觸控板，或是發生觸控板相關的錯誤，請參閱[觸控板](/index.php/Touchpad_Synaptics "Touchpad Synaptics")文章。

#### 設定 X

**警告:** 專有驅動通常需要在安裝之後重啟系統。詳情請參閱 [NVIDIA](/index.php/NVIDIA "NVIDIA") 或 [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")。

Xorg 具備自動偵測，`xorg.conf` 已經不太需要。若您仍希望手動設定 X 伺服器，請參閱 [Xorg](/index.php/Xorg "Xorg") wiki 頁面。

若您使用的鍵盤並非標準[美式](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")，可能需要[設定鍵盤布局](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")。

**註記:** `XkbLayout` 的值可能和 `loadkeys` 指令使用的鍵碼不同。`/usr/share/X11/xkb/rules/base.lst` 下有許多鍵盤配置與其變種的清單 (在開頭為 `! layout` 的行之後)。例如，`gb` 對應到「英文(英國)」，對終端機而言就是 `loadkeys uk`。

#### 測試 X

**提示:** 以下為選用步驟。若您是第一次安裝 Arch Linux，或是將 Arch 安裝在不熟悉的硬體上時，可以做個測試。

**註記:** 如果您的輸入裝置在測試中不起作用，請從 [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) 群組安裝需要的驅動後再試一遍。完整的可用輸入驅動清單可從呼叫 Pacman 搜尋得到 (按 `Q` 離開)：

```
$ pacman -Ss xf86-input | less

```

若您不需要[熱插拔](https://en.wikipedia.org/wiki/Hot-plugging "wikipedia:Hot-plugging")功能，只需安裝 [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) 或 [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse)，否則 (建議) 使用 `evdev` 做為輸入驅動。

安裝預設環境：

```
# pacman -S xorg-twm xorg-xclock xterm

```

若您在安裝 Xorg 前新增了非 root 的使用者帳號，該帳號的家目錄下會出現 `.xinitrc` 模版檔，必須將它刪除或註解掉。若選擇刪除，**X** 將以上述安裝的預設環境啟動。

```
$ rm ~/.xinitrc

```

**註記:** 當登入時，X 必須從同一台 tty 上執行，以保存 logind 階段。此由預設的 `/etc/X11/xinit/xserverrc` 控制。

執行下列指令，啟動 Xorg (測試) 階段：

```
$ startx

```

螢幕將出現幾個可移動的視窗，且您的滑鼠應該可以使用。如果您認為 **X** 執行的可圈可點、沒有問題，可以在 **X** 下的終端機輸入 `exit` 離開 **X** 環境，回到文字模式。

```
$ exit

```

若螢幕變成一片漆黑，可以試著切換到不同的虛擬終端機 (如 `Ctrl+Alt+F2`)，並以 root 身分登入(鍵入「root」、按 `Enter`、打入密碼後再按 `Enter` 即可)。

您可以試著殺掉 **X** 伺服器程序：

```
# pkill X

```

沒有作用的話就直接重啟系統：

```
# reboot

```

##### 疑難排解

若發生任何問題，到 `Xorg.0.log` 檢查錯誤。以 `(EE)` 開頭的行位代表錯誤，以 `(WW)` 開頭則代表警告，或許能提供一些問題發生的提示。

```
$ grep EE /var/log/Xorg.0.log

```

若看過 [Xorg](/index.php/Xorg "Xorg") 文章後仍無法解決問題，需要到 Arch Linux 論壇或 IRC 頻道尋求協助的話，記得安裝 [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste)，讓熱心的網友能透過連結了解您的問題：

```
# pacman -S wgetpaste
$ wgetpaste ~/.xinitrc
$ wgetpaste /etc/X11/xorg.conf
$ wgetpaste /var/log/Xorg.0.log

```

**註記:** 在網路上詢問問題時，請記得提供所有相關資訊 (硬體、驅動資訊等)。

#### 字型

預設系統只內含不可擴展的點陣字型，您可能希望安裝一套 TrueType 字型。如果您打算使用一個全方位功能的[桌面環境](/index.php/Desktop_environment "Desktop environment") (如 [KDE](/index.php/KDE "KDE"))，這個步驟就並非必要。DejaVu 是一套適用於一般用途的高品質字型，有良好的 [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") 支援：

```
# pacman -S ttf-dejavu

```

請參閱[字型設定](/index.php/Font_configuration "Font configuration")了解如何設定字型渲染，並參閱[字型](/index.php/Fonts_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Fonts (正體中文)")文章內的字型建議與安裝指示。

#### 選擇/安裝圖形介面

X 視窗系統提供了建立圖形使用者介面 (GUI) 的基本架構。

**註記:** 如何選擇桌面環境 (DE) 或視窗管理員 (WM)，是非常主觀的問題。根據**您自己**的需求選擇最好的環境。您也可以建置屬於自己的桌面環境：只需要一套視窗管理員加上自行選用的幾套軟體就夠了。

*   [視窗管理員](/index.php/Window_manager "Window manager") (WM) 會和 X 視窗系統一同控制程式視窗的位置與樣貌。

*   [桌面環境](/index.php/Desktop_environment "Desktop environment") (DE) 在 X 之上工作，與 X 一同提供完整功能的動態 GUI。一般的桌面環境會提供視窗管理員、圖示、小插件、視窗、工具列、資料夾、桌布、程式套組以及拖拉等功能。

除了手動用 `startx` (來自 [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit)) 啟動 X 以外，請參閱[顯示管理員](/index.php/Display_Manager_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Display Manager (正體中文)")了解登入管理員的使用方式，或是從[登入時啟動 X](/index.php/Start_X_at_Login_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Start X at Login (正體中文)") 了解從既存的虛擬終端機啟動的方式。

## 附錄

好奇 Arch 下有什麼吸引人的應用程式嗎？請參考[應用程式清單](/index.php/List_of_applications "List of applications")。

安裝好 Arch 以後，也歡迎參考[一般建議](/index.php/General_Recommendations_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "General Recommendations (正體中文)")內的設定教學，例如設定觸控板、字型算繪等等。