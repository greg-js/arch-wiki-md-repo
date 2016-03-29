**Состояние перевода:** На этой странице представлен перевод статьи [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Дата последней синхронизации: 24 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd/Timers&diff=0&oldid=427528).

Таймеры это файлы служб [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") имя которых оканчивается на `.timer` они контролируют файлы `.service` или события. Таймеры могут использоваться как альтернатива [cron](/index.php/Cron_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Cron (Русский)") (читайте [#В качестве замены cron](#.D0.92_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D0.B7.D0.B0.D0.BC.D0.B5.D0.BD.D1.8B_cron)). Таймеры имеют встроенную поддержку временных календарных событий, монотонных временных событий, и могут быть запущены в асинхронном режиме.

## Contents

*   [1 Юниты таймера](#.D0.AE.D0.BD.D0.B8.D1.82.D1.8B_.D1.82.D0.B0.D0.B9.D0.BC.D0.B5.D1.80.D0.B0)
*   [2 Служба юнита](#.D0.A1.D0.BB.D1.83.D0.B6.D0.B1.D0.B0_.D1.8E.D0.BD.D0.B8.D1.82.D0.B0)
*   [3 Управление](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
*   [4 Пример](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80)
    *   [4.1 Монотонный таймер](#.D0.9C.D0.BE.D0.BD.D0.BE.D1.82.D0.BE.D0.BD.D0.BD.D1.8B.D0.B9_.D1.82.D0.B0.D0.B9.D0.BC.D0.B5.D1.80)
    *   [4.2 Таймер в реальном времени](#.D0.A2.D0.B0.D0.B9.D0.BC.D0.B5.D1.80_.D0.B2_.D1.80.D0.B5.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.B8)
*   [5 В качестве замены cron](#.D0.92_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D0.B7.D0.B0.D0.BC.D0.B5.D0.BD.D1.8B_cron)
    *   [5.1 Полезности](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.2 Предостережения](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B5.D1.80.D0.B5.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [5.3 MAILTO](#MAILTO)
    *   [5.4 Использование crontab](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_crontab)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Юниты таймера

Таймеры *systemd* это файлы юнитов с суфиксом `.timer`. Таймеры, как и другие файлы [файлы настроек юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") и загружаются по одному и тому же пути, но включают в себя секцию `[Timer]`. Секция `[Timer]` определяет, когда и как таймер активизируется. Таймеры определяются в качестве одного из двух типов:

*   **Монотонный таймер** активируется после определенного промежутка времени по отношению к той или иной отправной точки. Есть несколько различных монотонных таймеров, но все они имеют вид: `On*Type*Sec=`. `OnBootSec` и `OnActiveSec` являются общими монотонными таймерами.
*   **Таймер реального времени** (также известный как таймер настенный часы) активируется на события календаря (как cronjobs). Для их определения используется опция `OnCalendar=`.

Для полного объяснения опций таймера смотрите `systemd.timer(5)` [странице справочного руководства](/index.php/%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0_%D1%81%D0%BF%D1%80%D0%B0%D0%B2%D0%BE%D1%87%D0%BD%D0%BE%D0%B3%D0%BE_%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%B0 "Страница справочного руководства"). Синтаксис аргументов для событий календаря и промежутка времени определяется на `systemd.time(7)` [странице справочного руководства](/index.php/%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0_%D1%81%D0%BF%D1%80%D0%B0%D0%B2%D0%BE%D1%87%D0%BD%D0%BE%D0%B3%D0%BE_%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%B0 "Страница справочного руководства").

## Служба юнита

For each `.timer` file, a matching `.service` file exists (e.g. `foo.timer` and `foo.service`). The `.timer` file activates and controls the `.service` file. The `.service` does not require an `[Install]` section as it is the *timer* units that are enabled. If necessary, it is possible to control a differently-named unit using the `Unit=` option in the timer's `[Timer]` section.

## Управление

To use a *timer* unit [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") it like any other unit (remember to add the `.timer` suffix). To view all started timers, run:

 `$ systemctl list-timers` 
```
NEXT                          LEFT        LAST                          PASSED     UNIT                         ACTIVATES
Thu 2014-07-10 19:37:03 CEST  11h left    Wed 2014-07-09 19:37:03 CEST  12h ago    systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
Fri 2014-07-11 00:00:00 CEST  15h left    Thu 2014-07-10 00:00:13 CEST  8h ago     logrotate.timer              logrotate.service

```

**Примечание:**

*   To list all timers (including inactive), use `systemctl list-timers --all`.
*   The status of a service started by a timer will likely be inactive unless it is currently being triggered.
*   If a timer gets out of sync, it may help to delete its `stamp-*` file in `/var/lib/systemd/timers`. These are zero length files which mark the last time each timer was run. If deleted, they will be reconstructed on the next start of their timer.

## Пример

No changes to service unit files are needed to schedule them with a timer. The following example schedules `foo.service` to be run with a corresponding timer called `foo.timer`.

### Монотонный таймер

A timer which will start 15 minutes after boot and again every week while the system is running.

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

### Таймер в реальном времени

A timer which starts once a week (at 12:00am on Monday). It starts once immediately if it missed the last start time (option `Persistent=true`), for example due to the system being powered off:

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

**Совет:** Special event expressions like `daily` and `weekly` refer to *specific start times* and thus any timers sharing such calendar events will start simultaneously. Timers sharing start events can cause poor system performance if the timers' services compete for system resources. The `RandomizedDelaySec` option avoids this problem by randomly staggering the start time of each timer. See `systemd.timer (5)`.

## В качестве замены cron

Although [cron](/index.php/Cron "Cron") is arguably the most well-known job scheduler, *systemd* timers can be an alternative.

### Полезности

The main benefits of using timers come from each job having its own *systemd* service. Some of these benefits are:

*   Jobs can be easily started independently of their timers. This simplifies debugging.
*   Each job can be configured to run in a specific environment (see the `systemd.exec(5)` [man page](/index.php/Man_page "Man page")).
*   Jobs can be attached to [cgroups](/index.php/Cgroups "Cgroups").
*   Jobs can be set up to depend on other *systemd* units.
*   Jobs are logged in the *systemd* journal for easy debugging.

### Предостережения

Some things that are easy to do with cron are difficult to do with timer units alone.

*   Complexity: to set up a timed job with *systemd* you create two files and run a couple `systemctl` commands. Compare that to adding a single line to a crontab.
*   Emails: there is no built-in equivalent to cron's `MAILTO` for sending emails on job failure. See the next section for an example of setting up an equivalent using `OnFailure=`.

### MAILTO

You can set up systemd to send an e-mail when a unit fails - much like Cron does with `MAILTO`. First you need two files: an executable for sending the mail and a *.service* for starting the executable. For this example, the executable is just a shell script using `sendmail`:

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

 `/etc/systemd/system/status-email-**user1**@.service` 
```
[Unit]
Description=status email for %I to **user1**

[Service]
Type=oneshot
ExecStart=/usr/local/bin/systemd-email **user1@mailhost** %i
User=nobody
Group=systemd-journal

```

First notice that the unit to send email about is an instance parameter, so this one service can be used to send email for many other units. However the recipient is hard-coded (since unit templates can only take a single parameter) so you will need to create multiple services if you want to send emails to different sets of recipients. At this point you should test the service to verify that you can receive the emails:

 `# systemctl start status-email-user1@dbus.service` 

Then simply [edit](/index.php/Systemd#Editing_provided_units "Systemd") the service you want emails for and add `OnFailure=status-email-user1@%n.service` to the `[Unit]` section. `%n` passes the unit's name to the template.

**Примечание:** If you set up SSMTP security according to [SSMTP#Security](/index.php/SSMTP#Security "SSMTP") the user `nobody` will not have access to `/etc/ssmtp/ssmtp.conf`, and the `systemctl start status-email-user1@dbus.service` command will fail. One solution is to use `root` as the User in the `status-email-user1@.service` module.

### Использование crontab

Several of the caveats can be worked around by installing a package that parses a traditional crontab to configure the timers. [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/) and [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/) are two such packages. These can provide the missing `MAILTO` feature.

If you like crontabs just because they provide a unified view of all scheduled jobs, `systemctl` can provide this. See [#Management](#Management).

## Смотрите также

*   [systemd.timer man page](http://www.freedesktop.org/software/systemd/man/systemd.timer.html) на freedesktop.org (Англ.)
*   [Fedora Project wiki page](https://fedoraproject.org/wiki/Features/SystemdCalendarTimers) on *systemd* calendar timers (Англ.)
*   [Раздел Gentoo wiki](https://wiki.gentoo.org/wiki/Systemd/ru#.D0.A1.D0.B5.D1.80.D0.B2.D0.B8.D1.81.D1.8B_.D1.82.D0.B0.D0.B9.D0.BC.D0.B5.D1.80.D0.BE.D0.B2) Сервисы таймеров *systemd*
*   **systemd-cron-next** — утилита для создания таймеров/служб из файлов crontab и anacrontab

	[https://github.com/kstep/systemd-cron-next](https://github.com/kstep/systemd-cron-next) || [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/)

*   **systemd-cron** — предоставляет юнитам systemd запускать скрипты cron; используя *systemd-crontab-generator* для конвертации crontab'ов

	[https://github.com/systemd-cron/systemd-cron](https://github.com/systemd-cron/systemd-cron) || [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/)