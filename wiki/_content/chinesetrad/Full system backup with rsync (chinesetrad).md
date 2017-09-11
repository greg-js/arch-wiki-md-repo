Related articles

*   [Backup programs](/index.php/Backup_programs "Backup programs")
*   [rsync](/index.php/Rsync "Rsync")

這篇文章是教你使用 [rsync](/index.php/Rsync "Rsync") 來備份你的 "/" ， 並且排除部份目錄。 這個方法比使用 `dd` 備份磁碟 ([disk cloning](/index.php/Disk_cloning "Disk cloning")) 更好。我們可以使用這個方法備份不同的磁區大小以及不同的檔案系統，而且這個方法也比使用 `cp -a` 來得更好，因為有更好的的檔案權限控管，以及保留檔案屬性還有 Access Control Lists (ACLs). [[1]](http://www.bestbits.at/acl/about.html)

## Contents

*   [1 只要執行一行指令](#.E5.8F.AA.E8.A6.81.E5.9F.B7.E8.A1.8C.E4.B8.80.E8.A1.8C.E6.8C.87.E4.BB.A4)
*   [2 使用 script](#.E4.BD.BF.E7.94.A8_script)
*   [3 修改開機需要的相關檔案](#.E4.BF.AE.E6.94.B9.E9.96.8B.E6.A9.9F.E9.9C.80.E8.A6.81.E7.9A.84.E7.9B.B8.E9.97.9C.E6.AA.94.E6.A1.88)
    *   [3.1 更新 fstab](#.E6.9B.B4.E6.96.B0_fstab)
    *   [3.2 更新 bootloader 的設定檔](#.E6.9B.B4.E6.96.B0_bootloader_.E7.9A.84.E8.A8.AD.E5.AE.9A.E6.AA.94)
*   [4 第一次開機](#.E7.AC.AC.E4.B8.80.E6.AC.A1.E9.96.8B.E6.A9.9F)
*   [5 延伸閱讀](#.E5.BB.B6.E4.BC.B8.E9.96.B1.E8.AE.80)

## 只要執行一行指令

使用 root 權限, 執行:

```
# rsync -aAXv /* /path/to/backup/folder --exclude={/dev/*,/proc/*,/sys/*,/tmp/*,/run/*,/mnt/*,/media/*,/lost+found}

```

如果你想要知道為什麼這些目錄被排除在外，你可以閱讀下一段的資訊。

**Note:** 如果你是重度使用 **hardlinks** 的使用者，你也許會想要使用 `rsync` **`-H`** 這個參數，在 /usr 的目錄中有許多的 hard links 當你使用這個參數後，將可以節省較多的備份空間。

**Note:** 如果你計劃將系統備份到 `/mnt` 或 `/media` 以外的地方，別忘了把他加入 --exclude 的清單中，以免造成無窮迴圈。

**Note:** 你也許會想要使用 rsync **`--delete`** 的參數，如果你需要經常的備份在同一個目錄中的話，這個參數可以幫助你刪除多餘的項目。

## 使用 script

底下的 script 也是提供一樣的備份方法，在備份的同時仍舊會保留 symbolic links, devices, permissions and ownerships, 以及其他的檔案屬性。你可以將你想要除外的部份放在 `--exclude` 的字串裏面。如果你想要瞭解更多，你可以參考 [rsync(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/rsync.1) 和 [date(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/date.1)。

**Note:** 如果你計劃將系統備份到 `/mnt` 或 `/media` 以外的地方，別忘了把他加入 --exclude 的清單中，以免造成無窮迴圈。

**Note:** 你也許會想要使用 rsync **`--delete`** 的參數，如果你需要經常的備份在同一個目錄中的話，這個參數可以幫助你刪除多餘的項目。

```
$ cd ~/Scripts
$ nano backup.sh
```

```
#!/bin/sh

if [ $# -lt 1 ]; then 
    echo "No destination defined. Usage: $0 destination" >&2
    exit 1
elif [ $# -gt 1 ]; then
    echo "Too many arguments. Usage: $0 destination" >&2
    exit 1
elif [ ! -d "$1" ]; then
   echo "Invalid path: $1" >&2
   exit 1
elif [ ! -w "$1" ]; then
   echo "Directory not writable: $1" >&2
   exit 1
fi

case "$1" in
  "/mnt") ;;
  "/mnt/"*) ;;
  "/media") ;;
  "/media/"*) ;;
  *) echo "Destination not allowed." >&2 
     exit 1 
     ;;
esac

START=$(date +%s)
rsync -aAXv /* $1 --exclude={/dev/*,/proc/*,/sys/*,/tmp/*,/run/*,/mnt/*,/media/*,/lost+found,/var/lib/pacman/sync/*}
FINISH=$(date +%s)
echo "total time: $(( ($FINISH-$START) / 60 )) minutes, $(( ($FINISH-$START) % 60 )) seconds" | tee $1/"Backup from $(date '+%A, %d %B %Y, %T')"
```

```
$ chmod +x backup.sh

```

**Note:** `/dev`，`/proc`，`/sys`，`/tmp`，`/run` 這些目錄被除外的原因，是因為這些目錄都會在開機的時候被產生出來，`/lost+found` 則是由 filesystem 來自己產出的。對 Arch Linux 來說，`/var/lib/pacman/sync/*` 是可以被除外的。這可以節省不少備份時間。這裏面的檔案放的都是所有 package 的描述，而我們可以透過`pacman -Syu` 來自動產生出來。而 `/var/log/journal/*` 也可以不用備份，這些都只是 systemd logs。你可能還想要排除 `/home/*/.thumbnails/*`，`/home/*/.mozilla/firefox/*.default/Cache/*` 和 `/home/*/.cache/chromium/*`。

備份是很容易的事。

只要你的系統可以正常運作，打開 terminal 並且使用 root 身份執行這個 script 即可：

```
# /home/user/Scripts/backup.sh /some/destination

```

(將 user 置換成你自己的 username )

你也可以置換 `$1` 成你想要的目的地位址，並使用 root 的身份來執行它：

```
# backup.sh

```

## 修改開機需要的相關檔案

在備份有開機磁區的的檔案系統時，常常會因為設定錯誤而導致系統無法正常開機，如果你因為要將系統備份到另外一個磁區或者磁碟，而且你也需要讓它能夠開機，你可以透過修改 `/etc/fstab` 以及更新你的 bootloader 的設定檔，來解決這個問題。

### 更新 fstab

在重開機之前你必須先修改備份後的系統的 [fstab](/index.php/Fstab "Fstab") 來讓它能夠讀取到變更後的磁區：

 `# nano /path/to/backup/etc/fstab` 
```
tmpfs        /tmp          tmpfs     nodev,nosuid             0   0

/dev/**sda1**    /boot         ext2      defaults                 0   2
/dev/sda5    none          swap      defaults                 0   0
/dev/sda6    /             ext4      defaults                 0   1
/dev/sda7    /home         ext4      defaults                 0   2
```

因為 rsync 將整個磁碟都備份過來，所以所有原本的 `sda` 掛載點，在重開機後會因為找不到開機檔而出錯，所以我們必須將掛載點更改成新的裝置，像是把 /boot 掛載點的 sda 更改成 sdb：

 `# nano /path/to/backup/etc/fstab` 
```
tmpfs        /tmp          tmpfs     nodev,nosuid             0   0

/dev/**sdb1**    /             ext4      defaults                 0   1
```

注意裝置名稱與檔案系統的類別，不要設錯了。

### 更新 bootloader 的設定檔

這一段主要是告訴你如何從你備份的磁區、磁碟開機。

如果你使用的是 [Syslinux](/index.php/Syslinux "Syslinux")，你只需要將原本的開機磁區指定到新的磁區上即可：

**Tip:** 在修改 `syslinux.cfg` 前，你也可以暫時性的修改開機選單，只要你在開機選單出現時按下 `Tab` 鍵，你就可以暫時的修改裏面的資訊，以便測試備份的磁區是否真的可用。

```
# nano /boot/syslinux/syslinux.cfg

```

如果你連開機磁區都想換到新的磁區上，你可以下這個指令：

```
# syslinux-install_update -i -a -m -c /mnt/backup

```

**Note:**

*   -i (安裝檔案)
*   -a (將磁區標記為開機磁區)
*   -m (安裝 MBR boot code)
*   -c (Chroot install (ex: -c /mnt))

如果你使用的是 [GRUB](/index.php/GRUB "GRUB")，建議你使用指令自動產生 `grub.cfg` 設定檔：

```
# pacman -S os-prober
# grub-mkconfig -o /boot/grub/grub.cfg

```

當然你也可以檢查設定檔是否正確，檔案在 `/boot/grub/grub.cfg`。確認 UUID 是否是新的磁區，不然他仍舊會使用舊的磁區來開機。

## 第一次開機

重開你的電腦，並且在 bootloader 選單中選擇正確的項目，於是將會第一次載入你的系統。系統將會重新檢查你的你的 `/` 並且產出其他相對應的檔案。

現在你可以重新編輯 `/etc/fstab` 來去增加之前被你移除掉的磁區和掛載點。

如果你將資料從 HDD 轉換到 SSD (固態硬碟)，別忘了啟動 TRIM。也別忘了使用 HDD 和 tmpfs 掛載點來降低 SSD 損害。- 可參考 [Relocate files to tmpfs](/index.php/Improving_performance#Relocate_files_to_tmpfs "Improving performance") 與 [Tips for Minimizing SSD Read & Writes](/index.php/Solid_State_Drives#Tips_for_minimizing_disk_reads.2Fwrites "Solid State Drives").

**Note:** 你可能需要再次重開機來讓服務可以被正常的運作。 如果你的 pulseaudio沒有辦法被正常的載入。 可以嘗試 restart dbus.service 來讓它正常。

## 延伸閱讀

1.  [Howto – local and remote snapshot backup using rsync with hard links](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) Includes file deduplication with hard-links, MD5 integrity signature, 'chattr' protection, filter rules, disk quota, retention policy with exponential distribution (backups rotation while saving more recent backups than older)