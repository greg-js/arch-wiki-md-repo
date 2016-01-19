# Optical disc drive (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Кодеки](/index.php/%D0%9A%D0%BE%D0%B4%D0%B5%D0%BA%D0%B8 "Кодеки")
*   [MPlayer (Русский)](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)")
*   [dvdbackup](/index.php/Dvdbackup "Dvdbackup")
*   [MEncoder (Русский)](/index.php/MEncoder_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MEncoder (Русский)")
*   [BluRay](/index.php/BluRay "BluRay")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

Из [Википедии](https://en.wikipedia.org/wiki/ru:%D0%9E%D0%BF%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D0%BF%D1%80%D0%B8%D0%B2%D0%BE%D0%B4 "wikipedia:ru:Оптический привод"):

_"Опти́ческий при́вод — устройство, имеющее механическую составляющую, управляемую электронной схемой и предназначенное для считывания и (в большинстве современных моделей) записи информации с оптических носителей информации в виде пластикового диска с отверстием в центре (компакт-диск, DVD и т. д.); процесс считывания/записи информации с диска осуществляется при помощи лазера."_

## Contents

*   [1 Запись](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C)
    *   [1.1 Установка утилит для записи](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8)
    *   [1.2 Создание ISO-образа из существующих файлов на жёстком диске](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_ISO-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_.D0.B8.D0.B7_.D1.81.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D1.83.D1.8E.D1.89.D0.B8.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.BD.D0.B0_.D0.B6.D1.91.D1.81.D1.82.D0.BA.D0.BE.D0.BC_.D0.B4.D0.B8.D1.81.D0.BA.D0.B5)
        *   [1.2.1 Основные опции](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B8)
        *   [1.2.2 graft-points](#graft-points)
    *   [1.3 Монтирование ISO-образа](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_ISO-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0)
    *   [1.4 Конвертирование img/ccd в ISO-образ](#.D0.9A.D0.BE.D0.BD.D0.B2.D0.B5.D1.80.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_img.2Fccd_.D0.B2_ISO-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7)
    *   [1.5 Определение название оптического привода](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0.D0.B7.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.BF.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.B8.D0.B2.D0.BE.D0.B4.D0.B0)
    *   [1.6 Определение метки тома CD или DVD](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D1.82.D0.BA.D0.B8_.D1.82.D0.BE.D0.BC.D0.B0_CD_.D0.B8.D0.BB.D0.B8_DVD)
    *   [1.7 Снятие ISO образа с CD, DVD или BD](#.D0.A1.D0.BD.D1.8F.D1.82.D0.B8.D0.B5_ISO_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_.D1.81_CD.2C_DVD_.D0.B8.D0.BB.D0.B8_BD)
    *   [1.8 Стирание CD-RW и DVD-RW](#.D0.A1.D1.82.D0.B8.D1.80.D0.B0.D0.BD.D0.B8.D0.B5_CD-RW_.D0.B8_DVD-RW)
    *   [1.9 Прожиг ISO-образа на CD, DVD или BD](#.D0.9F.D1.80.D0.BE.D0.B6.D0.B8.D0.B3_ISO-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_.D0.BD.D0.B0_CD.2C_DVD_.D0.B8.D0.BB.D0.B8_BD)
    *   [1.10 Проверка записанного диска](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0)
    *   [1.11 ISO 9660 и запись "на лету"](#ISO_9660_.D0.B8_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_.22.D0.BD.D0.B0_.D0.BB.D0.B5.D1.82.D1.83.22)
    *   [1.12 Мультисессия](#.D0.9C.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D1.81.D0.B5.D1.81.D1.81.D0.B8.D1.8F)
        *   [1.12.1 Мультисессия с помощью wodim](#.D0.9C.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D1.81.D0.B5.D1.81.D1.81.D0.B8.D1.8F_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_wodim)
        *   [1.12.2 Мультисессия с помощью growisofs](#.D0.9C.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D1.81.D0.B5.D1.81.D1.81.D0.B8.D1.8F_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_growisofs)
        *   [1.12.3 Мультисессия с помощью xorriso](#.D0.9C.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D1.81.D0.B5.D1.81.D1.81.D0.B8.D1.8F_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_xorriso)
    *   [1.13 BD Defect Management](#BD_Defect_Management)
    *   [1.14 Запись Audio CD](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_Audio_CD)
    *   [1.15 Запись BIN/CUE](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_BIN.2FCUE)
        *   [1.15.1 TOC/CUE/BIN для дисков со смешанным содержимым](#TOC.2FCUE.2FBIN_.D0.B4.D0.BB.D1.8F_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2_.D1.81.D0.BE_.D1.81.D0.BC.D0.B5.D1.88.D0.B0.D0.BD.D0.BD.D1.8B.D0.BC_.D1.81.D0.BE.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.BC.D1.8B.D0.BC)
    *   [1.16 Проблемы с записью](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D1.8C.D1.8E)
    *   [1.17 Запись CD/DVD/BD с помощью графических программ](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_CD.2FDVD.2FBD_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D1.85_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC)
        *   [1.17.1 Свободные графические программы](#.D0.A1.D0.B2.D0.BE.D0.B1.D0.BE.D0.B4.D0.BD.D1.8B.D0.B5_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
        *   [1.17.2 Nero Linux](#Nero_Linux)
*   [2 Вопроизведение мультимедиа](#.D0.92.D0.BE.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D0.BC.D0.B5.D0.B4.D0.B8.D0.B0)
    *   [2.1 CD](#CD)
    *   [2.2 DVD](#DVD)
*   [3 Риппинг](#.D0.A0.D0.B8.D0.BF.D0.BF.D0.B8.D0.BD.D0.B3)
    *   [3.1 CD](#CD_2)
    *   [3.2 DVD](#DVD_2)
        *   [3.2.1 dvd::rip](#dvd::rip)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Ошибка локали K3b](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D0.B8_K3b)
    *   [4.2 Brasero не может найти пустые диски](#Brasero_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.BD.D0.B0.D0.B9.D1.82.D0.B8_.D0.BF.D1.83.D1.81.D1.82.D1.8B.D0.B5_.D0.B4.D0.B8.D1.81.D0.BA.D0.B8)
    *   [4.3 Brasero не может нормализовать аудио CD](#Brasero_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.BD.D0.BE.D1.80.D0.BC.D0.B0.D0.BB.D0.B8.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE_CD)
    *   [4.4 VLC: Ошибка "... не может открыть диск /dev/dvd"](#VLC:_.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.22..._.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D1.82.D1.8C_.D0.B4.D0.B8.D1.81.D0.BA_.2Fdev.2Fdvd.22)
    *   [4.5 DVD-привод шумит](#DVD-.D0.BF.D1.80.D0.B8.D0.B2.D0.BE.D0.B4_.D1.88.D1.83.D0.BC.D0.B8.D1.82)
    *   [4.6 Воспроизведение не работает на новом компьютере (новом DVD-приводе)](#.D0.92.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0_.D0.BD.D0.BE.D0.B2.D0.BE.D0.BC_.D0.BA.D0.BE.D0.BC.D0.BF.D1.8C.D1.8E.D1.82.D0.B5.D1.80.D0.B5_.28.D0.BD.D0.BE.D0.B2.D0.BE.D0.BC_DVD-.D0.BF.D1.80.D0.B8.D0.B2.D0.BE.D0.B4.D0.B5.29)
    *   [4.7 Ни одна из вышеперечисленных программ не может рипнуть/кодировать DVD на мой жёсткий диск!](#.D0.9D.D0.B8_.D0.BE.D0.B4.D0.BD.D0.B0_.D0.B8.D0.B7_.D0.B2.D1.8B.D1.88.D0.B5.D0.BF.D0.B5.D1.80.D0.B5.D1.87.D0.B8.D1.81.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D1.80.D0.B8.D0.BF.D0.BD.D1.83.D1.82.D1.8C.2F.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_DVD_.D0.BD.D0.B0_.D0.BC.D0.BE.D0.B9_.D0.B6.D1.91.D1.81.D1.82.D0.BA.D0.B8.D0.B9_.D0.B4.D0.B8.D1.81.D0.BA.21)
    *   [4.8 Лог графической оболочки говорит о проблемах с бекендом](#.D0.9B.D0.BE.D0.B3_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B9_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_.D0.B3.D0.BE.D0.B2.D0.BE.D1.80.D0.B8.D1.82_.D0.BE_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0.D1.85_.D1.81_.D0.B1.D0.B5.D0.BA.D0.B5.D0.BD.D0.B4.D0.BE.D0.BC)
        *   [4.8.1 Особый случай: medium error / write error](#.D0.9E.D1.81.D0.BE.D0.B1.D1.8B.D0.B9_.D1.81.D0.BB.D1.83.D1.87.D0.B0.D0.B9:_medium_error_.2F_write_error)
    *   [4.9 AHCI](#AHCI)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Запись

**Важно:** Качество оптических приводов и самих дисков очень сильно варьируется. Главным образом, для получения надёжной записи рекомендуется производить ее на низкой скорости. Если появляются странные проблемы с записанными вами компакт-дисками, попробуйте производить запись на самой низкой скорости, которую поддерживает ваш привод.

Процесс прожига (записи данных на диск) состоит из получения файла образа и последующей его записи на оптический носитель. В принципе, образом может быть любой файл данных. Если вы хотите смонтировать записанный диск, то, как правило, следует указывать файловую систему ISO 9660\. Audio CD и мультимедийные CD обычно прожигаются из файла _.bin_ с использованием файла _.toc_ или _.cue_, который содержит информацию о расположении треков.

### Установка утилит для записи

Если вы хотите использовать программы с графическим интерфейсом, перейдите к разделу [#Запись CD/DVD/BD с помощью графических программ](#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_CD.2FDVD.2FBD_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D1.85_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC).

Работа с перечисленными здесь утилитами происходит из командной строки. Они являются бэкендами для большинства свободных графических программ для работы с CD, DVD и BD. Этими утилитами может быть полезно пользоваться напрямую, если у вас возникают проблемы с записью при помощи графической программы либо вы хотите автоматизировать запись с помощью скриптов.

Вам нужна как минимум одна программа для создания образов файловой системы и одна программа, которая может записывать данные на нужный вам тип носителя.

Доступные программы для создания образа ISO 9660:

*   _genisoimage_ из пакета [cdrkit](https://www.archlinux.org/packages/?name=cdrkit)
*   _mkisofs_ из пакета [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   _xorriso_ и _xorrisofs_ из пакета [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

Как правило, используется _genisoimage_.

Доступные программы для записи на носители:

*   _cdrdao_ из пакета [cdrdao](https://www.archlinux.org/packages/?name=cdrdao) (только для CD и только TOC/CUE/BIN)
*   _cdrecord_ из пакета [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   _cdrskin_ из пакета [libburn](https://www.archlinux.org/packages/?name=libburn)
*   _growisofs_ из пакета [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) (только для DVD и BD)
*   _wodim_ из пакета [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) (только для CD, для DVD устарела)
*   _xorriso_ и _xorrecord_ из пакета [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

Обычно используют _wodim_ для CD и _growisofs_ для DVD и Blu-ray дисков. Как обойти баг _growisofs_ с BD-R смотрите ниже. Для записи TOC/CUE/BIN файлов на CD, установите [cdrdao](https://www.archlinux.org/packages/?name=cdrdao).

Свободные графические программы для записи CD, DVD или BD используют как минимум один из перечисленных выше пакетов.

Программы 'mkisofs _и_ xorrisofs _поддерживают опции_ genisoimage_, описанные в этой статье._

Программы _cdrecord_ и _cdrskin_ поддерживают описанные опции _wodim_; _xorrecord_ также поддерживает их за исключением тех, которые предназначены для Audio CD.

**Обратите внимание:**

*   Файлы, устанавливаемые пакетами [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) и [cdrtools](https://www.archlinux.org/packages/?name=cdrtools) конфликтуют. Устанавливайте только один из пакетов.
*   Если вы хотите установить [cdrtools](https://en.wikipedia.org/wiki/ru:Cdrtools "wikipedia:ru:Cdrtools") убедитесь, что вы собрали пакет с помощью [makepkg](/index.php/Makepkg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Makepkg (Русский)") и установили его напрямую с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") — фронтенды pacman могут решить установить cdrkit вместо него.

### Создание ISO-образа из существующих файлов на жёстком диске

Чтобы упростить создание ISO-образа, скопируйте все файлы для записи в один каталог, например `./for_iso`.

Затем сгенерируйте образ с _genisoimage_:

```
$ genisoimage -V "_ARCHIVE_2013_07_27_" -J -r -o _isoimage.iso_ _./for_iso_

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

Также вы можете указать для _genisoimage_ сразу несколько файлов и каталогов, которые будут добавлены в образ:

```
$ genisoimage -V "_BACKUP_2013_07_27_" -J -r -o _backup_2013_07_27.iso_ \
  -graft-points \
  _/photos=/home/user/photos \_
        /mail=/home/user/mail \
        /photos/holidays=/home/user/holidays/photos

```

`-graft-points`

Позволяет задавать _определения путей_, которые состоят из целевого адреса на файловой системе ISO (например, `/photos`) и адреса источника на жёстком диске (например `/home/user/photos`). Эти адреса разделены символом "=".

В этом примере, содержимое каталогов `/home/user/photos`, `/home/user/mail` и `/home/user/holidays/photos` будет помещено в каталоги `/photos`, `/mail` и `/photos/holidays` на ISO образе, соответственно.

Программы _mkisofs_ и _xorrisofs_ принимают такие же опции. Для создания резервных копий важных данных рекомендуется использовать _xorrisofs_ с опцией `--for_backup`, которая создаст список контроля доступа и посчитает хеш-суммы MD5 для каждого файла с данными.

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
# mount -t iso9660 -o ro,loop=/dev/loop0 _/путь/к/файлу.iso_ _/точка/монтирования_

```

После просмотра содержимого не забудьте размонтировать образ:

```
# umount /cdrom

```

Если вы хотите смонтировать образ от имени обычного пользователя, смотрите [fuseiso](/index.php/Fuseiso "Fuseiso").

### Конвертирование img/ccd в ISO-образ

Чтобы сконвертировать образ `img`/`ccd`, воспользуйтесь утилитой [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso):

```
$ ccd2iso _~/image.img_ _~/image.iso_

```

### Определение название оптического привода

В примерах из этого раздела предполагается, что ваше записывающее устройство называется `/dev/sr0`.

Проверьте оптический привод командой

```
$ wodim dev=_/dev/sr0_ -checkdrive

```

которая отобразит производителя (поле `Vendor_info`) и модель (`Identification`) вашего привода.

Если привод не найден, проверьте, существуют ли какие-либо устройства `/dev/sr*` и предоставлены ли ими права на чтение/запись (`wr-`) вам или вашей группе. Если вы не нашли подходящих устройств `/dev/sr*`, попробуйте выполнить

```
# modprobe sr_mod

```

### Определение метки тома CD или DVD

Если вы хотите получить название/метку носителя, воспользуйтесь _dd_:

```
$ dd if=_/dev/sr0_ bs=1 skip=32808 count=32

```

### Снятие ISO образа с CD, DVD или BD

Следует определить размер файловой системы ISO перед тем, как копировать её на жёсткий диск. Большинство типов накопителей предоставляют больше данных, чем на них было записано во время самого последнего прожига.

Чтобы посчитать реальное количество блоков, воспользуйтесь программой _isosize_ из пакета [util-linux](https://www.archlinux.org/packages/?name=util-linux):

```
$ blocks=$(isosize -d 2048 _/dev/sr0_)

```

Проверьте, выглядит ли полученное число блоков правдоподобно:

 `$ echo "That would be $(expr $blocks / 512) MB"` 

```
That would be 589 MB

```

Затем скопируйте полученное количество данных с носителя на жёсткий диск:

```
$ dd if=_/dev/sr0_ of=_isoimage.iso_ bs=2048 count=$blocks

```

Не указывайте параметр `count=$blocks`, если вы не определяли количество блоков. Вероятно, файл образа получится больше, чем необходимо на самом деле. Тем не менее, полученный файл можно будет смонтировать. Он всё ещё будет помещаться на носителе такого же типа, что и исходный носитель, с которого считывался образ.

Если исходный носитель был загрузочным, то созданный образ также будет загрузочным. Вы можете использовать его как виртуальный диск для виртуальной машины или прожечь на оптический носитель, который станет загрузочным.

### Стирание CD-RW и DVD-RW

Перед тем, как записать новую информацию на уже использованный CD-RW, необходимо стереть с него старую. Это можно выполнить командой

```
$ wodim -v dev=_/dev/sr0_ blank=fast

```

Есть две опции для стирания данных: `blank=fast` (полная очистка) и `blank=full` (быстрая очистка). Полная очистка происходит во много раз медленнее, чем быстрая, однако использование быстрой лишает возможности мультисессионной записи на диск и записи поточных данных, длина которых неизвестна заранее (например, видео с камеры). Также имейте ввиду, что при быстрой очистке ваши данные не уничтожаются физически, и могут быть восстановлены посторонними лицами.

Вы также можете использовать другие программы:

```
$ cdrecord -v dev=_/dev/sr0_ blank=all
$ cdrskin -v dev=_/dev/sr0_ blank=all
$ xorriso -outdev _/dev/sr0_ -blank as_needed

```

Для стирания DVD-RW вы можете использовать утилиту _dvd+rw-format_ из пакета [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools):

```
$ dvd+rw-format -blank=fast _/dev/sr0_

```

Вы также можете использовать другие программы:

```
$ cdrskin -v dev=_/dev/sr0_ blank=format_overwrite
$ xorriso -outdev _/dev/sr0_ -format as_needed

```

Отформатированный DVD+RW (обратите внимание на `+`!) носитель может быть перезаписан без такой процедуры стирания. Поэтому необходимо лишь разово выполнить первичное форматирование командой:

```
$ dvd+rw-format -force _/dev/sr0_

```

Все другие типы носителей являются записываемыми либо только один раз (CD-R, DVD-R, DVD+R, BD-R) либо перезаписываемыми без необходимости стирания (DVD-RAM, BD-RE).

### Прожиг ISO-образа на CD, DVD или BD

Для записи подготовленного ISO-образа `isoimage.iso` на оптический носитель, используйте одну из указанных ниже команд.

Для CD выполните:

```
$ wodim -v -sao dev=_/dev/sr0_ _isoimage.iso_

```

и в случае DVD или BD:

```
$ growisofs -dvd-compat -Z _/dev/sr0_=_isoimage.iso_

```

Программы _cdrecord_, _cdrskin_ и _xorrecord_ могут быть использованы со всеми видами носителей с опциями, показанными на примере _wodim_.

**Обратите внимание:**

*   Убедитесь в том, что носитель не был смонтирован перед тем, как начнёте писать на него. Монтирование могло произойти автоматически если носитель содержит файловую систему. В лучшем случае это не даст записывающим программам использовать устройство прожига. В худшем — произойдут ошибки записи, потому что операции чтения будут мешать приводу.

Поэтому, если вы сомневаетесь, выполните:

```
# umount /dev/sr0

```

*   В программе _growisofs_ есть небольшая ошибка, касающаяся пустых BD-R носителей. Она выдаёт сообщение об ошибке после того, как прожиг завершён. Из-за этого такие программы, как _k3b_ думают, что весь процесс прожига был неудачным.

Чтобы исправить это, либо

*   *   отформатируйте пустой BD-R с помощью `dvd+rw-format _/dev/sr0_` перед тем как с ним будет работать _growisofs_
    *   либо используйте опцию _growisofs_ `-use-the-force-luke=spare:none`

### Проверка записанного диска

Вы можете проверить, что диск был записан правильно и не содержит ошибок. Всегда вынимайте носитель и снова вставляйте его перед тем, как выполнять проверку. Это будет гарантировать, что для чтения не используется какой-либо кеш, предоставляемый ядром.

Сначала вычислите контрольную сумму MD5 исходного образа:

 `$ md5sum _isoimage.iso_` 

```
 e5643e18e05f5646046bb2e4236986d8 isoimage.iso

```

Затем вычислите контрольную сумму файловой системы на носителе. Несмотря на то, что при чтении некоторых типов носителей выдаётся абсолютно такое же количество данных, какое было передано записывающей программе, при чтении многие других типов носителей к этим данным добавляется находящийся дальше мусор. Поэтому вы должны ограничить чтение размером файла ISO образа, вычислив точное количество блоков для чтения:

```
$ blocks=$(expr $(du -b _isoimage.iso_ | awk '{print $1}') / 2048)

```

 `$ dd if=''/dev/sr0'' bs=2048 count=$blocks | md5sum` 

```
 43992+0 records in
 43992+0 records out
 90095616 bytes (90 MB) copied, 0.359539 s, 251 MB/s
 e5643e18e05f5646046bb2e4236986d8  -

```

В обоих случаях должна быть вычислена та же самая контрольная сумма (в нашем примере `e5643e18e05f5646046bb2e4236986d8`). Если они не совпали, вероятно, вы также получите ошибку ввода/вывода при работе _dd_. При этом _dmesg_ может сообщать об ошибках SCSI и номерах блоков, если вам это интересно.

### ISO 9660 и запись "на лету"

Не обязательно сохранять образ на жесткий диск перед тем, как производить запись на оптический носитель. Только очень старые CD приводы на очень старых компьютерах могли испытывать проблемы с записью из-за пустого буфера привода.

Если вы опустите опцию `-o` команды _genisoimage_, то выходной поток будет направлен в стандартный вывод. Он может быть перенаправлен на стандартный ввод записывающих программ.

```
$ genisoimage -V "_ARCHIVE_2013_07_27_" -J -r _./for_iso_ | \
  wodim -v dev=_/dev/sr0_ -waiti -

```

Опция `-waiti` здесь не обязательна. Она предотвращает `wodim` от начала записи на носитель до того, как _genisoimage_ начнёт выводить данные. Это позволит _genisoimage_ читать носитель, не мешая уже начатому процессу прожига. Смотрите следующий раздел про мультисессии.

В случае DVD и BD вы можете использовать _growisofs_ для прожига "на лету", чтобы при этом она сама запускала _genisoimage_, следующим образом:

```
$ export MKISOFS="genisoimage"
$ growisofs -Z _/dev/sr0_ -V "_ARCHIVE_2013_07_27_" -r -J _./for_iso_

```

### Мультисессия

Файловая система ISO 9660 может использоваться также для мультисессионной записи, когда вы записываете какие-то данные на чистый носитель, а затем можете дозаписывать на него новые данные, начиная с адреса первого неиспользованного блока. Новое дерево каталогов перекрывает при этом старое, так, что новые файлы будут добавлены в уже существующие каталоги (вместе с теми, что там уже были), а файлы с полностью совпадающими именами будут считаться перезаписанными (при этом физически старые данные не стираются с диска, лишь становятся недоступными). Linux и многие другие операционные системы всегда монтируют самое новое дерево каталогов.

#### Мультисессия с помощью wodim

После записи CD-R и CD-RW все еще остаются дозаписываемыми, если при записи с _wodim_ была использована опция `-multi`:

```
$ wodim -v -multi dev=_/dev/sr0_ _isoimage.iso_

```

Чтобы выполнить новую сессию записи, необходимо запросить параметры сессии командой

```
$ m=$(wodim dev=_/dev/sr0_ -msinfo)

```

С помощью этих параметров вы можете сгенерировать ISO-образ для новой сессии:

```
$ genisoimage -M /dev/sr0 -C "$m" \
   -V "_ARCHIVE_2013_07_28_" -J -r -o _session2.iso_ _./more_for_iso_

```

Наконец, запишите полученный образ на носитель. Вы снова можете разрешить мультисессию опцией `-multi`:

```
$ wodim -v -multi dev=_/dev/sr0_ _session2.iso_

```

Программы _cdrskin_ и _xorrecord_ также разрешают мультисессию для DVD-R, DVD+R, BD-R и неформатированных DVD-RW. Программа _cdrecord_ разрешает мультисессию как минимум для DVD-R и DVD-RW. Разумеется, все они разрешают её с CD-R и CD-RW.

Большинство перезаписываемых носителей не записывают историю сессий, которая могла бы быть распознана монтирующим ядром. Но с помощью ISO 9660 можно добиться эффекта мультисессии даже на таких носителях.

_growisofs_ и _xorriso_ позволяют делать все то же самое без лишних действий.

#### Мультисессия с помощью growisofs

По умолчанию, _growisofs_ использует _mkisofs_ в качестве бекенда для генерирования ISO-образа, которой она передаёт большинство своих аргументов. Смотрите примеры с _genisoimage_, приведённые выше. Она запрещает опцию `-o` и объявляет устаревшей опцию `-C`. Вы можете сделать так, чтобы она работала с любой другой совместимой программой, установив переменную окружения `MKISOFS`:

```
$ export MKISOFS="genisoimage"
$ export MKISOFS="xorrisofs"

```

Для создания новой файловой системы на оптическом носителе используется опция `-Z`:

```
$ growisofs -Z _/dev/sr0_ -V "_ARCHIVE_2013_07_27_" -r -J _./for_iso_

```

Для добавления новых файлов в режиме мультисессии, запускайте программу с опцией `-M`:

```
$ growisofs -M _/dev/sr0_ -V "_ARCHIVE_2013_07_28_" -r -J _./more_for_iso_

```

Для получения дополнительной информации смотрите [инструкцию по growisofs](http://linux.die.net/man/1/growisofs), а также инструкции по _genisoimage_, _mkisofs_ и _xorrisofs_.

#### Мультисессия с помощью xorriso

`xorriso` самостоятельно проверяет, пуст ли накопитель и доступна ли дозапись на него в режиме мультисессии. Если диск не подходит для дозаписи, его следует сначала очистить. Для этого используется опция `-blank as_needed`, при указании которой диск будет очищен только в случае необходимости:

```
$ xorriso -outdev _/dev/sr0_ -blank as_needed \
          -volid "_ARCHIVE_2013_07_27_" -joliet on -add _./for_iso_ --

```

Если на диск уже были записаны данные, и дозапись возможна, _xorriso_ добавит указанные файлы на диск в случае, если вместо `-outdev` указана опция `-dev`. Разумеется, здесь не надо давать команду `-blank`

```
$ xorriso -dev _/dev/sr0_ \
          -volid "_ARCHIVE_2013_07_28_" -joliet on -add _./more_for_iso_ --

```

Для дополнительной информации смотрите [инструкцию](https://www.gnu.org/software/xorriso/man_1_xorriso.html) и особенно её [примеры](https://www.gnu.org/software/xorriso/man_1_xorriso.html#EXAMPLES)

### BD Defect Management

Обычно запись на носители BD-RE и форматированные BD-R производится с включенной функцией Defect Management (_управление дефектами_). При записи сразу же происходит чтение записанных блоков и их проверка. В случае несовпадения эти блоки записываются заново или перенаправляются в резервную область (_Spare Area_), где располагаются запасные блоки.

Эти проверки чтения снижают скорость записи более чем наполовину от номинальной скорости записи привода и BD-носителя, а иногда даже больше. Активное использование резервной области впоследствии приводит к большим задержкам во время чтения. Поэтому использование Defect Management не всегда бывает желательно.

_cdrecord_ не форматирует BD-R и не умеет отключать Defect Management на носителях BD-RE media.

_growisofs_ форматирует BD-R по умолчанию. Defect Management можно отключить с помощью опции `-use-the-force-luke=spare:none`. Однако, эта опция не работает с носителями BD-RE.

_cdrskin_, _xorriso_ и _xorrecord_ не форматируют BD-R по умолчанию. Они делают форматирование с помощью соответствующих опций `cdrskin blank=format_if_needed`, `xorriso -format as_needed`, `xorrecord blank=format_overwrite`. Эти три программы могут отключить Defect Management на BD-RE и на уже отформатированном BD-R с помощью опций `cdrskin stream_recording=on`, `xorriso -stream_recording on`, `xorrecord stream_recording=on`, соответственно.

### Запись Audio CD

Сохраните ваши аудиотреки в формате WAV, стерео 16 бит без сжатия. Чтобы переконвертировать MP3 в WAV, убедитесь, что пакет [lame](https://www.archlinux.org/packages/?name=lame) установлен, перейдите с помощью _cd_ в директорию с вашими MP3-файлами и выполните:

```
$ for i in *.mp3; do lame --decode "$i" "$(basename "$i" .mp3)".wav; done

```

В том случае, если вы получите ошибку при попытке записи WAV файлов, сконвертированных с помощью LAME, попробуйте декодировать с помощью [mpg123](https://www.archlinux.org/packages/?name=mpg123):

```
$ for i in *.mp3; do mpg123 --rate 44100 --stereo --buffer 3072 --resync -w $(basename $i .mp3).wav $i; done

```

Переименуйте файлы таким образом, чтобы они шли в нужном порядке следования при отображении их по алфавиту, например `01.wav`, `02.wav`, `03.wav` и т.д. Используйте следующую команду чтобы имитировать запись WAV файлов в качестве аудио CD:

```
$ wodim **-dummy** -v -pad speed=1 dev=_/dev/sr0_ -dao -swab *.wav

```

В случае, если вы обнаружите ошибки или пустые треки, как например:

```
Track 01: audio    0 MB (00:00.00) no preemp pad

```

попробуйте другой декодер (например _mpg123_) или используйте для записи _cdrecord_ из пакета [cdrtools](https://www.archlinux.org/packages/?name=cdrtools).

Обратите внимание, что [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) также содержит команду _cdrecord_, но это всего лишь символическая ссылка на _wodim_. Если все в порядке, уберите флаг `dummy`, чтобы на самом деле начать запись.

Для проверки записанного Audio CD используйте [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)"):

```
$ mplayer cdda://

```

### Запись BIN/CUE

Чтобы записать образ BIN/CUE, выполните:

```
$ cdrdao write --device _/dev/sr0_ _image.cue_

```

#### TOC/CUE/BIN для дисков со смешанным содержимым

ISO-образы содержат только одну дорожку данных. Если вы хотите создать образ диска со смешанным содержимым (дорожка данных с несколькими аудиотреками), то вам нужно будет создать пару TOC/BIN:

```
$ cdrdao read-cd --read-raw --datafile _image.bin_ --driver generic-mmc:0x20000 --device _/dev/cdrom_ _image.toc_

```

Некоторые программы умеют работать только с парой CUE/BIN; вы можете создать файл CUE с помощью _toc2cue_ (часть пакета [cdrdao](https://www.archlinux.org/packages/?name=cdrdao)):

```
$ toc2cue _image.toc_ _image.cue_

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

*   **cdw** — Фронтенд на ncurses над утилитами _cdrecord_, _mkisofs_, _growisofs_, _dvd+rw-mediainfo_, _dvd+rw-format_ и _xorriso_.

[http://cdw.sourceforge.net/](http://cdw.sourceforge.net/) || [cdw](https://aur.archlinux.org/packages/cdw/)<sup><small>AUR</small></sup>

*   **[GnomeBaker](https://en.wikipedia.org/wiki/ru:GnomeBaker "wikipedia:ru:GnomeBaker")** — Полнофункциональное приложение для записи CD/DVD для рабочего стола [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")

[http://gnomebaker.sourceforge.net/](http://gnomebaker.sourceforge.net/) || [gnomebaker](https://aur.archlinux.org/packages/gnomebaker/)<sup><small>AUR</small></sup>

*   **Graveman** — Приложение GTK для записи CD/DVD. Оно требует указания используемых устройств при настройке.

[http://graveman.tuxfamily.org/](http://graveman.tuxfamily.org/) || [graveman](https://aur.archlinux.org/packages/graveman/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/graveman)]</sup>

*   **[isomaster](https://en.wikipedia.org/wiki/ru:ISO_Master "wikipedia:ru:ISO Master")** — Редактор ISO-образов.

[http://littlesvr.ca/isomaster](http://littlesvr.ca/isomaster) || [isomaster](https://aur.archlinux.org/packages/isomaster/)<sup><small>AUR</small></sup>

*   **[K3b](https://en.wikipedia.org/wiki/ru:K3b "wikipedia:ru:K3b")** — Простое в использовании приложение на KDElibs для записи CD с богатым функционалом.

[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **[X-CD-Roast](https://en.wikipedia.org/wiki/ru:X-CD-Roast "wikipedia:ru:X-CD-Roast")** — Легковесная графическая оболочка над _cdrtools_ для записи CD и DVD.

[http://www.xcdroast.org/](http://www.xcdroast.org/) || [xcdroast](https://aur.archlinux.org/packages/xcdroast/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xcdroast)]</sup>

*   **Xfburn** — Простой фронтенд над библиотеками libburnia с поддержкой CD/DVD(-RW), ISO образов и BurnFree.

[http://goodies.xfce.org/projects/applications/xfburn](http://goodies.xfce.org/projects/applications/xfburn) || [xfburn](https://www.archlinux.org/packages/?name=xfburn)

*   **xorriso-tcltk** — Графический фронтенд над утилитой _xorriso_ для работы с ISO и записи CD/DVD/BD.

[https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif](https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif) || [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

#### Nero Linux

Nero Linux — это коммерческая программа для записи от создателей Nero для Windows — Nero AG. Основным преимуществом Nero Linux считают её интерфейс, который похож на версию для Windows. Таким образом, пользователи, перешедшие с Windows считают ее простой в использовании. Теперь версия для Linux включает Nero Express (предоставляет интерфейс в виде мастера, который проводит пользователя через процесс записи CD и DVD шаг за шагом), к которому привыкли ещё в версии для Windows. Также в версии 4 добавилась поддержка Defect Management для Blu-ray дисков, интеграция Isolinux для создания загрузочного носителя и поддержка аудиоформатов Musepack и AIFF...

Nero Linux 4 продаётся за $19.99, также есть бесплатная пробная версия.

*   [Nero Linux 4](http://www.nero.com/enu/promo-linux.html)
*   [nerolinux](https://aur.archlinux.org/packages/nerolinux/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/nerolinux)]</sup> [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") пакет.

Nero Linux предоставляет следующие возможности:

*   Простой пользовательский интерфейс в виде мастера для записи дисков Nero Linux Express 4.
*   Полная поддержка записи на Blu-ray.
*   Поддержка записи Audio CD (CD-DA), ISO 9660 (поддерживается Joliet), CD-text, загрузочных дисков ISOLINUX, Мультисессионных дисков, DVD-Video и miniDVD, а также двухслойных DVD.
*   Продвинутая запись с помощью Nero Burning ROM и клиента командной строки.

**Обратите внимание:** Необходимый модуль `sg` должен быть загружен автоматически, в противном случае смотрите [Модули ядра](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0 "Модули ядра") для информации о ручной настройке.

## Вопроизведение мультимедиа

### CD

Для прослушивания Audio CD [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [libcdio](https://www.archlinux.org/packages/?name=libcdio), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### DVD

[DVD](https://en.wikipedia.org/wiki/ru:DVD "wikipedia:ru:DVD") (Digital Versatile Disc или Digital Video Disc) — это оптический дисковый носитель, используемый для хранения видео и других данных.

Если вы хотите проиграть зашифрованный DVD, вы должны установить пакеты libdvd*:

*   [libdvdread](https://www.archlinux.org/packages/?name=libdvdread)
*   [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss)
*   [libdvdnav](https://www.archlinux.org/packages/?name=libdvdnav)

В дополнение к ним, вы должны установить какой-нибудь плеер. Популярными DVD-проигрывателями являются [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)"), [xine](https://en.wikipedia.org/wiki/ru:Xine "wikipedia:ru:Xine") и [VLC](/index.php/VLC "VLC"). Смотрите также список [видеоплееров](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9/%D0%9C%D1%83%D0%BB%D1%8C%D1%82%D0%B8%D0%BC%D0%B5%D0%B4%D0%B8%D0%B0#.D0.92.D0.B8.D0.B4.D0.B5.D0.BE_.D0.BF.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B8 "Список приложений/Мультимедиа") и специальные инструкции для [MPlayer](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_DVD_.D1.81_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.BE.D0.B9_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BD.D0.B0.D0.B2.D0.B8.D0.B3.D0.B0.D1.86.D0.B8.D0.B8 "MPlayer (Русский)").

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

[http://sourceforge.net/projects/grip/](http://sourceforge.net/projects/grip/) || [grip](https://www.archlinux.org/packages/?name=grip)

*   **KAudioCreator** — Программа для риппинга и кодирования Audio CD и кодирования файлов с диска.

[http://kde-apps.org/content/show.php/KAudioCreator?content=107645](http://kde-apps.org/content/show.php/KAudioCreator?content=107645) || [kaudiocreator](https://www.archlinux.org/packages/?name=kaudiocreator)

*   **morituri** — CD риппер, которому точность важнее скорости.

[http://thomas.apestaart.org/morituri/trac/](http://thomas.apestaart.org/morituri/trac/) || [morituri](https://www.archlinux.org/packages/?name=morituri)

*   **ripperX** — Программа на GTK+ для риппинга аудио и записи в MP3.

[http://sourceforge.net/projects/ripperx/](http://sourceforge.net/projects/ripperx/) || [ripperx](https://www.archlinux.org/packages/?name=ripperx)

*   **rubyripper** — Риппер аудиодисков, который выдаёт качественную запись путём многократного чтения, обнаружения и исправления различий.

[http://code.google.com/p/rubyripper/](http://code.google.com/p/rubyripper/) || [rubyripper](https://www.archlinux.org/packages/?name=rubyripper)

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

[http://www.pixelbeat.org/programs/dvd-vr/](http://www.pixelbeat.org/programs/dvd-vr/) || [dvd-vr](https://aur.archlinux.org/packages/dvd-vr/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dvd-vr)]</sup>

*   **[dvdbackup](/index.php/Dvdbackup "Dvdbackup")** — Программа, извлекающая данные без перекодирования. Она полезна для создания _физических_ копий зашифрованных DVD в сочетании с **libdvdcss**, а также при расшифровке видео другими утилитами, которые не умеют читать зашифрованные DVD.

[http://dvdbackup.sourceforge.net/](http://dvdbackup.sourceforge.net/) || [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup)

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Самостоятельная и свободная программа для широковещательной трансляции аудио и видео через интернет для Linux/Unix, способная сделать прямой рип в любой формат (аудио/видео) с ISO образа DVD-Video: просто выберите входящий поток как ISO образ и заполните необходимые параметры. Она умеет микшировать, подрезать, раздёлять выбранные потоки, а также имеет многие другие функции.

[http://ffmpeg.org/](http://ffmpeg.org/) || See [article](/index.php/FFmpeg#Package_installation "FFmpeg")

*   **HandBrake** — Многопоточный видео транскодер, который предоставляет как графический интерфейс, так и интерфейс командной строки и имеет много предустановленных настроек.

[http://handbrake.fr/](http://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **Hybrid** — Мультиплатформенная графическая оболочка на Qt для многих других утилит, который может конвертировать практически любой входной поток в x264/Xvid/VP8 + ac3/ogg/mp3/aac/flac внутрь контейнера mp4/m2ts/mkv/webm/mov/avi, Blu-ray или структуру AVCHD.

[http://www.selur.de/](http://www.selur.de/) || [hybrid-encoder](https://aur.archlinux.org/packages/hybrid-encoder/)<sup><small>AUR</small></sup>

*   **[MEncoder](/index.php/MEncoder_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MEncoder (Русский)")** — Свободный видеодекодер для командной строки, кодирующая и фильтрующая программа, выпущенная под лицензией GNU GPL. Практически является родственником MPlayer и может конвертировать все форматы, которые понимает MPlayer во множество сжатых и несжатых форматов, используя различные кодеки. Программы-обёртки, такие как [h264enc](https://aur.archlinux.org/packages/h264enc/)<sup><small>AUR</small></sup> и [undvd](https://aur.archlinux.org/packages/undvd/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/undvd)]</sup> могут предоставить более понятный интерфейс. Доступно много [графических оболочек](/index.php/MEncoder#GUI_frontends "MEncoder").

[http://www.mplayerhq.hu/](http://www.mplayerhq.hu/) || [mencoder](https://www.archlinux.org/packages/?name=mencoder)

*   **Transcode** — Видео/DVD риппер и энкодер с интерфейсом командной строки.

[http://tcforge.berlios.de/](http://tcforge.berlios.de/) || [transcode](https://www.archlinux.org/packages/?name=transcode)

#### dvd::rip

dvd::rip — это фронтенд для [transcode](https://www.archlinux.org/packages/?name=transcode), используемый для извлечения DVD на жёсткий диск и перекодировки или извлечения и перекодировки "на лету".

Следующие пакеты должны быть установлены:

*   [dvdrip](https://www.archlinux.org/packages/?name=dvdrip): GTK фронтенд над [transcode](https://www.archlinux.org/packages/?name=transcode), который делает риппинг и кодирование
*   [libdv](https://www.archlinux.org/packages/?name=libdv): Программный кодек для DV видео
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): Видеокодек с открытым исходным кодом. Пригодится, если вы хотите кодировать рипнутые вами файлы в XviD, MPEG-4 (свободная альтернатива кодеку DivX)
*   [divx4linux](https://aur.archlinux.org/packages/divx4linux/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/divx4linux)]</sup>: Если вы хотите кодировать рипнутые вами файлы в DivX
*   [subtitleripper](https://aur.archlinux.org/packages/subtitleripper/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/subtitleripper)]</sup>: Если вы хотите читать и обрабатывать субтитры

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

*   Перегенерируйте локали с помощью _locale-gen_:

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

Brasero использует [gvfs](https://www.archlinux.org/packages/?name=gvfs) для управления записывающими CD/DVD устройствами. Убедитесь, что ваш текущий сеанс [не поврежден](/index.php/General_troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8 "General troubleshooting (Русский)").

### Brasero не может нормализовать аудио CD

Если вы пытаетесь совершить запись, Brasero может остановиться на первом шаге (Normalization).

Чтобы этого избежать, вы можете отключить плагин нормализации в меню _Edit > Plugins_.

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

Если не работает воспроизведение на вашем новом компьютере (новом DVD-приводе), это может быть из-за того, что [код региона](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B5%D0%B3%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B5_%D0%BA%D0%BE%D0%B4%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%BE%D0%BF%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D1%85_%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2 "wikipedia:ru:Региональное кодирование оптических дисков") не установлен. Вы можете узнать и установить региональный код с помощью [regionset](https://aur.archlinux.org/packages/regionset/)<sup><small>AUR</small></sup>.

### Ни одна из вышеперечисленных программ не может рипнуть/кодировать DVD на мой жёсткий диск!

Убедитесь, что регион вашего DVD считывателя правильно задан; если этого не сделать, будут появляться необъяснимые ошибки связанные с [CSS](https://en.wikipedia.org/wiki/Content_Scramble_System "wikipedia:Content Scramble System"). Используйте [regionset](https://aur.archlinux.org/packages/regionset/)<sup><small>AUR</small></sup> для установки региона.

### Лог графической оболочки говорит о проблемах с бекендом

Если вы используете графическую программу и испытываете проблемы, при этом видите в логах что проблема связана с какой-то программой, используемой в качестве бекенда, попробуйте воспроизвести проблему, запустив программу-бекенд вручную, используя опции командной строки из логов. Независимо от того, удастся ли вам воспроизвести проблему или нет, вы можете сообщить о проблеме. Как именно вы это можете сделать смотрите в разделе [#Проблемы с записью](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D1.8C.D1.8E).

#### Особый случай: medium error / write error

Вот некоторые типичные сообщения о том, что вашему приводу не нравится конкретный носитель. Это можно исправить только используя другой привод или другой носитель. Смена программы вряд ли поможет.

K3b с _wodim_:

```
Sense Bytes: 70 00 03 00 00 00 00 12 00 00 00 00 0C 00 00 00
Sense Key: 0x3 Medium Error, Segment 0
Sense Code: 0x0C Qual 0x00 (write error) Fru 0x0

```

Brasero с _growisofs_:

```
BraseroGrowisofs stderr: :-[ WRITE@LBA=0h failed with SK=3h/ASC=0Ch/ACQ=00h]: Input/output error

```

Brasero с _libburn_:

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Optical_disc_drive_(Русский)&oldid=415675](https://wiki.archlinux.org/index.php?title=Optical_disc_drive_(Русский)&oldid=415675)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia (Русский)](/index.php/Category:Multimedia_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Multimedia (Русский)")
*   [Optical (Русский)](/index.php/Category:Optical_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Optical (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")