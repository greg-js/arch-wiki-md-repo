**Состояние перевода:** На этой странице представлен перевод статьи [systemd/Journal](/index.php/Systemd/Journal "Systemd/Journal"). Дата последней синхронизации: 7 февраля 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd/Journal&diff=0&oldid=565517).

*Основная статья: [systemd](/index.php/Systemd "Systemd").*

*systemd* имеет собственную систему ведения логов, названную журналом (journal). В связи с этим больше не требуется запускать демон `syslog`. Для чтения логов используйте команду:

```
# journalctl

```

В Arch Linux каталог `/var/log/journal/` является частью пакета [systemd](https://www.archlinux.org/packages/?name=systemd), и по умолчанию (когда в конфигурационном файле `/etc/systemd/journald.conf` параметр `Storage=` имеет значение `auto`) журнал записывается именно в `/var/log/journal/`. Если вы или какая-то программа удалит этот каталог, *systemd* **не** пересоздаст его автоматически и вместо этого будет писать свои журналы по непостоянному пути `/run/systemd/journal`. Однако каталог будет создан заново, когда вы установите `Storage=persistent` и выполните `systemctl restart systemd-journald` (или перезагрузитесь).

Сообщения в журнале классифицируются по приоритету и категориям (Facility). Классификация записей соответствует классическому протоколу [Syslog](https://en.wikipedia.org/wiki/Syslog "wikipedia:Syslog") ([RFC 5424](https://tools.ietf.org/html/rfc5424)).

## Contents

*   [1 Уровни приоритета](#Уровни_приоритета)
*   [2 Категории](#Категории)
*   [3 Фильтрация вывода](#Фильтрация_вывода)
*   [4 Ограничение размера журнала](#Ограничение_размера_журнала)
*   [5 Очистка файлов журнала вручную](#Очистка_файлов_журнала_вручную)
*   [6 Journald в связке с классическим демоном syslog](#Journald_в_связке_с_классическим_демоном_syslog)
*   [7 Перенаправление журнала на /dev/tty12](#Перенаправление_журнала_на_/dev/tty12)
*   [8 Выбор журнала для просмотра](#Выбор_журнала_для_просмотра)

## Уровни приоритета

Коды уровни важности сообщений syslog (в systemd называются приоритетами) используются для пометки важности сообщений [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Значение | Важность | Ключевое слово | Описание | Примеры |
| 0 | Emergency | emerg | System is unusable | Severe Kernel BUG, [systemd dumped core](/index.php/Systemd-coredump "Systemd-coredump").
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

## Категории

Коды категорий (facility) syslog используются для указания типа программы, добавляющего сообщение в лог [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Код категории | Ключевое слово | Описание | Информация |
| 0 | kern | kernel messages |
| 1 | user | user-level messages |
| 2 | mail | mail system | Archaic POSIX still supported and sometimes used (for more [mail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mail.1)) |
| 3 | daemon | system daemons | All daemons, including systemd and its subsystems |
| 4 | auth | security/authorization messages | Also watch for different facility 10 |
| 5 | syslog | messages generated internally by syslogd | For syslogd implementations (not used by systemd, see facility 3) |
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

Полезные категории для наблюдения: 0,1,3,4,9,10,15.

## Фильтрация вывода

*journalctl* позволяет фильтровать вывод по указанным полям. Помните, что, если должно быть отражено большое количество сообщений или необходима фильтрация в большом промежутке времени, то вывод этой команды может быть отложен на какое-то время.

**Совет:** Несмотря на то, что журнал хранится в двоичном формате, сообщения в нём хранятся без изменений. Это означает, что их можно просматривать при помощи *strings*, например, в окружении, в котором не установлен *systemd*. Пример команды: `$ strings /mnt/arch/var/log/journal/af4967d77fba44c6b093d0e9862f6ddd/system.journal | grep -i *сообщение*` 

Примеры:

*   Показать все сообщения с момента текущей загрузки системы: `# journalctl -b` Однако, пользователи часто интересуются сообщениями не для текущей, а для предыдущей загрузки (например, если произошел невосстановимый сбой системы). Это возможно, если задать параметр флагу `-b`: `journalctl -b -0` покажет сообщения с момента текущей загрузки, `journalctl -b -1` - предыдущей загрузки, `journalctl -b -2` - следующей за предыдущей, и т.д. Для просмотра полного описания смотрите страницу справочного руководства [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1): имеется гораздо более мощная семантика.
*   Показать все сообщения, начиная с какой-либо даты (и, если хотите, времени): `# journalctl --since="2012-10-30 18:17:16"` 
*   Показать все сообщения за последние 20 минут: `# journalctl --since "20 min ago"` 
*   Следить за появлением новых сообщений: `# journalctl -f` 
*   Показать все сообщения для конкретного исполняемого файла: `# journalctl /usr/lib/systemd/systemd` 
*   Показать все сообщения для конкретного процесса: `# journalctl _PID=1` 
*   Показать все сообщения для конкретного юнита: `# journalctl -u netcfg` 
*   Показать кольцевой буфер ядра: `# journalctl -k` 
*   Показать только сообщения с приоритетом error, critical и alert: `# journalctl -p err..alert` Числа тоже можно использовать: `journalctl -p 3..1`. Если указать одно ключевое слово/число: `journalctl -p 3` — все сообщения с более высоким приоритетом также будут показаны.
*   Показать auth.log эквивалентно фильтрации syslog facility: `# journalctl -f -l SYSLOG_FACILITY=10` 
*   Если в вашем каталоге с журналами (по умолчанию `/var/log/journal`) очень много данных, `journalctl` может заниматься фильтрацией вывода несколько минут. Это можно ускорить с помощью опции `--file`, попросив `journalctl` работать только с самым свежим журналом: `# journalctl --file /var/log/journal/*/system.journal -f` 

Для получения дополнительной информации смотрите страницы справочного руководства [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) и [systemd.journal-fields(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7) или [пост в блоге](http://0pointer.de/blog/projects/journalctl.html) Lennart'а.

**Совет:** По умолчанию *journalctl* отсекает части строк, которые не вписываются в экран по ширине, но иногда перенос строк предпочтительнее их отсечения. Управление этой возможностью производится посредством [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `SYSTEMD_LESS`, в которой содержатся опции, передаваемые в [less](/index.php/%D0%91%D0%B0%D0%B7%D0%BE%D0%B2%D1%8B%D0%B5_%D1%83%D1%82%D0%B8%D0%BB%D0%B8%D1%82%D1%8B#less "Базовые утилиты") (программа постраничного просмотра, используемая по умолчанию). По умолчанию ей присвоены опции `FRSXMK` (для получения дополнительной информации смотрите [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) и [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1)).

Если убрать опцию `S`, будет достигнут требуемый результат. Например, запустите *journalctl*, как показано здесь:

```
$ SYSTEMD_LESS=FRXMK journalctl

```
Если вы хотите, чтобы такое поведение использовалось по умолчанию, [экспортируйте](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#На_уровне_пользователя "Environment variables (Русский)") переменную из файла `~/.bashrc` или `~/.zshrc`

## Ограничение размера журнала

Если журнал сохраняется при перезагрузке, его размер по умолчанию ограничен значением в 10% от объема соответствующей файловой системы. Например, для каталога `/var/log/journal`, расположенной на корневом разделе в 20 ГиБ, максимальный размер журналируемых данных составит 2 ГиБ. Максимальный объем постоянного журнала можно контролировать опцией `SystemMaxUse` в конфигурационном файле `/etc/systemd/journald.conf`, поэтому для ограничения его объемом, например, в 50 МиБ раскомментируйте и отредактируйте соответствующую строку:

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

Перезапустите `systemd-journald.service` для применения изменений.

Для получения дополнительной информации обратитесь к странице справочного руководства [journald.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5).

## Очистка файлов журнала вручную

Файлы журнала находятся в `/var/log/journal` и могут быть удалены, к примеру, обычной командой `rm`. Также можно использовать `journalctl` для удаления части журналов по определённым критериям. Например:

*   Remove archived journal files until the disk space they use falls below 100M: `# journalctl --vacuum-size=100M` 
*   Make all journal files contain no data older than 2 weeks. `# journalctl --vacuum-time=2weeks` 

Для получения дополнительной информации, обратитесь к [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1).

## Journald в связке с классическим демоном syslog

Совместимость с классической реализацией non-journald aware [syslog](/index.php/Syslog-ng "Syslog-ng") можно обеспечить, заставив *systemd* направлять все сообщения через сокет `/run/systemd/journal/syslog`. Чтобы дать возможность демону syslog работать вместе с журналом *systemd*, следует привязать данный демон к указанному сокету вместо `/dev/log` ([официальное сообщение](http://lwn.net/Articles/474968/)). Пакетом [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) из репозиториев автоматически предоставляется необходимая конфигурация.

Начиная с версии systemd 216, по умолчанию `journald.conf` для передачи данных в сокет был изменён на `ForwardToSyslog=no`, чтобы избежать нагрузки на систему, потому что [rsyslog](/index.php/Rsyslog "Rsyslog") или [syslog-ng](/index.php/Syslog-ng "Syslog-ng") (начиная с версии 3.6) получают сообщения из журнала [самостоятельно](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

Смотрите [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") и [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng"), или соответственно [rsyslog](/index.php/Rsyslog "Rsyslog") для подробной информации о конфигурировании.

Если взамен вы используете [rsyslog](https://aur.archlinux.org/packages/rsyslog/), нет необходимости менять эту настройку, поскольку [rsyslog](/index.php/Rsyslog "Rsyslog") забирает сообщения из журнала [самостоятельно](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

## Перенаправление журнала на /dev/tty12

Создайте [drop-in каталог](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Редактирование_предоставленных_пакетами_файлов_юнитов "Systemd (Русский)") `/etc/systemd/journald.conf.d` и файл в нём `fw-tty12.conf` с содержимым:

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

Затем [перезапустите](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_юнитов "Systemd (Русский)") `systemd-journald`.

## Выбор журнала для просмотра

Если появилась необходимость проверить логи другой системы, которая неисправна, загрузитесь с работоспособной системы, чтобы восстановить неисправную систему. Примонтируйте диск неисправной системы, например в `/mnt` и укажите путь журнала через `-D`/`--directory`, например так:

```
$ journalctl -D */mnt*/var/log/journal -xe

```