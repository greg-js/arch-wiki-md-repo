Related articles

*   [Disk encryption#Preparing the disk](/index.php/Disk_encryption#Preparing_the_disk "Disk encryption")
*   [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk")

在加密您的裝置之前，這裡非常推薦使用隨機亂數去覆寫整個裝置以確保安全。為了避免加密攻擊或非預期的 [檔案救援](/index.php/File_recovery "File recovery")，這些資料應該要與 dm-crypt 所寫入的資料無法區分。更多完整的討論，請參閱 [Disk encryption#Preparing the disk](/index.php/Disk_encryption#Preparing_the_disk "Disk encryption")。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安全地覆寫硬碟](#安全地覆寫硬碟)
    *   [1.1 通用方法](#通用方法)
    *   [1.2 dm-crypt 的專用方法](#dm-crypt_的專用方法)
        *   [1.2.1 dm-crypt 覆寫一個空硬碟或空分割區](#dm-crypt_覆寫一個空硬碟或空分割區)
        *   [1.2.2 dm-crypt 在安裝後覆寫未使用空間](#dm-crypt_在安裝後覆寫未使用空間)
        *   [1.2.3 覆寫 LUKS 標頭](#覆寫_LUKS_標頭)
*   [2 分割磁區](#分割磁區)
    *   [2.1 物理分割區](#物理分割區)
    *   [2.2 堆疊的區塊裝置](#堆疊的區塊裝置)
    *   [2.3 Btrfs 子捲軸](#Btrfs_子捲軸)
    *   [2.4 開機磁區 （GRUB）](#開機磁區_（GRUB）)

## 安全地覆寫硬碟

在決定使用哪種方式覆寫硬碟之前，請記住只要任何一顆硬碟做為加密裝置之後，就不需要再執行這項操作。

**警告:** 開始之前請先妥善地備份任何有價值的重要資料！

**註記:** 當開始覆寫大量資料時，可能需要數小時至數天才可以完成。

**提示：**

*   覆寫過程中可能需要超過一天時間才能完成數 TB 大小的硬碟。為了在過程中依舊能使用電腦，您應該使用已安裝好的系統進行這項作業而不是使用 Live Arch 安裝系統。
*   對於 [Solid state drive (正體中文)](/index.php/SSD "SSD")，在做以下動作之前為了防止 [快閃記憶體](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk") 因快取的關係而無法完整覆寫資料，您應該執行 [SSD 的記憶單元清除](/index.php/Solid_state_drive/Memory_cell_clearing "Solid state drive/Memory cell clearing")。

### 通用方法

詳細的操作方式請參閱 [安全地清除硬碟](/index.php/Securely_wipe_disk "Securely wipe disk")。

### dm-crypt 的專用方法

以下兩種方式特別針對 dm-crypt 因為它們非常快速也可以在設定分割區後才執行。

在 [cryptsetup FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup) （2.19項 "*How can I wipe a device with crypto-grade randomness?*"） 中提到可以在既存的 dm-crypt 分割區 中使用偽造的亂數產生器對底層區塊裝置的未使用空間進行覆寫。它還宣稱可以保護防止洩漏使用方式。這是因為加密後的資料實際上與亂數資料無法分辨。

#### dm-crypt 覆寫一個空硬碟或空分割區

首先，在一個分割區上建立一個暫時的加密容器（`sdXY`）或完整的裝置（`sdX`）來加密：

```
# cryptsetup open --type plain -d /dev/urandom /dev/<block-device> to_be_wiped

```

您可以驗證它是否已經建立完成：

 `# lsblk` 
```
NAME          MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda             8:0    0  1.8T  0 disk
└─to_be_wiped 252:0    0  1.8T  0 crypt

```

使用 `0` 覆寫容器。因為上面開啟加密容器時使用 `-d /dev/urandom` 指定隨機數為解密金鑰，所以這裡不需要使用 `if=/dev/urandom`。

 `# dd if=/dev/zero of=/dev/mapper/to_be_wiped status=progress`  `1847386624 bytes (1.8 GB, 1.7 GiB) copied, 754 s, 2.4 MB/s` 
**提示：**

*   使用 *dd* 配合 `bs=` 選項，像是 `bs=1M`，可以增加硬碟在操作時的吞吐量。
*   確定分割區是否都已經在建立覆寫容器後被寫 0。在覆寫指令之後 `blockdev --getsize64 */dev/mapper/container*` 可以以 root 身份取得精確的容器大小。現在可以使用 *od* 指令來確定是否所有扇區都已經被寫 0，例如 `od -j *containersize - blocksize*` 可以查看覆寫完成後到結束位置。

最後，關閉暫時的加密容器：

```
# cryptsetup close to_be_wiped

```

當想要加密整個系統時，下一步請參閱 [#分割磁區](#分割磁區)。如果只是想加密單一分割區，請參閱 [加密非root檔案系統](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#分割區 "Dm-crypt/Encrypting a non-root file system (正體中文)")。

#### dm-crypt 在安裝後覆寫未使用空間

某些用戶沒有時間在 [安裝](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") 前執行覆寫，在加密系統開啟完成及掛載檔案系統後，可以達成類似的效果。請記得考慮有關於檔案系統是否有設定保留空間，像是給 root 帳號或其他 [磁碟配額](/index.php/Disk_quota "Disk quota") 等機制，即使使用 root 帳號也有可能被限制覆寫：有些部份的底層區塊裝置可能無法完全被寫入。

執行覆寫的方式，透過在加密容器中寫入一個檔案，這樣就會填滿剩餘的空間：

 `# dd if=/dev/zero of=/file/in/container status=progress`  `dd: writing to ‘/file/in/container’: No space left on device` 

同步硬碟快取後刪除剛剛所產生的檔案來釋放空間。

```
# sync
# rm /file/in/container

```

以上的操作必須執行於每個區塊裝置上分割區的檔案系統都執行過一遍。例如在 [LUKS 上的 LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system")，則必須在所有邏輯捲軸（LV）上都執行過。

#### 覆寫 LUKS 標頭

被 dm-crypt/LUKS 格式化的分割區標頭會含有密碼及加密選項， 當開啟區塊裝置時被稱為 `dm-mod`。在標頭之後才是實際的亂數資料分割區的開始。然而在重新安裝或停止使用（像是更換裝置或是販售電腦）已經亂數化的裝置，它 *可能* 只需要清除分割區的標頭，而不用執行又臭又長的覆寫過程。

清除 LUKS 標頭時將會刪除基於 PBKDF2 加密(AES)的主金鑰、鹽或其他東西。

**註記:** 寫入 LUKS 分割區 (本例中為 `/dev/sdX**1**`) 而不是直接指向磁碟裝置節點是很重要的關鍵。將加密設定在其他裝置映射層（device-mapper layer）之上，例如先設定好 RAID 後設定 LUKS 之後建立 LVM，應該分別地被寫入 RAID。

一個預設標頭只具有 256 bit 大小的單一金鑰槽應該為 1024KiB 的大小。也建議同時覆蓋由 dm-crypt 所寫入最前端前的 4Kib 資料，所以有 1028Kib 需要被覆蓋。總共是 `1052672` Byte。

沒有任何偏移的情況：

```
# head -c 1052672 /dev/urandom > */dev/sdX1*; sync

```

對於 512 bit 金鑰長度（例如 aes-xts-plain 的 512 bit 金鑰） 它的標頭長度是 2MiB。LUKS2 標頭是 4MiB。

如果有任何疑慮，大概覆蓋 10MiB 左右的大小也可以。

```
# dd if=/dev/urandom of=*/dev/sdX1* bs=512 count=20480

```

**註記:** 備份標頭檔案可以取得救援機會，但因為第一個加密的扇區被覆蓋了，可能會導致檔案系統毀損。請參閱其他的方有關如何備份關鍵的標頭區塊。

當使用隨機亂數覆寫標頭後，就只會剩下被加密的資料。一個例外是在 SSD 上，因為 SSD 會使用快取進行操作。理論上在一定時間內原始標頭還是會被快取起來，因此覆寫標頭後還是有可能可以使用。為了強烈的安全起見，還是建議 SSD 進行安全的資料覆寫（步驟請參考 cryptsetup 的 [FAQ 5.19](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)）。

## 分割磁區

本節只適用於加密整個系統。當裝置在安全的覆寫過後，接著要準確的選擇您的分割區方案，考量 dm-crypt 的需求及最終對管理系統的影響。

這裡開始請注意，[大部分](#開機磁區_（GRUB）) 的方法都需要有一個獨立的未加密 `/boot` 分割區，因為開機載入程式需要存取 `/boot` 目錄內的 initramfs 及加密模組才能完成開機（請參閱 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")）。如果因此有安全上的疑慮，請參閱 [dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties")。

另一個考量的重要因素是如何處理置換區域及系統暫停時如何處理，請參閱 [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption")。

### 物理分割區

最簡單的情況下加密可以直接作用於物理分割區上，如何建立分割區及方法請參閱 [Partitioning](/index.php/Partitioning "Partitioning")。就像其他未加密系統一樣，只需要 root 分割區即可，但就上述所說請避開 `/boot` 分區。這個方法可以自由決定哪些分割區要加密哪些不要，無論多少硬碟或分割區方法都一樣。當然也可以隨意增加或刪除分割區，但是變更分割區大小會受到硬碟大小本身的限制。最後請注意，打開每個加密分區都需要獨立的密語或金鑰，可以使用 `crypttab` 在開機過程中自動處理這些事情，請參閱 [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration")。

### 堆疊的區塊裝置

如果需要更大的靈活性，dm-crypt 可以與其他區塊裝置像是 [LVM](/index.php/LVM "LVM") 和 [RAID](/index.php/RAID "RAID") 共存。加密容器可以位於堆疊區塊裝置之上或之下：

*   如果 LVM/RAID 裝置建立在加密層之上（先加密再 LVM）， 則可以自由地增加刪除或變更檔案系統大小，但必須基於相同的加密分割區，然後這些則只需要一組密語或金鑰。但是因為加密是建立在物理分區之上，所以沒有辦法使用 LVM 或 RAID 的跨磁碟能力。
*   如果加密層是建立在 LVM/RAID 裝置之上（先 LVM 再加密），依然可以重新變更檔案系統的組成，但是會稍微複雜，必須要適當的調整各個加密層。此外，每一個加密層都需要獨立的密語或金鑰才能打開。但這是跨多硬碟的加密系統唯一一個的方法。

### Btrfs 子捲軸

[Btrfs](/index.php/Btrfs "Btrfs") 內的 [子捲軸](/index.php/Btrfs#Subvolumes "Btrfs") 可以與 dm-crypt 一起使用，如果不需要其他檔案系統則可以完全取代 LVM。但是請注意在 Linux 5.0 之前 Btrfs [不支援](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F) 置換檔案，所以如果您需要 [置換空間](/index.php/Swap "Swap") 且 Linux < 5.0 （像是[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)），則您就需要 [加密的置換空間](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption")。請參閱 [Dm-crypt/Encrypting an entire system#Btrfs subvolumes with swap](/index.php/Dm-crypt/Encrypting_an_entire_system#Btrfs_subvolumes_with_swap "Dm-crypt/Encrypting an entire system")。

### 開機磁區 （GRUB）

請參閱 [dm-crypt/Encrypting an entire system#Encrypted boot partition (GRUB)](/index.php/Dm-crypt/Encrypting_an_entire_system#Encrypted_boot_partition_(GRUB) "Dm-crypt/Encrypting an entire system")。