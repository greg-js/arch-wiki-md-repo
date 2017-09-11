Из [официальной страницы проекта](http://jonls.dk/redshift/):

	*Redshift adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less if you are working in front of the screen at night. This program is inspired by [f.lux](http://justgetflux.com) [...].*

Redshift регулирует цветовую температуру экрана в зависимости от вашего окружения. Это может помочь вашим глазам меньше уставать, если вы сидите за экраном в ночное время. Эта программа вдохновлена [f.lux](http://justgetflux.com)

Проект разрабатывается на [GitHub](https://github.com/jonls/redshift).

**Примечание:** На данный момент Redshift [работает только](https://github.com/jonls/redshift/issues/55) в среде [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"), а [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)") не поддерживается. Смотрите [#Для пользователей Wayland](#.D0.94.D0.BB.D1.8F_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_Wayland).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Окружение рабочего стола](#.D0.9E.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [1.2 Автозапуск](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.1 Быстрый запуск](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
    *   [2.2 Автоматическое определение расположения основываясь на GPS](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BF.D0.BE.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D1.8B.D0.B2.D0.B0.D1.8F.D1.81.D1.8C_.D0.BD.D0.B0_GPS)
    *   [2.3 Ручная настройка](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.4 Use real screen brightness](#Use_real_screen_brightness)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 redshift-gtk не запускается](#redshift-gtk_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [3.2 Failed to run Redshift due to geoclue2](#Failed_to_run_Redshift_due_to_geoclue2)
    *   [3.3 Способ автозапуска redshift в i3](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_redshift_.D0.B2_i3)
    *   [3.4 Для пользователей Wayland](#.D0.94.D0.BB.D1.8F_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_Wayland)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [redshift](https://www.archlinux.org/packages/?name=redshift). Или же можно установить собранный с минимальными зависимостями [redshift-minimal](https://aur.archlinux.org/packages/redshift-minimal/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### Окружение рабочего стола

Для окружения рабочего стола доступна утилита `redshift-gtk` входящая в пакет [redshift](https://www.archlinux.org/packages/?name=redshift). `redshift-gtk` будет отображать значок в системном трее для управления приложением. Redshift-gtk для работы требует установки трёх дополнительных пакетов [python-gobject](https://www.archlinux.org/packages/?name=python-gobject), [python-xdg](https://www.archlinux.org/packages/?name=python-xdg) и [librsvg](https://www.archlinux.org/packages/?name=librsvg), которые указаны в списке дополнительных зависимостей для основного пакета [redshift](https://www.archlinux.org/packages/?name=redshift). Пользователи [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") могут использовать пакет [plasma5-applets-redshift-control-git](https://aur.archlinux.org/packages/plasma5-applets-redshift-control-git/).

### Автозапуск

Известные реализации автозапуска redshift:

*   Вызов в скрипте `/etc/X11/xinit/xinitrc.d/`.
*   Активируя правым кликом значок системного трея redshift-gtk или plasma5-applets-redshift-control, выбрав 'Autostart'.
*   Используя один из двух предоставленных файлов [юнитов службы systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)"): `/usr/lib/systemd/user/redshift.service` или `/usr/lib/systemd/user/redshift-gtk.service`. Будьте осторожны: служба должна запускаться в пользовательском режиме, смотрите [основные настройки](/index.php/Systemd/User_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8 "Systemd/User (Русский)"). Переменная окружения `DISPLAY` должна быть установлена. Смотрите [DISPLAY и XAUTHORITY](/index.php/Systemd/User_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#DISPLAY_.D0.B8_XAUTHORITY "Systemd/User (Русский)").

**Примечание:** Файлы юнитов redshift содержат `Restart=always`, тем самым служба будет бесконечно перезагружаться (смотрите [systemd.service(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5))

## Конфигурация

Как минимум, для работы redshift требуется указать ваши координаты, т.е. широту и долготу вашего местоположения. Redshift использует несколько методов для получения вашего местонахождения. Если ни один из них не сработал (например не установлено ни одной из используемых вспомогательных программ), то вы должны ввести местоположение вручную. Значения большинства мест/городов можно взять в соответствующих страницах Википедии.

### Быстрый запуск

**Совет:** Сервис [Latlong.net](http://www.latlong.net/) позволяет получить координаты широты и долготы.

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

Для получения более подробной информации смотрите [форум](https://bbs.archlinux.org/viewtopic.php?pid=1389735#p1389735).

### Ручная настройка

Если был создан файл `~/.config/redshift.conf`, то Redshift будет использовать настройки, указанные в нем. Однако, Redshift самостоятельно не создаст конфигурационный файл, поэтому вам нужно создать его вручную.

Пример для Витебска/Беларуси:

**Примечание:** Redshift имеет баг с настройкой transition в конфигурационном файле, которая работает не так, как описано: переход между дневным и ночным режимом вступит в силу **только** при перезапуске (как следствие - с задержками). Для получения подробностей смотрите [страницу обсуждения](/index.php/Talk:Redshift#Day_and_night_transition "Talk:Redshift") и [обсуждение на странице проекта Redshift](https://github.com/jonls/redshift/issues/270).
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

### Use real screen brightness

Redshift has a brightness adjustment setting, but it does not work the way most people might expect. In fact it is a fake brightness adjustment obtained by manipulating the gamma ramps, which means that it does not reduce the backlight of the screen. [[1]](http://jonls.dk/redshift/#known-bugs-and-limitations)

Changing screen backlight is possible with redshift hooks and [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) and [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) but, please see [Backlight#xbacklight](/index.php/Backlight#xbacklight "Backlight") as there are some limitations and you may have to find another method of controlling the backlight depending on your hardware.

Вам необходимо создать исполняемый файл в `~/.config/redshift/hooks`. Вы можете воспользоваться приведённым примером:

 `~/.config/redshift/hooks/brightness.sh` 
```
#!/bin/sh

# Set brightness via xbrightness when redshift status changes

# Set brightness values for each status.
# Range from 1 to 100 is valid
brightness_day="100"
brightness_transition="50"
brightness_night="10"
# Set fade time for changes to one minute
fade_time=60000

case $1 in
	period-changed)
		case $3 in
			night)
				xbacklight -set $brightness_night -time $fade_time
				;;
			transition)
				xbacklight -set $brightness_transition -time $fade_time
				;;
			daytime)
				xbacklight -set $brightness_day -time $fade_time
				;;
		esac
		;;
esac
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

**Примечание:** До применения метода ниже закройте redshift-gtk и перезапустите службу geoclue. Sometimes the location service fails due to e.g. connection established after the location service.

По умолчанию сконфигурирован geoclue2 без доступа для Redshift. Чтобы открыть доступ, добавьте следующие строки в `/etc/geoclue/geoclue.conf`

 `/etc/geoclue/geoclue.conf` 
```
[redshift]
allowed=true
system=false
users=
```

### Способ автозапуска redshift в i3

Вы можете добавить в конфигурационный файл i3 следующее:

```
exec --no-startup-id redshift-gtk

```

### Для пользователей Wayland

Так как Wayland не поддерживает гамма-коррекцию, то на данный момент использование redhift в нём не даст никакого эффекта [[2]](https://github.com/jonls/redshift/issues/260). Предложение по реализации уже открыто в баг-трекере.[[3]](https://github.com/jonls/redshift/issues/55)

Если вы используете Gnome, то вы можете попробовать воспользоваться [gnome-shell-extension-redshift-native-git](https://aur.archlinux.org/packages/gnome-shell-extension-redshift-native-git/). После установки этого пакета перезапустите Gnome и включите Gnome Redshift Extension.

## Смотрите также

*   [Официальный сайт](http://jonls.dk/redshift)
*   [Redshift на github](http://github.com/jonls/redshift)
*   **sct** — set color temperature

	[sct](https://aur.archlinux.org/packages/sct/) || [sct](https://aur.archlinux.org/packages/sct/)

*   [Цветовая температура](https://en.wikipedia.org/wiki/ru:%D0%A6%D0%B2%D0%B5%D1%82%D0%BE%D0%B2%D0%B0%D1%8F_%D1%82%D0%B5%D0%BC%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D1%83%D1%80%D0%B0 "wikipedia:ru:Цветовая температура")