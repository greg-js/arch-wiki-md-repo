**Состояние перевода:** На этой странице представлен перевод статьи [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts"). Дата последней синхронизации: 4 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Java_Runtime_Environment_fonts&diff=0&oldid=403025).

Некоторые пользователи могут заметить, что шрифты в приложениях Java отображаются неприятно. Доступно несколько методов, чтобы улучшить отображение шрифтов в Oracle Java Runtime Environment (JRE). Эти методы могут использоваться по отдельности, но многие пользователи предпочтут использовать их вместе, чтобы получить лучший результат.

Для использования с Java, лучшим поддерживаемым форматом шрифтов будет TrueType.

## Contents

*   [1 Anti-aliasing (Сглаживание)](#Anti-aliasing_.28.D0.A1.D0.B3.D0.BB.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.29)
    *   [1.1 Базовые настройки](#.D0.91.D0.B0.D0.B7.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [1.2 Патч OpenJDK](#.D0.9F.D0.B0.D1.82.D1.87_OpenJDK)
*   [2 Выбор шрифта](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0)
    *   [2.1 Шрифты TrueType](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_TrueType)
    *   [2.2 Исправление Mojibake (для JRE8)](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_Mojibake_.28.D0.B4.D0.BB.D1.8F_JRE8.29)

## Anti-aliasing (Сглаживание)

### Базовые настройки

[Сглаживание](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization") доступно в Linux с версии Oracle Java 1.6 и OpenJDK. Чтобы сделать это в масштабе для всей системы, добавьте следующую строку в `/etc/environment`:

```
_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=*setting'*

```

Где `*setting*` это одно из значений:

| Установка | Описание |
| `off`, `false`, `default` | Без сглаживания |
| `on` | Полное сглаживание |
| `gasp` | Использовать встроенные в шрифт инструкции хинтинга |
| `lcd`, `lcd_hrgb` | Сглаживание настроенное для большинства популярных ЖК-мониторов |
| `lcd_hbgr`, `lcd_vrgb`, `lcd_vbgr` | Альтернативные настройки для ЖК-мониторов |

Параметры `gasp` и `lcd` в большинстве случаев хорошо работают.

Чтобы приложения Java ощущались и выглядели как GTK, замените следующей строкой:

```
_JAVA_OPTIONS='-Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel' 

```

**Обратите внимание:**

*   Описанные варианты работают только для приложений Java, которые используют их в GUI (графическом интерфейсе) Java, как например JDownloader; а не для приложений, которые используют Java только в качестве бакэнда, как OpenOffice.org и Matlab.
*   Шрифты **TrueType** содержат **g**rid-fitting **a**nd **s**can-conversion **p**rocedure (*GASP*) - таблицу с рекомендациями дизайнера для отображения шрифта в разных размерах pt. Для некоторых размеров рекомендуется использовать полное сглаживание, другим только хинтинг, а некоторые будут отображаться в виде растровых изображений. Для некоторых размеров шрифта, иногда используются комбинации.

Укажите переменную в командной строке перед выполнением (exectuable), чтобы попробовать новую настройку:

```
_JAVA_OPTIONS=*options* *exectuable* 

```

Перелогинтесь, чтобы изменения вступили в силу.

### Патч OpenJDK

В результате сглаживание может быть хуже нативных приложений, даже с принудительным сглаживанием в опциях Java. Это может быть исправлено с помощью патча (исправления) в OpenJDK, доступному в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"):

*   Исправленный **OpenJDK7** доступен как [jre7-openjdk-infinality](https://aur.archlinux.org/packages/jre7-openjdk-infinality/)
*   Исправленный **OpenJDK8** доступен как [jre8-openjdk-infinality](https://aur.archlinux.org/packages/jre8-openjdk-infinality/) (также доступны из [Неофициального репозитория Infinality](/index.php/Unofficial_user_repositories#infinality-bundle "Unofficial user repositories"))

Исправленные версии хорошо сочетаются с патчами [Infinality](/index.php/Infinality_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Infinality (Русский)") fontconfig и freetype.

## Выбор шрифта

### Шрифты TrueType

Некоторые приложения Java могут задать использование определенного шрифта TrueType; эти приложения должны быть в курсе пути каталога с нужным шрифтом. TrueType шрифты установлены в каталоге `/usr/share/fonts/TTF`. Добавьте следующую строку в `/etc/environment` чтобы включить эти шрифты.

```
JAVA_FONTS=/usr/share/fonts/TTF

```

Перелогинтесь, чтобы изменения вступили в силу.

### Исправление Mojibake (для JRE8)

Поместите файлы шрифтов в подкаталог. Создайте каталог, если он не существует.

```
/usr/lib/jvm/java-8-openjdk/jre/lib/fonts/fallback/

```