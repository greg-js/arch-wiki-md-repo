**Wayland** это новый протокол управления окнами для Linux. Использование Wayland требует внесения изменений в систему и повторной установки некоторых ее компонентов. Для получения дополнительной информации о Wayland смотрите [домашюю страницу](http://wayland.freedesktop.org/).

**Важно:** Wayland находится в процессе разработки и некоторая функциональность может быть ограничена.

## Contents

*   [1 Требования](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [4 Weston](#Weston)
    *   [4.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
    *   [4.2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_2)
    *   [4.3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
        *   [4.3.1 XWayland](#XWayland)
*   [5 GUI библиотеки](#GUI_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.D0.B8)
    *   [5.1 GTK+](#GTK.2B)
    *   [5.2 Qt5](#Qt5)
    *   [5.3 Clutter](#Clutter)
    *   [5.4 SDL](#SDL)
    *   [5.5 glfw](#glfw)
    *   [5.6 EFL](#EFL)
*   [6 Оконные менеджеры и оболочки рабочего стола](#.D0.9E.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B_.D0.B8_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [6.1 GNOME](#GNOME)
    *   [6.2 Hawaii](#Hawaii)
    *   [6.3 sway](#sway)
    *   [6.4 KDE](#KDE)
    *   [6.5 Orbment](#Orbment)
    *   [6.6 Velox](#Velox)
    *   [6.7 Orbital](#Orbital)
    *   [6.8 Papyros Shell](#Papyros_Shell)
    *   [6.9 Maynard](#Maynard)
    *   [6.10 Motorcar](#Motorcar)
*   [7 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [7.1 LLVM assertion failure](#LLVM_assertion_failure)
    *   [7.2 Не запускается Weston после обновления до 1.7](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_Weston_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B4.D0.BE_1.7)
*   [8 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Требования

В настоящее время Wayland будет работать только на системах, использующих [KMS](/index.php/KMS "KMS").

## Установка

Вероятней всего Wayland уже установлен на вашей системе, так как он является зависимостью для [gtk2](https://www.archlinux.org/packages/?name=gtk2) и [gtk3](https://www.archlinux.org/packages/?name=gtk3). Если же он отсутствует, пакет [wayland](https://www.archlinux.org/packages/?name=wayland) можно установить из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Использование

Wayland это просто библиотека, которая бесполезна сама по себе. Для использования этой технологии вместо сервера X понадобится композитный менеджер (такой как Weston).

## Weston

### Установка

Вам нужно установить пакет [weston](https://www.archlinux.org/packages/?name=weston) из официальных репозиториев.

### Использование

<caption>_**Горячие клавиши** (super = windows key - можно изменить, см. weston.ini)_</caption>
| Комманда | Действие |
| Ctrl + Alt + Backspace | Выйти из Weston |
| Super + Scroll (or PageUp/PageDown) | Увеличить/уменьшить рабочий стол |
| Super + Tab | Переключить окно |
| Super + ЛКМ | Переместить окно |
| Super + Колесо прокрутки | Изменить размер окна |
| Super + ПКМ | Повернуть окно! |
| Super + Alt + Колесо прокрутки | Изменить прозрачность окна |
| Super + K | Принудительно завершить активное окно |
| Super + KeyUp/KeyDown | Переключиться на предыдущее/следующее рабочее пространство |
| Super + Shift + KeyUp/KeyDown | Переключение рабочего пространства с захватом текущего окна |
| Super + F_**n**_ | Перейти на рабочее пространство _**n**_ |
| Super + S | Сделать скриншот |
| Super + R | Скринкастинг. |

Теперь, когда установлен Wayland и выполнены все требования, можно проверить его.

Можно запустить Weston прямо из активного X сеанса:

```
$ weston

```

Также Weston может быть запущен самостоятельно. Попробуйте выполнить в виртуальном терминале:

```
$ weston-launch

```

Если Weston на TTY, вы можете запустить демо приложения. Чтобы запустить эмулятор терминала:

```
$ weston-terminal

```

Чтобы разместить цветы по всему экрану:

```
$ weston-flower 

```

Для просмотра изображений:

```
$ weston-image image1.jpg image2.jpg...

```

### Настройка

Пример конфигурационного файла для раскладки клавиатуры, выбранных модулей и видоизмененного интерфейса. Подробности смотрите в `man weston.ini`:

 `~/.config/weston.ini` 

```
[core]
shell=desktop-shell.so
### для поддержки xwayland следущая строка должна быть раскоментирована ###
modules=xwayland.so

[libinput]
enable_tap=true

[shell]
background-image=/usr/share/archlinux/wallpaper/archlinux-simplyblack.png
### цвета в формате AARRGGBB ###
background-color=0x00ffffff
panel-color=0x00ffffff
locking=true
animation=zoom
close-animation=fade
focus-animation=dim-layer
#binding-modifier=ctrl
num-workspaces=6
### для выбора темы курсора нужно установить xcursor-themes из Extra. ###
#cursor-theme=whiteglass
#cursor-size=24

### настройки планшета ###
#lockscreen-icon=/usr/share/icons/gnome/256x256/actions/lock.png
#lockscreen=/usr/share/backgrounds/gnome/Garden.jpg
#homescreen=/usr/share/backgrounds/gnome/Blinds.jpg
#animation=fade

[keyboard]
keymap_rules=evdev
keymap_layout=us,ru
keymap_options=grp:caps_toggle
### keymap_options из /usr/share/X11/xkb/rules/base.lst ###

[terminal]
font=Terminus
font-size=14
#term=rxvt-unicode

[launcher]
icon=/usr/share/icons/gnome/32x32/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/32x32/apps/wireshark.png
path=/usr/bin/wireshark

[launcher]
icon=/usr/share/icons/hicolor/32x32/apps/firefox.png
path=/usr/bin/firefox

[launcher]
icon=/usr/share/icons/gnome/32x32/apps/arts.png
path=/usr/bin/weston-flower

[screensaver]
# Раскоментируйте путь, чтобы отключить заставку
path=/usr/libexec/weston-screensaver
duration=600

[input-method]
path=/usr/libexec/weston-keyboard

###  для дисплея ноутбука  ###
[output]
name=LVDS1
mode=1280x800
#transform=90

#[output]
#name=VGA1
# The following sets the mode with a modeline, you can get modelines for your preffered resolutions using the cvt utility
#mode=173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
#transform=flipped

#[output]
#name=X1
#mode=1024x768
#transform=flipped-270

```

#### XWayland

Пакет [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) доступен в официальных репозиториях.

Если вам понадобится запускать X-приложения из Weston, он будет вызывать Xwayland для обслуживания запросов. Для этого добавьте следующие строки в файл конфигурации:

 `~/.config/weston.ini` 

```
[core]
modules=xwayland.so,desktop-shell.so

```

## GUI библиотеки

(Подробности смотрите на [официальном сайте](http://wayland.freedesktop.org/toolkits.html))

### GTK+

В пакете [gtk3](https://www.archlinux.org/packages/?name=gtk3) из официальных репозиториев уже включена поддержка Wayland.

С версии GTK+ 3.0, GTK+ имеет поддержку нескольких бэкендов во время выполнения и может переключаться между ними таким же образом, Qt c lighthouse.

Когда включены оба бэкенда Wayland и X, GTK + по умолчанию будет использовать X11, но это можно изменить, переназначив переменную окружения: `GDK_BACKEND=wayland`.

### Qt5

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [qt5-wayland](https://www.archlinux.org/packages/?name=qt5-wayland). Чтобы запустить приложение Qt5 с плагином Wayland, установите [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `QT_QPA_PLATFORM=wayland-egl` .

### Clutter

Clutter toolkit имеет бэкенд Wayland, что позволяет ему работать в качестве клиента Wayland. Бэкенд включён в официальным пакет из extra .

Для запуска Clutter на Wayland, выставите `CLUTTER_BACKEND=wayland`.

### SDL

Экспериментальная поддержка wayland доступна с версии SDL 2.0.2 и включена по умолчанию Arch Linux.

Для запуска SDL на Wayland, выставите `SDL_VIDEODRIVER=wayland`.

### glfw

Версия 3.1 будет иметь поддержку Wayland через указанный флаг компиляции. В то же время вы можете установить пакет [glfw3-git](https://aur.archlinux.org/packages/glfw3-git/) и добавить Cmake-флаг `-DGLFW_USE_WAYLAND=ON`

### EFL

EFL полностью поддерживает Wayland. Для запуска EFL в Wayland смотрите [страницу проекта Wayland](http://wayland.freedesktop.org/efl.html).

## Оконные менеджеры и оболочки рабочего стола

### GNOME

**Важно:** Сеанс Gnome Wayland не запустится, если [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) не установлен .

Начиная с версии 3.14, Gnome поддерживает запуск рабочего стола используя Wayland. Gnome compositor может быть запущен без использования X, и будет выступать в качестве композитного менеджера Wayland.Он достаточно стабильный для повседневного использования, однако есть некоторые особенности, которые пока что не поддерживаются (см. документацию Gnome). Поэтому рабочий стол, приложения, использующие X будет работать с использованием XWayland.

Для запуска сеанса Gnome Wayland нужно использовать gdm login manager, в котором требуется выбрать "Gnome on Wayland".

### Hawaii

[см. страницу Hawaii](/index.php/Hawaii "Hawaii")

### sway

[Sway](https://github.com/SirCmpwn/sway) - это совместимый с i3 фреймовый оконный менеджер для Wayland.

### KDE

Начиная с KDE 4.11 beta поддерживается [KWin как композитный менеджер Wayland](http://blog.martin-graesslin.com/blog/2013/06/starting-a-full-kde-plasma-session-in-wayland/). При этом в настоящее время нет возможности использовать KWin в качестве менеджера сессии. Поддержка клиентов Wayland планируется с версии KDE 5.4.

### Orbment

[orbment](https://github.com/Cloudef/orbment) (ранее loliwm) - фреймовый оконный менеджер для Wayland.

### Velox

[velox](https://github.com/michaelforney/velox) простой фреймовый оконный менеджер, основанный на swc. Базируется на [dwm](/index.php/Dwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dwm (Русский)") и [xmonad](/index.php/Xmonad_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xmonad (Русский)").

### Orbital

[Orbital](https://github.com/giucam/orbital) это композитный менеджер Wayland и пользовательская оболочка, использующая Qt5 и Weston. Цель проекта заключается в создании простого, но гибкого и привлекательного рабочего стола Wayland рабочий. Это не полноценное окружение рабочего стола, а скорее аналог оконного менеджера для X11, такого как [Awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)") или [Fluxbox](/index.php/Fluxbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fluxbox (Русский)").

### Papyros Shell

[Papyros Shell](https://github.com/papyros/papyros-shell) это оболочка рабочего стола проекта [Papyros](http://papyros.io), построенная с использованием QtQuick и использущая QtCompositor в качестве композитного менеджера Wayland.

### Maynard

[Maynard](https://github.com/raspberrypi/maynard) это GTK клиент рабочего стола для Weston . Оболочка основана на наработках Weston gtk-shell.

### Motorcar

[Motorcar](https://github.com/evil0sheep/motorcar) - композитный менеджер и прототип интерфейса трёхмерного рабочего стола.

## Решение проблем

### LLVM assertion failure

Если вы получаете LLVM assertion failure, вам нужно пересобрать [mesa](https://www.archlinux.org/packages/?name=mesa) без Gallium LLVM пока эта проблема не будет исправлена.

Это может означать отключение некоторых драйверов, которым требуется LLVM. Если возникают проблемы с драйверами, то можно также попробовать предпринять следующее:

```
$ export EGL_DRIVER=/usr/lib/egl/egl_gallium.so

```

### Не запускается Weston после обновления до 1.7

Это может быть связано с загрузкой модуля `desktop-shell.so`, указанного в weston.ini. Требуется просто удалить его из строки конфигурации, подобно этой:

 `~/.config/weston.ini` 

```
[core]
modules=xwayland.so,desktop-shell.so

```

Убрав `desktop-shell.so`, получаем

 `~/.config/weston.ini` 

```
[core]
modules=xwayland.so

```

## См. также

*   [Cursor themes (Русский)](/index.php/Cursor_themes_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Cursor themes (Русский)")
*   [Arch Linux forum discussion](https://bbs.archlinux.org/viewtopic.php?id=107499)
*   [Официальная документация Wayland (англ.)](http://wayland.freedesktop.org/docs/html/)
*   [Возможности Wayland (англ.)](http://www.chaosreigns.com/wiki/Wayland_State)