[lm_sensors](http://lm-sensors.org/) (Linux-monitoring sensors) - свободное ПО, состоящее из драйверов и утилит, позволяющее отслеживать температуру, напряжение, скорость вращения вентиляторов в вашей системе. Следует помнить, что набор датчиков индивидуален для каждой системы, поэтому некоторые возможности могут быть недоступны. 

## Contents

*   [1 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [1.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.3 Просмотр датчиков](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.B4.D0.B0.D1.82.D1.87.D0.B8.D0.BA.D0.BE.D0.B2)
    *   [1.4 Считывание SPD-значений из памяти модулей (опционально)](#.D0.A1.D1.87.D0.B8.D1.82.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_SPD-.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B8.D0.B7_.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.28.D0.BE.D0.BF.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.29)
*   [2 Использование данных датчиков](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.B4.D0.B0.D1.82.D1.87.D0.B8.D0.BA.D0.BE.D0.B2)
    *   [2.1 Графические фронтэнды](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D1.84.D1.80.D0.BE.D0.BD.D1.82.D1.8D.D0.BD.D0.B4.D1.8B)
    *   [2.2 sensord](#sensord)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Регулировка значений](#.D0.A0.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9)
        *   [3.1.1 Пример 1\. Регулировка температурных смещений](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_1._.D0.A0.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D1.82.D0.B5.D0.BC.D0.BF.D0.B5.D1.80.D0.B0.D1.82.D1.83.D1.80.D0.BD.D1.8B.D1.85_.D1.81.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B9)
        *   [3.1.2 Пример 2\. Переименование параметров](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_2._.D0.9F.D0.B5.D1.80.D0.B5.D0.B8.D0.BC.D0.B5.D0.BD.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2)
        *   [3.1.3 Пример 3\. Изменение нумерации ядер для многопроцессорных систем](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_3._.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D1.83.D0.BC.D0.B5.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D1.8F.D0.B4.D0.B5.D1.80_.D0.B4.D0.BB.D1.8F_.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.BE.D1.80.D0.BD.D1.8B.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC)
    *   [3.2 Автоматизация развертывания lm_sensors](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.80.D0.B0.D0.B7.D0.B2.D0.B5.D1.80.D1.82.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_lm_sensors)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Модуль K10Temp](#.D0.9C.D0.BE.D0.B4.D1.83.D0.BB.D1.8C_K10Temp)
    *   [4.2 Датчики не работают с Linux 2.6.31](#.D0.94.D0.B0.D1.82.D1.87.D0.B8.D0.BA.D0.B8_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82_.D1.81_Linux_2.6.31)
    *   [4.3 Gigabyte GA-J1900N-D3V](#Gigabyte_GA-J1900N-D3V)
    *   [4.4 Laptop Screen issues after running sensors-detect](#Laptop_Screen_issues_after_running_sensors-detect)

## Использование

### Установка

Установите пакет [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### Настройка

Используйте **sensors-detect** для обнаружения и формирования списка модулей ядра:

```
sensors-detect

```

**Важно:** Если вы не уверены,то не выбирайте значения, отличные от предложенных (просто жмите `Enter`). Смотрите [#Laptop_Screen_issues_after_running_sensors-detect](#Laptop_Screen_issues_after_running_sensors-detect).

В результате будет создан конфигурационный файл `/etc/conf.d/lm_sensors`, используемый демоном `sensors`, который автоматически активируется ядром при загрузке. Программа будет задавать вопросы по различному железу. "Безопасные" ответы предусмотрены по умолчанию, так что слепое нажатие `Enter` на все вопросы не должно вызвать никаких проблем.

По окончанию определения датчиков будут доступны снимаемые ими значения.

Пример:

 `# sensors-detect` 
```
This program will help you determine which kernel modules you need
to load to use lm_sensors most effectively. It is generally safe
and recommended to accept the default answers to all questions,
unless you know what you're doing.

Some south bridges, CPUs or memory controllers contain embedded sensors.
Do you want to scan for them? This is totally safe. (YES/no): 
Module cpuid loaded successfully.
Silicon Integrated Systems SIS5595...                       No
VIA VT82C686 Integrated Sensors...                          No
VIA VT8231 Integrated Sensors...                            No
AMD K8 thermal sensors...                                   No
AMD Family 10h thermal sensors...                           No

...

Now follows a summary of the probes I have just done.
Just press ENTER to continue: 

Driver `coretemp':
  * Chip `Intel digital thermal sensor' (confidence: 9)

Driver `lm90':
  * Bus `SMBus nForce2 adapter at 4d00'
    Busdriver `i2c_nforce2', I2C address 0x4c
    Chip `Winbond W83L771AWG/ASG' (confidence: 6)

Do you want to overwrite /etc/conf.d/lm_sensors? (YES/no): 
ln -s '/usr/lib/systemd/system/lm_sensors.service' '/etc/systemd/system/multi-user.target.wants/lm_sensors.service'
Unloading i2c-dev... OK
Unloading cpuid... OK

```

**Обратите внимание:** Служба systemd добавится автоматически после того, как будет послан ответ **YES** на предложение создать `/etc/conf.d/lm_sensors`. Так же отвечая положительно эта служба будет незамедлительно запущена.

### Просмотр датчиков

Пример запуска `sensors`:

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +58.0°C  (high = +84.0°C, crit = +100.0°C)
Core 1:       +59.0°C  (high = +84.0°C, crit = +100.0°C)
Core 2:       +59.0°C  (high = +84.0°C, crit = +100.0°C)
Core 3:       +60.0°C  (high = +84.0°C, crit = +100.0°C)

nouveau-pci-0100
Adapter: PCI adapter
temp1:        +57.0°C  (high = +95.0°C, hyst =  +3.0°C)
                       (crit = +105.0°C, hyst =  +5.0°C)
                       (emerg = +135.0°C, hyst =  +5.0°C)

```

### Считывание SPD-значений из памяти модулей (опционально)

Чтобы получить значения таймингов SPD с модулей памяти, установите [i2c-tools](https://www.archlinux.org/packages/?name=i2c-tools) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). После установки загрузите `eeprom` [модуль ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)").

```
# modprobe eeprom

```

Теперь можно просмотреть значения с помощью `decode-dimms`.

Вот часть вывода с одной машины:

 `# decode-dimms` 
```
Memory Serial Presence Detect Decoder
By Philip Edelbrock, Christian Zuckschwerdt, Burkart Lingner,
Jean Delvare, Trent Piepho and others

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0050
Guessing DIMM is in                             bank 1

---=== SPD EEPROM Information ===---
EEPROM CRC of bytes 0-116                       OK (0x583F)
# of bytes written to SDRAM EEPROM              176
Total number of bytes in EEPROM                 512
Fundamental Memory type                         DDR3 SDRAM
Module Type                                     UDIMM

---=== Memory Characteristics ===---
Fine time base                                  2.500 ps
Medium time base                                0.125 ns
Maximum module speed                            1066MHz (PC3-8533)
Size                                            2048 MB
Banks x Rows x Columns x Bits                   8 x 14 x 10 x 64
Ranks                                           2
SDRAM Device Width                              8 bits
tCL-tRCD-tRP-tRAS                               7-7-7-33
Supported CAS Latencies (tCL)                   8T, 7T, 6T, 5T

---=== Timing Parameters ===---
Minimum Write Recovery time (tWR)               15.000 ns
Minimum Row Active to Row Active Delay (tRRD)   7.500 ns
Minimum Active to Auto-Refresh Delay (tRC)      49.500 ns
Minimum Recovery Delay (tRFC)                   110.000 ns
Minimum Write to Read CMD Delay (tWTR)          7.500 ns
Minimum Read to Pre-charge CMD Delay (tRTP)     7.500 ns
Minimum Four Activate Window Delay (tFAW)       30.000 ns

---=== Optional Features ===---
Operable voltages                               1.5V
RZQ/6 supported?                                Yes
RZQ/7 supported?                                Yes
DLL-Off Mode supported?                         No
Operating temperature range                     0-85C
Refresh Rate in extended temp range             1X
Auto Self-Refresh?                              Yes
On-Die Thermal Sensor readout?                  No
Partial Array Self-Refresh?                     No
Thermal Sensor Accuracy                         Not implemented
SDRAM Device Type                               Standard Monolithic

---=== Physical Characteristics ===---
Module Height (mm)                              15
Module Thickness (mm)                           1 front, 1 back
Module Width (mm)                               133.5
Module Reference Card                           B

---=== Manufacturer Data ===---
Module Manufacturer                             Invalid
Manufacturing Location Code                     0x02
Part Number                                     OCZ3G1600LV2G     

...

```

## Использование данных датчиков

### Графические фронтэнды

Есть много разнообразных фронтэндов для отображения данных датчиков.

*   [xsensors](https://www.archlinux.org/packages/?name=xsensors) - X11 интерфейс к lm_sensors
*   [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) - lm_sensors плагин для панели среды [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)")
*   [conky](/index.php/Conky_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Conky (Русский)") - Conky предоставляет расширенные возможности для мониторинга, основан на torsmo
*   [kdeutils-superkaramba](https://www.archlinux.org/packages/?name=kdeutils-superkaramba) - Superkaramba позволяет создавать различные виджеты для [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)"). См. примеры на [karamba section on kde-look.org](http://www.kde-look.org/index.php?xcontentmode=38)
*   [sensors-applet](https://www.archlinux.org/packages/?name=sensors-applet) - апплет [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") панели для отображения значений аппаратных датчиков, включая температуру ЦП, скорость вращения вентиляторов и вольтаж.

### sensord

Существует дополнительный демон sensord (включен в пакет [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors)), позволяющий записывать данные с сенсоров в [кольцевые базы данных](http://ru.wikipedia.org/wiki/Кольцевая_база_данных) (rrd) для последующей визуализации. Смотрите sensord для уточнения деталей.

## Советы и рекомендации

### Регулировка значений

В некоторых случаях отображаемые данные могут быть неверными или пользователи могут захотеть изменить вывод. К ним относятся:

*   Неправильные значения температуры из-за неправильного смещения (к примеру температура отображается на 20 ° C текущей).
*   Имеется потребность переименовать вывод для некоторых датчиков.
*   Ядра могут быть отображены в неправильном порядке.

Все вышеперечисленное (и многое другое) можно регулировать переопределив настройки программы, указанные в `/etc/sensors3.conf` путем создания файла `/etc/sensors.d/foo`, в котором можно будет переопределять любые настройки, используемые по умолчанию.  Рекомендуется переименовать 'foo' в соответствии с серией и моделью материнской платы, однако строгость в названии не является обязательной.

**Обратите внимание:** Уже готовые файлы настройки можно посмотреть на сайте [lm-sensor](http://www.lm-sensors.org/wiki/Configurations).

**Обратите внимание:** Не редактируйте /etc/sensors3.conf, т.к. при обновление он перепишется и соответственно измененные данные будут утеряны.

#### Пример 1\. Регулировка температурных смещений

Это реальный пример для системной платы Zotac ION-ITX-A-U. Значения coretemp смещены на 20 °C (более выше) и отрегулированы в соответствии со спецификацией Intel.

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +57.0°C  (crit = +125.0°C)
Core 1:       +55.0°C  (crit = +125.0°C)
...

```

Запустим `sensors` с параметром `-u`, чтобы увидеть, какие параметры доступны для каждого физического чипа (сырой режим)

 `$ sensors -u` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:
  temp2_input: 57.000
  temp2_crit: 125.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 55.000
  temp3_crit: 125.000
  temp3_crit_alarm: 0.000
...

```

Создаем следующий файл для переопределения значений по умолчанию:

 `/etc/sensors.d/Zotac-IONITX-A-U` 
```
chip "coretemp-isa-0000"
  label temp2 "Core 0"
  compute temp2 @-20,@-20

  label temp3 "Core 1"
  compute temp3 @-20,@-20

```

Теперь вызов `sensors` отобразит настроенные значения:

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +37.0°C  (crit = +105.0°C)
Core 1:       +35.0°C  (crit = +105.0°C)
...

```

#### Пример 2\. Переименование параметров

Это реальный пример для системной платы Asus A7M266\. Требуется указать более подробные названия значений температуры 'temp1' and 'temp2':

 `$ sensors` 
```
as99127f-i2c-0-2d
Adapter: SMBus Via Pro adapter at e800
...
temp1:        +35.0°C  (high =  +0.0°C, hyst = -128.0°C)
temp2:        +47.5°C  (high = +100.0°C, hyst = +75.0°C)
...

```

Создаем следующий файл, чтобы переопределить значения по умолчанию:

 `/etc/sensors.d/Asus_A7M266` 
```
chip "as99127f-*"
  label temp1 "Mobo Temp"
  label temp2 "CPU0 Temp"

```

Теперь вызов `sensors` отобразит настроенные значения:

 `$ sensors` 
```
as99127f-i2c-0-2d
Adapter: SMBus Via Pro adapter at e800
...
Mobo Temp:        +35.0°C  (high =  +0.0°C, hyst = -128.0°C)
CPU0 Temp:        +47.5°C  (high = +100.0°C, hyst = +75.0°C)
...

```

#### Пример 3\. Изменение нумерации ядер для многопроцессорных систем

Это реальный пример на HP Z600 workstation с двумя Xeon. Текущая нумерация физических ядер неверно: пронумерованы 0, 1, 9, 10, который повторяются во втором процессоре. Требуется получать значения температур ядер в последовательном порядке, т.е. 0,1,2,3,4,5,6,7.

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core 1:       +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core 9:       +66.0°C  (high = +85.0°C, crit = +95.0°C)
Core 10:      +66.0°C  (high = +85.0°C, crit = +95.0°C)

coretemp-isa-0004
Adapter: ISA adapter
Core 0:       +54.0°C  (high = +85.0°C, crit = +95.0°C)
Core 1:       +56.0°C  (high = +85.0°C, crit = +95.0°C)
Core 9:       +60.0°C  (high = +85.0°C, crit = +95.0°C)
Core 10:      +61.0°C  (high = +85.0°C, crit = +95.0°C)
...

```

Опять же, запустим `sensors` с параметром `-u`, чтобы увидеть, какие варианты доступны для каждого физического чипа:

 `$ sensors -u coretemp-isa-0000` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:
  temp2_input: 61.000
  temp2_max: 85.000
  temp2_crit: 95.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 61.000
  temp3_max: 85.000
  temp3_crit: 95.000
  temp3_crit_alarm: 0.000
Core 9:
  temp11_input: 62.000
  temp11_max: 85.000
  temp11_crit: 95.000
Core 10:
  temp12_input: 63.000
  temp12_max: 85.000
  temp12_crit: 95.000

```
 `$ sensors -u coretemp-isa-0004` 
```
coretemp-isa-0004
Adapter: ISA adapter
Core 0:
  temp2_input: 53.000
  temp2_max: 85.000
  temp2_crit: 95.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 54.000
  temp3_max: 85.000
  temp3_crit: 95.000
  temp3_crit_alarm: 0.000
Core 9:
  temp11_input: 59.000
  temp11_max: 85.000
  temp11_crit: 95.000
Core 10:
  temp12_input: 59.000
  temp12_max: 85.000
  temp12_crit: 95.000
...

```

Создадим следующий файл переопределения значения по умолчанию:

 `/etc/sensors.d/HP_Z600` 
```
chip "coretemp-isa-0000"
  label temp2 "Core 0"
  label temp3 "Core 1"
  label temp11 "Core 2"
  label temp12 "Core 3"

chip "coretemp-isa-0004"
  label temp2 "Core 4"
  label temp3 "Core 5"
  label temp11 "Core 6"
  label temp12 "Core 7"
```

Теперь вызов `sensors` отобразит настроенные значения:

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core0:        +64.0°C  (high = +85.0°C, crit = +95.0°C)
Core1:        +63.0°C  (high = +85.0°C, crit = +95.0°C)
Core2:        +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core3:        +66.0°C  (high = +85.0°C, crit = +95.0°C)

coretemp-isa-0004
Adapter: ISA adapter
Core4:        +53.0°C  (high = +85.0°C, crit = +95.0°C)
Core5:        +54.0°C  (high = +85.0°C, crit = +95.0°C)
Core6:        +59.0°C  (high = +85.0°C, crit = +95.0°C)
Core7:        +60.0°C  (high = +85.0°C, crit = +95.0°C)
...

```

### Автоматизация развертывания lm_sensors

Если потребуется развернуть lm_sensors на нескольких машинах можно использовать любое из следующих действий:

1\. Запуск в неинтерактивном режиме. Будут использоваться ответы по умолчанию (равнозначно нажатию ENTER):

```
# sensors-detect --auto

```

2\. Переопределить стандартные ответы и отвечать ДА на все вопросы:

```
# yes | sensors-detect

```

## Решение проблем

### Модуль K10Temp

У некоторых процессоров K10 имеются проблемы с датчиком температуры. Из документации к ядру (`linux-<version>/Documentation/hwmon/k10temp`):

	*All these processors have a sensor, but on those for Socket F or AM2+, the sensor may return inconsistent values (erratum 319). The driver will refuse to load on these revisions unless users specify the `force=1` module parameter.*

	*Due to technical reasons, the driver can detect only the mainboard's socket type, not the processor's actual capabilities. Therefore, users of an AM3 processor on an AM2+ mainboard, can safely use the `force=1` parameter.*

На проблемных машинах модуль сообщит "unreliable CPU thermal sensor; monitoring disabled". Можно принудительно загрузить его:

```
# rmmod k10temp
# modprobe k10temp force=1

```

Убедитесь, что датчик действительно является достоверными и надежными. Если это так, то можно отредактировать `/etc/modprobe.d/k10temp.conf`, добавив:

```
options k10temp force=1

```

Это позволит активировать модуль при загрузке.

### Датчики не работают с Linux 2.6.31

Изменения в версии 2.6.31 сделали некоторые датчики неработоспособными. Подробности смотрите в [этом FAQ](http://www.lm-sensors.org/wiki/FAQ/Chapter3#Mysensorshavestoppedworkinginkernel2.6.31). Чтобы исправить датчики, добавьте следующий [параметр ядра](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_enforce_resources=lax

```

**Важно:** В некоторых ситуациях, это может быть опасно. Прежде всего обязательно детально ознакомьтесь с FAQ.

Обратите внимание, что в большинстве случаев эта информация до сих пор доступна через другие модули (например, через ACPI модули) для опроса оборудования. Многие утилиты и мониторы (например, `/usr/bin/sensors`) могут собирать информацию из любого источника. По возможности их использование будет предпочтительней.

### Gigabyte GA-J1900N-D3V

The motherboard use the ITE IT8620E chip (useful also to read voltages, mainboard temp, fan speed). Since today 06/10/2014 lm_sensors has no driver support for chip ITE IT8620E [[1]](http://www.lm-sensors.org/wiki/Devices) [[2]](http://comments.gmane.org/gmane.linux.drivers.sensors/35168). lm_sensors developers had a report that the chip is somewhat compatible with the IT8728F for the hardware monitoring part.

You can load the module at runtime with modprobe:

```
$ modprobe it87 force_id=0x8728

```

Or you can use systemd-module-load.service to [load the module](/index.php/Kernel_modules#Loading "Kernel modules") during boot process by creating the following two files.

**/etc/modules-load.d/it87.conf** :

```
it87

```

**/etc/modprobe.d/it87.conf** :

```
options it87 force_id=0x8603

```

Once the module was loaded you can read informations with [Lm_sensors](/index.php/Lm_sensors "Lm sensors"):

```
$ sensors

```

Now you can also use [fancontrol](/index.php/Fancontrol "Fancontrol") to control the speedsteps of your case fan.

### Laptop Screen issues after running sensors-detect

This is caused by lm-sensors messing with the Vcom values of the screen while probing for sensors. It has been discussed and solved at the forums already: [https://bbs.archlinux.org/viewtopic.php?id=193048](https://bbs.archlinux.org/viewtopic.php?id=193048) However, make sure to read through the thread carefully before running any of the suggested commands.