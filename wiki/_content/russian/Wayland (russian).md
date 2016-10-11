**Wayland** это новый протокол управления окнами для Linux. Использование Wayland требует внесения изменений в систему и повторной установки некоторых ее компонентов. Для получения дополнительной информации о Wayland смотрите [домашюю страницу](http://wayland.freedesktop.org/).

## Contents

*   [1 Требования](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [4 Weston](#Weston)
    *   [4.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
    *   [4.2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_2)
    *   [4.3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
        *   [4.3.1 XWayland](#XWayland)
        *   [4.3.2 Запись скринкаста](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_.D1.81.D0.BA.D1.80.D0.B8.D0.BD.D0.BA.D0.B0.D1.81.D1.82.D0.B0)
        *   [4.3.3 High DPI дисплеи](#High_DPI_.D0.B4.D0.B8.D1.81.D0.BF.D0.BB.D0.B5.D0.B8)
        *   [4.3.4 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
*   [5 GUI библиотеки](#GUI_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.D0.B8)
    *   [5.1 GTK+ 3](#GTK.2B_3)
    *   [5.2 Qt5](#Qt5)
    *   [5.3 Clutter](#Clutter)
    *   [5.4 SDL](#SDL)
    *   [5.5 glfw](#glfw)
    *   [5.6 EFL](#EFL)
*   [6 Оконные менеджеры и оболочки рабочего стола](#.D0.9E.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B_.D0.B8_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
*   [7 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [7.1 LLVM assertion failure](#LLVM_assertion_failure)
    *   [7.2 Не запускается Weston после обновления до 1.7](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_Weston_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B4.D0.BE_1.7)
*   [8 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Требования

В настоящее время Wayland будет работать только на системах, использующих [KMS](/index.php/KMS "KMS").

## Установка

**Примечание:** Wayland, скорее всего, установлен на вашей системе, так как является зависимостью для [gtk2](https://www.archlinux.org/packages/?name=gtk2) и [gtk3](https://www.archlinux.org/packages/?name=gtk3).

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [wayland](https://www.archlinux.org/packages/?name=wayland).

## Использование

Wayland - библиотека, которая бесполезна сама по себе. Чтобы заменить X сервер, понадобится композитный менеджер (например, [#Weston](#Weston)).

## Weston

### Установка

Установите пакет [weston](https://www.archlinux.org/packages/?name=weston).

### Использование

<caption>***Горячие клавиши** (super = клавиша windows - можно изменить, смотрите weston.ini)*</caption>
| Комманда | Действие |
| Ctrl + Alt + Backspace | Выйти из Weston |
| Super + Scroll (or PageUp/PageDown) | Увеличить/уменьшить рабочий стол |
| Super + Tab | Переключить окно |
| Super + ЛКМ | Переместить окно |
| Super + ПКМ | Повернуть окно! |
| Super + Колесо прокрутки | Изменить размер окна |
| Super + Alt + Колесо прокрутки | Изменить прозрачность окна |
| Super + K | Принудительно завершить активное окно |
| Super + KeyUp/KeyDown | Переключиться на предыдущее/следующее рабочее пространство |
| Super + Shift + KeyUp/KeyDown | Переключение рабочего пространства с захватом текущего окна |
| Super + F***n*** | Перейти на рабочее пространство ***n*** |
| Super + S | Сделать скриншот |
| Super + R | Записать скринкаст. |

Теперь, когда установлен Wayland и выполнены все требования, можно проверить его.

Можно запустить Weston прямо из активного X сеанса:

```
$ weston

```

Кроме того, Weston может быть запущен самостоятельно. Попробуйте выполнить в виртуальном терминале:

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

Пример конфигурационного файла для раскладки клавиатуры, выбранных модулей и видоизмененного интерфейса. Подробности смотрите в [странице справочного руководства](/index.php/%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0_%D1%81%D0%BF%D1%80%D0%B0%D0%B2%D0%BE%D1%87%D0%BD%D0%BE%D0%B3%D0%BE_%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%B0 "Страница справочного руководства") `weston.ini`:

 `~/.config/weston.ini` 
```
[core]
# поддержка xwayland
modules=xwayland.so

[libinput]
enable_tap=true

[shell]
background-image=/usr/share/backgrounds/gnome/Aqua.jpg
background-color=0xff002244
panel-color=0x90ff0000
locking=true
animation=zoom
close-animation=fade
focus-animation=dim-layer
#binding-modifier=ctrl
#num-workspaces=6
### для поддержки тем курсоров установите xcursor-themes из репозитория Extra. ###
#cursor-theme=whiteglass
#cursor-size=24

### настройки планшета ###
#lockscreen-icon=/usr/share/icons/gnome/256x256/actions/lock.png
#lockscreen=/usr/share/backgrounds/gnome/Garden.jpg
#homescreen=/usr/share/backgrounds/gnome/Blinds.jpg
#animation=fade

### для дисплея ноутбука ###
#[output]
#name=LVDS1
#mode=1680x1050
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

[input-method]
#path=/usr/lib/weston/weston-keyboard

[keyboard]
keymap_rules=evdev
#keymap_layout=gb,de
#keymap_options=caps:ctrl_modifier,shift:both_capslock_cancel
### keymap_options from /usr/share/X11/xkb/rules/base.lst ###
numlock-on=true

[terminal]
#font=DroidSansMono
#font-size=14

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/gnome-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[launcher]
icon=/usr/share/weston/icon_flower.png
path=/usr/bin/weston-flower

[screensaver]
# Uncomment path to disable screensaver
path=/usr/libexec/weston-screensaver
duration=600

```

#### XWayland

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland).

Если вам понадобится запускать X-приложения из Weston, он будет вызывать Xwayland для обслуживания запросов. Для этого добавьте следующие строки в файл конфигурации:

 `~/.config/weston.ini` 
```
[core]
modules=xwayland.so

```

#### Запись скринкаста

У Weston есть встроенный записыватель скринкастов, который может быть запущен и остановлен посредством комбинации клавиш `Super+r`. Скринкасты сохраняются в файл `capture.wcap` в текущей рабочей директории Weston.

Формат WCAP - особый lossless видео формат, который записывает только разницу между кадрами, характерный для Weston. Чтобы просмотреть записанный скринкаст, файл WCAP нужно преобразовать в формат, который сможет понять медиаплеер. Сначала преобразуем картинку в формат пикселей YUV:

```
$ wcap-decode capture.wcap --yuv4mpeg2 > capture.y4m

```

Файл YUV может быть преобразован в другие форматы используя [FFmpeg](/index.php/FFmpeg "FFmpeg").

#### High DPI дисплеи

Для [Retina](https://en.wikipedia.org/wiki/ru:Retina "wikipedia:ru:Retina") или [HiDPI](/index.php/HiDPI "HiDPI") дисплеев, используйте:

 `~/.config/weston.ini` 
```
[output]
name=...
scale=2

```

#### Шрифты

Weston использует стандартный шрифт sans-serif для заголовков окон, часов и прочих. Смотрите [Font configuration (Русский)#Заменить или установить шрифты по умолчанию](/index.php/Font_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D0.B8.D0.BB.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E "Font configuration (Русский)") для получения инструкций о том, как изменить этот шрифт.

## GUI библиотеки

Смотрите подробности на [официальном сайте](http://wayland.freedesktop.org/toolkits.html))

### GTK+ 3

В пакете [gtk3](https://www.archlinux.org/packages/?name=gtk3) из официальных репозиториев уже включена поддержка Wayland.

С версии GTK+ 3.0, GTK+ имеет поддержку нескольких бэкендов во время выполнения и может переключаться между ними таким же образом, Qt c lighthouse.

Когда включены оба бэкенда Wayland и X, GTK + по умолчанию будет использовать X11, но это можно изменить, переназначив переменную окружения: `GDK_BACKEND=wayland`.

### Qt5

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [qt5-wayland](https://www.archlinux.org/packages/?name=qt5-wayland).

Чтобы запустить приложение Qt5 с плагином Wayland, установите [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `QT_QPA_PLATFORM=wayland-egl` .

### Clutter

Clutter toolkit имеет бэкенд Wayland, что позволяет ему работать в качестве клиента Wayland. Бэкенд включён в официальным пакет из extra .

Для запуска Clutter на Wayland, выставите `CLUTTER_BACKEND=wayland`.

### SDL

Экспериментальная поддержка wayland доступна с версии SDL 2.0.2 и включена по умолчанию Arch Linux.

Для запуска SDL на Wayland, выставите `SDL_VIDEODRIVER=wayland`.

### glfw

Экспериментальная поддержка Wayland уже присутствует в GLFW 3.1 и может быть включена при помощи флага CMake во время компиляции `-DGLFW_USE_WAYLAND=ON`. Вы также можете [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [glfw-wayland-git](https://aur.archlinux.org/packages/glfw-wayland-git/) из AUR.

### EFL

EFL полностью поддерживает Wayland. Для запуска EFL в Wayland смотрите [страницу проекта Wayland](http://wayland.freedesktop.org/efl.html).

## Оконные менеджеры и оболочки рабочего стола

| Имя | Тип | Описание |
| GNOME | Композитный | Смотрите [GNOME#Starting GNOME](/index.php/GNOME#Starting_GNOME "GNOME"). |
| Hawaii | *(Неопределенный)* | Смотрите [Hawaii](/index.php/Hawaii "Hawaii"). |
| sway | Тайловый | [Sway](/index.php/Sway "Sway") - совместимый с i3 менеджер окон для Wayland. [Github](https://github.com/SirCmpwn/sway) |
| Enlightenment | *(Неопределенный)* | Минималистический оконный менеджер Wayland с возможностью переключать композитинг. Изначально в E19 была поддержка Wayland, но была удалена и только в E20+ поддержка признана достаточно стабильной для регулярного использования. [Больше информации](https://www.enlightenment.org/about-wayland). |
| KDE Plasma | Композитный | Смотрите [KDE#Starting Plasma](/index.php/KDE#Starting_Plasma "KDE") |
| Orbment | Тайловый | [orbment](https://github.com/Cloudef/orbment) (раньше loliwm) - тайловый менеджер окон для Wayland. |
| Velox | Тайловый | [Velox](/index.php/Velox "Velox") - простой оконный менеджер, основанный на swc. Он вдохновлен [dwm](/index.php/Dwm "Dwm") и [xmonad](/index.php/Xmonad "Xmonad"). |
| Orbital | Композитный | [Orbital](https://github.com/giucam/orbital) - композитор и оболочка Wayland, использующая Qt5 и Weston. Целью проекта является создание простой, но гибкой и красивой среды рабочего стола Wayland. Orbital не есть полноценная среда рабочего стола, а скорее всего является аналогом оконных менеджеров в мире X11, таких как [Awesome](/index.php/Awesome "Awesome") или [Fluxbox](/index.php/Fluxbox "Fluxbox"). |
| Papyros Shell | *(Неопределенный)* | [Papyros Shell](https://github.com/papyros/papyros-shell) является оболочкой рабочего стола для [Papyros](/index.php/Papyros "Papyros"), созданная посредством QtQuick и QtCompositor в качестве композитора для Wayland. |
| Maynard | *(Неопределенный)* | [Maynard](https://github.com/raspberrypi/maynard) - оболочка рабочего стола для Weston, основанная на GTK. Она была основана на weston-gtk-shell - проекте Tiago Vignatti. |
| Motorcar | *(Неопределенный)* | [Motorcar](https://github.com/evil0sheep/motorcar) - композитор Wayland для исследования 3D окон. |
| Way Cooler | Тайловый | [way-cooler](https://aur.archlinux.org/packages/way-cooler/) является настраиваемым (через конфигурационный файлы lua) композитором Wayland, написанным на Rust. Вдохновленный i3 и awesome. |

Некоторые из установленных клиентов рабочего стола Wayland могут хранить информацию в файлах `/usr/share/wayland-sessions/*.desktop` для того, чтобы запускать их в Wayland.

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