**Примечание:** В настоящий момент статья переводится. Вы можете помочь завершить перевод скорее :)

**Важно:** Оригинальная английская статья ещё не завершена, к моменту начала перевода текст может оказаться устаревшим.

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
*   [2 Инструменты для работы с разделами](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D1.81_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0.D0.BC.D0.B8)
*   [3 Стратегии разбиения на разделы](#.D0.A1.D1.82.D1.80.D0.B0.D1.82.D0.B5.D0.B3.D0.B8.D0.B8_.D1.80.D0.B0.D0.B7.D0.B1.D0.B8.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BD.D0.B0_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8B)
*   [4 Важные моменты](#.D0.92.D0.B0.D0.B6.D0.BD.D1.8B.D0.B5_.D0.BC.D0.BE.D0.BC.D0.B5.D0.BD.D1.82.D1.8B)
*   [5 Creating new partitions](#Creating_new_partitions)
*   [6 Resizing partitions](#Resizing_partitions)
*   [7 Content from BG](#Content_from_BG)
    *   [7.1 Разметка жестких дисков](#.D0.A0.D0.B0.D0.B7.D0.BC.D0.B5.D1.82.D0.BA.D0.B0_.D0.B6.D0.B5.D1.81.D1.82.D0.BA.D0.B8.D1.85_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2)
        *   [7.1.1 Информация о разделах](#.D0.98.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0.D1.85)
        *   [7.1.2 Раздел Swap](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_Swap)
        *   [7.1.3 Схема разметки](#.D0.A1.D1.85.D0.B5.D0.BC.D0.B0_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.82.D0.BA.D0.B8)
        *   [7.1.4 Насколько большими должны быть мои разделы?](#.D0.9D.D0.B0.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B8.D0.BC.D0.B8_.D0.B4.D0.BE.D0.BB.D0.B6.D0.BD.D1.8B_.D0.B1.D1.8B.D1.82.D1.8C_.D0.BC.D0.BE.D0.B8_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8B.3F)
        *   [7.1.5 Create Partition:cfdisk](#Create_Partition:cfdisk)
    *   [7.2 Set Filesystem Mountpoints](#Set_Filesystem_Mountpoints)
        *   [7.2.1 Filesystem Types](#Filesystem_Types)
        *   [7.2.2 A note on Journaling](#A_note_on_Journaling)

## Обзор

*   Что такое разделы жёсткого диска?
*   Зачем разбивать на разделы жёсткий диск?

**Разбиение** жёсткого диска позволяет логически разделить всё доступное пространство на части, которые будут независимыми друг от друга. Информация о разделах хранится внутри MBR жёсткого диска.

Существует несколько причин для разбиение диска на разделы:

*   на компьютере используется несколько операционных систем (двойная, мультизагрузка)
*   есть необходимость использовать раздел подкачки swap
*   необходимо разделить данные логически (например, видеоклипы от фонотеки)
*   и др.

**Важно:** На диске может быть до 4 "первичных" (primary) разделов, или же до 3 первичных + 1 расширенный (extended) раздел. Расширенный раздел служит "контейнером" для "логических" разделов, последних может быть сколько угодно.

```
**Все разделы первичные**
+-------------+-------------+-------------+---------------------------------+
| Первичный 1 | Первичный 2 | Первичный 3 | Первичный 4                     |
+-------------+-------------+-------------+---------------------------------+

**Два первичных раздела и один расширенный, с двумя логическими**
+----------------+------------------+---------------------------------------+
| Первичный 1    | Первичный 2      | Расширенный                           |
|                |                  | +--------------------+--------------+ |
|                |                  | | Логический 1       | Логический 2 | |
|                |                  | +-----------------------------------+ |
+----------------+------------------+-------------+-------------------------+

```

## Инструменты для работы с разделами

*   fdisk & cfdisk
*   GNU Parted
*   QtParted & GParted

## Стратегии разбиения на разделы

*   "Всё в одном"
*   Отдельный раздел /boot
*   Отдельный раздел /home
*   Отдельный раздел /var
*   Отдельный раздел /usr

## Важные моменты

*   Размеры разделов
*   Файловые системы
*   LVM

## Creating new partitions

## Resizing partitions

## Content from BG

**Важно:** Операции над разделами жёсткого диска могут привести к потере данных. Настоятельно рекомендуем Вам создавать резервные копии важной информации.

**Важно:** Нажатие кнопки Cancel, в меню подготовки жёсткого диска, не отменит выбранные операции - смотри [FS#19805](https://bugs.archlinux.org/task/19805). Если вам необходимо прервать установку в этом месте, нажмите <Control>+C, чтобы полностью и немедленно покинуть установщик.

**Примечание:** Разбиение жесткого диска, при желании, можно провести до установки Archlinux, например используя [GParted](http://gparted.sourceforge.net/download.php) или другой подобный инструмент. Если диск уже был разбит до установки, то начните с [Set Filesystem Mountpoints](#Set_Filesystem_Mountpoints)

Посмотреть на текущую таблицу разделов можно с помощью программы `/sbin/fdisk` с ключом `-l` (маленькая L).

Откройте другую виртуальную консоль (<ALT>+F3) и введите:

```
# fdisk -l

```

Отметьте для себя все диски/разделы, которые вы будете использовать при установке Arch.

Вернитесь назад в консоль, где запущен скрипт установки <ALT>+F1

Выберете пункт "Prepare Hard Drive".

*   Вариант 1: Auto Prepare

Этот пункт поделит диск со следующими параметрами:

*   Загрузочный раздел с ФС ext2; точка монтирования: /boot; размер по умолчанию: 32MB. *Вам будет предложено изменить размер по своему усмотрению.*
*   Раздел подкачки swap, размер по умолчанию: 256MB. *Вам будет предложено изменить размер по своему усмотрению.*
*   Отдельные корневой(/) и /home разделы, (размеры тоже можно указать вручную). Возможные файловые системы: ext2, ext3, ext4, reiserfs, xfs and jfs, однако, обратите внимание, что при выборе опции Auto Prepare, файловые системы */ и /home будут одного типа*.

Будьте внимательны, опция Auto-prepare полностью сотрёт выбранный жёсткий диск. Внимательно прочитайте <font color="red">предупреждение</font>, предоставленное установщиком, и убедитесь,что действия производятся над нужным разделом.

*   Вариант 2: **(Рекомендуемый)** Partition Hard Drives (with cfdisk)

Эта опция предоставит наиболее надёжный и настраиваемый способ разбивки, отвечающий вашим персональным нуждам.

*Здесь более продвинутые пользователи GNU/Linux, хорошо знакомые с ручной разбивкой диска, могут сразу перейти к разделу **[D: Select Packages](#D:_Select_Packages)**.*

**Примечание:** Если вы устанавливаете систему на USB flash носитель, смотрите "[Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")".

#### Разметка жестких дисков

##### Информация о разделах

Разметка жесткого диска определяет особые области (разделы) на диске, каждая из которых выглядит и ведет себя как отдельный диск и на которых файловая система может быть создана (отформатирована).

*   Существуют 3 типа разделов диска:

1.  Primary (Первичный)
2.  Extended (Расширенный)
3.  Logical (Логический)

**Первичные** разделы могут быть загрузочными, их число ограничено 4-мя на диск или raid-массив. Если схема разбиения требует больше 4-х разделов, то требуется использование **расширенного** раздела, содержащего **логические** разделы.

Расширенные разделы не используются сами по себе; они представляют собой "контейнер" для логических разделов. Если требуется, жесткий диск может содержать один расширенный раздел, разделенный на логические разделы.

При разбиении диска можно наблюдать данную схему нумерации путем создания первичных разделов sda1, sda2, sda3 и следующего за ними расширенного раздела sda4, а затем созданных логических разделов внутри расширенного раздела sda5, sda6, и так далее.

##### Раздел Swap

Swap раздел - это место на жестком диске, где постоянно хранится виртуальная оперативная память, позволяющее ядру с легкостью использовать жесткий диск для хранения данных, которые не подходят для физической ОЗУ.

Исторически, основным правилом для установления размера раздела подкачки был умноженный на 2 размер физической ОЗУ. Со временем компьютеры стали оснащаться памятью большей емкостью и это правило перестало применяться. Это правило применяется в основном для компьютеров с ОЗУ до 512MB. Если же на вашем компьютере больше 1024MB ОЗУ, то про создание раздела подкачки можно и забыть, ведь всегда можно создать [swap file](/index.php/HOW_TO:_Create_swap_file "HOW TO: Create swap file") (с тех пор, как такая возможность появилась). В этом примере будет использоваться раздел подкачки размером в 1GB.

**Примечание:** Для использования гибернации, раздел подкачки должен быть по крайней мере **равен** размеру ОЗУ. Некоторые пользователи Arch даже рекомендуют делать размер раздела на 10-15% больше ОЗУ для предотвращения возможности появления плохих секторов.

##### Схема разметки

Разметка диска сугубо индивидуальна. Каждый пользователь делает выбор исходя из своих требований и возможностей железа. Если вам необходимо пользоваться и Windows, и Arch на одном компьютере, то пройдите в специальный раздел [Двойная загрузка: Windows и Arch](/index.php/Windows_and_Arch_Dual_Boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.94.D0.B2.D0.BE.D0.B9.D0.BD.D0.B0.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0:_Windows_.D0.B8_Arch "Windows and Arch Dual Boot (Русский)").

Файловые системы, претендующие на разбиение по разделам:

**/** (root) *Корневая файловая система (корень, рут) является первичной файловой системой и главенствующей, от которой происходят остальные. Все файлы и каталоги принадлежат корневому каталогу "/", даже если физически они расположены на разных устройствах. Содержимое корня должно загружаться, откатываться, восстанавливаться и/или исправляться. Поэтому не все каталоги в корневой директории могут быть отдельными разделами. Подробнее в предупреждении ниже.*

**/boot** *Этот каталог содержит ядро, ramdisk, конфигурационные файлы загрузки и т.д. /boot также хранит информацию, использованную до загрузки пользовательских программ. Он может включать главную загрузочную запись. /boot важен для загрузки системы и, если необходимо, может быть на отдельном разделе.*

**/home** *Хранит подкаталоги, названные в соответствии с пользователями, где хранятся личные данные и персональные настройки для приложений.*

**/usr** *Если "/" находится вверху иерархии, то второе место по праву занимает каталог /usr, который хранит большинство общедоступных утилит и программ. /usr содержит общую (доступную всем системным пользователям) информацию в режиме только для чтения. Это означает, что /usr доступен с разных хостов, но запрещен для записи, за исключением системных обновлений и апгрейдов. Любая персонифицированная, изменяемая информация должна содержаться в другом месте.*

**/tmp** *каталог, созданный для хранения временных файлов программ. Пример: файлы с расширением '.lck', которые используются для предотвращения размножения процессов, пока выполняется задача(выполняет роль семафора). Каталог /tmp чаще всего очищается при каждой перезагрузке и не предназначен для постоянного хранения данных и других подобных задач.*

**/var** *содержит самую различную информацию; файлы в процессе обработки, всевозможные логи(журналирование приложений), кэш pacman, ABS дерево, и т.д. /var, в свою очередь, осуществляет возможность оставаться /usr защищенным от записи. Все, что исторически попало в /usr и отвечает за текущую работу системы (в отличии от установки и работы программ) должно находиться в /var*

**Важно:** Помимо /boot, каталоги важные для загрузки: '***/bin', '/etc', '/lib', and '/sbin'. Разница в том, что они не могут быть в разных разделах с корневым каталогом /.***

***Здесь перечислены несколько преимуществ разбиения файловой системы на разделы, по сравнению с единственным разделом***:

*   Безопасность: Каждая файловая система может быть сконфигурирована в /etc/fstab как 'nosuid', 'nodev', 'noexec', 'readonly', и т.д.
*   Стабильность: Пользователь или программы способны захламить файловую системы, вызвать сбои в работе приложений. Но важные для работы системы модули и утилиты всегда будут работать, так как отделены на другом разделе.
*   Скорость: Часто используемая для записи файловая система может стать фрагментированной(лучший способ избегать этого - следить за наполнением раздела и не допускать наполнения "до упора"). Разделы не влияют друг на друга, и один из разделов может безболезненно быть дефрагментирован.
*   Целостность: Если одна файловая система испортится, остальные будут полностью функциональны.
*   Гибкость: Обмен данными между независимыми файловыми системами более целесообразен. Тип и характеристики каждой файловой системы могут отличаться в зависимости от характера и использования данных.

В следующем примере мы рассмотрим разбиение на корень /, /var, /home, и swap разделы.

**Примечание:** /var содержит много маленьких файлов. Учитывайте это при выборе типа файловой системы, если уделяете /var отдельный раздел

##### Насколько большими должны быть мои разделы?

Лучший ответ на этот вопрос для каждого свой. Вы просто можете создать **корневой и swap разделы или вообще только корневой** или последуйте следующим примерам, поддерживая тем самым некий условный стандарт:

*   Корневая файловая система (/) в данном примере будет содержать /usr, который может быть достаточно ёмким, в зависимости от установленного софта. 15-20 Гбайт зачастую достаточно обычному пользователю.

*   /var файловая система содержит много разной информации, [ABS](/index.php/ABS "ABS") дерево и кэш pacman. Сохранение закэшированных пакетов очень удобно и полезно; при необходимости можно будет сделать откат или даунгрейд пакета. /var имеет тенденцию к росту. Кэш pacman разрастается за долгий период времени, но не приносит проблем, если его иногда чистить. Если вы используете SSD, возможно вы захотите разместить /var на HDD и оставить / и /home разделы на SSD, чтобы избежать частых чтения/запись. 8-12 Гбайт на настольном ПК должно хватать обычному пользователю, если не используется большое количество 'тяжелых' приложений. Сервера склонны год от года увеличивать объем /var.

*   /home - это каталог, где содержится мультимедия, пользовательские настройки и т.д. На компьютерах зачастую /home становится самым объемным.. Помните, что при переустановке Arch /home остается нетронутым.

*   Добавление по 25% к размерам разделов обеспечат вам комфорт и спокойствие.

***К делу, пример: ~15Гбайт корневой (/) раздел, ~10Гбайт /var, 1Гбайт swap, и /home с местом для непредвиденных ситуаций.***

##### Create Partition:cfdisk

Start by creating the primary partition that will contain the **root**, (/) filesystem.

Choose **N**ew -> Primary and enter the desired size for root (/). Put the partition at the beginning of the disk.

Also choose the **T**ype by designating it as '83 Linux'. The created / partition shall appear as sda1 in our example.

Now create a primary partition for /var, designating it as **T**ype 83 Linux. The created /var partition shall appear as sda2

Next, create a partition for swap. Select an appropriate size and specify the **T**ype as 82 (Linux swap / Solaris). The created swap partition shall appear as sda3.

Lastly, create a partition for your /home directory. Choose another primary partition and set the desired size.

Likewise, select the **T**ype as 83 Linux. The created /home partition shall appear as sda4.

Example:

```
Name    Flags     Part Type    FS Type           [Label]         Size (MB)
-------------------------------------------------------------------------
sda1               Primary     Linux                             15440 #root
sda2               Primary     Linux                             10256 #/var
sda3               Primary     Linux swap / Solaris              1024  #swap
sda4               Primary     Linux                             140480 #/home

```

Choose **W**rite and type '**yes'**. Beware that this operation may destroy data on your disk. Choose **Q**uit to leave the partitioner. Choose Done to leave this menu and continue with "Set Filesystem Mountpoints".

**Примечание:** Since the latest developments of the Linux kernel which include the libata and PATA modules, all IDE, SATA and SCSI drives have adopted the sd*x* naming scheme. This is perfectly normal and should not be a concern.

#### Set Filesystem Mountpoints

Specify each partition and corresponding mountpoint to your requirements. (Recall that partitions end in a number. Therefore, **sda** is not itself a partition, but rather, signifies an entire drive)

##### Filesystem Types

Again, a filesystem type is a very subjective matter which comes down to personal preference. Each has its own advantages, disadvantages, and unique idiosyncrasies. Here is a very brief overview of supported filesystems:

1\. **ext2** *Second Extended Filesystem*- Old, reliable GNU/Linux filesystem. Very stable, but *without journaling support*. May be inconvenient for root (/) and /home, due to very long fsck's. *An ext2 filesystem can easily be converted to ext3.* Generally regarded as a good choice for /boot/.

2\. **ext3** *Third Extended Filesystem*- Essentially the ext2 system, but with journaling support. ext3 is backward compatible with ext2\. Extremely stable, mature, and by far the most widely used, supported and developed GNU/Linux FS.

**High Performance Filesystems:**

3\. **ext4** *Fourth Extended Filesystem*- Backward compatible with ext2 and ext3\. Introduces support for volumes with sizes up to 1 exabyte and files with sizes up to 16 terabytes. Increases the 32,000 subdirectory limit in ext3 to 64,000\. Offers online defragmentation ability.

4\. **ReiserFS** (V3)- Hans Reiser's high-performance journaling FS uses a very interesting method of data throughput based on an unconventional and creative algorithm. ReiserFS is touted as very fast, especially when dealing with many small files. ReiserFS is fast at formatting, yet comparatively slow at mounting. Quite mature and stable. ReiserFS is not actively developed at this time (Reiser4 is the new Reiser filesystem). Generally regarded as a good choice for /var/.

5\. **JFS** - IBM's **J**ournaled **F**ile**S**ystem- The first filesystem to offer journaling. JFS had many years of use in the IBM AIX® OS before being ported to GNU/Linux. JFS currently uses the least CPU resources of any GNU/Linux filesystem. Very fast at formatting, mounting and fsck's, and very good all-around performance, especially in conjunction with the deadline I/O scheduler. (See [JFS](/index.php/JFS "JFS").) Not as widely supported as ext or ReiserFS, but very mature and stable.

6\. **XFS** - Another early journaling filesystem originally developed by Silicon Graphics for the IRIX OS and ported to GNU/Linux. XFS offers very fast throughput on large files and large filesystems. Very fast at formatting and mounting. Generally benchmarked as slower with many small files, in comparison to other filesystems. XFS is very mature and offers online defragmentation ability.

*   JFS and XFS filesystems cannot be *shrunk* by disk utilities (such as gparted or parted magic)

##### A note on Journaling

All above filesystems, except ext2, utilize [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling file systems are fault-resilient file systems that use a journal to log changes before they are committed to the file system to avoid metadata corruption in the event of a crash. Note that not all journaling techniques are alike; specifically, only ext3 and ext4 offer *data-mode journaling*, (though, not by default), which journals *both* data *and* meta-data (but with a significant speed penalty). The others only offer *ordered-mode journaling*, which journals meta-data only. While all will return your filesystem to a valid state after recovering from a crash, *data-mode journaling* offers the greatest protection against file system corruption and data loss but can suffer from performance degradation, as all data is written twice (first to the journal, then to the disk). Depending upon how important your data is, this may be a consideration in choosing your filesystem type.

***Moving on...***

Choose and create the filesystem (format the partition) for / by selecting **yes**. You will now be prompted to add any additional partitions. In our example, sda2 and sda4 remain. For sda2, choose a filesystem type and mount it as /var. Finally, choose the filesystem type for sda4, and mount it as /home.

**Примечание:** If you have not created and do not need a separate /boot partition, you may safely ignore the warning that it does not exist.
Return to the main menu.