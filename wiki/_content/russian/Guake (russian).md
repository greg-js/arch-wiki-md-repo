Ссылки по теме

*   [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")

[Guake](http://guake.org) — выпадающий эмулятор терминала для [GNOME](/index.php/GNOME "GNOME") (наподобие [Yakuake](/index.php/Yakuake "Yakuake") для [KDE](/index.php/KDE "KDE"), [Tilda](/index.php/Tilda "Tilda") и консоли из игры Quake).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
*   [3 Автозапуск](#Автозапуск)
*   [4 Управление Guake из скрипта](#Управление_Guake_из_скрипта)
*   [5 Использование Guake на нескольких мониторах](#Использование_Guake_на_нескольких_мониторах)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 В сочетаниях клавиш не работает 'Ctrl'](#В_сочетаниях_клавиш_не_работает_'Ctrl')
*   [7 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [guake](https://www.archlinux.org/packages/?name=guake) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Использование

После установки вы можете запустить Guake командой:

```
$ guake

```

Теперь вы можете зайти в *Preferences* в контекстном меню для изменения сочетания клавиши для появления/исчезания терминала. По умолчанию используется клавиша `F12`.

Также, множество параметров Guake доступно в GConf. Для редактирования реестра GConf используйте какую-нибудь утилиту, например *gconf-editor*. Настройки Guake расположены в ветке *apps > guake* (`/apps/guake`). Если этого будет для вас недостаточно, вы всегда можете просто скопировать исполняемый файл *guake* (`/usr/bin/guake`) в `/usr/local/bin/guake` и отредактировать его в текстовом редакторе, так как это всего-лишь скрипт на [Python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)"). Не забудьте сделать файл исполняемым.

## Автозапуск

Для автоматического запуска Guake при входе в систему, создайте файл *.desktop* в `/etc/xdg/autostart/`:

```
# cp /usr/share/applications/guake.desktop /etc/xdg/autostart/

```

Для получения дополнительной информации смотрите статью [Автозапуск](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA "Автозапуск").

## Управление Guake из скрипта

Как и [Yakuake](/index.php/Yakuake_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Yakuake (Русский)"), Guake позволяет настраивать себя после запуска посредством передачи сигналов через [D-Bus](/index.php/D-Bus "D-Bus"). Таким образом, его можно использовать в сеансе, опрелеяемом пользователем (*user defined session*). Вы можете создавать вкладки, устанавливать их имена, запросить запуск конкретной команды в любой открытой вкладке или просто показать/скрыть окно Guake, вручную в окне любого терминала либо создав для этого скрипт. Ниже приведен пример такого скрипта.

Вы можете использовать сам исполняемый файл *guake* для отправки сообщений D-Bus. Вот список доступных опций, которые могут быть вам интересны:

*   `-t`, `--toggle-visibility` — переключить видимость окна терминала (отобразить, если спрятано, и наоборот). По сути, вы можете просто набрать `guake`, и, если терминал уже был запущен, будет переключена видимость его окна.
*   `-f`, `--fullscreen` — переключить Guake в полноэкранный режим.
*   `--show` — показать окно Guake.
*   `--hide` — спрятать окно Guake.
*   `-n *CUR_DIR*`, `--new-tab=*CUR_DIR*` — создать новую вкладку и выбрать ее. Если указано значение `CUR_DIR`, оно будет использовано для установки текущего каталога вкладки.
*   `-s *INDEX*`, `--select-tab=*INDEX*` — выбрать (сделать текущей) вкладку с номером `INDEX`. Вкладки нумеруются с нуля.
*   `-g`, `--selected-tab` — вывести номер текущей вкладки.
*   `-e *CMD*`, `--execute-command=*CMD*` — выполнить указанную команду `CMD` в текущей вкладке.
*   `-i *INDEX*`, `--tab-index=*INDEX*` — используется с `--rename-tab` для указания номера `INDEX` вкладки, которую необходимо переименовать. По умолчанию используется значение 0.
*   `--rename-tab=*TITLE*` — установить новое имя вкладки `TITLE`. Вы можете сбросить имя вкладки на значение по умолчанию, указав знак дефиса (`"-"`). Используйте опцию `-i`, чтобы указать, какую вкладку следует переименовать.
*   `--bgcolor=*RGB*` — установить цвет фона текущей вкладки `RGB`, указанный в шестнадцатеричном формате (`#rrggbb`).
*   `--fgcolor=*RGB*` — установить цвет текста текущей вкладки `RGB`, указанный в шестнадцатеричном формате (`#rrggbb`).
*   `-r *TITLE*`, `--rename-current-tab=*TITLE*` — то же, что и `--rename-tab`, но переименовывает текущую вкладку.
*   `-q`, `--quit` — завершить работу Guake.

Несколько опций можно использовать в одном вызове. Если при вызове еще не был запущен экземпляр Guake, он будет запущен и все указанные опции будут к нему применены.

Чтобы отобразить список всех доступных опций, наберите `guake --help`.

Пример:

```
#!/bin/bash

/usr/bin/guake &
sleep 5 # позволим Guake запуститься и создать сеанс D-Bus

# настроим единственную вкладку, которая открывается по умолчанию
guake --rename-tab="iotop" --execute="/usr/bin/iotop"

# создадим новую вкладку, запустим в ней сеанс bash
guake --new-tab --execute="/usr/bin/bash"
# затем вызовем htop, переименовав вкладку в "htop"
guake --execute="/usr/bin/htop" --rename-tab="htop"

# ...
guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/atop" --rename-tab="atop"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="~/.iptables.sh" --rename-tab="iptables -nvL"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/journalctl --follow --full" --rename-tab="journalctl"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/irssi" --rename-tab="irssi"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-tab="rootshell0"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-tab="rootshell1"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-tab="shell0"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-tab="shell1"

```

Обратите внимание, что следует подождать некоторое время, вызвав *sleep*, чтобы избежать состояния гонки между процессами.

## Использование Guake на нескольких мониторах

В GConf есть два ключа, которые позволяют настроить поведение окна Guake на системе с несколькими мониторами:

*   `/apps/guake/general/display_n` — номер экрана, на котором необходимо отображать окно Guake. Ингорируется, если ключ `mouse_display` имеет значение `true`. Если установлено некорректное значение (например, экран с таким номером был отсоединен), значение ключа будет автоматически сброшено к значению по умолчанию (0).

*   `/apps/guake/general/mouse_display` — появляться на том экране, на котором находится указатель мыши (`true`/`false`). Если установлено `true`, значение `display_n` будет проигнорировано.

Используйте какую-нибудь утилиту, например *gconf-editor* для редактирования параметров GConf.

## Решение проблем

### В сочетаниях клавиш не работает 'Ctrl'

В [guake](https://www.archlinux.org/packages/?name=guake) 0.4.2-7 есть баг, затрагивающий тех пользователей, которые используют `Ctrl` в сочетании клавиш для отображения/скрытия окна терминала (то есть, если установить сочетание `Ctrl+Shift+z`, окно будет показываться и просто по нажатию `Shift+z`, независимо от того, нажата ли `Ctrl`).

Для решения проблемы запустите *gconf-editor*, откройте ветку *apps > guake > keybindings > global* и в значении ключа `show_hide` замените `<Primary>` на `<Control>`.

## Смотрите также

*   [guake(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/guake.1)