**Состояние перевода:** На этой странице представлен перевод статьи [Desktop entries](/index.php/Desktop_entries "Desktop entries"). Дата последней синхронизации: 12 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Desktop_entries&diff=0&oldid=481786).

Спецификация freedesktop [ярлык приложения](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) предусматривает стандарт для приложений для интеграции в [среду рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"). Ярлыки приложений - это файлы конфигурации, описывающие, как запускается приложение, и какие данные оно может обрабатывать. Они также настраивают, как появляются приложения в меню со значком, на который распространяется соответствующий стандарт [спецификации меню](https://specifications.freedesktop.org/menu-spec/menu-spec-latest.html).

Наиболее распространенные ярлыки приложений представлены файлами `.desktop` и `.directory`. В этой статье кратко объясняется, как создавать полезные и соответствующие стандарту ярлыки приложений. Она в основном предназначена для разработчиков и сопровождающих пакетов(ы), но может также быть полезна разработчикам программного обеспечения и другим.

Существует примерно три типа ярлыков приложений:

	Приложение

	ярлык приложения

	Ссылка

	ярлык на веб-ссылку

	Каталог

	контейнер метаданных в меню

В следующих разделах будет примерно показано, как они создаются и проверяются.

Связанное с этим материалом, а также определенные в файлах `.desktop`, являются ассоциациями типа MIME для файлов данных. [Приложения по умолчанию](/index.php/Default_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Default applications (Русский)") описывают, как они настроены.

## Contents

*   [1 Ярлык приложения](#.D0.AF.D1.80.D0.BB.D1.8B.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [1.1 Пример файла](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0)
    *   [1.2 Определение ключа](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D1.8E.D1.87.D0.B0)
        *   [1.2.1 Осуждение](#.D0.9E.D1.81.D1.83.D0.B6.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Значки](#.D0.97.D0.BD.D0.B0.D1.87.D0.BA.D0.B8)
    *   [2.1 Распространенные форматы изображений](#.D0.A0.D0.B0.D1.81.D0.BF.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.8B_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [2.2 Преобразование значков](#.D0.9F.D1.80.D0.B5.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.BD.D0.B0.D1.87.D0.BA.D0.BE.D0.B2)
    *   [2.3 Получение значков](#.D0.9F.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.BD.D0.B0.D1.87.D0.BA.D0.BE.D0.B2)
*   [3 Инструменты](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B)
    *   [3.1 gendesk](#gendesk)
        *   [3.1.1 Как использовать](#.D0.9A.D0.B0.D0.BA_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D1.8C)
    *   [3.2 Список или поиск в файлах .desktop](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.B8.D0.BB.D0.B8_.D0.BF.D0.BE.D0.B8.D1.81.D0.BA_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0.D1.85_.desktop)
    *   [3.3 fbrokendesktop](#fbrokendesktop)
*   [4 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 Скрытие ярлыков приложений](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D1.8F.D1.80.D0.BB.D1.8B.D0.BA.D0.BE.D0.B2_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [4.2 Автозапуск](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
    *   [4.3 Изменение переменных среды](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D1.81.D1.80.D0.B5.D0.B4.D1.8B)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Ярлык приложения

Ярлыки для приложений или файлов `.desktop`, как правило, представляют собой комбинацию метаинформационных ресурсов и ярлыков приложений. Эти файлы обычно находятся в `/usr/share/applications` или `/usr/local/share/applications` для приложений, установленных в системе, или `~/.local/share/applications` для пользовательских приложений. Пользовательские ярлыки имеют приоритет над системными ярлыками.

### Пример файла

Ниже приведен пример его структуры с дополнительными комментариями. Этот пример предназначен только для быстрого ознакомления и не показывает, как использовать все возможные ключи ввода. Полный список ключей можно найти в [спецификация freedesktop.org](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#recognized-keys).

```
[Desktop Entry]

# Определение типа ярлыка приложений
Type=Application

# Версия спецификации ярлыков приложений, которой соответствует этот файл
Version=1.0

# Название приложения
Name=jMemorize

# Комментарий, который может/будет использоваться в качестве подсказки
Comment=Flash card based learning tool

# Путь к папке, в которой выполняется исполняемый файл
Path=/opt/jmemorise

# Исполняемый файл приложения, возможно с аргументами.
Exec=jmemorize

# Имя значка, который будет использоваться для отображения этого ярлыка.
Icon=jmemorize

# Описывает, должно ли это приложение запускаться в терминале или нет
Terminal=false

# Описывает категории, в которых должна отображаться этот ярлык
Categories=Education;Languages;Java;

```

### Определение ключа

Все признанные Desktop ярлыки приложений можно найти на сайте [freedesktop.org](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#recognized-keys). Например, ключ `Type` определяет три типа ярлыков: Приложение (тип 1), Ссылка (тип 2) и Каталог (тип 3).

*   Ключ `Version` обозначает версию спецификации ярлыка приложения, которая соответствует этому файлу, но не как не версию приложения.

*   `Name`, `GenericName` и `Comment` часто содержат избыточные значения в виде комбинаций из них, например:

```
Name=Pidgin Internet Messenger
GenericName=Internet Messenger

```

или

```
Name=NoteCase notes manager
Comment=Notes Manager

```

Этого следует избегать, поскольку это только будет запутывать пользователей. Ключ `Name` должен содержать только имя или хотя бы аббревиатуру/акроним, если они доступны.

*   `GenericName` должен указывать на категорию приложения, которая обозначает особый признак этого конкретного приложения (например Firefox является "веб-браузером").
*   `Comment` должен содержать любую полезную дополнительную информацию.

#### Осуждение

Существует много ключей, которые стали устаревшими с течением времени по мере созревания стандарта. Лучший/самый простой способ - использовать инструмент `desktop-file-validate`, который является частью пакета [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils). Чтобы проверить, выполните

```
$ desktop-file-validate <твой desktop-файл>

```

Это даст вам очень подробные и полезные предупреждения и сообщения об ошибках.

## Значки

Смотрите также [спецификация тем значков](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html).

### Распространенные форматы изображений

Ниже приведен краткий обзор форматов изображений, обычно используемых для значков.

<caption>Поддержка форматов изображений для значков, указанных в стандарте freedesktop.org.</caption>
| Расширение | Полное имя и/или описание | Тип графики | Формат контейнера | Поддерживаемый |
| .[png](https://en.wikipedia.org/wiki/ru:PNG "w:ru:PNG") | Portable Network Graphics | [Raster](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B2%D0%B0%D1%8F_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0 "w:ru:Растровая графика") | Нет | Да |
| .[svg(z)](https://en.wikipedia.org/wiki/ru:SVG "w:ru:SVG") | Scalable Vector Graphics | [Vector](https://en.wikipedia.org/wiki/ru:%D0%92%D0%B5%D0%BA%D1%82%D0%BE%D1%80%D0%BD%D0%B0%D1%8F_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0 "w:ru:Векторная графика") | Нет | Да (опционально) |
| .[xpm](https://en.wikipedia.org/wiki/ru:X_Pixmap "w:ru:X Pixmap") | X PixMap | [Raster](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B2%D0%B0%D1%8F_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0 "w:ru:Растровая графика") | Нет | Да (устаревший) |
| .[gif](https://en.wikipedia.org/wiki/ru:GIF "w:ru:GIF") | Graphics Interchange Format | [Raster](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B2%D0%B0%D1%8F_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0 "w:ru:Растровая графика") | Нет | Нет |
| .[ico](https://en.wikipedia.org/wiki/ru:ICO_(%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2) "w:ru:ICO (формат файлов)") | MS Windows Icon Format | [Raster](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B2%D0%B0%D1%8F_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0 "w:ru:Растровая графика") | Да | Нет |
| .[icns](https://en.wikipedia.org/wiki/Apple_Icon_Image "w:Apple Icon Image") | Apple Icon Image | [Raster](https://en.wikipedia.org/wiki/ru:%D0%A0%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B2%D0%B0%D1%8F_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0 "w:ru:Растровая графика") | Да | Нет |

### Преобразование значков

Если вы наткнулись на значок, который находится в формате, который не поддерживается стандартом freedesktop.org (например, `gif` или `ico`), вы можете использовать инструмент *преобразования* (который является частью пакета [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)), чтобы преобразовать его в поддерживаемый/рекомендованный формат, например:

```
$ convert <icon name>.gif <icon name>.png

```

Если вы преобразуете из формата контейнера, такого как `ico`, вы получите все изображения, которые были инкапсулированы в файл `ico` в форме `<icon name>-<number>.png`. Если вы хотите узнать размер изображения или количество изображений в файле контейнера, например `ico`, вы можете использовать инструмент *идентификации* (также часть пакета [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)):

 `$ identify /usr/share/vlc/vlc48x48.ico` 
```
/usr/share/vlc/vlc48x48.ico[0] ICO 32x32 32x32+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[1] ICO 16x16 16x16+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[2] ICO 128x128 128x128+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[3] ICO 48x48 48x48+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[4] ICO 32x32 32x32+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[5] ICO 16x16 16x16+0+0 8-bit DirectClass 84.3kb

```

Как вы можете видеть, на примере файла *ico*, что по названию можно предположить одно изображение размером 48x48, но на самом деле оно содержит не менее 6 разных размеров, из которых один больше 48x48, а именно 128x128.

Кроме того, вы можете использовать *icotool* (из [icoutils](https://www.archlinux.org/packages/?name=icoutils)) для извлечения png-изображений из контейнера ico:

```
$ icotool -x <icon name>.ico

```

Для извлечения изображений из контейнера .icns вы можете использовать *icns2png* (предоставленный [libicns](https://aur.archlinux.org/packages/libicns/)):

```
$ icns2png -x <icon name>.icns

```

### Получение значков

Хотя пакеты, которые уже поставляются с файлом .desktop, наверняка содержат значок или набор значков, иногда бывает, что разработчик не создал файл .desktop, но тем не менее может отправить значки. Поэтому неплохо начать поиск значков в исходном пакете. Вы можете, например, сначала фильтровать расширение с помощью **find**, а затем использовать **grep** для дальнейшей фильтрации по определенным ключевым словам, таких как имя пакета, "значок", "логотип" и т.д., если изображений достаточно много в исходном пакете.

```
$ find /path/to/source/package -regex ".*\.\(svg\|png\|xpm\|gif\|ico\)$"

```

Если разработчики приложения не включают значки в свои исходные пакеты, тогда следующим шагом будет поиск значков на их сайте. В некоторых проектах, например, *tvbrowser*, есть [страница с изображением/логотипом](http://enwiki.tvbrowser.org/index.php/Banners,_Logos_and_other_Promotion_Material), где могут быть найдены дополнительные значки. Если проект мультиплатформенный, может случиться так, что в пакете linux/unix отсутствует значок, тогда пакет Windows может предоставить его. Если в проекте используется [система управления версиями](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F_%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D1%8F%D0%BC%D0%B8 "w:ru:Система управления версиями"), например CVS/SVN и т.д., и у вас есть некоторый опыт работы с ней, вы также можете рассмотреть возможность просмотра ее для значков. Если все не удастся, проект может просто не иметь значка/логотипа еще.

## Инструменты

### gendesk

[gendesk](https://www.archlinux.org/packages/?name=gendesk) стартовал как инструмент, специально предназначенный для Arch Linux для генерации файлов .desktop, путем сбора необходимой информации непосредственно из файлов PKGBUILD. Теперь это общий инструмент, который принимает аргументы командной строки.

Значки могут быть автоматически загружены из [openiconlibrary](http://openiconlibrary.sourceforge.net/), если они доступны. (Источник значков можно легко изменить в будущем).

#### Как использовать

*   Добавьте `gendesk` в makedepends

*   Запустите функцию `prepare()` с:

 `gendesk --pkgname "$pkgname" --pkgdesc "$pkgdesc"` 

*   Альтернативно, если значок уже предоставлен (например, $pkgname.png). Флаг `-n` предназначен для не загрузки значка или использования значка по умолчанию. Пример:

 `gendesk -n --pkgname "$pkgname" --pkgdesc "$pkgdesc"` 

*   `$srcdir/$pkgname.desktop` будет создан и может быть установлен в функции `package()` с:

 `install -Dm644 "$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"` 

*   Значок можно установить с помощью:

 `install -Dm644 "$pkgname.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"` 

*   Используйте `--name='Program Name'` для выбора имени для входа в меню..

*   Для установки поля exec используйте `--exec='/opt/some_app/elf --with-ponies'`.

*   Смотрите [проект gendesk](https://github.com/xyproto/gendesk) для получения дополнительной информации.

### Список или поиск в файлах .desktop

[lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/) может отображать доступные файлы *.desktop* или искать их содержимое.

```
$ lsdesktopf
$ lsdesktopf --list
$ lsdesktopf --list gtk zh_TW,zh_CN,en_GB

```

Он также может выполнять поиск по типу MIME. Смотрите [приложения по умолчанию#lsdesktopf](/index.php/Default_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#lsdesktopf "Default applications (Русский)").

### fbrokendesktop

Скрипт [fbrokendesktop](https://aur.archlinux.org/packages/fbrokendesktop/) с использованием команды *which* для обнаружения сломанного `Exec`, который указывает на не существующий путь. Без каких-либо параметров он использует предварительно установленные каталоги в массиве `DskPath`. Он показывает только сломанный *.desktop* с полным отсутствием пути и имени файла.

Примеры

```
$ fbrokendesktop
$ fbrokendesktop /usr
$ fbrokendesktop /usr/share/apps/kdm/sessions/icewm.desktop

```

## Советы и хитрости

### Скрытие ярлыков приложений

Во-первых, скопируйте ярлык приложения в `~/.local/share/applications`, чтобы ваши изменения не были перезаписаны.

Затем, чтобы скрыть ярлык приложения во всех средах, откройте его в текстовом редакторе и добавьте следующую строку: `NoDisplay=true`.

Чтобы скрыть ярлык приложения на конкретной среде рабочего стола добавьте следующую строку в него: `NotShowIn=*desktop-name*`

где *desktop-name* может быть таким, как *GNOME*, *Xfce*, *KDE* и т.д. Ярлык приложения может быть скрытым более, чем в одной среде рабочего стола сразу - просто разделяйте имена сред рабочего стола точкой с запятой.

### Автозапуск

Если вы используете среду рабочего стола, совместимую с XDG, например GNOME или KDE, то она автоматически запускает файлы [*.desktop](/index.php/Desktop_entries "Desktop entries"), найденные в следующих каталогах:

*   Общесистемный: `$XDG_CONFIG_DIRS/autostart/` (`/etc/xdg/autostart/` по умолчанию)

*   GNOME также запускает файлы, найденные в `/usr/share/gnome/autostart/`

*   Пользовательский: `$XDG_CONFIG_HOME/autostart/` (`~/.config/autostart/` по умолчанию)

Пользователи могут переопределять общесистемные файлы `*.desktop` скопировав их в пользовательский каталог `~/.config/autostart/`.

Для более конкретного описания используемых каталогов смотрите [спецификацию автозапуска ярлыков приложений](http://standards.freedesktop.org/autostart-spec/autostart-spec-latest.html).

**Примечание:** Этот способ поддерживается только средами рабочего стола, совместимыми с XDG. Такие инструменты, как [dapper](https://aur.archlinux.org/packages/dapper/), [dex](https://www.archlinux.org/packages/?name=dex) или [fbautostart](https://aur.archlinux.org/packages/fbautostart/), могут использоваться для предоставления автозапуска XDG в неподдерживаемых средах рабочего стола, если существует какой-либо другой механизм автозапуска. Используйте существующий механизм, чтобы запустить инструмент автозапуска, совместимый с xdg.

### Изменение переменных среды

Отредактируйте команду `Exec`, добавив `env`, например:

 `~/.local/share/applications/abiword.desktop`  `Exec=env LANG=he_IL.UTF-8 abiword %U` 

## Смотрите также

*   [DeveloperWiki:Удаление файлов desktop](/index.php/DeveloperWiki:Removal_of_desktop_files "DeveloperWiki:Removal of desktop files")
*   [Ярлык (компьютер)](https://en.wikipedia.org/wiki/.desktop "wikipedia:.desktop")
*   [Информация для разработчиков](http://freedesktop.org/wiki/Howto_desktop_files)