**Состояние перевода:** На этой странице представлен перевод статьи [Cursor themes](/index.php/Cursor_themes "Cursor themes"). Дата последней синхронизации: 9 октября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Cursor_themes&diff=0&oldid=577454).

Дисплейный сервер сопровождается *темой курсора*, которая помогает в различных аспектах навигации и манипуляции GUI. Тема курсора уже включена в сервер, но другие темы также могут быть установлены.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 Пакеты](#Пакеты)
    *   [1.2 Вручную](#Вручную)
*   [2 Настройка](#Настройка)
    *   [2.1 Спецификация XDG](#Спецификация_XDG)
    *   [2.2 LXAppearance](#LXAppearance)
    *   [2.3 Среда рабочего стола](#Среда_рабочего_стола)
        *   [2.3.1 GNOME](#GNOME)
        *   [2.3.2 Mate](#Mate)
        *   [2.3.3 XFCE](#XFCE)
    *   [2.4 X resources](#X_resources)
    *   [2.5 Переменные окружения](#Переменные_окружения)
    *   [2.6 Менеджеры дисплея](#Менеджеры_дисплея)
        *   [2.6.1 GDM](#GDM)
*   [3 Решение проблем](#Решение_проблем)
    *   [3.1 Создание ссылок на недостающие курсоры](#Создание_ссылок_на_недостающие_курсоры)
    *   [3.2 Замена недостающих курсоров](#Замена_недостающих_курсоров)
        *   [3.2.1 rdesktop](#rdesktop)
    *   [3.3 Изменение стандартного курсора X сервера](#Изменение_стандартного_курсора_X_сервера)
    *   [3.4 .Xdefaults](#.Xdefaults)
    *   [3.5 Размер курсора не изменяется при загрузке](#Размер_курсора_не_изменяется_при_загрузке)
*   [4 Смотрите также](#Смотрите_также)

## Установка

Установка совершается посредством пакета или загрузки и извлечения темы в соответствующий каталог.

### Пакеты

Пакеты доступны в:

*   [Официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") — [поиск "xcursor-"](https://www.archlinux.org/packages/?sort=&q=xcursor-&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") — [поиск "cursor"](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=cursor&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

### Вручную

Тему курсора, не доступную в официальных репозиториях и AUR, можно установить вручную. Скачанные темы нужно будет поместить в каталог *icons* (так как курсоры могут быть вместе с иконками).

Сайты, где можно найти темы:

*   [GNOME Look](https://www.gnome-look.org/browse/cat/107/ord/latest/)
*   [Customize.org](http://www.customize.org/list/xcursors)
*   [Deviant Art](https://www.deviantart.com/browse/all/customization/skins/linuxutil/x11cursors/)
*   [Open Desktop](https://www.opendesktop.org/browse/cat/107/)

Чтобы установить тему для *конкретного пользователя*, распакуйте её в `~/.local/share/icons/` или `~/.icons/`:

```
 $ tar xvf foobar-cursor-theme.tar.gz -C ~/.local/share/icons

```

Структура папки с темой: `имя-темы/cursors`. Например: `~/.local/share/icons/*тема*/cursors/`. Также убедитесь, что извлечённые файлы следуют данной структуре.

**Примечание:** Используйте `/usr/share/icons` для *общесистемной* установки. Не следует напрямую распаковывать туда файлы, так как [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") не сможет их отследить; рекомендуется создать [пакет](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") с темой.

Выполните следующую команду, чтобы посмотреть уже установленные темы:

```
 find /usr/share/icons ~/.local/share/icons ~/.icons -type d -name "cursors"

```

Если пакет включает в себя файл `index.theme`, проверьте, есть ли внутри строка «Inherits». Если есть, то проверьте, существует ли указанная тема в системе (переименуйте, если необходимо).

## Настройка

Существуют различные способы настройки установленных тем.

### Спецификация XDG

Этот метод применим к [X11](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") и [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)").

Настройка для *конкретного пользователя* производится посредством `~/.icons/default/index.theme`; для *общесистемной* конфигурации используйте `/usr/share/icons/default/index.theme`.

Опция `Inherits` в разделе `[icon theme]` должна быть установлена на имя каталога темы `*имя_темы*`, например `xcursor-breeze-snow`:

 `~/.icons/default/index.theme` 
```
[icon theme] 
Inherits=*имя_темы*
```

Затем отредактируйте `~/.config/gtk-3.0/settings.ini`, заменяя `*имя_темы*` на соответствующее название:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-cursor-theme-name=*имя_темы*
```

Перелогиньтесь, чтобы изменения вступили в силу.

### LXAppearance

[LXAppearance](/index.php/LXDE#Cursors "LXDE") устанавливает курсор по умолчанию путём создания файла `~/.icons/default/index.theme`. LXAppearance перезапишет любые изменения, сделанные вручную. Не забудьте отредактировать `~/.config/gtk-3.0/settings.ini`, как это указано в [Спецификации XDG](#Спецификация_XDG), потому что некоторые приложения, например Firefox, используют эти настройки.

### Среда рабочего стола

[Среды рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") используют [протокол XSETTINGS](https://specifications.freedesktop.org/xsettings-spec/xsettings-latest.html), обычно реализуемый через демон настроек. Несмотря на возможность изменения темы на лету, в некоторых приложениях это не работает. Чтобы изменить тему вручную, смотрите [#Спецификацию XDG](#Спецификация_XDG).

#### GNOME

Тема курсора в [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") изменяется посредством [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) или gsettings:

```
gsettings set org.gnome.desktop.interface cursor-theme *имя_темы*

```

Изменение размера курсора (зависит от темы. Размеры могут быть следующими: 24, 32, 48, 64):

```
gsettings set org.gnome.desktop.interface cursor-size *размер*

```

#### Mate

В MATE можно использовать mate-control-center или gsettings:

```
gsettings set org.mate.peripherals-mouse cursor-theme *имя_темы*

```

Для изменения размера:

```
gsettings set org.mate.peripherals-mouse *размер*

```

#### XFCE

Чтобы изменить тему:

```
xfconf-query --channel xsettings --property /Gtk/CursorThemeName --set *имя_темы*

```

Для изменения размера:

```
xfconf-query --channel xsettings --property /Gtk/CursorThemeSize --set *размер*

```

### X resources

Для локального изменения темы, добавьте в `~/.Xresources`:

```
Xcursor.theme: *имя_темы*

```

Тема должна загрузиться оконным менеджером. Если этого не произошло, её можно принудительно загрузить посредством `~/.xinitrc` или [.xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)"):

```
$ xrdb ~/.Xresources

```

Если ваша тема поддерживает несколько размеров, добавьте в `~/.Xresources`:

```
Xcursor.size: 16

```

**Совет:** 32, 48 или 64 также могут быть хорошими размерами.

Если вы сомневаетесь в том, что ваша тема поддерживает несколько размеров, то запустите X без этих настроек и дайте ему выбрать размер автоматически. (Обратитесь к документации своего оконного менеджера для деталей.)

### Переменные окружения

Чтобы установить тему курсора для определённого приложения, используйте [переменные окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)"):

```
$ XCURSOR_THEME=ИмяТемы xclock

```

Если тема поддерживает несколько размеров, XCURSOR_SIZE является необязательным.

### Менеджеры дисплея

Тема курсора обычно устанавливается в пределах менеджера дисплея, но имейте в виду, она не переносится между сеансами.

#### GDM

Смотрите [GDM#Changing the cursor theme](/index.php/GDM#Changing_the_cursor_theme "GDM")

## Решение проблем

### Создание ссылок на недостающие курсоры

Приложения могу продолжать использовать тему по умолчанию, если в текущей теме отсутствуют некоторые курсоры. Это можно исправить, добавив ссылки на недостающие курсоры. Например:

```
$ cd ~/.icons/*тема*/cursors/
$ ln -s right_ptr arrow
$ ln -s cross crosshair
$ ln -s right_ptr draft_large
$ ln -s right_ptr draft_small
$ ln -s cross plus
$ ln -s left_ptr top_left_arrow
$ ln -s cross tcross
$ ln -s hand hand1
$ ln -s hand hand2
$ ln -s left_side left_tee
$ ln -s left_ptr ul_angle
$ ln -s left_ptr ur_angle
$ ln -s left_ptr_watch 08e8e1c95fe2fc01f976f1e063a24ccd

```

Если вышеуказанные действия не помогают, посмотрите в `/usr/share/icons/whiteglass/cursors`, чтобы увидеть, каких курсоров не хватает в теме, и добавить ссылки на них.

**Совет:** Также вы можете удалять ненужные курсоры. Например, удаление курсора "watch":
```
$ cd ~/.icons/*тема*/cursors/
$ rm watch left_ptr_watch
$ ln -s left_ptr watch
$ ln -s left_ptr left_ptr_watch

```

### Замена недостающих курсоров

Некоторые программы устанавливают свои курсоры `~/.Xresources`, которые вы, возможно, захотите переопределить. Типичным примером этого является программа rdesktop, которая подключается к компьютеру с Microsoft Windows и использует курсоры, полученные от удалённой машины, которые часто трудно увидеть из-за ограничений протокола, который обеспечивает плохое качество преобразования.

Проблему можно решить, заменив эти курсоры курсорами из этой же темы (или другой). Чтобы сделать это, необходимо получить **хеш** изображения. Это делается путём установки переменной окружения `XCURSOR_DISCOVER` и запуском требуемого приложения:

```
$ XCURSOR_DISCOVER=1 rdesktop ...

```

В первый раз (и только в первый раз) курсор установится, некоторые детали будут отображаться вот так:

```
Cursor image name: 24020000002800000528000084810000
...
Cursor image name: 7bf1cc07d310bf080118007e08fc30ff
...
Cursor hash 24020000002800000528000084810000 returns 0x0

```

Для поиска Xcursor использует директорию `~/.icons/default/cursors`, туда следует поместить недостающие курсоры. Создайте директорию, если она не существует:

```
$ mkdir -p ~/.icons/default/cursors

```

Далее создадим ссылку на хэш изображения. В примере используется курсор `left_ptr` из темы `Vanilla-DMZ`:

```
$ ln -s /usr/share/icons/Vanilla-DMZ/cursors/left_ptr ~/.icons/default/cursors/24020000002800000528000084810000

```

Изменения будут видны после перезапуска приложения. Никаких специальных методов запуска приложений не требуется.

#### rdesktop

Вот некоторые распространённые курсоры Microsoft Windows, которые rdesktop использует при подключении к удалённой машине под управлением Windows 7\. К сожалению, анимированные курсоры трудно переопределить, так как они отправляются по кадру, поэтому изображение нужно будет для каждого кадра!

```
$ ln -s /usr/share/icons/$THEME/cursors/xterm          ~/.icons/default/cursors/00000000017e000002fc000000000000
$ ln -s /usr/share/icons/$THEME/cursors/right_ptr      ~/.icons/default/cursors/00000093000010860000631100006609
$ ln -s /usr/share/icons/$THEME/cursors/plus           ~/.icons/default/cursors/01e00000201c00004038000080300000
$ ln -s /usr/share/icons/$THEME/cursors/left_ptr       ~/.icons/default/cursors/24020000002800000528000084810000
$ ln -s /usr/share/icons/$THEME/cursors/left_ptr_watch ~/.icons/default/cursors/6ce0180090108e0005814700a0021400
$ ln -s /usr/share/icons/$THEME/cursors/hand           ~/.icons/default/cursors/d2201000a2c622004385440041308800
$ ln -s /usr/share/icons/$THEME/cursors/watch          ~/.icons/default/cursors/fc618c00da110f0034fd0e004e082400

```

### Изменение стандартного курсора X сервера

Стандартный курсор X-сервера появляется в форме Xcursor в оконных менеджерах, где не установлен курсор по умолчанию в left_ptr или в оконных менеджерах, где используется XCB (таких как [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)")) вместо Xlib.

Чтобы исправить это, просто добавьте следующее в `~/.xinitrc`, файлы конфигурации xsession или оконного менеджера, которые выполняются при запуске, если это возможно (например, bspwmrc оконного менеджера bspwm):

```
$ xsetroot -cursor_name left_ptr

```

Список стилей курсора протокола X: [appendix B](https://tronche.com/gui/x/xlib/appendix/b/)

### .Xdefaults

Если у вас есть конфликтующие курсоры, это может быть вызвано тем, что другой курсор был определён в файле `~/.Xdefaults`.

### Размер курсора не изменяется при загрузке

Если вы хотите изменить размер курсора через `~/.Xresources` в `~/.xinitrc`, и он не изменяется, то проверьте, что xrandr запускается перед загрузкой `~/.Xresources`

`~/.xinitrc` должен выглядеть примерно следующим образом:

 `~/.xinitrc` 
```
xrandr &&
...
xrdb -merge ~/.Xresources &&
exec wm
```

## Смотрите также

*   [Xcursor(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xcursor.3) — больше информации о курсорах в X (поддерживаемые директории, форматы, совместимость и т.д.).