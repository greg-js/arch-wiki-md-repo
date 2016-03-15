Группы пользователей используются в GNU/Linux для [контроля доступа](https://en.wikipedia.org/wiki/Access_control#Computer_security "wikipedia:Access control") – члены групп имеют доступ к устройствам и файлам, принадлежащим этим группам. `/etc/group` – файл, описывающий и определяющий все группы в системе (см. `man group` для подробностей).

Данная статья предоставляет список основных групп и их назначений, а также команды для управления группами.

## Contents

*   [1 Полезные группы](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D1.8B)
*   [2 Group list](#Group_list)
*   [3 Манипуляция группами](#.D0.9C.D0.B0.D0.BD.D0.B8.D0.BF.D1.83.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B0.D0.BC.D0.B8)
    *   [3.1 Листинг групп](#.D0.9B.D0.B8.D1.81.D1.82.D0.B8.D0.BD.D0.B3_.D0.B3.D1.80.D1.83.D0.BF.D0.BF)
    *   [3.2 Поиск объектов, принадлежащих определённой группе](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.BE.D0.B1.D1.8A.D0.B5.D0.BA.D1.82.D0.BE.D0.B2.2C_.D0.BF.D1.80.D0.B8.D0.BD.D0.B0.D0.B4.D0.BB.D0.B5.D0.B6.D0.B0.D1.89.D0.B8.D1.85_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.91.D0.BD.D0.BD.D0.BE.D0.B9_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B5)
    *   [3.3 Управление членством в группах](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.87.D0.BB.D0.B5.D0.BD.D1.81.D1.82.D0.B2.D0.BE.D0.BC_.D0.B2_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B0.D1.85)
    *   [3.4 Управление группами](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B0.D0.BC.D0.B8)

## Полезные группы

Обычно непривилегированных пользователей (не root) добавляют в следующие группы для предоставления доступа к периферии и другому оборудованию:

*   **audio** - для доступа к аудио-устройствам
*   **floppy** - для доступа к дисководу гибких дисков
*   **lp** - для управления заданиями печати
*   **optical** - для доступа к оптическим устройствам, таким как CD и DVD приводы (например, для воспроизведения аудио-CD)
*   **power** - используется для управления питанием (например, выключение компрьютера)
*   **storage** - для управления устройствами хранения данных
*   **video** - для устройств видео-захвата и графического ускорения
*   **wheel** - для использования [sudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)")

## Group list

<caption>A list of groups and their function (sorted alphabetically)</caption>
| Группа | Затронуте файлы | Назначение |
| adm | /var/log/* | Доступ на чтение лог файлов в каталоге /var/log |
| audio | /dev/sound/*, /dev/snd/*, /dev/misc/rtc0 | Доступ к аудио устройствам. |
| avahi |
| bin | /usr/bin/* | Right to modify binaries only by root, but right to read or executed by anyone. (Please modify this for better understanding...) |
| camera | Доступ к [Цифровым Камерам](/index.php?title=%D0%A6%D0%B8%D1%84%D1%80%D0%BE%D0%B2%D1%8B%D0%BC_%D0%9A%D0%B0%D0%BC%D0%B5%D1%80%D0%B0%D0%BC&action=edit&redlink=1 "Цифровым Камерам (page does not exist)"). |
| clamav | /var/lib/clamav/*, /var/log/clamav/* |
| daemon |
| dbus | /var/run/dbus |
| disk | /dev/sda[1-9], /dev/sdb[1-9], etc | Доступ к блочным устройствам, не принадлежащим к другим группам, таким как optical, floppy, storage. |
| floppy | /dev/fd[0-9] | Доступ к флоппи дискам. |
| ftp | /srv/ftp |
| games | /var/games | Доступ к играм. |
| gdm |
| hal | /var/run/hald, /var/cache/hald |
| http |
| kmem | /dev/port, /dev/mem, /dev/kmem |
| locate | /usr/bin/locate, /var/lib/locate, /var/lib/slocate, /var/lib/mlocate | Права на использование команды updatedb. |
| log | /var/log/* | Доступ к файлам в /var/log, |
| lp | /etc/cups, /var/log/cups, /var/cache/cups, /var/spool/cups | Доступ к принтерам |
| mem |
| mail | /usr/bin/mail |
| network | Права на изменение настроек сети, например, когда используется [Networkmanager](/index.php/Networkmanager "Networkmanager"). |
| nobody | непривелегированный пользователь. |
| ntp |
| optical | /dev/sr[0-9], /dev/sg[0-9] | Доступ с оптическим дискам, таким как CD,CD-R,DVD,DVD-R. |
| policykit |
| power | Права на использование утилит [suspend](/index.php/Pm-utils "Pm-utils"). |
| rfkill |
| root | /* -- ALL FILES! | Полный контроль над системой (root, admin) |
| scanner | /var/lock/sane | Доступ к сканерам. |
| smmsp | группа sendmail (используется для электронной почты) |
| storage | Доступ к сменным устройствам: USB дискам,флешкам, mp3 плеерам. |
| stb-admin |
| sys | Права на администрирование принтеров системы печати CUPS. |
| thinkpad | /dev/misc/nvram | Права на использование утилит,таких как [tpb](/index.php/Tpb "Tpb"), для thinkpad. |
| tty | /dev/tty, /dev/vcc, /dev/vc, /dev/ptmx |
| users | Стандартная пользовательская группа. |
| uucp | /dev/ttyS[0-9] /dev/tts/[0-9] | Последовательные и USB устройства, такие как модемы, наладонники , COM-порты. |
| vboxusers | /dev/vboxdrv | Права на использование ПО VirtualBox. |
| video | /dev/fb/0, /dev/misc/agpgart | Доступ к устройствам видеозахвата, графическому ускорению DRI/3D. |
| vmware | Права на использование ПО VMware. |
| wheel | Права на использование [sudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)") (настраиваются с помощью visudo), Также определены в PAM |

## Манипуляция группами

### Листинг групп

Показ групп пользователя командой `groups`:

```
$ groups [пользователь]

```

Если `пользователь` не задан, будут показаны группы текущего пользователя.

Команда `id` предоставляет дополнительные детали, такие как UID пользователя и ассоциированные с ним идентификаторы GID:

```
$ id [пользователь]

```

Листинг всех групп системы:

```
$ cat /etc/group

```

### Поиск объектов, принадлежащих определённой группе

Перечисляет файлы, принадлежащие указанной группе, при помощи комманды `find`:

```
# find / -group [group]

```

### Управление членством в группах

Добавление пользователей в группу командой `gpasswd`:

```
# gpasswd -a [user] [group]

```

Удаление пользователя из группы:

```
# gpasswd -d [user] [group]

```

Если пользователь в текущий момент авторизирован, он должен выйти и авторизироваться заново, чтобы изменения возымели эффект.

### Управление группами

Создание новых групп командой `groupadd`:

```
# groupadd [группа]

```

Удаление существующей группы:

```
# groupdel [группа]

```