**翻译状态：** 本文是英文页面 [Systemd/Journal](/index.php/Systemd/Journal "Systemd/Journal") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-01-31，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd%2FJournal&diff=0&oldid=565200)可以查看翻译后英文页面的改动。

主文档请参考 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")。

systemd 提供了自己的日志系统（logging system），称为 journal。使用 systemd 日志，无需额外安装日志服务（syslog）。读取日志的命令：

```
# journalctl

```

默认情况下（当 `Storage=` 在文件 `/etc/systemd/journald.conf` 中被设置为 `auto`），日志记录将被写入 `/var/log/journal/`。该目录是 [systemd](https://www.archlinux.org/packages/?name=systemd) 软件包的一部分。若被删除，systemd **不会**自动创建它，直到下次升级软件包时重建该目录。如果该目录缺失，systemd 会将日志记录写入 `/run/systemd/journal`。这意味着，系统重启后日志将丢失。

**提示：** 如果 `/var/log/journal/` 位于 [btrfs](/index.php/Btrfs "Btrfs") 文件系统，应该考虑对这个目录禁用写入时复制，方法参阅[Btrfs#Copy-on-Write (CoW)](/index.php/Btrfs#Copy-on-Write_(CoW) "Btrfs")。

Systemd 日志事件提示信息的记录安装优先级和更能进行分离，符合经典的 BSD syslog 协议风格（[维基百科](https://en.wikipedia.org/wiki/Syslog "wikipedia:Syslog")，[RFC 5424](https://tools.ietf.org/html/rfc5424)）。

## Contents

*   [1 优先级](#优先级)
*   [2 功能](#功能)
*   [3 过滤输出](#过滤输出)
*   [4 日志大小限制](#日志大小限制)
*   [5 配合 syslog 使用](#配合_syslog_使用)
*   [6 手动清理日志](#手动清理日志)
*   [7 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
*   [8 转发 journald 到 /dev/tty12](#转发_journald_到_/dev/tty12)
*   [9 查看特定位置的日志](#查看特定位置的日志)

## 优先级

A syslog severity code (in systemd called priority) is used to mark the importance of a message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Value | Severity | Keyword | Description | Examples |
| 0 | Emergency | emerg | System is unusable | Severe Kernel BUG, systemd dumped core.
This level should not be used by applications. |
| 1 | Alert | alert | Should be corrected immediately | Vital subsystem goes out of work. Data loss.
`kernel: BUG: unable to handle kernel paging request at ffffc90403238ffc`. |
| 2 | Critical | crit | Critical conditions | Crashes, coredumps. Like familiar flash:
`systemd-coredump[25319]: Process 25310 (plugin-containe) of user 1000 dumped core`
Failure in the system primary application, like X11. |
| 3 | Error | err | Error conditions | Not severe error reported:
`kernel: usb 1-3: 3:1: cannot get freq at ep 0x84`,
`systemd[1]: Failed unmounting /var.`,
`libvirtd[1720]: internal error: Failed to initialize a valid firewall backend`). |
| 4 | Warning | warning | May indicate that an error will occur if action is not taken. | A non-root file system has only 1GB free.
`org.freedesktop. Notifications[1860]: (process:5999): Gtk-WARNING **: Locale not supported by C library. Using the fallback 'C' locale`. |
| 5 | Notice | notice | Events that are unusual, but not error conditions. | `systemd[1]: var.mount: Directory /var to mount over is not empty, mounting anyway`. `gcr-prompter[4997]: Gtk: GtkDialog mapped without a transient parent. This is discouraged`. |
| 6 | Informational | info | Normal operational messages that require no action. | `lvm[585]: 7 logical volume(s) in volume group "archvg" now active`. |
| 7 | Debug | debug | Information useful to developers for debugging the application. | `kdeinit5[1900]: powerdevil: Scheduling inhibition from ":1.14" "firefox" with cookie 13 and reason "screen"`. |

If issue you are looking for, was not found on according level, search it on couple of priority levels above and below. This rules are recommendations. Some errors considered a normal occasion for program so they marked low in priority by developer, and on the contrary, sometimes too many messages plaques too high priorities for them, but often it's an arguable situation. And often you really should solve an issue, also to understand architecture and adopt best practices.

Examples:

*   Info message: `pulseaudio[2047]: W: [pulseaudio] alsa-mixer.c: Volume element Master has 8 channels. That's too much! I can't handle that!` It is an warning or error by definition.
*   Plaguing alert message: `sudo[21711]:     user : a password is required ; TTY=pts/0 ; PWD=/home/user ; USER=root ; COMMAND=list /usr/bin/pacman --color auto -Sy` The [reason](https://bbs.archlinux.org/viewtopic.php?id=184455) - user was manually added to sudoers file, not to wheel group, which is arguably normal action, but sudo produced an alert on every occasion.

## 功能

A syslog facility code is used to specify the type of program that is logging the message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Facility code | Keyword | Description | Info |
| 0 | kern | kernel messages |
| 1 | user | user-level messages |
| 2 | mail | mail system | Archaic POSIX still supported and sometimes used system, for more [mail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mail.1)) |
| 3 | daemon | system daemons | All deamons, including systemd and its subsystems |
| 4 | auth | security/authorization messages | Also watch for different facility 10 |
| 5 | syslog | messages generated internally by syslogd | As it standartized for syslogd, not used by systemd (see facility 3) |
| 6 | lpr | line printer subsystem (archaic subsystem) |
| 7 | news | network news subsystem (archaic subsystem) |
| 8 | uucp | UUCP subsystem (archaic subsystem) |
| 9 | clock daemon | systemd-timesyncd |
| 10 | authpriv | security/authorization messages | Also watch for different facility 4 |
| 11 | ftp | FTP daemon |
| 12 | - | NTP subsystem |
| 13 | - | log audit |
| 14 | - | log alert |
| 15 | cron | scheduling daemon |
| 16 | local0 | local use 0 (local0) |
| 17 | local1 | local use 1 (local1) |
| 18 | local2 | local use 2 (local2) |
| 19 | local3 | local use 3 (local3) |
| 20 | local4 | local use 4 (local4) |
| 21 | local5 | local use 5 (local5) |
| 22 | local6 | local use 6 (local6) |
| 23 | local7 | local use 7 (local7) |

So, useful facilities to watch: 0,1,3,4,9,10,15.

## 过滤输出

`journalctl`可以根据特定字段过滤输出。如果过滤的字段比较多，需要较长时间才能显示出来。

示例：

显示本次启动后的所有日志：

```
# journalctl -b

```

不过，一般大家更关心的不是本次启动后的日志，而是上次启动时的（例如，刚刚系统崩溃了）。可以使用 `-b` 参数：

*   `journalctl -b -0` 显示本次启动的信息
*   `journalctl -b -1` 显示上次启动的信息
*   `journalctl -b -2` 显示上上次启动的信息 `journalctl -b -2`
*   只显示错误、冲突和重要告警信息 `# journalctl -p err..alert` 也可以使用数字， `journalctl -p 3..1`。If single number/keyword used, `journalctl -p 3` - all higher priority levels also included.

*   显示从某个日期 ( 或时间 ) 开始的消息: `# journalctl --since="2012-10-30 18:17:16"` 
*   显示从某个时间 ( 例如 20分钟前 ) 的消息: `# journalctl --since "20 min ago"` 
*   显示最新信息 `# journalctl -f` 
*   显示特定程序的所有消息: `# journalctl /usr/lib/systemd/systemd` 
*   显示特定进程的所有消息: `# journalctl _PID=1` 
*   显示指定单元的所有消息： `# journalctl -u man-db.service` 
*   显示内核环缓存消息r: `# journalctl -k` 
*   Show auth.log equivalent by filtering on syslog facility: `# journalctl -f -l SYSLOG_FACILITY=10` 
*   If your journal directory (by default located under `/var/log/journal`) contains huge amount of log data then `journalctl` can take several minutes in filtering output. You can speed it up significantly by using `--file` option to force `journalctl` to look only into most recent journal: `# journalctl --file /var/log/journal/*/system.journal -f` 

详情参阅[journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1)、[systemd.journal-fields(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7)，以及 Lennert 的这篇[博文](http://0pointer.de/blog/projects/journalctl.html)。

## 日志大小限制

如果按上面的操作保留日志的话，默认日志最大限制为所在文件系统容量的 10%，即：如果 `/var/log/journal` 储存在 50GiB 的根分区中，那么日志最多存储 5GiB 数据。可以修改配置文件指定最大限制。如限制日志最大 50MiB：

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

还可以通过配置片段而不是全局配置文件进行设置：

 `/etc/systemd/journald.conf.d/00-journal-size.conf` 
```
[Journal]
SystemMaxUse=50M
```

修改配置后要立即生效，请[重启](/index.php/Restart "Restart") `systemd-journald.service` 服务。

详情参见 [journald.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5).

## 配合 syslog 使用

systemd 提供了 socket `/run/systemd/journal/syslog`，以兼容传统日志服务。所有系统信息都会被传入。要使传统日志服务工作，需要让服务链接该 socket，而非 `/dev/log`（[官方说明](http://lwn.net/Articles/474968/)）。Arch 软件仓库中的 [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) 已经包含了需要的配置。

`journald.conf` 使用 `no` 转发socket . 为了使 *syslog-ng* 配合 *journald* , 你需要在 `/etc/systemd/journald.conf` 中设置 `ForwardToSyslog=yes` . 参阅 [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") 了解更多细节.

如果你选择使用 [rsyslog](https://aur.archlinux.org/packages/rsyslog/) , 因为 [rsyslog](/index.php/Rsyslog "Rsyslog") 从日志中 [直接](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald) 传出消息,所以不再必要改变那个选项..

设置开机启动 syslog-ng：

```
 # systemctl enable syslog-ng

```

[这里](http://0pointer.de/blog/projects/)有一份很不错的 `journalctl` 指南。

## 手动清理日志

`/var/log/journal` 存放着日志, `rm` 应该能工作. 或者使用`journalctl`,

例如:

*   清理日志使总大小小于 100M: `# journalctl --vacuum-size=100M` 
*   清理最早两周前的日志. `# journalctl --vacuum-time=2weeks` 

参阅 [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) 获得更多信息.

## Journald in conjunction with syslog

Compatibility with a classic, non-journald aware [syslog](/index.php/Syslog-ng "Syslog-ng") implementation can be provided by letting *systemd* forward all messages via the socket `/run/systemd/journal/syslog`. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)).

As of *systemd* 216 the default `journald.conf` for forwarding to the socket was changed to `ForwardToSyslog=no` to avoid system overhead, because [rsyslog](/index.php/Rsyslog "Rsyslog") or [syslog-ng](/index.php/Syslog-ng "Syslog-ng") (since 3.6) pull the messages from the journal by [itself](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

See [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") and [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng"), or [rsyslog](/index.php/Rsyslog "Rsyslog") respectively, for details on configuration.

## 转发 journald 到 /dev/tty12

建立一个 [drop-in directory](#Editing_provided_units) `/etc/systemd/journald.conf.d` 然后在其中建立 `fw-tty12.conf` :

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

然后重新启动 systemd-journald.

## 查看特定位置的日志

有时你希望查看另一个系统上的日志.例如从 Live 环境修复现存的系统.

这种情况下你可以挂载目标系统 ( 例如挂载到 `/mnt` ),然后用 `-D`/`--directory` 参数指定目录,像这样:

```
$ journalctl -D */mnt*/var/log/journal -xe

```