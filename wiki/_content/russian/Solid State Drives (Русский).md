Твердотельные накопители (SSD) не достаточно просто подключить чтобы они заработали должным образом. Необходимо учитывать некоторые специфичные вещи для достижения оптимальной производительности, такие как выравнивание разделов, выбор файловой системы, поддержка TRIM и т.д. Статья пытается охватить общую информацию и ключевые понятия, чтобы позволить пользователям получить максимальную отдачу от твердотельных дисков под Linux. Рекомендуется прочесть статью полностью перед тем, как следовать рекомендациям.

**Обратите внимание:** Хотя статья и предназначена для пользователей Linux, большая часть информации может относиться также и к другим операционным системам, таким как BSD, Mac OS X или Windows.

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
    *   [1.1 Преимущества перед HDD](#.D0.9F.D1.80.D0.B5.D0.B8.D0.BC.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4_HDD)
    *   [1.2 Недостатки](#.D0.9D.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D1.82.D0.BA.D0.B8)
    *   [1.3 На что обращать внимание перед покупкой](#.D0.9D.D0.B0_.D1.87.D1.82.D0.BE_.D0.BE.D0.B1.D1.80.D0.B0.D1.89.D0.B0.D1.82.D1.8C_.D0.B2.D0.BD.D0.B8.D0.BC.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4_.D0.BF.D0.BE.D0.BA.D1.83.D0.BF.D0.BA.D0.BE.D0.B9)
*   [2 Советы по увеличению производительности SSD](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.BF.D0.BE_.D1.83.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D1.8E_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8_SSD)
    *   [2.1 Выравнивание разделов](#.D0.92.D1.8B.D1.80.D0.B0.D0.B2.D0.BD.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
    *   [2.2 TRIM](#TRIM)
        *   [2.2.1 Проверьте, поддерживается ли TRIM](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D1.8C.D1.82.D0.B5.2C_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BB.D0.B8_TRIM)
        *   [2.2.2 Включите TRIM с помощью флагов монтирования](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D0.B5_TRIM_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D1.84.D0.BB.D0.B0.D0.B3.D0.BE.D0.B2_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
        *   [2.2.3 Применение TRIM по раписанию cron](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_TRIM_.D0.BF.D0.BE_.D1.80.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8E_cron)
        *   [2.2.4 Применение TRIM по systemd таймеру](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_TRIM_.D0.BF.D0.BE_systemd_.D1.82.D0.B0.D0.B9.D0.BC.D0.B5.D1.80.D1.83)
        *   [2.2.5 Включение TRIM с помощью tune2fs (Discouraged)](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_TRIM_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_tune2fs_.28Discouraged.29)
        *   [2.2.6 Включение TRIM для LVM](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_TRIM_.D0.B4.D0.BB.D1.8F_LVM)
        *   [2.2.7 Включение TRIM для dm-crypt](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_TRIM_.D0.B4.D0.BB.D1.8F_dm-crypt)
    *   [2.3 Планировщик ввода/вывода](#.D0.9F.D0.BB.D0.B0.D0.BD.D0.B8.D1.80.D0.BE.D0.B2.D1.89.D0.B8.D0.BA_.D0.B2.D0.B2.D0.BE.D0.B4.D0.B0.2F.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0)
        *   [2.3.1 Параметр ядра (для единственного накопителя)](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80_.D1.8F.D0.B4.D1.80.D0.B0_.28.D0.B4.D0.BB.D1.8F_.D0.B5.D0.B4.D0.B8.D0.BD.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BD.D0.B0.D0.BA.D0.BE.D0.BF.D0.B8.D1.82.D0.B5.D0.BB.D1.8F.29)
        *   [2.3.2 Использование udev как для одного накопителя, так и для нескольких разных](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_udev_.D0.BA.D0.B0.D0.BA_.D0.B4.D0.BB.D1.8F_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BD.D0.B0.D0.BA.D0.BE.D0.BF.D0.B8.D1.82.D0.B5.D0.BB.D1.8F.2C_.D1.82.D0.B0.D0.BA_.D0.B8_.D0.B4.D0.BB.D1.8F_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D1.85_.D1.80.D0.B0.D0.B7.D0.BD.D1.8B.D1.85)
    *   [2.4 Разделы подкачки на SSD](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8B_.D0.BF.D0.BE.D0.B4.D0.BA.D0.B0.D1.87.D0.BA.D0.B8_.D0.BD.D0.B0_SSD)
    *   [2.5 Hdparm shows "frozen" state](#Hdparm_shows_.22frozen.22_state)
    *   [2.6 Очистка ячеек памяти SSD](#.D0.9E.D1.87.D0.B8.D1.81.D1.82.D0.BA.D0.B0_.D1.8F.D1.87.D0.B5.D0.B5.D0.BA_.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8_SSD)
    *   [2.7 Resolving NCQ Errors](#Resolving_NCQ_Errors)
*   [3 Советы для уменьшения операций чтения/записи](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B4.D0.BB.D1.8F_.D1.83.D0.BC.D0.B5.D0.BD.D1.8C.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D0.BF.D0.B5.D1.80.D0.B0.D1.86.D0.B8.D0.B9_.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D1.8F.2F.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8)
    *   [3.1 Продуманная схема разделов](#.D0.9F.D1.80.D0.BE.D0.B4.D1.83.D0.BC.D0.B0.D0.BD.D0.BD.D0.B0.D1.8F_.D1.81.D1.85.D0.B5.D0.BC.D0.B0_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
    *   [3.2 Опция монтирования noatime](#.D0.9E.D0.BF.D1.86.D0.B8.D1.8F_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_noatime)
    *   [3.3 Расположите часто используемые файлы в оперативной памяти](#.D0.A0.D0.B0.D1.81.D0.BF.D0.BE.D0.BB.D0.BE.D0.B6.D0.B8.D1.82.D0.B5_.D1.87.D0.B0.D1.81.D1.82.D0.BE_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_.D0.B2_.D0.BE.D0.BF.D0.B5.D1.80.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D0.B9_.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8)
        *   [3.3.1 Профили браузеров](#.D0.9F.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B8_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.BE.D0.B2)
        *   [3.3.2 Другие файлы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B)
    *   [3.4 Компиляция в tmpfs](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_.D0.B2_tmpfs)
    *   [3.5 Отключение журналирования ФС](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B6.D1.83.D1.80.D0.BD.D0.B0.D0.BB.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.A4.D0.A1)
*   [4 Выбор файловой системы](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [4.1 Btrfs](#Btrfs)
    *   [4.2 Ext4](#Ext4)
    *   [4.3 XFS](#XFS)
    *   [4.4 JFS](#JFS)
    *   [4.5 Другие файловые системы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
*   [5 Обновление прошивок](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D1.88.D0.B8.D0.B2.D0.BE.D0.BA)
    *   [5.1 OCZ](#OCZ)
*   [6 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Обзор

### Преимущества перед HDD

*   Высокая скорость чтения. В 2-3 раза быстрее современных HDD (7200 об/мин на интерфейсе SATA2).
*   Устойчивая скорость чтения. Скорость чтения не уменьшается на протяжении всего объёма диска, тогда как производительность HDD падает при перемещении головок от края пластин к центру.
*   Минимальное время доступа. Приблизительно в 100 раз быстрее HDD. Например, 0,1 мс для SSD против 12-20 мс для HDD.
*   Высокая степень надежности.
*   Отсутствие движущихся частей.
*   Минимальный нагрев.
*   Минимальное потребление энергии. 1-2 Вт для SSD против 10-30 Вт для HDD (в зависимости от об/мин).
*   Легкие. Идеальное решение для ноутбуков.

### Недостатки

*   Цена за единицу объёма (сотни рублей за ГБ на SSD, тогда как стоимость ГБ на HDD измеряется копейками).
*   Ёмкость представленных моделей SSD намного ниже оной для HDD.
*   Большие ячейки памяти требуют различных оптимизаций файловых систем. Низкий уровень доступа скрыт за контроллером, в то время как современные ОС могли бы использовать низкий уровень для собственных оптимизаций.
*   Разделы и файловые системы требуют специальных оптимизаций. Размер страницы и размер стираемой страницы автоматически не определяется.
*   Ячейки изнашиваются. MLC-ячейки, произведённые по 50нм техпроцессу, могут выдерживать до 10 тысяч циклов записи; 35нм обычно выдерживают всего 5000 циклов, а 25нм — 3000 (чем меньше техпроцесс, тем больше плотность и ниже цена). Если участки записи распределены соответствующим образом, не слишком малы и верно выровнены, это увеличивает срок жизни ячеек пропорционально общему объёму. Ежедневные объёмы записи должны быть сбалансированными в течение всего срока службы. Однако, тесты [[1]](http://techreport.com/review/25889/the-ssd-endurance-experiment-500tb-update)[[2]](http://techreport.com/review/26523/the-ssd-endurance-experiment-casualties-on-the-way-to-a-petabyte)[[3]](http://techreport.com/review/27436/the-ssd-endurance-experiment-two-freaking-petabytes) проведённые на современных SSD показали, что износ накопителя является незначительным, а срок службы SSD сравним с оным для HDD, даже при больших объёмах записи.
*   Сложные прошивки и контроллеры. В них часто встречаются баги. Современные потребляют мощность, сравнимую с HDD. Они [реализуют](https://lwn.net/Articles/353411/) подобие журнально-структурированной файловой системы со сборкой мусора, переводят команды SATA, изначально предназначенные для HDD; некоторые реализуют сжатие на лету. Также контроллер распределяет циклы записи по всей области диска для предотвращения быстрого износа ячеек, объединяет несколько команд записи мелких данных в одну, опять же, для увеличения продолжительности жизни диска. Наконец, они перемещают ячейки с данными по диску, чтобы те со временем не потеряли содержимое.
*   Может падать производительность в зависимости от заполненности диска. Не все производители реализовывают сборку мусора достаточно хорошо, поэтому фрагментированное свободное пространство не всегда объединяется в целые ячейки.

### На что обращать внимание перед покупкой

Есть несколько ключевых особенностей, на которые стоит обратить внимание до покупки SSD.

*   Родная поддержка [TRIM](https://en.wikipedia.org/wiki/ru:TRIM "wikipedia:ru:TRIM"). Это жизненно необходимая функция для продления срока службы SSD и предотвращения уменьшения производительности операций записи от времени.
*   Ключевым моментом является покупка SSD верного объема. Для эффективной работы разделы во всех файловых системах должны быть заполнены не более, чем на 75%.

## Советы по увеличению производительности SSD

### Выравнивание разделов

Смотрите [Partitioning#Partition alignment](/index.php/Partitioning#Partition_alignment "Partitioning").

### TRIM

**Обратите внимание:** TRIM дословно переводится как "подрезка", "подравнивать". - прим. пер.

Большинство SSD накопителей поддерживают [команду ATA_TRIM](https://en.wikipedia.org/wiki/ru:TRIM "wikipedia:ru:TRIM"), с помощью которой осуществляется одинаковая производительность и распределение износа. За подробностями, описывающими производительность до и после использования TRIM обратитесь к [этому](https://sites.google.com/site/lightrush/random-1/howtoconfigureext4toenabletrimforssdsonubuntu) учебнику.

Начиная с ядра linux версии 3.7, следующие файловые системы поддерживают TRIM: [Ext4](/index.php/Ext4_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Ext4 (Русский)"), [Btrfs](/index.php/Btrfs "Btrfs"), [JFS](/index.php/JFS "JFS"), VFAT, [XFS](/index.php/XFS "XFS").

VFAT поддерживает TRIM только с помощью флага монтирования 'discard', а не с помощью fstrim.

Раздел [#Выбор файловой системы](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B) в этой статье содержит более подробную информацию.

#### Проверьте, поддерживается ли TRIM

```
# hdparm -I /dev/sda | grep TRIM
        *    Data Set Management TRIM supported (limit 1 block)

```

Чтобы понять, в чём отличие между "limit 1 block" и "limit 8 blocks", обратитесь к статье [wikipedia:TRIM#ATA](https://en.wikipedia.org/wiki/TRIM#ATA "wikipedia:TRIM")

#### Включите TRIM с помощью флагов монтирования

Используйте следующий флаг монтирования в вашем `/etc/fstab`, чтобы получить преимущества команды TRIM, описанные выше:

```
/dev/sda1  /       ext4   defaults,noatime,**discard**   0  1
/dev/sda2  /home   ext4   defaults,noatime,**discard**   0  2

```

**Обратите внимание:**

*   TRIM не включается по умолчанию при использовании шифрования блочных устройств на SSD; для дополнительной информации смотрите [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties").
*   Нет необходимости использовать флаг `discard`, если вы периодически запускаете `fstrim`.
*   Использование флага `discard` для корневого раздела с файловой системой ext3 приведёт к тому, что он будет смонтирован в режиме только-чтение.

**Важно:** Вы должны убедиться, что ваш SSD поддерживает TRIM перед тем, как пытаться монтировать раздел с флагом `discard`. Иначе вы можете потерять данные!

#### Применение TRIM по раписанию cron

**Обратите внимание:** Этот метод не работает для файловых систем VFAT.

Безусловно рекомендуется включать TRIM на поддерживаемых SSD накопителях. Однако, иногда на некоторых SSD это может приводить к [замедлению работы](https://patrick-nagel.net/blog/archives/337) при удалении файлов. Если это ваш случай, вы можете использовать fstrim как альтернативу.

```
# fstrim -v /

```

Раздел, который вы хотите "подтримить" должен быть примонтирован и должен быть указан точкой монтирования.

Если вам больше подходит данный способ, хорошей идеей будет запуск этой команды время от времени с помощью планировщика cron. Чтобы запускать эту команду ежедневно, установите cron пакет ([cronie](https://www.archlinux.org/packages/?name=cronie)), реализация которого по умолчанию установлена на запуск ежечасных, ежедневных, еженедельных и ежемесячных заданий. Обратите внимание, что [cronie systemd сервис](/index.php/Cron#Activation_and_autostart "Cron") не включен по умолчанию в новых установках Arch. Чтобы добавить эту команду в список ежедневных заданий cron, просто создайте скрипт script, содержащий эту команду и положите его в `/etc/cron.daily`, `/etc/cron.weekly`, и т.д. Если выбран этот способ, то рекомендуется подобрать соответствующие значения nice и ionice. После того как проделаете всё это, уберите опцию `discard` из `/etc/fstab`.

**Обратите внимание:** Сначала вы должны попробовать использовать способ с опцией монтирования `discard`. Данный же способ нужно выбирать только если первый вам не подошёл для нормальной реализации TRIM.

#### Применение TRIM по systemd таймеру

Пакет [util-linux](https://www.archlinux.org/packages/?name=util-linux) предоставляет [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") юнит файлы `fstrim.service` и `fstrim.timer` . Если [включить](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") таймер, то сервис будет активироваться еженедельно, подравнивая все примонтированные файловые системы на устройствах, поддерживающих операцию discard.

#### Включение TRIM с помощью tune2fs (Discouraged)

Вы можете статически установить флаг trim с помощью tune2fs:

```
# tune2fs -o discard /dev/sd**XY**

```

**Важно:** При использовании данного способа, опция `discard` [НЕ будет показана](https://bbs.archlinux.org/viewtopic.php?id=137314) командой `mount`.

#### Включение TRIM для LVM

Измените значение опции `issue_discards` с 0 на 1 в файле `/etc/lvm/lvm.conf`.

**Обратите внимание:** Enabling this option will "issue discards to a logical volumes's underlying physical volume(s) when the logical volume is no longer using the physical volumes' space (e.g. lvremove, lvreduce, etc)" (смотрите `man lvm.conf` и/или вписанные комментарии в `/etc/lvm/lvm.conf`). As such it does not seem to be required for "regular" TRIM requests (file deletions inside a filesystem) to be functional.

#### Включение TRIM для dm-crypt

**Важно:** The discard option allows discard requests to be passed through the encrypted block device. This improves performance on SSD storage but has security implications. See [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") for more information.

For non-root filesystems, configure `/etc/crypttab` to include `discard` in the list of options for encrypted block devices located on a SSD (see [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration")).

For the root filesystem, follow the instructions from [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") to add the right kernel parameter to the bootloader configuration.

### Планировщик ввода/вывода

Рассмотрим переход со стандартного [CFQ](https://en.wikipedia.org/wiki/CFQ "wikipedia:CFQ") планировщика (Completely Fair Queuing) к планировщикам [NOOP](https://en.wikipedia.org/wiki/NOOP_scheduler "wikipedia:NOOP scheduler") или [Deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "wikipedia:Deadline scheduler"). Последние два обеспечивают повышение производительности SSD. Планировщик NOOP, например, реализует простую очередь входящих запросов чтения/записи без их переупорядочивания или группировки тех, что физически расположены ближе на накопителе. На SSD, в отличие от HDD, время доступа одинаково для всех секторов, поэтому изменение порядка запросов не имеет смысла.

Arch по умолчанию использует планировщик CFQ. Убедиться в этом можно, выведя содержимое файла `/sys/block/sdX/queue/scheduler`:

```
$ cat /sys/block/sdX/queue/scheduler
noop deadline [cfq]

```

Планировщик, используемый в данный момент, в списке доступных планировщиков выделен квадратными скобками.

Вы можете поменять планировщик прямо на лету, без необходимости перезагрузки:

```
# echo noop > /sys/block/sd**X**/queue/scheduler

```

или:

```
$ sudo tee /sys/block/sd**X**/queue/scheduler <<< noop

```

Это непостоянный способ (то есть ваше изменение отменится после перезагрузки). Чтобы убедиться в том, что изменения вступили в силу, снова посмотрите содержимое файла и убедитесь, что теперь "noop" в квадратных скобках.

##### Параметр ядра (для единственного накопителя)

Если в системе единственным устройством накопления является SSD, то рекомендуется настроить планировщик ввода/вывода для всей системы с помощью [параметра ядра](/index.php/%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B_%D1%8F%D0%B4%D1%80%D0%B0 "Параметры ядра") `elevator=noop`.

##### Использование udev как для одного накопителя, так и для нескольких разных

Хотя вышеописанные методы будут работать без проблем, ниже представлено также довольно надёжное решение. Следует отметить, что с переходом на [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), файл rc.local больше не существует. Следовательно, было бы предпочтительнее использовать систему, которая отвечает за устройства, в первую очередь для реализации планировщика. В нашем случае это udev, и чтобы осуществить задуманное, всё что нам нужно — простое [udev](/index.php/Udev "Udev")-правило.

Создайте файл в директории /etc/udev/rules.d с именем, например, '60-schedulers.rules'. Запишите в него следующие строки:

```
# установка планировщика deadline для SSD
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="deadline"

# установка планировщика cfq для HDD
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="cfq"

```

Конечно же вы можете заменить deadline/cfq любыми другими планировщиками. Изменения вступают в силу после перезагрузки. Чтобы проверить сработало ли правило, выполните команду

```
$ cat /sys/block/sdX/queue/scheduler   #где X — буква физического накопителя

```

**Обратите внимание:** Имейте в виду, CFQ является планировщиком по умолчанию, так что второе правило на самом деле не нужно, если вы пользуетесь стандартным ядром. Также в примере имя правила начинается с числа 60, т. к. это число udev использует для своих строгих правил именования. Блочные устройства в этом диапазоне чисел могут модифицироваться, и это безопасная позиция для данного правила. Однако, правило может называться как угодно, при этом оканчиваться на '.rules'. (Источник: falconindy и w0ng на своём блоге)

### Разделы подкачки на SSD

Можно размещать раздел подкачки на SSD. Но с другой стороны, современные компьютеры, имеющие более 2 ГБ оперативной памяти, используют раздел подкачки очень редко. Заметным исключением являются системы, которые используют спящий режим. Следующая оптимизация для SSD уменьшает "swappiness" системы, чтобы избежать записей подкачки:

```
# echo 1 > /proc/sys/vm/swappiness

```

Или можно просто изменить файл `/etc/sysctl.d/40-swappiness.conf` как рекомендуется в вики-статье [Maximizing Performance](/index.php/Maximizing_performance#Swappiness "Maximizing performance"):

```
vm.swappiness=1
vm.vfs_cache_pressure=50

```

### Hdparm shows "frozen" state

Some motherboard BIOS' issue a "security freeze" command to attached storage devices on initialization. Likewise some SSD (and HDD) BIOS' are set to "security freeze" in the factory already. Both result in the device's password security settings to be set to **frozen**, as shown in below output:

 `:~# hdparm -I /dev/sda` 
```
Security: 
 	Master password revision code = 65534
 		supported
 	not	enabled
 	**not	locked**
 		**frozen**
 	not	expired: security count
 		supported: enhanced erase
 	4min for SECURITY ERASE UNIT. 2min for ENHANCED SECURITY ERASE UNIT.
```

Operations like formatting the device or installing operating systems are not affected by the "security freeze".

The above output shows the device is **not locked** by a HDD-password on boot and the **frozen** state safeguards the device against malwares which may try to lock it by setting a password to it at runtime.

If you intend to set a password to a "frozen" device yourself, a motherboard BIOS with support for it is required. A lot of notebooks have support, because it is required for [hardware encryption](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption"), but support may not be trivial for a desktop/server board. For the Intel DH67CL/BL motherboard, for example, the motherboard has to be set to "maintenance mode" by a physical jumper to access the settings (see [[4]](http://sstahlman.blogspot.in/2014/07/hardware-fde-with-intel-ssd-330-on.html?showComment=1411193181867#c4579383928221016762), [[5]](https://communities.intel.com/message/251978#251978)).

**Warning:** Do not try to change the above **lock** security settings with `hdparm` unless you know exactly what you are doing.

If you intend to erase the SSD, see [Securely wipe disk#hdparm](/index.php/Securely_wipe_disk#hdparm "Securely wipe disk") and [below](#SSD_Memory_Cell_Clearing).

### Очистка ячеек памяти SSD

В некоторых случаях, пользователь может полностью сбросить ячейки SSD в состояние, подобное моменту покупки нового накопителя, таким образом добиться [заводской производительности](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Скорость записи уменьшается со временем даже с поддержкой TRIM. TRIM работает только с удалением файлов, но не с перемещением и инкрементальными сохранениями.

Сброс ячеек легко выполнить за 3 шага, описанных в вики-статье [SSD Memory Cell Clearing](/index.php/SSD_Memory_Cell_Clearing "SSD Memory Cell Clearing").

### Resolving NCQ Errors

Some SSDs and SATA chipsets do not work properly with Linux Native Command Queueing (NCQ). The tell-tale dmesg errors look like this:

```
[ 9.115544] ata9: exception Emask 0x0 SAct 0xf SErr 0x0 action 0x10 frozen
[ 9.115550] ata9.00: failed command: READ FPDMA QUEUED
[ 9.115556] ata9.00: cmd 60/04:00:d4:82:85/00:00:1f:00:00/40 tag 0 ncq 2048 in
[ 9.115557] res 40/00:18:d3:82:85/00:00:1f:00:00/40 Emask 0x4 (timeout)

```

These may be resolved by one of the following methods:

1.  Update the firmware on the SSD. See [SSD#Firmware_Updates](/index.php/SSD#Firmware_Updates "SSD").
2.  Update the BIOS/UEFI on the motherboard. See [Flashing_BIOS_from_Linux](/index.php/Flashing_BIOS_from_Linux "Flashing BIOS from Linux").
3.  Disable NCQ on boot. Add `libata.force=noncq` to the kernel command line in the [Bootloader](/index.php/Bootloader "Bootloader") configuration.

If these do not resolve the problem or cause other issues, [file a bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines").

## Советы для уменьшения операций чтения/записи

Основной идеей долговечного использования SSD является перенос интенсивных операция ввода/вывода в оперативную память или HDD, в основном из-за большого размера блока очистки (512 КиБ в некоторых случаях).

**Обратите внимание:** 32ГБ SSD с посредственным 10-кратным показателем write amplification, стандартными 10000 циклами чтения/записи и **10ГБ записей в день** дают **8 лет жизни**. Также, дольше живут диски с наибольшими объемами и современными контроллерами, которые имеют меньший показатель write amplification.

Используйте команду `iotop -oPa` и отсортируйте по количеству записей, чтобы увидеть сколько пишется на диск.

### Продуманная схема разделов

Если в системе установлены одновременно оба типа дисков (HDD и SSD), то рекомендуется монтировать раздел `/var` на HDD, чтобы продлить жизнь SSD, избежав на нём множества операций чтения/записи.

Если же SSD является единственным диском в системе, и нет возможности использовать его совместно с HDD, разумно так же выделить отдельный раздел для `/var`, чтобы в дальнейшем при возникновении ошибки было легче восстановить систему. Например, если программа использовала всё доступное пространство в `/`, какой-либо лог превысил все разумные размеры, и т. п.

### Опция монтирования noatime

Монтируйте разделы SSD с опцией `noatime`. См. раздел [Параметры монтирования](#.D0.9F.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F).

Существует несколько ключевых параметров монтирования, используемых в `/etc/fstab` для разделов на SSD.

*   **noatime** - Во время чтения файлов не будет обновляться поле atime файловой системы, указывающее время последнего доступа к файлу. Важность данного параметра в том, что он убирает необходимость системы производить "ненужные" операции записи когда файл всего-навсего необходимо прочитать. Т. к. эти операции записи могут быть достаточно интенсивными при чтении большого количества файлов, отключение может дать неплохой прирост производительности и срока жизни. Заметьте, что информация о времени последней записи файла будет по-прежнему обновляться каждый раз, когда файл будет изменён.
    *   Однако, эта опция может вызвать проблемы с некоторыми программами, такими как [Mutt](/index.php/Mutt "Mutt"), т. к. время доступа к файлу станет меньше, чем время изменения, что вызовет проблемы в работе. Использование опции **relatime** вместо noatime позволит быть уверенным, что поле atime никогда не станет меньше, чем время изменения.
*   **discard** - Параметр discard включает команду TRIM для ядер версии 2.6.33 и выше. Не работает с файловой системой ext3; если всё же он включен на ext3, корневой раздел будет смонтирован только для чтения.

```
/dev/sda1 / ext4 defaults,relatime,discard 0 1
/dev/sda2 /home ext4 defaults,relatime,discard 0 1

```

**Важно:** Пользователь должен убедиться ещё ДО попытки монтирования раздела с опцией `discard`, что он работает на ядре версии 2.6.33 или выше, а также, что его SDD поддерживает TRIM. Иначе можно потерять данные!

### Расположите часто используемые файлы в оперативной памяти

#### Профили браузеров

Довольно просто можно перенести профили браузеров, таких как chromium, firefox, opera, и т.д. в оперативную память через tmpfs и использовать rsync для синхронизации с копиями на диске. Таким образом можно так же заметно сократить количество операций чтения/записи.

В AUR есть несколько пакетов для автоматизации этой операции, например [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/).

#### Другие файлы

По этой же вышеописанной причине можно расположить в оперативной памяти раздел `/srv/http` (если запущен web-сервер). Аналогом [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/) здесь будет [anything-sync-daemon](https://aur.archlinux.org/packages/anything-sync-daemon/), который позволяет определить **любую** директорию для синхронизации с оперативной памятью.

**Важно:** Не пытайтесь добавлять /var/log в anything-sync-daemon. Systemd очень разозлится на это.

### Компиляция в tmpfs

Перенос интенсивной компиляции в `/tmp` — отличная идея продления срока жизни диска. Если у вас имеется более 4ГБ оперативной памяти, строку tmp из `/etc/fstab` нужно изменить, чтобы раздел использовал больше половины доступной памяти, через параметр `size=`, т. к. `/tmp` при компиляции растёт очень быстро.

Пример для машины с 8ГБ оперативки:

```
tmpfs /tmp tmpfs nodev,nosuid,size=7G 0 0

```

### Отключение журналирования ФС

Использование журналируемых ФС типа ext3 или ext4 с отключенным журналом тоже сократит количество записей на SSD. Очевидным недостатком этого будет являться потеря данных при неудачном размонтировании (резкое отключение питания, блокировка ядра и т. д.). Однако, [Ted Tso](http://tytso.livejournal.com/61830.html) выступает в защиту журналирования на современных SSD, т. к. по его тестам оно незначительно влияет на количество записей в большинстве случаев:

**Количество записанных данных (в мегабайтах) на ФС ext4 с параметром noatime.**

| операция | с журналом | без журнала | разница |
| git clone | 367.0 | 353.0 | 3.81 % |
| make | 207.6 | 199.4 | 3.95 % |
| make clean | 6.45 | 3.73 | 42.17 % |

*"Результаты показали, что записанный объём при работе с большим количеством мета-данных почти в 2 раза выше, чем реальный размер файлов. Это ожидаемо, т. к. все изменения в блоках мета-данных сначала пишутся в журнал, и транзакция журнала сбрасывается перед тем, как мета-данные будут записаны в конечное положение на диск. Однако же, для обычных задач, где данные пишутся сразу за мета-данными, разница в лишних операциях записи минимальна."*

**Обратите внимание:** Пример make clean из таблицы выше показывает важность переноса компиляции в tmpfs как рекомендовано в предыдущем разделе!

## Выбор файловой системы

Существуют различные варианты файловых систем на выбор, включая Ext2/3/4, Btrfs, и т. д.

### Btrfs

Поддержка [Btrfs](http://ru.wikipedia.org/wiki/Btrfs) включена в ядро с версии 2.6.29\. Некоторые считают, что она является не достаточно стабильной для повседневного использования, в то время как есть и явные сторонники этого потенциального преемника ext4\. Рекомендуется прочитать статью [Btrfs](/index.php/Btrfs "Btrfs") для дополнительного ознакомления.

### Ext4

[Ext4](http://ru.wikipedia.org/wiki/Ext4) — ещё одна файловая система, поддерживающая SSD. Считается стабильной и пригодной для повседневного использования с версии ядра 2.6.28\. В отличие от Btrfs, ext4 не умеет автоматически определять тип диска; пользователь сам должен явно включить поддержку команды TRIM, используя параметр монтирования `discard` в [fstab](/index.php/Fstab "Fstab") (или командой `tune2fs -o discard /dev/sdaX`). См. [официальную документацию ядра](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=Documentation/filesystems/ext4.txt) для подробного ознакомления c ext4.

### XFS

Many users do not realize that in addition to ext4 and btrfs, [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") has TRIM support as well. This can be enabled in the usual ways. That is, the choice may be made of either using the discard option mentioned above, or by using the fstrim command. More information can be found on the [XFS wiki](http://xfs.org/index.php/FITRIM/discard).

### JFS

As of Linux kernel version 3.7, proper TRIM support has been added. So far, there is not a great wealth of information of the topic but it has certainly been picked up by [Linux news sites.](http://www.phoronix.com/scan.php?page=news_item&px=MTE5ODY) It is apparent that it can be enabled via the `discard` mount option, or by using the method of batch TRIMs with fstrim.

### Другие файловые системы

Существуют также другие файловые системы, специально [предназначенные для SSD](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D1%85_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D0.B4.D0.BB.D1.8F_.D1.84.D0.BB.D0.B5.D1.88-.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2_.2F_.D1.82.D0.B2.D0.B5.D1.80.D0.B4.D0.BE.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.BD.D0.BE.D1.81.D0.B8.D1.82.D0.B5.D0.BB.D0.B5.D0.B9 "wikipedia:ru:Список файловых систем"), например [F2FS](/index.php/F2FS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "F2FS (Русский)").

## Обновление прошивок

### OCZ

Для дисков компании OCZ имеется утилита командной строки для Linux (i686 и x86_64) на официальном [форуме](http://www.ocztechnology.com/ssd_tools/) или в [AUR](https://aur.archlinux.org) [ocztoolbox](https://aur.archlinux.org/packages/ocztoolbox/)

## См. также

*   [Discussion on Reddit about installing Arch on an SSD](http://www.reddit.com/r/archlinux/comments/rkwjm/what_should_i_keep_in_mind_when_installing_on_ssd/)