Ссылки по теме

*   [lm sensors (Русский)](/index.php/Lm_sensors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Lm sensors (Русский)")
*   [Conky (Русский)](/index.php/Conky_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Conky (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Hddtemp](/index.php/Hddtemp "Hddtemp"). Дата последней синхронизации: 12 сентября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Hddtemp&diff=0&oldid=582038).

[hddtemp](https://savannah.nongnu.org/projects/hddtemp/) — небольшая утилита (включающая в состав службу), позволяющая узнать температуру жёсткого диска посредством [S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") (для дисков, поддерживающих эту технологию).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
*   [3 Служба](#Служба)
    *   [3.1 Изменить предопределённый диск](#Изменить_предопределённый_диск)
*   [4 Мониторинг](#Мониторинг)
*   [5 Твердотельные накопители](#Твердотельные_накопители)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [hddtemp](https://www.archlinux.org/packages/?name=hddtemp).

## Использование

Hddtemp требует привилегий суперпользователя. Команда `hddtemp` требует указания как минимум одного физического устройства или нескольких, разделённых пробелами. Например:

```
# hddtemp /dev/disk/by-id/wwn-0x60015ee0000b237f /dev/sd*X2* ... /dev/sd*Xn*

```

**Примечание:** Названия блочных устройств в `/dev/`, подобно `/dev/sdX`, неоднозначны. См. статью [Persistent block device naming (Русский)](/index.php/Persistent_block_device_naming_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Persistent block device naming (Русский)") для получения информации об использовании постоянных путей устройств.

Для получения дополнительной информации смотрите man-страницу:

```
$ man hddtemp

```

## Служба

Запуск службы позволит получать информацию о температуре по TCP/IP обычному пользователю. Это может быть полезно для использования скриптов или систем мониторинга.

Служба [контролируется](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_юнитов "Systemd (Русский)") `hddtemp.service`.

Чтобы получить информацию о температуре, подключитесь к серверу со включённой службой, которая прослушивает порт 7634.

С помощью [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
$ telnet localhost 7634

```

С помощью [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat):

```
$ nc localhost 7634

```

Вывод будет примерно следующий:

```
|/dev/sda|ST3500413AS|32|C||/dev/sdb|ST2000DM001-1CH164|36|C|

```

Более читаемый вариант:

 `$ nc localhost 7634 |sed 's/|//m' | sed 's/||/ 
/g' | awk -F'|' '{print $1 " " $3 " " $4}'` 
```
/dev/sda 32 C 
/dev/sdb 36 C
```

### Изменить предопределённый диск

По умолчанию служба hddtemp отслеживает только `/dev/sda`. Если у вас несколько дисков, то вам потребуется [переопределить](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Редактирование_предоставленных_пакетами_файлов_юнитов "Systemd (Русский)") стандартную конфигурацию мониторинга.

Необходимо предварительно узнать, какие жёсткие диски поддерживают мониторинг. Для этого можно воспользоваться [smartmontools](https://www.archlinux.org/packages/?name=smartmontools).

Сначала запустите команду ниже, которая откроет ваш стандартный текстовый редактор:

```
# systemctl edit hddtemp.service

```

Добавьте следующий текст:

 `/etc/systemd/system/hddtemp.service.d/<temp file>` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/hddtemp --daemon --foreground /dev/disk/by-id/wwn-0x60015ee0000b237f /dev/sdb --listen=127.0.0.1
```

Измените названия устройств, которые вы хотите отслеживать.

После редактирования сохранитесь и выйдите из текстового редактора. *systemd* автоматически применит изменения и перезагрузит службу `hddtemp`.

Также можно воспользоваться скриптом [auto-generate](https://github.com/AndyCrowd/auto-generate-configuration-files/blob/master/gen-customexec.conf-hddtemp.sh), который определит поддерживаемые жёсткие диски с помощью [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) и напечатает результат в стандартный поток вывода.

## Мониторинг

Hddtemp может быть встроен в [различные системы мониторинга](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Состояние_системы "List of applications (Русский)"). [Conky](/index.php/Conky_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Conky (Русский)") также собран с поддержкой hddtemp в режиме демона. Вам нужно просто добавить `$hddtemp °C` в ваш конфигурационный файл conky.

## Твердотельные накопители

Для получения значения температуры hddtemp обычно считывает поле `194` данных S.M.A.R.T. жёсткого диска. В SSD накопителях информация о температуре обычно хранится в поле `190`. Можно посмотреть этот параметр, выполнив следующие команды:

```
$ smartctl -a /dev/sdX

```

или

```
$ hddtemp --debug /dev/sdX

```

где X — буква диска (например a,b,c...). Воспользуйтесь `lsblk` для проверки.

Другой способ — внести запись в базу данных hddtemp, указав требуемый накопитель с параметрами поля и единицы измерения в `/usr/share/hddtemp/hddtemp.db`. Например:

```
$ echo '"Samsung SSD 840 EVO 250GB" 190 C "Samsung SSD 840 EVO 250GB"' >> /usr/share/hddtemp/hddtemp.db

```