Ссылки по теме

*   [CUPS/Printer sharing (Русский)](/index.php/CUPS/Printer_sharing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS/Printer sharing (Русский)")
*   [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems")
*   [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting")
*   [Samba (Русский)](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)")
*   [LPRng](/index.php/LPRng "LPRng")

**Состояние перевода:** На этой странице представлен перевод статьи [CUPS](/index.php/CUPS "CUPS"). Дата последней синхронизации: 19 августа 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=CUPS&diff=0&oldid=485933).

[CUPS](http://www.cups.org/) - это стандартная система печати с открытым исходным кодом, разработанная Apple Inc. для MacOS® и других UNIX®-подобных операционных систем.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Интерфейсы подключения](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.1 USB](#USB)
    *   [2.2 Параллельный порт](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BB.D0.BB.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BF.D0.BE.D1.80.D1.82)
    *   [2.3 Cеть](#C.D0.B5.D1.82.D1.8C)
*   [3 Драйверы принтеров](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D1.8B_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.BE.D0.B2)
    *   [3.1 CUPS](#CUPS)
    *   [3.2 Foomatic](#Foomatic)
    *   [3.3 Специфические для производителя драйвера](#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8F_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0)
*   [4 URI принтера](#URI_.D0.BF.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.B0)
    *   [4.1 USB](#USB_2)
    *   [4.2 Параллельный порт](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BB.D0.BB.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BF.D0.BE.D1.80.D1.82_2)
    *   [4.3 Сеть](#.D0.A1.D0.B5.D1.82.D1.8C)
*   [5 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [5.1 Инструменты CLI](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B_CLI)
    *   [5.2 Веб интерфейс](#.D0.92.D0.B5.D0.B1_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
    *   [5.3 Приложения с GUI](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81_GUI)
*   [6 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [cups](https://www.archlinux.org/packages/?name=cups).

Для печати из приложений GTK3 вам потребуется дополнительно установить пакет [gtk3-print-backends](https://www.archlinux.org/packages/?name=gtk3-print-backends).

Если вы намерены "распечатать" документ PDF, тогда вам необходимо установить пакет [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf). По умолчанию файлы PDF хранятся в `/var/spool/cups-pdf/$USER`. Местоположение можно изменить в `/etc/cups/cups-pdf.conf`.

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `org.cups.cupsd.service`.

## Интерфейсы подключения

Дополнительные шаги для обнаружения принтера приведены ниже для различных интерфейсов подключения.

**Примечание:** Вспомогательные программы CUPS запускаются с использованием группы `lp` и `daemon`. Это позволяет вспомогательным программам получать доступ к файлам устройств принтера **и** в файлах конфигурации `/etc/cups/`, которые все принадлежат группе `lp`. Это поведение по умолчанию может привести к конфликту с доступом к устройствам с параллельным портом без принтера:

*   Добавление дополнительных пользователей в группу `lp` позволит этим пользователям читать файлы CUPS и
*   Вспомогательные программы CUPS могут получить доступ к любым устройствам с параллельным портом, не относящимся к принтеру.

Если это вызывает беспокойство, подумайте об использовании правила [Udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"), чтобы назначить другую группу для любого устройства с параллельным портом без принтера ([FS#50009](https://bugs.archlinux.org/task/50009)). Группа и пользователь, использующие CUPS, могут быть изменены, но, возможно, необходимо будет вручную разрешить некоторые файлы.

### USB

Чтобы узнать, обнаружен ли ваш USB-принтер:

 `$ lsusb` 
```
(...)
Bus 001 Device 007: ID 03f0:1004 Hewlett-Packard DeskJet 970c/970cse

```

### Параллельный порт

Чтобы использовать принтер с параллельным портом, требуются [модули ядра](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0 "Модули ядра") `lp`, `parport` и `parport_pc`.

 `$ dmesg | grep -i parport` 
```
 parport0: Printer, Hewlett-Packard HP LaserJet 2100 Series
 lp0: using parport0 (polling)

```

### Cеть

[Avahi](/index.php/Avahi "Avahi") можно использовать для сканирования принтеров в локальной сети. Чтобы использовать имена хостов [Avahi](/index.php/Avahi "Avahi") для подключения к сетевым принтерам, настройте [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") и [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") `org.cups.cupsd.service`.

Если система подключена к сетевому принтеру с использованием протокола [Samba](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)"), или если система должна быть сервером печати для клиентов Windows, установите пакет [samba](https://www.archlinux.org/packages/?name=samba).

## Драйверы принтеров

Драйверы для принтеров можно получить из любого из источников, приведенных ниже. Смотрите [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems") для неполного списка драйверов, которые работают.

Для управления принтером CUPS требуется файл PPD, а для большинства принтеров - некоторые [фильтры](https://www.cups.org/doc/man-filter.html). Подробнее о том, как CUPS использует PPD и фильтры, смотрите на [[1]](https://www.cups.org/doc/postscript-driver.html).

[Список принтеров OpenPrinting](http://www.openprinting.org/printers) содержит рекомендации для драйверов для многих принтеров. Он также поставляет файлы PPD для каждого принтера, но большинство из них доступны через [foomatic](#Foomatic) или рекомендованный пакет драйверов.

Когда файлы PPD предоставляются CUPS, тогда сервер CUPS будет регенерировать файлы PPD и сохранять их в `/etc/cups/ppd/`.

### CUPS

CUPS по умолчанию предоставляет несколько PPD и фильтры двоичных файлов, которые должны работать из коробки. CUPS также обеспечивает поддержку принтеров [AirPrint](https://en.wikipedia.org/wiki/ru:AirPrint "w:ru:AirPrint") и [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html).

### Foomatic

Проект [foomatic](https://wiki.linuxfoundation.org/openprinting/database/foomatic) предоставляет PPD для многих драйверов принтеров, как свободных, так и проприетарных. Для получения дополнительной информации о том, что делает foomatic смотрите [Обзор foomatic от разработчиков](http://www.openprinting.org/download/kpfeifle/LinuxKongress2002/Tutorial/IV.Foomatic-Developer/IV.tutorial-handout-foomatic-development.html).

Чтобы использовать foomatic, установите [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) и по крайней мере один из пакетов [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds), [foomatic-db-nonfree-ppds](https://www.archlinux.org/packages/?name=foomatic-db-nonfree-ppds), или [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds).

Для PPD foomatic могут потребоваться дополнительные фильтры, такие как [gutenprint](https://www.archlinux.org/packages/?name=gutenprint), [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) или другие (например [min12xxw](https://aur.archlinux.org/packages/min12xxw/)). Для [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) также может потребоваться [gsfonts](https://www.archlinux.org/packages/?name=gsfonts).

### Специфические для производителя драйвера

Многие производители принтеров поставляют свои собственные драйверы Linux. Они часто доступны в официальных хранилищах Arch или в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Некоторые из этих драйверов описаны более подробно в [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

## URI принтера

Ниже перечислены дополнительные шаги для ручного создания URI, если это необходимо.

### USB

CUPS должен иметь возможность автоматически генерировать URI для USB-принтеров, например `usb://HP/DESKJET%20940C?serial=CN16E6C364BH`.

Если этого не происходит, смотрите [CUPS/Troubleshooting#USB printers](/index.php/CUPS/Troubleshooting#USB_printers "CUPS/Troubleshooting") для устранения неполадок.

### Параллельный порт

URI должен иметь вид `parallel:*device*`. Например, если принтер подключен к `/dev/lp0`, используйте `parallel:/dev/lp0`. Если вы используете адаптер USB для параллельного порта, используйте `parallel:/dev/usb/lp0` в качестве URI принтера.

### Сеть

Если вы настроили [Avahi](/index.php/Avahi "Avahi"), как в [#Сеть](#.D0.A1.D0.B5.D1.82.D1.8C), CUPS должен определить URI принтера. Вы также можете использовать `avahi-discover`, чтобы найти имя вашего принтера и его адрес (например, `BRN30055C6B4C7A.local/10.10.0.155:631`).

URI также можно создать вручную, не используя [Avahi](/index.php/Avahi "Avahi"). Список доступных схем URI для сетевых принтеров доступен в документации CUPS [[2]](https://www.cups.org/doc/network.html#PROTOCOLS). Поскольку точные данные URI отличаются между принтерами, проверьте руководство принтера или [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

К удаленным серверам печати CUPS можно получить доступ через URI формы `ipp://*hostname*:631/printers/*queue_name*`. Подробнее о настройке удаленного сервера печати смотрите [CUPS/Printer sharing#Between GNU/Linux systems](/index.php/CUPS/Printer_sharing#Between_GNU.2FLinux_systems "CUPS/Printer sharing").

Смотрите [CUPS/Troubleshooting#Networking issues](/index.php/CUPS/Troubleshooting#Networking_issues "CUPS/Troubleshooting") для получения дополнительной информации о проблемах и их решений.

**Важно:** Не следует настраивать как сервер, так и клиент с помощью фильтра принтера - либо очереди печати на клиенте, либо сервер должен быть 'raw'. Это позволяет избежать отправки заданий печати через фильтры для принтера дважды, что может вызвать проблемы (например, [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1589908#p1589908)). Смотрите [#Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5) для примера установки очереди печати на 'raw'.

## Использование

CUPS можно полностью контролировать с помощью инструментов командной строки (CLI) из пакетов lp* и cups*. В качестве альтернативы можно использовать [#Веб интерфейс](#.D0.92.D0.B5.D0.B1_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81) или одно из нескольких [#Приложения с GUI](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81_GUI).

*   *Имя принтера* - короткое, но описательное имя, используемое в системе для идентификации принтера. Это имя не должно содержать пробелов или специальных символов. Например, принтер, соответствующий HP LaserJet 5P, может быть назван "hpljet5p". С каждым физическим принтером можно связать более одной очереди.
*   *Расположение* - это описание физического расположения принтера (например, "спальня", или "кухня"). Это помогает поддерживать несколько принтеров.
*   *Описание* - полное описание принтера. Обычно используется полное имя принтера (например, "HP LaserJet 5P").

### Инструменты CLI

Смотрите [локальную документацию CUPS](http://localhost:631/help/options.html) для получения дополнительных сведений об инструментах командной строки.

**Примечание:** Нельзя сгруппировать переключатели командной строки

	Список устройств

```
# lpinfo -v # 
$ /usr/lib/cups/backend/snmp *ip_address* # Используйте SNMP для поиска URI

```

	Список драйверов;

```
$ lpinfo -m

```

	Добавление нового принтера

```
# lpadmin -p *имя принтера* -E -v *uri* -m *model*

```

*Имя принтера* зависит от тебя. Например:

```
# lpadmin -p HP_DESKJET_940C -E -v "usb://HP/DESKJET%20940C?serial=CN16E6C364BH" -m drv:///HP/hp-deskjet_940c.ppd.gz
# lpadmin -p AirPrint -E -v "ipp://10.0.1.25/ipp/print" -m everywhere    # Принтеры без драйверов (Apple AirPrint или IPP Everywhere)
# lpadmin -p SHARED_PRINTER -m raw    # Необработанный принтер; нет PPD или фильтра

```

	Установите принтер по умолчанию

```
$ lpoptions -d *имя принтера*

```

	Изменение параметров

```
$ lpoptions -p *имя принтера* -l # Список параметров
$ lpoptions -p *имя принтера* -o *option*=*value* # Установка параметра

```

Например:

```
$ lpoptions -p HP_DESKJET_940C -o PageSize=A4

```

	Проверка cостояния принтера

```
$ lpstat -s
$ lpstat -p *имя принтера*

```

	Отключение принтера

```
# cupsdisable *имя принтера*

```

	Включение принтера

```
# cupsenable *имя принтера*

```

	Настройка принтера для приема заданий

```
# cupsaccept *имя принтера*

```

	Удаление принтера

Сначала настройте принтер для отклонения всех входящих записей:

```
# cupsreject *имя принтера*

```

Затем отключите его.

```
# cupsdisable *имя принтера*

```

Наконец, удалите его.

```
# lpadmin -x *имя принтера*

```

	Печать файла

```
$ lpr *файл*
$ lpr -# 17 *файл*            # распечатать файл 17 раз
$ echo "Привет, мир!" | lpr -p # распечатать результат команды. Переключатель -p добавляет заголовок.

```

	Проверка очереди

```
$ lpq
$ lpq -a # во всех очередях

```

	Очистка очереди

```
# lprm   # удаляет только последнюю запись
# lprm - # удаляет все записи

```

### Веб интерфейс

Сервером CUPS можно полностью управлять через веб-интерфейс, доступный по адресу [http://localhost:631/](http://localhost:631/).

**Примечание:** Если используется HTTPS-соединение с CUPS, оно может длиться очень долго, прежде чем интерфейс появится при первом доступе. Это связано с тем, что первый запрос инициирует создание SSL-сертификатов, которое может занимать много времени.

Для выполнения административных задач требуется аутентификация веб-интерфейса. Аутентифицируйте себя либо как `root`, либо убедитесь, что ваш пользователь входит в группу с полномочиями управления принтерами, для получения допольнительной информации смотрите [#Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0).

	Добавление принтера

Перейдите на страницу **Administration**.

	Изменение существующих принтеров

Перейдите на страницу **Printers** и выберите принтер для изменения.

	Проверка принтера

Перейдите на страницу **Printers** и выберите принтер.

### Приложения с GUI

Если у вашего пользователя нет достаточных привилегий для администрирования CUPS, приложения будут запрашивать пароль root при запуске. Чтобы предоставить пользователям права администратора без необходимости доступа root, смотрите [#Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0).

*   **print-manager** — Инструмент для управления заданиями печати и принтерами ([KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)")).

	[https://projects.kde.org/projects/kde/kdeutils/print-manager](https://projects.kde.org/projects/kde/kdeutils/print-manager) || [print-manager](https://www.archlinux.org/packages/?name=print-manager)

*   **system-config-printer** — Инструмент настройки принтера CUPS и апплет состояния ([GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и другие)

	[http://cyberelk.net/tim/software/system-config-printer/](http://cyberelk.net/tim/software/system-config-printer/) || [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer)

*   **gtklp** — Интерфейс GTK + для CUPS.

	[http://gtklp.sirtobi.com/index.shtml](http://gtklp.sirtobi.com/index.shtml) || [gtklp](https://aur.archlinux.org/packages/gtklp/)

# См. также

*   [Официальная документация CUPS documentation](http://localhost:631/documentation.html), *локальная установка*
*   [Официальный Веб-сайт CUPS](http://www.cups.org/)
*   [Linux Printing](http://www.linuxprinting.org/), *[Linux Foundation](http://www.linuxfoundation.org)*
*   [Руководство по печати в Gentoo](http://www.gentoo.org/doc/en/printing-howto.xml), *[Источники Документации Gentoo](http://www.gentoo.org/doc/en)*
*   [Форум пользователей Arch Linux](https://bbs.archlinux.org/)

*   [Простая установка принтеров HP](http://wiki.gotux.net/config/hp-printer)