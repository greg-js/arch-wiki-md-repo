## Contents

*   [1 Xbindkeys](#Xbindkeys)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Xbindkeysrc](#Xbindkeysrc)
    *   [3.2 Настройка с помощью графической оболочки](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B9_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
*   [4 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [5 Simulating multimedia keys](#Simulating_multimedia_keys)
*   [6 Troubleshooting](#Troubleshooting)

## Xbindkeys

Xbindkeys - программа, позволяющая назначать команды клавишам (в том числе мультимедийным) или сочетаниям клавиш. Она независима от DE/WM и может быть полезна, если вы часто их меняете.

## Установка

Установить xbindkeys можно из extra-репозитория:

```
# pacman -S xbindkeys

```

Также в [AUR](/index.php/AUR "AUR") доступна графическая оболочка [[1]](https://aur.archlinux.org/packages.php?ID=4200) для xbindkeys.

## Настройка

Создайте файл `.xbindkeysrc` в вашей домашней директории:

```
touch ~/.xbindkeysrc

```

Теперь вы можете редактировать его вручную, либо воспользоваться для настройки графической утилитой [[2]](https://aur.archlinux.org/packages.php?ID=4200).

### Xbindkeysrc

Посмотреть формат конфигурационного файла можно командой:

```
xbindkeys -k

```

Появится пустое окно. Нажимайте клавиши (сочетания клавиш), для которых вы хотите назначить команды и xbindkeys выведет вам кусок конфигурации, который можно использовать в `~/.xbindkeysrc`. Например, нажатие Alt + o приведёт к такому выводу:

```
"(Scheme function)"
    m:0x8 + c:32
    Alt + o

```

Первая строка содержит команду. Вторая - состояние (0x8) и код (32) клавиши, полученные `xev`. В третьей строке содержится удобочитаемое название клавиши (сочетания клавиш), соответствующее предоставленным кодам. Что-бы использовать этот вывод, скопируйте все три строки в файл `~/.xbindkeysrc` и замените "(Scheme function)" той командой, которою вы хотите назначить на соответствующую клавишу (сочетание клавиш). Ниже представлен пример конфигурационного файла для управления громкостью с помощью Fn-сочетаний. Символом # обозначаются комментарии.

```
# Increase volume
"amixer set Master playback 1+"
    m:0x0 + c:123
    XF86AudioRaiseVolume

# Decrease volume
"amixer set Master playback 1-"
    m:0x0 + c:122
    XF86AudioLowerVolume

# Toggle mute
"amixer set Master toggle"
    m:0x0 + c:121
    XF86AudioMute

```

**Tip:** Use *xbindkeys -mk* to keep the key prompt open for multiple keypresses. Press *q* to quit.

### Настройка с помощью графической оболочки

Просто запустите:

```
xbindkeys_config

```

## Использование

После настройки xbindkeys откройте `~/.xinitrc` и поместите

```
xbindkeys

```

перед командой старта вашего WM/DE.

## Simulating multimedia keys

The XF86Audio* and other multimedia keys[[3]](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols) are pretty-much well-recognized by the major DEs. For keyboards without such keys, you can simulate their effect with other keys

```
# Decrease volume on pressing Super-minus
"amixer set Master playback 1-"
   m:0x50 + c:20
   Mod2+Mod4 + minus

```

However, to actually call the keys themselves you can use tools like xdotool[[4]](http://www.semicomplete.com/projects/xdotool/) (its in [community]) and xmacro[[5]](http://xmacro.sourceforge.net/) (in the AUR). Unfortunately since you'd already be holding down some modifier key (Super or Shift, for example), X will see the result as Super-XF86AudioLowerVolume which won't do anything useful. Here's a script based on xmacro and xmodmap from the xorg-server-utils package for doing this[[6]](https://bbs.archlinux.org/viewtopic.php?pid=843395).

```
#!/bin/sh
echo 'KeyStrRelease Super_L KeyStrRelease minus' | xmacroplay :0;
xmodmap -e 'remove Mod4 = Super_L';
echo 'KeyStrPress XF86AudioLowerVolume KeyStrRelease XF86AudioLowerVolume' | xmacroplay :0;
xmodmap -e 'add Mod4 = Super_L';

```

This works for calling XF86AudioLowerVolume once (assuming you're using Super-minus), but repeatedly calling it without releasing the Super key (like tapping on a volume button) doesn't work. If you'd like it to work that way, add the following line to the bottom of the script.

```
echo 'KeyStrPress Super_L' | xmacroplay :0

```

With this modified script, if you press the key combination fast enough your Super_L key will remain 'on' till the next time you hit it, which may result in some interesting side-effects. Just tap it again to remove that state, or use the original script if you want things to 'just work' and do not mind not multi-tapping on volume up/down.

These instructions are valid for pretty much any one of the XF86 multimedia keys (important ones would be XF86AudioRaiseVolume, XF86AudioLowerVolume, XF86AudioPlay, XF86AudioPrev, XF86AudioNext).

## Troubleshooting

If, for any reason, a hotkey you *already* set in `~/.xbindkeysrc` doesn't work, open up a terminal and type the following:

```
xbindkeys -n

```

By pressing the non-working key, you will be able to see any error xbindkeys encounter (e.g: mistyped command/keycode,...).