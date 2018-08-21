Related articles

*   [systemd_(简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")
*   [systemd/User](/index.php/Systemd/User "Systemd/User")
*   [systemd FAQ_(简体中文)](/index.php/Systemd_FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd FAQ (简体中文)")
*   [cron_(简体中文)](/index.php/Cron_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cron (简体中文)")

**翻译状态：** 本文是英文页面 [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-10-25，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd%2FTimers&diff=0&oldid=340100)可以查看翻译后英文页面的改动。

Timers 是以 `.timer` 为后缀名的 [systemd](/index.php/Systemd "Systemd") 单元文件，用于控制 `.service` 文件或事件。Timers 可用来替换 [cron](/index.php/Cron "Cron")（阅读 [#替代 cron](#.E6.9B.BF.E4.BB.A3_cron)）。Timers 内置了日历定时事件和单调定时事件的支持，并可以异步执行这些事件。

## Contents

*   [1 定时器单元](#.E5.AE.9A.E6.97.B6.E5.99.A8.E5.8D.95.E5.85.83)
*   [2 服务单元](#.E6.9C.8D.E5.8A.A1.E5.8D.95.E5.85.83)
*   [3 管理](#.E7.AE.A1.E7.90.86)
*   [4 示例](#.E7.A4.BA.E4.BE.8B)
    *   [4.1 单调定时器](#.E5.8D.95.E8.B0.83.E5.AE.9A.E6.97.B6.E5.99.A8)
    *   [4.2 实时定时器](#.E5.AE.9E.E6.97.B6.E5.AE.9A.E6.97.B6.E5.99.A8)
*   [5 替代 cron](#.E6.9B.BF.E4.BB.A3_cron)
    *   [5.1 优势](#.E4.BC.98.E5.8A.BF)
    *   [5.2 注意事项](#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9)
    *   [5.3 发送邮件](#.E5.8F.91.E9.80.81.E9.82.AE.E4.BB.B6)
    *   [5.4 使用 crontab](#.E4.BD.BF.E7.94.A8_crontab)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 定时器单元

Timers 是以 `.timer` 为后缀的 *systemd* 单元文件。Timers 和其他[单元配置文件](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.BC.96.E5.86.99.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6 "Systemd (简体中文)")是类似的，它通过相同的路径加载，不同的是包含了 `[Timer]` 部分。 `[Timer]` 部分定义了何时以及如何激活定时事件。Timers 可以被定义成以下两种类型：

*   **单调定时器** 即从一个时间点过一段时间后激活定时任务。所有的单调计时器都遵循如下形式： `On*Type*Sec=`。 `OnBootSec` 和 `OnActiveSec` 是常用的单调定时器。
*   **实时定时器** (亦称"挂钟定时器") 通过日历事件激活（类似于 cronjobs ）定时任务。 使用 `OnCalender=` 来定义实时定时器。

要查阅完整的定时器选项，参见 `systemd.timer(5)` [man page](/index.php/Man_page "Man page")。 关于日历事件和时间段的定义参见 `systemd.time(7)` [man page](/index.php/Man_page "Man page").

## 服务单元

每个 `.timer` 文件所在目录都得有一个对应的 `.service` 文件（如 `foo.timer` 和 `foo.service`）。`.timer` 用于激活并控制 `.service` 文件。 `.service` 文件中不需要包含 `[Install]` 部分，因为这由 *timer* 单元接管。必要时通过在定时器的 `[Timer]` 部分指定 `Unit=` 选项来控制一个与定时器不同名的服务单元。

## 管理

使用 *timer* 单元时像其他单元一样 [enable](/index.php/Enable "Enable") 或 start 即可（别忘了添加 `.timer` 后缀）。要查看所有已启用的定时器，运行：

 `$ systemctl list-timers` 
```
NEXT                          LEFT        LAST                          PASSED     UNIT                         ACTIVATES
Thu 2014-07-10 19:37:03 CEST  11h left    Wed 2014-07-09 19:37:03 CEST  12h ago    systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
Fri 2014-07-11 00:00:00 CEST  15h left    Thu 2014-07-10 00:00:13 CEST  8h ago     logrotate.timer              logrotate.service

```

**注意:**

*   列出所有定时器（包括非活动的），使用下列命令： `systemctl list-timers --all`.
*   一个由定时器启动的服务的状态看上去会是 inactive 的，除非它当前正被触发。
*   若一个定时器不再同步，它可能会删除它在 `/var/lib/systemd/timers` 下的 `stamp-*` 文件。这些空文件只用于表示每个定时器上次运行的时间。删除后，他们将在下次定时器运行时自动重建。

## 示例

通过定时器预定执行的服务文件一般无需任何修改。以下示例将预定执行 `foo.service`，因此它的定时器应该被命名为 `foo.timer`。

### 单调定时器

定义一个在系统启动 15 分钟后执行，且之后每周都执行一次的定时器。

 `/etc/systemd/system/foo.timer` 
```
[Unit]
Description=Run foo weekly and on boot

[Timer]
OnBootSec=15min
OnUnitActiveSec=1w 

[Install]
WantedBy=timers.target

```

### 实时定时器

定义一个每周执行一次（明确时间为周一上午十二点）且上次未执行就立即执行的定时器。

 `/etc/systemd/system/foo.timer` 
```
[Unit]
Description=Run foo weekly

[Timer]
OnCalendar=weekly
Persistent=true     

[Install]
WantedBy=timers.target
```

**提示：** 特殊的事件表达式如 `daily` 和 `weekly` 表示 *特定的启动时间*，因此任何共享该日历事件的定时器将同时启动。如果该定时器的服务会计算系统资源，那么定时器共享启动事件可能会引起系统性能下降。可以考虑手动错开该定时器运行特定事件的时间，如 `OnCalendar=Wed, 23:15`。参见 [#注意事项](#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9).

## 替代 cron

尽管 [cron](/index.php/Cron "Cron") 毋庸置疑是最有名的计划任务管理器， 但 *systemd* 定时器仍可以作为一个替代品。

### 优势

使用定时器的最主要的优势在于每个任务都有它自己的 *systemd* 服务。这样做的好处包括：

*   任务可以简单地独立于他们的定时器启动，简化调试。
*   每个任务可配置运行于特定的环境中（参见 `systemd.exec(5)` [man page](/index.php/Man_page "Man page")）。
*   任务可以使用 [cgroups](/index.php/Cgroups "Cgroups") 特性。
*   任务可以配置依赖于其他 *systemd* 单元。
*   任务记录于 *systemd* 日志，便于调试。

### 注意事项

*   附注：使用 *systemd* 配置计划任务相比于在 crontab 中只需添加一行任务来说，你需要创建两个文件并运行几次 `systemctl` 命令。 [systemd-crontab-generator](https://aur.archlinux.org/packages/systemd-crontab-generator/) 和 [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/) 可以帮助你使用 crontab 来管理定时器服务。如果你喜欢 crontabs 只是因为它提供了查看所有计划任务的统一视图，`systemctl` 同样可以。参见 [#管理](#.E7.AE.A1.E7.90.86)。
*   邮件：目前还没有内置与 cron `MAILTO` 类似的任务失败时发送邮件的功能。 可以在每个服务文件中配置 `OnFailure=` 实现同样的功能。
*   随机延时：目前没还有内置与 cron 类似的 `RANDOM_DELAY` 功能来指定一个数字用于定时器延时执行。（参见 [bug report](https://bugs.freedesktop.org/show_bug.cgi?id=82084)）。 你不想同时执行的服务必须手动设置它们的定时器。

**注意:** `AccuracySec` 选项对于随机错开定时器执行时间是 **没有** 作用的，因为它"会在所有本地定时器单元间同步" (`systemd.timer(5)`)。换句话说， `AccuracySec` 会以相同的量改变所有定时器激活时间。例如，所有 `OnCalendar=daily` 的定时器单元，指定 `AccuracySec=15m` 将同时在 00:00 到 00:15 触发相关的服务。

### 发送邮件

像 Cron 的 `MAILTO` 一样，也可以配置 systemd 在单元失效时发送一个电子邮件。首先，这需要两个文件：一个可执行文件用来发送邮件；一个 *.service* 文件启动这个可执行文件。在本例中，可执行文件只是一个调用 `sendmail` 的shell 脚本：

 `/usr/local/bin/systemd-email` 
```
#!/bin/bash

/usr/bin/sendmail -t <<ERRMAIL
To: $1
From: systemd <root@$HOSTNAME>
Subject: $2
Content-Transfer-Encoding: 8bit
Content-Type: text/plain; charset=UTF-8

$(systemctl status --full "$2")
ERRMAIL
```

Whatever executable you use, it should probably take at least two arguments as this shell script does: the address to send to and the unit file to get the status of. The *.service* we create will pass these arguments:

 `/etc/systemd/system/status-email-user1@.service` 
```
[Unit]
Description=status email for %I to user1

[Service]
Type=oneshot
ExecStart=/usr/local/bin/systemd-email user1@mailhost %i
User=nobody
Group=systemd-journal

```

First notice that the unit to send email about is an instance parameter, so this one service can be used to send email for many other units. However the recipient is hard-coded (since unit templates can only take a single parameter) so you will need to create multiple services if you want to send emails to different sets of recipients. At this point you should test the service to verify that you can receive the emails:

 `# systemctl start status-email-user1@dbus.service` 

Then simply add `OnFailure=status-email-user1@%n.service` to the `[Unit]` section of any unit you want emails for. `%n` passes the unit's name to the template.

### 使用 crontab

Several of the caveats can be worked around by installing a package that parses a traditional crontab to configure the timers. [systemd-crontab-generator](https://aur.archlinux.org/packages/systemd-crontab-generator/) and [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/) from the [AUR](/index.php/AUR "AUR") are two such packages. These can provide the missing `MAILTO` and `RANDOM_DELAY` features.

If you like crontabs just because they provide a unified view of all scheduled jobs, `systemctl` can provide this. See [#Management](#Management).

## 参见

*   [systemd.timer man page](http://www.freedesktop.org/software/systemd/man/systemd.timer.html) on freedesktop.org
*   [Fedora Project wiki page](https://fedoraproject.org/wiki/Features/SystemdCalendarTimers) on *systemd* calendar timers
*   [Gentoo wiki section](https://wiki.gentoo.org/wiki/Systemd#Timer_services) on *systemd* timer services
*   **systemd-crontab-generator** — 一个从 crontab 和 anacrontab 文件生成 timers/services 文件的工具

	[https://github.com/kstep/systemd-crontab-generator](https://github.com/kstep/systemd-crontab-generator) || [systemd-crontab-generator](https://aur.archlinux.org/packages/systemd-crontab-generator/)

*   **systemd-cron** — 提供 systemd 单元运行 cron 脚本；使用 *systemd-crontab-generator* 转换 crontabs

	[https://github.com/systemd-cron/systemd-cron](https://github.com/systemd-cron/systemd-cron) || [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/)