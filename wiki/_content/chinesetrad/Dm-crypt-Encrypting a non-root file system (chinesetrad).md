以下是有關使用 dm-crypt 加密次要檔案系統（就是非 root 分割區）的範例。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 概覽](#概覽)
*   [2 分割區](#分割區)
    *   [2.1 手動掛載與卸載](#手動掛載與卸載)
    *   [2.2 自動解鎖及掛載](#自動解鎖及掛載)
        *   [2.2.1 在開機時](#在開機時)
        *   [2.2.2 在使用者當入時](#在使用者當入時)
*   [3 Loop 裝置](#Loop_裝置)
    *   [3.1 不使用 losetup](#不使用_losetup)
    *   [3.2 使用 losetup](#使用_losetup)
        *   [3.2.1 手動掛載與卸載](#手動掛載與卸載_2)

## 概覽

若只需保護敏感資料的話通常會加密次要檔案系統，而作業系統及程式檔案處於未加密狀態。這可以運用在許多外接媒體，像是隨身碟或隨身硬碟，因此可以安全地在不同電腦之間使用資料。也可以利用加密設定選擇誰擁有哪些分區的存取權限。

因為 dm-crypt 是 [底層區塊級](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") 加密層，它只能加密 [整個分割區](#分割區) 或 [loop 裝置](#Loop_裝置)。如果需要加密個人零散的檔案需要使用檔案系統級的加密層像是 [eCryptfs](/index.php/ECryptfs "ECryptfs") 或 [EncFS](/index.php/EncFS "EncFS")。請參閱 [Disk encryption](/index.php/Disk_encryption "Disk encryption") 取得更多有資訊關於保護隱私資料。

## 分割區

雖然以下使用 `/home` 分割區作為示範，但也適用於其他類似的非 root 分割區。

**提示：** 您可以建立每一個使用者 `/home` 目錄為單一的分割區， 或者建立一個所有使用者共用的 `/home` 目錄。

首先請確定目標分割區是空白的（沒有任何檔案系統）。如果已經建立好檔案系統請先刪除後重新建立一個空白分割區。然後準備安全的覆寫該分割區，請參閱 see [dm-crypt/Drive preparation (正體中文)#安全地覆寫硬碟](/index.php/Dm-crypt/Drive_preparation_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#安全地覆寫硬碟 "Dm-crypt/Drive preparation (正體中文)").

建立將包含加密容器的分割區。

然後使用以下指令建立 LUKS 標頭：

```
# cryptsetup *options* luksFormat *device*

```

使用剛剛所建立的分割區取代 `*device*` 。請參閱 [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") 取得 `*options*` 的詳細內容。

要獲得加密分區的存取權限，請使用裝置映射器解鎖，指令如下：

```
# cryptsetup open *device* *name*

```

解鎖之後，此分割區可以在 `/dev/mapper/*name*` 存取。現在請建立一個您想要的 [檔案系統](/index.php/File_system "File system") ：

```
# mkfs.*fstype* /dev/mapper/*name*

```

掛載檔案系統到 `/home`，或者只想要給單一使用者存取的 `/home/*username*` 目錄，請參閱[#手動掛載與卸載](#手動掛載與卸載).

**提示：** 可以掛載與卸載一次確認裝置映射是正常運作的。

### 手動掛載與卸載

掛載一個分割區：

```
# cryptsetup open *device* *name*
# mount -t *fstype* /dev/mapper/*name* /mnt/home

```

卸載一個分割區：

```
# umount /mnt/home
# cryptsetup close *name*

```

**Tip:** [GVFS](/index.php/GVFS "GVFS") 也可以掛載加密分割區。使用一個支援 gvfs 的檔案管理器（例如 [Thunar](/index.php/Thunar "Thunar")）掛載分割區，密碼提示視窗就會跳出來。對於其他桌面，[zulucrypt](https://aur.archlinux.org/packages/zulucrypt/) 也提供 GUI。

### 自動解鎖及掛載

這裡有三種方式可以自動解鎖分割區後掛載各自的檔案系統。

#### 在開機時

使用 `/etc/crypttab` 設定檔，將在開機時 systemd 的自動解析過程中解鎖。這方法推薦用於當您想要使用單一使用者家目錄分割區時或自動掛載其他已加密的區塊裝置。

請參閱 [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") 及 [Dm-crypt/System configuration#Mounting at boot time](/index.php/Dm-crypt/System_configuration#Mounting_at_boot_time "Dm-crypt/System configuration") 查看設定範例。

#### 在使用者當入時

使用 *pam_exec* 可以在使用者登入之時解鎖 (*cryptsetup open*) 分割區：這推薦用於各使用者擁有自己獨立加密的 `/home` 分割區。請參閱 [dm-crypt/Mounting at login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login")。

使用 [pam_mount](/index.php/Pam_mount "Pam mount") 也可以達成在使用者登入時解鎖的目的。

## Loop 裝置

這裡有兩種方式可以將 loop 裝置作為加密容器，一種直接使用 `losetup` 而另外一種則不使用。

### 不使用 losetup

透過以下指令可以完全避免使用 losetup [[1]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile)：

```
# dd if=/dev/urandom of=key.img bs=20M count=1
# cryptsetup --align-payload=1 luksFormat key.img
```

在執行 `cryptsetup`之前，請先參閱 [Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") 及 [Ciphers and modes of operation](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") f選擇您想使用的加密選項。

開啟裝置與建立 [檔案系統](/index.php/File_system "File system") 的步驟與 [#分割區](#分割區) 相同。

當檔案太小時可能會出現這樣 `Requested offset is beyond real size of device /dev/loop0` 的錯誤，大致上建立 4 MiB 的檔案就會成功了。[[2]](http://archive.is/VOh2p)

如果使用 `dd` 從 `/dev/urandom` 建立大檔案，將會停留在 32 MiB，需要使用 `iflag=fullblock` 選項才可以完整寫入。[[3]](https://unix.stackexchange.com/questions/178949/why-does-dd-from-dev-urandom-stops-early)

手動掛載與卸載的步驟跟 [#手動掛載與卸載](#手動掛載與卸載) 相同。

### 使用 losetup

Loop 裝置可以使用標準的 util-linux 工具 `losetup` 映射到底層區塊裝置檔案上。這個檔案可以擁有自己的檔案系統，可以如同其他檔案系統一樣使用。許多使用者知道 [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") 也是一的建立加密容器的工具。使用以下的範例透過 LUKS 加密 loopback 檔案系統一樣可以做到相同的功能。

首先請使用適當的 [隨機數生產器](/index.php/Random_number_generator "Random number generator") 建立加密容器：

```
# dd if=/dev/urandom of=/bigsecret bs=1M count=10

```

這樣會建立一個名為 `bigsecret`且大小為 10 megabytes 的檔案。

**註記:** 避免未來需要 [resize](/index.php/Dm-crypt/Device_encryption#Loopback_filesystem "Dm-crypt/Device encryption") 容器大小， 確保總大小大於加密大小，以便檔案系統內部需要管理的後設資料還有空間。如果您使用 LUKS 模式，他的標頭資料需要大約 1 至 2 megabytes。

接著建立裝置節點 `/dev/loop0`， 這樣我們就可以掛載使用我的們容器：

```
# losetup /dev/loop0 /bigsecret

```

**註記:** 如果出現 `/dev/loop0: No such file or directory` 這樣的錯誤訊息，您應該先載入 `modprobe loop` 內核模組。最近（Kernel 3.2）loop 裝置是照需求所建立的。使用 `# losetup -f` 請求新的 loop 裝置。

現在開始與 [#分割區](#分割區) 的操作方式相同，除了因為裝置已經隨機化所比不需要再次進行安全覆寫。

**提示：** 使用 *dm-crypt* 的容器可以非常的靈活。看看 [Tomb](/index.php/Tomb "Tomb") 的功能與文件。它提供了 *dm-crypt* 指令搞的包裝，可以快速且靈活的使用。

#### 手動掛載與卸載

卸載容器：

```
# umount /mnt/secret
# cryptsetup close secret
# losetup -d /dev/loop0

```

再次掛載容器：

```
# losetup /dev/loop0 /bigsecret
# cryptsetup open /dev/loop0 secret
# mount -t ext4 /dev/mapper/secret /mnt/secret

```