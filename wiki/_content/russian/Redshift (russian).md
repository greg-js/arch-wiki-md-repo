Из [официальной страницы проекта](http://jonls.dk/redshift/):

	*Redshift adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less if you are working in front of the screen at night. This program is inspired by [f.lux](http://justgetflux.com) [...].*

Redshift регулирует цветовую температуру экрана в зависимости от вашего окружения. Это может помочь вашим глазам меньше уставать, если вы сидите за экраном в ночное время. Эта программа вдохновлена [f.lux](http://justgetflux.com)

Проект разработан на [GitHub](https://github.com/jonls/redshift).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Окружение рабочего стола](#.D0.9E.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [1.2 Автозапуск](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.1 Быстрый старт](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D1.81.D1.82.D0.B0.D1.80.D1.82)
    *   [2.2 Автоматическое определение расположения основываясь на GPS](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BF.D0.BE.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D1.8B.D0.B2.D0.B0.D1.8F.D1.81.D1.8C_.D0.BD.D0.B0_GPS)
    *   [2.3 Ручная настройка](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 redshift-gtk не запускается](#redshift-gtk_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [3.2 Failed to run Redshift due to geoclue2](#Failed_to_run_Redshift_due_to_geoclue2)
*   [4 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Пакет [redshift](https://www.archlinux.org/packages/?name=redshift) доступен из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Или же можно установить собранный с минимальными зависимостями [redshift-minimal](https://aur.archlinux.org/packages/redshift-minimal/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### Окружение рабочего стола

Для окружения рабочего стола доступна утилита `redshift-gtk` входящая в пакет [redshift](https://www.archlinux.org/packages/?name=redshift). Redshift-gtk будет отображать значок в системном трее для управления приложением. Redshift-gtk требует установки дополнительных зависимостей [python-gobject](https://www.archlinux.org/packages/?name=python-gobject), [python-xdg](https://www.archlinux.org/packages/?name=python-xdg) и [librsvg](https://www.archlinux.org/packages/?name=librsvg) доступных из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Пользователи [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") могут использовать пакет [kdeplasma-applets-redshift](https://aur.archlinux.org/packages/kdeplasma-applets-redshift/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### Автозапуск

Есть два способа, позволяющих реализовать автозапуск redshift:

*   Используя один из двух предоставленных файлов юнитов службы systemd (см. [Использование юнитов systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)")): `/usr/lib/systemd/user/redshift.service` или `/usr/lib/systemd/user/redshift-gtk.service`.

**Примечание:** Для работы фaйлa юнита службы systemd необходимо установить переменную среды DISPLAY как описано здесь: [Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User"). Метод регулировки 'drm' не требует указывать эту переменную.

*   При запущенном redshift-gtk нажать правой кнопкой мыши по значку в системном трее и выбрать 'Autostart'.

## Конфигурация

Redshift для работы требует как минимум указать ваши координаты, т.е. широту и долготу вашего местоположения. Redshift использует несколько процедур для получения вашего местонахождения. Если ни одина из них не сработала (например не установлено ни одной из используемых вспомогательных программ), вы должны ввести местоположение вручную. Для большинства мест/городов простым способом будет посмотреть страницу Википедии нужного места и взять из неё значения (указать в поисковом запросе "координаты").

### Быстрый старт

Чтобы запустить приложение, используя базовую конфигурацию, задайте:

```
 $ redshift -l LAT:LON

```

где соответственно LAT - широта и LON - долгота вашего местонахождения.

### Автоматическое определение расположения основываясь на GPS

Можно использовать [gpsd](https://www.archlinux.org/packages/?name=gpsd) для автоматического определения вашего местоположения посредством GPS и использовать его данные в Redshift. Создайте следующий скрипт, который будет передавать значения `$lat` и `$lon` в `redshift -l $lat;$lon`:

```
#!/bin/bash
date
#gpsdata=$( gpspipe -w -n 10 |   grep -m 1 lon )
gpsdata=$( gpspipe -w | grep -m 1 TPV )
lat=$( echo "$gpsdata"  | jsawk 'return this.lat' )
lon=$( echo "$gpsdata"  | jsawk 'return this.lon' )
alt=$( echo "$gpsdata"  | jsawk 'return this.alt' )
dt=$( echo "$gpsdata" | jsawk 'return this.time' )
echo "$dt"
echo "Вы здесь: $lat, $lon и $alt"

```

Для получения более подробной информации см. [форум](https://bbs.archlinux.org/viewtopic.php?pid=1389735#p1389735).

### Ручная настройка

Если был создан файл `~/.config/redshift.conf`, то Redshift будет использовать настройки, указанные в нем. Тем не менее, Redshift самостоятельно не создаст конфигурационный файл, так что вам нужно создать его вручную.

Пример для Витебска/Беларуси:

 `~/.config/redshift.conf` 
```
; Общие настройки для redshift
[redshift]
; Установка дневной и ночной температур экрана
; Нейтральная температура цвета - 6500K. Использование этой величины
; не изменит температуру цвета дисплея. Установка температуры цвета
; больше этого значения приведет к более синему цвету экрана,
; установка меньшего значения - к более красному оттенку.
; Значения по умолчанию:
;  Температура цвета днем: 5500K
;  Температура цвета ночью: 3500K
temp-day=6500
temp-night=3500

; Включение/выключение плавного перехода между днём и ночью
; 0 сразу установит соответствующее значение температуры экрана по приходе дня  и ночи.
; 1 будет постепенно изменять цветовую температуру экрана
transition=1

; Установка яркости дисплея. По умолчанию 1.0
;brightness=0.9
; Начиная с версии 1.8 возможно использовать различные значения для дня и ночи.
brightness-day=0.8
brightness-night=0.7
; Установка гаммы экрана для (всех цветов, или каждого цветового канала в отдельности)
gamma=0.8
;gamma=0.8:0.7:0.8

; Установка источника местоположения: 'geoclue', 'gnome-clock', 'manual'
; наберите 'redshift -l list' чтобы увидеть возможные значения
; Их настройка производится в секции ниже
location-provider=manual

; Установка метода регулировки: 'randr', 'vidmode'
; наберите 'redshift -m list' чтобы увидеть все возможные значения
; 'randr' является предпочтительным методом, 'vidmode' на устаревшем API
; но работает в некоторых случаях, когда 'randr' отказывается.
; Их настройка производится в секции ниже.
adjustment-method=randr

; Конфигурация источников местоположения:
; наберите 'redshift -l ИСТОЧНИК:help' чтобы увидеть настройки
; напр.: 'redshift -l manual:help'
[manual]
lat=55.11
lon=30.1

; Конфигурация метода регулировки
; наберите 'redshift -m METHOD:help' чтобы увидеть настройки
; напр.: 'redshift -m randr:help'
; В этом примере, randr сконфигурирован для регулировки экрана 0
; Обратите внимание, что нумерация начинается с 0, так что это на самом деле это первый экран
[randr]
screen=0
```

## Решение проблем

### redshift-gtk не запускается

Redshift-gtk требует дополнительных зависимостей для правильной работы. Для проверки недостающих зависимостей, запустите `redshift-gtk` из эмулятора терминала. Вывод будет примерно следующий:

```
 Traceback (most recent call last):
   File "/usr/bin/redshift-gtk", line 26, in <module>
     from redshift_gtk.statusicon import run
   File "/usr/lib/python3.4/site-packages/redshift_gtk/statusicon.py", line 31, in <module>
     from gi.repository import Gtk, GLib
 ImportError: No module named 'gi.repository'

```

Чтобы решить эту проблему, установите [python-gobject](https://www.archlinux.org/packages/?name=python-gobject), [python-xdg](https://www.archlinux.org/packages/?name=python-xdg), и [librsvg](https://www.archlinux.org/packages/?name=librsvg) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### Failed to run Redshift due to geoclue2

По умолчанию сконфигурирован geoclue2 без доступа для Redshift. Чтобы открыть доступ, добавьте следующие строки в `/etc/geoclue/geoclue.conf`

 `/etc/geoclue/geoclue.conf` 
```
[redshift]
allowed=true
system=false
users=
```

## См. также

*   [Официальный сайт](http://jonls.dk/redshift)
*   [Redshift на github](http://github.com/jonls/redshift)
*   [Цветовая температура](https://en.wikipedia.org/wiki/ru:%D0%A6%D0%B2%D0%B5%D1%82%D0%BE%D0%B2%D0%B0%D1%8F_%D1%82%D0%B5%D0%BC%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D1%83%D1%80%D0%B0 "wikipedia:ru:Цветовая температура")