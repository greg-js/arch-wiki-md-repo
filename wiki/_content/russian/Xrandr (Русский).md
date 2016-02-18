*xrandr* - это официальная программа настройки [оконной системы X](https://en.wikipedia.org/wiki/ru:X_Window_System "wikipedia:ru:X Window System"). С ее помощью можно изменить параметры вывода изображения [RandR](https://en.wikipedia.org/wiki/ru:RandR "wikipedia:ru:RandR"). Для получения информации о настройке вывода изображения сразу на несколько мониторов смотрите статью [Multihead](/index.php/Multihead "Multihead").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Тест режимов вывода изображения](#.D0.A2.D0.B5.D1.81.D1.82_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.BE.D0.B2_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
*   [4 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
    *   [4.1 Поиск отсутствующих режимов](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D1.85_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.BE.D0.B2)
        *   [4.1.1 EDID checksum is invalid](#EDID_checksum_is_invalid)
    *   [4.2 Добавление отсутствующих режимов работы](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D1.85_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.BE.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B)
    *   [4.3 Разрешение оказалось ниже, чем хотелось бы](#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D0.BB.D0.BE.D1.81.D1.8C_.D0.BD.D0.B8.D0.B6.D0.B5.2C_.D1.87.D0.B5.D0.BC_.D1.85.D0.BE.D1.82.D0.B5.D0.BB.D0.BE.D1.81.D1.8C_.D0.B1.D1.8B)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr). Также существуют графические оболочки [arandr](https://www.archlinux.org/packages/?name=arandr) и [lxrandr](https://www.archlinux.org/packages/?name=lxrandr).

## Тест режимов вывода изображения

Если запустить *xrandr* без дополнительных параметров, то она проверит все доступные интерфейсы (`LVDS`, `VGA-0`, и.т.д.) выведет их состояние и возможные режимы работы для них.

 ` $ xrandr` 
```
Screen 0: minimum 320 x 200, current 1440 x 900, maximum 8192 x 8192
VGA disconnected (normal left inverted right x axis y axis)
LVDS connected (normal left inverted right x axis y axis)
   1440x900       59.9*+
   1280x854       59.9  
   1280x800       59.8  
...

```

Вы можете использовать *xrandr* для установки разрешения на нужном интерфейсе (режим работы с этим разрешением должен быть в списке выше):

```
$ xrandr --output LVDS --mode 1280x800

```

Если в списке присутствуют несколько режимов с одинаковым разрешением, но разной частотой, то необходимо в параметрах так же указывать нужную частоту `--rate`, либо её можно задать потом отдельно. Например:

```
$ xrandr --output LVDS --mode 1280x800 --rate 75

```

Параметр `--auto` запустит интерфейс в режиме с максимально возможными параметрами (имеющимися в списке выше).

```
$ xrandr --output LVDS --auto

```

Можно указывать несколько интерфейсов в одной команде например, выключить `LVDS` и включить `HDMI-0` в автоматическом режиме:

```
$ xrandr --output LVDS --off --output HDMI-0 --auto

```

**Обратите внимание:**

*   Изменения внесённые *xrandr* **не запоминаются** после окончания X сессии.
*   *xrandr* имеет большое количество параметров - читайте `man xrandr`.

## Настройка

*xrandr* сам по себе является простым интерфейсом для конфигурации RandR и не имеет собственных файлов конфигурации. Тем не менее существует множество способов задать нужные параметры:

1.  Сконфигурировать RandR можно без помощи *xrandr* через файлы конфигурации [X configuration files](/index.php/Xorg#Configuration "Xorg"), смотрите так же [Multihead#RandR](/index.php/Multihead#RandR "Multihead"). Это метод позволяет создать только статическую конфигурацию.
2.  Также можно использовать *xrandr* непосредственно в время запуска X сервера. Смотрите [Autostarting#Graphical](/index.php/Autostarting#Graphical "Autostarting").
3.  Динамические конфигурации можно получить используя различные скрипты вызова *xrandr* которые в свою очередь можно запускать по определённым события ( подключение, отключение интерфейсов и.т.п. ), смотрите [udev](/index.php/Udev "Udev") и [acpid](/index.php/Acpid "Acpid"). В секции [#Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B) приведено несколько скриптов.

**Обратите внимание:** В KDM и GDM есть сценарии запуска которые выполняются до запуска X сервера. Для GDM, это `/etc/gdm/`, а для KDM `/usr/share/config/kdm/Xsetup` и для SDDM это `/usr/share/sddm/scripts/Xsetup`. Этот метод требует прав на доступ к корневым каталогам и изменения файлов системных конфигураций, однако позволяет внести изменения до запуска xprofile.

### Примеры

1\. Позволяет включать интерфейс VGA или .др, отключая при этом LVDS или др.

**Обратите внимание:**

*   Для ноутбуков по умолчанию используется `$IN` LVDS.

```
#!/bin/bash

IN="LVDS1"
EXT="VGA1"

if (xrandr | grep "$EXT disconnected"); then
    xrandr --output $EXT --off --output $IN --auto
else
    xrandr --output $IN --off --output $EXT --auto
fi

```

2\. Позволяет включать интерфейс VGA или .др , и затем отключать их после отключения внешнего монитора.

```
#!/bin/bash

IN="LVDS1"
EXT="VGA1"

if (xrandr | grep "$EXT disconnected"); then
    xrandr --output $IN --auto --output $EXT --off 
else
    xrandr --output $IN --auto --primary --output $EXT --auto --right-of $IN
fi

```

3\. Позволяет автоматизировать выбор режимов работы для всех подключённых мониторов.

```
# get info from xrandr
connectedOutputs=$(xrandr | grep " connected" | sed -e "s/\([A-Z0-9]\+\) connected.*/\1/")
activeOutput=$(xrandr | grep -E " connected (primary )?[1-9]+" | sed -e "s/\([A-Z0-9]\+\) connected.*/\1/")

# initialize variables
execute="xrandr "
default="xrandr "
i=1
switch=0

for display in $connectedOutputs
do
	# build default configuration
	if [ $i -eq 1 ]
	then
		default=$default"--output $display --auto "
	else
		default=$default"--output $display --off "
	fi

	# build "switching" configuration
	if [ $switch -eq 1 ]
	then
		execute=$execute"--output $display --auto "
		switch=0
	else
		execute=$execute"--output $display --off "
	fi

	# check whether the next output should be switched on
	if [ $display = $activeOutput ]
	then
		switch=1
	fi

	i=$(( $i + 1 ))
done

# check if the default setup needs to be executed then run it
echo "Resulting Configuration:"
if [ -z "$(echo $execute | grep "auto")" ]
then
	echo "Command: $default"
	`$default`
else
	echo "Command: $execute"
	`$execute`
fi
echo -e "
$(xrandr)"

```

4\. Позволяет автоматизировать выбор режимов работы для всех подключённых мониторов.

**Обратите внимание:**

*   I am using it with [srandrd](https://aur.archlinux.org/packages/srandrd/) in my [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) like so ([#Example 3](#Example_3) didn't work for me for some reason or other):.

 `~/.xprofile` 
```
srandrd ~/.i3/detect_displays.sh

```

```
#!/bin/bash

XRANDR="xrandr"
CMD="${XRANDR}"
declare -A VOUTS
eval VOUTS=$(${XRANDR}|awk 'BEGIN {printf("(")} /^\S.*connected/{printf("[%s]=%s ", $1, $2)} END{printf(")")}')
declare -A POS
#XPOS=0
#YPOS=0
#POS="${XPOS}x${YPOS}"

POS=([X]=0 [Y]=0)

find_mode() {
  echo $(${XRANDR} |grep ${1} -A1|awk '{FS="[ x]"} /^\s/{printf("WIDTH=%s
HEIGHT=%s", $4,$5)}')
}

xrandr_params_for() {
  if [ "${2}" == 'connected' ]
  then
    eval $(find_mode ${1})  #sets ${WIDTH} and ${HEIGHT}
    MODE="${WIDTH}x${HEIGHT}"
    CMD="${CMD} --output ${1} --mode ${MODE} --pos ${POS[X]}x${POS[Y]}"
    POS[X]=$((${POS[X]}+${WIDTH}))
    return 0
  else
    CMD="${CMD} --output ${1} --off"
    return 1
  fi
}

for VOUT in ${!VOUTS[*]}
do
  xrandr_params_for ${VOUT} ${VOUTS[${VOUT}]}
done
set -x
${CMD}
set +x

```

5\. Позволяет включить интерфейс если подключённое устройство находится в спящем режиме(DisplayPort и аналоги).

```
local times=2
local seconds=1

while [ $times -gt 0 ]; do
    xrandr 1> /dev/null
    sleep $seconds
    let times-=1
done

```

## Устранение неполадок

### Поиск отсутствующих режимов

Из за различных факторов *xrandr* не всегда может корректно определить режимы работы устройств. Это можно исправить добавив нужный режим в ручную. Для начала запускаем `gtf` или `cvt` чтобы получить **Modeline** с нужными нам параметрами:

**Обратите внимание:**

*   для некоторых LCD мониторов (например samsung 2343NW), необходимо использовать "cvt -r".

 `$ cvt 1280 1024` 
```
# 1280x1024 59.89 Hz (CVT 1.31M4) hsync: 63.67 kHz; pclk: 109.00 MHz
Modeline "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync

```

**Обратите внимание:** Если используется драйвер intel [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), то необходимый режим вместе с другими параметрами можно увидеть в `/var/log/Xorg.0.log` — он может отличатся от выданного `gtf` или `cvt`:
```
[    45.063] (II) intel(0): clock: 241.5 MHz   Image Size:  597 x 336 mm
[    45.063] (II) intel(0): h_active: 2560  h_sync: 2600  h_sync_end 2632 h_blank_end 2720 h_border: 0
[    45.063] (II) intel(0): v_active: 1440  v_sync: 1443  v_sync_end 1448 v_blanking: 1481 v_border: 0

```

```
xrandr --newmode "2560x1440" 241.50 2560 2600 2632 2720 1440 1443 1448 1481 -hsync +vsync

```

Теперь можно создать новый режим для xrandr:

**Обратите внимание:** Modeline из строки нужно убрать.

```
$ xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync

```

После создания необходимо добавить режим для интерфейса на котором вы будете его использовать.

**Обратите внимание:** добавлять необходимо только название режима.

```
$ xrandr --addmode VGA1 1280x1024_60.00

```

После этого можно его использовать:

```
$ xrandr --output VGA1 --mode 1280x1024_60.00

```

**Обратите внимание:** Изменения внесённые *xrandr* **не запоминаются** после окончания X сессии.

Для тестирования режимов лучше всего использовать конструкции типа (которые после таймаута восстанавливают прежний режим):

```
$ xrandr --output VGA1 --mode 1280x1024_60.00 && sleep 5 && xrandr --newmode "1024x768-safe" 65.00 1024 1048 1184 1344 768 771 777 806 -HSync -VSync && xrandr --addmode VGA1 1024x768-safe && xrandr --output VGA1 --mode 1024x768-safe

```

#### EDID checksum is invalid

Если приведущий метод приводит к ошибке `*ERROR* EDID checksum is invalid`, смотрите [KMS#Forcing modes and EDID](/index.php/KMS#Forcing_modes_and_EDID "KMS") и [[1]](http://askubuntu.com/questions/201081/how-can-i-make-linux-behave-better-when-edid-is-unavailable).

### Добавление отсутствующих режимов работы

После того как нашли нужный режим с помощью `xrandr`, его можно добавить в `/etc/X11/xorg.conf.d/*`:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Monitor"
    Identifier "VGA1"
    Modeline "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync
    Option "PreferredMode" "1280x1024_60.00"
EndSection

Section "Screen"
    Identifier "Screen0"
    Monitor "VGA1"
    DefaultDepth 24
    SubSection "Display"
        Modes "1280x1024_60.00"
    EndSubSection
EndSection

Section "Device"
    Identifier "Device0"
    Driver "intel"
EndSection
```

**Обратите внимание:** Не забывайте изменять драйвер `intel` на нужный, например `nvidia`.

### Разрешение оказалось ниже, чем хотелось бы

**Обратите внимание:** Сначала попробуйте этот метод [#Поиск отсутствующих режимов](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D1.85_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.BE.D0.B2).

Background: ATI X1550 based video card and two LCD monitors DELL 2408(up to 1920x1200) and Samsung 206BW(up to 1680x1050). Upon first login after installation, the resolution default to 1152x864\. xrandr does not list any resolution higher than 1152x864\. You may want to try editing /etc/X11/xorg.conf.d/*, add a section about virtual screen, logout, login and see if this helps. If not then read on.

change /etc/X11/xorg.conf.d/*

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Screen"
        ...
        SubSection "Display"
                Virtual 3600 1200
        EndSubSection
EndSection

```

About the numbers: DELL on the left and Samsung on the right. So the virtual width is of sum of both LCD width 3600=1920+1680; Height then is figured as the max of them, which is max(1200,1050)=1200\. If you put one LCD above the other, use this calculation instead: (max(width1, width2), height1+height2).

## Смотрите также

*   [https://wiki.ubuntu.com/X/Config/Resolution](https://wiki.ubuntu.com/X/Config/Resolution)
*   [RandR 1.2 tutorial](http://wiki.debian.org/XStrikeForce/HowToRandR12)
*   [Xorg RandR 1.2 on ThinkWiki](http://www.thinkwiki.org/wiki/Xorg_RandR_1.2)
*   [FAQVideoModes - more information about modelines](http://www.x.org/wiki/FAQVideoModes#ObtainingmodelinesfromWindowsprogramPowerStrip)