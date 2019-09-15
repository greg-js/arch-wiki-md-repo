**Состояние перевода:** На этой странице представлен перевод статьи [Fail2ban](/index.php/Fail2ban "Fail2ban"). Дата последней синхронизации: 6 июня 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Fail2ban&diff=0&oldid=574713).

[Fail2ban](https://www.fail2ban.org/wiki/index.php/Main_Page) сканирует лог-файлы (например, `/var/log/httpd/error_log`) и блокирует IP-адреса, которые ведут себя подозрительно, к примеру, делая слишком много попыток входа с неверным паролем в попытках найти уязвимости и т.п. Обычно Fail2ban используется для обновления правил с целью блокировки IP-адресов на определённое время, но можно настроить и другие действия — например, отправку письма по электронной почте.

**Важно:** Использование блокировки по IP защитит только от простейших атак, но для работы потребуется дополнительный демон и правильно настроенное журналирование. К тому же злоумышленники, знающие ваш IP-адрес, могут послать пакеты с подменёнными заголовками отправителя и лишить вас доступа к серверу. Не забудьте прописать собственные IP-адреса в `ignoreip`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
    *   [2.1 fail2ban-client](#fail2ban-client)
*   [3 Настройка](#Настройка)
    *   [3.1 Включение "клеток"](#Включение_"клеток")
    *   [3.2 Почтовые уведомления](#Почтовые_уведомления)
    *   [3.3 Межсетевой экран и службы](#Межсетевой_экран_и_службы)
*   [4 Советы и рекомендации](#Советы_и_рекомендации)
    *   [4.1 Пользовательская "клетка" SSH](#Пользовательская_"клетка"_SSH)
    *   [4.2 Защита службы](#Защита_службы)
*   [5 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [fail2ban](https://www.archlinux.org/packages/?name=fail2ban).

## Использование

[Настройте](#Настройка) Fail2ban, после чего [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `fail2ban.service`.

### fail2ban-client

Утилита fail2ban-client позволяет мониторить "клетки" (jails) (reload, restart, status и т.д.). Чтобы увидеть список всех доступных команд, введите:

```
$ fail2ban-client

```

Просмотр включённых "клеток" (jails):

```
# fail2ban-client status

```

Проверка статуса "клетки" на примере таковой для *sshd*:

 `# fail2ban-client status sshd` 
```
Status for the jail: sshd
|- Filter
|  |- Currently failed: 1
|  |- Total failed:     9
|  `- Journal matches:  _SYSTEMD_UNIT=sshd.service + _COMM=sshd
`- Actions
   |- Currently banned: 1
   |- Total banned:     1
   `- Banned IP list:   0.0.0.0

```

## Настройка

Рекомендуется [создать](/index.php/%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D1%82%D1%8C "Создать") файл `/etc/fail2ban/jail.local`, так как `/etc/fail2ban/jail.conf` может быть перезаписан во время обновления системы. К примеру, задать время блокировки в 1 день можно следующим образом:

 `/etc/fail2ban/jail.local` 
```
[DEFAULT]
bantime = 1d

```

Также можно создавать отдельные файлы *name.local* в каталоге `/etc/fail2ban/jail.d`, например, `/etc/fail2ban/jail.d/sshd.local`.

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `fail2ban.service` для применения изменений.

### Включение "клеток"

По умолчанию все "клетки" отключены. [Добавьте](/index.php/%D0%94%D0%BE%D0%B1%D0%B0%D0%B2%D1%8C%D1%82%D0%B5 "Добавьте") строку `enabled = true` к конфигурации той "клетки", которую необходимо включить. Например, включение "клетки" [OpenSSH (Русский)](/index.php/OpenSSH_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "OpenSSH (Русский)") выглядит следующим образом:

 `/etc/fail2ban/jail.local` 
```
[sshd]
enabled = true
```

См. [#Пользовательская "клетка" SSH](#Пользовательская_"клетка"_SSH).

### Почтовые уведомления

Для получения электронных писем при блокировке IP-адресов следует настроить SMTP-клиент (например, [msmtp](/index.php/Msmtp "Msmtp")) и изменить действие по умолчанию:

 `/etc/fail2ban/jail.local` 
```
[DEFAULT]
destemail = вашеимя@example.com
sender = вашеимя@example.com

# для блокировки и отправки электронного письма на destemail с whois-отчётом
action = %(action_mw)s

# то же, что и action_mw, но включает в себя ещё и связанные строки из лога
#action = %(action_mwl)s

```

### Межсетевой экран и службы

Большинство и служб должны работать по умолчанию. См. содержимое директории `/etc/fail2ban/action.d/` для получения примеров, например, [ufw.conf](https://github.com/fail2ban/fail2ban/blob/master/config/action.d/ufw.conf).

## Советы и рекомендации

### Пользовательская "клетка" SSH

**Важно:** Зная ваш IP-адрес, злоумышленник может послать пакеты с подменёнными заголовками отправителя, тем самым лишив вас доступа к серверу. [Ключи SSH](/index.php/%D0%9A%D0%BB%D1%8E%D1%87%D0%B8_SSH "Ключи SSH") предоставляют отличное решение проблемы брутфорса без подобных последствий.

Отредактируйте файл `/etc/fail2ban/jail.d/sshd.local`, добавив эту секцию и обновив список доверенных IP-адресов в `ignoreip`:

 `/etc/fail2ban/jail.d/sshd.local` 
```
[sshd]
enabled   = true
filter    = sshd
banaction = iptables
backend   = systemd
maxretry  = 5
findtime  = 1d
bantime   = 2w
ignoreip  = 127.0.0.1/8
```

**Примечание:**

*   Может понадобиться задать `LogLevel VERBOSE` в файле `/etc/ssh/sshd_config`, чтобы разрешить Fail2ban полноценный мониторинг. В противном случае, ошибки ввода пароля могут быть неправильно зарегистрированы.
*   Fail2ban поддерживает IPv6 с версии 0.10\. Настройте [межсетевой экран](/index.php/%D0%9C%D0%B5%D0%B6%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B9_%D1%8D%D0%BA%D1%80%D0%B0%D0%BD "Межсетевой экран") соответственно, например, [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `ip6tables.service`.

**Совет:**

*   При использовании фронтендов [iptables (Русский)](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)"), например, [ufw](/index.php/Ufw "Ufw"), можно использовать `banaction = ufw` вместо iptables.
*   При использовании [Shorewall](/index.php/Shorewall "Shorewall") можно прописать `banaction = shorewall` и также задать значение `ALL` параметру `BLACKLIST` в файле `/etc/shorewall/shorewall.conf`. В противном случае, правила, добавленные для блокировки IP-адреса, будут влиять только на новые соединения.

### Защита службы

Поскольку Fail2ban следует запускать от имени *суперпользователя*, дополнительно защитить службу можно с помощью [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)").

[Создайте](/index.php/%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%B9%D1%82%D0%B5 "Создайте") конфигурационный [drop-in файл](/index.php/Drop-in_%D1%84%D0%B0%D0%B9%D0%BB "Drop-in файл") для службы `fail2ban.service`:

 `/etc/systemd/system/fail2ban.service.d/override.conf` 
```
[Service]
PrivateDevices=yes
PrivateTmp=yes
ProtectHome=read-only
ProtectSystem=strict
NoNewPrivileges=yes
ReadWritePaths=-/var/run/fail2ban
ReadWritePaths=-/var/lib/fail2ban
ReadWritePaths=-/var/log/fail2ban
ReadWritePaths=-/var/spool/postfix/maildrop
CapabilityBoundingSet=CAP_AUDIT_READ CAP_DAC_READ_SEARCH CAP_NET_ADMIN CAP_NET_RAW
```

Параметр `CAP_DAC_READ_SEARCH` (в строке `CapabilityBoundingSet`) позволяет Fail2ban читать любые файлы и каталоги, а `CAP_NET_ADMIN` и `CAP_NET_RAW` позволяют задавать правила межсетевого экрана посредством [iptables (Русский)](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") или [nftables](/index.php/Nftables "Nftables"). Подробнее см. [capabilities(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/capabilities.7).

При использовании параметра `ProtectSystem=strict` иерархия [файловой системы](/index.php/File_systems_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "File systems (Русский)") будет доступна только для чтения, а `ReadWritePaths` позволит Fail2ban также вести запись в заданные каталоги.

От имени суперпользователя создайте каталог `/var/log/fail2ban` и пропишите в файл `/etc/fail2ban/fail2ban.local` корректный путь `logtarget`:

 `/etc/fail2ban/fail2ban.local` 
```
[Definition]
logtarget = /var/log/fail2ban/fail2ban.log

```

Для применения изменений в файлах юнитов [перезагрузите демон systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_юнитов "Systemd (Русский)") и [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `fail2ban.service`.

## Смотрите также

*   [Using a Fail2Ban Jail to Whitelist a User](https://www.the-art-of-web.com/system/fail2ban-action-whitelist/)
*   [Optimising your Fail2Ban filters](https://www.the-art-of-web.com/system/fail2ban-filters/)
*   [Fail2Ban and sendmail](https://www.the-art-of-web.com/system/fail2ban-sendmail/)
*   [Fail2Ban and iptables](https://www.the-art-of-web.com/system/fail2ban/)
*   [Fail2Ban 0.8.3 Howto](https://www.the-art-of-web.com/system/fail2ban-howto/)
*   [Monitoring the fail2ban log](https://www.the-art-of-web.com/system/fail2ban-log/)