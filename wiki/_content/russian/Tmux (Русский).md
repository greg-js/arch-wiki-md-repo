**Состояние перевода:** На этой странице представлен перевод статьи [Tmux](/index.php/Tmux "Tmux"). Дата последней синхронизации: 5 сентября 2015‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Tmux&diff=0&oldid=398381).

[Tmux](http://tmux.sourceforge.net/) — терминальный мультиплексор берущий своё начало из мира BSD. Он позволяет создавать несколько терминалов (или окон), каждый из которых выполняет отдельную программу, а так же управлять этими терминалами на одном экране. tmux может быть отвязан от экрана и продолжать свою работу в фоновом режиме, а позже — привязан вновь. Он использует библиотеку ncurses.

Во многом, он похож на программу [GNU Screen](/index.php/Screen_Tips "Screen Tips"), но имеет некоторые отличия. (Кто сказал улучшения?) За более подробной информацией обращайтесь на [официальный вебсайт](http://tmux.sourceforge.net/).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Клавиши управления](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [2.1.1 Copy Mode](#Copy_Mode)
    *   [2.2 Переход по URL](#.D0.9F.D0.B5.D1.80.D0.B5.D1.85.D0.BE.D0.B4_.D0.BF.D0.BE_URL)
    *   [2.3 Правильное определение терминала](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
    *   [2.4 Другие настройки](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [2.5 Автозапуск посредством systemd](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D0.BE.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.BE.D0.BC_systemd)
*   [3 Инициализация сеансов](#.D0.98.D0.BD.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.BE.D0.B2)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Проблемы с прокруткой](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.BE.D0.B9)
    *   [4.2 Mouse scrolling](#Mouse_scrolling)
    *   [4.3 Fix reverse-video/italic mode in urxvt](#Fix_reverse-video.2Fitalic_mode_in_urxvt)
    *   [4.4 Shift+F6 не работает в Midnight Commander](#Shift.2BF6_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.B2_Midnight_Commander)
*   [5 X clipboard integration](#X_clipboard_integration)
    *   [5.1 Urxvt middle click](#Urxvt_middle_click)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Start tmux with default session layout](#Start_tmux_with_default_session_layout)
        *   [6.1.1 Get the default layout values](#Get_the_default_layout_values)
        *   [6.1.2 Define the default tmux layout](#Define_the_default_tmux_layout)
        *   [6.1.3 Autostart tmux with default tmux layout](#Autostart_tmux_with_default_tmux_layout)
        *   [6.1.4 Alternate approach for default session](#Alternate_approach_for_default_session)
    *   [6.2 Start tmux in urxvt](#Start_tmux_in_urxvt)
    *   [6.3 Start tmux on every shell login](#Start_tmux_on_every_shell_login)
    *   [6.4 Start a non-login shell](#Start_a_non-login_shell)
    *   [6.5 Use tmux windows like tabs](#Use_tmux_windows_like_tabs)
    *   [6.6 Clients simultaneously interacting with various windows of a session](#Clients_simultaneously_interacting_with_various_windows_of_a_session)
    *   [6.7 Correct the TERM variable according to terminal type](#Correct_the_TERM_variable_according_to_terminal_type)
    *   [6.8 Изменить конфигурацию при запущенном tmux](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8E_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.89.D0.B5.D0.BD.D0.BD.D0.BE.D0.BC_tmux)
    *   [6.9 Template script to run program in new session resp. attach to existing one](#Template_script_to_run_program_in_new_session_resp._attach_to_existing_one)
    *   [6.10 Terminal emulator window titles](#Terminal_emulator_window_titles)
    *   [6.11 Automatic layouting](#Automatic_layouting)
    *   [6.12 Vim friendly configuration](#Vim_friendly_configuration)
    *   [6.13 Prevent tmux freezing when lots of text is sent to output](#Prevent_tmux_freezing_when_lots_of_text_is_sent_to_output)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Pacman "Pacman") пакет [tmux](https://www.archlinux.org/packages/?name=tmux) доступный в [официальных репозиториях](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D1%85 "Официальных репозиториях").

## Настройка

Пользовательский файл настроек должен быть расположен в `~/.tmux.conf`, в то время как глобальный — в `/etc/tmux.conf`. Стандартные конфигурационные файлы размещены в директории `/usr/share/tmux/`.

### Клавиши управления

По умолчанию, клавишами перехода в режим управления является комбинация клавиш `Ctrl-b`. Например, для вертикального разделения окна `Ctrl-b+%`.

После разделения окна на несколько панелей, панели могут быть изменены, используя следующее сочетание клавиш: `Ctrl-b`) и, продолжая удерживать Ctrl, нажмите клавишу вправо/влево/вверх/вниз. Менять панели местами можно таким же способом, только с нажатием _o_ вместо клавиш направления.

**Совет:** Для имитации управления аналогично [screen](/index.php/GNU_Screen_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNU Screen (Русский)") используйте содержимое файла `/usr/share/tmux/screen-keys.conf` в качестве рабочего конфигурационного.

Привязки клавиш для различных команд могут быть изменены в `tmux.conf`. Например, модификатор управления `Ctrl-b` может быть изменен на `Ctrl-a` после добавления следующих команд в конфигурационном файле:

```
unbind C-b
set -g prefix C-a
bind C-a send-prefix

```

**Совет:** В качестве префикса выступает клавиша модификатор. Вы также можете использовать `Alt` вместо `Ctrl`, указав: `set -g prefix m-'\'`

Управление панелями:

```
Ctrl-b %  (Разделить окно вертикально)
Ctrl-b "  “split-window” (Разделить окно горизонтально)
Ctrl-b o или Ctrl-b Tab (Перейти к следующей панели)
Ctrl-b {  (Переместить текущую панель влево)
Ctrl-b }  (Переместить текущую панель вправо)

```

Управление окнами:

```
Ctrl-b c  создать новое окно 
Ctrl-b ,.  переименовать текущее окно — введите новое имя и нажмите Enter
Ctrl-b l (Переход предыдущему окну)
Ctrl-b w (Список всех окон с нумерацией)
Ctrl-b <window number> (Перемещение по указанному номеру окна, по умолчанию в диапазоне от 0 до 9)
Ctrl-b q  (Показать номера панелей; перейти в область по нажатии клавиши, соответствующей номеру)

```

Для удобной навигации со множеством окон tmux имеет возможность поиска, используя комбинации клавиш:

```
Ctrl-b f <window name> (Поиск по названию окна)
Ctrl-b w (Выбор окна из интерактивного списка)

```

#### Copy Mode

A tmux window may be in one of several modes. The default permits direct access to the terminal attached to the window; the other is copy mode. Once in copy mode you can navigate the buffer including scrolling the history. Use vi or emacs-style key bindings in copy mode. The default is emacs, unless VISUAL or EDITOR contains ‘vi’

To enter copy mode do the following:

```
Ctrl-b [

```

You can navigate the buffer as you would in your default editor.

To quit copy mode, use one of the following keybindings:

vi mode:

```
q

```

emacs mode:

```
Esc

```

### Переход по URL

Чтобы перейти по URL, который появляется в tmux, должен быть установлен и настроен [urlview](https://aur.archlinux.org/packages/urlview/).

С открытием нового терминала:

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; run-shell "$TERMINAL -e urlview /tmp/tmux-buffer"

```

С открытием нового окна tmux:

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; new-window -n "urlview" '$SHELL -c "urlview < /tmp/tmux-buffer"'

```

### Правильное определение терминала

Если вы используете 256-цветный терминал, то понадобится скорректировать его в tmux. Для этого укажите в `tmux.conf`:

```
set -g default-terminal "screen-256color" 

```

Если клавиши xterm будут активированы в `tmux.conf`, то вам потребуется пересобрать библиотеку terminfo для объявления новых управляющих символов, иначе приложения могут их не распознать. После составления следующего в `tic` вы сможете использовать "xterm-screen-256color" в качестве вашего TERM:

```
# A screen- based TERMINFO that declares the escape sequences
# enabled by the tmux config "set-window-option -g xterm-keys".
#
# Prefix the name with xterm- since some applications inspect
# the TERM *name* in addition to the terminal capabilities advertised.
xterm-screen-256color|GNU Screen with 256 colors bce and tmux xterm-keys,

# As of Nov'11, the below keys are picked up by
# .../tmux/blob/master/trunk/xterm-keys.c:
	kDC=\E[3;2~, kEND=\E[1;2F, kHOM=\E[1;2H,
	kIC=\E[2;2~, kLFT=\E[1;2D, kNXT=\E[6;2~, kPRV=\E[5;2~,
	kRIT=\E[1;2C,

# Change this to screen-256color if the terminal you run tmux in
# doesn't support bce:
	use=screen-256color-bce,

```

### Другие настройки

Установить возможность скроллинга до 10000 строк:

```
set -g history-limit 10000

```

Режим копирования на клавише "Esc":

```
unbind [
bind Escape copy-mode

```

Переместить буфер обмена tmux в буфер обмена X:

```
bind-key C-y save-buffer /tmp/tmux-buffer \; run-shell "cat /tmp/tmux-buffer | xclip"

```

Часы, вызываемые Ctrl-b t:

```
set-window-option -g clock-mode-colour cyan
set-window-option -g clock-mode-style 24

```

Отключить визуальную активность:

```
set -g visual-activity off
set -g visual-bell off

```

Заголовок окна

```
set-option -g set-titles on
set-option -g set-titles-string '#S:#I.#P #W' # window number,program name,active (or not)
set-window-option -g automatic-rename on # auto name

```

Сообщения

```
#set-window-option -g mode-bg magenta
#set-window-option -g mode-fg black
#set-option -g message-bg magenta
#set-option -g message-fg black

```

Панель состояния

```
set-option -g status-utf8 on
set-option -g status-justify right
set-option -g status-bg black
set-option -g status-fg cyan
set-option -g status-interval 5
set-option -g status-left-length 30
set-option -g status-left '#[fg=magenta]» #[fg=blue,bold]#T#[default]'
set-option -g status-right '#[fg=cyan]»» #[fg=blue,bold]###S #[fg=magenta]%R %m-%d#(acpi | cut -d ',' -f 2)#[default]'
set-option -g visual-activity on
set-window-option -g monitor-activity on
set-window-option -g window-status-current-fg white

```

### Автозапуск посредством systemd

Есть некоторые заметные преимущества в запуске сервера tmux при загрузке. Новый сеанс tmux начнется значительно быстрее, если служба была запущена.

Кроме того, ваш сеанс tmux будет сохранен вместе со всеми изменениями, даже если на текущий момент вход в систему не выполнен

Следующий файл-юнит позволит запускать _tmux_ как службу для указанного пользователя (имея название вида `tmux@_имя пользователя_.service`):

 `/etc/systemd/system/tmux@.service` 

```
[Unit]
Description=Start tmux in detached session

[Service]
Type=forking
User=%I
ExecStart=/usr/bin/tmux new-session -s %u -d
ExecStop=/usr/bin/tmux kill-session -t %u

[Install]
WantedBy=multi-user.target

```

**Совет:** You may want to add `WorkingDirectory=_custom_path_` to customize working directory.

Кроме того, вы можете разместить этот файл в ваш [пользовательский](/index.php/Systemd/User "Systemd/User") каталог, например в `~/.config/systemd/user/tmux.service`. Таким образом, служба tmux запустится сразу после входа в систему.

## Инициализация сеансов

Можно настроить tmux таким образом, чтобы он запускался с предопределённым набором окон, добавив следующие команды в ваш `.tmux.conf`:

```
new  -n WindowName Command
neww -n WindowName Command
neww -n WindowName Command

```

Чтобы запустить сеанс с разделёнными окнами (панелями), добавьте команду splitw после neww, таким образом:

```
new  -s SessionName -n WindowName Command
neww -n foo/bar foo
splitw -v -p 50 -t 0 bar
selectw -t 1 
selectp -t 0

```

откроет два окна, второе из которых будет называться foo/bar и будет разделено вертикально пополам с командой foo запущенной перед командой bar. Фокус будет передан второму окну(foo/bar), левой панели (foo).

**Обратите внимание:** Нумерация сеансов, окон и панелей начинается с нуля, если не указан параметр base-index со значением 1 в `.tmux.conf`

Чтобы управлять несколькими сеансами, подключайте раздельные файлы сеансов в конфигурационном файле:

```
# инициализация сеансов
bind F source-file ~/.tmux/foo
bind B source-file ~/.tmux/bar

```

## Решение проблем

### Проблемы с прокруткой

Если у вас проблемы с прокруткой клавишами Shift-PageUp/Shift-PageDown в терминале, попробуйте следующее:

```
set -g terminal-overrides 'xterm*:smcup@:rmcup@'

```

Если возникают проблемы с прокруткой клавишами Shift-Page Up/Down в терминале, укажите следующую команду в `tmux.conf`. Она отключит возможности smcup и rmcup в любом поддерживающем их терминале, в том числе `xterm`:

```
set -ga terminal-overrides ',xterm*:smcup@:rmcup@'

```

This tricks the terminal emulator into thinking Tmux is a full screen application like pico or mutt[[1]](http://superuser.com/questions/310251/use-terminal-scrollbar-with-tmux), which will make the scrollback be recorded properly. Beware however, it will get a bit messed up when switching between windows/panes. Consider using Tmux's native scrollback instead.

### Mouse scrolling

**Note:** This interferes with selection buffer copying and pasting. To copy/paste to/from the selection buffer hold the shift key.

If you want to scroll with your mouse wheel, ensure mode-mouse is on in .tmux.conf

```
setw -g mode-mouse on

```

You can set scroll History with:

```
set -g history-limit 30000

```

### Fix reverse-video/italic mode in urxvt

If your reverse-video and italic modes are reversed, you may follow these instructions. This happens for example in vim when italics are replaced by highlighting, or in less when the search highlighting is replaced by italics. This is because the screen terminfo doesn't define italics, and the italics escape of urxvt happens to be the standout escape defined in the terminfo. In this solution, you may replace `screen_terminfo="screen"` by `screen_terminfo="screen-256color"`.

```
 mkdir $HOME/.terminfo/
 screen_terminfo="screen"

```

Create a new terminfo adding the italic escape code:

```
 infocmp "$screen_terminfo" | sed \
 -e 's/^screen[^|]*|[^,]*,/screen-it|screen with italics support,/' \
 -e 's/%?%p1%t;3%/%?%p1%t;7%/' \
 -e 's/smso=[^,]*,/smso=\\E[7m,/' \
 -e 's/rmso=[^,]*,/rmso=\\E[27m,/' \
 -e '$s/$/ sitm=\\E[3m, ritm=\\E[23m,/' > /tmp/screen.terminfo

```

Compile this terminfo:

```
 tic /tmp/screen.terminfo

```

Then, you must add the following line in your tmux.conf. If you already defined `default-terminal`, just replace it.

```
 set -g default-terminal "screen-it"

```

The source of this solution can be found at [[2]](http://tmux.svn.sourceforge.net/viewvc/tmux/trunk/FAQ), in the section entitled "vim displays reverse video instead of italics, while less displays italics (or just regular text) instead of reverse. What's wrong?".

### Shift+F6 не работает в Midnight Commander

Если не работает сочитание клавиш `Shift+F6` с `TERM=screen` или с `TERM=screen-256color`, то попробуйте выполнить следующую команду из tmux:

```
infocmp > screen (or screen-256color)

```

Откройте файл в текстовом редакторе и добавьте следующую строку в конце файла:

```
kf16=\E[29~,

```

Затем скомпилируйте файл с `tic`. После чего клавиши будут работать.

## X clipboard integration

**Tip:** The tmux plugin [tmux-yank](https://github.com/tmux-plugins/tmux-yank) provides similar functionality.

It is possible to copy tmux selection to X clipboard (and to X primary/secondary selection) and in reverse direction. The following tmux config file snippet effectively integrates X clipboard/selection with the current tmux selection using the program [xsel](https://www.archlinux.org/packages/?name=xsel):

```
# Emacs style
bind-key -t emacs-copy M-w copy-pipe "xsel -i -p -b"
bind-key C-y run "xsel -o | tmux load-buffer - ; tmux paste-buffer"

```

```
# Vim style
bind-key -t vi-copy y copy-pipe "xsel -i -p -b"
bind-key p run "xsel -o | tmux load-buffer - ; tmux paste-buffer"

```

It is encouraged to use `xsel` instead of `xclip`, because xclip does not close STDOUT after it has read from tmux's buffer. As such, tmux doesn't know that the copy task has completed, and continues to wait for xclip's termination, thereby rendering tmux unresponsive.

### Urxvt middle click

**Note:** To use this, you need to enable mouse support

There is an unofficial perl extension (mentioned in the official [FAQ](http://sourceforge.net/p/tmux/tmux-code/ci/master/tree/FAQ)) to enable copying/pasting in and out of urxvt with tmux via Middle Mouse Clicking.

First, you will need to download the perl script and place it into urxvts perl lib:

```
wget [http://anti.teamidiot.de/static/nei/*/Code/urxvt/osc-xterm-clipboard](http://anti.teamidiot.de/static/nei/*/Code/urxvt/osc-xterm-clipboard)
mv osc-xterm-clipboard /usr/lib/urxvt/perl/
```

You will also need to enable that perl script in your .Xdefaults:

 `~/.Xdefaults` 

```
...
*URxvt.perl-ext-common:		osc-xterm-clipboard
...

```

Next, you want to tell tmux about the new function and enable mouse support (if you haven't already). The third option is optional, to enable scrolling and selecting inside panes with your mouse:

 `~/.tmux.conf` 

```
...
set-option -ga terminal-override ',rxvt-uni*:XT:Ms=\E]52;%p1%s;%p2%s\007'
set-window-option -g mode-mouse on
set-option -g mouse-select-pane on
...

```

That's it. Be sure to end all instances of tmux before trying the new MiddleClick functionality.

While in tmux, Shift+MiddleMouseClick will paste the clipboard selection while just MiddleMouseClick will paste your tmux buffer. Outside of tmux, just use MiddleMouseClick to paste your tmux buffer and your standard Ctrl-c to copy.

## Tips and tricks

### Start tmux with default session layout

To setup your default Tmux session layout, you install [tmuxinator](https://aur.archlinux.org/packages/tmuxinator/) from [AUR](/index.php/AUR "AUR"). Test your installation with

```
tmuxinator doctor

```

#### Get the default layout values

Start Tmux as usual and configure your windows and panes layout as you like. When finished, get the current layout values by executing (while you are still within the current Tmux session)

```
tmux list-windows

```

The output may look like this (two windows with 3 panes and 2 panes layout)

```
0: default* (3 panes) [274x83] [layout 20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}] @2 (active)
1: remote- (2 panes) [274x83] [layout e3d3,274x83,0,0[274x41,0,0,4,274x41,0,42,7]] @3                                         

```

The Interesting part you need to copy for later use begins after **[layout...** and excludes **... ] @2 (active)**. For the first window layout you need to copy e.g. **20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}**

#### Define the default tmux layout

Knowing this, you can exit the current tmux session. Following this, you create your default Tmux session layout by editing Tmuxinator's config file (Don't copy the example, get your layout values as described above)

 `~/.tmuxinator/default.yml` 

```
name: default
root: ~/
windows:
  - default:
      layout: 20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}
      panes:
        - clear
        - vim
        - clear && emacs -nw
  - remote:
      layout: 24ab,274x83,0,0{137x83,0,0,3,136x83,138,0,4}
      panes:
        - 
        - 

```

The example defines two windows named "default" and "remote". With your determined layout values. For each pane you have to use at least one `-` line. Within the first window panes you start the commandline "clear" in pane one, "vim" in pane two and "clear && emacs -nw" executes two commands in pane three on each Tmux start. The second window layout has two panes without defining any start commmands.

Test the new default layout with (yes, it is "mux"):

```
mux default

```

#### Autostart tmux with default tmux layout

If you like to start your terminal session with your default Tmux session layout edit

 `~/.bashrc` 

```
 if [ -z "$TMUX" ]; then
   mux default          
 fi                     

```

#### Alternate approach for default session

Instead of using the above method, one can just write a bash script that when run, will create the default session and attach to it. Then you can execute it from a terminal to get the pre-designed configuration in that terminal

```
#!/bin/bash
tmux new-session -d -n WindowName Command
tmux new-window -n NewWindowName
tmux split-window -v
tmux selectp -t 1
tmux split-window -h
tmux selectw -t 1
tmux -2 attach-session -d

```

### Start tmux in urxvt

Use this command to start urxvt with a started tmux session. I use this with the exec command from my .ratpoisonrc file.

 `urxvt -e bash -c "tmux -q has-session && exec tmux attach-session -d || exec tmux new-session -n$USER -s$USER@$HOSTNAME"` 

### Start tmux on every shell login

Simply add the following line of bash code to your .bashrc before your aliases; the code for other shells is very similar:

 `~/.bashrc` 

```
# If not running interactively, do not do anything
[[ $- != *i* ]] && return
[[ -z "$TMUX" ]] && exec tmux

```

**Note:** This snippet ensures that tmux is not launched inside of itself (something tmux usually already checks for anyway). tmux sets $TMUX to the socket it is using whenever it runs, so if $TMUX isn't set or is length 0, we know we aren't already running tmux.

Add the following snippet to start only one session (unless you start some manually), on login, try attach at first, only create a session if no tmux is running.

```
# TMUX
if which tmux >/dev/null 2>&1; then
    #if not inside a tmux session, and if no session is started, start a new session
    test -z "$TMUX" && (tmux attach || tmux new-session)
fi

```

The following snippet does the same thing, but also checks tmux is installed before trying to launch it. It also tries to reattach you to an existing tmux session at logout, so that you can shut down every tmux session quickly from the same terminal at logout.

```
# TMUX
if which tmux >/dev/null 2>&1; then
    # if no session is started, start a new session
    test -z ${TMUX} && tmux

    # when quitting tmux, try to attach
    while test -z ${TMUX}; do
        tmux attach || break
    done
fi

```

Another possibility is to try to attach to existing deattached session or start a new session:

```
if [[ -z "$TMUX" ]] ;then
    ID="`tmux ls | grep -vm1 attached | cut -d: -f1`" # get the id of a deattached session
    if [[ -z "$ID" ]] ;then # if not available create a new one
        tmux new-session
    else
        tmux attach-session -t "$ID" # if available attach to it
    fi
fi

```

**Note:** Instead of using the bashrc file, you can launch tmux when you start your terminal emulator. (i. e. urxvt -e tmux)

### Start a non-login shell

Tmux starts a [login shell](http://unix.stackexchange.com/questions/38175) [by default](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/5997), which may result in multiple negative side effects:

*   Users of [fortune](https://en.wikipedia.org/wiki/fortune_(Unix) "wikipedia:fortune (Unix)") may notice that quotes are printed when creating a new panel.
*   The configuration files for login shells such as `~/.profile` are interpreted each time a new panel is created, so commands intended to be run on session initialization (e.g. setting audio level) are executed.

To disable this behaviour, add to `~/.tmux.conf`:

```
set -g default-command "${SHELL}"

```

### Use tmux windows like tabs

The following settings added to `~/.tmux.conf` allow to use tmux windows like tabs, such as those provided by the reference of these hotkeys — [urxvt's tabbing extensions](/index.php/Rxvt-unicode#urxvtq_with_tabbing "Rxvt-unicode"). An advantage thereof is that these virtual “tabs” are independent of the terminal emulator.

```
#urxvt tab like window switching (-n: no prior escape seq)
bind -n S-down new-window
bind -n S-left prev
bind -n S-right next
bind -n C-left swap-window -t -1
bind -n C-right swap-window -t +1

```

Of course, those should not overlap with other applications' hotkeys, such as the terminal's. Given that they substitute terminal tabbing that might as well be deactivated, though.

It can also come handy to supplement the EOT hotkey `Ctrl+d` with one for tmux's detach:

```
bind-key -n C-j detach

```

### Clients simultaneously interacting with various windows of a session

In [Practical Tmux](http://mutelight.org/articles/practical-tmux), Brandur Leach writes:

	Screen and tmux's behaviour for when multiple clients are attached to one session differs slightly. In Screen, each client can be connected to the session but view different windows within it, but in tmux, all clients connected to one session must view the same window.

	This problem can be solved in tmux by spawning two separate sessions and synchronizing the second one to the windows of the first, then pointing a second new session to the first.

The script “`tmx`” below implements this — the version here is slightly modified to execute “`tmux new-window`” if “1” is its second parameter. Invoked as `tmx <base session name> [1]` it launches the base session if necessary. Otherwise a new “client” session linked to the base, optionally add a new window and attach, setting it to kill itself once it turns “zombie”.

 `tmx` 

```
#!/bin/bash

#
# Modified TMUX start script from:
#     http://forums.gentoo.org/viewtopic-t-836006-start-0.html
#
# Store it to `~/bin/tmx` and issue `chmod +x`.
#

# Works because bash automatically trims by assigning to variables and by 
# passing arguments
trim() { echo $1; }

if [[ -z "$1" ]]; then
    echo "Specify session name as the first argument"
    exit
fi

# Only because I often issue `ls` to this script by accident
if [[ "$1" == "ls" ]]; then
    tmux ls
    exit
fi

base_session="$1"
# This actually works without the trim() on all systems except OSX
tmux_nb=$(trim `tmux ls | grep "^$base_session" | wc -l`)
if [[ "$tmux_nb" == "0" ]]; then
    echo "Launching tmux base session $base_session ..."
    tmux new-session -s $base_session
else
    # Make sure we are not already in a tmux session
    if [[ -z "$TMUX" ]]; then
        echo "Launching copy of base session $base_session ..."
        # Session id is date and time to prevent conflict
        session_id=`date +%Y%m%d%H%M%S`
        # Create a new session (without attaching it) and link to base session 
        # to share windows
        tmux new-session -d -t $base_session -s $session_id
        if [[ "$2" == "1" ]]; then
		# Create a new window in that session
		tmux new-window
	fi
        # Attach to the new session & kill it once orphaned
	tmux attach-session -t $session_id \; set-option destroy-unattached
    fi
fi

```

A useful setting for this is

```
setw -g aggressive-resize on

```

added to `~/.tmux.conf`. It causes tmux to resize a window based on the smallest client actually viewing it, not on the smallest one attached to the entire session.

An alternative taken from [[3]](http://sourceforge.net/mailarchive/forum.php?thread_name=CAPBqLKEC0MAFR%2BWUYqCuyd%3DKB47HK8CFSuAf%3Dd%3DW2H3F4fpMZw%40mail.gmail.com&forum_name=tmux-users) is to put the following ~/.bashrc:

 `.bashrc` 

```
function rsc() {
  CLIENTID=$1.`date +%S`
  tmux new-session -d -t $1 -s $CLIENTID \; set-option destroy-unattached \; attach-session -t $CLIENTID
}

function mksc() {
  tmux new-session -d -s $1
  rsc $1
}

```

Citing the author:

	"mksc foo" creates a always detached permanent client named "foo". It also calls "rsc foo" to create a client to newly created session. "rsc foo" creates a new client grouped by "foo" name. It has destroy-unattached turned on so when I leave it, it kills client.

	Therefore, when my computer looses network connectivity, all "foo.something" clients are killed while "foo" remains. I can then call "rsc foo" to continue work from where I stopped.

### Correct the TERM variable according to terminal type

Instead of [setting a fixed TERM variable in tmux](#Setting_the_correct_term), it is possible to set the proper TERM (either `screen` or `screen-256color`) according to the type of your terminal emulator:

 `~/.tmux.conf` 

```
## set the default TERM
set -g default-terminal screen

## update the TERM variable of terminal emulator when creating a new session or attaching a existing session
set -g update-environment 'DISPLAY SSH_ASKPASS SSH_AGENT_PID SSH_CONNECTION WINDOWID XAUTHORITY TERM'
## determine if we should enable 256-colour support
if "[[ ${TERM} =~ 256color || ${TERM} == fbterm ]]" 'set -g default-terminal screen-256color'

```

 `~/.zshrc` 

```
## workaround for handling TERM variable in multiple tmux sessions properly from [http://sourceforge.net/p/tmux/mailman/message/32751663/](http://sourceforge.net/p/tmux/mailman/message/32751663/) by Nicholas Marriott
if [[ -n ${TMUX} && -n ${commands[tmux]} ]];then
        case $(tmux showenv TERM 2>/dev/null) in
                *256color) ;&
                TERM=fbterm)
                        TERM=screen-256color ;;
                *)
                        TERM=screen
        esac
fi
```

### Изменить конфигурацию при запущенном tmux

По умолчанию tmux считывает `~/.tmux.conf` только тогда, когда он не был еще запущен. Для того, чтобы tmux загрузить файл конфигурации после запуска, выполните:

```
tmux source-file <path>

```

Можно назначит хоткей для этого, добавив в `~/.tmux.conf`, например:

```
bind r source-file <path>

```

Или же нажать `Ctrl-b :` и набрать:

```
source-file <path>

```

### Template script to run program in new session resp. attach to existing one

This script checks for a program presumed to have been started by a previous run of itself. Unless found it creates a new tmux session and attaches to a window named after and running the program. If however the program was found it merely attaches to the session and selects the window.

```
#!/bin/bash

PID=$(pidof $1)

if [ -z "$PID" ]; then
    tmux new-session -d -s main ;
    tmux new-window -t main -n $1 "$*" ;
fi
    tmux attach-session -d -t main ;
    tmux select-window -t $1 ;
exit 0

```

A derived version to run _irssi_ with the _nicklist_ plugin can be found on [its ArchWiki page](/index.php/Irssi#irssi_with_nicklist_in_tmux "Irssi").

### Terminal emulator window titles

If you SSH into a host in a tmux window, you'll notice the window title of your terminal emulator remains to be `user@localhost` rather than `user@server`. To allow the title bar to adapt to whatever host you connect to, set the following in `~/.tmux.conf`

```
set -g set-titles on
set -g set-titles-string "#T"

```

For `set-titles-string`, `#T` will display `user@host:~` and change accordingly as you connect to different hosts.

### Automatic layouting

When creating new splits or destroying older ones the currently selected layout isn't applied. To fix that, add following binds which will apply the currently selected layout to new or remaining panes:

```
bind-key -n M-c kill-pane \; select-layout
bind-key -n M-n split-window \; select-layout

```

### Vim friendly configuration

See [[4]](https://gist.github.com/anonymous/6bebae3eb9f7b972e6f0) for a configuration friendly to [vim](/index.php/Vim "Vim") users.

### Prevent tmux freezing when lots of text is sent to output

If a program run inside tmux runs amok and starts printing lots of output, tmux tends to hang and `Ctrl+C` does not get through. This can be prevented by limiting how much text is printed to the console at any time.

```
setw -g c0-change-trigger 10
setw -g c0-change-interval 250

```

## Смотрите также

*   [Ветка про Tmux на форумах Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=84157&p=1) (англ.)
*   [Сравнение Screen и tmux](http://www.dayid.org/os/notes/tm.html) (англ.)
*   [powerline](https://github.com/Lokaltog/powerline) - плагин для vim, реализующий динамический статус бар, совместимый со множеством приложений, в том числе с tmux.
*   [Плагины для tmux](https://github.com/tmux-plugins)

**Учебники**

*   [Приручаем Tmux для повседневных нужд](http://habrahabr.ru/post/165437/)
*   [Practical Tmux](http://mutelight.org/articles/practical-tmux) (англ.)
*   [Tmux FAQ (OpenBSD)](http://www.openbsd.org/faq/faq7.html#tmux) (англ.)
*   [man page (OpenBSD)](http://www.openbsd.org/cgi-bin/man.cgi?query=tmux) (англ.)
*   [Tmux tutorial Part 1](http://blog.hawkhost.com/2010/06/28/tmux-the-terminal-multiplexer/) and [Part 2](http://blog.hawkhost.com/2010/07/02/tmux-%E2%80%93-the-terminal-multiplexer-part-2) (англ.)