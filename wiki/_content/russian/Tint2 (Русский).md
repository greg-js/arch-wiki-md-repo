[tint2](http://code.google.com/p/tint2/) — легковесная системная панель, прекрасно вписывающаяся в [философию Arch](https://wiki.archlinux.org/index.php/The_Arch_Way_%28%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9%29). Может быть настроена для отображения панели задач, системный лотка, индикатора батареи и часов. С помощью несложных манипуляций можно настроить внешний вид и расширить функционал панели. Не имеет зависимостей. Все это делает её идеальным вариантом для тех, кому необходима системная панель, но оконный менеджер не предоставляет такой возможности по умолчанию (например, пользователям [Openbox](/index.php/Openbox "Openbox").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Ярлыки приложений в tint2-svn](#.D0.AF.D1.80.D0.BB.D1.8B.D0.BA.D0.B8_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B2_tint2-svn)
    *   [2.2 Меню приложений в OpenBox3](#.D0.9C.D0.B5.D0.BD.D1.8E_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B2_OpenBox3)
*   [3 Запуск tint2](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_tint2)
*   [4 Прозрачность](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
*   [5 Полезные ссылки](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

[tint2](https://www.archlinux.org/packages/?name=tint2) доступен из репозитория сообщества:

```
# pacman -S tint2

```

## Настройка

Конфигурационный файл создается при первом запуске панели и находится здесь: `~/.config/tint2/tint2rc`. Изменяя параметры можно настроить шрифты, цвета, порядок расположения элементов и другие свойства панели.

Полное описание параметров tint2 находится [в справочнике проекта](http://code.google.com/p/tint2/wiki/Configure)

Пакет tint2 содержит встроенный графический инструмент для настройки внешнего вида, _tint2conf_. Также существует альтернативный графический инструмент настройки, [tintwizard](https://aur.archlinux.org/packages/tintwizard/).

### Ярлыки приложений в tint2-svn

Используя ответвление [tint2-svn](https://aur.archlinux.org/packages/tint2-svn/), можно расширить возможности панели. Однако, в таком случае настройку панели придется выполнять вручную: _tint2conf_ в пакете отсутствует, а _tintwizard_ не способен работать с ярлыкaми.

**Важно:** Если вы воспользуетесь _tintwizard_ для изменения панели после ручного добавления ярлыков, все изменения, связанные с ярлыками, будут утрачены

Чтобы добавить ярлыки на панель, необходимо внести изменения в файл конфигурации _tint2_:

*   Добавить следующую строку после `# Panel`:

```
panel_items = LTSBC

```

*   В конец файла добавить секцию `Launchers`:

```
# Launchers
launcher_icon_theme = LinuxLex-8
launcher_padding = 5 0 10
launcher_background_id = 9
launcher_icon_size = 85
launcher_item_app = /some/where/application.desktop
launcher_item_app = /some/where/anotherapplication.desktop

```

Параметр `panel_items` определяет порядок отображения следующих элементов:

	L

	Ярлыки приложений

	T

	Панель задач

	S

	Системный лоток

	B

	Индикатор батареи

	C

	Часы

Параметр `launcher_icon_theme` определяет используемый пакет иконок, заранее установленных в системе. Параметры `launcher_item_app` определяют ссылки на файлы _.desktop_, которые будут вызывать запуск программ. Такие файлы можно найти в каталоге `/usr/share/applications`.

### Меню приложений в OpenBox3

Ни _tint2_, ни его ответвление, _tint2-svn_, не поддерживают вложенные меню. Но с помощью небольшой хитрости можно получить нечто похожее на это. Вам понадобятся пакеты [tint2-svn](https://aur.archlinux.org/packages/tint2-svn/), [openbox](https://www.archlinux.org/packages/?name=openbox) и [xdotool](https://www.archlinux.org/packages/?name=xdotool).

Задаем комбинацию клавиш для открытия меню OpenBox, создаем следующую запись между тегами `<keyboard>` и `</keyboard>` в файле `~/.config/openbox/rc.xml`:

```
<keybind key="C-A-space">
  <action name="ShowMenu"><menu>root-menu</menu></action>
</keybind>

```

Вы можете изменить `root-menu` на любое _menu-id_, описанное в файле `~/.config/openbox/menu.xml`.

Теперь при нажатии `Ctrl-Alt-Spacebar` будет открываться _root-menu_ (которое также открывается при правом клике на рабочем столе). С помощью [xdotool](https://www.archlinux.org/packages/?name=xdotool) проверьте меню (`xdotool key ctrl+alt+space`): оно должно появиться под курсором мыши.

В каталоге `/usr/share/applications/` создаем файл `tint2.desktop` со следующим содержимым:

```
[Desktop Entry]
Exec=xdotool key ctrl+alt+space

```

В файлового менеджера откройте файл `tint2.desktop`: снова должно появиться меню под курсором.

Добавьте в файл конфигурации `~/.config/tint2/tint2rc` строку `launcher_item_app &#61 /usr/share/applications/tint2.desktop`. После перезапуска панели меню будет отображаться на ней в виде ярлыка.

Больше информации о настройке меню в OpenBox можно найти в [официальном источнике](http://openbox.org/wiki/Help:Menus). Также вы можете использовать [menumaker](https://www.archlinux.org/packages/?name=menumaker), чтобы создать полноценный `menu.xml`, включающий большинство установленных программ.

## Запуск tint2

Вы можете запустить tint2 командой:

```
$ tint2

```

Чтобы запускать tint2 при старте [X](/index.php/X "X"), отредактируйте `~/.xinitrc`. Например, для запуска вместе с [openbox](/index.php/Openbox "Openbox"):

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
**tint2 &**
exec openbox-session

```

Чтобы запустить tint2 при старте [Openbox](/index.php/Openbox "Openbox"), отредактируйте `~/.config/openbox/autostart`, добавив следующее:

```
tint2 &

```

**Обратите внимание:** Если у вас отсутствует файл `~/.config/openbox/autostart`, используйте следующую команду: `cp /etc/xdg/autostart ~/.config/openbox/autostart`

Более подробно о возможности автозапуска в Openbox читайте в [официальном источнике](http://openbox.org/wiki/Help:Autostart).

## Прозрачность

Чтобы сделать tint2 красивее, потребуются дополнительные инструменты. Если ваш рабочий стол настолько прост, что не содержит обоев, значит ваш оконный менеджер просто их не поддерживает (Openbox), или такая функция отключена в настройках.

Чтобы получить возможность использовать обои в Openbox, установите [Xcompmgr]] или [Cairo Compmgr](/index.php/Cairo_Compmgr "Cairo Compmgr"):

```
# pacman -S xcompmgr

```

или

```
# pacman -S cairo-compmgr

```

Xcompmgr запускается так:

```
$ xcompmgr

```

Вам необходимо будет перезапустить tint2, чтобы получить поддержку прозрачности. Если Xcompmgr используется исключительно для обеспечения поддержки прозрачности в tint2, вы можете запускать его в `~/.config/openbox/autostart`:

```
# запуск Xcomppmgr и tint2 в Openbox
if which tint2 >/dev/null 2>&1; then
  (sleep 2 && xcompmgr) &
  (sleep 2 && tint2) &
fi

```

Другие (более удобные) пути запуска Xcompmgr при запуске обсуждаются в статье [Openbox](/index.php/Openbox "Openbox").

## Полезные ссылки

Руководство по настройке на русском языке [[1]](http://dolganov.wordpress.com/2010/04/04/tint2-%D0%B1%D1%8B%D1%81%D1%82%D1%80%D0%B0%D1%8F-%D0%B8-%D0%BB%D0%B5%D0%B3%D0%BA%D0%B0%D1%8F-%D0%BF%D0%B0%D0%BD%D0%B5%D0%BB%D1%8C-%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D1%82%D1%80%D0%B5%D0%B9)