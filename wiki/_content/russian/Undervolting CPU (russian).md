Ссылки по теме

*   [PHC (Русский)](/index.php/PHC_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PHC (Русский)")
*   [CPU frequency scaling (Русский)](/index.php/CPU_frequency_scaling_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CPU frequency scaling (Русский)")
*   [Improving performance (Русский)](/index.php/Improving_performance_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Improving performance (Русский)")
*   [Benchmarking](/index.php/Benchmarking "Benchmarking")
*   [Fan speed control](/index.php/Fan_speed_control "Fan speed control")

**Состояние перевода:** На этой странице представлен перевод статьи [Undervolting CPU](/index.php/Undervolting_CPU "Undervolting CPU"). Дата последней синхронизации: 5 июня 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Undervolting_CPU&diff=0&oldid=574612).

Понижение напряжения ("даунвольтинг" или "андервольтинг") — процесс, который позволяет уменьшить энергопотребление и тепловыделение, не влияя на производительность системы. Обратите внимание, что в большинстве материнских плат ПК настроить напряжение процессора можно также и в BIOS.

**Важно:** Неправильная настройка напряжения процессора может вызвать полный отказ оборудования. Вас предупредили!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Описание](#Описание)
*   [2 Утилиты](#Утилиты)
    *   [2.1 intel-undervolt](#intel-undervolt)
        *   [2.1.1 Установка](#Установка)
        *   [2.1.2 Настройка и использование](#Настройка_и_использование)
    *   [2.2 amdctl](#amdctl)
        *   [2.2.1 Установка](#Установка_2)

## Описание

*   [PHC (Русский)](/index.php/PHC_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PHC (Русский)") — утилита для уменьшения напряжения некоторых старых поколений процессоров Intel и AMD. **Не** совместимо с [драйвером управления частотой процессора](/index.php/CPU_frequency_scaling_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Драйвер_управления_частотой_процессора "CPU frequency scaling (Русский)") `intel_pstate`.
*   [#intel-undervolt](#intel-undervolt) — утилита для уменьшения напряжения процессоров Intel Haswell и выше с помощью MSR. Совместима с `intel_pstate`.
*   [#amdctl](#amdctl) — утилита для уменьшения напряжения процессоров AMD K10 и выше.

## Утилиты

### intel-undervolt

[Intel-undervolt](https://github.com/kitsunyan/intel-undervolt) — утилита, основанная на данной [статье](https://github.com/mihic/linux-intel-undervolt) для уменьшения напряжения процессоров Intel Haswell и выше, используя [MSR](https://en.wikipedia.org/wiki/ru:%D0%9C%D0%BE%D0%B4%D0%B5%D0%BB%D0%B5%D0%B7%D0%B0%D0%B2%D0%B8%D1%81%D0%B8%D0%BC%D1%8B%D0%B5_%D1%80%D0%B5%D0%B3%D0%B8%D1%81%D1%82%D1%80%D1%8B "wikipedia:ru:Моделезависимые регистры") и регистры MCHBAR. Кроме того, она позволяет изменять лимиты мощности и температуры.

#### Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [intel-undervolt](https://aur.archlinux.org/packages/intel-undervolt/).

#### Настройка и использование

Следующая команда выведет настройки напряжения, использующиеся в данный момент:

```
# intel-undervolt read

```

Теперь отредактируйте конфигурационный файл `/etc/intel-undervolt.conf`. Пример конфигурационного файла с уменьшением напряжения кэша процессора на -100mV:

**Примечание:** Судя по всему, значения 'CPU' и 'GPU' не имеют никакого эффекта (во всяком случае, на ноутбуке [ASUS Zenbook UX430UQ](/index.php/ASUS_Zenbook_UX430UQ "ASUS Zenbook UX430UQ")).
 `/etc/intel-undervolt.conf` 
```
...
apply 0 'CPU' 0
apply 1 'GPU' 0
apply 2 'CPU Cache' -100
apply 3 'System Agent' 0
apply 4 'Analog I/O' 0
...

```

Как только вы сохраните конфигурационный файл, проверьте его:

```
# intel-undervolt apply

```

Если настройка была применена, утилита выведет *Success*. Вы можете дважды проверить *текущую* конфигурацию, используя следующую команду:

```
# intel-undervolt read

```

Как только вы найдёте стабильные значения, вы можете также [включить](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C "Включить") `intel-undervolt.service`, чтобы сделать эти настройки постоянными.

### amdctl

[amdctl](https://github.com/kevinlekiller/amdctl/) — утилита для понижения напряжения процессоров AMD K10 и выше.

#### Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [amdctl-git](https://aur.archlinux.org/packages/amdctl-git/).