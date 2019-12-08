Ссылки по теме

*   [KDE (Русский)](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Yakuake](/index.php/Yakuake "Yakuake"). Дата последней синхронизации: 2 декабря 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Yakuake&diff=0&oldid=590474).

[Yakuake](https://www.kde.org/applications/system/yakuake/) — выпадающий сверху эмулятор терминала для [KDE (Русский)](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") в стиле [Guake (Русский)](/index.php/Guake_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Guake (Русский)") для [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"), [Tilda](/index.php/Tilda "Tilda") или консоли в игре Quake.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
*   [3 Управление Yakuake из скрипта](#Управление_Yakuake_из_скрипта)
    *   [3.1 dbus-send вместо qdbus](#dbus-send_вместо_qdbus)
*   [4 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [yakuake](https://www.archlinux.org/packages/?name=yakuake).

## Использование

После установки вы можете запустить Yakuake следующей командой:

```
$ yakuake

```

Теперь вы можете настроить Yakuake нажав на кнопку *Открыть меню* (средняя кнопка в правом нижнем углу окна терминала) и выбрав *Комбинации клавиш* для изменения сочетания клавиш для появления/исчезания терминала. По умолчанию используется клавиша F12.

## Управление Yakuake из скрипта

Как и [Guake (Русский)](/index.php/Guake_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Guake (Русский)"), Yakuake позволяет контролировать себя во время исполнения посредством передачи сигналов через [D-Bus](/index.php/D-Bus "D-Bus"). Таким образом, его можно использовать в сеансе, определяемом пользователем (user defined session). Вы можете создавать вкладки, задавать им названия, запрашивать запуск конкретной команды в любой открытой вкладке или просто показывать/скрывать окно Yakuake, вручную в терминале или создав для этого отдельный скрипт.

Ниже приведён пример такого скрипта. Он включает в себя открытие и переименование вкладок, разделение окна терминала и запуск команд.

```
#!/bin/bash
# Запуск Yakuake с настройками пользователя. Информация основана на [http://forums.gentoo.org/viewtopic-t-873915-start-0.html](http://forums.gentoo.org/viewtopic-t-873915-start-0.html)
# Добавление сессий с предыдущего сайта больше не работает, используйте этот: [http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/](http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/)

# Данная строка нужна в случае, если Yakuake не воспринимает ввод через fcitx.
/usr/bin/yakuake --im /usr/bin/fcitx --inputstyle onthespot &

# Это даёт Yakuake несколько секунд перед отправкой сигналов D-Bus.
sleep 2      

# Запуск htop в отдельной вкладке, разделение терминала и запуск iotop.                                                        
TERMINAL_ID_0=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId 0)
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 0 "user"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 0 "htop"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalLeftRight ${TERMINAL_ID_0}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 1 "iotop

# Запуск нескольких сессий root-пользователя в одной вкладке (сверху и снизу).                                                                                
SESSION_ID_1=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession)
TERMINAL_ID_1=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId ${SESSION_ID_1})
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 1 "root"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 2 "su"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalTopBottom ${TERMINAL_ID_1}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 3 "su" 

# Запуск irssi в отдельной вкладке.                                                                                          
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 2 "irssi"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 4 "ssh home -t 'tmux attach -t irssi; bash -l'" 

# Запуск нескольких терминалов SSH в одной вкладке.                                                                                   
SESSION_ID_2=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession)
TERMINAL_ID_2=$(qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.terminalIdsForSessionId ${SESSION_ID_2})
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 3 "work server"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 5 "ssh work"
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.splitTerminalLeftRight ${TERMINAL_ID_2}
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 6 "ssh work" 

```

### dbus-send вместо qdbus

Вы можете заменить *qdbus* из состава [Qt (Русский)](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)") более традиционной утилитой *dbus-send*. Например, чтобы показать/скрыть окно Yakuake:

```
$ dbus-send --type=method_call --dest=org.kde.yakuake /yakuake/window org.kde.yakuake.toggleWindowState

```

## Смотрите также

*   [Взаимодействие с Yakuake посредством D-BUS](https://gentoo.ru/node/21774)
*   [Создание скриптов для Yakuake на coderwall.com](https://coderwall.com/p/kq9ghg/yakuake-scripting)