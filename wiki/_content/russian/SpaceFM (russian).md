**Состояние перевода:** На этой странице представлен перевод статьи [SpaceFM](/index.php/SpaceFM "SpaceFM"). Дата последней синхронизации: 1 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=SpaceFM&diff=0&oldid=402487).

Related articles

*   [Функциональность файлового менеджера](/index.php/%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0 "Функциональность файлового менеджера")
*   [PCManFM (Русский)](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PCManFM (Русский)")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")

Ответвлённый от [PCManFM](/index.php/PCManFM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PCManFM (Русский)"), SpaceFM - это лёгкий, очень настраиваемый, десктоп-независимый, мультипанельный менеджер файлов c поддержкой вкладок и окружением рабочего стола. Имеет виртуальную файловую систему, диспетчер устройств [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"), настраиваемую систему меню и интеграцию [bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)"). Для получения дополнительной информации смотрите [официальный сайт SpaceFM](http://ignorantguru.github.io/spacefm/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
    *   [2.1 Поиск файлов](#Поиск_файлов)
    *   [2.2 Управление рабочим столом](#Управление_рабочим_столом)
    *   [2.3 Монтирование удалённых хостов](#Монтирование_удалённых_хостов)
*   [3 Советы и рекомендации](#Советы_и_рекомендации)
    *   [3.1 Открыть архив приложением, вместо распаковывания](#Открыть_архив_приложением,_вместо_распаковывания)
    *   [3.2 Показать пользовательскую команду контекстного меню только на определённых файлах / папках](#Показать_пользовательскую_команду_контекстного_меню_только_на_определённых_файлах_/_папках)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 Не меняется размер колонок](#Не_меняется_размер_колонок)
    *   [4.2 Ошибки сегментации](#Ошибки_сегментации)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [spacefm](https://aur.archlinux.org/packages/spacefm/).

Если же вы хотите использовать версию на GTK+ 2, используйте пакет [spacefm-gtk2](https://aur.archlinux.org/packages/spacefm-gtk2/).

## Использование

Смотрите [Пользовательскую документацию (En)](http://ignorantguru.github.io/spacefm/spacefm-manual-en.html).

### Поиск файлов

В SpaceFM есть встроенный поиск файлов похожий на [catfish](https://www.archlinux.org/packages/?name=catfish):

```
$ spacefm -f

```

### Управление рабочим столом

SpaceFM включает в себя легкий менеджер рабочего стола. [[1]](http://ignorantguru.github.io/spacefm/spacefm-manual-en.html#invocation-desktopmanager). Он заменяет меню рабочего стола, добавляет значки на рабочем столе, и устанавливает обои.

Для восстановления своего меню оконного менеджера, откройте `Desktop preferences`

```
$ spacefm --desktop-pref

```

и включите опцию `Right click shows WM menu` во вкладке `Desktop`. Попробуйте добавить эту команду в keybind и / или родное меню рабочего стола для быстрого доступа.

Для запуска SpaceFM в качестве [демона](/index.php/Daemons_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemons (Русский)") без управления рабочим столом [[2]](http://ignorantguru.github.io/spacefm/spacefm-manual-en.html#invocation-daemonmode), воспользуйтесь:

```
$ spacefm -d

```

SpaceFM может быть автоматически запущен как демон или как автономный менеджер рабочего стола [(оконный менеджер)](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") не зависящий от оконного менеджера. Если оконный менеджер не предоставляет автостарт, отредактируйте [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") или [xprofile](/index.php/Xprofile "Xprofile").

### Монтирование удалённых хостов

SpaceFM поддерживает монтирование удалённых хостов [udevil](/index.php/File_manager_functionality#udevil.2Fdevmon "File manager functionality"). Чтобы добавить удаленный хост, добавьте URL доступа в адресной строке. Должно всплыть окно терминала, показывающее процесс монтирования (это полезно для отслеживания ошибок).

Обзор поддерживаемых удаленных хостов доступен в [udevil help](http://ignorantguru.github.io/udevil/udevil--help.html). Например, чтобы монтировать удалённый FTP сервер:

```
ftp://user:pass@sys.domain/share

```

## Советы и рекомендации

### Открыть архив приложением, вместо распаковывания

По умолчанию, SpaceFM настроен на извлечение архива по двойному щелчку по нём. Если вы хотите открывать архив программой по умолчанию, такой как [file-roller](https://www.archlinux.org/packages/?name=file-roller), тогда выберите архив, щелкните правой кнопкой мыши, в контекстном меню выберите: Open / Archive default / Open With App

### Показать пользовательскую команду контекстного меню только на определённых файлах / папках

Если вы хотите использовать команду в пользовательском меню, которое должно быть показано только при выборе файлов или папок, добавьте следующие правила тут `Menu Item Properties -> Context`:

```
MIME Type equals true
File Is Dir equals true
File Is Text equals true

```

## Решение проблем

### Не меняется размер колонок

Это встречалось только в первых версиях SpaceFM (GTK+ 2). [[3]](https://github.com/IgnorantGuru/spacefm/issues/382)

### Ошибки сегментации

Если SpaceFM падает с ошибками, например:

```
localhost kernel: [245086.687050] spacefm[30684]: segfault at 3e8000003e8 ip 00007fc95c586866 sp 00007fffb1dc9cc0 error 4 in libgtk-x11-2.0.so.0.2400.24[7fc95c446000+435000]

```

SpaceFM использует различные элементы интерфейса, и, таким образом, чтобы изменить восприимчивую к неисправности тему (особенно в GTK+ 3). Попробуйте другую тему, напримел Raleigh (тема по умолчанию). Для этого в SpaceFM (только для GTK+ 2):

```
GTK2_RC_FILES=/usr/share/themes/Raleigh/gtk-2.0/gtkrc spacefm

```

Смотрите [[4]](http://ignorantguru.github.io/spacefm/spacefm-manual-en.html#invocation-gtkthemes) для подробностей.