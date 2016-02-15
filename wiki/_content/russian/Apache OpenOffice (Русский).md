**Обратите внимание:** Официальная поддержка [OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org") прекращена, настоятельно рекомендуется использовать форк: [LibreOffice](/index.php/LibreOffice_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LibreOffice (Русский)").

## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.1 Управление расширениями и проверка правописания в OpenOffice 3.x](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8_.D0.B8_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BF.D1.80.D0.B0.D0.B2.D0.BE.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B2_OpenOffice_3.x)
        *   [2.1.1 French dictionary](#French_dictionary)
    *   [2.2 Настройка переменных окружения OOo](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_OOo)
        *   [2.2.1 Глобальная конфигурация](#.D0.93.D0.BB.D0.BE.D0.B1.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
        *   [2.2.2 Environment variable scripts](#Environment_variable_scripts)
    *   [2.3 KDE4 look & feel для OpenOffice](#KDE4_look_.26_feel_.D0.B4.D0.BB.D1.8F_OpenOffice)
*   [3 Запуск OpenOffice](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_OpenOffice)
*   [4 Известные проблемы](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)

## Введение

[OpenOffice.org](http://www.openoffice.org/) - лидирующий проект с открытым исходным, предоставляющий комплекс программ, для решения офисных задач, таких как: работа с текстом, таблицами, презентациями, графикой, базами данных и т.д.

Arch, предлагает 4 вида подготовленых пакетов для OpenOffice с разными названиями:

**openoffice-base**

Это всегда последняя стабильная версия OpenOffice.
Текущая версия: 3.2.0
Запустить можно командой "soffice" или с панели запуска Рабочего Стола

**openoffice-base-beta**

Этот пакет позволяет посмотреть новые возможности, которые будут реализованы в будущих релизах. Он проходит несколько стадий: альфа, бета и кандидат в релизы, для последующего перемещения в стабильный релиз. Текущая версия: 3.2.0_ooo320_m12-1 Запустить можно командой "soffice-beta" или с панели запуска Рабочего Стола
Можно установить совместно со стабильной версией. Будьте осторожны при тестировании, пишите об ошибках OpenOffice и пакета сборки в наш багтрекер. С планами можно ознакомится на [http://wiki.services.openoffice.org/wiki/OOoRelease311](http://wiki.services.openoffice.org/wiki/OOoRelease311)

**openoffice-base-devel**

Этот пакет обновляется время от времени и является рабочим полигоном для сборщика пакетов, а также для любителей тестировать новые возможности. О проблемах, найденных в программе сообщайте в основной трекер [http://www.openoffice.org/issues/query.cgi](http://www.openoffice.org/issues/query.cgi) Текущая версия: 3.3_dev300_m70-1 Запустить можно командой "soffice-dev" или с панели запуска Рабочего Стола. Можно установить совместно со стабильной и бета версиями. С планами можно ознакомится на [http://wiki.services.openoffice.org/wiki/OOoRelease32](http://wiki.services.openoffice.org/wiki/OOoRelease32)

**go-openoffice**

В дополнение к этим пакетам есть пакет go-openoffice, также называемый ooo-build - "форк от Novell" находящийся в репозитории extra, с включенымми расширениями и возможностями, доступных в Ubuntu, OpenSuSE и других дистрибутивах. Для тех пользователей Arch, которые перешли на него с других дистрибутивов, go-openoffice может показаться более привычным. It will always be the latest stable release in extra based on the source of openoffice-base pkg. Future beta/devel versions will go to the testing repo.
Right now go-openoffice cannot be installed along any other openoffice branch. It's a replacement.

**Обратите внимание:** Если вы используете более чем одну версию openoffice-base, настоятельно рекомендуется всегда создавать резервную копию папки `~/.openoffice{2,3}` !

## Установка

*   Сначала установите [Java](/index.php/Java "Java") (это опционально, но все же **очень** рекомендуется)
*   Убедитесь, что перечисленные шрифты установлены, иначе увидите вместо букв прямоугольники:

```
# pacman -S ttf-dejavu artwiz-fonts ttf-ms-fonts (и любые другие, которые нжны для поддержки вашего языка)

```

*   Загрузите стабильную версию — base и/или beta и/или devel и/или go-oo:

```
# pacman -S openoffice-base openoffice-base-beta openoffice-base-devel go-openoffice.

```

*   Загрузите языковой пакет, главный пакет содержит только файлы для локали en_US. We offer now all upstream shipped langpacks. На сегодня языковые пакеты для go-openoffice не предоставляются.

```
# pacman -S openoffice-en_GB openoffice-de ....

```

### Управление расширениями и проверка правописания в OpenOffice 3.x

Пакет Arch поставляется с некоторыми словарями. Запустите Управление расширеними (Extension manager), если ваш язык там уже присутствует, просто загрузив какую-нибудь ОО программу (Writer, к примеру) и запустите Extension Manager из меню Tools. Оттуда укажите местоположение для установки словаря проверки орфографии:

```
/usr/lib/openoffice/share/extension/install

```

Alternatively, there are several ways to accomplish this:

*   1) Use the Extension manager from OOo menu for download and installation - installs only for the user into his ~/.openoffice.org/3/user/uno_packages/cache
*   2) Download the extension and install it using "unopkg add extension" for the user or
*   3) Download the extension and install it using "unopkg add --shared extension" for every user on the system (requires root permission)

#### French dictionary

As of openoffice 3.0.0-2 the french dictionary is buggy due to a character encoding problem. To solve this problem, first execute the following commands (you'll need **zip** and **unzip** packages):

```
$ cp /opt/openoffice/share/extension/install/dict-fr.oxt dict-fr.oxt
$ unzip dict-fr.oxt -d dict-fr
$ cd dict-fr
$ iconv -f ISO-8859-15 -t UTF-8 dictionaries.xcu > dictionaries.xcu.utf
$ mv dictionaries.xcu.utf dictionaries.xcu
$ zip ../dict-fr.oxt *
$ cd ../
$ rm -r dict-fr

```

then go in the openoffice extension manager (Tools menu) and install the dictionary from the new dict-fr.oxt file.

### Настройка переменных окружения OOo

OpenOffice supports to use several toolkits for drawing and integrates into different desktop environments in a clean way. To choose by hand, you need to set the OOO_FORCE_DESKTOP environment variable.

Для запуска OpenOffice.org в режиме GTK2 (это режим по умолчанию), вы можете выполнить команду (используя bash, это касается и всех приведенных ниже случаев):

```
 # OOO_FORCE_DESKTOP=gnome soffice

```

Для запуска OpenOffice.org в режиме QT/KDE3, вы можете выполнить команду:

```
 # OOO_FORCE_DESKTOP=kde soffice

```

Для запуска OpenOffice.org в режиме QT4/KDE4, вы можете выполнить команду:

```
 # OOO_FORCE_DESKTOP=kde4 soffice

```

**Обратите внимание:** Поскольку KDE look был удален в Openoffice3, то настоятельно рекомендуется использовать режим GTK для всех пользователей. Интеграция KDE4 находится на экспериментальном уровне в go-openoffice и в openoffice-base-devel (starting from m56)

#### Глобальная конфигурация

Для глобальной настройки OpenOffice, вы можете вписывать переменные в /etc/profile.d/openoffice.sh.

#### Environment variable scripts

If for whatever reason you don't want to configure the look globaly, as a non-gnome/kde user you may run into problems when trying to add the environment variable to the command in a *box menu, as such menus don't seem to like environment variables.

This script will run openoffice using the GTK look while still accepting command line options like -writer.

```
 #!/bin/sh

 #### openoffice-gtk - A script to start openoffice with the GNOME/GTK environment

 OOO_FORCE_DESKTOP=gnome /usr/bin/soffice "$@"

```

Just use this script as a command (e.g, /usr/bin/openoffice-gtk) for your menu or whatever other sort of launcher you use.

**Обратите внимание:** If you open a file in a filemanager, for example Thunar, the default look will be used, as the file association will not use your personal script.

### KDE4 look & feel для OpenOffice

OOO_FORCE_DESKTOP=gnome never did the trick for me. A good workaround is to set (as root):

```
export SAL_GTK_USE_PIXMAPPAINT=1

```

в /etc/profile.d/openoffice.sh. Убедитесь, что в системных настройках KDE4 в Appearance > GTK styles and fonts (сперва необходимо установить gtk-qt-engine) выбрано "use my KDE style in GTK applications".

## Запуск OpenOffice

Если вы хотите запустить спецефический модуль OpenOffice.org (вместо стандартного Startcenter), к примеру, текстовый редактор (Write), таблицу (Calc) или презентационную программу (Impress), используйте следующее:

Writer

```
 /usr/bin/soffice -writer

```

Calc

```
 /usr/bin/soffice -calc

```

Impress

```
 /usr/bin/soffice -impress

```

Draw

```
 /usr/bin/soffice -draw

```

Math (Редактор формул)

```
 /usr/bin/soffice -math

```

Base (Базы данных)

```
 /usr/bin/soffice -base

```

Printer Administration (Рекумендуем запускать с привилегиями root)

```
 /usr/bin/spadmin

```

## Известные проблемы

*   qt look'n feel since kde4 release, go-openoffice and openoffice-base-devel have kde4 integeration
*   Проблема рендеринга в некоторых темных темах [GTK+](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") и gtk-qt-engine. Обратите свой взор на пакет [openoffice-dark-gtk-fix](https://aur.archlinux.org/packages/openoffice-dark-gtk-fix/), а если вы используете go-openoffice - на [go-openoffice-dark-gtk-fix](https://aur.archlinux.org/packages/go-openoffice-dark-gtk-fix/)