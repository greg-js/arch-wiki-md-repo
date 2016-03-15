**Состояние перевода:** На этой странице представлен перевод статьи [Xinitrc](/index.php/Xinitrc "Xinitrc"). Дата последней синхронизации: 2 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xinitrc&diff=0&oldid=423699).

Файл `~/.xinitrc` представляет собой шелл-скрипт передаваемый `xinit` посредством команды `startx`. Он используется для запуска [Среды рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"), [Оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") и других программ запускаемых с X сервером (например запуска демонов, и установки переменных окружений. Программа `xinit` запускает [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") сервер и работает в качестве программы первого клиента на системах не использующих [Экранный менеджер](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

Одной из основных функций `~/.xinitrc` является указание, какой клиент X Window System будет запущен каждому пользователю при вызове `startx` или `xinit`. Существует множество дополнительных настроек и команд, которые также могут быть добавлены в `~/.xinitrc` согласно вашей дальнейшей настройке системы.

Большинство DMs также используют подобный [xprofile](/index.php/Xprofile "Xprofile") перед xinit.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [4 Автозапуск X при входе в систему](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [4.1 Автоматический вход в виртуальной консоли](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B2.D1.85.D0.BE.D0.B4_.D0.B2_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8)
*   [5 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.1 Переопределение xinitrc из командной строки](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_xinitrc_.D0.B8.D0.B7_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8)
    *   [5.2 Создание выбора DE/WM (Окружения рабочего стола/Оконного менеджера)](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2.D1.8B.D0.B1.D0.BE.D1.80.D0.B0_DE.2FWM_.28.D0.9E.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0.2F.D0.9E.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0.29)
    *   [5.3 Запуск приложений без оконного менеджера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B1.D0.B5.D0.B7_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)

## Установка

[Установите](/index.php/Install "Install") [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit), чтобы использовать *xinit* и *startx*.

## Настройка

Если `.xinitrc` присутствует в домашнем каталоге пользователя, *startx* и *xinit* выполнят его. Иначе *startx* выполнит по умолчанию `/etc/X11/xinit/xinitrc`.

**Примечание:** *Xinit* имеет собственное поведение по умолчанию, вместо выполнения файла. Для подробностей,смотрите `man 1 xinit`.

Это значение по умолчанию xinitrc запустит базовую среду с [Twm](/index.php/Twm "Twm"), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) и [Xterm](/index.php/Xterm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xterm (Русский)") (при условии, что необходимые пакеты установлены). Поэтому, чтобы запустить другой оконный менеджер или окружение рабочего стола, сначала создайте копию по умолчанию `xinitrc` в вашем домашнем каталоге:

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

Это делается так (вместо создания с нуля) чтобы сохранить некоторое желаемое поведение по умолчанию в исходном файле, например, поиске скриптов из `/etc/X11/xinit/xinitrc.d`. Сценарии в этом каталоге без `.sh` расширения не считаются исходным кодом.

Добавьте нужные команды и *удалите/закоментируйте противоречивые строки*. Помните, строки, следующие после `exec` будут игнорироваться. Например, для запуска [openbox](/index.php/Openbox#Standalone "Openbox"):

 `~/.xinitrc` 
```
...

if [ -d /etc/X11/xinit/xinitrc.d ] ; then
    for f in /etc/X11/xinit/xinitrc.d/**?*.sh** ; do
        [ -x "$f" ] && . "$f"
    done
    unset f
fi

# twm &
# xclock -geometry 50x50-1+1 &
# xterm -geometry 80x50+494+51 &
# xterm -geometry 80x20+494-0 &
# exec xterm -geometry 80x66+0+0 -name login

## некоторые приложения, которые должны быть запущены в фоновом режиме
xscreensaver **&**
xsetroot -cursor_name left_ptr **&**
**exec** openbox-session

```

**Примечание:** По крайней мере, убедитесь, что блок *if* в примере выше, присутствует в вашем файле `.xinitrc` для того чтобы подать скрипт `/etc/X11/xinit/xinitrc.d/30-dbus.sh`. Иначе сессия [D-Bus](/index.php/D-Bus "D-Bus") не будет запущена.

## Запуск

Долговыполняемые программы стартуют перед оконным менеджером, такие как заставки и обои приложения. Они должны либо сами выполняться параллельно, либо работать в фоновом режиме (добавьте знак `&`). Иначе, сценарий остановится и будет ждать каждую программу, чтобы закончить перед запуском оконного менеджера. Обратите внимание, что некоторые программы не должны стартовать параллельно, во избежании потока ошибок, как в случае с [xrdb](/index.php/Xrdb "Xrdb"). Подготовка `exec` заменит процесс скрипта с процессом оконного менеджера, так что Х не завершится, даже если этот процесс распараллелен в фоне.

Для запуска Xorg от имени обычного пользователя, выполните:

```
$ startx

```

или

```
$ xinit -- :1 -nolisten tcp vt$XDG_VTNR

```

Выбранный вами оконный менеджер (или окружение рабочего стола) теперь запустится правильно.

Для выхода из X, запустите функцию выхода вашего оконного менеджера (при условии, что он есть). Если нет такой возможности, запустите:

```
$ pkill -15 Xorg

```

**Примечание:** *pkill* убьет все запущенные экземпляры X. Для специального убивания оконного менеджера на текущем VT, используйте:
```
WM_PID=$(xprop -id $(xprop -root _NET_SUPPORTING_WM_CHECK \
| awk -F'#' '{ print $2 }') _NET_WM_PID \
| awk -F' = ' '{ print $2 }')

kill -15 $WM_PID
```

Программа `xprop` доступна в пакете [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) из [Официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

**Примечание:**

*   Команды запускают [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") на томже виртуальном терминале, в который вошёл пользователь. [[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html) Это поддерживает авторизованную сессию с `logind`, и предотвращает обход блокировщика экрана, при переключении терминалов.
*   Вы должны указать `vt$XDG_VTNR` в качестве опции командной строки для *xinit* чтобы [сохранить права сессии (preserve session permissions)](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").
*   *xinit* не обрабатывает несколько сеансов, когда вы уже вошли в другой виртуальный терминал. Для этого необходимо указать сессию добавления `-- :*session_no*`. Если X уже запущен, то вы должны начать с: 1 или больше.
*   По умолчанию, экран X должен быть на том же терминале, где и произошел вход. Это обрабатывается `/etc/X11/xinit/xserverrc` по умолчанию. Смотрите [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") для подробностей.
*   Если вы хотите получить экран Х отдельно от консоли вызова сервера X, вы можете сделать это при помощи оболочки X сервера `/usr/lib/systemd/systemd-multi-seat-x`. Для удобства *startx* может быть настроен на использование этой оболочки, изменяя ваш`~/.xserverrc`.
*   Если вы решите использовать *xinit* вместо *startx*, тогда вы несете ответственность за прохождение `-nolisten tcp` и обеспечение не сломанной сессии запуская X на другом tty.
*   Если X завершает с сообщением об ошибке "SocketCreateListener() failed", вам возможно потребуется удалить файлы сокетов в `/tmp/.X11-unix`. Это может произойти, если ранее Xorg был выполнен от root.

## Автозапуск X при входе в систему

**Примечание:** Это решение запускает X на том же терминале использующимся для входа, который нужен чтобы поддержать сеанс регистрации.

Для [Bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)"), добавьте следующее в нижнюю часть `~/.bash_profile`. Если файл не существует, скопируйте шаблон-версию с `/etc/skel/.bash_profile`. Для [Zsh](/index.php/Zsh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Zsh (Русский)"), добавьте в `~/.zlogin` (или в `~/.zprofile`).

```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**Примечание:**

*   Вы можете заменить `-eq 1` по сравнению с `-le 3` (от vt1 до vt3) если вы хотите использовать графические логины на более чем одном VT.
*   Чтобы сохранить ссессию logind, Х должен всегда работать на томже терминале, где произошел Вход (логин). Это работает по умолчанию `/etc/X11/xinit/xserverrc`.
*   `xinit` может быть быстрее, чем `startx`, но нужны дополнительные параметры, например `-nolisten tcp`.
*   Если вы хотите оставаться в системе, когда заканчивается Х сессия, удалите `exec`.

Смотрите также [Fish#Запуск X при входе в систему](/index.php/Fish_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83 "Fish (Русский)") и [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

### Автоматический вход в виртуальной консоли

Этот метод можно объединить с [автоматическим входом в виртуальной консоли](/index.php/Automatic_login_to_virtual_console_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Automatic login to virtual console (Русский)"). При этом вы должны установить правильные зависимости для выполнения автологина Systemd чтобы убедиться, что dbus запускается до чтения `~/.xinitrc` и старта pulseaudio (смотрите: [BBS#155416](https://bbs.archlinux.org/viewtopic.php?id=155416))

## Советы и хитрости

### Переопределение xinitrc из командной строки

Если у вас есть рабочий `~/.xinitrc`, но хотите попробовать другие WM/DE, вы можете запустить его используя *startx* с указанием пути к оконному менеджеру:

```
$ startx /full/path/to/window-manager

```

Если оконный менеджер принимает аргументы, они должны быть взяты в кавычки в качестве части первого параметра *startx*:

```
$ startx "/full/path/to/window-manager --key value"

```

Обратите внимание что **требуется** полный путь. По желанию, вы можете также переопределить `/etc/X11/xinit/xserverrc` файл (который хранит значение по умолчанию X сервера) с пользовательскими опциями, путем добавления их после `--`, например:

```
$ startx /usr/bin/enlightenment -- -nolisten tcp -br +bs -dpi 96 vt$XDG_VTNR

```

или

```
$ xinit /usr/bin/enlightenment -- -nolisten tcp -br +bs -dpi 96 vt$XDG_VTNR

```

Смотрите также `man startx`.

**Совет:** Это может быть использовано даже для запуска программ с графическим интерфейсом, но без каких-либо особенностей оконного менеджера. Смотрите также [#Запуск приложений без оконного менеджера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B1.D0.B5.D0.B7_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0) и [Запуск программ в отдельном экране X](/index.php/Running_program_in_separate_X_display_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Running program in separate X display (Русский)").

### Создание выбора DE/WM (Окружения рабочего стола/Оконного менеджера)

Если вы часто переключаетесь между различными DEs/WMs, рекомендуется использовать [Display manager](/index.php/Display_manager "Display manager") или добавить код в `.xinitrc`. Следующий код, описанный в нескольких строчках, будет принимать аргумент и загружать желаемое окружение рабочего стола или менеджера окон.

В следующем примере `~/.xinitrc` показано как запустить конкретную DE/WM с аргументом:

 `~/.xinitrc` 
```
...

# Xfce передаётся по умолчанию
session=${1:-xfce}

case $session in
    awesome           ) exec awesome;;
    bspwm             ) exec bspwm;;
    catwm             ) exec catwm;;
    cinnamon          ) exec cinnamon-session;;
    dwm               ) exec dwm;;
    enlightenment     ) exec enlightenment_start;;
    ede               ) exec startede;;
    fluxbox           ) exec startfluxbox;;
    gnome             ) exec gnome-session;;
    gnome-classic     ) exec gnome-session --session=gnome-classic;;
    i3|i3wm           ) exec i3;;
    icewm             ) exec icewm-session;;
    jwm               ) exec jwm;;
    kde               ) exec startkde;;
    mate              ) exec mate-session;;
    monster|monsterwm ) exec monsterwm;;
    notion            ) exec notion;;
    openbox           ) exec openbox-session;;
    unity             ) exec unity;;
    xfce|xfce4        ) exec startxfce4;;
    xmonad            ) exec xmonad;;
    # Не известная сессия, попробуйте запустить в качестве команды
    *) exec $1;;
esac

```

Затем скопируйте файл `/etc/X11/xinit/xserverrc` в ваш домашний каталог:

```
$ cp /etc/X11/xinit/xserverrc ~/.xserverrc

```

После этого, вы можете легко запустить конкретный DE/WM передавая аргумент, например:

```
$ xinit
$ xinit gnome
$ xinit kde
$ xinit wmaker

```

или

```
$ startx
$ startx ~/.xinitrc gnome
$ startx ~/.xinitrc kde
$ startx ~/.xinitrc wmaker

```

### Запуск приложений без оконного менеджера

Можно запустить только определенные приложения без оконного менеджера. Хотя, это будет полезно только для одного приложения, запущенного в полноэкранном режиме. Напирмер:

 `~/.xinitrc` 
```
...

exec chromium

```

С помощью этого метода необходимо установить геометрию каждого окна приложения с помощью своих собственных файлов настроек, если вообще возможно.

**Совет:** Этот метод может быть полезен для запуска графических игр, чтобы улучшить их производительность. Т.к. при таком способе оконный менеджер не будет использовать память и процессор.

Смотрите также [Display manager (Русский)#Запуск приложений без оконного менеджера](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B1.D0.B5.D0.B7_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0 "Display manager (Русский)").