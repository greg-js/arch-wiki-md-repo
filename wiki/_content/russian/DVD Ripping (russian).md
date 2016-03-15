**Риппинг** (Ripping) -- это процесс извлечения аудио или видео информации на жёсткий диск, обычно из сменных носителей или мультимедиа потоков.

Как правило, в задаче риппинга DVD выделяют две проблемы:

1.  Извлечение данных -- копирование аудио и/или видео данных на жёсткий диск
2.  Перекодирование -- конвертирование извлечённых данных в желаемый формат

Одни утилиты выполняют обе задачи, другие же решают только одну из проблем.

## Contents

*   [1 dvdbackup](#dvdbackup)
*   [2 dvd::rip](#dvd::rip)
*   [3 HandBrake](#HandBrake)
*   [4 MEncoder](#MEncoder)
    *   [4.1 Dvd2Avi](#Dvd2Avi)
    *   [4.2 Графические оболочки MEncoder](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_MEncoder)

## dvdbackup

[dvdbackup](/index.php/Dvdbackup "Dvdbackup") позволяет извлечь данные с DVD или защищённого DVD (понадобится [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss)). dvdbackup может пригодиться для создания точных копий защищённых DVD, или же для подготовки расшифрованных данных для программ, которые не умеют работать с защищёнными дисками.

## dvd::rip

[dvdrip](https://www.archlinux.org/packages/?name=dvdrip) -- графическая оболочка для [transcode](https://www.archlinux.org/packages/?name=transcode). Вы можете использовать его для извлечения данных и кодирования "на лету".

Вам понадобятся следующие пакеты:

*   [dvdrip](https://www.archlinux.org/packages/?name=dvdrip): графическая оболочка (GTK) для [transcode](https://www.archlinux.org/packages/?name=transcode), которая выполняет извлечение и кодирование данных
*   [libdv](https://www.archlinux.org/packages/?name=libdv): программный кодек для DV video
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): если вы планируете кодировать видео в XviD, открытый кодек MPEG-4 (свободная альтернатива DivX)
*   [divx4linux](https://aur.archlinux.org/packages/divx4linux/): если вы планируете кодировать видео в DivX

Настройки dvd::rip, в большинстве своём, хорошо документированы или же очевидны. Но если вам всё-таки понадобится помощь, загляните [сюда](http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp).

Чаще всего весь риппинг DVD сводится к выбору желаемого кодека (или кодеков), заголовков и щелчку на кнопке "Rip".

## HandBrake

HandBrake -- многопоточный кодировщик видео, который поставляется как в консольном, так и в графическом варианте, вместе с большим количеством предустановленных настроек. Этот пакет доступен в репозитории extra: [handbrake](https://www.archlinux.org/packages/?name=handbrake).

```
# pacman -S handbrake

```

## MEncoder

MEncoder -- это свободная (GPL) утилита командной строки для (де)кодирования и фильтрации видео. Она тесно связана с MPlayer и может конвертировать все форматы, поддерживаемые MPlayer, во множество сжатых и несжатых форматов с использованием различных кодеков.

MEncoder включён в пакет [mplayer](https://www.archlinux.org/packages/?name=mplayer). Подробности можно узнать в [Вики Gentoo](http://en.gentoo-wiki.com/wiki/Mencoder).

### Dvd2Avi

Простой [bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)")-скрипт, использующий MEncoder, можно найти на странице [Dvd2Avi](/index.php/Dvd2Avi "Dvd2Avi").

### Графические оболочки MEncoder

Если вам не нравится командная строка, вы можете выбрать для себя одну из нескольких графических оболочек для MEncoder.

На официальной странице MPlayer есть [список](http://www.mplayerhq.hu/design7/projects.html#mencoder_frontends) доступных графических оболочек.