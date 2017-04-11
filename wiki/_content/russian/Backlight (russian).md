Контролировать яркость экрана бывает непросто. На многих компьютерах нет физического переключателя, а вместо него используются программные решения, которые не всегда работают как положено. Однако, чаще всего это возможно. Найдите работающий способ для вашего оборудования. Слишком яркие экраны могут привести к потере зрения!

Существует много способов регулировать яркость подсветки монитора, экрана ноутбука или встроенной экранной панели (как в iMac) с помощью программного обеспечения, но в зависимости от оборудования и модели иногда доступны не все варианты. В данной статье предпринимается попытка обобщить все возможные пути регулирования яркости подсветки экрана.

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
*   [2 ACPI](#ACPI)
    *   [2.1 Параметры ядра](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [2.2 Правило Udev](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D0.BE_Udev)
*   [3 Выключение подсветки](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D1.81.D0.B2.D0.B5.D1.82.D0.BA.D0.B8)
*   [4 Служба systemd-backlight](#.D0.A1.D0.BB.D1.83.D0.B6.D0.B1.D0.B0_systemd-backlight)
*   [5 Утилиты настройки](#.D0.A3.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [5.1 xbacklight](#xbacklight)
    *   [5.2 Другие утилиты](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B)
    *   [5.3 setpci](#setpci)
*   [6 Color correction](#Color_correction)
    *   [6.1 xcalib](#xcalib)
    *   [6.2 Xflux](#Xflux)
    *   [6.3 redshift](#redshift)
    *   [6.4 NVIDIA settings](#NVIDIA_settings)
    *   [6.5 Increase brightness above maximum level](#Increase_brightness_above_maximum_level)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Backlight PWM modulation frequency (Intel i915 only)](#Backlight_PWM_modulation_frequency_.28Intel_i915_only.29)
    *   [7.2 Inverted Brightness (Intel i915 only)](#Inverted_Brightness_.28Intel_i915_only.29)
    *   [7.3 sysfs modified but no brightness change](#sysfs_modified_but_no_brightness_change)

## Обзор

Существует несколько способов контролировать яркость. В соответствии с этим обуждением [[1]](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/397617) и этой wiki страницей [[2]](https://wiki.ubuntu.com/Kernel/Debugging/Backlight), способы контроля делятся на следующие категории:

*   яркость управляется горячей клавишей, определённой производителем, и нет интерфейса для того, чтобы ОС могла настраивать яркость.
*   яркость можно контролировать через ACPI или через графический драйвер.
*   яркость можно контролировать посредством аппаратного регистра с помощью setpci.

Все методы доступны пользователю через `/sys/class/backlight` и xrandr/xbacklight может выбрать один способ контролировать яркость. Пока еще не совсем понятно, который из способов xbacklight предпочитает по умолчанию.

*Смотрите [FS#27677](https://bugs.archlinux.org/task/27677) для xbacklight, если вам выдает "No outputs have backlight property."* Есть временное решение, в случае если xrandr/xbacklight не выбирает нужную папку в `/sys/class/backlight`: Вы можете указать ту, которая вам нужна в xorg.conf, внеся имя той папки в поле "Backlight" секции Device (смотрите [https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741) внизу страницы для более подробной информации).

## ACPI

Яркость подсветки экрана регулируется установлением уровня питания светодиодов или катодов. Уровень питания может часто контролироваться с помощью ACPI модуля ядра для видео. Интерфейс к этому модулю доступен через папку sysfs в `/sys/class/backlight`.

Имя папки зависит от модели видеокарты.

 `# ls /sys/class/backlight/` 
```
acpi_video0

```

Именно эта подсветка - управляется видеокартой ATI. В видеокарте Intel она называется `intel_backlight`. В следующем примере используется `acpi_video0`.

Папка содержит следующие файлы и папки:

 `# ls /sys/class/backlight/acpi_video0/` 
```
actual_brightness  brightness         max_brightness     subsystem/    uevent             
bl_power           device/            power/             type

```

Максимальную яркость можно прочитать из `max_brightness`, которая обычно равна 15.

 `# cat /sys/class/backlight/acpi_video0/max_brightness` 
```
15

```

Яркость может быть изменена, написав число в `brightness`. Здесь невозможно использовать число выше максимальной яркости.

```
# tee /sys/class/backlight/acpi_video0/brightness <<< 5

```

### Параметры ядра

Иногда ACPI не работает должным образом из-за различных реализаций материнской платы и особенностей ACPI. Этому могут быть подвержены некоторые ноутбуки с двойной графикой (например, выделенный графический процессор Nvidia / Radeon с интегрированным графическим процессором Intel / AMD). На ноутбуках с Nvidia Optimus параметр ядра nomodeset может помешать регулировке подсветки.

Кроме того, иногда может быть необходимо зарегистрировать свою собственную подсветку `acpi_video0`, даже если другая уже существует (например, `intel_backlight`), что может быть достигнуто добавлением следующих [параметров ядра](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_backlight=video
acpi_backlight=vendor
acpi_backlight=native

```

Если вы обнаружите, что изменение подсветки `acpi_video0` на самом деле не изменяет яркость, вам может потребоваться использовать `acpi_backlight=none`.

**Совет:**

*   На ноутбуках Asus вам может также понадобиться загрузить [модуль ядра](/index.php/Kernel_module "Kernel module") `asus-nb-wmi`.
*   Отключение legacy-загрузки на Dell XPS13 приводит к невозможности изменить подсветку.

### Правило Udev

Если доступен интерфейс ACPI, уровень подсветки может быть установлен во время загрузки с использованием правила [udev](/index.php/Udev "Udev"):

 `/etc/udev/rules.d/81-backlight.rules` 
```
# Установить уровень подсветки равным 8
SUBSYSTEM=="backlight", ACTION=="add", KERNEL=="acpi_video0", ATTR{brightness}="8"
```

**Примечание:** Служба systemd-backlight восстанавливает предыдущий уровень яркости подсветки во время загрузки. Чтобы предотвратить конфликты для указанных выше правил, см. [#Служба systemd-backlight](#.D0.A1.D0.BB.D1.83.D0.B6.D0.B1.D0.B0_systemd-backlight).

**Совет:** Чтобы настроить подсветку в зависимости от состояния питания, см. [Power management#Using a script and an udev rule](/index.php/Power_management#Using_a_script_and_an_udev_rule "Power management") и используйте выбранную вами [утилиту](#.D0.A3.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8) в скрипте.

## Выключение подсветки

Выключение подсветки (например, при закрытии крышки ноутбука) может быть полезно для сохранения заряда батареи. Выполните следующую команду:

```
$ sleep 1 && xset dpms force off

```

Подсветка должна включиться снова при движении мыши или вводе с клавиатуры. Если предыдущая команда не работает, есть шанс, что `vbetool` заработает. Отметьте, однако, что в этом случае подсветка должна быть вручную активирована снова. Выполните:

```
$ vbetool dpms off

```

Чтобы снова включить подсветку:

```
$ vbetool dpms on

```

Например, это можно использовать при закрытии крышки ноутбука с помощью [Acpid](/index.php/Acpid "Acpid").

## Служба systemd-backlight

Пакет [systemd](/index.php/Systemd "Systemd") содержит "static" службу `systemd-backlight@.service`, которая включена по умолчанию. Она сохраняет яркость подсветки во время выключения ПК и восстанавливает при включении. Эта служба использует ACPI метод, описанный в [#ACPI](#ACPI), создавая службы для каждой папки, найденной в `/sys/class/backlight/`. Например, если есть папка `acpi_video0`, она создаст службу `systemd-backlight@backlight:acpi_video0.service`. Если вы используете другие методы установки яркости во время загрузки, рекомендуется [маскировать](/index.php/Mask "Mask") службу `systemd-backlight@.service`, чтобы сделать невозможным ее запуск.

Некоторые ноутбуки имеют несколько видеоадаптеров (как Optimus) и восстановление подсветки не выполняется в следствие ошибок. Попробуйте [маскировать](/index.php/Systemd#Using_units "Systemd") *instance* этой службы, например `systemd-backlight@backlight\:acpi_video1` в случае `acpi_video1`.

Из man-страницы systemd-backlight@.service:

systemd-backlight принимает следующий параметр командной строки:

```
systemd.restore_state=

```

Принимает логическое значение. По умолчанию "1".

Если "0", не восстанавливает настройки яркости во время загрузки. Однако, настройки будут всё равно сохраняться при выключении.

## Утилиты настройки

### xbacklight

Яркость может быть установлена с помощью пакета [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight).

**Примечание:**

*   xbacklight работает только с intel. Radeon не поддерживает свойство подсветки RandR.
*   xbacklight в настоящий момент не работает с modesetting-драйвером [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=96572).

Чтобы установить яркость в 50% от максимальной:

```
$ xbacklight -set 50

```

Приращения могут использоваться вместо абсолютных значений, например, для увеличения или уменьшения яркости на 10%:

```
$ xbacklight -inc 10
$ xbacklight -dec 10

```

Гамма может быть установлена с использованием пакета [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) или [xorg-xgamma](https://www.archlinux.org/packages/?name=xorg-xgamma). Следующие команды создают одинаковый эффект.

```
$ xrandr --output LVDS1 --gamma 1.0:1.0:1.0
$ xgamma -rgamma 1 -ggamma 1 -bgamma 1

```

**Совет:** Эти команды могут быть привязаны к клавишам клавиатуры, как описано в [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

Если вы сталкиваетесь с ошибкой "No outputs have backlight property", это потому, что xrandr/xbacklight не выбирает правильную папку в `/sys/class/backlight`. Вы можете указать папку, настроив опцию `Backlight` в device-разделе файла xorg.conf. К примеру, если имя папки `intel_backlight`, раздел device может быть настроен следующим образом:

 `/etc/X11/xorg.conf` 
```
Section "Device"
    Identifier  "Card0"
    Driver      "intel"
    Option      "Backlight"  "intel_backlight"
EndSection
```

См. [FS#27677](https://bugs.archlinux.org/task/27677) и [[4]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741) для подробностей.

### Другие утилиты

*   **light** — Light последователь *LightScript*.

	[https://github.com/haikarainen/light](https://github.com/haikarainen/light) || [light](https://aur.archlinux.org/packages/light/)

*   **acpilight** — acpilight содержит "xbacklight"-совместимую утилиту, которая использует sys файловую систему для установки яркости экрана. Т.к. она не использует X вообще, ее также можно использовать в консоли и с Wayland. Она не имеет проблем с KMS драйверами. Кроме того, на ноутбуках ThinkPad можно также настраивать подсветку клавиатуры.

	[https://github.com/wavexx/acpilight/](https://github.com/wavexx/acpilight/) || [acpilight](https://aur.archlinux.org/packages/acpilight/)

*   **illum** — ilum следит за клавишами увеличения и уменьшения яркости на всех устройствах ввода (с помощью libevdev) и настраивает яркость по нажатию клавиши (через sysfs). Написана для новых BIOS/UEFI, которые не обрабатывают нажатия этих клавиш за вас. Это альтернатива обработке этих клавиш через acpi или с помощью горячих клавиш x11/wm.

	[https://github.com/jmesmon/illum](https://github.com/jmesmon/illum) || [illum-git](https://aur.archlinux.org/packages/illum-git/)

*   **relight** — Этот пакет предоставляет `relight.service`, [systemd](/index.php/Systemd "Systemd")-службу для автоматического восстановления предыдущих настроек подсветки во время перезагрузки вместе с использованием ACPI метода, описанного выше, и *relight-menu* — диалоговое меню для выбора и настройки подсветки на разных экранах.

	[http://xyne.archlinux.ca/projects/relight](http://xyne.archlinux.ca/projects/relight) || [relight](https://aur.archlinux.org/packages/relight/)

*   **calise** — Основное достоинство этой программы в том, что она очень точная, потребляет мало ресурсов и имеет демон-версию (.service файл для пользователей systemd также доступен). Она практически не влияет на время работы от батареи.

	[http://calise.sourceforge.net/mediawiki/index.php/Main_Page](http://calise.sourceforge.net/mediawiki/index.php/Main_Page) || [calise](https://aur.archlinux.org/packages/calise/)

*   **brightd** — brightd автоматически приглушает (но не переводит в режим ожидания) экран, если в течение какого-то времени пользователь не взаимодействует с ПК. Хорошее дополнение к [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") для того, чтобы экран не гас внезапно.

	[http://www.pberndt.com/Programme/Linux/brightd/](http://www.pberndt.com/Programme/Linux/brightd/) || [brightd](https://aur.archlinux.org/packages/brightd/)

*   **lux** — lux это совместимый с POSIX сценарий оболочки для управления яркостью на контролерах подсветки.

	[https://github.com/Ventto/lux](https://github.com/Ventto/lux) || [lux](https://aur.archlinux.org/packages/lux/)

*   **BacklightTooler** — BacklightTooler это инструмент управления подсветкой с автоматической настройкой яркости с использованием веб-камеры.

	[https://github.com/cotix/backlighttooler](https://github.com/cotix/backlighttooler) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

### setpci

Для настройки подсветки можно установить регистр видеокарты. Это означает, что вы настраиваете подсветку, напрямую манипулируя оборудованием, что может быть рискованным и, как правило, не является хорошей идеей. Этот метод поддерживается не всеми графическими картами.

Используя этот метод, вам сначала нужно использовать `lspci` чтобы найти ваш графический адаптер.

```
# setpci -s 00:02.0 F4.B=0

```

## Color correction

### xcalib

**Note:** *xcalib* does *not* change the backlight power, it just modifies the video LUT table: this means that your battery life will be unaffected by the change. Nevertheless, it could be useful when no backlight control is available (Desktop PCs). Use `xcalib -clear` to reset the LUT.

The package [xcalib](https://aur.archlinux.org/packages/xcalib/) ([upstream URL](http://xcalib.sourceforge.net/)) is available in the [AUR](/index.php/AUR "AUR") and can be used to dim the screen. A demonstration video is available on [YouTube](https://www.youtube.com/watch?v=A9xsvntT6i4). This program can correct gamma, invert colors, and reduce contrast, the latter of which we use in this case. For example, to dim down:

```
$ xcalib -co 40 -a

```

This program uses ICC technology to interact with X11 and while the screen is dimmed, you may find that the mouse cursor is just as bright as before.

### Xflux

Xflux is the [f.lux](http://justgetflux.com) port for the X-Windows system. It fluctuates your screen between blue during the day and yellow or orange at night. This helps you adapt to the time of day and stop staying up late because of your bright computer screen.

Various packages exist in the AUR that use *f.lux*.[[5]](https://aur.archlinux.org/packages/?O=0&K=xflux) The "main" package is [xflux](https://aur.archlinux.org/packages/xflux/) which handles the command line functionality of *f.lux*. Various daemons exist to handle the automatic startup of the xflux package.

### redshift

The program [redshift](/index.php/Redshift "Redshift") in the official repositories uses `randr` to adjust the screen brightness depending on the time of day and your geographic position. It can also do RGB gamma corrections and set color temperatures. As with `xcalib`, this is very much a software solution and the look of the mouse cursor is unaffected. To execute a single quick adjustment of the brightness, try something like this:

```
redshift -o -l 0:0 -b 0.8 -t 6500:6500

```

**Tip:** If your longitude is west or your latitude is south, you should input it as negative.

Example for Berkeley, CA:

```
redshift-gtk -l 37.8717:-122.2728 

```

### NVIDIA settings

Users of [NVIDIA's proprietary drivers](/index.php/NVIDIA "NVIDIA") users can change display brightness via the nvidia-settings utility under "X Server Color Correction." However, note that this has absolutely nothing to do with backlight (intensity), it merely adjusts the color output. (Reducing brightness this way is a power-inefficient last resort when all other options fail; increasing brightness spoils your color output completely, in a way similar to overexposed photos.)

### Increase brightness above maximum level

You can use [xrandr](/index.php/Xrandr "Xrandr") to increase brightness above its maximum level:

```
$ xrandr --output *output_name* --brightness 2

```

This will set the brightness level to 200%. It will cause higher power usage and sacrifice color quality for brightness, nevertheless it is particularly suited for situations where the ambient light is very bright (e.g. sunlight).

## Troubleshooting

### Backlight PWM modulation frequency (Intel i915 only)

Laptops with LED backlight are known to have screen flicker sometimes. This is because the most efficient way of controlling LED backlight brightness is by turning the LED's on and off very quickly varying the amount of time they are on.

However, the frequency of the switching, so-called PWM (pulse-width modulation) frequency, may not be high enough for the eye to perceive it as a single brightness and instead see flickering. This causes some people to have symptoms such as headaches and eyestrain.

If you have an Intel i915 GPU, then it may be possible to adjust PWM frequency to eliminate flicker.

Period of PWM (inverse to frequency) is stored in 4 higher bytes of `0xC8254` register (if you are using the Intel GM45 chipset use address `0x61254` instead). To manipulate registers values install [intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools) from the official repositories.

To increase the frequency, period must be reduced. For example:

 `# intel_reg read 0xC8254`  `0xC8254 : 0x12281228` 

Then to double PWM frequency divide 4 higher bytes by 2 and write back resulting value, keeping lower bytes unchanged:

```
# intel_reg write 0xC8254 0x09141228

```

You can use online calculator to calculate desired value [http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html](http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html)

To set new frequency automatically, consider writing an udev rule or install [intelpwm-udev](https://aur.archlinux.org/packages/intelpwm-udev/).

### Inverted Brightness (Intel i915 only)

Symptoms:

*   after installing `xf86-video-intel` systemd-backlight.service turns off the backlight during boot
    *   possible solution: mask systemd-backlight.service
*   switching from X to another VT turns the backlight off
*   the brightness keys are inverted (i.e. turning up the brightness makes the screen darker)

This problem may be solved by adding `i915.invert_brightness=1` to the list of [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### sysfs modified but no brightness change

**Note:** This behavior and their workarounds have been confirmed on the Dell M6700 with Nvidia K5000m (BIOS version prior to A10) and Clevo P750ZM (Eurocom P5 Pro Extreme) with Nvidia 980m.

On some systems, the brighness hotkeys on your keyboard correctly modify the values of the acpi interface in `/sys/class/backlight/acpi_video0/actual_brightness` but the brightness of the screen is not changed. Brigthness applets from [desktop environments](/index.php/Desktop_environments "Desktop environments") may also show changes to no effect.

If you have tested the recommended kernel parameters and only `xbacklight` works, then you may be facing an incompatibility between your BIOS and kernel driver.

In this case the only solution is to wait for a fix either from the BIOS or GPU driver manufacturer.

A workaround is to use the inotify kernel api to trigger `xbacklight` each time the value of `/sys/class/backlight/acpi_video0/actual_brightness` changes.

First [install](/index.php/Install "Install") [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools). Then create a script around inotify that will be launched upon each boot or through [autostart](/index.php/Autostart "Autostart").

 `/usr/local/bin/xbacklightmon` 
```
#!/bin/sh

path=/sys/class/backlight/acpi_video0

luminance() {
    read -r level < "$path"/actual_brightness
    factor=$((100 / max))
    printf '%d
' "$((level * factor))"
}

read -r max < "$path"/max_brightness

xbacklight -set "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    xbacklight -set "$(luminance)"
done

```