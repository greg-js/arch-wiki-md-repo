**PowerNow** это технология используемая в некоторых процессорах AMD. Она динамически изменяет напряжение и скорость процессора с целью уменьшить энергопотребление и тепловыделение. Ее еще называют _Cool'n'Quiet_.

## Contents

*   [1 Проверка поддержки PowerNow процессором](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_PowerNow_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.BE.D1.80.D0.BE.D0.BC)
*   [2 Настройка PowerNow в ядре](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_PowerNow_.D0.B2_.D1.8F.D0.B4.D1.80.D0.B5)
*   [3 Настройка Изменения Частоты из пространства пользователя (с использованием cpudyn)](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.A7.D0.B0.D1.81.D1.82.D0.BE.D1.82.D1.8B_.D0.B8.D0.B7_.D0.BF.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.81.D1.82.D0.B2.D0.B0_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.28.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_cpudyn.29)
*   [4 Тестирование](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [5 Альтернатива: cpufrequtils](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.B0:_cpufrequtils)

## Проверка поддержки PowerNow процессором

Если у Вас Intel Core 2:

```
# modprobe acpi_cpufreq

```

Если более ранний процессор Intel, то команда возвратит:

```
FATAL: Error inserting acpi_cpufreq (.../acpi-cpufreq.ko): No such device 

```

тогда попробуйте:

```
# modprobe p4-clockmod
# modprobe speedstep-ich

```

для Pentium 4 или Pentium III-M, или более ранних.

Если у Вас AMD64 (или Sempron-k8):

```
# modprobe powernow-k8

```

Если у Вас более старый процессор попробуйте модули <tt>powernow-k7</tt> или <tt>powernow-k6</tt>.

Если процессор не поддерживает PowerNow, или Cool'n'Quiet отключен в BIOS'e Вы увидите ошибку сразу после попытки загрузки модуля:

```
FATAL: Error inserting powernow_k8 (/lib/modules/2.6.16-ARCH/kernel/arch/i386/kernel/cpu/cpufreq/powernow-k8.ko): No such device

```

Чтобы проверить поддерживает ли загруженное ядро PowerNow! напишите

```
# dmesg | grep powernow

```

Вывод должен выглядеть примерно так (пример для AMD64 3400+ Clawhammer)

```
powernow-k8: Found 1 AMD Athlon 64 / Opteron processors (version 1.60.2)
powernow-k8:    0 : fid 0x10 (2400 MHz), vid 0x2 (1500 mV)
powernow-k8:    1 : fid 0xe (2200 MHz), vid 0x6 (1400 mV)
powernow-k8:    2 : fid 0xc (2000 MHz), vid 0xa (1300 mV)
powernow-k8:    3 : fid 0xa (1800 MHz), vid 0xe (1200 mV)
powernow-k8:    4 : fid 0x2 (1000 MHz), vid 0x12 (1100 mV)

```

## Настройка PowerNow в ядре

Загрузите модули <tt>powernow-k8</tt>, <tt>cpufreq_powersave</tt>, <tt>cpufreq_userspace</tt>, <tt>cpufreq_conservative</tt>, <tt>cpufreq_ondemand</tt> и <tt>freq_table</tt> используя <tt>modprobe</tt>, добавьте их в массив <tt>MODULES</tt> в файле <tt>/etc/rc.conf</tt>.

Затем воспользуйтесь одной из команд для загрузки соответствующей политики энергосбережения статичное минимальное энергопотребление

1.  echo powersave > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

динамическая политика, повышающая энергопотребление по надобности (рекомендуется для мобильных устройств вроде ноутбуков)

1.  echo conservative > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

аналог предыдущей, но рекомендуется для настольных систем

1.  echo ondemand > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

## Настройка Изменения Частоты из пространства пользователя (с использованием cpudyn)

```
# pacman -S acpid cpudyn

```

Запуск cpudyn:

```
# /etc/rc.d/cpudyn start

```

Добавьте <tt>cpudyn</tt> в массив <tt>DAEMONS</tt> в файле <tt>/etc/rc.conf</tt>.

Настройка cpudyn и [acpid](/index.php/Acpid "Acpid") выходит за рамки этой статьи.

## Тестирование

Чтобы проверить работает ли изменение частоты, выполните:

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq

```

и сравните с:

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq

```

Также можно выполнить:

```
cat /dev/urandom > /dev/null

```

в другой консоли, <tt>scaling_cur_freq</tt> должен сравняться с <tt>scaling_max_freq</tt>.

## Альтернатива: cpufrequtils

Это более простой и прямолинейный способ настройки. This is a much easier and straight-forward method of setting this up.

1\. Установите cpufrequtils

```
pacman -S cpufrequtils

```

2\. Отредактируйте должным образом /etc/conf.d/cpufreq

```
# доступные политики:
#  ondemand, performance, powersave, conservative, userspace
governor="ondemand"

# возможные суффиксы: Hz, kHz (default), MHz, GHz, THz
min_freq="2.25GHz"
max_freq="3GHz"

```

Обязательно проверьте эти частоты, т.к. по умолчанию выставлены именно вышеприведенные.

3\. Добавьте нужный модуль (напр. powernow, powernow-k6, или powernow-k8) в массив MODULES в файле /etc/rc.conf - по умолчанию они не загружаются.

4\. Добавьте 'cpufreq' в массив DAEMONS в файле /etc/rc.conf чтобы он запускался во время загрузки. Чтобы запустить его прямо сейчас:

```
/etc/rc.d/cpufreq start

```