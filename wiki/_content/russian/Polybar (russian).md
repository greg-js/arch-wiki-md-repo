**Состояние перевода:** На этой странице представлен перевод статьи [Polybar](/index.php/Polybar "Polybar"). Дата последней синхронизации: 30 июля 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Polybar&diff=0&oldid=578417).

[polybar](https://github.com/jaagr/polybar) — быстрый и лёгкий инструмент для создания статус-баров. Он нацелен на лёгкую персонализацию, используя множество модулей и позволяя, например, отображать рабочие столы, дату или громкость звука. Особенно Polybar полезен в [оконных менеджерах](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") без панели или с её ограниченной функциональностью, таких как [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)") или [i3](/index.php/I3_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "I3 (Русский)"). Polybar также можно использовать и в [окружениях рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"), например, в [Plasma](/index.php/Plasma_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Plasma (Русский)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Запуск Polybar](#Запуск_Polybar)
    *   [2.2 Пример конфигурационного файла](#Пример_конфигурационного_файла)
    *   [2.3 Запуск с оконным менеджером](#Запуск_с_оконным_менеджером)
        *   [2.3.1 bspwm](#bspwm)
        *   [2.3.2 i3](#i3)
*   [3 Решение проблем](#Решение_проблем)
    *   [3.1 Cannot open shared object file libjsoncpp.so](#Cannot_open_shared_object_file_libjsoncpp.so)
*   [4 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [polybar](https://aur.archlinux.org/packages/polybar/). Экспериментальная версия доступна в пакете [polybar-git](https://aur.archlinux.org/packages/polybar-git/).

## Настройка

Скопируйте пример конфигурационного файла из `/usr/share/doc/polybar/config` в `$XDG_CONFIG_HOME/polybar/config`

#### Запуск Polybar

Polybar можно запустить со следующими параметрами:

```
Usage: polybar [OPTION]... BAR

  -h, --help               Display this help and exit
  -v, --version            Display build details and exit
  -l, --log=LEVEL          Set the logging verbosity (default: WARNING)
                           LEVEL is one of: error, warning, info, trace
  -q, --quiet              Be quiet (will override -l)
  -c, --config=FILE        Path to the configuration file
  -r, --reload             Reload when the configuration has been modified
  -d, --dump=PARAM         Print value of PARAM in bar section and exit
  -m, --list-monitors      Print list of available monitors and exit
  -w, --print-wmname       Print the generated WM_NAME and exit
  -s, --stdout             Output data to stdout instead of drawing it to the X window
  -p, --png=FILE           Save png snapshot to FILE after running for 3 seconds

```

Но скорее всего, вы будете запускать Polybar с оконным менеджером, см. раздел [#Запуск с оконным менеджером](#Запуск_с_оконным_менеджером).

#### Пример конфигурационного файла

Пример простого конфигурационного файла:

```
[bar/mybar]
modules-right = date

[module/date]
type = internal/date
date = %Y-%m-%d%
```

Он создаёт статус-бар `mybar` с модулем `date`.

Также по умолчанию polybar создаёт пример со многими преднастроенными модулями в файле `/usr/share/doc/polybar/config`.

**Примечание:** Пример конфигурационного файла может по умолчанию не работать и его необходимо настроить под свои нужды.

#### Запуск с оконным менеджером

Создайте [исполняемый](/index.php/Help:Reading_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Сделать_исполняемым "Help:Reading (Русский)") файл, содержащий процесс загрузки, например, `$HOME/.config/polybar/launch.sh`:

```
#!/bin/bash

# Завершить текущие экземпляры polybar
killall -q polybar

# Ожидание полного завершения работы процессов
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done

# Запуск Polybar со стандартным расположением конфигурационного файла в ~/.config/polybar/config
polybar mybar &

echo "Polybar загрузился..."

```

Данный скрипт означает, что при перезагрузке оконного менеджера также перезагрузится и Polybar.

###### bspwm

Если вы используете [bspwm](/index.php/Bspwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bspwm (Русский)"), добавьте следующее содержание в `bspwmrc`:

```
$HOME/.config/polybar/launch.sh

```

###### i3

Если вы используете [i3](/index.php/I3_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "I3 (Русский)"), добавьте следующее содержание в его конфигурационный файл:

```
exec_always --no-startup-id $HOME/.config/polybar/launch.sh

```

## Решение проблем

### Cannot open shared object file libjsoncpp.so

Попробуйте переустановить Polybar, как описано в [issue](https://github.com/jaagr/polybar/issues/885) на GitHub.

Если проблема не решится, попробуйте [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [jsoncpp](https://www.archlinux.org/packages/?name=jsoncpp).

## Смотрите также

*   [Polybar Github Wiki](https://github.com/jaagr/polybar/wiki/)