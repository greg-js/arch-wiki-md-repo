**Состояние перевода:** На этой странице представлен перевод статьи [Cursor themes](/index.php/Cursor_themes "Cursor themes"). Дата последней синхронизации: 18 февраля 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Cursor_themes&diff=0&oldid=482682).

Дисплейный сервер сопровождается *темой курсора*, которая помогает в различных аспектах навигации и манипуляции GUI. Тема курсора уже включена в сервер, но другие также могут быть установлены.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Пакеты](#.D0.9F.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
    *   [1.2 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Спецификация XDG](#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_XDG)
    *   [2.2 LXAppearance](#LXAppearance)
    *   [2.3 Среда рабочего стола](#.D0.A1.D1.80.D0.B5.D0.B4.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
        *   [2.3.1 GNOME](#GNOME)
        *   [2.3.2 Mate](#Mate)
    *   [2.4 X resources](#X_resources)
    *   [2.5 Переменные окружения](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.6 Менеджеры дисплея](#.D0.9C.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B_.D0.B4.D0.B8.D1.81.D0.BF.D0.BB.D0.B5.D1.8F)
        *   [2.6.1 GDM](#GDM)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Создание ссылок на недостающие курсоры](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BE.D0.BA_.D0.BD.D0.B0_.D0.BD.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D1.8E.D1.89.D0.B8.D0.B5_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D1.8B)
    *   [3.2 Замена недостающих курсоров](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_.D0.BD.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D1.8E.D1.89.D0.B8.D1.85_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D0.BE.D0.B2)
        *   [3.2.1 rdesktop](#rdesktop)
    *   [3.3 Изменение стандартного курсора X сервера](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D0.B0_X_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [3.4 .Xdefaults](#.Xdefaults)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Установка совершается посредством пакета или загрузки и извлечения темы в соответствующий каталог.

### Пакеты

Пакеты доступны в:

*   [Официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") - [поиск "xcursor-"](https://www.archlinux.org/packages/?sort=&q=xcursor-&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") — [поиск "cursor"](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=cursor&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

### Вручную

Тему курсора, не доступную в официальных репозиториях и AUR, можно установить вручную. Скачанные темы нужно будет поместить в каталог *icons* (так как курсоры могут быть вместе с иконками).

Сайты, где можно найти темы:

*   [GNOME Look](https://www.gnome-look.org/browse/cat/107/ord/latest/)
*   [Customize.org](http://www.customize.org/list/xcursors)
*   [Deviant Art](http://www.deviantart.com/browse/all/customization/skins/linuxutil/x11cursors/)

Чтобы установить тему для *конкретного пользователя*, распакуйте ее в `~/.icons/`:

```
$ bsdtar xvf foobar-cursor-theme.tar.gz --directory ~/.icons

```

Структура папки, где содержаться темы, - `имя-темы/cursors`, например: `~/.icons/*тема*/cursors/`. Убедитесь в том, что извлеченные файлы следуют данной структуре.

**Примечание:** Используйте `/usr/share/icons` для *общесистемной* установки. Не следует напрямую распаковывать туда файлы, так как [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") не сможет их отследить; рекомендуется создать [пакет](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") с темой.

Чтобы посмотреть установленные темы:

```
find /usr/share/icons ~/.icons -type d -name "cursors"

```

Если пакет включает в себя файл `index.theme`, проверьте, есть ли линия «Inherits» внутри. Если есть, то проверьте, существует ли такая же тема в системе (переименуйте, если необходимо).

## Настройка

Существуют различные способы настройки установленных тем.

### Спецификация XDG

Этот метод применим к [X11](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") и [Wayland](/index.php/Wayland_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wayland (Русский)").

Отредактируйте `/usr/share/icons/default/index.theme` с привилегиями суперпользователя.

Укажите имя каталога темы:

 `/usr/share/icons/default/index.theme` 
```
[icon theme] 
Inherits=*имя-темы*
```

Затем отредактируйте `~/.config/gtk-3.0/settings.ini`.

Измените в следующей строчке *имя-темы* на имя директории темы:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-cursor-theme-name=*имя-темы*
```

Перелогинтесь, чтобы изменения вступили в силу.

### LXAppearance

[LXAppearance](/index.php/LXDE#Cursors "LXDE") устанавливает курсор по умолчанию путем создания файла `~/.icons/default/index.theme`. LXAppearance перезапишет любые изменения, сделанные вручную. Не забудьте отредактировать `~/.config/gtk-3.0/settings.ini`, как это указано в [Спецификации XDG](#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_XDG), потому что некоторые приложения, например Firefox, используют эти настройки.

### Среда рабочего стола

[Среды рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") используют [протокол XSETTINGS](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html), обычно реализуемый через демон настроек. Это позволяет менять курсор на лету, но он может изменяться между приложениями. Смотрите [#Спецификацию XDG](#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_XDG), чтобы изменить тему вручную.

#### GNOME

Тема курсора в [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") изменяется посредством [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) или gsettings:

```
gsettings set org.gnome.desktop.interface cursor-theme *имя-темы*

```

Также изменение размера курсора (зависит от темы. Размеры: 24, 32, 48, 64):

```
gsettings set org.gnome.desktop.interface cursor-size *размер*

```

#### Mate

В MATE можно использовать mate-control-center или gsettings, чтобы изменить тему:

```
gsettings set org.mate.peripherals-mouse cursor-theme *имя-темы*

```

Для изменения размера:

```
gsettings set org.mate.peripherals-mouse *размер*

```

### X resources

Для локального изменения темы, добавьте в `~/.Xresources`:

```
Xcursor.theme: *имя-темы*

```

Тема курсоров должна загрузиться оконным менеджером; если нет, можно принудительно применить тему посредством `~/.xinitrc` или [.xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)") (в зависимости от личных предпочтений):

```
$ xrdb ~/.Xresources

```

Добавьте данную строку в `~/.Xresources`, если ваша тема поддерживает несколько размеров:

```
Xcursor.size: 16

```

**Совет:** 32, 48 или 64 также могут быть хорошим размером.

Если вы сомневаетесь в том, что ваша тема поддерживает несколько размеров, то запустите X без данных настроек и дайте ему возможность выбрать размер автоматически. (Обратитесь к документации своего оконного менеджера для деталей.)

### Переменные окружения

Используйте [переменные окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)"), чтобы установить временную тему курсора для определенного приложения, например:

```
$ XCURSOR_THEME=НазваниеТемы xclock

```

XCURSOR_SIZE является необязательным, если тема поддерживает несколько размеров.

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

Если вышеуказанные действия не помогают, просмотрите директорию `/usr/share/icons/whiteglass/cursors` для того, чтобы увидеть каких курсоров не хватает в вашей теме и добавьте ссылки на них.

**Совет:** Также вы можете удалить ненужные курсоры. Например, удаление курсора "watch":
```
$ cd ~/.icons/*тема*/cursors/
$ rm watch left_ptr_watch
$ ln -s left_ptr watch
$ ln -s left_ptr left_ptr_watch

```

### Замена недостающих курсоров

Некоторые программы устанавливают свои курсоры, которые вы, возможно, захотите переопределить. Типичным примером этого является программа rdesktop, которая подключается к компьютеру с ОС Microsoft Windows и использует курсоры, полученные от удаленной машины, которые может часто быть трудно увидеть из-за ограничения протокола, который обеспечивает плохое качество преобразования.

Проблему можно решить заменив эти курсоры, курсорами из этой же темы (или другой). Чтобы сделать это необходимо получить **хэш-код** изображения. Это делается путем установки переменной окружения `XCURSOR_DISCOVER` и запуском требуемого приложения:

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

Для поиска xcursor использует директорию `~/.icons/default/cursors`, туда следует поместить недостающие курсоры. Создайте директорию, если она не существует:

```
$ mkdir -p ~/.icons/default/cursors

```

Далее, создадим ссылку на хэш-код изображения. В примере используется курсор `left_ptr` из темы `Vanilla-DMZ`:

```
$ ln -s /usr/share/icons/Vanilla-DMZ/cursors/left_ptr ~/.icons/default/cursors/24020000002800000528000084810000

```

Изменения будут видны после перезапуска приложения. Никаких специальных методов запуска приложений не требуется.

#### rdesktop

Вот некоторые распространенные курсоры Microsoft Windows, rdesktop использует их при подключении к удаленной машине под управлением Windows 7\. К сожалению анимированные курсоры трудно переопределить, так как они отправляются по-кадру, поэтому изображение нужно будет для каждого кадра!

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

Стандартный курсор X-сервера появляется в форме Xcursor в оконных менеджерах, где не установлен курсор по умолчанию в left_ptr или в оконных менеджерах, где используется XCB (таких как [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)"))) вместо Xlib.

Чтобы исправить это, просто добавьте следующее в `~/.xinitrc`, файлы конфигурации xsession или оконного менеджера, которые выполняются при запуске, если это возможно (например, bspwmrc оконного менеджера bspwm):

```
$ xsetroot -cursor_name left_ptr

```

Для получения дополнительной информации смотрите [Awesome wiki](http://awesome.naquadah.org/wiki/FAQ/ru#.D0.9A.D0.B0.D0.BA_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B8.D1.82.D1.8C_.D1.82.D0.B5.D0.BC.D1.83_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D0.B0_.D0.B2_Awesome.3F).

### .Xdefaults

Если у вас есть конфликтующие курсоры, это может быть вызвано тем, что другой курсор определен в файле `~/.Xdefaults`.

## Смотрите также

*   [man Xcursor](http://www.x.org/releases/current/doc/man/man3/Xcursor.3.xhtml) - больше информации о курсорах в X (поддерживаемые директории, форматы, совместимость и т.д.).