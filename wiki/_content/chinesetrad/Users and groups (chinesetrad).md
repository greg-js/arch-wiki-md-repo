相關文章

*   [開發者 Wiki:UID / GID 資料庫 (英)](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database")
*   [polkit (英)](/index.php/Polkit "Polkit")
*   [chmod (英)](/index.php/Chmod "Chmod")
*   [更改使用者名稱 (英)](/index.php/Change_username "Change username")

**翻譯狀態：** 本文章是 [Users_and_Groups](/index.php/Users_and_Groups "Users and Groups") 的翻譯版本。最近一次的翻譯時間：2014-01-23。點擊[本連結](https://wiki.archlinux.org/index.php?title=Users_and_Groups&diff=0&oldid=290182)查看英文頁面之後的變更。

GNU/Linux 利用使用者和群組的概念來[控制存取](https://en.wikipedia.org/wiki/access_control#Computer_security "wikipedia:access control") — 也就是控制系統的檔案、目錄、周邊設備的存取權。Linux 預設對存取權限的控制相當簡易。更多進階的存取控制請參閱 [ACL](/index.php/ACL "ACL") 和 [LDAP 驗證](/index.php/LDAP_authentication "LDAP authentication")。

## Contents

*   [1 概要](#.E6.A6.82.E8.A6.81)
*   [2 權限與擁有權](#.E6.AC.8A.E9.99.90.E8.88.87.E6.93.81.E6.9C.89.E6.AC.8A)
*   [3 檔案清單](#.E6.AA.94.E6.A1.88.E6.B8.85.E5.96.AE)
*   [4 使用者管理](#.E4.BD.BF.E7.94.A8.E8.80.85.E7.AE.A1.E7.90.86)
    *   [4.1 使用者資料庫](#.E4.BD.BF.E7.94.A8.E8.80.85.E8.B3.87.E6.96.99.E5.BA.AB)
*   [5 群組管理](#.E7.BE.A4.E7.B5.84.E7.AE.A1.E7.90.86)
*   [6 群組清單](#.E7.BE.A4.E7.B5.84.E6.B8.85.E5.96.AE)
    *   [6.1 使用者群組](#.E4.BD.BF.E7.94.A8.E8.80.85.E7.BE.A4.E7.B5.84)
    *   [6.2 系統群組](#.E7.B3.BB.E7.B5.B1.E7.BE.A4.E7.B5.84)
    *   [6.3 軟體群組](#.E8.BB.9F.E9.AB.94.E7.BE.A4.E7.B5.84)
    *   [6.4 不建議或已不使用的群組](#.E4.B8.8D.E5.BB.BA.E8.AD.B0.E6.88.96.E5.B7.B2.E4.B8.8D.E4.BD.BF.E7.94.A8.E7.9A.84.E7.BE.A4.E7.B5.84)

## 概要

任何使用電腦的人都可以算是「使用者」。在這裡，我們描述的是代表每個使用者的「名稱」。有些人會採用真名，如 Mary 或 Bill，也有人使用 Dragonlady 或 Pirate 這些和真名無關的名稱。電腦在乎的只有每個用來建立帳號的名稱，這些使用者必須使用自己設定的名稱獲得存取權，才能使用電腦。某些系統服務也會利用一些受限制或帶權限的使用者帳號來執行。

管理使用者的目的，在於以特定方式限制存取以保障安全。超級使用者 (root) 可以完全存取作業系統與設定資料；該帳號規劃只作管理用途。未充分授權的使用者可以使用 [su](/index.php/Su "Su") 和 [sudo](/index.php/Sudo "Sudo") 程式讓權限能有限度的提升。

每個人都可以有兩個以上的帳號，每個帳號都使用不同的名稱。另外，有些名稱有其特殊用途，不能隨意拿來取名，比如說 "root"。

多個使用者可以組成一個「群組」，使用者可以選擇加入一個既存群組，以獲取該群組的特有存取權。

**註記:** 新手應該謹慎使用這些工具，不要動到任何與他們自己帳號無關的「既存」帳號。

## 權限與擁有權

摘錄自 [In UNIX Everything is a File](http://ph7spot.com/musings/in-unix-everything-is-a-file)：

	*The UNIX operating system crystallizes a couple of unifying ideas and concepts that shaped its design, user interface, culture and evolution. One of the most important of these is probably the mantra: "everything is a file," widely regarded as one of the defining points of UNIX.*

	*This key design principle consists of providing a unified paradigm for accessing a wide range of input/output resources: documents, directories, hard-drives, CD-ROMs, modems, keyboards, printers, monitors, terminals and even some inter-process and network communications. The trick is to provide a common abstraction for all of these resources, each of which the UNIX fathers called a "file." Since every "file" is exposed through the same API, you can use the same set of basic commands to read/write to a disk, keyboard, document or network device.*

摘錄自 [Extending UNIX File Abstraction for General-Purpose Networking](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf)：

	*A fundamental and very powerful, consistent abstraction provided in UNIX and compatible operating systems is the file abstraction. Many OS services and device interfaces are implemented to provide a file or file system metaphor to applications. This enables new uses for, and greatly increases the power of, existing applications — simple tools designed with specific uses in mind can, with UNIX file abstractions, be used in novel ways. A simple tool, such as cat, designed to read one or more files and output the contents to standard output, can be used to read from I/O devices through special device files, typically found under the `/dev` directory. On many systems, audio recording and playback can be done simply with the commands, "`cat /dev/audio > myfile`" and "`cat myfile > /dev/audio`," respectively.*

在 GNU/Linux 系統下，所有檔案都歸屬於一位使用者和一個群組。另外還有三種存取權限：讀取、寫入與執行。檔案的擁有者、檔案的所屬群組和其他人 (無擁有權) 分別套用不同的存取權限。透過 `ls -l` 指令可以看出誰擁有這個檔案，權限又怎麼設定：

 `$ ls -l /boot/` 
```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux
```

第一行顯示檔案的權限 (以 `vmlinuz-linux` 為例，其權限設定為 `-rw-r--r--`)。第三行與第四行分別顯示檔案的擁有者和所屬群組。上面範例中，所有檔案都屬於 *root* 使用者，以及 *root* 群組。

 `$ ls -l /media/` 
```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared
```

在這個範例，`sf_Shared` 目錄屬於 *root* 使用者以及 *vboxsf* 群組。使用 stat 指令可以得知檔案的擁有者和權限：

擁有者：

 `$ stat -c %U /media/sf_Shared/`  `root` 

所屬群組：

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

存取權限：

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

存取權限以三組子字串表示，分別代表擁有者、所屬群組、其他人對該檔案的權限。舉例來說，`-rw-r--r--` 代表檔案擁有者對該檔案可以讀取、寫入，但無法執行 (`rw-`)，至於隸屬於該檔案所屬群組的使用者，以及其他使用者，只能對檔案作讀取 (`r--` 和 `r--`)。另一個範例中，`drwxrwx---` 代表檔案擁有者，以及隸屬於檔案所屬群組的使用者，都可以對該檔案讀取、寫入並執行 (`rwx` 和 `rwx`)，其他使用者則沒有任何可用權限 (`---`)。第一個字元代表檔案類型。

用 `find` 指令列出某個使用者/群組擁有什麼檔案：

```
# find / -group [group]

```

```
# find / -user [user]

```

檔案的擁有者和所屬群組可以透過 `chown` (change owner；更改擁有者) 指令更改。檔案的存取權限可以透過 `chmod` (change mode；更改模式) 指令更改。

一些額外的詳細資訊請參閱 [chown(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1)，[chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1)，以及 [Linux 檔案權限](http://www.tuxfiles.org/linuxhelp/filepermissions.html)。

## 檔案清單

**警告:** 不要手動編輯這些檔案。使用指定工具可以正確處理鎖定問題，並避開任何使資料庫格式無效的風險。請參閱[#使用者管理](#.E4.BD.BF.E7.94.A8.E8.80.85.E7.AE.A1.E7.90.86)與[#群組管理](#.E7.BE.A4.E7.B5.84.E7.AE.A1.E7.90.86)瞭解個大概。

| 檔案 | 目的 |
| `/etc/shadow` | 保全的使用者帳號資訊 |
| `/etc/passwd` | 使用者帳號資訊 |
| `/etc/gshadow` | 包含群組帳號的影子資訊 |
| `/etc/group` | 定義使用者所屬群組為何 |
| `/etc/sudoers` | 允許執行 sudo 的名單 |
| `/home/*` | 家目錄 |

## 使用者管理

`who` 指令可以用來列出所有登入系統的使用者。

使用 `useradd` 指令新增使用者：

```
# useradd -m -g [起始群組] -G [額外群組] -s [登入用 Shell] [使用者名稱]

```

*   **`-m`** 建立使用者的家目錄為 `/home/[使用者名稱]`；一個非 root 的使用者在家目錄內可以寫入、刪除檔案並安裝程式。
*   **`-g`** 定義使用者起始登入群組的群組名稱或編號；群組名稱必須存在；若提供群組編號，其指定的群組必須是一個已存在的群組；若未指定此項，useradd 將參考 `/etc/login.defs` 內所包含的 `USERGROUPS_ENAB` 變數。
*   **`-G`** 引進一個輔助群組清單，讓使用者同時成為這些群組的成員；每個群組以逗號分隔，不包含任何空格；預設情況下，使用者只會隸屬於其起始群組。
*   **`-s`** 定義使用者預設登入用 Shell 的路徑與檔名；當開機程序結束後，預設登入用 Shell 就變成所指定的 Shell；若選擇 Bash 以外的 Shell，請確認已經安裝所選 Shell 的軟體包。

**警告:** 登入 shell 應為 `/etc/shells` 有列出的 shell。使用 PAM 的程式會藉由 `pam_shells` 模組檢查。

一個典型桌面系統下的範例：新增 *archie* 這個使用者，並指定登入用 Shell 為 bash：

```
# useradd -m -g users -G wheel -s /bin/bash archie

```

之後若要將使用者加入其它群組，使用

```
# usermod -aG [額外群組] [使用者名稱]

```

或是使用 gpasswd。使用者一次只能加入 (或移出) 一個群組。

```
# gpasswd --add [username] [group]

```

**警告:** 若從上面的 `usermod` 指令拿掉 `-a` 選項，該使用者將會被踢出所有未列於 `[額外群組]` 的群組 (也就是說，使用者將只有 `[額外群組]` 所列舉群組的成員身分)。

若要在 *GECOS* 欄位 (例如，使用者的全名) 輸入使用者資訊：

```
# chfn [使用者名稱]

```

(此方式下 `chfn` 將以互動模式執行)。

指定使用者的密碼：

```
# passwd [username]

```

標示使用者密碼已經過期，要求他們在第一次登入時建立新密碼：

```
# chage -d 0 [username]

```

使用者帳號可以使用 `userdel` 指令刪除。

```
# userdel -r [username]

```

`-r` 選項代表同時刪除該使用者的家目錄與郵件佇列。

### 使用者資料庫

本機的使用者資訊會儲存在 `/etc/passwd` 檔案。列出系統上所有使用者帳號：

```
$ cat /etc/passwd

```

一行會列出一個帳號，格式如下：

```
account:password:UID:GID:GECOS:directory:shell

```

欄位意義：

*   `account` 為使用者的名稱
*   `password` 為使用者的密碼
*   `UID` 為使用者的數字 ID
*   `GID` 為使用者主群組的數字 ID
*   `GECOS` 為選填欄位，使用者的個人資料；通常包含使用者的全名
*   `directory` 為使用者的 `$HOME` 目錄
*   `shell` 為使用者的指令直譯程式 (預設為 `/bin/sh`)

**註記:** Arch Linux 使用**影子**密碼。由於 `passwd` 檔案可以無限制地讀取，在該檔案儲存密碼 (雜湊值或其它方式) 非常不安全。`password` 欄位內只包含一個佔位字元 (`x`)，代表密碼的雜湊值已儲存於存取受限的檔案 `/etc/shadow`。

## 群組管理

`/etc/group` 這個檔案定義了系統內的群組 (詳情列於 [group(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/group.5))。

以 `groups` 指令顯示使用者所屬群組：

```
$ groups [使用者]

```

若忽略`[使用者]`，將顯示目前使用者加入的群組名稱。

`id` 指令提供更多的詳細資料，像是使用者的 UID 與關聯 GID：

```
$ id [使用者]

```

列出系統上所有群組：

```
$ cat /etc/group

```

用 `groupadd` 指令建立新群組：

```
# groupadd [群組]

```

用 `gpasswd` 指令將使用者加入群組：

```
# gpasswd -a [使用者] [群組]

```

刪除群組：

```
# groupdel [群組]

```

將使用者自群組中移除：

```
# gpasswd -d [使用者] [群組]

```

若使用者目前已登入，他/她必須登出後再行登入，變動才會生效。

## 群組清單

### 使用者群組

**註記:**

*   只要 *logind* 階段沒有損毀，正常的桌面權限如音效、3D、列印、掛載等都能直接獲得，不必加入這些群組。(若要檢查，詳見[一般疑難排解#階段權限](/index.php/General_troubleshooting#Session_permissions "General troubleshooting"))。

工作站/桌面使用者通常會將他們的非 root 使用者帳號加入以下某些群組，對周邊設備與其它硬體的存取才會被允許，以便進行系統管理：

| 群組 | 影響檔案 | 目的 |
| camera | 存取[數位相機](/index.php/Digital_Cameras "Digital Cameras")。 |
| floppy | `/dev/fd[0-9]` | 存取軟碟機。 |
| games | `/var/games` | 存取某些遊戲軟體。 |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | 使用 [updatedb](https://en.wikipedia.org/wiki/updatedb "wikipedia:updatedb") 指令的權利。 |
| networkmanager | 您的使用者帳號需要這個，才能以 [NetworkManager](/index.php/NetworkManager "NetworkManager") 連上無線網路。這個群組預設不包含進 Arch，必須手動加入。 |
| rfkill | `/dev/rfkill` | 控制無線裝置電力狀態的權利 (rfkill 使用)。 |
| users | 一般使用者群組。 |
| uucp | `/dev/ttyS[0-9]`, `/dev/tts/[0-9]` | 序列與 USB 裝置，如數據機、手持設備、RS-232/序列埠。 |
| wheel | 管理性群組，通常用來給予 [sudo](/index.php/Sudo "Sudo") 與 [su](/index.php/Su "Su") 指令的存取 (預設皆不使用，可在 `/etc/pam.d/su` 和 `/etc/pam.d/su-l` 設置)。 |

### 系統群組

以下群組作為系統用途，不太被一般 Arch 使用者所使用：

**註記:**

*   在 Arch 移轉到 systemd 之前，某些群組是必須的。現在就不需要了。請參閱 [Systemd 的「補充資料」一節](/index.php/Systemd#Supplementary_information "Systemd")。

| 群組 | 影響檔案 | 目的 |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | 在所有階段對音效硬體的直接存取 ([ALSA](/index.php/ALSA "ALSA") 和 [OSS](/index.php/OSS "OSS") 皆提出要求)。本機階段已經有能力播放音效、存取混音器控制。 |
| avahi |
| bin | 無 | 歷史的遺骸 |
| clamav | `/var/lib/clamav/*`, `/var/log/clamav/*` | [Clam AntiVirus](/index.php/Clam_AntiVirus "Clam AntiVirus") 使用。 |
| daemon |
| dbus | `/var/run/dbus/*` |
| disk | `/dev/sda[1-9]`, `/dev/sdb[1-9]` | 存取區塊裝置，不受 `optical`、`floppy` 與 `storage` 等群組的影響。 |
| ftp | `/srv/ftp` | [FTP](https://en.wikipedia.org/wiki/FTP "wikipedia:FTP") 伺服器使用，如 [Proftpd](/index.php/Proftpd "Proftpd") |
| fuse | fuse 使用，允許使用者掛載。 |
| gdm | X 伺服器認證目錄 (ServAuthDir) | [GDM](/index.php/GDM "GDM") 群組。 |
| http |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| log | `/var/log/*` | 存取 `/var/log` 下的日誌檔。 |
| lp | `/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups` | 存取印表機硬體；讓使用者能夠管理列印工作。 |
| mail | `/usr/bin/mail` |
| mem |
| mpd | `/var/lib/mpd/*`, `/var/log/mpd/*`, `/var/run/mpd/*`，另外再加上音樂目錄 | [MPD](/index.php/MPD "MPD") 群組。 |
| network | 改變網路設定值的權利；像是使用 [NetworkManager](/index.php/NetworkManager "NetworkManager")。 |
| nobody | 沒有權限的群組。 |
| ntp | `/var/lib/ntp/*` | [NTPd](/index.php/NTPd "NTPd") 群組。 |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | 存取光學裝置，如 CD/DVD 光碟機。 |
| policykit | [PolicyKit](/index.php/PolicyKit "PolicyKit") 群組。 |
| power | 使用 [Pm-utils](/index.php/Pm-utils "Pm-utils") (暫停、休眠...) 與電力管理控制的權利。 |
| root | `/*` | 完整的系統管理與控制權 (root, admin)。 |
| scanner | `/var/lock/sane` | 存取掃描器硬體。 |
| smmsp | [sendmail](https://en.wikipedia.org/wiki/sendmail "wikipedia:sendmail") 群組。 |
| storage | 存取可移除裝置，如 USB 外接硬碟、快速插拔裝置、MP3 播放器；讓使用者能夠掛載儲存裝置。 |
| sys | 管理 [CUPS](/index.php/CUPS "CUPS") 內印表機的權利。 |
| systemd-journal | `/var/log/journal/*` | 提供完整的 systemd 日誌存取。否則只顯示使用者產生的訊息。 |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` | 例：存取 `/dev/ACMx` |
| vboxsf | 虛擬機器共享資料夾 | [VirtualBox](/index.php/VirtualBox "VirtualBox") 使用。 |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | 存取影像擷取裝置、2D/3D 硬體加速、幀緩衝 (使用 [X](/index.php/Xorg "Xorg") **不需要**加入本群組)。本機階段已經有能力使用硬體加速與影像擷取。 |

### 軟體群組

以下群組允許其成員使用特定軟體：

| 群組 | 影響檔案 | 目的 |
| adbusers | `/dev/` 下的裝置節點 | 存取「[Android](/index.php/Android "Android") 除錯橋接器」(Android Debugging Bridge) 的權利。 |
| cdemu | `/dev/vhba_ctl` | 使用 [CDemu](/index.php/CDemu "CDemu") 驅動模擬的權利。 |
| thinkpad | `/dev/misc/nvram` | ThinkPad 使用者用來存取諸如 [tpb](/index.php/Tpb "Tpb") 等工具。 |
| vboxusers | `/dev/vboxdrv` | 使用 VirtualBox 軟體的權利。 |
| vmware | 使用 [VMware](/index.php/VMware "VMware") 軟體的權利。 |
| ssh | 設定 [Sshd](/index.php/Sshd "Sshd")，只允許該群組的成員登入。 |
| wireshark | 用 [Wireshark](/index.php/Wireshark "Wireshark") 抓取封包的權利。 |

### 不建議或已不使用的群組

以下群組目前不被任何人使用：

| 群組 | 目的 |
| stb-admin | **已不再使用！**存取 [system-tools-backends](http://system-tools-backends.freedesktop.org/) 的權利 |
| kvm | 以前要讓非 root 的使用者存取使用 [KVM](/index.php/KVM "KVM") 的虛擬機器，需要將使用者新增到 `kvm` 群組。現在會自動使用 [udev](/index.php/Udev "Udev") 規則，因此該群組已不建議使用。 |