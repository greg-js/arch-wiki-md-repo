**Состояние перевода:** На этой странице представлен перевод статьи [OpenRC](/index.php/OpenRC "OpenRC"). Дата последней синхронизации: 3 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=OpenRC&diff=0&oldid=418899).

**Важно:** Arch Linux официально поддерживает только [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). При обращении за поддержкой, пожалуйста, укажите, что пользуетесь OpenRC

[OpenRC](https://wiki.gentoo.org/wiki/OpenRC) - менеджер служб, поддерживаемый разработчиками Gentoo. Это система инициализации на основе зависимостей, которая работает вместе с программой инициализации [SysVinit](/index.php/SysVinit "SysVinit").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Загрузка](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Подготовка](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.2 Службы](#.D0.A1.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
    *   [2.3 Сеть](#.D0.A1.D0.B5.D1.82.D1.8C)
    *   [2.4 Логи загрузки](#.D0.9B.D0.BE.D0.B3.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [2.5 Имя хоста (Hostname)](#.D0.98.D0.BC.D1.8F_.D1.85.D0.BE.D1.81.D1.82.D0.B0_.28Hostname.29)
    *   [2.6 Модули ядра](#.D0.9C.D0.BE.D0.B4.D1.83.D0.BB.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [2.7 Локаль](#.D0.9B.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Ошибка при размонтировании /tmp](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8_.D1.80.D0.B0.D0.B7.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.2Ftmp)
    *   [3.2 Не работает отключение IPv6](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_IPv6)
    *   [3.3 Во время выключения, и перемонтирования раздела root, происходят ошибки чтения](#.D0.92.D0.BE_.D0.B2.D1.80.D0.B5.D0.BC.D1.8F_.D0.B2.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F.2C_.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0_root.2C_.D0.BF.D1.80.D0.BE.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D1.8F.D1.82_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B8_.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.4 Не найден /etc/sysctl.conf](#.D0.9D.D0.B5_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD_.2Fetc.2Fsysctl.conf)
*   [4 Использование OpenRC с окружением рабочего стола (DE)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_OpenRC_.D1.81_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0_.28DE.29)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

OpenRC и сопутствующие пакеты доступны в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Для получения подробной информации о компонентах инициализации смотрите [Init](/index.php/Init "Init").

Установите пакет [openrc](https://aur.archlinux.org/packages/openrc/) или [openrc-git](https://aur.archlinux.org/packages/openrc-git/). В качестве init процесса используется [openrc-sysvinit](https://aur.archlinux.org/packages/openrc-sysvinit/) или [busybox](https://www.archlinux.org/packages/?name=busybox). Файлы сервисов содержатся в пакете [openrc-arch-services-git](https://aur.archlinux.org/packages/openrc-arch-services-git/).

Для поддержки совместимости с [initscripts-fork](https://aur.archlinux.org/packages/initscripts-fork/), файлы настроек будут установлены в `**/etc/openrc/**`. Бинарный sysvinit init устанавливается в `/usr/bin/init-openrc` для совместимости с [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) или подобных пакетов.

### Загрузка

Для загрузки с OpenRC, добавьте `init=/usr/bin/init-openrc` в [параметры ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)"). Чтобы вернуться к systemd, удалите этот параметр ядра.

Каталог `/etc/openrc/conf.d`, и файл `/etc/openrc/rc.d` используются для настройки.

## Настройка

Для получения общей информации о настройке OpenRC смотрите:

*   [руководство OpenRC (Англ.)](http://www.calculate-linux.org/main/en/openrc_manuals)
*   [миграция на OpenRC (Англ.)](http://www.gentoo.org/doc/en/openrc-migration.xml)
*   [gentoo wiki](http://wiki.gentoo.org/wiki/OpenRC).

### Подготовка

Смотрите [Init#Configuration](/index.php/Init#Configuration "Init").

### Службы

Службы OpenRC включаются от имени суперпользователя (root) используя `rc-update add *имя службы* *runlevel*`. По крайней мере рекомендуется включить следующие службы:

| Имя службы | [Runlevel](https://wiki.gentoo.org/wiki/OpenRC#Named_runlevels) | Описание |
| udev | sysinit | Устройство горячего подключения |
| alsa | default | [ALSA](/index.php/ALSA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ALSA (Русский)") state |
| acpid | default | ACPI events |
| dbus | default | Шина сообщений |
| dcron | default | Планировщик |
| syslog-ng | default | Системные журналы (логи) |

Смотрите также [Native services](https://wiki.gentoo.org/wiki/Systemd#Native_services) и [демоны](/index.php/Daemons_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemons (Русский)").

### Сеть

Для общей информации по сети смотрите [Network configuration](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)").

Сеть настраивается с помощью `newnet`. [[1]](https://github.com/funtoo/openrc/blob/master/README.newnet) Измените файл `/etc/openrc/conf.d/network`; поддерживаются обе команды `ip` ([iproute2](https://www.archlinux.org/packages/?name=iproute2)) и `ifconfig` ([net-tools](https://www.archlinux.org/packages/?name=net-tools)). Ниже приведён пример с использованием `ip`.

```
ip_eth0="192.168.1.2/24"
defaultiproute="via 192.168.1.1"
ifup_eth0="ip link set \$int mtu 1500"

```

Сетевой сервис добавляется в загрузочный уровень по умолчанию, так что дальнейшие действия не требуются.

**Note:** Вы также можете воспользоваться [NetworkManager](/index.php/NetworkManager "NetworkManager"), [dhcpcd](/index.php/Dhcpcd "Dhcpcd") или [netcfg](https://aur.archlinux.org/packages/netcfg/) включая соответствующие сервисы. [netcfg](https://aur.archlinux.org/packages/netcfg/) имитирует поведение [netctl](/index.php/Netctl "Netctl") (смотрите [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1489283#p1489283) если вы хотите включать профили соединения при загрузке - требующие `wpa_actiond`). Вы можете проконсультироваться с [официальной документацией](https://www.archlinux.org/netcfg/features.html) или [старой wiki документацией](https://wiki.archlinux.org/index.php?title=Netcfg&oldid=243178) (последняя версия [2012-05-13](https://www.archlinux.org/news/netcfg-282-release/))

### Логи загрузки

Чтобы включить ведение журнала загрузки, раскомментируйте строку `rc_logger="YES"` в `/etc/openrc/rc.conf`. Когда он включен, журналы загрузки хранятся в `/var/log/rc.log`

### Имя хоста (Hostname)

OpenRC устанавливает имя хоста из `/etc/openrc/conf.d/hostname`. Файл выглядит следующим образом:

```
# Set to the hostname of this machine
hostname="myhostname"
```

### Модули ядра

OpenRC использует `/etc/openrc/conf.d/modules` вместо `/etc/modules-load.d`. Например:

 `/etc/openrc/conf.d/modules` 
```
# Вы должны ознакомится с настройками и документацией вашего ядра
# для списка модулей и их параметров.

modules="vboxdrv acpi_cpufreq"
```

### Локаль

Раскладка клавиатуры настраивается с помощью `/etc/openrc/conf.d/keymaps` и `/etc/openrc/conf.d/consolefont`. Вы также можете настроить параметры через файл `/etc/locale.conf`, который получается с помощью `/etc/profile.d/locale.sh`.

Смотрите [[3]](http://wiki.gentoo.org/wiki/Localization/HOWTO#Keyboard_layout_for_the_console) и [Locale](/index.php/Locale "Locale") для подробностей.

## Решение проблем

### Ошибка при размонтировании /tmp

При выключении системы, вы можете получить сообщение об ошибке, например:

```
* Unmounting /tmp ... 
* in use but fuser finds nothing [ !! ]
```

Это можно исправить путем добавления

```
no_umounts="/tmp"

```

в `/etc/openrc/conf.d/localmount`

**Примечание:** Эта проблема проявляется только если ваш tmp примонтирован как tmpfs.

### Не работает отключение IPv6

Одним из вариантов является добавление:

```
# Disable ipv6
net.ipv6.conf.all.disable_ipv6 = 1

```

в файле с расширением `.conf` в `/etc/openrc/sysctl.d`

### Во время выключения, и перемонтирования раздела root, происходят ошибки чтения

Если такое происходит, отредактируйте файл `/etc/openrc/init.d/mount-ro` и поместите:

```
telinit u

```

после следующей строки:

```
# Flush all pending disk writes now
sync; sync

```

### Не найден /etc/sysctl.conf

По умолчанию, `sysctl --system` вызывается для загрузки настройки sysctl. [[4]](https://github.com/OpenRC/openrc/blob/master/init.d/sysctl.Linux.in#L17) Он содержит файл `/etc/sysctl.conf`, который удалён в Arch. [[5]](https://www.archlinux.org/news/deprecation-of-etcsysctlconf/)

Чтобы предотвратить ошибку "файл не найден", создайте файл:

```
# touch /etc/sysctl.conf

```

## Использование OpenRC с окружением рабочего стола (DE)

Если используется *OpenRC* с [окружением рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"), может помочь ConsoleKit. Установите [сервис](https://gist.github.com/ad73f9087f39d7cadd8e) в `/etc/openrc/init.d`, и включите его:

```
# rc-update add consolekit default

```

Для большей информации смотрите [ConsoleKit](/index.php/ConsoleKit "ConsoleKit").

## Смотрите также

*   [Реально ли установить и пользоваться Arch без systemd?](http://archlinux.org.ru/forum/post/156161/)
*   [Wikipedia OpenRC](https://en.wikipedia.org/wiki/ru:OpenRC "wikipedia:ru:OpenRC")
*   [Gentoo wiki](https://wiki.gentoo.org/wiki/OpenRC)
*   [OpenRC for Arch Linux - sourceforge repository](https://sourceforge.net/projects/archopenrc)
*   [Forum thread about OpenRC in Arch](https://bbs.archlinux.org/viewtopic.php?id=152606)
*   [Blog: OpenRC on Arch Linux](http://blog.notfoss.com/posts/openrc-on-arch-linux/)
*   [Manjaro wiki](https://wiki.manjaro.org/index.php?title=OpenRC,_an_alternative_to_systemd)