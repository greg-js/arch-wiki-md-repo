# MEncoder (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [DVD риппинг](/index.php/Optical_disc_drive_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#DVD "Optical disc drive (Русский)")
*   [MPlayer](/index.php/MPlayer "MPlayer")
*   [Video2dvdiso](/index.php/Video2dvdiso "Video2dvdiso")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

## Установка

Пакет MEncoder устанавливается из extra репозитория командой:

```
# pacman -S mencoder

```

## Основы

Основной синтаксис выглядит следующим образом:

```
mencoder исходное_видео.mpg -o новое_видео.avi -ovc видео_кодек -oac аудио_кодек -vf видео_фильтры -af аудио_фильтры -of контейнер

```

Чтобы узнать более подробную информацию о каждом из вышеперечисленных параметров укажите в командной строке после данного параметра значение help. Например:

```
mencoder -ovc help
mencoder -oac help
mencoder -vf help
mencoder -of help

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=MEncoder_(Русский)&oldid=412726](https://wiki.archlinux.org/index.php?title=MEncoder_(Русский)&oldid=412726)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia (Русский)](/index.php/Category:Multimedia_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Multimedia (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")