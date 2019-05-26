**Состояние перевода:** На этой странице представлен перевод статьи [CUPS](/index.php/CUPS "CUPS"). Дата последней синхронизации: 27 марта 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=CUPS&diff=0&oldid=569911).

Ссылки по теме

*   [CUPS/Совместное использование принтеров](/index.php/CUPS/%D0%A1%D0%BE%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%BD%D0%BE%D0%B5_%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D0%B2 "CUPS/Совместное использование принтеров")
*   [CUPS/Принтероспецифичные проблемы](/index.php/CUPS/%D0%9F%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D1%87%D0%BD%D1%8B%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B "CUPS/Принтероспецифичные проблемы")
*   [CUPS/Решение проблем](/index.php/CUPS/%D0%A0%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC "CUPS/Решение проблем")
*   [Samba (Русский)](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)")
*   [LPRng](/index.php/LPRng "LPRng")

[CUPS](https://www.cups.org/) - это стандартная система печати с открытым исходным кодом, разработанная Apple Inc. для MacOS® и других UNIX®-подобных операционных систем.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 Сокет-активация](#Сокет-активация)
*   [2 Интерфейсы подключения](#Интерфейсы_подключения)
    *   [2.1 USB](#USB)
    *   [2.2 Параллельный порт](#Параллельный_порт)
    *   [2.3 Cеть](#Cеть)
*   [3 Драйверы принтеров](#Драйверы_принтеров)
    *   [3.1 CUPS](#CUPS)
    *   [3.2 Фильтры OpenPrinting CUPS](#Фильтры_OpenPrinting_CUPS)
    *   [3.3 Foomatic](#Foomatic)
    *   [3.4 Gutenprint](#Gutenprint)
    *   [3.5 Специфические для производителя драйвера](#Специфические_для_производителя_драйвера)
*   [4 URI принтера](#URI_принтера)
    *   [4.1 USB](#USB_2)
    *   [4.2 Параллельный порт](#Параллельный_порт_2)
    *   [4.3 Сеть](#Сеть)
*   [5 Использование](#Использование)
    *   [5.1 Инструменты CLI](#Инструменты_CLI)
    *   [5.2 Веб интерфейс](#Веб_интерфейс)
    *   [5.3 Приложения с GUI](#Приложения_с_GUI)
*   [6 Настройка](#Настройка)
    *   [6.1 cups-browsed](#cups-browsed)
    *   [6.2 Серверы печати и удаленное администрирование](#Серверы_печати_и_удаленное_администрирование)
    *   [6.3 Разрешение аутентификации администратора через PolicyKit](#Разрешение_аутентификации_администратора_через_PolicyKit)
    *   [6.4 Без локального сервера CUPS](#Без_локального_сервера_CUPS)
*   [7 Решение проблем](#Решение_проблем)
*   [8 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [cups](https://www.archlinux.org/packages/?name=cups).

Если вы намерены "распечатать" в документ PDF, тогда вам необходимо установить пакет [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf). По умолчанию файлы PDF хранятся в `/var/spool/cups-pdf/*имя_пользователя*`. Местоположение можно изменить в `/etc/cups/cups-pdf.conf`.

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `org.cups.cupsd.service`.

### Сокет-активация

[cups](https://www.archlinux.org/packages/?name=cups) предоставляет юнит `org.cups.cupsd.socket`. Если сокет `org.cups.cupsd.socket` [включен](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") (а служба `org.cups.cupsd.service` [отключена](/index.php/%D0%9E%D1%82%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Отключите")), systemd не будет запускать CUPS сразу, а просто будет слушать соответствующие сокеты. Затем всякий раз, когда программа пытается обратиться к одному из этих сокетов, systemd будет запускать службу `org.cups.cupsd.service` и прозрачно передавать управление этими портами процессу CUPS.

Таким образом, CUPS запускается только тогда, когда программа хочет его использовать.

## Интерфейсы подключения

Дополнительные шаги для обнаружения принтера приведены ниже для различных интерфейсов подключения.

**Примечание:**

*   Вспомогательные программы CUPS запускаются с использованием пользователя и группы `cups`. Это позволяет им получать доступ к файлам принтера и читать файлы конфигурации в `/etc/cups/`, которые принадлежат группе `cups`.
*   До [cups](https://www.archlinux.org/packages/?name=cups) версии 2.2.6-2, [вместо группы `cups` использовалась](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/cups&id=a209bf21797a239c7ddb4614f0266ba1e5238622) группа `lp`. После обновления файлы в `/etc/cups` должны принадлежать группе `cups`, а в файле `/etc/cups/cups-files.conf` должно быть прописано `User 209` и `Group 209`.

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

Чтобы обнаружить или предоставить общий доступ к принтерам с помощью DNS-SD/mDNS, настройте [разрешение имени узла .local](/index.php/Avahi#Hostname_resolution "Avahi") через [Avahi](/index.php/Avahi "Avahi") и [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `org.cups.cupsd.service`.

**Примечание:** DNS-SD поддерживается только при использовании [Avahi](/index.php/Avahi "Avahi"). CUPS не поддерживает использование [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") для DNS-SD. Для получения дополнительной информации смотрите [CUPS issue 5452](https://github.com/apple/cups/issues/5452).

Для предоставления общего доступа к принтерам с помощью [Samba](/index.php/Samba "Samba"), например, если система должна быть сервером печати для клиентов Windows, необходим пакет [samba](https://www.archlinux.org/packages/?name=samba).

## Драйверы принтеров

Драйверы для принтеров можно получить из любого из источников, приведенных ниже. Смотрите [CUPS/Принтероспецифичные проблемы](/index.php/CUPS/%D0%9F%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D1%87%D0%BD%D1%8B%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B "CUPS/Принтероспецифичные проблемы") для неполного списка драйверов, которые работают.

Для управления принтером CUPS требуется файл PPD, а для большинства принтеров - некоторые [фильтры](https://www.cups.org/doc/man-filter.html). Подробнее о том, как CUPS использует PPD и фильтры, смотрите на [[1]](https://www.cups.org/doc/postscript-driver.html).

[Список принтеров OpenPrinting](http://www.openprinting.org/printers) содержит рекомендации для драйверов для многих принтеров. Он также поставляет файлы PPD для каждого принтера, но большинство из них доступны через [foomatic](#Foomatic) или рекомендованный пакет драйверов.

Когда файлы PPD предоставляются CUPS, тогда сервер CUPS будет регенерировать файлы PPD и сохранять их в `/etc/cups/ppd/`.

### CUPS

CUPS обеспечивает поддержку принтеров [AirPrint](https://en.wikipedia.org/wiki/ru:AirPrint "w:ru:AirPrint") и [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html).

### Фильтры OpenPrinting CUPS

Рабочая группа OpenPrinting в Linux Foundation предоставляет [cups-filters](https://wiki.linuxfoundation.org/openprinting/cups-filters). Это бэкэнды, фильтры и другие двоичные файлы, которые когда-то были частью CUPS, но больше не поддерживаются Apple. Они доступны в пакете [cups-filters](https://www.archlinux.org/packages/?name=cups-filters), который является зависимостью для [cups](https://www.archlinux.org/packages/?name=cups).

Для принтеров Non-PostScript требуется установить [ghostscript](https://www.archlinux.org/packages/?name=ghostscript). Для [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) также может потребоваться [gsfonts](https://www.archlinux.org/packages/?name=gsfonts).

### Foomatic

Рабочая группа [foomatic](https://wiki.linuxfoundation.org/openprinting/database/foomatic) в OpenPrinting в Linux Foundation предоставляет PPD для многих драйверов принтеров, как свободных, так и проприетарных. Для получения дополнительной информации о том, что делает foomatic, смотрите [Обзор foomatic от разработчиков](http://www.openprinting.org/download/kpfeifle/LinuxKongress2002/Tutorial/IV.Foomatic-Developer/IV.tutorial-handout-foomatic-development.html).

Чтобы использовать foomatic, установите [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) и по крайней мере один из пакетов:

*   [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) - коллекция файлов XML, используемая foomatic-db-engine для генерации файлов PPD.
*   [foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds) - прекомпилированные файлы PPD.
*   [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree) - коллекция файлов XML под несвободными лицензиями от производителей принтеров, используемая foomatic-db-engine для генерации файлов PPD.
*   [foomatic-db-nonfree-ppds](https://www.archlinux.org/packages/?name=foomatic-db-nonfree-ppds) - прекомпилированные файлы PPD под несвободными лицензиями.

Для PPD foomatic могут потребоваться дополнительные фильтры, такие как [min12xxw](https://aur.archlinux.org/packages/min12xxw/).

### Gutenprint

Проект [Gutenprint](http://gimp-print.sourceforge.net/) предоставляет драйвера для Canon, Epson, Lexmark, Sony, Olympus, и принтеров PCL для использования с CUPS и [GIMP](/index.php/GIMP "GIMP").

Установите [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) и [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds).

**Примечание:** Когда пакет Gutenprint обновился, принтеры, использующие драйвера Gutenprint, будут остановлены, пока вы не выполните от суперпользователя команду `cups-genppdupdate` и не перезапустите CUPS. Команда *cups-genppdupdate* обновит файлы PPD для всех настроенных принтеров. Для получения дополнительной информации смотрите [cups-genppdupdate(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cups-genppdupdate.8).

### Специфические для производителя драйвера

Многие производители принтеров поставляют свои собственные драйверы Linux. Они часто доступны в официальных хранилищах Arch или в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Некоторые из этих драйверов описаны более подробно в [CUPS/Принтероспецифичные проблемы](/index.php/CUPS/%D0%9F%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D1%87%D0%BD%D1%8B%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B "CUPS/Принтероспецифичные проблемы").

## URI принтера

Ниже перечислены дополнительные шаги для ручного создания URI, если это необходимо. Для некоторых принтеров или драйверов нужны особые URI, описанные в [CUPS/Принтероспецифичные проблемы](/index.php/CUPS/%D0%9F%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D1%87%D0%BD%D1%8B%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B "CUPS/Принтероспецифичные проблемы").

### USB

CUPS должен иметь возможность автоматически генерировать URI для USB-принтеров, например `usb://HP/DESKJET%20940C?serial=CN16E6C364BH`.

Если этого не происходит, смотрите [CUPS/Решение проблем#USB-принтеры](/index.php/CUPS/%D0%A0%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC#USB-принтеры "CUPS/Решение проблем") для получения информации об устранении неполадок.

### Параллельный порт

URI должен иметь вид `parallel:*device*`. Например, если принтер подключен к `/dev/lp0`, используйте `parallel:/dev/lp0`. Если вы используете адаптер USB для параллельного порта, используйте `parallel:/dev/usb/lp0` в качестве URI принтера.

### Сеть

Если вы настроили [Avahi](/index.php/Avahi "Avahi"), как в [#Сеть](#C.D0.B5.D1.82.D1.8C), CUPS должен определить URI принтера. Вы также можете использовать `avahi-discover`, чтобы найти имя вашего принтера и его адрес (например, `BRN30055C6B4C7A.local/10.10.0.155:631`).

URI также можно создать вручную, не используя [Avahi](/index.php/Avahi "Avahi"). Список доступных схем URI для сетевых принтеров доступен в [документации CUPS](https://www.cups.org/doc/network.html#PROTOCOLS). Поскольку точные данные URI отличаются между принтерами, проверьте руководство принтера или [CUPS/Принтероспецифичные проблемы](/index.php/CUPS/%D0%9F%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D1%87%D0%BD%D1%8B%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B "CUPS/Принтероспецифичные проблемы").

URI для сетевых принтеров [SMB](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)") описаны на справочной странице [smbspool(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smbspool.8).

К удаленным серверам печати CUPS можно получить доступ через URI формы `ipp://*hostname*:631/printers/*queue_name*`. Подробнее о настройке удаленного сервера печати смотрите [CUPS/Printer sharing#Between GNU/Linux systems](/index.php/CUPS/Printer_sharing#Between_GNU/Linux_systems "CUPS/Printer sharing").

Смотрите [CUPS/Решение проблем#Проблемы с сетью](/index.php/CUPS/%D0%A0%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC#Проблемы_с_сетью "CUPS/Решение проблем") для получения дополнительной информации о проблемах и их решений.

**Важно:** Не следует настраивать как сервер, так и клиент с помощью фильтра принтера - либо очереди печати на клиенте, либо сервер должен быть 'raw'. Это позволяет избежать отправки заданий печати через фильтры для принтера дважды, что может вызвать проблемы (например, [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1589908#p1589908)). Смотрите [#Использование](#Использование) для примера установки очереди печати на 'raw'.

## Использование

CUPS можно полностью контролировать с помощью инструментов командной строки (CLI) из пакетов lp* и cups*. В качестве альтернативы можно использовать [#Веб интерфейс](#Веб_интерфейс) или одно из нескольких [#Приложения с GUI](#Приложения_с_GUI).

*   *Имя принтера* - короткое, но описательное имя, используемое в системе для идентификации принтера. Это имя не должно содержать пробелов или специальных символов. Например, принтер, соответствующий HP LaserJet 5P, может быть назван "hpljet5p". С каждым физическим принтером можно связать более одной очереди.
*   *Расположение* - это описание физического расположения принтера (например, "спальня", или "кухня"). Это помогает поддерживать несколько принтеров.
*   *Описание* - полное описание принтера. Обычно используется полное имя принтера (например, "HP LaserJet 5P").

### Инструменты CLI

Смотрите [локальную документацию CUPS](http://localhost:631/help/options.html) для получения дополнительных сведений об инструментах командной строки.

**Примечание:** Нельзя сгруппировать переключатели командной строки

	Список устройств

```
# lpinfo -v
$ /usr/lib/cups/backend/snmp *ip_address* # Используйте SNMP для поиска URI

```

	Список моделей

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
# lpadmin -p Test_Printer -E -v "ipp://10.0.1.3/ipp/print" -m pxlmono.ppd    # Указание PPD вместо модели

```

**Примечание:** При указании PPD используйте только имя файла, а не полный путь (например, `pxlmono.ppd` вместо `/usr/share/ppd/cupsfilters/pxlmono.ppd`)

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
$ echo 'Привет, мир!' | lpr -p # распечатать результат команды. Переключатель -p добавляет заголовок.

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

Для выполнения административных задач требуется аутентификация веб-интерфейса. Аутентифицируйте себя либо как `root`, либо убедитесь, что ваш пользователь входит в группу с полномочиями управления принтерами, для получения дополнительной информации смотрите [#Настройка](#Настройка).

	Добавление принтера

Перейдите на вкладку **Администрирование**.

	Изменение существующих принтеров

Перейдите на вкладку **Принтеры** и выберите принтер для изменения.

	Проверка принтера

Перейдите на вкладку **Принтеры** и выберите принтер.

### Приложения с GUI

Если у вашего пользователя нет достаточных привилегий для администрирования CUPS, приложения будут запрашивать пароль root при запуске. Чтобы предоставить пользователям права администратора без необходимости доступа root, смотрите [#Настройка](#Настройка).

*   **GtkLP** — Интерфейс GTK+ для CUPS.

	[https://gtklp.sirtobi.com/index.shtml](https://gtklp.sirtobi.com/index.shtml) || [gtklp](https://aur.archlinux.org/packages/gtklp/)

*   **print-manager** — Инструмент для управления заданиями печати и принтерами ([KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)")).

	[https://cgit.kde.org/print-manager.git](https://cgit.kde.org/print-manager.git) || [print-manager](https://www.archlinux.org/packages/?name=print-manager)

*   **system-config-printer** — Инструмент настройки принтера GTK+ и апплет состояния ([GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и другие).

	[http://cyberelk.net/tim/software/system-config-printer/](http://cyberelk.net/tim/software/system-config-printer/) || [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer)

## Настройка

Настройки сервера CUPS находятся в `/etc/cups/cupsd.conf` и `/etc/cups/cups-files.conf` (смотрите [cupsd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cupsd.conf.5) и [cups-files.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cups-files.conf.5)). После редактирования любого из этих файлов, [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") `org.cups.cupsd.service`, чтобы применить произведенные изменения. Настройки по умолчанию подходят для большинства пользователей.

[Группы](/index.php/%D0%93%D1%80%D1%83%D0%BF%D0%BF%D1%8B "Группы") с правами администрирования принтера определены в `SystemGroup` в `/etc/cups/cups-files.conf`. Группы `sys` и `root` используется по умолчанию.

Пакет [cups](https://www.archlinux.org/packages/?name=cups) собран с поддержкой [libpaper](https://www.archlinux.org/packages/?name=libpaper) и значением по умолчанию для формата бумаги **Письмо** для файла libpaper. Чтобы избежать необходимости изменять размер бумаги для каждого принтера, отредактируйте `/etc/papersize` и задайте размер бумаги по умолчанию для вашей системы. Для получения дополнительной информации смотрите [papersize(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/papersize.5).

По умолчанию все журналы отправляются в файлы в `/var/log/cups/`. Изменив значения директив `AccessLog`, `ErrorLog` и `PageLog` в `/etc/cups/cups-files.conf` на `syslog`, то CUPS сможет отправлять логи в [журнал systemd](/index.php/%D0%96%D1%83%D1%80%D0%BD%D0%B0%D0%BB_systemd "Журнал systemd"). Смотрите [вики-страницу fedora](https://fedoraproject.org/wiki/Changes/CupsJournalLogging) для получения информации об исходном предлагаемом изменении.

### cups-browsed

CUPS может использовать [Avahi](/index.php/Avahi "Avahi") для обнаружения неизвестных общих принтеров в вашей сети. Это может быть полезно при больших настройках, где сервер неизвестен. Чтобы использовать эту функцию, настройте [разрешение .local hostname](/index.php/Avahi#Hostname_resolution "Avahi") и запустите службы `avahi-daemon.service` и `cups-browsed.service`. Задания отправляются непосредственно на принтер без какой-либо обработки, поэтому созданные очереди могут не работать, однако для принтеров, не требущих драйверов, такие как те, которые поддерживают [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html) или [AirPrint](https://en.wikipedia.org/wiki/ru:AirPrint "w:ru:AirPrint") все должно работать из коробки.

**Примечание:**

*   Поиск сетевых принтеров [может значительно увеличить время, необходимое для загрузки вашего компьютера](https://bbs.archlinux.org/viewtopic.php?pid=1720219#p1720219).
*   Служба `cups-browsed.service` необходима только для динамического добавления и удаления принтеров, когда они появляются и исчезают из сети. Она не требуется, если вы просто хотите добавить сетевой принтер с поддержкой DNS-SD/mDNS в CUPS.

### Серверы печати и удаленное администрирование

Для получения дополнительной информации смотрите [CUPS/Совместное использование принтеров](/index.php/CUPS/%D0%A1%D0%BE%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%BD%D0%BE%D0%B5_%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BE%D0%B2 "CUPS/Совместное использование принтеров") и [CUPS/Printer sharing#Remote administration](/index.php/CUPS/Printer_sharing#Remote_administration "CUPS/Printer sharing").

### Разрешение аутентификации администратора через PolicyKit

[PolicyKit](/index.php/Polkit_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Polkit (Русский)") можно настроить так, чтобы пользователи могли настраивать принтеры с помощью графического интерфейса без пароля администратора.

**Примечание:** Возможно, вам понадобится установить [cups-pk-helper](https://www.archlinux.org/packages/?name=cups-pk-helper) для работы с этими правилами.

Вот пример, который позволяет членам [группы](/index.php/%D0%93%D1%80%D1%83%D0%BF%D0%BF%D1%8B "Группы") wheel управлять принтерами без пароля:

 `/etc/polkit-1/rules.d/49-allow-passwordless-printer-admin.rules` 
```
polkit.addRule(function(action, subject) { 
    if (action.id == "org.opensuse.cupspkhelper.mechanism.all-edit" && 
        subject.isInGroup("wheel")){ 
        return polkit.Result.YES; 
    } 
});

```

### Без локального сервера CUPS

CUPS можно настроить для прямого подключения к удаленным серверам принтеров вместо запуска локального сервера печати. Для этого потребуется [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [libcups](https://www.archlinux.org/packages/?name=libcups). Некоторым приложениям по-прежнему потребуется пакет [cups](https://www.archlinux.org/packages/?name=cups) для печати.

**Важно:** Доступ к удаленным принтерам без локального сервера CUPS не рекомендуется разработчиками. [[3]](https://lists.cups.org/pipermail/cups/2015-October/027229.html)

Чтобы использовать удаленный сервер CUPS, установите [переменную окружения](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "Переменные окружения") `CUPS_SERVER` в `printerserver.mydomain:port`. Например, если вы хотите использовать другой сервер печати для одного экземпляра [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)") (замените `printserver.mydomain:port` на имя/порт своего сервера печати):

```
$ CUPS_SERVER=printserver.mydomain:port firefox

```

## Решение проблем

Для получения дополнительной информации смотрите [CUPS/Решение проблем](/index.php/CUPS/%D0%A0%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC "CUPS/Решение проблем").

# Смотрите также

*   [Официальная документация CUPS documentation](http://localhost:631/help), *локальная установка*
*   [Википедия:Common UNIX Printing System](https://en.wikipedia.org/wiki/ru:Common_UNIX_Printing_System "w:ru:Common UNIX Printing System")
*   [Домашняя страница OpenPrinting](http://www.linuxfoundation.org/collaborate/workgroups/openprinting)
*   [Руководство по печати OpenSuSE Concepts - объясняет полный рабочий процесс печати](https://en.opensuse.org/Concepts_printing)
*   [OpenSuSE CUPS в двух словах - быстрый обзор CUPS](https://en.opensuse.org/SDB:CUPS_in_a_Nutshell)
*   [Руководство по печати Gentoo](https://wiki.gentoo.org/wiki/Printing/ru)
*   [Портал печати Debian - подробные технические руководства](https://wiki.debian.org/Printing "debian:Printing")
*   [Обзор печати Debian - основной вид системы печати CUPS](https://wiki.debian.org/ru/SystemPrinting "debian:ru/SystemPrinting")