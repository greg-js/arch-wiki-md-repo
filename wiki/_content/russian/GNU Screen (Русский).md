[GNU Screen](http://www.gnu.org/s/screen/) - обертка, которая позволяет отделить консольную программу от терминала. Например, screen позволяется пользователям запустить консольную программу в одном из терминальных эмуляторов под X, закрыть его и продолжить работу с программой в другом терминале. В данной статье приведены различные советы и рекомендации по использованию screen.

Если вы ищете пошаговое руководство, то его можно найти на gentoo wiki: [http://wiki.gentoo.org/wiki/Screen](http://wiki.gentoo.org/wiki/Screen)

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Основы](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D1.8B)
    *   [2.1 Стандартные команды](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D1.8B)
*   [3 Запуск в окне 1](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2_.D0.BE.D0.BA.D0.BD.D0.B5_1)
*   [4 Вложенные сессии screen](#.D0.92.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8_screen)
*   [5 Исправление проблемы с остатками текста](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BE.D1.81.D1.82.D0.B0.D1.82.D0.BA.D0.B0.D0.BC.D0.B8_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.B0)
*   [6 Используем 256 цветов](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC_256_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2)
*   [7 Используем 256 цветов в Rxvt-Unicode (urxvt)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC_256_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2_.D0.B2_Rxvt-Unicode_.28urxvt.29)
*   [8 Информационный статус-бар](#.D0.98.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D1.8B.D0.B9_.D1.81.D1.82.D0.B0.D1.82.D1.83.D1.81-.D0.B1.D0.B0.D1.80)
*   [9 Отключаем приветственное сообщение](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B0.D0.B5.D0.BC_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.81.D0.BE.D0.BE.D0.B1.D1.89.D0.B5.D0.BD.D0.B8.D0.B5)
*   [10 Превращаем строку хард-статуса в динамический заголовок окна urxvt|xterm|aterm](#.D0.9F.D1.80.D0.B5.D0.B2.D1.80.D0.B0.D1.89.D0.B0.D0.B5.D0.BC_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D1.83_.D1.85.D0.B0.D1.80.D0.B4-.D1.81.D1.82.D0.B0.D1.82.D1.83.D1.81.D0.B0_.D0.B2_.D0.B4.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.B3.D0.BE.D0.BB.D0.BE.D0.B2.D0.BE.D0.BA_.D0.BE.D0.BA.D0.BD.D0.B0_urxvt.7Cxterm.7Caterm)
*   [11 Используем механизм прокрутки X](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC_.D0.BC.D0.B5.D1.85.D0.B0.D0.BD.D0.B8.D0.B7.D0.BC_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8_X)
*   [12 Добавляем пункт в GRUB для загрузки в Screen](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D1.8F.D0.B5.D0.BC_.D0.BF.D1.83.D0.BD.D0.BA.D1.82_.D0.B2_GRUB_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.B2_Screen)
*   [13 Исправляем зависание Midnight Commander при запуске в screen](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D1.8F.D0.B5.D0.BC_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_Midnight_Commander_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.B2_screen)
*   [14 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

GNU Screen можно установить из репозитория extra:

```
# pacman -S screen

```

## Основы

Команды вводятся после нажатия Ctrl+A. Данная комбинация настраивается опцией _escape_ в ~/.screenrc. Пример:

```
escape ``

```

устанавливает escape-команду на клавишу `

### Стандартные команды

*   `ctrl+a` `?` Отображает список команд и их параметры по умолчанию
*   `ctrl+a` `:` Ввод команды для screen
*   `ctrl+a` `"` Список окон
*   `ctrl+a` `0` Открыть окно 0
*   `ctrl+a` `A` Переименовать текущее окно
*   `ctrl+a` `a` Отправить `ctrl+a` в текущее окно
*   `ctrl+a` `c` Создать новое окно
*   `ctrl+a` `S` Разделить текущее окно на два региона
*   `ctrl+a` `tab` Переключить фокус ввода на следующий регион
*   `ctrl+a` `ctrl+a` Переключение между текущим и предыдущим регионами
*   `ctrl+a` `Esc` Перейти в режим копирования (используйте enter для выделения текста)
*   `ctrl+a` `]` Вставка текста
*   `ctrl+a` `Q` Закрыть все регионы кроме текущего
*   `ctrl+a` `X` Закрыть текущий регион
*   `ctrl+a` `d` Отключиться от текущей сессии screen, оставив ее работающей. Для переподключения используйте `screen -r`

## Запуск в окне 1

По умолчанию, первое окно screen имеет номер 0\. Возможно, вы предпочтете начать с нумерацию с единицы, добавьте это в ~/.screenrc:

```
bind c screen 1
bind ^c screen 1
bind 0 select 10                                                            
screen 1

```

## Вложенные сессии screen

It's possible to get stuck in a nested screen session. A common scenario: you start an ssh session from within a screen session. Within the ssh session, you start screen. By default, the outer screen session that was launched first responds to C-a commands. To send a command to the inner screen session, use C-a a, followed by your command. For example:

C-a a d

	Detaches the inner screen session.

C-a a K

	Kills the inner screen session.

## Исправление проблемы с остатками текста

When you open a text editor like nano in screen and then close it, the text may stay visible in your terminal. To fix this, put the following in your ~/.screenrc:

```
altscreen on

```

## Используем 256 цветов

By default, screen uses an 8-color terminal emulator. Use the following line to enable more colors, which is useful if you are using a more-capable terminal emulator:

```
term screen-256color

```

If this fails to render 256 colors in [xterm](/index.php/Xterm "Xterm"), try the following instead:

```
attrcolor b ".I"    # allow bold colors - necessary for some reason
termcapinfo xterm 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'   # tell screen how to set colors. AB = background, AF=foreground
defbce on    # use current bg color for erased chars

```

## Используем 256 цветов в Rxvt-Unicode (urxvt)

If you are using `rxvt-unicode-256color` from `[community]`, you may need to add this line in your `~/.screenrc` to enable 256 colors while in screen.

```
terminfo rxvt-unicode 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'

```

## Информационный статус-бар

The default statusbar may be a little lacking. You may find this one more helpful:

```
hardstatus off
hardstatus alwayslastline
hardstatus string '%{= kG}[ %{G}%H %{g}][%= %{= kw}%?%-Lw%?%{r}(%{W}%n*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}][%{B} %m-%d
 %{W} %c %{g}]'

```

## Отключаем приветственное сообщение

Add to ~/.screenrc:

```
startup_message off

```

## Превращаем строку хард-статуса в динамический заголовок окна urxvt|xterm|aterm

This one's pretty simple; just switch your current hardstatus line into a caption line with notification, and edit accordingly:

```
backtick 1 5 5 true
termcapinfo rxvt* 'hs:ts=\E]2;:fs=\007:ds=\E]2;\007'
hardstatus string "screen (%n: %t)"
caption string "%{= kw}%Y-%m-%d;%c %{= kw}%-Lw%{= kG}%{+b}[%n %t]%{-b}%{= kw}%+Lw%1`"
caption always

```

This will give you something like "screen (0 bash)" in the title of your terminal emulator. The caption supplies the date, current time, and colorizes your screen window collection.

## Используем механизм прокрутки X

The scroll buffer of GNU Screen can be accessed with C-a. However, this is very inconvenient. To use the scroll bar of e.g. xterm or konsole, add the following line to ~/.screenrc

```
termcapinfo xterm* ti@:te@

```

## Добавляем пункт в GRUB для загрузки в Screen

If you mostly use X but occasionally want to run a Screen-as-window-manager session, here's one way to do it by adding a GRUB entry for Screen on a virtual console (text terminal).

GRUB allows you to designate what runlevel you want so we'll use runlevel 4 for this purpose. Clone an appropriate GRUB entry and add a '4' to the kernel boot parameters list, like so:

```
# (0) Arch Linux
title  Arch Linux Screen
root   (hd0,2)
kernel /vmlinuz-linux root=/dev/disk/your_disk ro acpi_no_auto_ssdt irqpoll 4
initrd /initramfs-linux.img
```

Add some entries to /etc/inittab to indicate what should happen on runlevel 4, substituting your user name for <user>:

```
# gnu screen on rl4
scr2:4:respawn:/sbin/mingetty --autologin <user> tty1 linux

```

The line uses mingetty to [automatically login some user to a virtual console on startup](/index.php/Automatically_login_some_user_to_a_virtual_console_on_startup "Automatically login some user to a virtual console on startup"). You will need to install the [mingetty package](https://aur.archlinux.org/packages.php?ID=13793) (AUR). The inittab line segments are separated by colons. The first part (scr*) is simply an id. The second part is the runlevel: This should only happen on runlevel 4 (which isn't used in any default setup - 3 is by default for a tty login and 5 is for X). 'Respawn' causes init to repeat the command (i.e. autologin) if the user logs out. We'll need to see that nothing else happens on virtual console 1 when we use runlevel 4, so remove '4' from the the first of the agetty lines:

 `c1:235:respawn:/sbin/agetty -8 38400 vc/1 linux` 

Once logged in we want to ensure that screen is started. Add the following to the end of your .bash_profile:

```
  vico="$(tty | grep -oE ....$)"
  case "$vico" in
	tty1) TERM=screen; exec /usr/bin/screen -R arch;;
  esac

```

This checks for the current runlevel and will launch a screen session immediately after the autologin if the runlevel is 4.

This can also be adapted to run screen on a virtual console next to X, simply checking for the current tty instead of the current runlevel. This check to see if we're on virtual console 3:

```
  vico="$(tty | grep -oE ....$)"
  case "$vico" in
	vc/3) TERM=screen; exec /usr/bin/screen;;
  esac

```

Set inittab/mingetty to automaically log in to vc/3 on runlevel 5 and you're set.

## Исправляем зависание Midnight Commander при запуске в screen

In some cases (need deeper inspection) [old gpm bug](https://bugzilla.redhat.com/show_bug.cgi?id=168076) gets alive. So, then you try to run mc inside screen, you get a frozen screen's window. Try to kill gpm daemon before starting mc and/or disable it in _/etc/rc.conf_.

## См. также

*   [MacOSX Hints - Automatically using screen in your shell](http://www.macosxhints.com/article.php?story=20021114055617124)
*   [Gentoo Wiki - Tutorial for screen](http://wiki.gentoo.org/wiki/Screen)
*   [Arch Forums - Regarding 256 color issue with urxvt](https://bbs.archlinux.org/viewtopic.php?id=50647)
*   [Arch Forums - .screenrc configs with screenshots](https://bbs.archlinux.org/viewtopic.php?id=55618)
*   [tmux](/index.php/Tmux "Tmux"), еще один консольный мультиплексор