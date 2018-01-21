Related articles

*   [Шрифты](/index.php/%D0%A8%D1%80%D0%B8%D1%84%D1%82%D1%8B "Шрифты")
*   [Настройка шрифтов/Примеры](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%88%D1%80%D0%B8%D1%84%D1%82%D0%BE%D0%B2/%D0%9F%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B "Настройка шрифтов/Примеры")
*   [Infinality (Русский)](/index.php/Infinality_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Infinality (Русский)")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [Шрифты Microsoft](/index.php/%D0%A8%D1%80%D0%B8%D1%84%D1%82%D1%8B_Microsoft "Шрифты Microsoft")
*   [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description")
*   [Шрифты окружения Java Runtime](/index.php/%D0%A8%D1%80%D0%B8%D1%84%D1%82%D1%8B_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F_Java_Runtime "Шрифты окружения Java Runtime")

**Состояние перевода:** На этой странице представлен перевод статьи [Font configuration](/index.php/Font_configuration "Font configuration"). Дата последней синхронизации: 7 Декабря 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Font_configuration&diff=0&oldid=455396).

[Fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig/) - это библиотека, разработанная для предоставления списка доступных [шрифтов](/index.php/Fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fonts (Русский)") приложениям, а также для настройки того, как шрифты будут отображены: смотрите [Wikipedia:Fontconfig](https://en.wikipedia.org/wiki/Fontconfig "wikipedia:Fontconfig"). Библиотека FreeType [freetype2](https://www.archlinux.org/packages/?name=freetype2) отображает (рендерит) шрифты, основываясь на этих настройках.

Хотя Fontconfig является стандартом в современном Linux, некоторые приложения полагаются на оригинальном способе отбора шрифтов и отображения, в [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description").

Пакеты отображения шрифтов на Arch Linux включает в себя поддержку *freetype2* с включенным переводчиком байт-кода (BCI). Для лучшего отображения шрифтов, особенно на ЖК-мониторах, см [#Настройка Fontconfig](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Fontconfig) и [Настройка шрифтов/Примеры](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%88%D1%80%D0%B8%D1%84%D1%82%D0%BE%D0%B2/%D0%9F%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B "Настройка шрифтов/Примеры").

## Contents

*   [1 Пути шрифтов](#.D0.9F.D1.83.D1.82.D0.B8_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
*   [2 Настройка Fontconfig](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Fontconfig)
    *   [2.1 Предварительные установки](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B2.D0.B0.D1.80.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [2.2 Anti-aliasing (сглаживание)](#Anti-aliasing_.28.D1.81.D0.B3.D0.BB.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.29)
    *   [2.3 Hinting (Хинтинг)](#Hinting_.28.D0.A5.D0.B8.D0.BD.D1.82.D0.B8.D0.BD.D0.B3.29)
        *   [2.3.1 Байт-код Переводчик (Byte-Code Interpreter, BCI)](#.D0.91.D0.B0.D0.B9.D1.82-.D0.BA.D0.BE.D0.B4_.D0.9F.D0.B5.D1.80.D0.B5.D0.B2.D0.BE.D0.B4.D1.87.D0.B8.D0.BA_.28Byte-Code_Interpreter.2C_BCI.29)
        *   [2.3.2 Autohinter (Авто Хинтинг)](#Autohinter_.28.D0.90.D0.B2.D1.82.D0.BE_.D0.A5.D0.B8.D0.BD.D1.82.D0.B8.D0.BD.D0.B3.29)
        *   [2.3.3 Hintstyle (Стиль Хинтинга)](#Hintstyle_.28.D0.A1.D1.82.D0.B8.D0.BB.D1.8C_.D0.A5.D0.B8.D0.BD.D1.82.D0.B8.D0.BD.D0.B3.D0.B0.29)
    *   [2.4 Субпиксельное отображение](#.D0.A1.D1.83.D0.B1.D0.BF.D0.B8.D0.BA.D1.81.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
        *   [2.4.1 LCD filter (ЖК-фильтр)](#LCD_filter_.28.D0.96.D0.9A-.D1.84.D0.B8.D0.BB.D1.8C.D1.82.D1.80.29)
        *   [2.4.2 Расширенная спецификация ЖК-фильтра (LCD filter)](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D1.81.D0.BF.D0.B5.D1.86.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_.D0.96.D0.9A-.D1.84.D0.B8.D0.BB.D1.8C.D1.82.D1.80.D0.B0_.28LCD_filter.29)
    *   [2.5 Отключение авто хинтинга (auto-hinter) для жирных (bold) шрифтов](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE_.D1.85.D0.B8.D0.BD.D1.82.D0.B8.D0.BD.D0.B3.D0.B0_.28auto-hinter.29_.D0.B4.D0.BB.D1.8F_.D0.B6.D0.B8.D1.80.D0.BD.D1.8B.D1.85_.28bold.29_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
    *   [2.6 Заменить или установить шрифты по умолчанию](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D0.B8.D0.BB.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [2.7 Белый список и чёрный список шрифтов](#.D0.91.D0.B5.D0.BB.D1.8B.D0.B9_.D1.81.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.B8_.D1.87.D1.91.D1.80.D0.BD.D1.8B.D0.B9_.D1.81.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
    *   [2.8 Отключение растровых шрифтов](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B2.D1.8B.D1.85_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
    *   [2.9 Отключить масштабирование растровых шрифтов](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D0.BC.D0.B0.D1.81.D1.88.D1.82.D0.B0.D0.B1.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B2.D1.8B.D1.85_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
    *   [2.10 Создать стили для жирных и курсивных «некомплектных» шрифтов](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D1.82.D1.8C_.D1.81.D1.82.D0.B8.D0.BB.D0.B8_.D0.B4.D0.BB.D1.8F_.D0.B6.D0.B8.D1.80.D0.BD.D1.8B.D1.85_.D0.B8_.D0.BA.D1.83.D1.80.D1.81.D0.B8.D0.B2.D0.BD.D1.8B.D1.85_.C2.AB.D0.BD.D0.B5.D0.BA.D0.BE.D0.BC.D0.BF.D0.BB.D0.B5.D0.BA.D1.82.D0.BD.D1.8B.D1.85.C2.BB_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
    *   [2.11 Изменение главного правила](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B3.D0.BB.D0.B0.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D0.B0)
    *   [2.12 Запрос текущих настроек](#.D0.97.D0.B0.D0.BF.D1.80.D0.BE.D1.81_.D1.82.D0.B5.D0.BA.D1.83.D1.89.D0.B8.D1.85_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
*   [3 Приложения без поддержки fontconfig](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_fontconfig)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Искаженные шрифты](#.D0.98.D1.81.D0.BA.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [4.2 Calibri, Cambria, Monaco, и т. д. не отображаются правильно](#Calibri.2C_Cambria.2C_Monaco.2C_.D0.B8_.D1.82._.D0.B4._.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE)
    *   [4.3 Приложения переопределяют hinting](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.B5.D1.80.D0.B5.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.8F.D1.8E.D1.82_hinting)
    *   [4.4 Приложения не используют hinting из настроек DE](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BD.D0.B5_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8E.D1.82_hinting_.D0.B8.D0.B7_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_DE)
    *   [4.5 Неправильный hinting в приложениях GTK на НЕ-Gnome системах](#.D0.9D.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_hinting_.D0.B2_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.D1.85_GTK_.D0.BD.D0.B0_.D0.9D.D0.95-Gnome_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0.D1.85)
    *   [4.6 Проблема шрифтов в Сгенерированных файлах PDF](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2_.D0.B2_.D0.A1.D0.B3.D0.B5.D0.BD.D0.B5.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0.D1.85_PDF)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Пути шрифтов

Шрифты, которые будут известны приложениям, должны быть каталогизированы для лёгкого и быстрого доступа.

Пути шрифтов изначально известные Fontconfig находятся в: `/usr/share/fonts/`, `~/.local/share/fonts` (и `~/.fonts/`, - в настоящее время не рекомендуется). Fontconfig будет сканировать эти каталоги рекурсивно. Для простоты организации и установки, рекомендуется использовать эти пути шрифтов, когда [добавляете шрифты](/index.php/Fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0 "Fonts (Русский)").

Чтобы увидеть список известных Fontconfig шрифтов:

```
$ fc-list : file

```

Для больших выводных форматов, смотрите [fc-list(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fc-list.1).

Проверьте известные пути шрифтов Xorg, посмотрев свой журнал:

```
$ grep /fonts /var/log/Xorg.0.log

```

**Совет:**

*   Вы также можете проверить список [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")'а на наличие известных путей шрифтов с помощью команды `xset q`.
*   Используйте `/var/log/Xorg.0.log` если Xorg запускается с правами суперпользователя.

Имейте в виду, что Xorg не ищет рекурсивно в каталоге `/usr/share/fonts/` как это делает Fontconfig. Чтобы добавить путь, нужно указать полный путь:

```
Section "Files"
    FontPath     "/usr/share/fonts/local/"
EndSection

```

Если вы хотите установить пути шрифтов на уровне пользователя, вы можете добавлять и удалять пути шрифтов по умолчанию, добавив следующую строку(и) в `~/.xinitrc`:

```
xset +fp /usr/share/fonts/local/           # Добавляет привычный путь шрифтов в список Xorg'а известных путей шрифтов
xset -fp /usr/share/fonts/sucky_fonts/     # Удаляет указанный путь шрифта из списка Xorg'а известных путей шрифтов

```

Чтобы увидеть список известных шрифтов Xorg используйте `xlsfonts`, из пакета [xorg-xlsfonts](https://www.archlinux.org/packages/?name=xorg-xlsfonts).

## Настройка Fontconfig

Fontconfig описан на странице man [fonts-conf](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html).

Настройка может быть сделана для каждого пользователя отдельно, с помощью `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, и на глобальном уровне с помощью `/etc/fonts/local.conf`. Установки в настройках для каждого пользователя, имеют приоритет над глобальной настройкой. Оба эти файла используют тот же синтаксис.

**Примечание:** Файлы настроек и каталоги: `~/.fonts.conf/`, `~/.fonts.conf.d/` и `~/.fontconfig/*.cache-*` являются устаревшими с версии [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 2.10.1 ([переданной в апстрим](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb185d5651b57380b0a9443001e8051b29d)) и не будут прочитаны по умолчанию в будущих версиях пакета. Новые пути в `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, `$XDG_CONFIG_HOME/fontconfig/conf.d/NN-name.conf` и `$XDG_CACHE_HOME/fontconfig/*.cache-*` соответственно. Если используется второе расположение, убедитесь в правильном названии файла (где `NN` состоит из двух цифр, как `00`, `10`, или `99`).

Fontconfig собирает все свои настройки в центральном файле (`/etc/fonts/fonts.conf`). Этот файл заменяется в ходе обновления fontconfig и не должен быть отредактирован. Fontconfig-совместимые приложения читают этот файл, чтобы узнать о доступных шрифтах и как они будут отображены. Этот файл представляет собой конгломерат из правил глобальных настроек (`/etc/fonts/local.conf`), настроенные предустановки в `/etc/fonts/conf.d/`, и пользовательском файле настроек (`$XDG_CONFIG_HOME/fontconfig/fonts.conf`). `fc-cache` может быть использован для восстановления настроек fontconfig, хотя изменения будут видны только в недавно запущенных приложениях.

**Примечание:** Для некоторых рабочих сред (например [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)")) используется *Панель Управления Шрифтами* которая будет автоматически создавать или перезаписывать файл настроек шрифта пользователя. Для этих рабочих сред, лучше чтобы настройки соответствовали вашим уже определённым настройкам шрифтов, чтобы получить ожидаемое поведение.

Файлы настроек Fontconfig используют формат [XML](https://en.wikipedia.org/wiki/ru:XML "wikipedia:ru:XML") и обязательный заголовок:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- поместите настройки сюда -->

</fontconfig>

```

Примеры настроек в этой статье, пропускают эти тэги.

### Предварительные установки

Предварительные установки есть в каталоге `/etc/fonts/conf.avail`. Они могут быть включены созданием [символьной ссылки](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%B8%D0%BC%D0%B2%D0%BE%D0%BB%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F_%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "w:ru:Символическая ссылка") на них, для каждого пользователя и глобально, как описано в `/etc/fonts/conf.d/README`. Эти предварительные установки переопределят соответствие параметров в соответствующих файлах настроек.

Например, для включения sub-pixel (суб-пиксельного) RGB отображения глобально:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/10-sub-pixel-rgb.conf

```

Тоже самое, но для настройки каждому пользователю:

```
$ mkdir $XDG_CONFIG_HOME/fontconfig/conf.d
$ ln -s /etc/fonts/conf.avail/10-sub-pixel-rgb.conf $XDG_CONFIG_HOME/fontconfig/conf.d

```

### Anti-aliasing (сглаживание)

[Растеризация шрифтов](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization") преобразует данные векторного шрифта в растровые, так что они могут быть отображены. В результате могут появиться ступеньки/зубцы, из-за [наложения (алиасинга)](https://en.wikipedia.org/wiki/ru:%D0%90%D0%BB%D0%B8%D0%B0%D1%81%D0%B8%D0%BD%D0%B3 "wikipedia:ru:Алиасинг"). Методика известна как [Анти-алиасинг/сглаживание (Anti-aliasing)](https://en.wikipedia.org/wiki/Anti-aliasing "wikipedia:Anti-aliasing"), и может быть использована для повышения разрешения видимых краев шрифта. Сглаживание **включено (true)** по умолчанию. Для того, чтобы отключить его:

```
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

```

**Примечание:** некоторые приложения, такие как [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") могут [переопределить настройки сглаживания по умолчанию](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC).

### Hinting (Хинтинг)

[Хинтование шрифта](https://en.wikipedia.org/wiki/ru:%D0%A5%D0%B8%D0%BD%D1%82%D0%B8%D0%BD%D0%B3 "wikipedia:ru:Хинтинг") (также известное как инструктаж) - это использование математических инструкций для настройки отображения контура шрифта так, чтобы он был на одной линии с растрировой сеткой (т.е. пиксельной сеткой экрана). Ожидаемый эффект, - сделать шрифты на вид более чёткими, чтобы они были более читабельные. Шрифты выравниваются правильно без хинтинга, когда экран имеет 300 [DPI](https://en.wikipedia.org/wiki/ru:Dots_per_inch "wikipedia:ru:Dots per inch"). Доступно два типа Хинтинга.

#### Байт-код Переводчик (Byte-Code Interpreter, BCI)

Использование хинтинга BCI. Инструкции в шрифтах TrueType предоставляются в соответствии с интерпретатором FreeTypes. Хинтинг BCI прекрасно работает со шрифтами с хорошими инструкциями хинтинга. По умолчанию хинтинг **включен (enabled)**. Для его отключения:

```
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

```

#### Autohinter (Авто Хинтинг)

Autohinter пытается сделать автоматический хинтинг и игнорирует существующую информацию хинтинга. Первоначально это было по умолчанию, поскольку шрифты TrueType2 были защищены патентом, но теперь срок патентов истёк, и там очень мало оснований, чтобы использовать Авто Хинтинг. Это лучше работает со шрифтами, которые поломанные или не содержат информацию по хинтингу, но это будет не оптимально для шрифтов с хорошей информацией хинтинга. К распространённым шрифтам Авто Хинтинг в дальейшем не будет полезным. По умолчанию автохинтинг **отключен (disabled)**. Чтобы его включить:

```
  <match target="font">
    <edit name="autohint" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### Hintstyle (Стиль Хинтинга)

Hintstyle это сумма изменений шрифта, сделанных чтобы выстроить его по пиксельной сетке. Значения хинтинга: `hintnone`(без хинтинга), `hintslight`(лёгкий хинтинг), `hintmedium`(средний хинтинг), и `hintfull`(полный хинтинг). `hintslight` сделает шрифт более нечётким выстраивая по сетке, но сохранит лучше форму шрифта, в то время как `hintfull` сделает чётким шрифт, выровняет хорошо по пиксельной сетке, но больше потеряет форму шрифта. **`hintslight`** установлен по умолчанию. Для того, чтобы изменить его:

```
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintnone</const>
    </edit>
  </match>

```

**Примечание:** некоторые приложения, такие как [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") могут [переопределить настройки хинтинга по умолчанию](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC).

### Субпиксельное отображение

Большинство мониторов производятся сегодня используя спецификацию RGB (Red, Green, Blue, - Красный, Зелёный, Синий). Fontconfig'у нужно знать свой тип монитора, чтобы иметь возможность отображать шрифты правильно. Мониторы могут быть: **RGB** (наиболее распространенный), **BGR**, **V-RGB** (вертикальный), или даже **V-BGR**. Тест монитора можно найти [здесь](http://www.lagom.nl/lcd-test/subpixel.php).

Чтобы включить субпиксельное отоброжение:

```
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

```

**Примечание:** Subpixel rendering effectively triples the horizontal (or vertical) resolution for fonts by making use of subpixels. The default autohinter and subpixel rendering are not designed to work together, hence you will want to enable the subpixel autohinter. Prior to [freetype2](https://www.archlinux.org/packages/?name=freetype2) 2.7, the subpixel hinting mode was configurable with the `FT2_SUBPIXEL_HINTING` [environment variable](/index.php/Environment_variable "Environment variable"). Possible values were `0` (disabled), `1` (Infinality) and `2` (minimal). From [freetype2](https://www.archlinux.org/packages/?name=freetype2) 2.7, subpixel hinting uses upstream's configuration method, which has a different syntax. Subpixel hinting mode configured in the file `/etc/profile.d/freetype2.sh` which includes a brief documentation. Possible values are `truetype:interpreter-version=35` (classic mode/2.6 default), `truetype:interpreter-version=38` ("Infinality" mode), `truetype:interpreter-version=40` (minimal mode/2.7 default).

#### LCD filter (ЖК-фильтр)

При использовании субпиксельного отображения, необходимо включить ЖК-фильтр, который предназначен для снижения цветной окантовки. Это описано в разделе [ЖК-фильтр](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html) в справке по FreeType 2 API. Различные варианты описаны в разделе [FT_LcdFilter](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html#FT_LcdFilter), и проиллюстрированы на этой [странице теста ЖК-фильтра](http://www.spasche.net/files/lcdfiltering/).

Фильтр `lcddefault` будет работать для большинства пользователей. Другие доступные фильтры, которые могут использоваться в особых случаях: `lcdlight`; фильтр идеально подходит для шрифтов, которые выглядят слишком жирными или нечеткими, `lcdlegacy`, оригинальный фильтр Cairo; и `lcdnone` чтобы отключить его полностью.

```
  <match target="font">
      <edit name="lcdfilter" mode="assign">
      <const>lcddefault</const>
    </edit>
  </match>

```

#### Расширенная спецификация ЖК-фильтра (LCD filter)

Если налицо, встроенные ЖК-фильтры не являются удовлетворительными, можно настроить отображение шрифта очень особенно, путем создания пользовательского пакета freetype2 и модификации жестко закодированных фильтров. [Система сборки Arch](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") может быть использована для создания и установки пакетов из исходников.

**Совет:** С пакетами [Infinality](/index.php/Infinality_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Infinality (Русский)"), ЖК-фильтр может быть изменён без пересборки.

Во-первых, обновите freetype2 PKGBUILD как root:

```
# abs extra/freetype2

```

Этот пример использует `/var/abs/build` в качестве каталога сборки, замените его в соответствии с вашей личной настройкой ABS. Загрузите и извлеките пакет freetype2 как обычный пользователь:

```
$ cd /var/abs/build
$ cp -r ../extra/freetype2 .
$ cd freetype2
$ makepkg -o

```

Отредактируйте файл `src/freetype-VERSION/src/base/ftlcdfil.c` и найдите определённые константы `default_filter[5]`:

```
static const FT_Byte  default_filter[5] =
    { 0x10, 0x40, 0x70, 0x40, 0x10 };

```

Эта константа определяет применение низкочастотного фильтра к отоброжению символа. Изменить его по мере необходимости. Сохраните файл, соберите и установите пользовательский пакет:

```
$ makepkg -e
# pacman -Rd freetype2
# pacman -U freetype2-VERSION-ARCH.pkg.tar.xz

```

Перезагрузитесь или перезапустите X. Теперь фильтр lcddefault должен отобразить шрифты по-другому.

### Отключение авто хинтинга (auto-hinter) для жирных (bold) шрифтов

Авто хинтинг использует сложные методы для отображения шрифтов, но часто делает жирные шрифты слишком широкими. К счастью, решение может быть найдено в отключении авто хинтинга для жирных шрифтов, оставляя авто хинтинг для остальных:

```
...
<match target="font">
    <test name="weight" compare="more">
        <const>medium</const>
    </test>
    <edit name="autohint" mode="assign">
        <bool>false</bool>
    </edit>
</match>
...

```

### Заменить или установить шрифты по умолчанию

Самый надёжный способ сделать это, добавить фрагмент XML, похожий на тот, как показано ниже. *Использование атрибута "binding" (связывания) даст вам лучший результат, например, в Firefox где вы не можете изменить замену шрифтов.* Это приведёт к использованию Ubuntu, вместо того чтобы использовать Georgia:

```
...
 <match target="pattern">
   <test qual="any" name="family"><string>georgia</string></test>
   <edit name="family" mode="assign" binding="same"><string>Ubuntu</string></edit>
 </match>
...

```

Альтернативный подход состоит в установке "предпочтительного" шрифта, но *это работает только если оригинального шрифта нет в системе*, в этом случае заданный шрифт будет заменен:

```
...
<!-- Заменить Helvetica на Bitstream Vera Sans Mono -->
<!-- Обратите внимание, что псевдоним для Helvetica должен уже существовать по умолчанию в файлах настроек -->
<alias>
    <family>Helvetica</family>
    <prefer><family>Bitstream Vera Sans Mono</family></prefer>
    <default><family>fixed</family></default>
</alias>
...

```

### Белый список и чёрный список шрифтов

Элемент `<selectfont>` используется в сочетании с элементами выбора: `<acceptfont>` и `<rejectfont>`, - белого списка или черного списка шрифтов, для принятия перечня и согласования запросов. Самый простой и наиболее типичным случай использования его для `<rejectfont>` (отклонения) одного шрифта, который должен быть установлен, однако выходит сопоставимым со стандартным запросом шрифту, который вызывает проблемы в пользовательских интерфейсах. Во-первых, получите имя Family (семейства) как указано в самом шрифте:

 `$ fc-scan .fonts/lklug.ttf --format='%{family}
'`  `LKLUG` 

Затем используйте это имя Family в строфе `<rejectfont>`:

```
<selectfont>
    <rejectfont>
        <pattern>
            <patelt name="family" >
                <string>LKLUG</string>
            </patelt>
        </pattern>
    </rejectfont>
</selectfont>

```

Обычно, когда оба элемента объединены, `<rejectfont>` сначала используется в более общем согласовании glob для reject (отклонения) большой группы (таких, как целый каталог), затем после него используется `<acceptfont>` белый список отдельных шрифтов из большой группы чёрного списка.

```
<selectfont>
    <rejectfont>
        <glob>/usr/share/fonts/OTF/*</glob>
    </rejectfont>
    <acceptfont>
        <pattern>
            <patelt name="family" >
                <string>Monaco</string>
            </patelt>
        </pattern>
    </acceptfont>
</selectfont>

```

### Отключение растровых шрифтов

Чтобы отключить растровые шрифты (которые иногда используются в качестве «резерва» вместо отсутствующих шрифтов, в результате чего текст будет отображён некачественно), используйте `70-no-bitmaps.conf` (который не размещается в FontConfig по умолчанию):

Растровые шрифты иногда используются в качестве резервных шрифтов, заместо отсутствующих/недоступных шрифтов, которые могут делать текст пиксельным (со ступеньками), или слишком большим. Чтобы отключить такое поведение, используйте `70-no-bitmaps.conf` [#Предварительные установки](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B2.D0.B0.D1.80.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8).

Чтобы отключить встроенные растровые шрифты у всех шрифтов:
 `~/.config/fontconfig/conf.d/20-no-embedded.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit name="embeddedbitmap" mode="assign">
      <bool>false</bool>
    </edit>
  </match>
</fontconfig>

```

Чтобы отключить встроенные растровые шрифты для определенного шрифта:

```
<match target="font">
  <test qual="any" name="family">
    <string>Monaco</string>
  </test>
  <edit name="embeddedbitmap"><bool>false</bool></edit>
</match>

```

### Отключить масштабирование растровых шрифтов

Чтобы отключить масштабирование растровых шрифтов (которое часто делает их размытыми), удалите `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`.

### Создать стили для жирных и курсивных «некомплектных» шрифтов

FreeType имеет возможность автоматически создавать *italic* (курсивные) и **bold** (жирные) стили для шрифтов, которые не имеют их, но только если это явно требуется приложению. Данные программы редко отправляют эти запросы. В этом разделе охватывается принуждение «вручную» генерировать отсутствующие стили.

Начните редактировать `/usr/share/fonts/fonts.cache-1` как описано ниже. Храните изменённые копии в другом файле, поскольку обновление шрифтов с помощью `fc-cache` будет перезаписывать `/usr/share/fonts/fonts.cache-1`.

Предположим что шрифт Dupree установлен:

```
"dupree.ttf" 0 "Dupree:style=Regular:slant=0:weight=80:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Дублируйте строку, измените `style=Regular` на `style=Bold` или любой другой стиль. Также измените `slant=0` на `slant=100` для italic (курсива), `weight=80` на `weight=200` для bold (жирного), или объедините их для ***bold italic*** (жирного курсива):

```
"dupree.ttf" 0 "Dupree:style=Bold Italic:slant=100:weight=200:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Теперь добавьте необходимые изменения в`$XDG_CONFIG_HOME/fontconfig/fonts.conf`:

```
...
<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
         <!-- other fonts here .... -->
     </test>
     <test name="weight" compare="more_eq"><int>140</int></test>
     <edit name="embolden" mode="assign"><bool>true</bool></edit>
</match>

<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
        <!-- other fonts here .... -->
    </test>
    <test name="slant" compare="more_eq"><int>80</int></test>
    <edit name="matrix" mode="assign">
        <times>
            <name>matrix</name>
                <matrix>
                    <double>1</double><double>0.2</double>
                    <double>0</double><double>1</double>
                </matrix>
        </times>
    </edit>
</match>
...

```

**Совет:** Используйте значение 'embolden' для существующих bold (жирный) шрифтов, для того чтобы сделать их ещё жирнее.

### Изменение главного правила

Fontconfig обрабатывает файлы `/etc/fonts/conf.d` в числовом порядке. Это позволяет правилам или файлам переопределять друг друга, но часто сбивает пользователей с толку о том, какой файл будет анализарован последним.

Чтобы гарантировать, что персональные настройки имеют приоритет над любыми другими правилами, измените их порядок:

```
# cd /etc/fonts/conf.d
# mv 50-user.conf 99-user.conf

```

Это изменение окажется ненужным в большинстве случаев, так как пользователь получит достаточно контроля по умолчанию, чтобы установить собственные предпочтения шрифта. Такие как: хинтинг, свойства сглаживания, псевдонимы новых шрифтов в общих семействах шрифтов и т. д.

### Запрос текущих настроек

Чтобы узнать, какие настройки вступили в силу, используйте`fc-match --verbose`. К примеру:

```
$ fc-match --verbose Sans
family: "DejaVu Sans"(s)
hintstyle: 3(i)(s)
hinting: True(s)
...

```

Посмотрите значения чисел в [http://www.freedesktop.org/software/fontconfig/fontconfig-user.html](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html). Например. 'hintstyle: 3' означает 'hintfull'

## Приложения без поддержки fontconfig

Некоторые приложения, как [Urxvt](/index.php/Rxvt-unicode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Rxvt-unicode (Русский)") игнорируют настройки fontconfig. Вы можете обойти эту проблему с помощью `~/.Xresources`, который такой же гибкий как fontconfig. Как пример (смотрите [#Настройка Fontconfig](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Fontconfig)), и для объяснения вариантов :

 `~/.Xresources` 
```
Xft.autohint: 0
Xft.lcdfilter: lcddefault
Xft.hintstyle: hintslight
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Убедитесь, что настройки загружаются должным образом, когда запускается X с `xrdb -q` (для получения дополнительной информации смотрите статью [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х")).

## Решение проблем

### Искаженные шрифты

**Примечание:** 96 DPI не является стандартом. Вы должны использовать фактическое DPI монитора, чтобы получить надлежащее отображение шрифтов, особенно при использовании субпиксельного отображения.

Если шрифты еще неожиданно большие или маленькие, с плохими пропорциями или просто отображаются плохо, то Fontconfig может использовать неверный DPI.

Fontconfig должен быть в состоянии определить параметры DPI, обнаруженные сервером Xorg. Вы можете проверить автоматическое обнаружение DPI с помощью `xdpyinfo` (предоставляется пакетом [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo)):

 `$ xdpyinfo | grep dots` 
```
  resolution:    102x102 dots per inch

```

Если DPI определяется некорректно (обычно из-за неправильного [EDID](https://en.wikipedia.org/wiki/ru:Extended_display_identification_data "wikipedia:ru:Extended display identification data") монитора), вы можете указать его вручную в настройках Xorg, смотрите [Размер дисплея/DPI](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D0.B7.D0.BC.D0.B5.D1.80_.D0.B4.D0.B8.D1.81.D0.BF.D0.BB.D0.B5.D1.8F.2FDPI "Xorg (Русский)"). Это рекомендуемое решение, но оно не может работать c драйверами, в которых есть баги/ошибки.

Fontconfig пользуется по умолчанию переменной Xft.dpi, если она установлена. Xft.dpi обычно устанавливается окружением рабочего стола (обычно в настройках DPI Xorg'а) либо вручную в `~/.Xdefaults` или `~/.Xresources`. Воспользуйтесь xrdb для получения значения:

 `$ xrdb -query | grep dpi` 
```
Xft.dpi:	102

```

Те, кто еще имеют проблемы, могут вернуться к ручной установке DPI используя FontConfig:

```
...
<match target="pattern">
   <edit name="dpi" mode="assign"><double>102</double></edit>
</match>
...

```

### Calibri, Cambria, Monaco, и т. д. не отображаются правильно

Некоторые масштабируемые шрифты имеют встроенные растровые версии, которые предоставляются, главным образом, при меньших размерах. В этом случае использование [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts") в качестве замены, может улучшить отображение.

You can also force using scalable fonts at all sizes by [disabling embedded bitmap](#Disable_bitmap_fonts), sacrificing some rendering quality.

### Приложения переопределяют hinting

Некоторые приложения или окружения рабочего стола, по умолчанию, могут переопределять настройки fontconfig, такие как хинтинг и сглаживание. Это может случится с [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") 3, например когда вы используете приложения Qt, как [vlc](https://www.archlinux.org/packages/?name=vlc) или [smplayer](https://www.archlinux.org/packages/?name=smplayer). В таких случаях используйте специальную программу для применения настроек. Для GNOME, попробуйте [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) и установите сглаживание в `Rgba` вместо установленного по умолчанию `Grayscale`.

### Приложения не используют hinting из настроек DE

Например, в GNOME иногда случается, что Firefox применяет полный хинтинг (full hinting) даже если он установлен на "none" в настройках GNOME, что в результате приводит к резким и широким шрифтам. В этом случае вам придётся добавить настройку хинтинга в ваш файл `fonts.conf`:

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>	
<fontconfig>
 <match target="font">
  <edit mode="assign" name="hinting">
   <bool>false</bool>
  </edit>
 </match>
</fontconfig>

```

В этом примере хинтинг установлен на "grayscale".

### Неправильный hinting в приложениях GTK на НЕ-Gnome системах

[GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") использует систему настройки отображения шрифтов XSETTINGS. Без gnome-settings-daemon, приложения GTK полагаются на fontconfig, но некоторые шрифты получают неправильный хинтинг, заставляя их выглядеть слишком жирными или светлыми.

Простым решением, в качестве замены gnome-settings-daemon, будет использование [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/) чтобы предоставить настройки, например:

 `~/.xsettingsd` 
```
Xft/Hinting 1
Xft/RGBA "rgb"
Xft/HintStyle "hintslight"
Xft/Antialias 1

```

Или вы можете написать настройки шрифтов, как директивы `Xft.*` в `~/.Xresources` без использования настроек демона.

### Проблема шрифтов в Сгенерированных файлах PDF

Если следующая команда

```
fc-match helvetica

```

создаёт

```
helvR12-ISO8859-1.pcf.gz: "Helvetica" "Regular"

```

то, скорее всего, растровый шрифт обеспечивается [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi), шрифт будет встроен в PDF сгенерированный каким-либо приложением с помощью "Печать в файл" или "Экспорт". Скорее всего растровый шрифт был установлен в результате установки всей группы [xorg](https://www.archlinux.org/groups/x86_64/xorg/) (что обычно НЕ рекомендуется). Чтобы решить проблему растровых шрифтов, вы можете удлить пакет. Установите [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) (Type 1) или [tex-gyre-fonts](https://www.archlinux.org/packages/?name=tex-gyre-fonts) (OpenType) для соответствующей свободной замены Helvetica (и других шрифтоф на основе PostScript/PDF).

Также эта проблема может появится при открытии PDF, которому требуется Helvetica, и он не встроен для просмотра.

## Смотрите также

*   [Пользовательское руководство Fontconfig (Англ.)](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html)
*   [Fonts in X11R6.8.2](http://www.x.org/X11R6.8.2/doc/fonts.html) - Официальная информаци по шрифтам Xorg (Англ.)
*   [обзор FreeType 2 (Англ.)](http://freetype.sourceforge.net/freetype2/)
*   [Дискуссия Gentoo об отображении шрифтов (Англ.)](https://forums.gentoo.org/viewtopic-t-723341.html)
*   [On slight hinting](http://www.freetype.org/freetype2/docs/text-rendering-general.html)