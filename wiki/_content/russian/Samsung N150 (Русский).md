Эта статья описывает установку и настройку 64х-битной версии Arch Linux на нетбук Samsung N150\. Согласно выводу dmidecode, эта статья также может быть полезной для моделей N210 и N220.

## Contents

*   [1 Обзор комплектующих](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80_.D0.BA.D0.BE.D0.BC.D0.BF.D0.BB.D0.B5.D0.BA.D1.82.D1.83.D1.8E.D1.89.D0.B8.D1.85)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Настройка устройств](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [3.1 Проводная сеть (Ethernet)](#.D0.9F.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.B0.D1.8F_.D1.81.D0.B5.D1.82.D1.8C_.28Ethernet.29)
    *   [3.2 Беспроводная сеть (Wi-Fi)](#.D0.91.D0.B5.D1.81.D0.BF.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.B0.D1.8F_.D1.81.D0.B5.D1.82.D1.8C_.28Wi-Fi.29)
        *   [3.2.1 Atheros AR9285](#Atheros_AR9285)
        *   [3.2.2 Realtek 8192E](#Realtek_8192E)
        *   [3.2.3 Broadcom BCM4313 (Samsung N150+)](#Broadcom_BCM4313_.28Samsung_N150.2B.29)
    *   [3.3 Графика](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.B0)
        *   [3.3.1 Подсветка](#.D0.9F.D0.BE.D0.B4.D1.81.D0.B2.D0.B5.D1.82.D0.BA.D0.B0)
    *   [3.4 Звук](#.D0.97.D0.B2.D1.83.D0.BA)
    *   [3.5 Ждущий режим (STR/S3)](#.D0.96.D0.B4.D1.83.D1.89.D0.B8.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.28STR.2FS3.29)
    *   [3.6 Спящий режим (hibernate)](#.D0.A1.D0.BF.D1.8F.D1.89.D0.B8.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.28hibernate.29)
    *   [3.7 Сенсорная панель (Тачпад)](#.D0.A1.D0.B5.D0.BD.D1.81.D0.BE.D1.80.D0.BD.D0.B0.D1.8F_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D1.8C_.28.D0.A2.D0.B0.D1.87.D0.BF.D0.B0.D0.B4.29)
    *   [3.8 Управление частотой процессора](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D0.BE.D0.B9_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.BE.D1.80.D0.B0)
*   [4 Клавиша Fn](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B0_Fn)
*   [5 Уменьшение времени загрузки](#.D0.A3.D0.BC.D0.B5.D0.BD.D1.8C.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)

# Обзор комплектующих

Нетбук Samsung N150 оснащается процессором [Intel Atom](https://en.wikipedia.org/wiki/Intel_Atom "wikipedia:Intel Atom") N450 ("Pineview") с интегрированной видеокартой [Intel GMA 3100 GPU](/index.php/Intel "Intel") и чипсетом с кодовым названием "Pine Trail". В отличие от ранних одноядерных процессоров Intel Atom серий N2xx and Z, N450 поддерживает набор инструкций x86_64\. Несмотря на то, что согласно информации DMI системная плата поддерживает до 8 Гб оперативной памяти, встроенный контроллер памяти Atom N450 может адресовать максимум 2 Гб.

Так как ввиду аппаратных ограничений для адресного пространства достаточно 32 бит, основное преимущество 64-битной версии Arch на данной модели заключается в удобстве использования пакетов AUR, собранных на более мощных 64-битных системах, принадлежащих тому же владельцу.

Поставляемые версии модели N150 (на начало марта 2010) включают "начальную" версию общеизвестной проприетарной ОС и поэтому содержат только 1 Гб памяти в виде одной планки DDR2 667Mhz SODIMM, которую можно заменить. Согласно информации DMI, нетбук содержит 2 mini PCIe слота, один из которых занят (встроенной?) беспроводной сетевой картой на базе чипа Atheros AR9285\. Другие версии этой модели могут комплектоваться (встроенным?) 3G адаптером, установленным в другой слот.

Внешние порты представляют собой 3 USB 2.0 порта, 1 VGA порт, 10/100 LAN порт (на чипе Marvell 88E8040 PCI-E), разъемы для наушников/микрофона и встроенный кардридер форматов SD/SDHC/MMC. Встроенная вебкамера с разрешением VGA (640x480) подсоединена к внутреннему USB контроллеру.

# Установка

Поскольку у нетбуков нет оптических приводов, предпочтительный способ установки - через USB флешку. В процессе первой загрузки установочного образа 2009.08, система перезагрузится после инициализации процессора. При последующих перезагрузках с тем же самым ядром подобное поведение не проявляется, тем не менее, возможна перезагрузка в процессе первой загрузки после смены/обновления ядра.

В этой статье предполагается, что для установки будет использоваться весь жесткий диск, затирая предустановленную производителем ОС и программы (включая разделы восстановления). Пока что не выяснено, какие именно разделы требуются для корректой работы программы восстановления: сохранения только первого раздела, неизвестного типа, **не** достаточно. Если вы желаете сохранить предустановленный механизм восстановления, вам следует создать набор из DVD-дисков, используя внешний DVD привод, перед установкой Arch Linux.

Во время первой установки, cfdisk будет вылетать с ошибкой из-за неправильной разметки на диске, выходящей за его границы (согласно геометрии по умолчанию для дисков в Linux). Решение - в запуске fdisk и создания новой, пустой таблицы разделов. **ВНИМАНИЕ: Эта операция уничтожит существующую таблицу разделов жесткого диска, с потерей всех данных, находящихся на нем.**

```
fdisk /dev/sda << EOF
o
w
EOF

```

После создания на диске пустой таблицы разделов, cfdisk в процессе установки будет работать правильно.

# Настройка устройств

## Проводная сеть (Ethernet)

Адаптер на чипе Marvell 88E8040 работает "из коробки" с ядром с конфигурацией "по умолчанию". При установке [networkmanager](https://www.archlinux.org/packages/?name=networkmanager), процесс загрузки может быть ускорен задержкой инициализации сети до появления графического интерфейса.

## Беспроводная сеть (Wi-Fi)

Samsung N150 поставляется с беспроводными картами на двух различных чипах: Atheros AR9285 и Realtek 8192E.

Примечание: Модель Samsung N150+ может комплектоваться беспроводной картой на чипе Broadcom BCM4313.

### Atheros AR9285

Беспроводной адаптер на этом чипе работает "из коробки", включая полную поддержку шифрования WPA2-PSK через NetworkManager. Мощность передатчика может быть изменена при установке пакета [rfkill](https://www.archlinux.org/packages/?name=rfkill), с помощью следующего скрипта, помещенного, к примеру, в /usr/local/sbin/rftoggle

```
#!/bin/bash

blocked=`rfkill list wlan | grep "Soft blocked: yes"`

if [ -z "$blocked" ]; then
   rfkill block wlan
else
   rfkill unblock wlan
fi

```

### Realtek 8192E

Драйвер для RTL8192E есть в ядре Arch'а, но для драйвера необходима прошивка. Ее можно взять в пакете [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) или собрать самостоятельно из AUR'a. Смотри также [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Broadcom BCM4313 (Samsung N150+)

Samsung N150-Plus имеет встроенный адаптер BCM4313 с блютузом. С ядром новее v2.6.37 работает из коробки. Спасибо открытому драйверу brcm80211\. Модуля для этой карты в старом ядре нет, и поэтому необходимо установить сторонний драйвер. Его можно найти в AUR'e: [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) Или, если вы хотите собрать его вручную: [http://www.broadcom.com/support/802.11/linux_sta.php](http://www.broadcom.com/support/802.11/linux_sta.php) Этот драйвер работает по большей части работает хорошо, за исключением того, что не может подключаться в "скрытым" сетям.

За более подробной информацией обратитесь к этой статье: [Broadcom wireless](https://wiki.archlinux.org/index.php/Broadcom_wireless#Wi-Fi_card_does_not_work_or_show_up_since_kernel_upgrade_.28brcmsmac.29)

## Графика

Встроенная в Atom N450 графика на базе [Intel GMA 3100 GPU](/index.php/Intel "Intel"), работает с [Kernel Mode Setting](/index.php/KMS "KMS") без дополнительных плясок с бубном. Ранняя инициализация KMS, похоже, незначительно ускоряет скорость загрузки и может быть включена добавлением следующей строки в /etc/mkinitcpio.conf (если подобная строчка уже существует, просто добавьте нужные модули в нее):

```
MODULES="**intel_agp i915**"

```

Запустите `mkinitcpio -p linux`, чтобы новые модули добавились в загрузочный образ.

В отличие от более ранней модели [N140](/index.php/Samsung_N140 "Samsung N140"), у модели N150 не замечено проблем с режимом энергосбережения дисплея.

Для модели Samsung 150 Plus может потребоватся утилита 915resolution. Но версия из AUR не сработает с сообщением об ошибке: `Intel chipset detected. However, 915resolution was unable to determine the chipset type. Chipset Id: a0108086`

Существует пропатченая версия для этого чипа.

Включив однажды доп. клавиши (смотри ниже), комбинация Fn+F4 будет переключать вывод изображения между только встроенным экраном, расширенным режимом и режимом дублирования изображения (clone) автоматически, когда внешний монитор подключен к VGA порту.

### Подсветка

Так же как и на других ноутбуках и нетбуках Samsung, прямое управление подсветкой через ACPI в данной модели невозможно. Вместо этого, управление подсветкой может осуществляться изменением настроек графического адаптера через PCI шину с помощью следующего скрипта. Для легкости использования дополнительных кнопок (с Fn), поместите этот скрипт в /usr/local/sbin/backlight

```
#!/bin/bash
# increase/decrease/set brightness (range 0-255)

# PCI device on which to operate
DEVICE=00:02.0

# Amount to raise/lower the backlight when called with "up" or "down"
AMOUNT=8

# Minimum backlight value reachable via "down"
MIN=1

# Default backlight level when toggling on
DEFAULT=64

#get current brightness in hex and convert to decimal
var1=`setpci -s $DEVICE F4.B`
var1d=$((0x$var1))
case "$1" in
       up)
           # вычислить новую яркость
           var2=`echo "ibase=10; obase=16; a=($var1d+$AMOUNT); if (a<255) print a else print 255" | bc`
           echo "$0: яркость увеличена с 0x$var1 до 0x$var2"
           setpci -s $DEVICE F4.B=$var2
           ;;
       down)
           #calculate new brightness
           var2=`echo "ibase=10; obase=16; a=($var1d-$AMOUNT);if (a>$MIN) print a else print $MIN" | bc`
           echo "$0: яркость уменьшена с 0x$var1 до 0x$var2"
           setpci -s $DEVICE F4.B=$var2
           ;;
       set)
           # "set" позволяет выставить яркость в 0, т.е. выключить подсветку
           echo "$0: установка яркости в 0x$2"
           setpci -s $DEVICE F4.B=$2
           ;;
       toggle)
           if [ $var1d -eq 0 ] ; then
               echo "повышение яркости"
               setpci -s $DEVICE F4.B=$DEFAULT
           else
               echo "уменьшение яркости"
               setpci -s $DEVICE F4.B=0
           fi
           ;;
       *)
           echo "использование: $0 {up|down|set <val>|toggle}"
           echo "$0: текущая яркость - 0x$var1"
           ;;
esac
exit 0

```

## Звук

Звук на базе Intel HD Audio в этой модели работает "из коробки", разве что нужно увеличить громкость канала "speaker". Установите пакет [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), чтобы получить скрипт, сохраняющий и восстанавливающий уровни громкости во время загрузки (Не забудьте добавить пункт "alsa" в массив DAEMONS в файле /etc/rc.conf).

Для владельцев модели N210, чтобы включить встроенный микрофон, вам нужно выполнить следующие команды:

```
# echo 0x19 0x90A70011 > /sys/class/sound/hwC0D0/user_pin_configs
# echo 1 > /sys/class/sound/hwC0D0/reconfig

```

## Ждущий режим (STR/S3)

В среде Gnome 2.28 и при установленном пакете [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager), ждущий режим работает без дополнительного вмешательства при закрытии крышки нетбука. Процесс приостановки работы занимает до 30 секунд. Выход из ждущего режима в конфигурации по умолчанию требует нажатия кнопки включения нетбука. Пробуждение из спячки при открытии крышки или нажатия кнопок на клавиатуре можно включить настройкой в BIOS'е.

При наличии беспроводной сетевой карты на чипе realtek, сеть не всегда восстанавливается при выходе из ждущего режима. Выгрузка и последующая загрузка модуля r8192e_pci решают эту проблему. Также, это может быть автоматически настроено при помощи пакета [Pm-utils](/index.php/Pm-utils "Pm-utils").

## Спящий режим (hibernate)

Спящий режим с использованием [pm-utils](/index.php/Pm-utils "Pm-utils") все еще не работает корректно. В процессе запуска из спящего режима появляются ошибки заголовков ELF, связанные с glibc, успешно предотвращающие запуск новых программ (включая /sbin/shutdown). Более того, даже если эта проблема будет устранена, процесс восстановления из раздела подкачки занимает немного больше времени, чем "холодный" запуск системы.

С ядром 2.6.36, на некоторых моделях N-серии необходимо добавить intel_idle.max_cstate=0 к параметрам загрузки ядра для корректной работы ждущего/спящего режимов.

## Сенсорная панель (Тачпад)

Тачпад Synaptics работает для однопальцевых операций и прокрутки с помощью его правого края без дополнительной настройки. При нажатии Fn+F10 BIOS автоматически включает или выключает тачпад. Чтобы отображать сообщение об этом, необходимо установить пакет [xosd](https://www.archlinux.org/packages/?name=xosd) и настроить скрипт, выводящий сообщение при нажатии Fn+F10 (смотри далее о настройке доп. клавиш). Поместите этот скрипт в /usr/local/bin/report_touchpad

```
#!/bin/bash

FONT='-adobe-helvetica-bold-*-*-*-34-*-*-*-*-*-*-*'
DELAY=1
state=Unknown

case "$1" in
   on)
      state="включен"
      ;;
   off)
      state="отключен"
      ;;
   *)
      echo "Использование: $0 {on|off}"
      exit 2
      ;;
esac

osd_cat -A center -p middle -f $FONT -d $DELAY << EOF
Тачпад $state
EOF

exit 0

```

Чтобы тачпад понимал нажатия на него, самым простым решением будет установить пакеты [gsynaptics](https://www.archlinux.org/packages/?name=gsynaptics) или [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings). Хотя согласно документам поставляемым с нетбуком, заявлена поддержка мультитача (для двухпальцевых нажатий, прокрутки двумя пальцами и т.д.), не похоже, что это работает правильно.

Для владельцев модели N220 (не тестировалось на N150, но возможно будет работать), эти параметры для включают мультитач на тачпаде (файл /etc/hal/fdi/policy/11-x11-synaptics.fdi)

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<deviceinfo version="0.2">
  <device>
    <match key="info.capabilities" contains="input.touchpad">
      <merge key="input.x11_driver" type="string">synaptics</merge>
      <merge key="input.x11_options.TapButton1" type="string">1</merge>
      <merge key="input.x11_options.TapButton2" type="string">2</merge>
      <merge key="input.x11_options.TapButton3" type="string">3</merge>
      <merge key="input.x11_options.SHMConfig" type="string">true</merge>
      <merge key="input.x11_options.VertEdgeScroll" type="string">false</merge>
      <merge key="input.x11_options.PalmDetect" type="string">false</merge>
      <merge key="input.x11_options.VerteScrollDelta" type="string">100</merge>
      <merge key="input.x11_options.VertTwoFingerScroll" type="string">true</merge>
      <merge key="input.x11_options.HorizTwoFingerScroll" type="string">true</merge>
      <merge key="input.x11_options.EmulateTwoFingerMinZ" type="string">40</merge>
      <merge key="input.x11_options.EmulateTwoFingerMinW" type="string">5</merge>
    </match>
  </device>
</deviceinfo>

```

## Управление частотой процессора

Чтобы включить управление частотой процессора, вам необходимо добавить несколько модулей ядра в автозагрузку в файле /etc/rc.conf:

```
MODULES=(acpi-cpufreq cpufreq-ondemand cpufreq-powersave)

```

Смена режимов использования процессора ядром между производительным (performance), автоматическим (ondemand) и энергосберегающим (powersave) может производиться с помощью следующего скрипта, установленного в /usr/local/sbin/cpufreq_toggle

```
#!/bin/bash

current=`cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor`
future=unknown

if [ "$current" == "performance" ]; then
   future="ondemand"
elif [ "$current" == "ondemand" ]; then
   future="powersave"
else
   future="performance"
fi

echo "$future" > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
echo "$future" > /sys/devices/system/cpu/cpu1/cpufreq/scaling_governor

echo "$future"

```

Для вывода сообщения о текущем режиме через сообщение на дисплее (полезно при назначении комбинации Fn+F8 на смену режимов), следующий скрипт должен быть установлен в /usr/local/bin/cpufreq_toggle_osd

```
#!/bin/bash

FONT='-adobe-helvetica-bold-*-*-*-34-*-*-*-*-*-*-*'
DELAY=1

state=`sudo /usr/local/sbin/cpufreq_toggle`
message="CPU Performance State Unknown"

if [ "$state" == "performance" ]; then
   message="Режим производительности"
elif [ "$state" == "powersave" ]; then
   message="Режим энергосбережения"
elif [ "$state" == "ondemand" ]; then
   message="Автоматический режим"
fi

osd_cat -A center -p middle -f $FONT -d $DELAY << EOF
$message
EOF

exit 0

```

По умолчанию, система будет загружена с режимом "производительность". Чтобы включать автоматический режим в конце загрузки, добавьте следующие строки в /etc/rc.local

```
echo "ondemand" > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
echo "ondemand" > /sys/devices/system/cpu/cpu1/cpufreq/scaling_governor

```

# Клавиша Fn

Некоторые из спец. комбинаций клавиш в модели N150 работают сразу, но большинство - нет. Нестандартные сканкоды с клавиатуры передаются ядру, которое не знает, как преобразовать их в стандартные сканкоды. Что еще хуже, большинство сканкодов сообщают только о нажатии клавиши, но не о ее отпускании. Добавление следующие строчки в /etc/rc.local задействует все спец. клавиши и назначит им правильные сканкоды:

```
setkeycodes e002 227   # Fn+F4 maps to switchvidmode
setkeycodes e003 236   # Fn+F2 maps to battery
setkeycodes e004 148   # Fn+F5 maps to prog1
setkeycodes e006 238   # Fn+F9 maps to wlan
setkeycodes e008 225   # Fn+Up maps to brightnessup
setkeycodes e009 224   # Fn+Dn maps to brightnessdown
setkeycodes e031 149   # Fn+F7 maps to prog2
setkeycodes e033 202   # Fn+F8 maps to prog3
setkeycodes e077 191   # Fn+F10 maps to F21 whenever the touchpad is enabled
setkeycodes e079 192   # Fn+F10 maps to F22 whenever the touchpad is disabled

# Ensure key release events occur for all except Fn+F7, which properly reports a key release for some reason
echo 130,131,132,134,136,137,179,247,249 > /sys/devices/platform/i8042/serio0/force_release

```

To enable hotkeys to change backlight, wireless, and system performance settings, it is necessary to give regular users certain permissions via the [sudo](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)") command. Run visudo as root and add the following to the Cmnd alias specifications:

```
Cmnd_Alias NETBOOK_CMDS = /usr/local/sbin/backlight, /usr/local/sbin/rftoggle, /usr/local/sbin/cpufreq_toggle

```

Затем добавьте следующую строку в конец файла:

```
%users ALL=(ALL) NOPASSWD: NETBOOK_CMDS

```

Теперь нестандартные сочетания клавиш могут быть добавлены в ДЕ посредством окна "Комбинации клавиш клавиатуры".

| Назначение | Команда | Сочетание клавиш |
| Выключить тачпад | /usr/local/bin/report_touchpad off | Нажмите Fn+F10, когда тачпад включен. |
| Включить тачпад | /usr/local/bin/report_touchpad on | Нажмите Fn+F10, когда тачпад выключен. |
| Изменение частоты процессора | /usr/local/bin/cpufreq_toggle_osd | Fn+F8 |
| Увеличить яркость подсветки | sudo /usr/local/sbin/backlight up | Fn+<ВВЕРХ> |
| Уменьшить яркость подсветки | sudo /usr/local/sbin/backlight down | Fn+<ВНИЗ> |
| Вкл/Выкл wi-fi | sudo /usr/local/sbin/rftoggle | Fn+F9 |
| Вкл/Выкл подсветку экрана | sudo /usr/local/sbin/backlight toggle | Fn+F5 |

# Уменьшение времени загрузки

Чтобы заставить нетбук загружаться максимально быстро, нам нужно уменьшить задержки и заставить демонов запускаться в фоне. Две полезные модификации загрузчика (в данном случае - grub): измените параметр "timeout" на 2 секунды, вместо 5и - по умолчанию и добавьте параметр "quiet", чтобы подавить вывод некоторых сообщений ядра (которые отнимают время). Указанные параметры можно поменять в файле /boot/grub/menu.lst

```
timeout    2
...
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz26 root=/dev/sda3 ro quiet
initrd /kernel26.img

```

Учтите, что может быть здравой идеей **не** добавлять параметр "quiet" ко второму пункту загрузчика (который используется при сбоях ядра из первого пункта), в этом случае вывод сообщений ядра поможет вам определить проблему. Впрочем, вы можете отредактировать эти параметры непосредственно при загрузке (нажать "e" на нужном пункте меню загрузчика).

Заставить демонов грузиться в фоне немного сложнее, учитывая, что один демон может зависить от одного или нескольких других. Тем не менее, можно использовать преимущество известных "задержек" в процессе загрузки (напр. запуск подсистемы X11), что позволяет некоторым демонам (таких как NetworkManager) спокойно запускаться в фоне, перед тем как они действительно понадобятся.

```
DAEMONS=(syslog-ng !network hal @networkmanager @sensors @alsa !netfs @crond)

```

С вышеуказанными настройками, графический менеджер входа в систему появляется через 37-38 секунд после "холодной" загрузки (включая задержки BIOS'а и grub'а)