# LibreOffice (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

С домашней страницы [LibreOffice](http://ru.libreoffice.org/):

_LibreOffice — мощный офисный пакет, полностью совместимый с 32/64-битными системами. Переведён более чем на 30 языков мира. Поддерживает большинство популярных операционных систем, включая GNU/Linux, Microsoft Windows и Mac OS X._

## Contents

*   [1 LibreOffice в Arch Linux](#LibreOffice_.D0.B2_Arch_Linux)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Управление расширениями](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8)
*   [4 Проверка правописания](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BF.D1.80.D0.B0.D0.B2.D0.BE.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F)
*   [5 Правила переноса](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.BD.D0.BE.D1.81.D0.B0)
*   [6 Тезаурус](#.D0.A2.D0.B5.D0.B7.D0.B0.D1.83.D1.80.D1.83.D1.81)
*   [7 Установка макросов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BC.D0.B0.D0.BA.D1.80.D0.BE.D1.81.D0.BE.D0.B2)
*   [8 Запуск LibreOffice](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_LibreOffice)
*   [9 Ускоряем LibreOffice](#.D0.A3.D1.81.D0.BA.D0.BE.D1.80.D1.8F.D0.B5.D0.BC_LibreOffice)
*   [10 Устранение несправностей](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BD.D0.BE.D1.81.D1.82.D0.B5.D0.B9)
    *   [10.1 Шрифт подстановки](#.D0.A8.D1.80.D0.B8.D1.84.D1.82_.D0.BF.D0.BE.D0.B4.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [10.2 Сглаживание](#.D0.A1.D0.B3.D0.BB.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [10.3 Проблемы с проверкой правописания](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.BE.D0.B9_.D0.BF.D1.80.D0.B0.D0.B2.D0.BE.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [10.4 Темные темы GTK, иконки и gtk-qt-engine](#.D0.A2.D0.B5.D0.BC.D0.BD.D1.8B.D0.B5_.D1.82.D0.B5.D0.BC.D1.8B_GTK.2C_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_.D0.B8_gtk-qt-engine)
    *   [10.5 Особенности при использовании сетевых папок](#.D0.9E.D1.81.D0.BE.D0.B1.D0.B5.D0.BD.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.BF.D1.80.D0.B8_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D1.8B.D1.85_.D0.BF.D0.B0.D0.BF.D0.BE.D0.BA)
    *   [10.6 Исправляем Java Framework Error](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D1.8F.D0.B5.D0.BC_Java_Framework_Error)
    *   [10.7 LibreOffice не находит мои сертификаты](#LibreOffice_.D0.BD.D0.B5_.D0.BD.D0.B0.D1.85.D0.BE.D0.B4.D0.B8.D1.82_.D0.BC.D0.BE.D0.B8_.D1.81.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D1.8B)
    *   [10.8 LibreOffice не открывает документы расположенные в сети через Dolphin в KDE](#LibreOffice_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.B4.D0.BE.D0.BA.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B_.D1.80.D0.B0.D1.81.D0.BF.D0.BE.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B2_.D1.81.D0.B5.D1.82.D0.B8_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Dolphin_.D0.B2_KDE)

## LibreOffice в Arch Linux

LibreOffice - это официально поддерживаемый офисный пакет, который является заменой OpenOffice. ([[arch-general](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html) Dropping Oracle OpenOffice])

LibreOffice доступен в репозитории [[extra](https://www.archlinux.org/packages/?q=libreoffice)].

## Установка

Убедитесь, что у Вас установлены шрифты, в противном случае вы увидите прямоугольники вместо букв:

```
# pacman -S ttf-dejavu artwiz-fonts

```

Установите один из следующих пакетов с [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

```
   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) это ответвление с новыми улучшениями программ.
   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) является поддерживаемым ответвлением.

```

Проверьте опциональную зависимость, которую выводит [pacman](https://www.archlinux.org/packages/?name=pacman). Java Runtime Environment не требуется, пока вы не захотите использовать Libreoffice Base: см. [Java (Русский)](/index.php/Java_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Java (Русский)"). Вам может понадобиться [hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/)<sup><small>AUR</small></sup>, чтобы использовать [некоторые модули](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) в LibreOffice Base.

## Управление расширениями

Arch предоставляет дополнительные расширения, такие как: pdfimport presentation-minimizer presenter-screen report-builder wiki-publisher ct2n hunart numbertext oooblogger typo watch-window diagram.

Также можете использовать встроенный в LibreOffice менеджер расширений или посмотрите [список расширений на сайте](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List).

## Проверка правописания

Для проверки правописания необходимо установить пакет hunspell и словарь для него:

```
$ pacman -S hunspell

```

Словарь можно найти на [AUR](https://aur.archlinux.org/packages.php?ID=44349).

## Правила переноса

Для установки правил переноса Вам нужно установить пакет hyphen и набор правил для него.

```
$ pacman -S hyphen

```

Набор правил доступен на [AUR](https://aur.archlinux.org/packages.php?ID=45584).

## Тезаурус

Чтобы использовать Тезаурус, необходимо установить:

```
$ pacman -S mythes

```

И, по аналогии с предыдущими опциями, установить пакет с [AUR](https://aur.archlinux.org/packages.php?ID=45585).

## Установка макросов

В Arch Linux путь к макросам по-умолчанию:

```
~/.config/libreoffice/3/user/Scripts/

```

Также нужно учитывать, что если Вы намерены использовать макросы, Вам нужно установить Java Runtime Environment. Однако ее отключение может положительно сказаться на скорости работы программы.

## Запуск LibreOffice

Если Вы хотите запустить определенный модуль LibreOffice, например, текстовый процессор Writer, редактор таблиц Calc или программу для создания презентаций Impress, посмотрите следующие скрипты:

Writer (текстовый процессор)

```
 /usr/bin/libreoffice -writer or /usr/bin/soffice -writer

```

Calc (редактор таблиц)

```
 /usr/bin/libreoffice -calc

```

Impress (редактор презентаций)

```
 /usr/bin/libreoffice -impress

```

Draw (создание диаграмм и чертежей)

```
 /usr/bin/libreoffice -draw

```

Math (редактор формул)

```
 /usr/bin/libreoffice -math

```

Base (интерфейс СУБД)

```
 /usr/bin/libreoffice -base

```

## Ускоряем LibreOffice

Некоторые из настроек могут уменьшить время загрузки LibreOffice и скорость ее работы. Однако, потребление оперативной памяти тоже возрастет. Эти настройки можно найти в меню _Сервис > Параметры_.

*   В закладке _Память_:
    *   Снизьте число шагов, на которое можно вернуться при редактировании, например 20 или 30.
    *   Установить _Использовать для LibreOffice_ равным 128МБ
    *   Установите _Памяти на объект_ равным 20МБ
    *   Если Вы часто применяете LibreOffice, проверьте, что используется Quickstarter.
*   В закладке _Java_, снимите галочку с Use a Java runtime environment.

## Устранение несправностей

### Шрифт подстановки

Его можно изменить в опциях LibreOffice. Из выпадающего меню выберите _Tools > Options > LibreOffice > Fonts_. Поставьте галочку в поле _Apply Replacement Table_. Выберите шрифт `Andale Sans UI` и выберите желаемый шрифт для опции _Replace with_. Когда закончите, нажмите _checkmark_. Затем выберите опции _Always_ и _Screen only_. Нажимайте ОК. Затем Вам нужно перейти в меню _Tools > Options > LibreOffice > View_ и снять галочку с опции "Use system font for user interface". Если Вы используете несглаженный шрифт, например, Arial, также придется убрать опцию "Screen font antialiasing".

### Сглаживание

Выполните:

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

Чтобы сделать изменение постоянным, добавьте "`Xft.lcdfilter: lcddefault`" в `~/.Xresources` файл. ([[1]](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19))

Если не сработало, можно также добавить "`Xft.lcdfilter: lcddefault`" в `~/.Xdefaults`. Если такого файла нет, создайте его.

### Проблемы с проверкой правописания

Проблемы с проверкой правописания могут быть вызваны неверной кодировкой словарей. Чтобы устранить эту проблему, следуйте инструкциям.

Найдите, где хранятся файлы словарей (к примеру, `pacman -Ql openoffice-base`). Большая часть дистрибутивов устанавливает их в `/usr/lib/openoffice/share/extension/install`. Как только путь найден, присвойте его значение переменной shell:

```
droot="/usr/lib/openoffice/share/extension/install"

```

Установите пакеты [unzip](https://www.archlinux.org/packages/?name=unzip) и [zip](https://www.archlinux.org/packages/?name=zip) для того, чтобы иметь возможность распаковать файлы словарей:

```
pkg=$(pacman -T unzip zip) || pacman -S $pkg

```

Для справки, чтобы получить список словарей, входящих в состав базового пакета:

```
cd "$droot" && ls | sed -rn 's,^dict-(..)\.oxt$,\1,p'

```

Определите, какие языковые словари Вам нужно исправить:

```
lang="en ru"

```

Распакуйте эти словари и конвертируйте их кодировку в _UTF-8_:

```
tmp="/tmp/dictfix-$USER-$$"

mkdir "$tmp"
cd "$tmp"

for i in $lang; do
	i="$droot/dict-$i.oxt"
	unzip "$i" -d oxt.tmp
	iconv -f ISO-8859-15 -t UTF-8 oxt.tmp/dictionaries.xcu > dict.tmp
	mv dict.tmp oxt.tmp/dictionaries.xcu
	(cd oxt.tmp && zip -r "$i" .)
done

rm -rf "$tmp"

```

Наконец, при помощи встроенного менеджера расширений (_Tools_) установите словари из получившихся в итоге файлов `dict-_xx_.oxt`.

### Темные темы GTK, иконки и gtk-qt-engine

Для исправления посмотрите [openoffice-dark-gtk-fix](https://aur.archlinux.org/packages/openoffice-dark-gtk-fix/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/openoffice-dark-gtk-fix)]</sup>, а если у Вас go-openoffice, то см. [go-openoffice-dark-gtk-fix](https://aur.archlinux.org/packages.php?ID=28879) на AUR. Это исправление также устанавливает признак 'OOO_FORCE_DESKTOP=gnome'. Также можно посмотреть [для дополнительной информации](http://user.services.openoffice.org/en/forum/viewtopic.php?f=16&t=27216#p123942).

**В новой версии OOO (3.2.0) и LibreOffice** эти исправления больше не работают. Если у Вас темная тема GTK, Вы не сможете сменить иконки. Цвета, однако, можно настроить вручную через меню _Options -> Appearance_, но программы Impress и Calc (другие может быть тоже) останутся темного цвета пока Вы не выключите автоматическое распознавание высококонтрастных тем. Эта проблема вызвана стандартной настройкой “Automatically detect high contrast mode of operating system”. Чтобы ее изменить, отредактируйте:

**Tools > Options... > Accesibility** > Снять галочку:   [ ] Automatically detect high contrast mode of operating system

Теперь Вы можете задавать цвета в меню _Options -> Appearance_.

### Особенности при использовании сетевых папок

Если программа зависает при попытке открыть/сохранить документ в сетевую папку, попробуйте закомментировать следующие строчки символом "#" в /usr/lib/openoffice/program/soffice (/usr/bin/soffice если используете go-openoffice):

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

Исходное сообщение [здесь](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx).  

**Обратите внимание:** Текст выше только для NFSv3\. NFSv4 отлично работает с OpenOffice.

### Исправляем Java Framework Error

Если у Вас появилось такое сообщение об ошибки во время работы с OpenOffice:

```
[Java framework] Error in function createSettingsDocument (elements.cxx).
javaldx failed!

```

Попробуйте изменить владельца папки `~/.config/`:

```
sudo chown -vR username:users ~/.config

```

[Пост на форуме Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=93168)

### LibreOffice не находит мои сертификаты

Если Вы не видите своих сертификатов при попытке подписать документ, Вам необходимо их сконфигурировать в программах Firefox или Thunderbird. Если же и после этого их не видно, наберите команду:

```
export MOZILLA_CERTIFICATE_FOLDER=$HOME/.mozilla/firefox/XXXXXX.default/

```

[Нахождение сертификатов](http://wiki.services.openoffice.org/wiki/Certificate_Detection)

### LibreOffice не открывает документы расположенные в сети через Dolphin в KDE

Если при открытии документов из сетевых каталогов всплывет сплеш-заставка LibreOffice и затем ничего не происходит, то наберите команды для изменения Desktop-файлов приложения:

```
sudo sed -i 's/X-GIO-NoFuse=true/#X-GIO-NoFuse=true/' /usr/share/applications/libreoffice-*
sudo sed -i 's/X-KDE-Protocols=file,http,smb,ftp,webdav/#X-KDE-Protocols=file,http,smb,ftp,webdav/' /usr/share/applications/libreoffice-*

```

[Источник](http://www.addalab.it/how-open-network-document-using-kde-and-libreoffice)

Retrieved from "[https://wiki.archlinux.org/index.php?title=LibreOffice_(Русский)&oldid=415355](https://wiki.archlinux.org/index.php?title=LibreOffice_(Русский)&oldid=415355)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")