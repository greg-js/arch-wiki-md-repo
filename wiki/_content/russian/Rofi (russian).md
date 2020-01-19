Ссылки по теме

*   [Список приложений/Другие#Утилиты запуска приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9/%D0%94%D1%80%D1%83%D0%B3%D0%B8%D0%B5#Утилиты_запуска_приложений "Список приложений/Другие")

**Состояние перевода:** На этой странице представлен перевод статьи [Rofi](/index.php/Rofi "Rofi"). Дата последней синхронизации: 16 января 2020\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Rofi&diff=0&oldid=593734).

[Rofi](https://github.com/DaveDavenport/rofi) — переключатель окон, диалоговое окно для запуска приложений и ssh, а также замена [dmenu](/index.php/Dmenu_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dmenu (Русский)"). Разработка началась в качестве клона [simpleswitcher](https://github.com/seanpringle/simpleswitcher), написанного [Sean Pringle](https://github.com/seanpringle), а затем расширенного [Dave Davenport](https://github.com/DaveDavenport).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
*   [3 Rofi как замена dmenu](#Rofi_как_замена_dmenu)
*   [4 Выполнение команд оболочки из rofi](#Выполнение_команд_оболочки_из_rofi)
*   [5 Пользовательские темы](#Пользовательские_темы)
    *   [5.1 Предоставляемые темы](#Предоставляемые_темы)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [rofi](https://www.archlinux.org/packages/?name=rofi).

## Настройка

В настоящее время существует четыре способа задания параметров настроек:

*   Локальная настройка. Обычно, в зависимости от XDG, располагается в `~/.config/rofi/config`. Используется формат файлов Xresources.
*   Новый формат темы, который может содержать блок объявлений *configuration*: `~/.config/rofi/config.rasi`.
*   Xresources: значения ключей хранятся в Xserver.
*   Параметры командной строки.

**Примечание:** формат файлов Xresources устареет в будущих версиях *rofi*.

Поэтому команда

```
rofi -combi-modi window,drun,ssh -theme solarized -font "hack 10" -show combi

```

может быть описана в файле настроек следующим образом (новый формат темы):

```
configuration {
 modi: "window,drun,ssh,combi";
 theme: "solarized";
 font: "hack 10";
 combi-modi: "window,drun,ssh";
 }

```

Чтобы получить полный список параметров для файла `config.rasi`, выполните `rofi -dump-config`. Также можно записать вывод этой команды непосредственно в файл `config.rasi` с помощью `rofi -dump-config > ~/.config/rofi/config.rasi`.

**Примечание:** Пользователи i3 должны знать, что использование запятых в файле настроек i3 может привести к проблемам. Чтобы назначить запуск *rofi* на сочетание клавиш, используйте файл настроек *rofi* или замените запятые символом `#`, например: `rofi -combi-modi window#drun#ssh`.

## Rofi как замена dmenu

*Rofi* ведёт себя подобно *dmenu*, если вызывается с именем *dmenu* (через символическую ссылку). Можно установить пакет [rofi-dmenu](https://aur.archlinux.org/packages/rofi-dmenu/), который создаёт символическую ссылку *dmenu* на *rofi*. После этого программы, вызывающие *dmenu* (так же как и *passmenu* из [pass](/index.php/Pass "Pass")), будут использовать *rofi* вместо *dmenu*.

Чтобы *rofi* приобрёл внешний вид, приблизительно похожий на внешний вид *dmenu*, используйте следующие параметры:

```
rofi -show run -modi run -location 1 -width 100 \
		 -lines 2 -line-margin 0 -line-padding 1 \
		 -separator-style none -font "mono 10" -columns 9 -bw 0 \
		 -disable-history \
		 -hide-scrollbar \
		 -color-window "#222222, #222222, #b1b4b3" \
		 -color-normal "#222222, #b1b4b3, #222222, #005577, #b1b4b3" \
		 -color-active "#222222, #b1b4b3, #222222, #007763, #b1b4b3" \
		 -color-urgent "#222222, #b1b4b3, #222222, #77003d, #b1b4b3" \
		 -kb-row-select "Tab" -kb-row-tab ""

```

## Выполнение команд оболочки из rofi

Чтобы запускать команды оболочки или скрипты непосредственно из *rofi* с возможностью отображения вывода, сделайте следующее:

*   настройте переменную `PATH` в файле `~/.profile`, а не (например) в файле `~/.bashrc`, затем перезайдите в менеджер окон или среду рабочего стола;
*   установите параметр `-run-shell-command '{terminal} -e \\"{cmd}; read -n 1 -s"'`. Это позволит вводить команды в поле ввода, а затем после нажатия SHIFT+ENTER терминал останется открытым, пока не будет нажата какая-либо клавиша.

Пример для i3, использующий экранированную последовательность:

```
 bindsym $mod+d exec --no-startup-id "rofi -show drun -font \\"DejaVu 9\\" -run-shell-command '{terminal} -e \\" {cmd}; read -n 1 -s\\"'"

```

## Пользовательские темы

Чтобы просмотреть и применить темы для *rofi*, используйте следующую команду:

```
rofi-theme-selector

```

Настройки могут быть сохранены в файле [.Xresources](/index.php/X_resources_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "X resources (Русский)") (требуется пакет [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb)). Чтобы применить изменения, перезагрузите `.Xresources` с помощью `xrdb -load ~/.Xresources`.

### Предоставляемые темы

Смотрите официальный репозиторий [rofi-themes](https://github.com/DaveDavenport/rofi-themes), чтобы получить список доступных пользовательских тем.

Загрузите одну из тем `.rasi` и поместите её в `~/.config/rofi/example.rasi`. После этого загрузите тему с помощью параметра командной строки:

```
rofi <options> -theme example

```

или с помощью файла настроек:

```
rofi.theme:    example

```