Контролировать яркость экрана бывает непросто. На многих компьютерах нет физического переключателя, а вместо него используются программные решения, которые не всегда работают как положено. Однако, чаще всего это возможно. Найдите работающий способ для вашего оборудования. Слишком яркие экраны могут привести к потере зрения!

Существует много способов регулировать яркость подсветки монитора, экрана ноутбука или встроенной экранной панели (как в iMac) с помощью программного обеспечения, но в зависимости от оборудования и модели иногда доступны не все варианты. В данной статье предпринимается попытка обобщить все возможные пути регулирования яркости подсветки экрана.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Обзор](#Обзор)
*   [2 ACPI](#ACPI)
    *   [2.1 Параметры ядра](#Параметры_ядра)
    *   [2.2 Правило Udev](#Правило_Udev)
*   [3 Выключение подсветки](#Выключение_подсветки)
*   [4 Служба systemd-backlight](#Служба_systemd-backlight)
*   [5 Утилиты настройки](#Утилиты_настройки)
    *   [5.1 xbacklight](#xbacklight)
    *   [5.2 Другие утилиты](#Другие_утилиты)
    *   [5.3 setpci](#setpci)
    *   [5.4 Использование DBus с Gnome](#Использование_DBus_с_Gnome)
*   [6 Цветовая коррекция](#Цветовая_коррекция)
    *   [6.1 xcalib](#xcalib)
    *   [6.2 Xflux](#Xflux)
    *   [6.3 redshift](#redshift)
    *   [6.4 NVIDIA settings](#NVIDIA_settings)
    *   [6.5 Увеличение яркости выше максимального уровня](#Увеличение_яркости_выше_максимального_уровня)
*   [7 Внешние мониторы](#Внешние_мониторы)
*   [8 Решение проблем](#Решение_проблем)
    *   [8.1 Частота ШИМ-модуляции подсветки (только для Intel i915)](#Частота_ШИМ-модуляции_подсветки_(только_для_Intel_i915))
    *   [8.2 Инвертированная яркость (только для Intel i915)](#Инвертированная_яркость_(только_для_Intel_i915))
    *   [8.3 sysfs изменен, но нет изменения яркости](#sysfs_изменен,_но_нет_изменения_яркости)

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

Яркость может быть изменена, если записать число в `brightness`. Здесь невозможно использовать число выше максимальной яркости.

```
# tee /sys/class/backlight/acpi_video0/brightness <<< 5

```

### Параметры ядра

Иногда ACPI не работает должным образом из-за различных реализаций материнских плат и особенностей ACPI, что может приводить, например, к неточным оповещениям о яркости. Этому могут быть подвержены некоторые ноутбуки с двойной графикой (например, выделенный графический процессор Nvidia / Radeon с интегрированным графическим процессором Intel / AMD). Кроме того, иногда может быть необходимо зарегистрировать свою собственную подсветку `acpi_video0`, даже если другая уже существует (например, `intel_backlight`), что может быть достигнуто добавлением следующих [параметров ядра](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_backlight=video
acpi_backlight=vendor
acpi_backlight=native

```

Если вы обнаружите, что изменение подсветки `acpi_video0` на самом деле не изменяет яркость, вам может потребоваться использовать `acpi_backlight=none`.

**Совет:**

*   На ноутбуках Nvidia Optimus параметра ядра nomodeset может препятствовать регулировке подсветки.
*   На ноутбуках Asus вам может также понадобиться загрузить [модуль ядра](/index.php/Kernel_module "Kernel module") `asus-nb-wmi`.
*   Отключение legacy-загрузки на Dell XPS13 приводит к невозможности изменить подсветку.

### Правило Udev

Если доступен интерфейс ACPI, уровень подсветки может быть установлен во время загрузки с использованием правила [udev](/index.php/Udev "Udev"):

 `/etc/udev/rules.d/81-backlight.rules` 
```
# Установить уровень подсветки равным 8
SUBSYSTEM=="backlight", ACTION=="add", KERNEL=="acpi_video0", ATTR{brightness}="8"
```

**Примечание:** Служба systemd-backlight восстанавливает предыдущий уровень яркости подсветки во время загрузки. Чтобы предотвратить конфликты для указанных выше правил, см. [#Служба systemd-backlight](#Служба_systemd-backlight).

**Совет:** Чтобы настроить подсветку в зависимости от состояния питания, см. [Power management#Using a script and an udev rule](/index.php/Power_management#Using_a_script_and_an_udev_rule "Power management") и используйте выбранную вами [утилиту](#Утилиты_настройки) в скрипте.

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
*   xbacklight в настоящий момент не работает с modesetting-драйвером [[3]](https://gitlab.freedesktop.org/xorg/xserver/issues/47).

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

*   **brightnessctl** — Легковесный инструмент контроля яркости (совместимый с Wayland).

	[https://github.com/Hummer12007/brightnessctl](https://github.com/Hummer12007/brightnessctl) || [brightnessctl](https://www.archlinux.org/packages/?name=brightnessctl)

*   **light** — Light последователь *LightScript*.

	[https://github.com/haikarainen/light](https://github.com/haikarainen/light) || [light](https://www.archlinux.org/packages/?name=light)

*   **acpilight** — acpilight содержит "xbacklight"-совместимую утилиту, которая использует sys файловую систему для установки яркости экрана. Т.к. она не использует X вообще, ее также можно использовать в консоли и с Wayland. Она не имеет проблем с KMS драйверами. Кроме того, на ноутбуках ThinkPad можно также настраивать подсветку клавиатуры.

	[https://github.com/wavexx/acpilight/](https://github.com/wavexx/acpilight/) || [acpilight](https://www.archlinux.org/packages/?name=acpilight)

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

*   **Clight** — Вдохновленная calise, но с множеством новых функций и написанная на Си. Её первоначальной целью было превратить веб-камеру в датчик освещенности: она будет регулировать подсветку экрана на основе яркости окружающего пространства.

	[https://github.com/FedeDP/Clight](https://github.com/FedeDP/Clight) || [clight-git](https://aur.archlinux.org/packages/clight-git/)

### setpci

Для настройки подсветки можно установить регистр видеокарты. Это означает, что вы настраиваете подсветку, напрямую манипулируя оборудованием, что может быть рискованным и, как правило, не является хорошей идеей. Этот метод поддерживается не всеми графическими картами.

Используя этот метод, вам сначала нужно использовать `lspci` чтобы найти ваш графический адаптер.

```
# setpci -s 00:02.0 F4.B=0

```

### Использование DBus с Gnome

Яркость также можно регулировать с помощью настроек gnome. При использовании этого метода изменения отражаются в интерфейсе gnome.

```
gdbus call --session --dest org.gnome.SettingsDaemon.Power --object-path /org/gnome/SettingsDaemon/Power --method org.freedesktop.DBus.Properties.Set org.gnome.SettingsDaemon.Power.Screen Brightness "<int32 50>"

```

Пошаговое изменение яркости (для контроля с клавиатуры) также может быть реализовано этим методом.

```
gdbus call --session --dest org.gnome.SettingsDaemon.Power --object-path /org/gnome/SettingsDaemon/Power --method org.gnome.SettingsDaemon.Power.Screen.StepUp
gdbus call --session --dest org.gnome.SettingsDaemon.Power --object-path /org/gnome/SettingsDaemon/Power --method org.gnome.SettingsDaemon.Power.Screen.StepDown

```

## Цветовая коррекция

### xcalib

**Примечание:** *xcalib не меняет* силу подсветки, а просто модифицирует LUT-таблицу: это означает, что время работы от батареи не изменится. Однако, это может быть полезно, когда регулировка подсветки недоступна (настольные ПК). Используйте `xcalib -clear`, чтобы сбросить LUT.

Пакет [xcalib](https://aur.archlinux.org/packages/xcalib/) ([upstream URL](http://xcalib.sourceforge.net/)) доступен в [AUR](/index.php/AUR "AUR") и может использоваться, чтобы уменьшить яркость экрана. Видео-демонстрация доступна на [YouTube](https://www.youtube.com/watch?v=A9xsvntT6i4). Эта программа может корректировать гамму, инвертировать цвета и уменьшать контраст. Например, чтобы уменьшить яркость посредством изменения контраста:

```
$ xcalib -co 40 -a

```

Эта программа использует технологию ICC для взаимодействия с X11, и пока экран затенен, вы можете обнаружить, что курсор мыши так же ярок, как и раньше.

### Xflux

Xflux это порт [f.lux](http://justgetflux.com) для системы X-Windows. Он меняет оттенок экрана между синим в течение дня и желтым или оранжевым ночью. Это помогает вам адаптироваться к времени суток и перестать поздно ложиться спать из-за вашего яркого монитора.

В AUR существуют различные пакеты, которые используют *f.lux*.[[5]](https://aur.archlinux.org/packages/?O=0&K=xflux) "Основной" пакет - [xflux](https://aur.archlinux.org/packages/xflux/), который охватывает функционал командной строки *f.lux*. Существуют различные демоны для автоматического запуска пакета xflux.

### redshift

[Redshift](/index.php/Redshift "Redshift") использует `randr`, чтобы настроить яркость экрана в зависимости от времени суток и вашего географического положения. Она также может выполнять RGB гамма-коррекцию и задавать цветовые температуры. Как и `xcalib`, это лишь программное решение, и внешний вид курсора мыши не изменяется. Чтобы выполнить быструю настройку яркости, попробуйте что-то вроде этого:

```
redshift -o -l 0:0 -b 0.8 -t 6500:6500

```

**Совет:** Если ваша долгота западная или широта южная, вы должны ввести ее как отрицательную. Пример для Berkeley, CA:
```
redshift-gtk -l 37.8717:-122.2728 

```

### NVIDIA settings

Пользователи [несвободных драйверов NVIDIA](/index.php/NVIDIA "NVIDIA") могут менять яркость дисплея с помощью утилиты nvidia-settings в разделе "X Server Color Correction". Однако, заметьте, что это не имеет ничего общего с подсветкой (Интенсивность), она всего лишь регулирует цветность. (Уменьшение яркости таким образом не является энергоэффективным. Используйте его в последнюю очередь, если все другие варианты не срабатывают; увеличение яркости портит цвета на экране полностью, по аналогии с засвеченностью фотографий.)

### Увеличение яркости выше максимального уровня

Вы можете испльзовать [xrandr](/index.php/Xrandr "Xrandr") для увеличения яркости выше максимального уровня:

```
$ xrandr --output *output_name* --brightness 2

```

Это установит уровень яркости на 200%. Это приведёт к повышению энергопотребления и снижению качества цвета в пользу яркости, тем не менее оно особенно подходит для ситуаций, когда окружающий свет очень яркий (например, солнечный свет).

## Внешние мониторы

DDC/CI (Командный интерфейс обмена данными между компьютером и монитором) может использоваться для связи с внешними мониторами, реализующими стандарт MCCS (Monitor Control Command Set) по шине I2C.

DDC может контролировать яркость, контрастность, входы и т.д. на поддерживаемых мониторах. Настройки, доступные с панели OSD (экранное меню), также могут управляться через DDC.

Утилита [ddcutil](http://www.ddcutil.com/) может использоваться, чтобы вывести или поменять настройки яркости:

 `# ddcutil capabilities | grep Brightness` 
```
  Feature: 10 (Brightness)

```
 `# ddcutil getvcp 10`  `VCP code 0x10 (Brightness                    ): current value =    60, max value =   100` 
```
# ddcutil setvcp 10 70

```

## Решение проблем

### Частота ШИМ-модуляции подсветки (только для Intel i915)

Известно, что на ноутбуках со светодиодной подсветкой иногда мерцает экран. Это объясняется тем, что наиболее эффективным способом управления яркостью подсветки светодиодов является быстрое включение и выключение светодиодов, изменяя время их свечения.

Однако, частота переключения, так называемая частота ШИМ (широтно-импульсная модуляция), может быть недостаточно высокой, чтобы глаз воспринимал её как непрерывное свечение, и вместо этого видно мерцание. Это вызывает у некоторых людей такие симптомы, как головные боли и усталость глаз.

Если у вас графический адаптер Intel i915, то возможно настроить частоту ШИМ, чтобы устранить мерцание.

Период ШИМ (обратно пропорциональный частоте) записывается в 4 старших байта регистра `0xC8254` (если вы используете чипсет Intel GM45, вместо этого используйте адрес `0x61254`). Чтобы манипулировать значениями регистров, установите [intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools) из официальных репозиториев.

Чтобы увеличить частоту, период должен быть уменьшен. Например:

 `# intel_reg read 0xC8254`  `0xC8254 : 0x12281228` 

Затем, чтобы удвоить частоту ШИМ, разделите 4 старших байта на 2 и запишите полученное значение, сохраняя нижние байты неизменными:

```
# intel_reg write 0xC8254 0x09141228

```

Вы можете использовать онлайн-калькулятор для расчета желаемого значения [http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html](http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html)

Чтобы установить новую частоту автоматически, попробуйте написать правило udev или установить [intelpwm-udev](https://aur.archlinux.org/packages/intelpwm-udev/).

### Инвертированная яркость (только для Intel i915)

Симптомы:

*   после установки `xf86-video-intel` systemd-backlight.service выключает подсветку во время загрузки
    *   возможное решение: маскировать systemd-backlight.service
*   переключение с X на другую виртуальную консоль выключает подсветку
*   кнопки регулировки подсветки инвертированы (например, увеличение яркости делает экран темнее)

Эта проблема может быть решена добавлением `i915.invert_brightness=1` в список [параметров ядра](/index.php/Kernel_parameters "Kernel parameters").

### sysfs изменен, но нет изменения яркости

**Примечание:** Такое поведение и способы его обхода были подтверждены на Dell M6700 с Nvidia K5000m (версия BIOS до A10) и Clevo P750ZM (Eurocom P5 Pro Extreme) с Nvidia 980m.

На некоторых системах горячие клавиши яркости на клавиатуре корректно изменяют значения интерфейса acpi в `/sys/class/backlight/acpi_video0/actual_brightness`, но яркость экрана не изменяется. Апплеты яркости в [окружениях рабочего стола](/index.php/Desktop_environments "Desktop environments") могут также показывать изменения без результатов.

Если вы протестировали рекомендуемые параметры ядра и только `xbacklight` работает, вы можете столкнуться с несовместимостью между вашим BIOS и драйвером ядра.

В этом случае единственное решение - дождаться исправления от производителя BIOS или драйвера GPU.

Обходной путь - использовать inotify api ядра для запуска `xbacklight` каждый раз, когда изменяется значение `/sys/class/backlight/acpi_video0/actual_brightness`.

Сперва [установите](/index.php/Install "Install") [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools). Затем создайте скрипт, который будет запускаться при каждом включении с помощью [автозагрузки](/index.php/Autostart "Autostart").

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