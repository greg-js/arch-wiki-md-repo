NVIDIA Optimus - технология, которая дает интегрированной графике Intel и дискретной Nvidia работать сообща в лаптопах. Чтобы заставить Optimus работать в Arch Linux потребуется сделать несколько непростых шагов, описанных ниже. Вот доступные решения:

*   отключить один из графических адаптеров в BIOS, что увеличит продолжительность работы батареи, если отключить чип Nvidia. Но это невозможно сделать в некоторых BIOS.
*   использование официальной поддержки Optimus включенной в проприетарный драйвер [Nvidia](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)"), который предоставит хороший опыт работы, в сравнении с [nouveau](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)"), с картами Nvidia, но не поддерживает переключения GPU и содержит больше ошибок.
*   использование функционала [PRIME](/index.php/PRIME "PRIME"), входящего в свободные драйвера [nouveau](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)").Эти драйвера поддерживают переключение GPU, но предоставляют более низкую производительность, чем проприетарный драйвер [Nvidia](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)"), также, до сих пор, не реализовано никакого энергосбережения.
*   использование [Bumblebee](/index.php/Bumblebee_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bumblebee (Русский)"), решения сторонних разработчиков для реализации функционала подобного Optimus, поддерживающего переключение GPU и энергосбережение, но требующего более тонкой настройки.

## Contents

*   [1 Отключение одного из GPU](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B8.D0.B7_GPU)
*   [2 Используя драйвера Nvidia](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_Nvidia)
*   [3 Альтернативная конфигурация](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
*   [4 Экранные менеджеры](#.D0.AD.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
    *   [4.1 LightDM](#LightDM)
    *   [4.2 SDDM](#SDDM)
    *   [4.3 GDM](#GDM)
    *   [4.4 KDM](#KDM)
    *   [4.5 Проверка 3D](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_3D)
*   [5 Проблемы](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [5.1 Тиринг](#.D0.A2.D0.B8.D1.80.D0.B8.D0.BD.D0.B3)
    *   [5.2 EDID errors in Xorg.log](#EDID_errors_in_Xorg.log)
*   [6 Используя nouveau](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_nouveau)
*   [7 Используя Bumblebee](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_Bumblebee)

## Отключение одного из GPU

Если требуется использовать только один из видеоадаптеров, проверьте опции BIOS. Найдите опцию, отключающую один из них. Некоторые лаптопы поддерживают отключение только одного из чипов. Если необходимо использовать обе видеокарты или невозможно отключить ту, что не нужна ищите решение ниже.

## Используя драйвера Nvidia

Проприетарный драйвер [Nvidia](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") не поддерживает динамического переключения в отличие от [nouveau](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)"). В наличии проблемы с тирингом, о которых Nvidia знает, но не спешит исправлять. Однако, эти драйвера предоставляют более высокую производительность в сравнении с драйверами [nouveau](/index.php/Nouveau_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nouveau (Русский)").

Первым делом, установите пакеты [nvidia](https://www.archlinux.org/packages/?name=nvidia), [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl) и [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) из официальных репозиториев. После настройте xorg.conf. Узнайте PCI адрес карты Nvidia, для этого введите: $ lspci | grep -E "VGA|3D"

PCI адрес выглядит примерно так 01:00.0\. В xorg.conf, отредактируйте 01:00.0 на 1:0:0.

**Примечание:** Начиная с Xorg-server 1.17-1 [FS#43830](https://bugs.archlinux.org/task/43830) связана с модулем modesetting сохраняющимся в конфигурациях Optimus. Решением для некоторых систем является установка Option "AccelMethod" в "none" как описано ниже. Для других же подойдет "sna", смотреть [#Альтернативная конфигурация](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F).

**Примечание:** В некоторых системах эта настройка нарушает автоматическое определение параметров монитора драйверами nvidia через файл EDID. В таком случае смотрите [#EDID errors in Xorg.log](#EDID_errors_in_Xorg.log).

Если X.ORG X сервер версии 1.17.2 и выше:

 `/etc/X11/xorg.conf` 
```
Section "Module"
    Load "modesetting"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "тут>"
    Option "AllowEmptyInitialConfiguration"
EndSection

```

Для более старых версий X сервера:

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
    Identifier "layout"
    Screen 0 "nvidia"
    Inactive "intel"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    **# Change BusID if necessary.**
    **BusID "PCI:1:0:0"**
EndSection

Section "Screen"
    Identifier "nvidia"
    Device "nvidia"
    Option "AllowEmptyInitialConfiguration" "Yes"
EndSection

Section "Device"
    Identifier "intel"
    Driver "modesetting"
    **# Change BusID if necessary.**
    **BusID "PCI:0:2:0"**
    Option "AccelMethod" "none"
EndSection

Section "Screen"
    Identifier "intel"
    Device "intel"
EndSection

```

Далее добавьте в начало ~/.xinitrc две строки:

```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

Теперь перезагрузитесь для запуска драйверов и X. Если dpi дисплея не верный добавьте строку:

 `xrandr --dpi96` 

Если при загрузке X появился черный экран, удостоверьтесь, что в файле ~/.xinitrc нет & перед xrandr. Если & есть, то видимо оконный менеджер запускается раньше, чем команда xrandr завершает выполнение, что и приводит к черному экрану.

Если черный экран еще есть, смотрите [#Альтернативная конфигурация](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F) ниже.

## Альтернативная конфигурация

Если возникли сбои в работе Xorg-server 1.17.1 и выше с описанной выше конфигурацией, измените раздел для Intel в /etc/X11/xorg.conf как показано ниже:

 `/etc/X11/xorg.conf` 
```
Section "Device"
    Identifier "intel"
    Driver "modesetting"
    BusID "PCI:0:2:0"
    Option "AccelMethod" "sna"
    #Option "TearFree" "True"
    #Option "Tiling" "True"
    #Option "SwapbuffersWait" "True"
EndSection
```

Как указано выше BusID должен совпадать с выводом lspci. Найдите строку с "VGA compatible controller", которая содержит "Intel". Например: $ lspci | grep VGA 00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)

Если X запустился, но на экране ничего не происходит, проверьте содержит ли /var/log/xorg.conf подобную строку:

 `/var/log/xorg.conf` 
```
[ 16112.937] (EE) Screen 1 deleted because of no matching config section.

```

Если да, проблема может исчезнуть при добавлении раздела ServeLayout в /etc/X11/xorg.conf

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
    Identifier "layout"
    Screen 1 "nvidia"
    Inactive "intel"
EndSection

```

## Экранные менеджеры

При использовании менеджеров входа, создайте или отредактируйте скрипт настройки вместо использования ~/.xinitrc.

### LightDM

Для LightDM:

 `/etc/lightdm/display_setup.sh` 
```
#!/bin/sh
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

Сделайте этот скрипт выполняемым:

 `# chmod +x /etc/lightdm/display_setup.sh` 

Теперь настройте LightDM для запуска скрипта, отредактировав раздел [Seat:*] в /etc/lightdm/lightdm.conf:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
display-setup-script=/etc/lightdm/display_setup.sh
```

Теперь перезагрузитесь и DM запуститься.

### SDDM

 `/usr/share/sddm/scripts/Xsetup` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

### GDM

Для GDM создайте новый файл .desktop:

 `/usr/share/grm/greeter/autostart/optimus.desktop` 
```
[Desktop Entry]
Type=Application
Name=Optimus
Exec=sh -c "xrandr --setprovideroutputsource modesetting NVIDIA-0; xrandr --auto"
NoDisplay=true
X-GNOME-Autostart-Phase=DisplayServer
```

Удостоверьтесь, что GDM использует X как стандартный бэкенд.

### KDM

Для KDM, добавьте строки xrandr в файл /usr/share/config/kdm/Xsetup.

### Проверка 3D

Для проверки работает ли чип Nvidia установите mesa-demos и запустите: $ glxinfo |grep NVIDIA

## Проблемы

### Тиринг

К сожалению, эта проблема на данный момент не имеет решения и известна Nvidia.

### EDID errors in Xorg.log

Эта ошибка возникает когда драйвер [nvidia](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)") не определяет EDID для дисплея. Необходимо вручную указать путь к файлу EDID или предоставить ту же информацию подобным образом.

Для предоставления пути к файлу EDID отредактируйте раздел "Device" для NVIDIA в Xorg.conf, добавив эти строки. **Не забудьте изменить поля в соответствии с вашей системой**:

 `/etc/X11/xorg.conf` 
```
Section "Device"
    Option "ConnectedMonitor" "CRT-0"
    Option "CustomEDID" "CRT-0:/sys/class/drm/card0-LVDS-1/edid"
    Option "IgnoreEDID" "false"
    Option "UseEDID" "true"
EndSection
```

Если Xorg не запускается попробуйте поменять ссылки CRT на DFB. card0 это идентификатор чипа Intel, который подключен к дисплею с помощью LVDS. Если расположение аппаратных средств отличается, значение пользовательского EDID может быть другим. Путь же будет начинаться с /sys/class/drm.

## Используя nouveau

Свободные драйвера nouveau ([xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau))могут динамически переключаться с драйвером Intel ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)) используя технологию PRIME. Для более подробной информации смотрите [PRIME](/index.php/PRIME "PRIME").

## Используя Bumblebee

Если хотите использовать Bumblebee, который поддерживает энергосбережение и другие полезные функции, смотрите [Bumblebee](/index.php/Bumblebee "Bumblebee").