相關文章

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [Removing System Encryption](/index.php/Removing_System_Encryption "Removing System Encryption")

## Contents

*   [1 常見方法](#.E5.B8.B8.E8.A6.8B.E6.96.B9.E6.B3.95)
*   [2 裝置的準備](#.E8.A3.9D.E7.BD.AE.E7.9A.84.E6.BA.96.E5.82.99)
*   [3 加密裝置](#.E5.8A.A0.E5.AF.86.E8.A3.9D.E7.BD.AE)
*   [4 系統配置](#.E7.B3.BB.E7.B5.B1.E9.85.8D.E7.BD.AE)
*   [5 置換裝置的加密](#.E7.BD.AE.E6.8F.9B.E8.A3.9D.E7.BD.AE.E7.9A.84.E5.8A.A0.E5.AF.86)
*   [6 特色](#.E7.89.B9.E8.89.B2)
*   [7 另外參見](#.E5.8F.A6.E5.A4.96.E5.8F.83.E8.A6.8B)

## 常見方法

這部分主要介紹使用 *dm-crypt* 對系統或某個掛載點進行加密。即您必須熟系在不同狀況下需要使用不同的加密方法。這裡有些跨連結的子頁面可以參考。

如果您想要加密的是非根目錄，像是[分割區](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system")或是[Loop 裝置](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system")，請參閱[Dm-crypt/加密非root檔案系統](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system")。

如果您想要加密的是整個系統，特別是跟目錄，請參閱[Dm-crypt/加密整個系統](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system")。許多方法可以適用，包含利用 *dm-crypt* 配合 *LUKS* 擴充功能，*plan* 模式加密及*LVM*。

## 裝置的準備

[Dm-crypt/裝置的準備](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") 詳細說明許多操作，像是 [安全地抹除裝置資料](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation") 和 在使用 *dm-crypt* 操作分割區的具體要點。

## 加密裝置

[Dm-crypt/裝置加密](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption") 將會引導你如何使用 dm-crypt 內提供的 [cryptsetup](/index.php/Dm-crypt/Device_encryption#Cryptsetup_usage "Dm-crypt/Device encryption") 對系統進行加密。它包含了 [dm-crypt 加密選項](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption") 的範例、處理 [金鑰檔](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") 的建立、使用 LUKS 進行 [金鑰管理](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption") 以及 [備份與還原](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption")。

## 系統配置

[Dm-crypt/系統配置](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") 說明當加密系統時應該如何去配置 [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration")、the [boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") 以及 [crypttab](/index.php/Crypttab "Crypttab") 檔。

## 置換裝置的加密

[Dm-crypt/置換空間加密](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") 說明如果加入一個置換空間到已加密的系統中。置換空間分區同時也必須被加密，保護任何被系統放進置換空間的資料。這部分詳細說明 [不支援](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#Without_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") 以及 [支援](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#With_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") 休眠（suspend-to-disk）功能。

## 特色

[Dm-crypt/特色](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") 說明一些特殊操作，像是 [確保開機引導分區未被加密](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties")、[使用 GPG 或 OpenSSL 加密金鑰檔](/index.php/Dm-crypt/Specialties#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties")、一個 [透過網路開機及解密](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties") 的方法、[設定SSD的 discard/TRIM 參數](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") 以及處理 [加密勾子（hook）及多硬碟](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties")。

## 另外參見

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - 專案首頁。
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - LUKS 首頁及[FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - 主要及重要說明文件。
*   [cryptsetup repository](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) 及 [release](https://www.kernel.org/pub/linux/utils/cryptsetup/) 封存。
*   [DOXBOX](https://github.com/t-d-k/doxbox) - 支援在 Microsoft Windows 下解密 LUKS 加密分割區。