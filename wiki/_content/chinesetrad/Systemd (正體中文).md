節錄自 [systemd 專案網頁](http://freedesktop.org/wiki/Software/systemd):

**systemd** 是一個Linux的系統與服務管理器, 並且相容於 SysV 與 LSB init scripts. systemd 提供並行化任務的能力, 使用 socket 與 [D-Bus](/index.php/D-Bus "D-Bus") 來啟動服務, 按照需要啟動服務(daemons), 使用 Linux [control groups](/index.php/Cgroups "Cgroups") 來追蹤程序, 支援系統快照與回復系統狀態, 維護掛載與自動掛載點. 並由精密的控制來管理各個服務. 它亦可以完美的取代 sysvinit。

**Note:** 若希望了解 Arch 為何轉變到 systemd, 請參照 [這篇文章](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

## 遷移至 systemd 前須考慮的事

*   高度建議先把 [rc.conf](/index.php/Rc.conf "Rc.conf") 轉換至最新的 **initscripts**. 當你轉換至這個設定, 你就做完大部分遷移到 systemd 必須的事項。
*   了解一下 [systemd](http://freedesktop.org/wiki/Software/systemd/)。
*   注意到 systemd 有自己的 **日誌**系統來取代 **syslog**, 但兩者是可以並存的。 參見[#與syslog](#.E8.88.87syslog)
*   雖然 systemd 可以取代一些功能像是 **cron**, **acpid**, **xinetd** 等, 但是除非你希望以 systemd 替代, 要不然是可以不用改變的。

## systemd 安裝

systemd 可以與 Arch 默認的啟動系統[initscripts](https://www.archlinux.org/packages/?name=initscripts) 共存, 並且透過增加/移除[核心參數](/index.php?title=%E6%A0%B8%E5%BF%83%E5%8F%83%E6%95%B8&action=edit&redlink=1 "核心參數 (page does not exist)")`init=/usr/lib/systemd/systemd`來切換。