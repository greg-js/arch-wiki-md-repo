**Yakuake** — выпадающий сверху эмулятор терминала для [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") в стиле [Tilda](/index.php/Tilda "Tilda"), [Guake](/index.php/Guake_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Guake (Русский)") для [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и консоли в игре Quake.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Управление Yakuake из скрипта](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_Yakuake_.D0.B8.D0.B7_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0)
    *   [3.1 dbus-send вместо qdbus](#dbus-send_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_qdbus)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [yakuake](https://www.archlinux.org/packages/?name=yakuake) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Использование

После установки вы можете запустить Yakuake командой:

```
$ yakuake

```

Теперь вы можете настроить Yakuake, выбрав *Open Menu* (средняя кнопка внизу справа окна терминала), затем *Configure Yakuake*. Выберите *Configure Shortcuts* для изменения сочетания клавиши для появления/исчезания терминала. По умолчанию используется клавиша `F12`.

## Управление Yakuake из скрипта

Как и [Guake](/index.php/Guake_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Guake (Русский)"), Yakuake позволяет настраивать себя после запуска посредством передачи сигналов через [D-Bus](/index.php/D-Bus "D-Bus"). Таким образом, его можно использовать в сеансе, опрелеяемом пользователем (*user defined session*). Вы можете создавать вкладки, устанавливать их имена, запросить запуск конкретной команды в любой открытой вкладке или просто показать/скрыть окно Yakuake, вручную в окне любого терминала либо создав для этого скрипт. Ниже приведен пример такого скрипта.

```
#!/bin/bash
# Starting yakuake based on user preferences. Information based on [http://forums.gentoo.org/viewtopic-t-873915-start-0.html](http://forums.gentoo.org/viewtopic-t-873915-start-0.html)
# Adding sessions from previous website is broken, use this: [http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/](http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/)
# This line is needed in case yakuake does not accept fcitx inputs.
/usr/bin/yakuake --im /usr/bin/fcitx --inputstyle onthespot

# Start iotop in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 0 "iotop"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 0 "iotop"

# Start htop in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 1 "htop"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 1 "htop"

# Start atop in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 2 "atop"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 2 "atop"

# Start (watching) iptables in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 3 "iptables -nvL"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 3 "~/.iptables.sh"

# Start journalctl --follow --full in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 4 "journalctl"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 4 "journalctl --follow --full"

# Start irssi in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 5 "irssi"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 5 "irssi"

# Start root shell 1 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 6 "rootshell0"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 6 "sudo -i"

# Start root shell 2 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 7 "rootshell1"
qdbus org.kde.yakuake /yakuake/sessions runCommandInTerminal 7 "sudo -i"

# Start shell 1 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 8 "shell0"

# Start shell 2 in its own tab.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus org.kde.yakuake /yakuake/tabs setTabTitle 9 "shell1"

# Kill default (and now redundant) new shell tab. Already there are two shells each opened for both root and user.
qdbus org.kde.yakuake /yakuake/sessions org.kde.yakuake.removeSession 10

```

### dbus-send вместо qdbus

Вы можете заменить *qdbus* из состава [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)") более традиционной утилитой *dbus-send*. Например, чтобы показать/скрыть окно Yakuake:

```
$ dbus-send  --type=method_call --dest=org.kde.yakuake /yakuake/window org.kde.yakuake.toggleWindowState

```

## Смотрите также

*   [Взаимодействие с Yakuake посредством D-BUS](http://gentoo.ru/node/21774)