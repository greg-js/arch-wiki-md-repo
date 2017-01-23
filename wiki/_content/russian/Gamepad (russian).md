Работа с джойстиками в Linux подразумевает некоторые сложности. Не потому что они плохо поддерживаются, а потому, что вам нужно определить, какие модули подключить, чтобы ваш геймпад заработал, а это не всегда очевидно.

## Contents

*   [1 Системы ввода для геймпадов](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0_.D0.B4.D0.BB.D1.8F_.D0.B3.D0.B5.D0.B9.D0.BC.D0.BF.D0.B0.D0.B4.D0.BE.D0.B2)
*   [2 Определение нужных модулей](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D1.83.D0.B6.D0.BD.D1.8B.D1.85_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
    *   [2.1 Подключение модулей для аналоговых устройств](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D0.B4.D0.BB.D1.8F_.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D1.8B.D1.85_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [2.2 Джойстики USB](#.D0.94.D0.B6.D0.BE.D0.B9.D1.81.D1.82.D0.B8.D0.BA.D0.B8_USB)
*   [3 Проверка конфигурации](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Joystick API](#Joystick_API)
    *   [3.2 evdev API](#evdev_API)
*   [4 Настройка "мертвых зон" и калибровка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.22.D0.BC.D0.B5.D1.80.D1.82.D0.B2.D1.8B.D1.85_.D0.B7.D0.BE.D0.BD.22_.D0.B8_.D0.BA.D0.B0.D0.BB.D0.B8.D0.B1.D1.80.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [4.1 "Мертвые зоны" в wine](#.22.D0.9C.D0.B5.D1.80.D1.82.D0.B2.D1.8B.D0.B5_.D0.B7.D0.BE.D0.BD.D1.8B.22_.D0.B2_wine)
    *   [4.2 "Мертвые зоны" в Xorg](#.22.D0.9C.D0.B5.D1.80.D1.82.D0.B2.D1.8B.D0.B5_.D0.B7.D0.BE.D0.BD.D1.8B.22_.D0.B2_Xorg)
    *   [4.3 "Мертвые зоны" Joystick API](#.22.D0.9C.D0.B5.D1.80.D1.82.D0.B2.D1.8B.D0.B5_.D0.B7.D0.BE.D0.BD.D1.8B.22_Joystick_API)
    *   [4.4 "Мертвые зоны" evdev API](#.22.D0.9C.D0.B5.D1.80.D1.82.D0.B2.D1.8B.D0.B5_.D0.B7.D0.BE.D0.BD.D1.8B.22_evdev_API)
    *   [4.5 Настройка кривых](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D1.80.D0.B8.D0.B2.D1.8B.D1.85)
*   [5 Отключение управления мышью при помощи джойстика](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BC.D1.8B.D1.88.D1.8C.D1.8E_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D0.B4.D0.B6.D0.BE.D0.B9.D1.81.D1.82.D0.B8.D0.BA.D0.B0)
*   [6 Использование джойстика для отправки нажатия клавиш](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B6.D0.BE.D0.B9.D1.81.D1.82.D0.B8.D0.BA.D0.B0_.D0.B4.D0.BB.D1.8F_.D0.BE.D1.82.D0.BF.D1.80.D0.B0.D0.B2.D0.BA.D0.B8_.D0.BD.D0.B0.D0.B6.D0.B0.D1.82.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
    *   [6.1 при помощи X.org](#.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_X.org)
*   [7 Специфические устройства](#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
    *   [7.1 Танцевальные платформы](#.D0.A2.D0.B0.D0.BD.D1.86.D0.B5.D0.B2.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.BB.D0.B0.D1.82.D1.84.D0.BE.D1.80.D0.BC.D1.8B)
    *   [7.2 Logitech Thunderpad Digital](#Logitech_Thunderpad_Digital)
    *   [7.3 Контроллер Nintendo Gamecube](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80_Nintendo_Gamecube)
    *   [7.4 Контроллер PlayStation 3/4](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80_PlayStation_3.2F4)
        *   [7.4.1 Подключение через Bluetooth](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Bluetooth)
    *   [7.5 Steam Controller](#Steam_Controller)
        *   [7.5.1 Wine](#Wine)
    *   [7.6 Контроллер Xbox 360](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80_Xbox_360)
        *   [7.6.1 SteamOS xpad](#SteamOS_xpad)
        *   [7.6.2 xboxdrv](#xboxdrv)
            *   [7.6.2.1 Несколько контроллеров](#.D0.9D.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80.D0.BE.D0.B2)
            *   [7.6.2.2 Имитация контроллера XBox360 другими контроллерами](#.D0.98.D0.BC.D0.B8.D1.82.D0.B0.D1.86.D0.B8.D1.8F_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80.D0.B0_XBox360_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D0.BC.D0.B8_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80.D0.B0.D0.BC.D0.B8)
                *   [7.6.2.2.1 Logitech Dual Action](#Logitech_Dual_Action)
                *   [7.6.2.2.2 Контроллер PlayStation 2 через адаптер USB](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80_PlayStation_2_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_.D0.B0.D0.B4.D0.B0.D0.BF.D1.82.D0.B5.D1.80_USB)
                *   [7.6.2.2.3 Контроллер PlayStation 2 через USB](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80_PlayStation_2_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_USB)
                *   [7.6.2.2.4 Контроллер PlayStation 2 через Bluetooth](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80_PlayStation_2_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Bluetooth)
                *   [7.6.2.2.5 Контроллер PlayStation 4](#.D0.9A.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.BB.D0.B5.D1.80_PlayStation_4)
*   [8 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [8.1 Перемещение курсора мыши джойстиком](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D0.B0_.D0.BC.D1.8B.D1.88.D0.B8_.D0.B4.D0.B6.D0.BE.D0.B9.D1.81.D1.82.D0.B8.D0.BA.D0.BE.D0.BC)
    *   [8.2 Джойстик не работает в играх на FNA/SDL](#.D0.94.D0.B6.D0.BE.D0.B9.D1.81.D1.82.D0.B8.D0.BA_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.B2_.D0.B8.D0.B3.D1.80.D0.B0.D1.85_.D0.BD.D0.B0_FNA.2FSDL)
    *   [8.3 Геймпад не распознается никакими программами](#.D0.93.D0.B5.D0.B9.D0.BC.D0.BF.D0.B0.D0.B4_.D0.BD.D0.B5_.D1.80.D0.B0.D1.81.D0.BF.D0.BE.D0.B7.D0.BD.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BD.D0.B8.D0.BA.D0.B0.D0.BA.D0.B8.D0.BC.D0.B8_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B0.D0.BC.D0.B8)
    *   [8.4 Не работает Steam Controller](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_Steam_Controller)

## Системы ввода для геймпадов

Вообще, в Linux имеется две различных системы ввода для джойстиков. Оригинальный интерфейс 'Joystick' и более новый, основанный на 'evdev'.

`/dev/input/jsX` указывают на интерфейс API 'Joystick', а `/dev/input/event*` - на варианты с 'evdev'(то же относится и к другим устройствам, таким, как мыши и клавиатуры). Символические ссылки на эти устройства также находятся тут: `/dev/input/by-id/` и тут: `/dev/input/by-path/`, где традиционные названия, использующие API 'Joystick' заканчиваются на `-joystick`, в то время, как использующие'evdev' - на `-event-joystick`.

Большинство новых игр используют по умолчанию интерфейс 'evdev', так как он поддерживает более детализированную информацию о доступных кнопках и аналоговых стиках, а также поддерживает функцию обратной связи.

Хотя SDL1.x по умолчанию использует интерфейс 'evdev', вы можете принудительно заставить ее использовать старый API 'Joystick', установив переменную окружения `SDL_JOYSTICK_DEVICE=/dev/input/js0`. Это может помочь во многих играх, таких, как X3\. SDL2.x поддерживает только новый интерфейс 'evdev'.

Также стоит упомянуть, что существует еще драйвер xorg `xf86-input-joystick`. Он лишь позволяет вам контролировать клавиатуру и мышь при помощи джойстика в xorg, что не актуально для большинства пользователей. Отключение этой функции описано ниже в [Disable Joystick From Controlling Mouse](#Disable_Joystick_From_Controlling_Mouse), но в большинстве случаев вам нужно просто-напросто удалить этот пакет.

## Определение нужных модулей

Если вы не используете совсем старый джойстик, который использует гейм-порт или собственный USB-протокол, вам понадобятся только стандартные USB HID модули.

Для подробного изучения модулей, связанных с джойстиками в Linux, вам нужно получить доступ к исходным кодам ядра Linux - в особенности к секции Documentation. К сожалению, пакеты ядра pacman не содержат необходимой информации. Если у вас есть скачанные исходные коды ядра, посмотрите в `Documentation/input/joystick.txt`. Вы также можете просматривать дерево ядра на сайте [kernel.org](https://kernel.org/), нажав ссылку "browse" для ядра, которые вы используете, а затем нажав на ссылку "tree" вверху. Вот ссылка на документацию по [последней версии ядра](https://git.kernel.org/cgit/linux/kernel/git/stable/linux-stable.git/tree/Documentation/input/joystick.txt).

Некоторые геймпады требуют специфических модулей. Например, такие, как контроллер Microsoft Sidewinder (`sidewinder`) или цифровые контроллеры Logitech (`adi`). Множество старых моделей джойстиков будут работать с простым модулем `analog`. Если ваш джойстик подключается к гейм-порту звуковой карты, вам понадобятся драйверы для вашей звуковой карты, однако, для некоторых из них, например для SoundBlaster Live, имеется специальный драйвер гейм-порта (`emu10k1-gp`). Старинные карты с интерфейсом ISA могут потребовать модуль `ns558`, который является стандартным модулем для гейм-порта.

Как видите, существует большое количество различных модуей, которые могут понадобиться, чтобы ваш джойстик заработал в Linux, так что в рамках этой статьи невозможно рассмотреть все варианты. Пожалуйста, изучите документацию, упомянутую выше, для более подробной информации.

### Подключение модулей для аналоговых устройств

Вам нужно подключить модуль для вашего гейм-порта (`ns558`, `emu10k1-gp`, `cs461x`, и т.д. ...), модуль джойстика (`analog`, `sidewinder`, `adi`, и т.д...) и в конце концов - драйвер джойстика для ядра (`joydev`). Создайте новый файл с названиями этих модулей в `/etc/modules-load.d/`, либо просто используйте modprobe. Модуль `gameport` должен подключиться автоматически, т.к. является зависимым от других.

### Джойстики USB

Просто используйте modprobe для драйвера джойстика (`usbhid` и `joydev`). Если у вас мышь и клавиатура USB, модуль `usbhid` уже подключен, и вам остается только подключить модуль `joydev`.

## Проверка конфигурации

Когда все модули подключены, вы должны увидеть новое устройство `/dev/input/js0` и файл, заканчивающийся на `-event-joystick` в папке `/dev/input/by-id`. Просто используйте `cat` на этих файлах устройств, чтобы понять, что джойстик работает - покрутите стики, понажимайте кнопки, вы увидите кракозябры, выводимые на экран при взаимодействии с джойстиком.

Оба интерфейса также поддерживаются wine и определяются как отдельные устройства. Это можно проверить при помощи `wine control joy.cpl`.

### Joystick API

Существует много приложений, которые позволяют проверить работу джойстика с использованием этого старого API, наиболее простое - `jstest` из пакета [joyutils](https://www.archlinux.org/packages/?name=joyutils). Если вывод программы сложно прочитать из-за того, что строка слишком длинная, вы можете воспользоваться графическими средствами. В KDE4 есть встроенная утилита в панели Input Devices системных настроек. Также можно воспользоваться пакетом [jstest-gtk-git](https://aur.archlinux.org/packages/jstest-gtk-git/).

Пользоваться `jstest` очень просто - просто запустите `jstest /dev/input/js0`, и программа начнет выводить строку с состоянием всех осей стиков (нормализованных к {-32767,32767}) и кнопок.

При запуске `jstest-gtk`, программа покажет список всех доступных геймпадов, и вам нужно будет только выбрать один из них и нажать кнопку "Properties"

### evdev API

Новый API 'evdev' может быть проверен с использованием программы проверки геймпада SDL2, либо при помощи программы `evtest` из репозитория community. Установите [sdl2-jstest-git](https://aur.archlinux.org/packages/sdl2-jstest-git/), а затем запустите `sdl2-jstest --test 0`. Если у вас подключено несколько контроллеров, используйте `sdl2-jstest --list`, чтобы вывести список их ID.

Для проверки обратной связи геймпада, используйте `fftest` из пакета `linuxconsole`:

```
$ fftest /dev/input/by-id/usb-*event-joystick

```

## Настройка "мертвых зон" и калибровка

Если вы хотите настроить "мертвые зоны" (или вовсе убрать их) для ваших аналоговых устройств ввода, вы должны сделать это отдельно для xorg (для эмуляции клавиатуры и мыши), Joystick API и evdev API.

### "Мертвые зоны" в wine

Добавьте следующую запись в реестр и пропишите ей строковое значение от 0 до 10000 (затрагивает все оси стиков)

```
HKEY_CURRENT_USER\Software\Wine\DirectInput\DefaultDeadZone

```

Источник: [UsefulRegistryKeys](http://wiki.winehq.org/UsefulRegistryKeys)

### "Мертвые зоны" в Xorg

Добавьте примерно такую строку в `/etc/X11/xorg.conf.d/50-joystick.conf` перед `EndSection`:

```
Option "MapAxis1" "deadzone=1000"

```

1000 - это значение по умолчанию, но вы можете сделать его любым между 0 и 30 000\. Чтобы узнать номер оси, смотрите раздел "Проверка конфигурации" этой статьи. Если вы знаете номер конкретной оси, просто допишите `deadzone=value` после пробела в конце параметра.

### "Мертвые зоны" Joystick API

Самый простой способ - использовать `jstest-gtk` из пакета [jstest-gtk-git](https://aur.archlinux.org/packages/jstest-gtk-git/). Выберите контроллер, который вы хотите отредактировать, нажмите кнопку "Calibration" внизу диалогового окна (**не нажимайте** "Start Calibration" в этом окне!). Теперь вы можете установить значения параметров CenterMin и CenterMax (которые отвечают за центральную "мертвую зону"), RangeMin и RangeMax, которые отвечают за крайние точки "мертвых зон". Учтите, что настройки калибровки применяются, когда приложение подключается к геймпаду, так что вам придется перезапустить игру или приложение, чтобы увидеть изменения в калибровке.

После настройки "мертвых зон", используйте `jscal`, чтобы создать новый шелл-скрипт с нужными значениями.

```
$ jscal -p /dev/input/jsX > jscal.sh # replace X with your joystick's number 
$ chmod +x jscal.sh

```

Теперь вам нужно создать правило для [udev](/index.php/Udev "Udev"), например `/etc/udev/rules.d и назвать его 85-jscal.rules`, чтобы скрипт автоматически выполнялся, когда вы подключаете контроллер:

```
SUBSYSTEM=="input", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="c268", ACTION=="add", RUN+="/usr/bin/jscal.sh"

```

Для получения idVendor и idProduct, используйте `udevadm info --attribute-walk --name /dev/input/jsX`. Если у вас несколько джойстиков, используйте названия `/dev/input/by-id/*-joystick`.

### "Мертвые зоны" evdev API

В данный момент не существует отдельного приложения, позволяющего откалибровать джойстик для `evdev` API, но есть `G25manage`, распространяемое вместе с игрой VDrift, которое позволяет настраивать центральные "мертвые зоны".

Самый простой способ получить VDrift - скачать его ([github](https://github.com/VDrift/vdrift/tree/master/tools/G25manage)) и скомпилировать при помощи `make`.

После этого вы сможете изменить конфигурацию при помощи:

```
$ ./G25manage --showcalibration /dev/input/by-id/usb-*-event-joystick

```

Для изменения "мертвых зон" любых осей, используйте следующую команду:

```
$ ./G25manage --evdev /dev/input/by-id/usb-*-event-joystick --axis 0 --deadzone 0

```

Используйтесь файлом правил udev для установки новых значений автоматически при подключении джойстика.

Учтите, что внутри ядра этот параметр называется `flatness` и устанавливается при помощи `EVIOCSABS` `ioctl`.

Конфигурация по умолчанию будет выглядеть примерно так:

 `$ ./G25manage --showcalibration /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick` 
```
Supported Absolute axes:
   Absolute axis 0x00 (0) (X Axis) (min: 0, max: 65535, flatness: 4095 (=6.25%), fuzz: 255)
   Absolute axis 0x01 (1) (Y Axis) (min: 0, max: 65535, flatness: 4095 (=6.25%), fuzz: 255)
   Absolute axis 0x05 (5) (Z Rate Axis) (min: 0, max: 4095, flatness: 255 (=6.23%), fuzz: 15)
   Absolute axis 0x10 (16) (Hat zero, x axis) (min: -1, max: 1, flatness: 0 (=0.00%), fuzz: 0)
   Absolute axis 0x11 (17) (Hat zero, y axis) (min: -1, max: 1, flatness: 0 (=0.00%), fuzz: 0)
```

В то время, как более удачная настройка может быть достигнута примерно так (повторить для каждой оси):

 `$ ./G25manage --evdev /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick --axis 0 --deadzone 512` 
```
Event device file: /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick
 Axis index to deal with: 0
 New dead zone value: 512
 Trying to set axis 0 deadzone to: 512
   Absolute axis 0x00 (0) (X Axis) Setting deadzone value to : 512
 (min: 0, max: 65535, flatness: 512 (=0.78%), fuzz: 255)
```

### Настройка кривых

Если ваша игра использует ограниченное количество кнопок или поддерживает несколько контроллеров, можно достичь хороших результатов используя `xboxdrv` для изменения кривых джойстика.

Ниже приведены настройки, которые я использовал для Saitek X-55 HOTAS:

```
$ xboxdrv --evdev /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Throttle_G0000021-event-joystick \
  --evdev-no-grab --evdev-absmap 'ABS_#40=x1,ABS_#41=y1,ABS_X=x2,ABS_Y=y2' --device-name 'Hat and throttle' \
  --ui-axismap 'x2^cal:-32000:0:32000=,y2^cal:-32000:0:32000=' --silent

```

Это привязывает событие EV_ABS с id 40 и 41 (используйте xboxdrv с параметром --evdev-debug для просмотра списка зарегистрированных событий), которое является обычно недоступным "курсором мыши" на гашетке, на первый геймпад и гашетку второго геймпада, а также закрепляет верхние и нижние границы, потому что они не всегда полностью обрабатываются.

Немного интереснее настройка для стика:

```
$ xboxdrv --evdev /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick \
  --evdev-no-grab --evdev-absmap 'ABS_X=x1' --evdev-absmap 'ABS_Y=y1' --device-name 'Joystick' \
  --ui-axismap 'x1^cal:-32537:-455:32561=,x1^dead:-900:700:1=,x1^resp:-32768:-21845:-2000:0:2000:21485:32767=' \
  --ui-axismap 'y1^cal:-32539:-177:32532=,y1^dead:-700:2500:1=,y1^resp:-32768:-21845:-2000:0:2000:21485:32767=' \
  --evdev-absmap 'ABS_RZ=x2' --ui-axismap 'x2^cal:-32000:-100:32000,x2^dead:-1500:1000:1=,x2^resp:-32768:-21845:-2000:0:2000:21485:32767=' \
  --silent

```

Здесь осуществляется привязка трех осей джойстика к осям геймпада и меняется их калибровка (минимальное значение, среднее значение, максимальное значение), "мертвые зоны" (отрицательная сторона, положительная сторона, флаг для включения сглаживания) и, наконец, смена кривой джойстика на более плоскую в середине.

Вы также можете изменить отзывчивость, установив значение 'sen' (sensitivity). Установка этого значения в 0 даст вам линейную чувствительность, значение -1 - очень неотзывчивую ось, а значение 1 - очень отзывчивую. Можно использовать средние значения, чтобы сделать ее более или менее отзывчивой. Xboxdrv использует квадратичную формулу для подсчета финального значение, так что установка значения этого параметра даст более "гладкий" эффект, чем установка значения 'rest', приведенная выше.

Еще одна полезная функция xboxdrv - программа может работать как со старым Joystick API, так и с новым evded, так что она должна быть совместима практически с каждым приложением.

## Отключение управления мышью при помощи джойстика

Если вы хотите играть в игры при помощи контроллера, вы, возможно, захотите отключить управление курсором мыши при помощью джойстика. Чтобы сделать это, отредактируйте файл /etc/X11/xorg.conf.d/50-joystick.conf примерно так:

 `/etc/X11/xorg.conf.d/50-joystick.conf ` 
```
Section "InputClass"
        Identifier "joystick catchall"
        MatchIsJoystick "on"
        MatchDevicePath "/dev/input/event*"
        Driver "joystick"
        Option "StartKeysEnabled" "False"       #Отключение поддержки
        Option "StartMouseEnabled" "False"      #мыши
EndSection
```

## Использование джойстика для отправки нажатия клавиш

Существует несколько программ, позволяющих отправлять нажатия клавиш при помощи джойстика, таких, как, например, [rejoystick](https://aur.archlinux.org/packages/rejoystick/), [qjoypad](https://aur.archlinux.org/packages/qjoypad/) или [antimicro-qt4](https://aur.archlinux.org/packages/antimicro-qt4/). Все они не требуют дополнительной настройки X.org.

### при помощи X.org

Это хорошее решение для систем, где перезагрузка Xorg случается очень редко, потому что это статическая конфигурация, загружаемая только при запуске X. Я использую его на моем медиа-сервере под управлением XBMC с Logitech Cordless RublePad 2\. Из-за проблемы с тем, что "крестовина" распознается как еще одна ось, мне приходилось запускать [Joy2key](/index.php/Joy2key "Joy2key") в качестве обходного пути. Когда я обновился до XBMC 11.0 с joy2key 1.6.3-1, эта настройка перестала работать. Так что в конце-концов я решил заставить Xorg обрабатывать события джойстика.

Для начала, убедитесь, что у вас установлен [xf86-input-joystick](https://aur.archlinux.org/packages/xf86-input-joystick/). Затем создайте файл `/etc/X11/xorg.conf.d/51-joystick.conf` примерно такого вида:

```
 Section "InputClass"
  Identifier "Joystick hat mapping"
  Option "StartKeysEnabled" "True"
  #MatchIsJoystick "on"
  Option "MapAxis5" "keylow=113 keyhigh=114"
  Option "MapAxis6" "keylow=111 keyhigh=116"
 EndSection

```

**Note:** Строка *MatchIsJoystick "on"* вроде как не нужна для этого файла, но вы, возможно, захотите раскомментировать ее

Отключение управления мышью при помощи джойстика

## Специфические устройства

В то время, как большинство джойстиков, особенно USB-совместимые, просто должны работать, некоторые могут потребовать альтернативные драйверы (или будут лучше работать при их использовании). Если ничего не заработало с первого раза, не отчаивайтесь и еще раз вдумчиво прочитайте документацию!

### Танцевальные платформы

Большинство танцевальных платформ просто работают. Однако, некоторые платформы, особенно от игровых консолей, которые подключаются через адаптер, частенько грешат тем, что привязывают кнопки направлений к осям. Это приводит к тому, что "влево-вправо" или "вверх-вниз" нажимаются одновременно. Для устройств, распознанных xpad, это можно поправить при помощи модулей:

```
 # modprobe -r xpad
 # modprobe xpad dpad_to_buttons=1

```

### Logitech Thunderpad Digital

В Logitech Thunderpad Digital не будут отображаться все кнопки, если вы используете модуль `analog`. Воспользуйтесь специальным модулем `adi` для этого контроллера.

### Контроллер Nintendo Gamecube

Отключение управления мышью при помощи джойстика У Dolphin Emulator есть [вики-страница](https://wiki.dolphin-emu.org/index.php?title=How_to_use_the_Official_GameCube_Controller_Adapter_for_Wii_U_in_Dolphin), на которой объясняется, как пользоваться официальным USB-адаптером Nintendo с контроллером от Gamecube. Эта конфигурация также работает с адаптером контроллера Mayflash, если установить переключатель в положение "Wii U".

По умолчанию контроллер будет зарегистрирован [udev](/index.php/Udev "Udev"), но будет доступен только для пользователя root. Вы можете исправить это, добавив правило для udev:

 `/etc/udev/rules.d/51-gcadapter.rules`  `SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="0337", MODE="0666"` 

Это свяжет устройство USB с определенными ID изготовителя и продукта, а также установит разрешения для файла устройства в 0666, чтобы программы, запущенные не из-под root, могли получить доступ к контроллеру.

Перезагрузить udev и применить новую конфигурацию можно при помощи

```
 # udevadm control --reload-rules

```

### Контроллер PlayStation 3/4

Отключение управления мышью при помощи джойстика Контроллеры Dualshock 3, Dualshock 4 и Sixaxis будут работать прямо "из коробки", будучи подключенными к USB (для начала работы необходимо нажать кнопку PS). Также возможна работа с ними через Bluetooth.

Steam корректно распознает их как геймпады от PS3, так что можно включить режим Big Picture, нажав кнопку PS. В режиме Big Picture и в некоторых играх, эти геймпады могут вести себя как контроллеры от Xbox 360\. Управление курсором мыши при помощи геймпада по умолчанию включено. Если вы хотите выключить его, см. [#Отключение управления мышью при помощи джойстика](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BC.D1.8B.D1.88.D1.8C.D1.8E_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D0.B4.D0.B6.D0.BE.D0.B9.D1.81.D1.82.D0.B8.D0.BA.D0.B0)

##### Подключение через Bluetooth

Установите пакеты [bluez-plugins](https://www.archlinux.org/packages/?name=bluez-plugins) и [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), в состав которого входит плагин *sixaxis*. Затем сделайте [start](/index.php/Start "Start") `bluetooth.service`, подключите контроллер по USB, и плагин автоматически пошлет адрес вашего адаптера bluetooth в контроллер.

Теперь можно отключить контроллер, в следующий раз, когда вы нажмете кнопку PS, он подключится без дополнительных действий. Только не забывайте отключать контроллер, когда закончите, иначе, он будет оставаться подключенным, включенным и будет разряжаться батарея.

### Steam Controller

Пакет [steam](https://www.archlinux.org/packages/?name=steam) (начиная с версии 1.0.0.51-1) позволяет распознать контроллер и предоставляет эмуляцию клавиатуры/мыши/геймпада пока запущен Steam. Для работы эмуляции геймпада, нужно включить внутриигровое наложение в Steam. Вам, возможно, понадобится запустить `udevadm trigger` от root или отключить и вновь подключить донгл, если контроллер не работает сразу же после установки и запуска Steam. Если ничего не помогает, попробуйте перезагрузить компьютер, когда донгл подключен.

Если вы не можете заставить Steam Controller работать, см. [#Steam Controller Not Pairing](#Steam_Controller_Not_Pairing).

В качестве альтернативы, можете установить [python-steamcontroller-git](https://aur.archlinux.org/packages/python-steamcontroller-git/), чтобы заработала эмуляция контроллера и мыши без Steam.

#### Wine

Вы можете также использовать [python-steamcontroller-git](https://aur.archlinux.org/packages/python-steamcontroller-git/) для работы со Steam Controller в играх, запущенных из-под Wine. Вам нужно найти и скачать файл `xbox360cemu.v.3.0.rar` (например, отсюда: [ссылка с 2shared](http://www.2shared.com/file/wcq8xuPf/xbox360cemuv30.html)). Затем скопируйте файлы `dinput8.dll`, `xbox360cemu.ini`, `xinput1_3.dll` и `xinput_9_1_0.dll` в папку с файлом запуска игры. Отредактируйте `xbox360cemu.ini`, изменив только следующие значения в разделе `[PAD1]`, чтобы корректно переназначить конфигурацию Steam Controller в XBox Controller.

 `xbox360cemu.ini` 
```
Right Analog X=4
Right Analog Y=-5
A=1
B=2
X=3
Y=4
Back=7
Start=8
Left Thumb=10
Right Thumb=11
Left Trigger=a3
Right Trigger=a6
```

Теперь запустите python-steamcontroller в режиме Xbox360 (`sc-xbox.py start`). Возможно, вы также захотите скопировать `XInputTest.exe` из `xbox360cemu.v.3.0.rar` в ту же папку и запустить этот файл при помощи Wine, чтобы проверить работу геймпада. Однако, эмуляция клавиатуры и мыши при помощи этого метода не работает.

### Контроллер Xbox 360

Как проводные, так и беспроводные (с модулем *Xbox 360 Wireless Receiver for Windows*) модели поддерживаются модулем ядра `xpad` и должны работать без установки дополнительных пакетов.

Имеются сообщения о проблемах с некоторыми новыми моделями проводных и беспроводных контроллерах при использовании стандартного драйвера xpad, такие, как:

*   некорректное назначение кнопок. ([обсуждение на баг-трекере Steam](https://github.com/ValveSoftware/steam-for-linux/issues/95#issuecomment-14009081))
*   неработающая синхронизация. Все четыре зеленых индикатора моргают, но контроллер работает. ([обсуждение на форуме Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=156028))

Если вы испытываете подобные проблемы, можете использовать либо [#SteamOS xpad](#SteamOS_xpad), либо [#xboxdrv](#xboxdrv) вместо стандартного драйвера `xpad`.

Если вы хотите управлять мышью при помощи контроллера, либо назначить кнопки клавишам, используйте пакет [xf86-input-joystick](https://aur.archlinux.org/packages/xf86-input-joystick/) (дополнительную информацию о настройке см. `man joystick`). Если курсор мыши блокируется в углу экрана, может помочь изменение параметра `MatchDevicePath` в файле `/etc/X11/xorg.conf.d/50-joystick.conf` с `/dev/input/event*` на `/dev/input/js*`.

**Совет:** Если вы пользуетесь программой управления питанием [TLP](/index.php/TLP "TLP"), могут возникнуть проблемы с подключением Microsoft Wireless Adapter (например, LED-индикатор может погаснуть через пару секунд после подключения адаптера, и контроллер не подключится). Это происходит из-за функции автоматического "засыпания" USB при использовании TLP, решением является добавление ID Wireless Adapter в черный список этой функции. (USB_BLACKLIST, см [настройку TLP](http://linrunner.de/en/tlp/docs/tlp-configuration.html#usb) для дополнительной информации).

#### SteamOS xpad

Если у вас возникли проблемы со стандартным модулем ядра `xpad`, вы можете установить версию SteamOS. Также известно о проблемах совместимости беспроводных геймпадов Xbox360 с играми, созданными при помощи GameMaker Studio. Если вы столкнетесь с такой проблемой, единственный известный выход - использовать xboxdrv. В YoYo Games отказались рассматривать это как баг продукта, поэтому вряд ли, что когда-нибудь проблема будет решена.

Для начала убедитесь, что у вас в системе установлен и запущен [DKMS](/index.php/DKMS "DKMS"), затем установите модифицированный модуль ядра [steamos-xpad-dkms](https://aur.archlinux.org/packages/steamos-xpad-dkms/). В процессе установки вы увидите сообщение о том, что новый модуль ядра xpad подключен к вашему текущему ядру:

```
Creating symlink /var/lib/dkms/steamos-xpad-dkms/0.1/source ->
                 /usr/src/steamos-xpad-dkms-0.1

DKMS: add completed.

Kernel preparation unnecessary for this kernel.  Skipping...

Building module:
cleaning build area....
make KERNELRELEASE=3.12.8-1-ARCH KVERSION=3.12.8-1-ARCH....
cleaning build area....

```

Затем выгрузите старый модуль и подключите новый:

```
# rmmod xpad
# modprobe steamos-xpad

```

Или просто перезагрузите компьютер.

#### xboxdrv

xboxdrv - это альтернатива `xpad`, которая предоставляет бОльший функционал и может лучше работать с некоторыми контроллерами. Xboxdrv работает в пользовательском окружении и может быть запущен как системная служба. Установите его при помощи пакета [xboxdrv](https://aur.archlinux.org/packages/xboxdrv/). Затем выполните [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `xboxdrv.service`.

##### Несколько контроллеров

xboxdrv поддерживает несколько контроллеров, но они должны быть сконфигурированы в `/etc/default/xboxdrv`. Для каждого дополнительного контроллера добавьте строку `next-controller = true`. Например, при использовании четырех контроллеров, добавьте ее три раза:

```
 [xboxdrv]
 silent = true
 next-controller = true
 next-controller = true
 next-controller = true
 [xboxdrv-daemon]
 dbus = disabled

```

Затем сделайте [restart](/index.php/Restart "Restart") `xboxdrv.service`.

##### Имитация контроллера XBox360 другими контроллерами

xboxdrv может использоваться для регистрации любого контроллера в качестве контроллера Xbox 360 с помощью `--mimic-xpad`. Это может помочь в играх, которые поддерживают контроллеры Xbox360, но имеют проблемы с обнаружением или работой с другими геймпадами.

Для начала вам нужно выяснить, как называется каждая кнопка вашего контроллера. Для этого можно использовать [evtest](https://www.archlinux.org/packages/?name=evtest). Выполните `evtest` и выберите ID события устройства (`/dev/input/event*`), относящийся к вашему контроллеру. Нажимайте кнопки на контроллере и двигайте стики, чтобы прочитать их названия.

Пример вывода:

```

Event: time 1380985017.964843, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90003
Event: time 1380985017.964843, type 1 (EV_KEY), code 290 (BTN_THUMB2), value 1
Event: time 1380985017.964843, -------------- SYN_REPORT ------------
Event: time 1380985018.076843, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90003
Event: time 1380985018.076843, type 1 (EV_KEY), code 290 (BTN_THUMB2), value 0
Event: time 1380985018.076843, -------------- SYN_REPORT ------------
Event: time 1380985018.460841, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90002
Event: time 1380985018.460841, type 1 (EV_KEY), code 289 (BTN_THUMB), value 1
Event: time 1380985018.460841, -------------- SYN_REPORT ------------
Event: time 1380985018.572835, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90002
Event: time 1380985018.572835, type 1 (EV_KEY), code 289 (BTN_THUMB), value 0
Event: time 1380985018.572835, -------------- SYN_REPORT ------------
Event: time 1380985019.980824, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90006
Event: time 1380985019.980824, type 1 (EV_KEY), code 293 (BTN_PINKIE), value 1
Event: time 1380985019.980824, -------------- SYN_REPORT ------------
Event: time 1380985020.092835, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90006
Event: time 1380985020.092835, type 1 (EV_KEY), code 293 (BTN_PINKIE), value 0
Event: time 1380985020.092835, -------------- SYN_REPORT ------------
Event: time 1380985023.596806, type 3 (EV_ABS), code 3 (ABS_RX), value 18
Event: time 1380985023.596806, -------------- SYN_REPORT ------------
Event: time 1380985023.612811, type 3 (EV_ABS), code 3 (ABS_RX), value 0
Event: time 1380985023.612811, -------------- SYN_REPORT ------------
Event: time 1380985023.708768, type 3 (EV_ABS), code 3 (ABS_RX), value 14
Event: time 1380985023.708768, -------------- SYN_REPORT ------------
Event: time 1380985023.724772, type 3 (EV_ABS), code 3 (ABS_RX), value 128
Event: time 1380985023.724772, -------------- SYN_REPORT ------------

```

В данном случае `BTN_THUMB`, `BTN_THUMB2` и `BTN_PINKIE` являются кнопками, а `ABS_RX` - это ось Х аналогового стика. Теперь можно имитировать контроллер Xbox360 следующей командой:

```
$ xboxdrv --evdev /dev/input/event* --evdev-absmap ABS_RX=X2 --evdev-keymap BTN_THUMB2=a,BTN_THUMB=b,BTN_PINKIE=rt --mimic-xpad

```

Приведенный выше пример является неполным. Он привязывает только одну ось стика и три кнопки в качестве примера. Используйте `xboxdrv --help-button`, чтобы узнать названия кнопок и осей стиков контроллера Xbox360 и привязать их в соответствии с командой выше. Привязки осей стиков должны следовать после `--evdev-absmap`, а привязки кнопок - после `--evdev-keymap` (список, разделенный запятыми; без пробелов).

По умолчанию xboxdrv выводит все события в терминал. Таким образом, можно понять, что все привязки являются корректными. Используйте опцию `--silent`, чтобы отключить вывод в терминал.

###### Logitech Dual Action

Геймпад Logitech Dual Action очень похож (в контексте привязки кнопок) на геймпад от PS2, но некторые кнопки и гашетки нужно поменять местами, чтобы имитировать контроллер Xbox.

```
 # xboxdrv --evdev /dev/input/event* \
   --evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RZ=x2,ABS_Z=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
   --axismap -Y1=Y1,-Y2=Y2 \
   --evdev-keymap BTN_TRIGGER=x,BTN_TOP=y,BTN_THUMB=a,BTN_THUMB2=b,BTN_BASE3=back,BTN_BASE4=start,BTN_BASE=lt,BTN_BASE2=rt,BTN_TOP2=lb,BTN_PINKIE=rb,BTN_BASE5=tl,BTN_BASE6=tr \
   --mimic-xpad --silent

```

###### Контроллер PlayStation 2 через адаптер USB

Чтобы исправить назначение кнопок адаптеров PS2 и имитировать контроллер Xbox, выполните следующую команду:

```
 # xboxdrv --evdev /dev/input/event* \
   --evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RZ=x2,ABS_Z=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
   --axismap -Y1=Y1,-Y2=Y2 \
   --evdev-keymap   BTN_TOP=x,BTN_TRIGGER=y,BTN_THUMB2=a,BTN_THUMB=b,BTN_BASE3=back,BTN_BASE4=start,BTN_BASE=lb,BTN_BASE2=rb,BTN_TOP2=lt,BTN_PINKIE=rt,BTN_BASE5=tl,BTN_BASE6=tr \
   --mimic-xpad --silent

```

###### Контроллер PlayStation 2 через USB

Если взять контроллер PS3 и подключить его по USB, xboxdrv не нужно указывать никаких привязок (они встроены). Просто запустите программу (и отключите текущий запущенный драйвер), и все заработает.

```
# xboxdrv --silent --detach-kernel-driver

```

###### Контроллер PlayStation 2 через Bluetooth

Подключив контроллер по Bluetooth, найдите его адрес при помощи `bluetoothctl`. Затем создайте новое правило для udev следующего содержания:

 `/etc/udev/rules.d/99-dualshock.rules`  `KERNEL=="event*", SUBSYSTEM=="input", ATTRS{uniq}=="<device_addr_you_got_on_pairing>", SYMLINK+="input/dualshock3"` 

Адрес контроллера пишется строчными буквами, например `06:9a:b4:c8:ef:8b`.

Теперь запустите xboxdrv:

```
$ xboxdrv --evdev /dev/input/dualshock3 --mimic-xpad

```

###### Контроллер PlayStation 4

Чтобы исправить привязяки кнопок контроллера PS4, воспользуйтесь следующей командой xboxdrv (или попробуйте программу [ds4drv](https://github.com/chrippa/ds4drv)):

```
 # xboxdrv  \                                                                      
   --evdev /dev/input/by-id/usb-Sony_Computer_Entertainment_Wireless_Controller-event-joys>
   --evdev-absmap ABS_X=x1,ABS_Y=y1                 \                               
   --evdev-absmap ABS_Z=x2,ABS_RZ=y2                \                               
   --evdev-absmap ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \                               
   --evdev-keymap BTN_A=x,BTN_B=a                   \                               
   --evdev-keymap BTN_C=b,BTN_X=y                   \                               
   --evdev-keymap BTN_Y=lb,BTN_Z=rb                 \                               
   --evdev-keymap BTN_TL=lt,BTN_TR=rt               \
   --evdev-keymap BTN_SELECT=tl,BTN_START=tr        \                               
   --evdev-keymap BTN_TL2=back,BTN_TR2=start        \                               
   --evdev-keymap BTN_MODE=guide                    \                               
   --axismap -y1=y1,-y2=y2                          \                               
   --mimic-xpad                                     \                               
   --silent

```

## Решение проблем

### Перемещение курсора мыши джойстиком

Иногда USB-геймпад может быть распознан как HID-совместимая мышь (только в сеансе X, несмотря на то, что он установлен как устройство `/dev/input/js0`). Известная проблема - когда курсоры мыши передвигается стиками джойстика или блокируется на краю экрана. Если ваша программа может определить геймпад сама, можете удалить пакет xf86-input-joystick. Более элегантное решение - [#Отключение управления мышью при помощи джойстика](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BC.D1.8B.D1.88.D1.8C.D1.8E_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D0.B4.D0.B6.D0.BE.D0.B9.D1.81.D1.82.D0.B8.D0.BA.D0.B0).

### Джойстик не работает в играх на FNA/SDL

Если вы пользуетесь ноунейм-геймпадом, вы можете столкнуться с проблемами с его определением в играх на SDL. С [14 мая 2015](https://github.com/flibitijibibo/FNA/commit/e55742cfe7e38b778a21ed8a12cb2f2081490d8d) вы можете положить файл `gamecontrollerdb.txt` в папку с запускаемым файлом гры на FNA, например, [SDL_GameControllerDB](https://github.com/gabomdq/SDL_GameControllerDB).

Другой способ, который подходит также для более ранних версий FNA и SDL - создание привязки кнопок самостоятельно. Для этого необходимо скачать исходники SDL отсюда: [http://libsdl.org/](http://libsdl.org/), перейти в папку `/test/`, собрать программу `controllermap.c` (или установить пакет [controllermap](https://aur.archlinux.org/packages/controllermap/)) и запустить тест. После завершения теста controllermap, будет сгенерирован guid, который нужно подставить в переменную окружения `SDL_GAMECONTROLLERCONFIG`, которой в последствии будут пользоваться игры на SDL/FNA. Например:

```
 $ export SDL_GAMECONTROLLERCONFIG="030000008f0e00000300000010010000,GreenAsia Inc. USB Joystick ,platform:Linux,x:b3,a:b2,b:b1,y:b0,back:b8,start:b9,dpleft:h0.8,dpdown:h0.0,dpdown:h0.4,dpright:h0.0,dpright:h0.2,dpup:h0.0,dpup:h0.1,leftshoulder:h0.0,leftshoulder:b6,lefttrigger:b4,rightshoulder:b7,righttrigger:b5,leftstick:b10,rightstick:b11,leftx:a0,lefty:a1,rightx:a3,righty:a2,"

```

### Геймпад не распознается никакими программами

Некоторые программы, например, Steam, могут распознать только первый джойстик, с которым столкнутся. Из-за бага в драйвере беспроводных устройств Microsoft, это может быть донгл bluetooth от беспроводной клавиатуры или мыши. Если вы увидите, что `/dev/input/js*` и `/dev/input/event*` принадлежат приемнику bluetooth-клавиатуры, вы можете автоматически избавиться от них, создав соответствующие правила udev. Создайте `/`:

 `/etc/udev/rules.d/99-btcleanup.rules` 
```
ACTION=="add", KERNEL=="js[0-9]*", SUBSYSTEM=="input", KERNELS=="...", ATTRS{bInterfaceSubClass}=="00", ATTRS{bInterfaceProtocol}=="00", ATTRS{bInterfaceNumber}=="02", RUN+="/usr/bin/rm /dev/input/js%n"
ACTION=="add", KERNEL=="event*", SUBSYSTEM=="input", KERNELS=="...", ATTRS{bInterfaceSubClass}=="00", ATTRS{bInterfaceProtocol}=="00", ATTRS{bInterfaceNumber}=="02", RUN+="/usr/bin/rm /dev/input/event%n"

```

Correct the `KERNELS=="..."`. Узнать нужные значения можно так:

```
# udevadm info -an /dev/input/js0

```

Предпожим, что устройство "под вопросом" - это `/dev/input/js0`. После создания правила выполните:

```
# udevadm control --reload

```

Затем переподключите проблемное устройство. Файлы должны исчезнуть.

### Не работает Steam Controller

Если Steam Controller не подключается в беспроводном режиме, но работает с использованием кабеля, вам, возможно, необходимо создать следующее правило udev, предложенное Valve [[1]](https://steamcommunity.com/app/353370/discussions/0/490123197956024380/):

`/lib/udev/rules.d/99-steam-controller-perms.rules`

```
# This rule is needed for basic functionality of the controller in Steam and keyboard/mouse emulation
SUBSYSTEM=="usb", ATTRS{idVendor}=="28de", MODE="0666"

# This rule is necessary for gamepad emulation; make sure you replace 'pgriffais' with a group that the user that runs Steam belongs to
KERNEL=="uinput", MODE="0660", GROUP="steamcontroller", OPTIONS+="static_node=uinput"

```

Также создайте группу пользователей Steam Controller:

```
# groupadd steamcontroller

```

И добавьте своего пользователя в эту группу:

```
# gpasswd -a $USER steamcontroller

```