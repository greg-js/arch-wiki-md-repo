Related articles

*   [xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Default applications (Русский)](/index.php/Default_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Default applications (Русский)")
*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")

Из [freedesktop.org](https://www.freedesktop.org/wiki/Software/xdg-user-dirs/):

	xdg-user-dirs - это инструмент, помогающий управлять пользовательскими каталогами, такими как папка рабочего стола и папка с музыкой. Он также обрабатывает локализацию (перевод) имен файлов.

	Это работает благодаря раннему старту [xdg-user-dirs-update(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-user-dirs-update.1). Программа считывает файл конфигурации и набор каталогов по умолчанию. Затем создает их локализованные версии в домашнем каталоге пользователя и настраивает конфигурационный файл в `$XDG_CONFIG_HOME/user-dirs.dirs` (XDG_CONFIG_HOME по умолчанию ~/.config), который приложения могут читать, чтобы найти эти каталоги.

Большинство [файловых менеджеров](/index.php/File_manager "File manager") указывают каталоги пользователей XDG со специальными значками.

## Создание каталогов по умолчанию

Установите [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs), а затем выполните:

```
$ xdg-user-dirs-update

```

При выполнении он автоматически создаст файлы конфигурации: `~/.config/user-dirs.dirs` и `~/.config/user-dirs.locale`.

## Создание пользовательских каталогов

Как локальные `~/.config/user-dirs.dirs`, так и глобальные `/etc/xdg/user-dirs.defaults` файлы конфигурации используют формат переменных окружения, чтобы указать на пользовательские каталоги:`XDG_DIRNAME_DIR="$HOME/directory_name"`. Пример файла конфигурации:

 `~/.config/user-dirs.dirs` 
```
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOCUMENTS_DIR="$HOME/Документы"
XDG_DOWNLOAD_DIR="$HOME/Загрузки"
XDG_MUSIC_DIR="$HOME/Музыка"
XDG_PICTURES_DIR="$HOME/Изображения"
XDG_PUBLICSHARE_DIR="$HOME/Общедоступные"
XDG_TEMPLATES_DIR="$HOME/Шаблоны"
XDG_VIDEOS_DIR="$HOME/Видео"
```

Поскольку [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) загрузит локальный файл конфигурации, чтобы указать на соответствующие пользовательские каталоги, вы можете указать пользовательские папки. Например, если пользовательская папка для переменной `XDG_DOWNLOAD_DIR` была названа `$HOME/Internet` в `~/.config/user-dirs.dirs`, любое приложение, использующее эту переменную, будет использовать этот каталог.

**Примечание:** Как и во многих файлах конфигурации, локальные настройки переопределяют глобальные. Вам нужно будет создать новые пользовательские каталоги.

Кроме того, также можно указать пользовательские папки с помощью командной строки. Например, следующая команда даст те же результаты, что и в приведенном выше файле конфигурации:

```
$ xdg-user-dirs-update --set DOWNLOAD ~/Internet

```

## Запрос настроенных каталогов

После установки любой пользовательский каталог можно посмотреть с помощью [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs). Например, следующая команда покажет местоположение каталога `Templates`, которое, конечно, соответствует переменной `XDG_TEMPLATES_DIR` в локальном файле конфигурации:

```
$ xdg-user-dir TEMPLATES

```