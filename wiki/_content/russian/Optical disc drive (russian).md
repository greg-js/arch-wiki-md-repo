Ссылки по теме

*   [Кодеки](/index.php/%D0%9A%D0%BE%D0%B4%D0%B5%D0%BA%D0%B8 "Кодеки")
*   [MPlayer (Русский)](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)")
*   [dvdbackup](/index.php/Dvdbackup "Dvdbackup")
*   [MEncoder](/index.php/MEncoder "MEncoder")
*   [BluRay](/index.php/BluRay "BluRay")

Из [Википедии](https://en.wikipedia.org/wiki/ru:%D0%9E%D0%BF%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D0%BF%D1%80%D0%B8%D0%B2%D0%BE%D0%B4 "wikipedia:ru:Оптический привод"):

	*"Опти́ческий при́вод — устройство, имеющее механическую составляющую, управляемую электронной схемой и предназначенное для считывания и (в большинстве современных моделей) записи информации с оптических носителей информации в виде пластикового диска с отверстием в центре (компакт-диск, DVD и т. д.); процесс считывания/записи информации с диска осуществляется при помощи лазера."*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Запись](#Запись)
    *   [1.1 Установка утилит для записи](#Установка_утилит_для_записи)
    *   [1.2 Создание ISO-образа из существующих файлов на жёстком диске](#Создание_ISO-образа_из_существующих_файлов_на_жёстком_диске)
        *   [1.2.1 Основные опции](#Основные_опции)
        *   [1.2.2 graft-points](#graft-points)
    *   [1.3 Монтирование ISO-образа](#Монтирование_ISO-образа)
    *   [1.4 Конвертирование img/ccd в ISO-образ](#Конвертирование_img/ccd_в_ISO-образ)
    *   [1.5 Определение название оптического привода](#Определение_название_оптического_привода)
    *   [1.6 Определение метки тома CD или DVD](#Определение_метки_тома_CD_или_DVD)
    *   [1.7 Снятие ISO образа с CD, DVD или BD](#Снятие_ISO_образа_с_CD,_DVD_или_BD)
    *   [1.8 Стирание CD-RW и DVD-RW](#Стирание_CD-RW_и_DVD-RW)
    *   [1.9 Прожиг ISO-образа на CD, DVD или BD](#Прожиг_ISO-образа_на_CD,_DVD_или_BD)
    *   [1.10 Проверка записанного диска](#Проверка_записанного_диска)
    *   [1.11 ISO 9660 и запись "на лету"](#ISO_9660_и_запись_"на_лету")
    *   [1.12 Мультисессия](#Мультисессия)
        *   [1.12.1 Мультисессия с помощью wodim](#Мультисессия_с_помощью_wodim)
        *   [1.12.2 Мультисессия с помощью growisofs](#Мультисессия_с_помощью_growisofs)
        *   [1.12.3 Мультисессия с помощью xorriso](#Мультисессия_с_помощью_xorriso)
    *   [1.13 BD Defect Management](#BD_Defect_Management)
    *   [1.14 Запись Audio CD](#Запись_Audio_CD)
    *   [1.15 Запись BIN/CUE](#Запись_BIN/CUE)
        *   [1.15.1 TOC/CUE/BIN для дисков со смешанным содержимым](#TOC/CUE/BIN_для_дисков_со_смешанным_содержимым)
    *   [1.16 Проблемы с записью](#Проблемы_с_записью)
    *   [1.17 Запись CD/DVD/BD с помощью графических программ](#Запись_CD/DVD/BD_с_помощью_графических_программ)
        *   [1.17.1 Свободные графические программы](#Свободные_графические_программы)
        *   [1.17.2 Nero Linux](#Nero_Linux)
*   [2 Вопроизведение мультимедиа](#Вопроизведение_мультимедиа)
    *   [2.1 CD](#CD)
    *   [2.2 DVD](#DVD)
*   [3 Риппинг](#Риппинг)
    *   [3.1 CD](#CD_2)
    *   [3.2 DVD](#DVD_2)
        *   [3.2.1 dvd::rip](#dvd::rip)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 Ошибка локали K3b](#Ошибка_локали_K3b)
    *   [4.2 Brasero не может найти пустые диски](#Brasero_не_может_найти_пустые_диски)
    *   [4.3 Brasero не может нормализовать аудио CD](#Brasero_не_может_нормализовать_аудио_CD)
    *   [4.4 VLC: Ошибка "... не может открыть диск /dev/dvd"](#VLC:_Ошибка_"..._не_может_открыть_диск_/dev/dvd")
    *   [4.5 DVD-привод шумит](#DVD-привод_шумит)
    *   [4.6 Воспроизведение не работает на новом компьютере (новом DVD-приводе)](#Воспроизведение_не_работает_на_новом_компьютере_(новом_DVD-приводе))
    *   [4.7 Ни одна из вышеперечисленных программ не может рипнуть/кодировать DVD на мой жёсткий диск!](#Ни_одна_из_вышеперечисленных_программ_не_может_рипнуть/кодировать_DVD_на_мой_жёсткий_диск!)
    *   [4.8 Лог графической оболочки говорит о проблемах с бекендом](#Лог_графической_оболочки_говорит_о_проблемах_с_бекендом)
        *   [4.8.1 Особый случай: medium error / write error](#Особый_случай:_medium_error_/_write_error)
    *   [4.9 AHCI](#AHCI)
*   [5 Смотрите также](#Смотрите_также)

## Запись

**Важно:** Качество оптических приводов и самих дисков очень сильно варьируется. Главным образом, для получения надёжной записи рекомендуется производить ее на низкой скорости. Если появляются странные проблемы с записанными вами компакт-дисками, попробуйте производить запись на самой низкой скорости, которую поддерживает ваш привод.

Процесс прожига (записи данных на диск) состоит из получения файла образа и последующей его записи на оптический носитель. В принципе, образом может быть любой файл данных. Если вы хотите смонтировать записанный диск, то, как правило, следует указывать файловую систему ISO 9660\. Audio CD и мультимедийные CD обычно прожигаются из файла *.bin* с использованием файла *.toc* или *.cue*, который содержит информацию о расположении треков.

### Установка утилит для записи

Если вы хотите использовать программы с графическим интерфейсом, перейдите к разделу [#Запись CD/DVD/BD с помощью графических программ](#Запись_CD/DVD/BD_с_помощью_графических_программ).

Работа с перечисленными здесь утилитами происходит из командной строки. Они являются бэкендами для большинства свободных графических программ для работы с CD, DVD и BD. Этими утилитами может быть полезно пользоваться напрямую, если у вас возникают проблемы с записью при помощи графической программы либо вы хотите автоматизировать запись с помощью скриптов.

Вам нужна как минимум одна программа для создания образов файловой системы и одна программа, которая может записывать данные на нужный вам тип носителя.

Доступные программы для создания образа ISO 9660:

*   *genisoimage* из пакета [cdrkit](https://www.archlinux.org/packages/?name=cdrkit)
*   *mkisofs* из пакета [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   *xorriso* и *xorrisofs* из пакета [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

Как правило, используется *genisoimage*.

Доступные программы для записи на носители:

*   *cdrdao* из пакета [cdrdao](https://www.archlinux.org/packages/?name=cdrdao) (только для CD и только TOC/CUE/BIN)
*   *cdrecord* из пакета [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   *cdrskin* из пакета [libburn](https://www.archlinux.org/packages/?name=libburn)
*   *growisofs* из пакета [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) (только для DVD и BD)
*   *wodim* из пакета [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) (только для CD, для DVD устарела)
*   *xorriso* и *xorrecord* из пакета [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

Обычно используют *wodim* для CD и *growisofs* для DVD и Blu-ray дисков. Как обойти баг *growisofs* с BD-R смотрите ниже. Для записи TOC/CUE/BIN файлов на CD, установите [cdrdao](https://www.archlinux.org/packages/?name=cdrdao).

Свободные графические программы для записи CD, DVD или BD используют как минимум один из перечисленных выше пакетов.

Программы 'mkisofs *и* xorrisofs *поддерживают опции* genisoimage*, описанные в этой статье.*

Программы *cdrecord* и *cdrskin* поддерживают описанные опции *wodim*; *xorrecord* также поддерживает их за исключением тех, которые предназначены для Audio CD.

**Примечание:**

*   Файлы, устанавливаемые пакетами [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) и [cdrtools](https://www.archlinux.org/packages/?name=cdrtools) конфликтуют. Устанавливайте только один из пакетов.
*   Если вы хотите установить [cdrtools](https://en.wikipedia.org/wiki/ru:Cdrtools и установили его напрямую с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") — фронтенды pacman могут решить установить cdrkit вместо него.

### Создание ISO-образа из существующих файлов на жёстком диске

Чтобы упростить создание ISO-образа, скопируйте все файлы для записи в один каталог, например `./for_iso`.

Затем сгенерируйте образ с *genisoimage*:

```
$ genisoimage -V "*ARCHIVE_2013_07_27*" -J -r -o *isoimage.iso* *./for_iso*

```

Каждая из указанных опций описана в следующих разделах.

#### Основные опции

	`-V`

	Задаёт название файловой системы, которое ей будет присвоено. Спецификации стандарта ISO 9660 накладывают ограничения на длину строки в 32 символа, а также ограничивают набор разрешённых символов следующими: от "A" до "Z", от "0" до "9" и "_". Эта метка может потом отображаться потом как точка монтирования, если носитель был смонтирован автоматически.

	`-J`

	Включает расширение [Joliet](https://en.wikipedia.org/wiki/ru:Joliet "wikipedia:ru:Joliet"), которое создает специальную таблицу в образе для хранения имен файлов в Unicode (до 64 символов UTF-16).

	`-joliet-long`

	Увеличивает длину имен файлов с 64 до 103 знаков в Joilet-таблице, однако не соответствует спецификациям Joliet и не везде поддерживается.

	`-r`

	Включает расширение [Rock Ridge](https://en.wikipedia.org/wiki/ru:Rock_Ridge "wikipedia:ru:Rock Ridge"), которое добавляет совместимость с файловыми системами POSIX, включая длинные 255-символьные имена файлов и поддержку прав доступа.

	`-o`

	Имя выходного файла образа.

#### graft-points

Также вы можете указать для *genisoimage* сразу несколько файлов и каталогов, которые будут добавлены в образ:

```
$ genisoimage -V "*BACKUP_2013_07_27*" -J -r -o *backup_2013_07_27.iso* \
  -graft-points \
  */photos=/home/user/photos \*
        /mail=/home/user/mail \
        /photos/holidays=/home/user/holidays/photos

```

	`-graft-points`

	Позволяет задавать *определения путей*, которые состоят из целевого адреса на файловой системе ISO (например, `/photos`) и адреса источника на жёстком диске (например `/home/user/photos`). Эти адреса разделены символом "=".

В этом примере, содержимое каталогов `/home/user/photos`, `/home/user/mail` и `/home/user/holidays/photos` будет помещено в каталоги `/photos`, `/mail` и `/photos/holidays` на ISO образе, соответственно.

Программы *mkisofs* и *xorrisofs* принимают такие же опции. Для создания резервных копий важных данных рекомендуется использовать *xorrisofs* с опцией `--for_backup`, которая создаст список контроля доступа и посчитает хеш-суммы MD5 для каждого файла с данными.

О дополнительных возможностях программ вы можете узнать из их руководств:

*   [genisoimage](http://linux.die.net/man/1/genisoimage)
*   [mkisofs](http://cdrtools.sourceforge.net/private/man/cdrecord/index.html)
*   [xorrisofs](https://www.gnu.org/software/xorriso/man_1_xorrisofs.html)

### Монтирование ISO-образа

Вы можете смонтировать ISO-образ, чтобы просмотреть его содержимое. Первым делом убедитесь, что модуль `loop` загружен ядром:

```
# modprobe loop

```

Теперь, чтобы смонтировать образ:

```
# mount -t iso9660 -o ro,loop=/dev/loop0 */путь/к/файлу.iso* */точка/монтирования*

```

После просмотра содержимого не забудьте размонтировать образ:

```
# umount /cdrom

```

Если вы хотите смонтировать образ от имени обычного пользователя, смотрите [FuseISO](/index.php/FuseISO "FuseISO").

### Конвертирование img/ccd в ISO-образ

Чтобы сконвертировать образ `img`/`ccd`, воспользуйтесь утилитой [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso):

```
$ ccd2iso *~/image.img* *~/image.iso*

```

### Определение название оптического привода

В примерах из этого раздела предполагается, что ваше записывающее устройство называется `/dev/sr0`.

Проверьте оптический привод командой

```
$ wodim dev=*/dev/sr0* -checkdrive

```

которая отобразит производителя (поле `Vendor_info`) и модель (`Identification`) вашего привода.

Если привод не найден, проверьте, существуют ли какие-либо устройства `/dev/sr*` и предоставлены ли ими права на чтение/запись (`wr-`) вам или вашей группе. Если вы не нашли подходящих устройств `/dev/sr*`, попробуйте выполнить [load](/index.php/Kernel_modules "Kernel modules") module `sr_mod` manually.

### Определение метки тома CD или DVD

Если вы хотите получить название/метку носителя, воспользуйтесь *dd*:

```
$ dd if=*/dev/sr0* bs=1 skip=32808 count=32

```

### Снятие ISO образа с CD, DVD или BD

Следует определить размер файловой системы ISO перед тем, как копировать её на жёсткий диск. Большинство типов накопителей предоставляют больше данных, чем на них было записано во время самого последнего прожига.

Чтобы посчитать реальное количество блоков, воспользуйтесь программой *isosize* из пакета [util-linux](https://www.archlinux.org/packages/?name=util-linux):

```
$ blocks=$(isosize -d 2048 */dev/sr0*)

```

Проверьте, выглядит ли полученное число блоков правдоподобно:

 `$ echo "That would be $(expr $blocks / 512) MB"` 
```
That would be 589 MB

```

Затем скопируйте полученное количество данных с носителя на жёсткий диск:

```
$ dd if=*/dev/sr0* of=*isoimage.iso* bs=2048 count=$blocks

```

Не указывайте параметр `count=$blocks`, если вы не определяли количество блоков. Вероятно, файл образа получится больше, чем необходимо на самом деле. Тем не менее, полученный файл можно будет смонтировать. Он всё ещё будет помещаться на носителе такого же типа, что и исходный носитель, с которого считывался образ.

Если исходный носитель был загрузочным, то созданный образ также будет загрузочным. Вы можете использовать его как виртуальный диск для виртуальной машины или прожечь на оптический носитель, который станет загрузочным.

### Стирание CD-RW и DVD-RW

Перед тем, как записать новую информацию на уже использованный CD-RW, необходимо стереть с него старую. Это можно выполнить командой

```
$ wodim -v dev=*/dev/sr0* blank=fast

```

Есть две опции для стирания данных: `blank=fast` (полная очистка) и `blank=full` (быстрая очистка). Полная очистка происходит во много раз медленнее, чем быстрая, однако использование быстрой лишает возможности мультисессионной записи на диск и записи поточных данных, длина которых неизвестна заранее (например, видео с камеры). Также имейте ввиду, что при быстрой очистке ваши данные не уничтожаются физически, и могут быть восстановлены посторонними лицами.

Вы также можете использовать другие программы:

```
$ cdrecord -v dev=*/dev/sr0* blank=all
$ cdrskin -v dev=*/dev/sr0* blank=all
$ xorriso -outdev */dev/sr0* -blank as_needed

```

Для стирания DVD-RW вы можете использовать утилиту *dvd+rw-format* из пакета [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools):

```
$ dvd+rw-format -blank=fast */dev/sr0*

```

Вы также можете использовать другие программы:

```
$ cdrskin -v dev=*/dev/sr0* blank=format_overwrite
$ xorriso -outdev */dev/sr0* -format as_needed

```

Отформатированный DVD+RW (обратите внимание на `+`!) носитель может быть перезаписан без такой процедуры стирания. Поэтому необходимо лишь разово выполнить первичное форматирование командой:

```
$ dvd+rw-format -force */dev/sr0*

```

Все другие типы носителей являются записываемыми либо только один раз (CD-R, DVD-R, DVD+R, BD-R) либо перезаписываемыми без необходимости стирания (DVD-RAM, BD-RE).

### Прожиг ISO-образа на CD, DVD или BD

Для записи подготовленного ISO-образа `isoimage.iso` на оптический носитель, используйте одну из указанных ниже команд.

Для CD выполните:

```
$ wodim -v -sao dev=*/dev/sr0* *isoimage.iso*

```

и в случае DVD или BD:

```
$ growisofs -dvd-compat -Z */dev/sr0*=*isoimage.iso*

```

Программы *cdrecord*, *cdrskin* и *xorrecord* могут быть использованы со всеми видами носителей с опциями, показанными на примере *wodim*.

**Примечание:**

*   Убедитесь в том, что носитель не был смонтирован перед тем, как начнёте писать на него. Монтирование могло произойти автоматически если носитель содержит файловую систему. В лучшем случае это не даст записывающим программам использовать устройство прожига. В худшем — произойдут ошибки записи, потому что операции чтения будут мешать приводу.

Поэтому, если вы сомневаетесь, выполните:

```
# umount /dev/sr0

```

*   В программе *growisofs* есть небольшая ошибка, касающаяся пустых BD-R носителей. Она выдаёт сообщение об ошибке после того, как прожиг завершён. Из-за этого такие программы, как *k3b* думают, что весь процесс прожига был неудачным.

Чтобы исправить это, либо

*   *   отформатируйте пустой BD-R с помощью `dvd+rw-format */dev/sr0*` перед тем как с ним будет работать *growisofs*
    *   либо используйте опцию *growisofs* `-use-the-force-luke=spare:none`

### Проверка записанного диска

Вы можете проверить, что диск был записан правильно и не содержит ошибок. Всегда вынимайте носитель и снова вставляйте его перед тем, как выполнять проверку. Это будет гарантировать, что для чтения не используется какой-либо кеш, предоставляемый ядром.

Сначала вычислите контрольную сумму MD5 исходного образа:

 `$ md5sum *isoimage.iso*` 
```
 e5643e18e05f5646046bb2e4236986d8 isoimage.iso

```

Затем вычислите контрольную сумму файловой системы на носителе. Несмотря на то, что при чтении некоторых типов носителей выдаётся абсолютно такое же количество данных, какое было передано записывающей программе, при чтении многие других типов носителей к этим данным добавляется находящийся дальше мусор. Поэтому вы должны ограничить чтение размером файла ISO образа, вычислив точное количество блоков для чтения:

```
$ blocks=$(expr $(du -b *isoimage.iso* | awk '{print $1}') / 2048)

```
 `$ dd if=''/dev/sr0'' bs=2048 count=$blocks | md5sum` 
```
 43992+0 records in
 43992+0 records out
 90095616 bytes (90 MB) copied, 0.359539 s, 251 MB/s
 e5643e18e05f5646046bb2e4236986d8  -

```

В обоих случаях должна быть вычислена та же самая контрольная сумма (в нашем примере `e5643e18e05f5646046bb2e4236986d8`). Если они не совпали, вероятно, вы также получите ошибку ввода/вывода при работе *dd*. При этом *dmesg* может сообщать об ошибках SCSI и номерах блоков, если вам это интересно.

### ISO 9660 и запись "на лету"

Не обязательно сохранять образ на жесткий диск перед тем, как производить запись на оптический носитель. Только очень старые CD приводы на очень старых компьютерах могли испытывать проблемы с записью из-за пустого буфера привода.

Если вы опустите опцию `-o` команды *genisoimage*, то выходной поток будет направлен в стандартный вывод. Он может быть перенаправлен на стандартный ввод записывающих программ.

```
$ genisoimage -V "*ARCHIVE_2013_07_27*" -J -r *./for_iso* | \
  wodim -v dev=*/dev/sr0* -waiti -

```

Опция `-waiti` здесь не обязательна. Она предотвращает `wodim` от начала записи на носитель до того, как *genisoimage* начнёт выводить данные. Это позволит *genisoimage* читать носитель, не мешая уже начатому процессу прожига. Смотрите следующий раздел про мультисессии.

В случае DVD и BD вы можете использовать *growisofs* для прожига "на лету", чтобы при этом она сама запускала *genisoimage*, следующим образом:

```
$ export MKISOFS="genisoimage"
$ growisofs -Z */dev/sr0* -V "*ARCHIVE_2013_07_27*" -r -J *./for_iso*

```

### Мультисессия

Файловая система ISO 9660 может использоваться также для мультисессионной записи, когда вы записываете какие-то данные на чистый носитель, а затем можете дозаписывать на него новые данные, начиная с адреса первого неиспользованного блока. Новое дерево каталогов перекрывает при этом старое, так, что новые файлы будут добавлены в уже существующие каталоги (вместе с теми, что там уже были), а файлы с полностью совпадающими именами будут считаться перезаписанными (при этом физически старые данные не стираются с диска, лишь становятся недоступными). Linux и многие другие операционные системы всегда монтируют самое новое дерево каталогов.

#### Мультисессия с помощью wodim

После записи CD-R и CD-RW все еще остаются дозаписываемыми, если при записи с *wodim* была использована опция `-multi`:

```
$ wodim -v -multi dev=*/dev/sr0* *isoimage.iso*

```

Чтобы выполнить новую сессию записи, необходимо запросить параметры сессии командой

```
$ m=$(wodim dev=*/dev/sr0* -msinfo)

```

С помощью этих параметров вы можете сгенерировать ISO-образ для новой сессии:

```
$ genisoimage -M /dev/sr0 -C "$m" \
   -V "*ARCHIVE_2013_07_28*" -J -r -o *session2.iso* *./more_for_iso*

```

Наконец, запишите полученный образ на носитель. Вы снова можете разрешить мультисессию опцией `-multi`:

```
$ wodim -v -multi dev=*/dev/sr0* *session2.iso*

```

Программы *cdrskin* и *xorrecord* также разрешают мультисессию для DVD-R, DVD+R, BD-R и неформатированных DVD-RW. Программа *cdrecord* разрешает мультисессию как минимум для DVD-R и DVD-RW. Разумеется, все они разрешают её с CD-R и CD-RW.

Большинство перезаписываемых носителей не записывают историю сессий, которая могла бы быть распознана монтирующим ядром. Но с помощью ISO 9660 можно добиться эффекта мультисессии даже на таких носителях.

*growisofs* и *xorriso* позволяют делать все то же самое без лишних действий.

#### Мультисессия с помощью growisofs

По умолчанию, *growisofs* использует *mkisofs* в качестве бекенда для генерирования ISO-образа, которой она передаёт большинство своих аргументов. Смотрите примеры с *genisoimage*, приведённые выше. Она запрещает опцию `-o` и объявляет устаревшей опцию `-C`. Вы можете сделать так, чтобы она работала с любой другой совместимой программой, установив переменную окружения `MKISOFS`:

```
$ export MKISOFS="genisoimage"
$ export MKISOFS="xorrisofs"

```

Для создания новой файловой системы на оптическом носителе используется опция `-Z`:

```
$ growisofs -Z */dev/sr0* -V "*ARCHIVE_2013_07_27*" -r -J *./for_iso*

```

Для добавления новых файлов в режиме мультисессии, запускайте программу с опцией `-M`:

```
$ growisofs -M */dev/sr0* -V "*ARCHIVE_2013_07_28*" -r -J *./more_for_iso*

```

Для получения дополнительной информации смотрите инструкцию по [growisofs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/growisofs.1), а также инструкции по *genisoimage*, *mkisofs* и *xorrisofs*.

#### Мультисессия с помощью xorriso

`xorriso` самостоятельно проверяет, пуст ли накопитель и доступна ли дозапись на него в режиме мультисессии. Если диск не подходит для дозаписи, его следует сначала очистить. Для этого используется опция `-blank as_needed`, при указании которой диск будет очищен только в случае необходимости:

```
$ xorriso -outdev */dev/sr0* -blank as_needed \
          -volid "*ARCHIVE_2013_07_27*" -joliet on -add *./for_iso* --

```

Если на диск уже были записаны данные, и дозапись возможна, *xorriso* добавит указанные файлы на диск в случае, если вместо `-outdev` указана опция `-dev`. Разумеется, здесь не надо давать команду `-blank`

```
$ xorriso -dev */dev/sr0* \
          -volid "*ARCHIVE_2013_07_28*" -joliet on -add *./more_for_iso* --

```

Для дополнительной информации смотрите [инструкцию](https://www.gnu.org/software/xorriso/man_1_xorriso.html) и особенно её [примеры](https://www.gnu.org/software/xorriso/man_1_xorriso.html#EXAMPLES)

### BD Defect Management

Обычно запись на носители BD-RE и форматированные BD-R производится с включенной функцией Defect Management (*управление дефектами*). При записи сразу же происходит чтение записанных блоков и их проверка. В случае несовпадения эти блоки записываются заново или перенаправляются в резервную область (*Spare Area*), где располагаются запасные блоки.

Эти проверки чтения снижают скорость записи более чем наполовину от номинальной скорости записи привода и BD-носителя, а иногда даже больше. Активное использование резервной области впоследствии приводит к большим задержкам во время чтения. Поэтому использование Defect Management не всегда бывает желательно.

*cdrecord* не форматирует BD-R и не умеет отключать Defect Management на носителях BD-RE media.

*growisofs* форматирует BD-R по умолчанию. Defect Management можно отключить с помощью опции `-use-the-force-luke=spare:none`. Однако, эта опция не работает с носителями BD-RE.

*cdrskin*, *xorriso* и *xorrecord* не форматируют BD-R по умолчанию. Они делают форматирование с помощью соответствующих опций `cdrskin blank=format_if_needed`, `xorriso -format as_needed`, `xorrecord blank=format_overwrite`. Эти три программы могут отключить Defect Management на BD-RE и на уже отформатированном BD-R с помощью опций `cdrskin stream_recording=on`, `xorriso -stream_recording on`, `xorrecord stream_recording=on`, соответственно.

### Запись Audio CD

Сохраните ваши аудиотреки в формате WAV, стерео 16 бит без сжатия. Чтобы переконвертировать MP3 в WAV, убедитесь, что пакет [lame](https://www.archlinux.org/packages/?name=lame) установлен, перейдите с помощью *cd* в директорию с вашими MP3-файлами и выполните:

```
$ for i in *.mp3; do lame --decode "$i" "$(basename "$i" .mp3)".wav; done

```

В том случае, если вы получите ошибку при попытке записи WAV файлов, сконвертированных с помощью LAME, попробуйте декодировать с помощью [mpg123](https://www.archlinux.org/packages/?name=mpg123):

```
$ for i in *.mp3; do mpg123 --rate 44100 --stereo --buffer 3072 --resync -w $(basename $i .mp3).wav $i; done

```

Переименуйте файлы таким образом, чтобы они шли в нужном порядке следования при отображении их по алфавиту, например `01.wav`, `02.wav`, `03.wav` и т.д. Используйте следующую команду чтобы имитировать запись WAV файлов в качестве аудио CD:

```
$ wodim **-dummy** -v -pad speed=1 dev=*/dev/sr0* -dao -swab *.wav

```

В случае, если вы обнаружите ошибки или пустые треки, как например:

```
Track 01: audio    0 MB (00:00.00) no preemp pad

```

попробуйте другой декодер (например *mpg123*) или используйте для записи *cdrecord* из пакета [cdrtools](https://www.archlinux.org/packages/?name=cdrtools).

Обратите внимание, что [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) также содержит команду *cdrecord*, но это всего лишь символическая ссылка на *wodim*. Если все в порядке, уберите флаг `dummy`, чтобы на самом деле начать запись.

Для проверки записанного Audio CD используйте [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)"):

```
$ mplayer cdda://

```

### Запись BIN/CUE

Чтобы записать образ BIN/CUE, выполните:

```
$ cdrdao write --device */dev/sr0* *image.cue*

```

#### TOC/CUE/BIN для дисков со смешанным содержимым

ISO-образы содержат только одну дорожку данных. Если вы хотите создать образ диска со смешанным содержимым (дорожка данных с несколькими аудиотреками), то вам нужно будет создать пару TOC/BIN:

```
$ cdrdao read-cd --read-raw --datafile *image.bin* --driver generic-mmc:0x20000 --device */dev/cdrom* *image.toc*

```

Некоторые программы умеют работать только с парой CUE/BIN; вы можете создать файл CUE с помощью *toc2cue* (часть пакета [cdrdao](https://www.archlinux.org/packages/?name=cdrdao)):

```
$ toc2cue *image.toc* *image.cue*

```

### Проблемы с записью

Если у вас возникают проблемы, вы можете обратиться за помощью к почтовой рассылке [cdwrite@other.debian.org](mailto:cdwrite@other.debian.org), либо написать на один из ящиков поддержки, которые обычно указываются внизу на man-странице программы.

Сообщите о том, какие команды вы использовали, тип носителя (CD-R, DVD+RW, ...), опишите, что вы хотели сделать и что получилось на самом деле. Возможно, вас попросят установить самую последнюю версию программы либо даже версию для разработчиков и сделать тестовые команды. Также ожидайте того, что ваш привод просто не любит определенные типы носителей.

### Запись CD/DVD/BD с помощью графических программ

Есть несколько программ, которые позволяют записывать CD в графическом режиме.

Смотрите [Wikipedia:Comparison of disc authoring software](https://en.wikipedia.org/wiki/Comparison_of_disc_authoring_software "wikipedia:Comparison of disc authoring software").

#### Свободные графические программы

*   **[AcetoneISO](https://en.wikipedia.org/wiki/ru:AcetoneISO "wikipedia:ru:AcetoneISO")** — Инструмент для работы с ISO типа "все в одном" (поддерживает образы BIN, MDF, NRG, IMG, DAA, DMG, CDI, B5I, BWI, PDI и ISO).

	[http://sourceforge.net/projects/acetoneiso](http://sourceforge.net/projects/acetoneiso) || [acetoneiso2](https://www.archlinux.org/packages/?name=acetoneiso2)

*   **BashBurn** — Легковесная графическая оболочка над утилитами записи CD/DVD.

	[http://bashburn.dose.se/](http://bashburn.dose.se/) || [bashburn](https://www.archlinux.org/packages/?name=bashburn)

*   **[Brasero](https://en.wikipedia.org/wiki/ru:Brasero "wikipedia:ru:Brasero")** — Приложение для записи дисков для рабочего стола GNOME, разработанное так, чтобы быть простым насколько это возможно. Часть пакета [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Brasero](https://wiki.gnome.org/Apps/Brasero) || [brasero](https://www.archlinux.org/packages/?name=brasero)

*   **cdw** — Фронтенд на ncurses над утилитами *cdrecord*, *mkisofs*, *growisofs*, *dvd+rw-mediainfo*, *dvd+rw-format* и *xorriso*.

	[http://cdw.sourceforge.net/](http://cdw.sourceforge.net/) || [cdw](https://aur.archlinux.org/packages/cdw/)

*   **[GnomeBaker](https://en.wikipedia.org/wiki/ru:GnomeBaker "wikipedia:ru:GnomeBaker")** — Полнофункциональное приложение для записи CD/DVD для рабочего стола [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")

	[http://gnomebaker.sourceforge.net/](http://gnomebaker.sourceforge.net/) || [gnomebaker](https://aur.archlinux.org/packages/gnomebaker/)

*   **Graveman** — Приложение GTK для записи CD/DVD. Оно требует указания используемых устройств при настройке.

	[http://graveman.tuxfamily.org/](http://graveman.tuxfamily.org/) || [graveman](https://aur.archlinux.org/packages/graveman/)

*   **[isomaster](https://en.wikipedia.org/wiki/ru:ISO_Master "wikipedia:ru:ISO Master")** — Редактор ISO-образов.

	[http://littlesvr.ca/isomaster](http://littlesvr.ca/isomaster) || [isomaster](https://aur.archlinux.org/packages/isomaster/)

*   **[K3b](https://en.wikipedia.org/wiki/ru:K3b "wikipedia:ru:K3b")** — Простое в использовании приложение на KDElibs для записи CD с богатым функционалом.

	[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **[X-CD-Roast](https://en.wikipedia.org/wiki/ru:X-CD-Roast "wikipedia:ru:X-CD-Roast")** — Легковесная графическая оболочка над *cdrtools* для записи CD и DVD.

	[http://www.xcdroast.org/](http://www.xcdroast.org/) || [xcdroast](https://aur.archlinux.org/packages/xcdroast/)

*   **Xfburn** — Простой фронтенд над библиотеками libburnia с поддержкой CD/DVD(-RW), ISO образов и BurnFree.

	[http://goodies.xfce.org/projects/applications/xfburn](http://goodies.xfce.org/projects/applications/xfburn) || [xfburn](https://www.archlinux.org/packages/?name=xfburn)

*   **xorriso-tcltk** — Графический фронтенд над утилитой *xorriso* для работы с ISO и записи CD/DVD/BD.

	[https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif](https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif) || [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

#### Nero Linux

Nero Linux — это коммерческая программа для записи от создателей Nero для Windows — Nero AG. Основным преимуществом Nero Linux считают её интерфейс, который похож на версию для Windows. Таким образом, пользователи, перешедшие с Windows считают ее простой в использовании. Теперь версия для Linux включает Nero Express (предоставляет интерфейс в виде мастера, который проводит пользователя через процесс записи CD и DVD шаг за шагом), к которому привыкли ещё в версии для Windows. Также в версии 4 добавилась поддержка Defect Management для Blu-ray дисков, интеграция Isolinux для создания загрузочного носителя и поддержка аудиоформатов Musepack и AIFF...

Nero Linux 4 продаётся за $19.99, также есть бесплатная пробная версия.

*   [Nero Linux 4](http://www.nero.com/enu/promo-linux.html)
*   [nerolinux](https://aur.archlinux.org/packages/nerolinux/) [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") пакет.

Nero Linux предоставляет следующие возможности:

*   Простой пользовательский интерфейс в виде мастера для записи дисков Nero Linux Express 4.
*   Полная поддержка записи на Blu-ray.
*   Поддержка записи Audio CD (CD-DA), ISO 9660 (поддерживается Joliet), CD-text, загрузочных дисков ISOLINUX, Мультисессионных дисков, DVD-Video и miniDVD, а также двухслойных DVD.
*   Продвинутая запись с помощью Nero Burning ROM и клиента командной строки.

**Примечание:** Необходимый модуль `sg` должен быть загружен автоматически, в противном случае смотрите [Модули ядра](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0 "Модули ядра") для информации о ручной настройке.

## Вопроизведение мультимедиа

### CD

Для прослушивания Audio CD [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [libcdio](https://www.archlinux.org/packages/?name=libcdio), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### DVD

[DVD](https://en.wikipedia.org/wiki/ru:DVD "wikipedia:ru:DVD") (Digital Versatile Disc или Digital Video Disc) — это оптический дисковый носитель, используемый для хранения видео и других данных.

Если вы хотите проиграть зашифрованный DVD, вы должны установить пакеты libdvd*:

*   [libdvdread](https://www.archlinux.org/packages/?name=libdvdread)
*   [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss)
*   [libdvdnav](https://www.archlinux.org/packages/?name=libdvdnav)

В дополнение к ним, вы должны установить какой-нибудь плеер. Популярными DVD-проигрывателями являются [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)"), [xine](https://en.wikipedia.org/wiki/ru:Xine "wikipedia:ru:Xine") и [VLC](/index.php/VLC "VLC"). Смотрите также список [видеоплееров](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9/%D0%9C%D1%83%D0%BB%D1%8C%D1%82%D0%B8%D0%BC%D0%B5%D0%B4%D0%B8%D0%B0#Видео_проигрыватели "Список приложений/Мультимедиа") и специальные инструкции для [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Воспроизведение_DVD_с_поддержкой_меню_навигации "MPlayer (Русский)").

## Риппинг

[Риппинг](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B8%D0%BF%D0%BF%D0%B8%D0%BD%D0%B3 "wikipedia:ru:Риппинг") — это процесс копирования аудио или видео на жёсткий диск, обычно со съёмных носителей или медиапотоков.

### CD

*   **[Abcde](https://en.wikipedia.org/wiki/ABCDE "wikipedia:ABCDE")** — Комплексная программа с интерфейсом командной строки для копирования Audio CD.

	[http://abcde.einval.com/](http://abcde.einval.com/) || [abcde](https://www.archlinux.org/packages/?name=abcde)

*   **[Asunder](https://en.wikipedia.org/wiki/Asunder "wikipedia:Asunder")** — Программа на GTK+ для риппинга CD.

	[http://littlesvr.ca/asunder/](http://littlesvr.ca/asunder/) || [asunder](https://www.archlinux.org/packages/?name=asunder)

*   **[cdparanoia](https://en.wikipedia.org/wiki/ru:cdparanoia "wikipedia:ru:cdparanoia")** — Программа Compact Disc Digital Audio (CDDA) Digital Audio Extraction (DAE).

	[http://xiph.org/paranoia/index.html](http://xiph.org/paranoia/index.html) || [cdparanoia](https://www.archlinux.org/packages/?name=cdparanoia)

*   **Gnac** — Аудиоконвертер для GNOME.

	[http://gnac.sourceforge.net/](http://gnac.sourceforge.net/) || [gnac](https://www.archlinux.org/packages/?name=gnac)

*   **Goobox** — CD плеер и риппер для GNOME.

	[https://people.gnome.org/~paobac/goobox/](https://people.gnome.org/~paobac/goobox/) || [goobox](https://www.archlinux.org/packages/?name=goobox)

*   **[Grip](https://en.wikipedia.org/wiki/ru:Grip "wikipedia:ru:Grip")** — Быстрый и лёгкий CD риппер внутри проекта GNOME, который похож на [Audiograbber](https://en.wikipedia.org/wiki/ru:Audiograbber "wikipedia:ru:Audiograbber").

	[http://sourceforge.net/projects/grip/](http://sourceforge.net/projects/grip/) || [grip](https://aur.archlinux.org/packages/grip/)

*   **KAudioCreator** — Программа для риппинга и кодирования Audio CD и кодирования файлов с диска.

	[http://kde-apps.org/content/show.php/KAudioCreator?content=107645](http://kde-apps.org/content/show.php/KAudioCreator?content=107645) || [kaudiocreator](https://www.archlinux.org/packages/?name=kaudiocreator)

*   **morituri** — CD риппер, которому точность важнее скорости.

	[http://thomas.apestaart.org/morituri/trac/](http://thomas.apestaart.org/morituri/trac/) || [morituri](https://www.archlinux.org/packages/?name=morituri)

*   **ripperX** — Программа на GTK+ для риппинга аудио и записи в MP3.

	[http://sourceforge.net/projects/ripperx/](http://sourceforge.net/projects/ripperx/) || [ripperx](https://aur.archlinux.org/packages/ripperx/)

*   **rubyripper** — Риппер аудиодисков, который выдаёт качественную запись путём многократного чтения, обнаружения и исправления различий.

	[http://code.google.com/p/rubyripper/](http://code.google.com/p/rubyripper/) || [rubyripper](https://aur.archlinux.org/packages/rubyripper/)

*   **[Sound Juicer](https://en.wikipedia.org/wiki/ru:Sound_Juicer "wikipedia:ru:Sound Juicer")** — CD риппер для GNOME.

	[http://burtonini.com/blog/computers/sound-juicer](http://burtonini.com/blog/computers/sound-juicer) || [sound-juicer](https://www.archlinux.org/packages/?name=sound-juicer)

*   **soundKonverter** — Фронтенд для нескольких аудиоконвертеров.

	[http://www.kde-apps.org/content/show.php?content=29024](http://www.kde-apps.org/content/show.php?content=29024) || [soundkonverter](https://www.archlinux.org/packages/?name=soundkonverter)

### DVD

Часто процесс риппинга DVD можно разбить на две подзадачи:

1.  **Извлечение данных** — копирование аудио- и/или видеоданных на жёсткий диск,
2.  [Транскодинг](https://en.wikipedia.org/wiki/Transcode "wikipedia:Transcode") — преобразование извлечённых данных в удобный для вас формат.

Некоторые утилиты выполняют обе задачи, а некоторые выполняют какую-либо одну из этих задач:

*   **dvd-vr** — Утилита, которая легко конвертирует VRO-файлы, извлечённые с [DVD-VR](https://en.wikipedia.org/wiki/DVD-VR "wikipedia:DVD-VR") и разбивает их на обычные VOB-файлы.

	[http://www.pixelbeat.org/programs/dvd-vr/](http://www.pixelbeat.org/programs/dvd-vr/) || [dvd-vr](https://aur.archlinux.org/packages/dvd-vr/)

*   **[dvdbackup](/index.php/Dvdbackup "Dvdbackup")** — Программа, извлекающая данные без перекодирования. Она полезна для создания *физических* копий зашифрованных DVD в сочетании с **libdvdcss**, а также при расшифровке видео другими утилитами, которые не умеют читать зашифрованные DVD.

	[http://dvdbackup.sourceforge.net/](http://dvdbackup.sourceforge.net/) || [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup)

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Самостоятельная и свободная программа для широковещательной трансляции аудио и видео через интернет для Linux/Unix, способная сделать прямой рип в любой формат (аудио/видео) с ISO образа DVD-Video: просто выберите входящий поток как ISO образ и заполните необходимые параметры. Она умеет микшировать, подрезать, раздёлять выбранные потоки, а также имеет многие другие функции.

	[http://ffmpeg.org/](http://ffmpeg.org/) || See [article](/index.php/FFmpeg#Package_installation "FFmpeg")

*   **HandBrake** — Многопоточный видео транскодер, который предоставляет как графический интерфейс, так и интерфейс командной строки и имеет много предустановленных настроек.

	[http://handbrake.fr/](http://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **Hybrid** — Мультиплатформенная графическая оболочка на Qt для многих других утилит, который может конвертировать практически любой входной поток в x264/Xvid/VP8 + ac3/ogg/mp3/aac/flac внутрь контейнера mp4/m2ts/mkv/webm/mov/avi, Blu-ray или структуру AVCHD.

	[http://www.selur.de/](http://www.selur.de/) || [hybrid-encoder](https://aur.archlinux.org/packages/hybrid-encoder/)

*   **[MEncoder](/index.php/MEncoder "MEncoder")** — Свободный видеодекодер для командной строки, кодирующая и фильтрующая программа, выпущенная под лицензией GNU GPL. Практически является родственником MPlayer и может конвертировать все форматы, которые понимает MPlayer во множество сжатых и несжатых форматов, используя различные кодеки. Программы-обёртки, такие как [h264enc](https://aur.archlinux.org/packages/h264enc/) и [undvd](https://aur.archlinux.org/packages/undvd/) могут предоставить более понятный интерфейс. Доступно много [графических оболочек](/index.php/MEncoder#GUI_frontends "MEncoder").

	[http://www.mplayerhq.hu/](http://www.mplayerhq.hu/) || [mencoder](https://www.archlinux.org/packages/?name=mencoder)

*   **Transcode** — Видео/DVD риппер и энкодер с интерфейсом командной строки.

	[http://tcforge.berlios.de/](http://tcforge.berlios.de/) || [transcode](https://www.archlinux.org/packages/?name=transcode)

#### dvd::rip

dvd::rip — это фронтенд для [transcode](https://www.archlinux.org/packages/?name=transcode), используемый для извлечения DVD на жёсткий диск и перекодировки или извлечения и перекодировки "на лету".

Следующие пакеты должны быть установлены:

*   [dvdrip](https://aur.archlinux.org/packages/dvdrip/): GTK фронтенд над [transcode](https://www.archlinux.org/packages/?name=transcode), который делает риппинг и кодирование
*   [libdv](https://www.archlinux.org/packages/?name=libdv): Программный кодек для DV видео
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): Видеокодек с открытым исходным кодом. Пригодится, если вы хотите кодировать рипнутые вами файлы в XviD, MPEG-4 (свободная альтернатива кодеку DivX)
*   [divx4linux](https://aur.archlinux.org/packages/divx4linux/): Если вы хотите кодировать рипнутые вами файлы в DivX
*   [subtitleripper](https://aur.archlinux.org/packages/subtitleripper/): Если вы хотите читать и обрабатывать субтитры

В основном, все настройки dvd::rip хорошо документированы и интуитивно понятны. Если вам понадобится помощь, смотрите [http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp](http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp).

Запись DVD — это просто вопрос выбора предпочитаемого кодека(ов), выбора нужных титров, и нажатие кнопки "Rip".

## Решение проблем

### Ошибка локали K3b

Если при запуске K3b появляется следующее сообщение об ошибке:

```
System locale charset is ANSI_X3.4-1968
Your system's locale charset (i.e. the charset used to encode file names) is
set to ANSI_X3.4-1968\. It is highly unlikely that this has been done intentionally.
Most likely the locale is not set at all. An invalid setting will result in
problems when creating data projects.Solution: To properly set the locale
charset make sure the LC_* environment variables are set. Normally the distribution
setup tools take care of this.

```

Это означает, что ваша локаль настроена неправильно.

Чтобы исправить это,

*   Удалите `/etc/locale.gen`
*   Переустановите [glibc](https://www.archlinux.org/packages/?name=glibc)
*   Отредактируйте `/etc/locale.gen`, раскомментировав все локали, которые соответствуют вашему языку и предпочтениям И ВСЕ локали `en_US` для совместимости:

```
en_US.UTF-8 UTF-8
en_US ISO-8859-1

```

*   Перегенерируйте локали с помощью *locale-gen*:

 `# locale-gen` 
```
Generating locales...
en_US.UTF-8... done
en_US.ISO-8859-1... done
pt_BR.UTF-8... done
pt_BR.ISO-8859-1... done
Generation complete.

```

Подробная информация [здесь](https://bbs.archlinux.org/viewtopic.php?pid=251512%29;).

### Brasero не может найти пустые диски

Brasero использует [gvfs](https://www.archlinux.org/packages/?name=gvfs) для управления записывающими CD/DVD устройствами. Убедитесь, что ваш текущий сеанс [не поврежден](/index.php/General_troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Разрешения_сессии "General troubleshooting (Русский)").

### Brasero не может нормализовать аудио CD

Если вы пытаетесь совершить запись, Brasero может остановиться на первом шаге (Normalization).

Чтобы этого избежать, вы можете отключить плагин нормализации в меню *Edit > Plugins*.

### VLC: Ошибка "... не может открыть диск /dev/dvd"

Если у вас возникает ошибка "vlc dvdread could not open the disc "/dev/dvd"", это может быть из-за того, что в вашей системе нету устройства `/dev/dvd`. Udev больше не создаёт `/dev/dvd`, а использует `/dev/sr0` вместо него. Чтобы решить эту проблему, отредактируйте файл конфигурации VLC (`~/.config/vlc/vlcrc`):

```
# DVD device (string)
dvd=/dev/sr0

```

### DVD-привод шумит

Если при проигрывании DVD видео система очень сильно шумит, это может быть из-за того, что диск крутится быстрее, чем нужно. Чтобы временно изменить скорость привода, выполните:

```
# eject -x 12 /dev/dvd

```

В некоторых случаях:

```
# hdparm -E12 /dev/dvd

```

Можете указать любую поддерживаемую вашим приводом скорость, и использовать 0 для установки максимальной скорости.

[Настройка скорости CD-ROM и DVD-ROM приводов](http://hektor.umcs.lublin.pl/~mikosmul/computing/tips/cd-rom-speed.html)

### Воспроизведение не работает на новом компьютере (новом DVD-приводе)

Если не работает воспроизведение на вашем новом компьютере (новом DVD-приводе), это может быть из-за того, что [код региона](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B5%D0%B3%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B5_%D0%BA%D0%BE%D0%B4%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%BE%D0%BF%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D1%85_%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2 "wikipedia:ru:Региональное кодирование оптических дисков") не установлен. Вы можете узнать и установить региональный код с помощью [regionset](https://aur.archlinux.org/packages/regionset/).

### Ни одна из вышеперечисленных программ не может рипнуть/кодировать DVD на мой жёсткий диск!

Убедитесь, что регион вашего DVD считывателя правильно задан; если этого не сделать, будут появляться необъяснимые ошибки связанные с [CSS](https://en.wikipedia.org/wiki/Content_Scramble_System "wikipedia:Content Scramble System"). Используйте [regionset](https://aur.archlinux.org/packages/regionset/) для установки региона.

### Лог графической оболочки говорит о проблемах с бекендом

Если вы используете графическую программу и испытываете проблемы, при этом видите в логах что проблема связана с какой-то программой, используемой в качестве бекенда, попробуйте воспроизвести проблему, запустив программу-бекенд вручную, используя опции командной строки из логов. Независимо от того, удастся ли вам воспроизвести проблему или нет, вы можете сообщить о проблеме. Как именно вы это можете сделать смотрите в разделе [#Проблемы с записью](#Проблемы_с_записью).

#### Особый случай: medium error / write error

Вот некоторые типичные сообщения о том, что вашему приводу не нравится конкретный носитель. Это можно исправить только используя другой привод или другой носитель. Смена программы вряд ли поможет.

K3b с *wodim*:

```
Sense Bytes: 70 00 03 00 00 00 00 12 00 00 00 00 0C 00 00 00
Sense Key: 0x3 Medium Error, Segment 0
Sense Code: 0x0C Qual 0x00 (write error) Fru 0x0

```

Brasero с *growisofs*:

```
BraseroGrowisofs stderr: :-[ WRITE@LBA=0h failed with SK=3h/ASC=0Ch/ACQ=00h]: Input/output error

```

Brasero с *libburn*:

```
BraseroLibburn Libburn reported an error SCSI error on write(16976,16): [3 0C 00] Write error

```

### AHCI

Если ваш новый DVD-привод распознан, но не монтируется, проверьте, использует ли ваш BIOS режим [AHCI](/index.php/AHCI "AHCI") и добавьте модуль в образ ядра.

Отредактируйте `/etc/mkinitcpio.conf` и добавьте `ahci` в переменную `MODULES` (подробнее смотрите в [mkinitcpio](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)")):

```
MODULES="ahci"

```

Пересоберите образ ядра, чтобы он включал новый добавленный модуль:

```
# mkinitcpio -p linux

```

## Смотрите также

*   RIAA and actual laws allow backup of physically obtained media under these conditions [RIAA - the law](https://www.riaa.com/physicalpiracy.php?content_selector=piracy_online_the_law).
*   [Convert any Movie to DVD Video](/index.php/Convert_any_Movie_to_DVD_Video "Convert any Movie to DVD Video")
*   [Main page of the project Libburnia](http://libburnia-project.org/)