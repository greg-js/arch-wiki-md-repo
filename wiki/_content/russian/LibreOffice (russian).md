С домашней страницы [LibreOffice](http://ru.libreoffice.org/):

	*LibreOffice — мощный офисный пакет, полностью совместимый с 32/64-битными системами. Переведён более чем на 30 языков мира. Поддерживает большинство популярных операционных систем, включая GNU/Linux, Microsoft Windows и Mac OS X.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 LibreOffice в Arch Linux](#LibreOffice_в_Arch_Linux)
*   [2 Установка](#Установка)
*   [3 Темы оформления](#Темы_оформления)
    *   [3.1 Темы Firefox](#Темы_Firefox)
    *   [3.2 Отключение логотипа запуска](#Отключение_логотипа_запуска)
*   [4 Управление расширениями](#Управление_расширениями)
*   [5 Дополнительные словари](#Дополнительные_словари)
    *   [5.1 Проверка правописания](#Проверка_правописания)
    *   [5.2 Правила переноса](#Правила_переноса)
    *   [5.3 Тезаурус](#Тезаурус)
*   [6 Установка макросов](#Установка_макросов)
*   [7 Запуск LibreOffice](#Запуск_LibreOffice)
*   [8 Ускоряем LibreOffice](#Ускоряем_LibreOffice)
*   [9 Устранение несправностей](#Устранение_несправностей)
    *   [9.1 Шрифт подстановки](#Шрифт_подстановки)
    *   [9.2 Сглаживание](#Сглаживание)
    *   [9.3 Проблемы с проверкой правописания](#Проблемы_с_проверкой_правописания)
    *   [9.4 Темные темы GTK, иконки и gtk-qt-engine](#Темные_темы_GTK,_иконки_и_gtk-qt-engine)
    *   [9.5 Особенности при использовании сетевых папок](#Особенности_при_использовании_сетевых_папок)
    *   [9.6 Исправляем Java Framework Error](#Исправляем_Java_Framework_Error)
    *   [9.7 LibreOffice не находит мои сертификаты](#LibreOffice_не_находит_мои_сертификаты)
    *   [9.8 LibreOffice не открывает документы расположенные в сети через Dolphin в KDE](#LibreOffice_не_открывает_документы_расположенные_в_сети_через_Dolphin_в_KDE)

## LibreOffice в Arch Linux

LibreOffice - это официально поддерживаемый офисный пакет, который является заменой OpenOffice. ([[arch-general](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html) Dropping Oracle OpenOffice]) and main article LibreOffice доступен в репозитории [[extra](https://www.archlinux.org/packages/?q=libreoffice)].

## Установка

Убедитесь, что у Вас установлены шрифты, в противном случае вы увидите прямоугольники вместо букв:

```
# pacman -S ttf-dejavu artwiz-fonts

```

Установите один из следующих пакетов с [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) - стабильная ветвь обновлений
*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) - новые функции появляются сначала здесь, часто обновляется

Проверьте опциональную зависимость, которую выводит [pacman](https://www.archlinux.org/packages/?name=pacman). Java Runtime Environment не требуется, пока вы не захотите использовать Libreoffice Base: см. [Java (Русский)](/index.php/Java_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Java (Русский)"). Вам может понадобиться [hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/), чтобы использовать [некоторые модули](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) в LibreOffice Base.

## Темы оформления

LibreOffice поддерживает интеграцию тем [GTK+ (Русский)](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") and [Qt (Русский)](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)"). Смотри также [Uniform look for Qt and GTK applications (Русский)](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform look for Qt and GTK applications (Русский)").

Наборы библиотек проверяются в следующем порядке:

```
gtk3 > gtk > kde4 > generic

```

Чтобы принудительно использовать определенный интерфейс VCL UI, используйте одну из `SAL_USE_VCLPLUGIN=gen`, `SAL_USE_VCLPLUGIN=kde4`, `SAL_USE_VCLPLUGIN=gtk` или `SAL_USE_VCLPLUGIN=gtk3` переменных среды ([environment variables (Русский)](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)")). Можно снять комментирование с этих переменных в `/etc/profile.d/libreoffice-fresh.sh` или `/etc/profile.d/libreoffice-still.sh`.

Однако, если в программе всё похоже на использование значков Windows 95/98, перейдите в меню *Tools > Options...*, (в котором представлено диалоговое окно Options), затем выберите *LibreOffice > Accessibility* и снимите флажок *Automatically detect high-contrast mode of operating system*.

Если это не сработает сразу, вам может потребоваться изменить набор значков, который используется; это также находится в диалоговом окне Options в разделе *LibreOffice > View* с двумя всплывающими окнами для *Icon size and style* (последнее всплывающее окно должно быть изменено на нечто иное, чем "High-contrast").

### Темы Firefox

LibreOffice может использовать темы Firefox. Войдите в настройки LibreOffice и выберите *Personalization > Select Theme* (*Персонализация > Выбор Темы*), затем вставьте URL адрес вашей любимой. Удобная кнопка в диалоговом окне позволяет открыть браузер.

Темы можно найти в [репозитории тем Mozilla](https://addons.mozilla.org/en-US/firefox/themes/).

### Отключение логотипа запуска

Если вы предпочитаете отключать логотип запуска, откройте `/etc/libreoffice/sofficerc`, найдите строку содержащую `Logo=` и замените на `Logo=0`.

**Note:** Эта переменная не связана с поддержкой Logo scripting.

## Управление расширениями

Arch предоставляет дополнительные расширения, такие как: pdfimport presentation-minimizer presenter-screen report-builder wiki-publisher ct2n hunart numbertext oooblogger typo watch-window diagram.

Также можете использовать встроенный в LibreOffice менеджер расширений или посмотрите [список расширений на сайте](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List).

## Дополнительные словари

С учётом того, что пакеты для поддержки русского языка присутствуют только в [AUR](/index.php/AUR "AUR"), для установки удобно использовать [AUR helper](/index.php/AUR_helpers_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR helpers (Русский)"). Ниже приведены названия пакетов для поддержки английского и русского языков.

### Проверка правописания

Установите [hunspell](https://www.archlinux.org/packages/?name=hunspell) и словари для него: [hunspell-en_US](https://www.archlinux.org/packages/?name=hunspell-en_US) [hunspell-ru-aot](https://aur.archlinux.org/packages/hunspell-ru-aot/). Также в доступны [hunspell-ru](https://aur.archlinux.org/packages/hunspell-ru/) (старый), [hunspell-ru-aot-ieyo](https://aur.archlinux.org/packages/hunspell-ru-aot-ieyo/) (не различает е/ё).

### Правила переноса

Установите [hyphen](https://www.archlinux.org/packages/?name=hyphen) и набор правил для него: [hyphen-en](https://www.archlinux.org/packages/?name=hyphen-en) [hyphen-ru](https://aur.archlinux.org/packages/hyphen-ru/).

### Тезаурус

Установите [libmythes](https://www.archlinux.org/packages/?name=libmythes) и словари для него: [mythes-en](https://www.archlinux.org/packages/?name=mythes-en) [mythes-ru](https://aur.archlinux.org/packages/mythes-ru/).

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

Некоторые из настроек могут уменьшить время загрузки LibreOffice и скорость ее работы. Однако, потребление оперативной памяти тоже возрастет. Эти настройки можно найти в меню *Сервис > Параметры*.

*   В закладке *Память*:
    *   Снизьте число шагов, на которое можно вернуться при редактировании, например 20 или 30.
    *   Установить *Использовать для LibreOffice* равным 128МБ
    *   Установите *Памяти на объект* равным 20МБ
    *   Если Вы часто применяете LibreOffice, проверьте, что используется Quickstarter (использовать быстрый запуск).
*   В закладке *Расширенные возможности*, снимите галочку с Use a Java runtime environment (использовать виртуальную машину java).

## Устранение несправностей

### Шрифт подстановки

Его можно изменить в опциях LibreOffice. Из выпадающего меню выберите *Tools > Options > LibreOffice > Fonts* (Сервис > Параметры > LibreOffice > Шрифты). Поставьте галочку в поле *Apply Replacement Table* (применить таблицу замен). Выберите шрифт `Andale Sans UI` и выберите желаемый шрифт для опции *Replace with* (заменить на). Когда закончите, нажмите *checkmark* (галочку). Затем выберите опции *Always*(всегда) и *Screen only* (экран). Нажимайте ОК. Затем Вам нужно перейти в меню *Tools > Options > LibreOffice > View* (Сервис > Параметры > LibreOffice > Вид) и снять галочку с опции "Use system font for user interface". Если Вы используете несглаженный шрифт, например, Arial, также придется убрать опцию "Screen font antialiasing" (использовать сглаживание).

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

Распакуйте эти словари и конвертируйте их кодировку в *UTF-8*:

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

Наконец, при помощи встроенного менеджера расширений (*Tools*) установите словари из получившихся в итоге файлов `dict-*xx*.oxt`.

### Темные темы GTK, иконки и gtk-qt-engine

Для исправления посмотрите [openoffice-dark-gtk-fix](https://aur.archlinux.org/packages/openoffice-dark-gtk-fix/), а если у Вас go-openoffice, то см. [go-openoffice-dark-gtk-fix](https://aur.archlinux.org/packages.php?ID=28879) на AUR. Это исправление также устанавливает признак 'OOO_FORCE_DESKTOP=gnome'. Также можно посмотреть [для дополнительной информации](http://user.services.openoffice.org/en/forum/viewtopic.php?f=16&t=27216#p123942).

**В новой версии OOO (3.2.0) и LibreOffice** эти исправления больше не работают. Если у Вас темная тема GTK, Вы не сможете сменить иконки. Цвета, однако, можно настроить вручную через меню *Options -> Appearance*, но программы Impress и Calc (другие может быть тоже) останутся темного цвета пока Вы не выключите автоматическое распознавание высококонтрастных тем. Эта проблема вызвана стандартной настройкой “Automatically detect high contrast mode of operating system”. Чтобы ее изменить, отредактируйте:

```
Tools > Options... > Accesibility|> Снять галочку:   [ ] Automatically detect high contrast mode of operating system

```

Теперь Вы можете задавать цвета в меню *Options -> Appearance*.

### Особенности при использовании сетевых папок

Если программа зависает при попытке открыть/сохранить документ в сетевую папку, попробуйте закомментировать следующие строчки символом "#" в /usr/lib/openoffice/program/soffice (/usr/bin/soffice если используете go-openoffice):

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

Исходное сообщение [здесь](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx).

**Примечание:** Текст выше только для NFSv3\. NFSv4 отлично работает с OpenOffice.

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