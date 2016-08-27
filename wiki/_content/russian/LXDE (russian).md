[LXDE.org|Lightweight X11 Desktop Environment](http://lxde.org/): *"Одно из главных достоинств LXDE - небольшие требования к железу. Философия LXDE - это лёгкость, полезность и практичность."*

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск окружения LXDE](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_LXDE)
    *   [2.1 Display Managers](#Display_Managers)
    *   [2.2 Консоль](#.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Автомонтирвание](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.2 Автозапуск программ](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC)
    *   [3.3 Горячие клавиши](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
    *   [3.4 Курсоры](#.D0.9A.D1.83.D1.80.D1.81.D0.BE.D1.80.D1.8B)
    *   [3.5 Шрифты настройка](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.6 Раскладка клавиатуры](#.D0.A0.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
        *   [3.6.1 udev](#udev)
        *   [3.6.2 Другие способы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D1.8B)
        *   [3.6.3 Посредством LXDE](#.D0.9F.D0.BE.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.BE.D0.BC_LXDE)
    *   [3.7 LXDM](#LXDM)
        *   [3.7.1 Установка LXDM](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_LXDM)
        *   [3.7.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
            *   [3.7.2.1 Ожидаемое поведение после Logout](#.D0.9E.D0.B6.D0.B8.D0.B4.D0.B0.D0.B5.D0.BC.D0.BE.D0.B5_.D0.BF.D0.BE.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_Logout)
            *   [3.7.2.2 Автоматический вход](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B2.D1.85.D0.BE.D0.B4)
    *   [3.8 PCManFM](#PCManFM)
    *   [3.9 Замена оконного менеджера](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
    *   [3.10 Выключение, Перезагрузка (LXSession-logout)](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5.2C_.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.28LXSession-logout.29)
    *   [3.11 Редактирование меню приложений](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)

## Установка

LXDE модульный и вы можете выбирать только те пакеты, которые вам нужны.

Минимально необходимые пакеты для запуска LXDE: [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession), [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) и оконный менеджер.

Вы можете установить группу пакетов LXDE:

```
# pacman -S lxde

```

Установятся следующие пакеты:

*   [gpicview](https://www.archlinux.org/packages/?name=gpicview): Простой и легкий просмоторщик изображений
*   [libfm](https://www.archlinux.org/packages/?name=libfm): Библиотека для работы с файлами (lxshortcut: Простое средство редактирования ярлычков)
*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance): Редактор тем для изменения GTK+ тем, иконок и шрифтов для приложений GTK
*   [lxappearance-obconf](https://www.archlinux.org/packages/?name=lxappearance-obconf): Плагин для настройки Openbox через LXAppearance
*   [lxde-common](https://www.archlinux.org/packages/?name=lxde-common): Установки по умолчанию конфигурационных файлов для большинства интегрированных компонентов LXDE
*   [lxde-icon-theme](https://www.archlinux.org/packages/?name=lxde-icon-theme): Тема значков LXDE
*   [lxdm](https://www.archlinux.org/packages/?name=lxdm): Легковесный менеджер дисплея приветствия
*   [lxinput](https://www.archlinux.org/packages/?name=lxinput): Конфигурационная утилита для клавиатуры и мышки в LXDE
*   [lxlauncher](https://www.archlinux.org/packages/?name=lxlauncher): Панель запуска приложений для нетбуков
*   [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data): Коллекция файлов адаптирующая меню LXDE под стандарты спецификации freedesktop.org
*   [lxmusic](https://www.archlinux.org/packages/?name=lxmusic): Минималистичный проигрыватель музыки базирующийся на xmms2
*   [lxpanel](https://www.archlinux.org/packages/?name=lxpanel): Панель задач с менеджером приложений, меню программ и апплетов
*   [lxrandr](https://www.archlinux.org/packages/?name=lxrandr): Менеджер экрана для LXDE
*   [lxsession](https://www.archlinux.org/packages/?name=lxsession): Совместимый X11 менеджер сессий с поддержкой выключения, перезагрузки и ждущего режима
*   [lxtask](https://www.archlinux.org/packages/?name=lxtask): Диспетчер задач и системный монитор LXDE
*   [lxterminal](https://www.archlinux.org/packages/?name=lxterminal): Стандартный эмулятор терминала для LXDE
*   [menu-cache](https://www.archlinux.org/packages/?name=menu-cache): Механизм кеширования для freedesktop.org-совместимых меню
*   [openbox](https://www.archlinux.org/packages/?name=openbox): Легкий и удобно конфигурируемый менеджер окон (рекомендуемый менеджер, разработанный вне проекта LXDE).
*   [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm): Файловый менеджер, функционал рабочего стола и обоев

Вам также следует установить [Gamin](/index.php/Gamin "Gamin"). [Gamin](/index.php/Gamin "Gamin") - это инструмент для отслеживания изменений в файлах и директориях, который является реализацией подсистемы FAM. Запуск производится по требованию программ, которые им поддерживаются, поэтому не требуется отдельно демона, подобного [FAM](/index.php/FAM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "FAM (Русский)"). Если у Вас установлен [FAM](/index.php/FAM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "FAM (Русский)") - удалите запуск этого демона из `/etc/rc.conf` и остановите его перед установкой [Gamin](/index.php/Gamin "Gamin")

```
pacman -S gamin

```

Другие легковесные приложения, которые рекомендуется использовать на слабых системах:

*   [leafpad](https://www.archlinux.org/packages/?name=leafpad): Простой и легкий текстовый редактор
*   [mousepad](https://www.archlinux.org/packages/?name=mousepad): Простой текстовый редактор (является текстовым редактором по умолчанию среды Xfce)
*   [xarchiver](https://www.archlinux.org/packages/?name=xarchiver): Легкий архиватор
*   [obconf](https://www.archlinux.org/packages/?name=obconf): Инструмент для настройки тем и стилей Openbox

## Запуск окружения LXDE

Есть несколько способов запустить LXDE.

### Display Managers

Если Вы используете менеджеры [SLiM](/index.php/SLiM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SLiM (Русский)"), [GDM](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"), или [KDM](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)"), в настройках сессии нужно выбрать LXDE.

Инструкция по использованию LXDM [ниже на этой странице](/index.php/LXDE#LXDM "LXDE").

Если не используете менеджер дисплея приветствия добавьте

```
export DESKTOP_SESSION=LXDE

```

в ваш `~/.bash_profile` Для првавильного функционирования [Xdg-open](/index.php/Xdg-open "Xdg-open")

### Консоль

Для использования команды **startx** необходимо добавить в файл [`~/.xinitrc`](/index.php/Xinit "Xinit") команду запуска LXDE:

```
exec startlxde

```

Если Вы хотите выполнять **startx** автоматически при загрузке, прочитайте статью [Запуск X при загрузке](/index.php/Start_X_at_Boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D0.B2.D1.8B.D0.B1.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.BC_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.BC_.D0.B1.D0.B5.D0.B7_.D0.BB.D0.BE.D0.B3.D0.B8.D0.BD.D0.B0 "Start X at Boot (Русский)").

**Для других задач Вы должны быть уверены, что демон dbus запущен.**

## Советы и рекомендации

### Автомонтирвание

[PCManFM (Русский)#Работа с томами](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D0.B1.D0.BE.D1.82.D0.B0_.D1.81_.D1.82.D0.BE.D0.BC.D0.B0.D0.BC.D0.B8 "PCManFM (Русский)")

### Автозапуск программ

	файлы *.desktop*

Вы можете скопировать ярлык программы *.desktop* из `/usr/share/applications/` в `~/.config/autostart/`. Например, добавим в автозапуск *lxterminal*:

```
$ ln -s /usr/share/applications/lxterminal.desktop ~/.config/autostart/

```

После добавления файлов *.desktop* Вы можете упралять ими с помощью [lxsession-edit](https://aur.archlinux.org/packages/lxsession-edit/).

	файл autostart

Второй способ - использование файла `~/.config/lxsession/LXDE/autostart`. Этот файл - не скрипт, но каждая строка представляет собой команду, которая будет выполнена, если строка начинается с символа `@`. Команда после `@` будет автоматически повторно выполняться, если она падает. Например, чтобы выполнить *lxterminal* и *leafpad* автоматически при запуске:

 `~/.config/lxsession/LXDE/autostart` 
```
@lxterminal
@leafpad

```

**Примечание:** Пoсле команды **не нужно** ставить символ `&`

Существует также глобальный файл автозапуска `/etc/xdg/lxsession/LXDE/autostart`. Если эти файлы присутствуют одновременно, то оба будут выполнены.

### Горячие клавиши

Управление горячими клавишами осуществляется через Openbox и подробно описаны [здесь](http://openbox.org/wiki/Help:Bindings). Пользователи LXDE должны следовать этим инструкциям, чтобы отредактировать файл **~/.config/openbox/lxde-rc.xml**

Дополнительный графический интерфейс для редактирования горячих клавиш - [obkey](https://aur.archlinux.org/packages/obkey/) доступен в AUR. Поумолчанию obkey редактирует файл rc.xml, Но вы можете использовать его в LXDE таким образом:

```
$ obkey ~/.config/openbox/lxde-rc.xml

```

Больше информации о obkey [здесь](http://code.google.com/p/obkey/).

### Курсоры

Основная статья: [Темы курсора](/index.php/%D0%A2%D0%B5%D0%BC%D1%8B_%D0%BA%D1%83%D1%80%D1%81%D0%BE%D1%80%D0%B0 "Темы курсора").

Последний [lxappearance2-git](https://aur.archlinux.org/packages/lxappearance2-git/) предоставляет функциональные возможности для изменения тем курсора. Если Вы не хотите устанавливать экспериментальный *lxappearance2*, можете указать свою тему курсора в файле `~/.Xdefaults`. Смотрите раздел [Темы курсора#Настройка](/index.php/%D0%A2%D0%B5%D0%BC%D1%8B_%D0%BA%D1%83%D1%80%D1%81%D0%BE%D1%80%D0%B0#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Темы курсора").

Простым способом является добавление курсора к теме по умолчанию. Сначала нужно создать каталог `/usr/share/icons/default`, then you can specify to add to the icon theme the cursor. This will use the [xcursor-bluecurve](https://www.archlinux.org/packages/?name=xcursor-bluecurve) pointer theme:

 `/usr/share/icons/default/index.theme` 
```
[icon theme]
Inherits=Bluecurve
```

### Шрифты настройка

Для установки шрифтов, вы можете использовать [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) и установить основной шрифт. Для настройки других шрифтов можно использовать **Openbox configuration tool** ObConf:

```
# pacman -S obconf

```

### Раскладка клавиатуры

#### udev

Когда вы используете [udev](/index.php/Udev "Udev"), конфигурация ввода по умолчанию записываются в `/etc/X11/xorg.conf.d/10-evdev.conf` в `Section "InputClass"`. Вы можете редактировать этот или создать новый файл `/etc/X11/xorg.conf.d/20-keyboard.conf` по следующему примеру (переключение раскладки клавишами Alt+Shift, индикация CAPS-диодом на клавиатуре):

```
Section "InputClass"
    Identifier          "evdev keyboard catchall"
    MatchIsKeyboard     "on"
    MatchDevicePath     "/dev/input/event*"
    Driver              "evdev"
    Option              "XkbModel" "pc104"
    Option              "XkbLayout" "us,ru"
    Option "XkbOptions" "grp:alt_shift_toggle,grp_led:caps"
EndSection

```

Вы можете найти список всех значений в `/usr/share/X11/xkb/rules/base.lst`.

#### Другие способы

1 способ: Добавьте в /etc/xdg/lxsession/LXDE/autostart следующие строки перед @lxpanel --profile LXDE:

```
@setxkbmap -option grp:switch,grp:alt_shift_toggle,grp_led:scroll us,ru

```

или в ~/.config/lxsession/LXDE/autostart (для конкретного пользователя):

```
setxkbmap -option grp:switch,grp:alt_shift_toggle,grp_led:scroll us,ru

```

2 способ: Create /etc/xdg/autostart/setxkmap.desktop as following:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Name=Fix keyboard settings
Exec=setxkbmap -rules xorg -layout "us,ru" -variant ",winkeys" -option "grp:ctrl_shift_toggle"
Terminal=false
Type=Application 

```

3 способ: Добавьте в ~/.Xkbmap, для текущего пользователя, или в /etc/X11/Xkbmap, для всей системы, строку:

```
-option grp:ctrl_shift_toggle,grp_led:scroll us,ru

```

4 способ: Добавьте следующую строку в /etc/X11/xinit/xinitrc или ~/.xinitrc:

```
setxkbmap -option grp:ctrl_shift_toggle,grp_led:scroll us,ru

```

5 способ: Установите [fbxkb](https://aur.archlinux.org/packages/fbxkb/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)")

6 способ: [Xorg (Русский)#Переключение раскладок средствами X.org](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0.D0.BC.D0.B8_X.org "Xorg (Русский)")

#### Посредством LXDE

1.  Правый клик на панели задач
2.  “Добавить/убрать элементы панели”
3.  “Добавить”
4.  “Индикатор раскладок клавиатуры”

### LXDM

LXDE теперь обеспечивает экспериментальную менеджер дисплея приветствия LXDM. Это реализовано с GTK+ и [supports theming](http://blog.lxde.org/?p=595).

#### Установка LXDM

```
# pacman -S lxdm

```

Для автоматического запуска LXDM Вы можете редактировать `/etc/inittab` или `/etc/rc.conf`. Для получения дополнительной информации см. [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер").

#### Настройка

Все конфигурационные файлы для LXDM расположены в `/etc/lxdm`. Основной файл конфигурации `lxdm.conf` хорошо документирован в его коментарии. Файл, `Xsession`, является общесистемным и не должен редактироваться. Другие файлы - это bash скрипты, которые выполняются при наступлении определенных событий в LXDM. К ним относятся:

1.  `LoginReady`: Выполняется с правами root когда LXDM готова показать окно входа в систему.
2.  `PreLogin`: Выполняется с правами root перед входом пользователя.
3.  `PostLogin`: Выполняется с правами авторизованного пользователя сразу после входа.
4.  `PostLogout`: Выполняется с правами авторизованного пользователя после выхода.
5.  `PreReboot`: Выполняется с правами root перед перезагрузкой компьютера с LXDM.
6.  `PreShutdown`: Выполняется с правами root перед выключением компьютера с LXDM.

##### Ожидаемое поведение после Logout

Может быть немного удивительно, что LXDM по умолчанию не очищает фон рабочего стола и не убивает процессы пользователя после его выхода. Для решения проблемы необходимо добавить в файл `/etc/lxdm/PostLogout`:

```
#!/bin/sh

# Kills all your processes when you log out.
killall --user $USER -TERM

# Set's the desktop background to solid black. Useful if you have multiple monitors.
xsetroot -solid black

```

##### Автоматический вход

Если вы хотите войти в учетную запись без ввода пароля, найдите строку в `/etc/lxdm/lxdm.conf`, которая выглядит следующим образом:

```
#autologin=username

```

Раскомментируйте его и подставьте нужное имя пользователя, вместо "username".

### [PCManFM](/index.php/PCManFM "PCManFM")

Если вы хотите иметь доступ к Корзине, монтированию томов и folder/file tracking Вам необходима поддержка gvfs:

```
pacman -S polkit-gnome gvfs

```

polkit-gnome обеспечивает аутентификацию и должен быть запущен при входе в систему:

```
$ mkdir -p ~/.config/autostart
$ cp /etc/xdg/autostart/polkit-gnome-authentication-agent-1.desktop ~/.config/autostart

```

В Arch'е этот файл в настоящее время не работает на некоторых системах. Если у вас проблема запуском, удалите строку

```
OnlyShowIn=GNOME;XFCE;

```

из файла `~/.config/autostart/polkit-gnome-authentication-agent-1.desktop`:

[PCManFM @ LXDE wiki](http://wiki.lxde.org/en/LXDE:PCManFM_build_and_setup_guide#Setup_Runtime_Environment_Correctly)

### Замена оконного менеджера

[Openbox](/index.php/Openbox "Openbox"), стандартный менеджер окон LXDE, может быть заменен другими. Например fvwm, icewm, dwm, metacity, compiz ...etc.

LXDE будет пытаться использовать оконный менеджер из пользовательского фаула конфигурации lxsession `~/.config/lxsession/LXDE/desktop.conf`.Если его не существует, будет пытаться использовать глобальный файл конфигурации `/etc/xdg/lxsession/LXDE/desktop.conf`.

Замените команду openbox-lxde на ваш менеджер окон:

```
[Session]
window_manager=openbox-lxde

```

Для metacity:

```
window_manager=metacity

```

Для compiz:

```
window_manager=compiz ccp --indirect-rendering

```

### Выключение, Перезагрузка (LXSession-logout)

Для работы Выключения, Перезагрузки, Режима сна и Режима ожидания Должен быть запущен dbus. Должен быть установлен пакет upower.

```
# pacman -S upower

```

См. [xinitrc#Preserving the session](/index.php/Xinitrc#Preserving_the_session "Xinitrc") подробнее о logind/ConsoleKit.

### Редактирование меню приложений

(нужно проверить перевод). Ссылка на [оригинал](/index.php/LXDE#Application_menu_editing "LXDE")

Меню приложений работает через передачу `.desktop` файлов, которые расположены в `/usr/share/applications`. Многие DE запускают программы, которые supersede эти настройки для кастомизации меню. Для LXDE еще только создают редактор меню приложений, но вы можете настроить его вручную, если нужно. Сторонние редакторы меню вы можете найти в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") - [lxmed](https://aur.archlinux.org/packages/lxmed/).

Чтобы добавить или редактировать элемент меню, создайте или сделайте ссылку на `.desktop` файл в `/usr/share/applications`. Смотрите [the desktop entry specification](http://standards.freedesktop.org/desktop-entry-spec/latest/) на freedesktop.org для получения информации о структуре `.desktop` файлов.

Для удаления элементов из меню вместо удаления `.desktop` файлов, вы можете редактировать файл элемента, добавляя следующую строку:

```
NoDisplay=true.

```

Для ускорения процесса редактирования большого числа файлов вы можете поместить их в цикл. Например:

```
cd /usr/share/applications
for i in program1.desktop program2.desktop ...; do cp /usr/share/applications/$i \
/home/user/.local/share/applications/; echo "NoDisplay=true" >> \
/home/user/.local/share/applications/$i; done

```

Это будет работать для всех приложений, исключая KDE. Для них единственный путь удалить их из списка меню - зайти в KDE и использовать собственный редактор меню. Для каждого элемента, который вы не желаете лицезреть, проверьте опцию 'Show only in KDE' (*отображать только в KDE*). Если добавление NoDisplay=True не работает, вы можете добавить ShowOnlyIn=XFCE.