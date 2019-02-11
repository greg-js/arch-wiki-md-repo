**Важно:** Использование блокировки по IP защитит только от тривиальных атак, но для работы потребуется дополнительный демон и правильно настроенное логирование (раздел /var может переполниться, особенно если злоумышленник целенаправленно ломает сервер). К тому же, если злоумышленники узнают ваш IP адрес, они могут послать пакеты с подменёнными заголовками отправителя и отберут у вас доступ к серверу. [SSH keys](/index.php/SSH_keys "SSH keys") предоставляют элегантное решение проблемы брут форса без перечисленных проблем.

[Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page) сканирует различные текстовые лог-файлы и блокирует IP, которые делают слишком много ошибок ввода пароля, обновляя правила файрвола для отклонения IP-адреса, сходно с [Sshguard](/index.php/Sshguard "Sshguard").

**Важно:** Для корректной работы инструмент должен правильно парсить IP-адреса в лог-файлах. Всегда **проверяйте** лог-фильтры для каждого приложения, требующего защиты.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 systemd](#systemd)
*   [2 Укрепление](#Укрепление)
    *   [2.1 Возможности](#Возможности)
    *   [2.2 Filesystem Access](#Filesystem_Access)
*   [3 SSH jail](#SSH_jail)
*   [4 Смотрите также](#Смотрите_также)

## Установка

Установите [fail2ban](https://www.archlinux.org/packages/?name=fail2ban) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Если вы хотите, чтобы Fail2ban отсылал письма, когда кто-то был забанен, вы должны настроить [SSMTP](/index.php/SSMTP "SSMTP") (к примеру).

### systemd

Используйте юнит сервис `fail2ban.service`, в соответствии с инструкциями [systemd](/index.php/Systemd "Systemd").

## Укрепление

На данный момент fail2ban требует запуска от имени root, следовательно, вы можете дополнительно укрепить процесс с помощью systemd. Ссылка: [systemd for Administrators, Part XII](http://0pointer.de/blog/projects/security.html)

### Возможности

For added security consider limiting fail2ban capabilities by specifying `CapabilityBoundingSet` in the [drop-in configuration file](/index.php/Systemd#Editing_provided_units "Systemd") for the provided `fail2ban.service`:

 `/etc/systemd/system/fail2ban.service.d/capabilities.conf` 
```
[Service]
CapabilityBoundingSet=CAP_DAC_READ_SEARCH CAP_NET_ADMIN CAP_NET_RAW
```

In the example above, `CAP_DAC_READ_SEARCH` will allow fail2ban full read access, and `CAP_NET_ADMIN` and `CAP_NET_RAW` allow setting of firewall rules with [iptables](/index.php/Iptables "Iptables"). Additional capabilities may be required, depending on your fail2ban configuration. See [capabilities(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/capabilities.7) for more info.

### Filesystem Access

Also considering limiting file system read and write access, by using *ReadOnlyDirectories* and *ReadWriteDirectories*, again under the `[Service]` section. For example:

```
ReadOnlyDirectories=/
ReadWriteDirectories=/var/run/fail2ban /var/lib/fail2ban /var/spool/postfix/maildrop /tmp

```

In the example above, this limits the file system to read-only, except for `/var/run/fail2ban` for pid and socket files, and `/var/spool/postfix/maildrop` for [postfix](/index.php/Postfix "Postfix") sendmail. Again, this will be dependent on you system configuration and fail2ban configuration. The `/tmp` directory is needed for some fail2ban actions. Note that adding `/var/log` is necessary if you want fail2ban to log its activity.

## SSH jail

Edit `/etc/fail2ban/jail.conf` and modify the ssh-iptables section to enable it and configure the action.

**Note:** Due to the possibility of the `jail.conf` file being overwritten or improved during a distribution update, it is recommended to provide customizations in a `jail.local` file, or separate *.conf* files under the `jail.d/` directory, e.g. `jail.d/ssh-iptables.conf`.

If your firewall is iptables:

```
[ssh-iptables]
enabled  = true
filter   = sshd
action   = iptables[name=SSH, port=ssh, protocol=tcp]
           sendmail-whois[name=SSH, dest=your@mail.org, sender=fail2ban@mail.com]
logpath  = /var/log/auth.log
maxretry = 5

```

Fail2Ban from version 0.9 can also read directly from the systemd journal by setting `backend = systemd`.

If your firewall is shorewall:

```
[ssh-shorewall]
enabled  = true
filter   = sshd
action   = shorewall
           sendmail-whois[name=SSH, dest=your@mail.org, sender=fail2ban@mail.com]
logpath  = /var/log/auth.log
maxretry = 5

```

**Note:** You can set `BLACKLIST` to `ALL` in `/etc/shorewall/shorewall.conf` otherwise the rule added to ban an IP address will affect only new connections.

Also do not forget to add/change:

```
LogLevel VERBOSE

```

in your `/etc/ssh/sshd_config`. Else, password failures are not logged correctly.

## Смотрите также

*   [sshguard](/index.php/Sshguard "Sshguard")