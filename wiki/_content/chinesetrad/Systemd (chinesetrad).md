Related articles

*   [Systemd FAQ](/index.php/Systemd_FAQ "Systemd FAQ")
*   [Init to systemd cheatsheet](/index.php/Init_to_systemd_cheatsheet "Init to systemd cheatsheet")
*   [udev](/index.php/Udev "Udev")

節錄自 [systemd 專案網頁](http://freedesktop.org/wiki/Software/systemd):

**systemd** 是一個Linux的系統與服務管理器, 並且相容於 SysV 與 LSB init scripts. systemd 提供並行化任務的能力, 使用 socket 與 [D-Bus](/index.php/D-Bus "D-Bus") 來啟動服務, 按照需要啟動服務(daemons), 使用 Linux [control groups](/index.php/Cgroups "Cgroups") 來追蹤程序, 支援系統快照與回復系統狀態, 維護掛載與自動掛載點. 並由精密的控制來管理各個服務. 它亦可以完美的取代 sysvinit。目前Arch已經採用[Systemd](/index.php/Systemd "Systemd")取代sysvinit。

**Note:** 若希望了解 Arch 為何轉變到 systemd, 請參照 [這篇文章](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 systemd 基本工具](#systemd_基本工具)
    *   [1.1 分析系統狀態](#分析系統狀態)
    *   [1.2 使用單元](#使用單元)
    *   [1.3 電源管理](#電源管理)
*   [2 編寫單元檔案](#編寫單元檔案)
    *   [2.1 處理依賴關係](#處理依賴關係)
    *   [2.2 服務類型](#服務類型)
    *   [2.3 修改現有單元檔](#修改現有單元檔)
*   [3 目標（target）](#目標（target）)
    *   [3.1 获取當前目標](#获取當前目標)
    *   [3.2 創建新目標](#創建新目標)
    *   [3.3 目標表](#目標表)
    *   [3.4 切换執行級別/目標](#切换執行級別/目標)
    *   [3.5 修改預設執行級別/目標](#修改預設執行級別/目標)
*   [4 臨時檔案](#臨時檔案)
*   [5 定時器](#定時器)
*   [6 日誌](#日誌)
    *   [6.1 過濾輸出](#過濾輸出)
    *   [6.2 日誌大小的限制](#日誌大小的限制)
    *   [6.3 配合 syslog 使用](#配合_syslog_使用)
    *   [6.4 手動清理日誌](#手動清理日誌)
    *   [6.5 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
    *   [6.6 轉送 journald 到 /dev/tty12](#轉送_journald_到_/dev/tty12)
    *   [6.7 查看特定位置的日誌](#查看特定位置的日誌)
*   [7 疑難解答](#疑難解答)
    *   [7.1 尋找錯誤](#尋找錯誤)
    *   [7.2 診斷開機問題](#診斷開機問題)
    *   [7.3 診斷一个特定服務](#診斷一个特定服務)
    *   [7.4 關機/重啟十分緩慢](#關機/重啟十分緩慢)
    *   [7.5 短時處理程序無日誌記錄](#短時處理程序無日誌記錄)
    *   [7.6 禁止在程序崩溃时转储内存](#禁止在程序崩溃时转储内存)
    *   [7.7 啟動時間太長](#啟動時間太長)
    *   [7.8 systemd-tmpfiles-setup.service 在啟動時啟動失敗](#systemd-tmpfiles-setup.service_在啟動時啟動失敗)
    *   [7.9 不能設定在開機時启动軟連結到 /etc/systemd/system 的服務](#不能設定在開機時启动軟連結到_/etc/systemd/system_的服務)
*   [8 相關資源](#相關資源)

## systemd 基本工具

查看和控制systemd的主要命令是`systemctl`。該命令可用查看系統狀態和管理系統及服務。詳見[systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)。

**提示:** * 在 `systemctl` 參數中添加 `-H <使用者名稱>@<主機名>` 可以實現對其他機器的遠端控制。該過程使用 [SSH](/index.php/SSH "SSH")連線。

*   `systemadm` 是 systemd 的官方圖形前端。[官方軟體倉庫](/index.php/Official_repositories "Official repositories") 提供了稳定版本 [systemd-ui](https://www.archlinux.org/packages/?name=systemd-ui)。
*   [Plasma](/index.php/Plasma "Plasma") 用戶可以安裝 *systemctl* 圖像前端 [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/)。安裝後可以在 *System administration* 下找到

### 分析系統狀態

顯示 **系統狀態**:

```
$ systemctl status

```

顯示激活的單元（Unit）：

```
$ systemctl

```

以下命令等效：

```
$ systemctl list-units

```

顯示執行失敗的單元：

```
$ systemctl --failed

```

所有可用的單元檔案存放在 `/usr/lib/systemd/system/` 和 `/etc/systemd/system/` 目錄（後者優先級更高）。查看所有已安裝服務：

```
$ systemctl list-unit-files

```

### 使用單元

一个單元（Unit）的設定檔可以描述如下內容之一：系統服務（`.service`）、掛載點（`.mount`）、sockets（`.sockets`） 、系統設備（`.device`）、交換分割區（`.swap`）、檔案路徑（`.path`）、啟動目標（`.target`）、由 systemd 管理的計時器（`.timer`）。請參考 [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5)。

使用 `systemctl` 控制單元時，通常需要使用單元檔案的全名，包括附檔名（例如 `sshd.service`）。但是有些單元可以在`systemctl`中使用簡寫方式。

*   如果無附檔名，systemctl 預設把附檔名當作 `.service`。例如 `netcfg` 和 `netcfg.service` 是等價的。
*   掛載點會自動轉化為相應的 `.mount` 單元。例如 `/home` 等價于 `home.mount`。
*   設備會自動轉化為为相應的 `.device` 單元，所以 `/dev/sda2` 等價於 `dev-sda2.device`。

**Note:** 有一些單元的名稱包含一个 `@` 标记， (e.g. `name@*string*.service`): 這意味着它是範本单元 `name@.service` 的一个 實例。 `*string*` 被稱作實例標識符, 在 *systemctl* 調用範本單元時，會將其當作一个參數傳給範本單元，範本單元會使用這個傳入的參數代替範本中的 `%I` 指示符。

在實例化之前，*systemd* 會先檢查 `name@string.suffix` 檔案是否存在（如果存在，應該就是直接使用這個檔案，而不是將範本實例化了）。大多數情況下，包换 `@` 標記都意味着這個檔案是範本。如果一個範本單元沒有實例化就調用，該調用會返回失敗，因為範本單元中的 `%I` 指示符沒有被替換。

**Tip:**

*   下面的大部分命令都可以跟多个單元名, 詳細資訊常見 [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)。
*   從[systemd 220版本](https://github.com/systemd/systemd/blob/master/NEWS#L323-L326)開始, `systemctl`命令在`enable`、`disable`和`mask`子命令中增加了`--now`選項，可以實現激活的同時啟動服務，取消激活的同时停止服務。
*   一个軟體包可能會提供多个不同的單元。如果你已经安裝了軟體包，可以通过`pacman -Qql *package* | grep systemd`命令檢查這個軟體包提供了哪些單元。

立即激活單元：

```
# systemctl start <單元>

```

立即停止單元：

```
# systemctl stop <單元>

```

重启單元：

```
# systemctl restart <單元>

```

重新載入配置：

```
# systemctl reload <單元>

```

顯示單元的運行狀態：

```
$ systemctl status <單元>

```

檢查單元是否配置為自動啟動：

```
$ systemctl is-enabled <單元>

```

開機時自动激活單元：

```
# systemctl enable <單元>

```

取消開機自動激活單元：

```
# systemctl disable <單元>

```

禁用一个單元(禁用后，間接啟動也是不可能的)：

```
# systemctl mask <單元>

```

取消禁用一个單元：

```
# systemctl unmask <單元>

```

顯示單元的手冊頁（必须須由單元檔案提供）：

```
# systemctl help <單元>

```

重新載入 systemd，掃描新的或有變動的單元：

```
# systemctl daemon-reload

```

### 電源管理

安裝 [polkit](/index.php/Polkit "Polkit") 後才可以一般使用者身分使用電源管理。

如果你正登入在一个本機的`systemd-logind`工作階段，且當前沒有其它活動的工作階段，那麼以下命令無需root權限即可執行。否則（例如，當前有另一个使用者登入在某个tty），systemd 將會自動請求輸入root密碼。

重新啟動：

```
$ systemctl reboot

```

關機：

```
$ systemctl poweroff

```

待機：

```
$ systemctl suspend

```

休眠：

```
$ systemctl hibernate

```

混合休眠模式（同时休眠到硬碟並待機）：

```
$ systemctl hybrid-sleep

```

## 編寫單元檔案

`systemd` [單元檔案](http://www.freedesktop.org/software/systemd/man/systemd.unit.html)的語法來源於XDG桌面入口設定檔`.desktop`檔案，最初的源头則是Microsoft Windows的`.ini`檔案。單元檔案可以從2個地方載入，優先級從低到高分別是：

*   `/usr/lib/systemd/system/`: 軟體包安裝的單元
*   `/etc/systemd/system/`: 系統管理員安裝的單元

*   當`systemd`執行在[使用者模式](/index.php/Systemd/User#How_it_works "Systemd/User")下时，使用的載入路徑是完全不同的。
*   systemd 單元名稱仅能包含 ASCII 字符, 下劃線和點號. 其它字符需要用 C-style "\x2d" 替換. 參閱 [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) 和 [systemd-escape(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-escape.1).}}

單元檔的語法，可以參考系統中已經安裝的單元，也可以參考[systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5)中的[EXAMPLES章節](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples)。

**提示:** 以 `#` 開頭的注释可能也能用在 unit-files 中, 但是只能在新行中使用。 不要在 *systemd* 的參數後面使用行末註釋， 否則 unit 將會啟動失敗。

### 處理依賴關係

使用systemd时，可通過正確編寫單元檔來解決其依賴關係。典型的情況是，單元`A`要求單元`B`在`A`啟動之前執行。在此情況下，向單元`A`設定檔中的 `[Unit]` 段添加 `Requires=B` 和 `After=B` 即可。若此依賴關係是可选的，可添加 `Wants=B` 和 `After=B`。請注意 `Wants=` 和 `Requires=` 並不意味着 `After=`，即如果 `After=` 選項沒有制定，這兩個單元將被並行啟動。

依賴關係通常被用在服務（service）而不是[目標（target）](#目標（target）)上。例如， `network.target` 一般會被某个配置網路介面的服務引入，所以，將自訂的單元排在該服務之後即可，因為 `network.target` 已經啟動。

### 服務類型

編寫自訂的 service 檔案时，可以選擇幾種不同的服務啟動方式。啟動方式可通过設定檔 `[Service]` 段中的 `Type=` 參數進行設定。

*   `Type=simple`（預設值）：systemd認為該服務將立即啟動。服務程序不會fork。如果該服務要啟動其他服務，不要使用此類型啟動，除非該服務是socket激活型。
*   `Type=forking`：systemd認為當該服務程序fork，且父程序退出後服務啟動成功。對於常規的守护程序（daemon），除非你確定此啟動方式無法滿足需求，使用此類型啟動即可。使用此啟動類型應該同時指定 `PIDFile=`，以便systemd能夠跟踪服務的主程序。
*   `Type=oneshot`：這一選項適用於只执行一項任務、随後立即退出的服務。可能需要同時設定 `RemainAfterExit=yes` 使得 systemd 在服務程序退出之後仍然認為服務處於激活狀態。
*   `Type=notify`：與 `Type=simple` 相同，但約定服務會在就緒後向 systemd 發送一個信號。這一通知的實現由 `libsystemd-daemon.so` 提供。
*   `Type=dbus`：若以此方式啟動，當指定的 `BusName` 出現在D-Bus系統總線上时，systemd認為服務就緒。
*   `Type=idle`: `systemd`會等待所有工作處理完成後，才開始執行`idle`類型的單元。其他行為和`Type=simple` 類似。

`type`的更多解釋可以參考 [systemd.service(5)](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=)。

### 修改現有單元檔

為了避免和 pacman 衝突，不應該直接編輯軟體包提供的檔案. 要更改由軟體包提供的單元檔，先創建名為 `/etc/systemd/system/<單元名>.d/` 的目錄（如 `/etc/systemd/system/httpd.service.d/`），然後放入 `*.conf` 檔案，其中可以添加或重設參數。這裡設定的參數優先級高於原來的單元檔案。例如，如果想添加一个額外的依賴，創建這麼一個檔案即可：

 `/etc/systemd/system/<unit>.d/customdependency.conf` 
```
[Unit]
Requires=<新依賴>
After=<新依賴>
```

As another example, in order to replace the `ExecStart` directive for a unit that is not of type `oneshot`, create the following file:

 `/etc/systemd/system/*unit*.d/customexec.conf` 
```
[Service]
ExecStart=
ExecStart=*new command*
```

想知道為什麼修改 `ExecStart` 前必須將其置空，參見 ([[1]](https://bugzilla.redhat.com/show_bug.cgi?id=756787#c9)).

下面是自動重啟服務的一个例子:

 `/etc/systemd/system/*unit*.d/restart.conf` 
```
[Service]
Restart=always
RestartSec=30
```

然後執行以下命令使更改生效：

```
# systemctl daemon-reload
# systemctl restart <單元>

```

此外，把舊的單元檔案從 `/usr/lib/systemd/system/` 複製到 `/etc/systemd/system/`，然後進行修改，也可以達到同樣的效果。在 `/etc/systemd/system/` 目錄中的單元檔的優先級總是高於 `/usr/lib/systemd/system/` 目錄中的同名單元檔案。注意，當 `/usr/lib/` 中的單元檔因軟體包升級而變更时，`/etc/` 中自訂的單元檔案不會同步更新。此外，你還得執行行 `systemctl reenable <unit>`，手動重新啟用該單元。因此，建議使用前面一種利用 `*.conf` 的方法。

**提示:** 用 `systemd-delta` 命令來查看哪些單元檔案被覆蓋、哪些被修改。系統維護的時候需要即時了解哪些單元已經有了更新。

安裝 [vim-systemd](https://aur.archlinux.org/packages/vim-systemd/) 軟體包，可以使 unit 設定檔在 [Vim](/index.php/Vim "Vim") 下支持語法高亮。

## 目標（target）

執行級別（runlevel）是一个舊的概念。現在，systemd 引入了一個和執行級別功能相似又不同的概念——目標（target）。不像數字表示的執行級別，每個*目標*都有名字和獨特的功能，並且能同時啟用多個。一些*目標*繼承其他*目標*的服務，並啟動新服務。systemd 提供了一些模仿 sysvinit 執行級別的*目標*，仍可以使用舊的 `telinit 執行級別` 命令切換。

### 获取當前目標

不要使用 `runlevel` 命令了：

```
$ systemctl list-units --type=target

```

### 創建新目標

在 Fedora 中，啟動級別 0、1、3、5、6 都被赋予特定用途，並且都對應一個 systemd 的*目標*。然而，沒有什麼很好的移植用戶定義的執行級別（2、4）的方法。要實現類似功能，可以以原有的執行級別為基礎，創建一个新的*目標* `/etc/systemd/system/<新目標>`（可以參考 `/usr/lib/systemd/system/graphical.target`），創建 `/etc/systemd/system/<新目標>.wants` 目錄，向其中加入額外服務的連結（指向 `/usr/lib/systemd/system/` 中的單元檔案）。

### 目標表

| SysV 執行級別 | Systemd 目標 | 註釋 |
| 0 | runlevel0.target, poweroff.target | 停機，關閉系統（halt） |
| 1, s, single | runlevel1.target, rescue.target | 單使用者模式 |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | 用戶自訂启动級別，通常識別為級別3。 |
| 3 | runlevel3.target, multi-user.target | 多使用者，無圖形界面。使用者可以通過終端或網路登入。 |
| 5 | runlevel5.target, graphical.target | 多用戶，圖形界面。繼承級別3的服務，並啟動圖形界面服務。 |
| 6 | runlevel6.target, reboot.target | 重新開機 |
| emergency | emergency.target | 急救模式（Emergency shell） |

### 切换執行級別/目標

systemd 中，執行級別通過“目標單元”設定。通过如下命令切換：

```
# systemctl isolate graphical.target

```

該命令對下次啟動無影响。等價於`telinit 3` 或 `telinit 5`。

### 修改預設執行級別/目標

開機啟動進入的目標是 `default.target`，預設連結到 `graphical.target` （大致相當於原來的啟動級別5）。可以通過[內核參數](/index.php/Kernel_parameters "Kernel parameters")更改預設啟動級別：

*   `systemd.unit=multi-user.target` （大致相當於級別3）
*   `systemd.unit=rescue.target` （大致相當於級別1）

另一個方法是修改 `default.target`。可以通過 `systemctl` 修改它：

```
# systemctl set-default multi-user.target

```

要覆蓋已經設置的*default.target*，請使用 force:

```
# systemctl set-default -f multi-user.target

```

可以在 `systemctl` 的輸出中看到命令执行的效果：連結 `/etc/systemd/system/default.target` 被創建，指向新的預設啟動級別。

## 臨時檔案

`/usr/lib/tmpfiles.d/` 和 `/etc/tmpfiles.d/` 中的檔案描述了 systemd-tmpfiles 如何創建、清理、删除臨時檔案和目錄，這些檔案和目錄通常存放在 `/run` 和 `/tmp` 中。設定檔名稱為 `/etc/tmpfiles.d/<program>.conf`。此處的配置能覆蓋 `/usr/lib/tmpfiles.d/`目錄中的同名配置。

臨時檔案通常和服務檔案同时提供，以生成守護程序需要的檔案和目錄。例如 [Samba](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Samba (简体中文)") 服務需要目錄 `/run/samba` 存在並設置正確的權限位，就象這樣：

 `/usr/lib/tmpfiles.d/samba.conf` 
```
D /run/samba 0755 root root

```

此外，臨時檔案還可以用來在開機時向特定檔案寫入某些內容。比如，要禁止系統從USB裝置唤醒，利用舊的 `/etc/rc.local` 可以用 `echo USBE > /proc/acpi/wakeup`，而現在可以這麼做：

 `/etc/tmpfiles.d/disable-usb-wake.conf` 
```
w /proc/acpi/wakeup - - - - USBE

```

詳情參見`systemd-tmpfiles(8)` 和 [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5)。

**注意:** 該方法不能向 `/sys` 中的設定檔加入參數，因為 `systemd-tmpfiles-setup` 有可能在相關模組載入前運行。這種情況下，需要首先通過 `modinfo <模組名>` 確認需要的參數，並在 [`/etc/modprobe.d` 下的一个檔案](/index.php/Kernel_modules#Options "Kernel modules")中設置改參數。另外，還可以使用 [udev 規則](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#udev規則 "Udev (简体中文)")，在設備就緒時設定相應屬性。

## 定時器

Systemd Timer是以 *.timer* 为附檔名的設定檔，記錄由system裡面由時間觸發的動作, Timer可以替代 *cron* 的大部分功能。請參閱 [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")和[cron](/index.php/Cron "Cron").

## 日誌

systemd 提供了自己的日誌系統（logging system），稱為 [journald](/index.php?title=Journald&action=edit&redlink=1 "Journald (page does not exist)"). 使用 systemd 日誌，無需額外安裝日誌服務（syslog）。讀取日誌的命令：

```
# journalctl

```

預設情況下（當 `Storage=` 在檔案 `/etc/systemd/journald.conf` 中被設定為 `auto`），日誌記錄将被寫入 `/var/log/journal/`。該目錄是 [systemd](https://www.archlinux.org/packages/?name=systemd) 軟體包的一部分。若被删除，systemd **不會**自動創建它，直到下次升級軟體包时重建該目錄。如果該目錄缺失，systemd 會將日誌記錄寫入 `/run/systemd/journal`。這意味著，系統重啟後日誌將丟失。

**Tip:** 如果 `/var/log/journal/` 位于 [btrfs](/index.php/Btrfs "Btrfs") 檔案系統，應該考慮對這個目錄禁用寫入時複製（COW，Copy On Write），參閱[Btrfs#Copy-on-Write (CoW)](/index.php/Btrfs#Copy-on-Write_(CoW) "Btrfs").

### 過濾輸出

`journalctl`可以根據特定字段過濾输出。如果過濾的字段比較多，需要較長時間才能顯示出來。

示例：

顯示本次啟動後的所有日誌：

```
# journalctl -b

```

不過，一般大家更關心的不是本次啟動後的日誌，而是上次啟動時的（例如，剛剛系統崩溃了）。可以使用 `-b` 參數:

*   `journalctl -b -0` 顯示本次啟動的訊息
*   `journalctl -b -1` 顯示上次啟動的訊息
*   `journalctl -b -2` 顯示上上次啟動的訊息 `journalctl -b -2`

*   現實從某个日期 ( 或時間 ) 開始的訊息: `# journalctl --since="2012-10-30 18:17:16"` 
*   顯示從某個時間 ( 例如 20分鐘前 ) 的訊息: `# journalctl --since "20 min ago"` 
*   顯示最新訊息 `# journalctl -f` 
*   顯示特定程式的所有訊息: `# journalctl /usr/lib/systemd/systemd` 
*   顯示特定處理程序的所有訊息: `# journalctl _PID=1` 
*   顯示指定單元的所有訊息： `# journalctl -u netcfg` 
*   顯示內核環快取訊息r: `# journalctl -k` 
*   Show auth.log equivalent by filtering on syslog facility: `# journalctl -f -l SYSLOG_FACILITY=10` 

詳情請參閱[journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1)、[systemd.journal-fields(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7)。

### 日誌大小的限制

如果按上面的操作保留日誌的話，預設的日誌最大限制为所在檔案系統容量的 10%，即：如果 `/var/log/journal` 儲存在 50GiB 的根分割區中，那麼日誌最多存储 5GiB 的資料。可以修改設定檔指定最大限制。如限制日誌最大 50MiB：

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

詳情請參考 [journald.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5).

### 配合 syslog 使用

systemd 提供了 socket `/run/systemd/journal/syslog`，以相容傳統日誌服務。所有系统資訊都會被傳入。要使傳統日誌服務工作，需要讓服務連結該 socket，而非 `/dev/log`（[官方說明](http://lwn.net/Articles/474968/)）。Arch 軟體仓庫中的 [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) 已經包含了需要的配置。

*systemd* 216 開始,`journald.conf` 使用 `no` 轉送socket . 为了使 *syslog-ng* 配合 *journald* , 你需要在 `/etc/systemd/journald.conf` 中設置 `ForwardToSyslog=yes` . 參閱 [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") 了解更多細節.

如果你選擇使用 [rsyslog](https://aur.archlinux.org/packages/rsyslog/) , 因為 [rsyslog](/index.php/Rsyslog "Rsyslog") 從日誌中 [直接](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald) 傳出消息,所以不再必要改變那個選項..

設定開機啟動 syslog-ng：

```
 # systemctl enable syslog-ng

```

### 手動清理日誌

`/var/log/journal` 存放着日誌, `rm` 應該能工作. 或者使用`journalctl`,

例如:

*   清理日誌使總大小小於 100M: `# journalctl --vacuum-size=100M` 
*   清理最早兩週前的日誌. `# journalctl --vacuum-time=2weeks` 

參閱 {ic|man journalctl}} 获得更多資訊.

### Journald in conjunction with syslog

Compatibility with a classic, non-journald aware [syslog](/index.php/Syslog-ng "Syslog-ng") implementation can be provided by letting *systemd* forward all messages via the socket `/run/systemd/journal/syslog`. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)).

As of *systemd* 216 the default `journald.conf` for forwarding to the socket was changed to `ForwardToSyslog=no` to avoid system overhead, because [rsyslog](/index.php/Rsyslog "Rsyslog") or [syslog-ng](/index.php/Syslog-ng "Syslog-ng") (since 3.6) pull the messages from the journal by [itself](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

See [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") and [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng"), or [rsyslog](/index.php/Rsyslog "Rsyslog") respectively, for details on configuration.

### 轉送 journald 到 /dev/tty12

建立一個 [drop-in directory](#Editing_provided_units) `/etc/systemd/journald.conf.d` 然後在其中建立 `fw-tty12.conf` :

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

然後重新啟動 systemd-journald.

### 查看特定位置的日誌

有时你希望查看另一個系統上的日誌.例如从 Live 環境修复現有的系統.

這種情況下你可以掛載目標系統 ( 例如掛載到 `/mnt` ),然後用 `-D`/`--directory` 參數指定目錄,像這樣:

```
$ journalctl -D */mnt*/var/log/journal -xe

```

## 疑難解答

### 尋找錯誤

這個例子中的失敗的服務是 `systemd-modules-load` :

**1.** 通過 *systemd* 尋找啟動失敗的服務:

 `$ systemctl --state=failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

**2.** 我們發現了啟動失敗的 `systemd-modules-load` 服務. 我們想知道更多諮詢:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: loaded (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **failed** (Result: exit-code) since So 2013-08-25 11:48:13 CEST; 32s ago
     Docs: man:systemd-modules-load.service(8).
           man:modules-load.d(5)
  Process: **15630** ExecStart=/usr/lib/systemd/systemd-modules-load (**code=exited, status=1/FAILURE**)
```

如果沒有列出 `Process ID`, 通過 `systemctl` 重新啟動失敗的服務 ( 例如 `systemctl restart systemd-modules-load` )

**3.** 現在得到了 PID ,你就可以進一步探查錯誤的詳細資訊了.通過下列的命令收集日誌,PID 參數是你剛剛得到的 `Process ID` (例如 15630):

 `$ journalctl -b _PID=15630` 
```
-- Logs begin at Sa 2013-05-25 10:31:12 CEST, end at So 2013-08-25 11:51:17 CEST. --
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'blacklist usblp'**
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'install usblp /bin/false'**
```

**4.** 我們發現有些內核模組的設定檔不正確,因此在 `/etc/modules-load.d/` 中檢查一下:

 `$ ls -Al /etc/modules-load.d/` 
```
...
-rw-r--r--   1 root root    79  1\. Dez 2012  blacklist.conf
-rw-r--r--   1 root root     1  2\. Mär 14:30 encrypt.conf
-rw-r--r--   1 root root     3  5\. Dez 2012  printing.conf
-rw-r--r--   1 root root     6 14\. Jul 11:01 realtek.conf
-rw-r--r--   1 root root    65  2\. Jun 23:01 virtualbox.conf
...

```

**5.** 錯誤訊息 `Failed to find module 'blacklist usblp'` 也許和 `blacklist.conf` 相關. 讓我們註釋掉第三步發現的錯誤的選項:

 `/etc/modules-load.d/blacklist.conf` 
```
**#** blacklist usblp
**#** install usblp /bin/false

```

**6.** 最後重新啟動 `systemd-modules-load` 服務:

```
$ systemctl start systemd-modules-load

```

如果服務成功啟動，不會有任何輸出.如果你还是遇到了錯誤,回到步驟三,获得新的 PID 来跟踪日誌並解決錯誤.

可以像這樣確認服務成功啟動:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: **loaded** (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **active (exited)** since So 2013-08-25 12:22:31 CEST; 34s ago
     Docs: man:systemd-modules-load.service(8)
           man:modules-load.d(5)
 Process: 19005 ExecStart=/usr/lib/systemd/systemd-modules-load (code=exited, status=0/SUCCESS)
Aug 25 12:22:31 mypc systemd[1]: **Started Load Kernel Modules**.
```

參閱 [#診斷開機問題](#診斷開機問題) 一節获得更多探查錯誤的方法.

### 診斷開機問題

使用如下內核參數開機： `systemd.log_level=debug systemd.log_target=kmsg log_buf_len=1M`

更多有關偵錯的資訊，參見[[2]](http://freedesktop.org/wiki/Software/systemd/Debugging)。

### 診斷一个特定服務

如果某个 *systemd* 服務的工作狀況不合你的預期，因此你希望偵錯的话,設定 `SYSTEMD_LOG_LEVEL` [環境變數](/index.php/Environment_variable "Environment variable") 为 `debug` . 例如以偵錯模式執行 *systemd-networkd* 服務:

```
# systemctl stop systemd-networkd
# SYSTEMD_LOG_LEVEL=debug /lib/systemd/systemd-networkd

```

或者等價的,臨時編輯系統單元檔,例如:

 `/lib/systemd/system/systemd-networkd.service` 
```
[Service]
...
Environment=SYSTEMD_LOG_LEVEL=debug
....
```

如果經常需要偵錯資訊,以[一般方法](#修改現有單元檔)增加環境變數.

### 關機/重啟十分緩慢

如果關機特别慢（甚至跟當機了一样），很可能是某个拒不退出的服務在作怪。systemd 會等待一段時間，然後再嘗試殺死它。請閱讀[這篇文章](http://freedesktop.org/wiki/Software/systemd/Debugging#Shutdown_Completes_Eventually)，確認你是否是該問題的受害者。

### 短時處理程序無日誌記錄

若 `journalctl -u foounit.service` 沒有顯示某个短時處理程序的任何輸出，那麼改用 PID 試試。例如，若 `systemd-modules-load.service` 执行失敗，那麼先用 `systemctl status systemd-modules-load` 查詢其 PID（比如是123），然後檢索該 PID 相關的日誌 `journalctl -b _PID=123`。執行時處理程序的日誌元資料（諸如 _SYSTEMD_UNIT 和 _COMM）被亂序收集在 `/proc` 目錄。要修复該問題，必須修改內核，使其通過Socket連線來提供上述資料，該過程類似於 SCM_CREDENTIALS。

### 禁止在程序崩溃时转储内存

要使用老的內核轉儲，創建下面檔案:

 `/etc/sysctl.d/49-coredump.conf` 
```
kernel.core_pattern = core
kernel.core_uses_pid = 0
```

然後執行：

```
# /usr/lib/systemd/systemd-sysctl

```

同樣可能需要執行“unlimit”設定檔案大小：

```
$ ulimit -c unlimited

```

更多資訊請參閱 [sysctl.d](http://www.freedesktop.org/software/systemd/man/sysctl.d.html) 和 [/proc/sys/kernel](https://www.kernel.org/doc/Documentation/sysctl/kernel.txt) 。

### 啟動時間太長

不少用戶使用 `systemd-analyze` 命令以後報告啟動的時間比預計的要長,通常會說 `systemd-analyze` 分析結果表示 [NetworkManager](/index.php/NetworkManager "NetworkManager") 佔用了太多的啟動時間.

有些用戶的問題是 `/var/log/journal` 資料夾似乎過大.這也許也會對像`systemctl status` 或 `journalctl` 的命令有影响.一种解決方案是删除其中的檔案 (但最好將他們備份到某处) 然後限制日誌檔案的大小.請參考[journald](/index.php?title=Journald&action=edit&redlink=1 "Journald (page does not exist)").

### systemd-tmpfiles-setup.service 在啟動時啟動失敗

從 systemd 219 開始, `/usr/lib/tmpfiles.d/systemd.conf` 指定 `/var/log/journal` 的 ACL 屬性和目錄, 因此日誌所在的檔案系統上要啟用ACL.

參考 [Access Control Lists#Enabling ACL](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") 获得如何包含 `/var/log/journal` 啟動 ACL 的詳細資訊.

### 不能設定在開機時启动軟連結到 /etc/systemd/system 的服務

如果 `/etc/systemd/system/*foo*.service` 是个符號連結， 執行 `systemctl enable *foo*.service` 時可能遇到這樣的錯誤:

```
Failed to issue method call: No such file or directory

```

這是 systemd 的 [設計選擇](https://bugzilla.redhat.com/show_bug.cgi?id=955379#c14) ,可以通過輸入絕對路徑來規避這個錯誤:

```
# systemctl enable */absolute/path/foo*.service

```

## 相關資源

*   [[3]](http://www.freedesktop.org/wiki/Software/systemd官方網站)
*   [[Wikipedia:zh:systemd|維基百科對systemd的介紹]
*   [systemd優化](http://freedesktop.org/wiki/Software/systemd/Optimizations)
*   [常見問題FAQ](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [[4]](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks小技巧)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [Fedora對systemd的介紹](http://fedoraproject.org/wiki/Systemd)