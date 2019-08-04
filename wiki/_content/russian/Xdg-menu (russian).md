**Состояние перевода:** На этой странице представлен перевод статьи [Xdg-menu](/index.php/Xdg-menu "Xdg-menu"). Дата последней синхронизации: 27 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xdg-menu&diff=0&oldid=428040).

**Меню XDG** создаёт меню для оконных менеджеров используя [Стандарт Меню Free Desktop](http://standards.freedesktop.org/menu-spec/menu-spec-latest.html). Вы можете [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu).

Поддерживаются следующие оконные менеджеры:

*   twm
*   ion3
*   WindowMaker
*   fvwm2
*   icewm
*   blackbox
*   fluxbox
*   openbox
*   awesome

Также с XDG совместимы: KDE, Gnome, Xfce, Enlightenment.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Иерархия меню](#Иерархия_меню)
*   [2 Настройка](#Настройка)
    *   [2.1 Добавление записей рабочего стола из других каталогов](#Добавление_записей_рабочего_стола_из_других_каталогов)
*   [3 Использование](#Использование)
    *   [3.1 xdg_menu](#xdg_menu)
    *   [3.2 Обновление меню](#Обновление_меню)
*   [4 Примеры](#Примеры)
    *   [4.1 Awesome](#Awesome)
        *   [4.1.1 С xdg_menu](#С_xdg_menu)
    *   [4.2 IceWM](#IceWM)
        *   [4.2.1 С xdg_menu](#С_xdg_menu_2)
        *   [4.2.2 С update-menus](#С_update-menus)
    *   [4.3 Ion3](#Ion3)
        *   [4.3.1 С xdg_menu](#С_xdg_menu_3)
        *   [4.3.2 С update-menus](#С_update-menus_2)
    *   [4.4 FluxBox](#FluxBox)
        *   [4.4.1 С xdg_menu](#С_xdg_menu_4)
        *   [4.4.2 С update-menus](#С_update-menus_3)
    *   [4.5 OpenBox](#OpenBox)
        *   [4.5.1 С xdg_menu](#С_xdg_menu_5)
        *   [4.5.2 Как pipe menu](#Как_pipe_menu)
        *   [4.5.3 С update-menus](#С_update-menus_4)
    *   [4.6 Twm](#Twm)
        *   [4.6.1 С xdg_menu](#С_xdg_menu_6)
        *   [4.6.2 С update-menus](#С_update-menus_5)
    *   [4.7 WindowMaker](#WindowMaker)
        *   [4.7.1 С xdg_menu](#С_xdg_menu_7)
        *   [4.7.2 С update-menus](#С_update-menus_6)
    *   [4.8 Fvwm2](#Fvwm2)
        *   [4.8.1 С xdg_menu](#С_xdg_menu_8)
        *   [4.8.2 С update-menus](#С_update-menus_7)
    *   [4.9 BlackBox](#BlackBox)
        *   [4.9.1 С xdg_menu](#С_xdg_menu_9)
        *   [4.9.2 С update-menus](#С_update-menus_8)
*   [5 Смотрите также](#Смотрите_также)

### Иерархия меню

*   Applications
    *   Accessibility
    *   Accessories
    *   Development
    *   Education
    *   Games
    *   Graphics
    *   Internet
    *   Multimedia
    *   Office
    *   Other
    *   Science
    *   System

## Настройка

Xdg_menu опирается на сведения для генерации меню из трёх источников: root menu (главное меню) или другими словами, шаблон меню XML, как правило передающихся в командной строке, информация и ряд конфигурационных файлов кэшируются, после последнего запуска.

*   Вы можете найти несколько шаблонов меню в `/etc/xdg/menus`.
*   После изменения кода в xdg_menu, чтобы изменить схему, убедитесь, что вы удалили всё в `~/.xdg_menu_cache`, иначе вы потратите много времени, пытаясь выяснить, почему ваши изменения в скрипатх Perl не принимаются.
*   Вы можете найти индивидуальные конфигурации приложений в `/usr/share/applications`

Другие каталоги файлов конфигурации можно найти в каталоге /usr/share. В большинстве случаев вам не нужно трогать их. Если вы хотите, изменить то, как ваше меню располагается, вы можете изменить шаблон меню. Основные изменения требуют тонкой настройки скрипта perl xdg_menu. Если вы обнаружили, что приложения не отображаются или что они вызывают что-то не то, то вам нужно будет посмотреть в файл .desktop в `/usr/share/applications`. Проверьте этот [файл стандартов](http://standards.freedesktop.org/desktop-entry-spec/desktop-entry-spec-1.0.html).

### Добавление записей рабочего стола из других каталогов

По умолчанию, меню XDG будет заполняться приложениями которые устанавливают свои desktop entries в `/usr/share/applications`. Чтобы добавить в меню приложение, которое устанавливает свои desktop entry в пользовательский каталог, такой как `~/.local/share/applications`, отредактируйте файл `/etc/xdg/menus/arch-applications.menu` и добавьте тэг `<AppDir>` для соответствующего каталога, смотрите ниже:

 `/etc/xdg/menus/arch-applications.menu` 
```
<Menu>

  <Name>Applications</Name>
  <Directory>Arch-Applications.directory</Directory>
  <DefaultAppDirs/>
  **<AppDir>/home/*Ваш логин*/.local/share/applications</AppDir>**
  <DefaultDirectoryDirs/>
  <DefaultMergeDirs/>
  ...

```

## Использование

### xdg_menu

```
xdg_menu [--format <format>] [--desktop <desktop>] 
         [--charset <charset>] [--language <language>]  
	 [--root-menu <root-menu>] [--die-on-error]
	 [--fullmenu] [--help]

	format - output format
	         possible formats: twm, WindowMaker, fvwm2, icewm, ion3
	                           blackbox, fluxbox, openbox, 
				   xfce4, openbox3, openbox3-pipe, awesome
				   readable
		 default: WindowMaker

 	fullmenu  - output a full menu and not only a submenu

	desktop - desktop name for NotShowIn and OnlyShowIn
		 default: the same as format

	charset - output charset
		 default: <locale>

	language - output language
		 default: <locale>

	root-menu - location of root menu file
		 default: /opt/gnome/etc/xdg/menus/applications.menu

	die-on-error - abort execution on any error, 
		 default: try to continue

	verbose - print debugging information

	help - print this text

```

### Обновление меню

Обновление меню XDG в Оконных Менеджерах можно сделать автоматически, при помощи настроек **update-menus**.

Скрипт-оболочка xdg_menu, опирается на `/etc/update-menus.conf`

Вам надо установить [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu) (xdg_menu)

`/etc/update-menus.conf` - выберите из списка Оконные Менеджеры, для которых меню должно быть сгенерировано. Комментарии с # разрешены.

Все сгенерированные меню, находятся в `/var/cache/xdg-menu/`. Для получения дополнительной информации смотрите разделы этой страницы, в которых говорится о специфичных примерах для Оконных Менеджеров.

## Примеры

### Awesome

#### С xdg_menu

```
$ xdg_menu --format awesome --root-menu /etc/xdg/menus/arch-applications.menu >~/.config/awesome/archmenu.lua

```

Затем измените `rc.lua` как показано ниже

*   Добавьте требуемый оператор для вашего нового файла `menu.lua`
*   Добавьте запись в свой объект awful.menu для нового меню, которое вызывает xdgmenu

```
...
xdg_menu = require("archmenu")
...

...
mymainmenu = awful.menu({ items = { { "awesome", myawesomemenu, beautiful.awesome_icon },
                                    { "Applications", xdgmenu },
                                    { "open terminal", terminal }
                                  }
                        })
...

```

### IceWM

#### С xdg_menu

```
$ xdg_menu --format icewm --fullmenu --root-menu /etc/xdg/menus/arch-applications.menu >>~/.icewm/programs

```

#### С update-menus

*   Раскоментируйте icewm в /etc/update-menus.conf
*   Выполните update-menus от суперпользователя (root)
*   Сделайте символьную ссылку в /var/cache/xdg-menu/icewm/programs на ~/.icewm/programs

### Ion3

#### С xdg_menu

```
$ xdg_menu --format ion3  --root-menu /etc/xdg/menus/arch-applications.menu >~/.ion3/default-session--0/_xdg-menu.lua

```

После этого измените cfg_menus.lua включите файл _xdg-menu.lua и добавьте меню в mainmenu. Например:

```
...

dopath("_xdg-menu")

-- Main menu
defmenu("mainmenu", {
    submenu("XDG Menu",         "<NAME-OF-FIRST-MENU-IN-_xdg-menu.lua-FILE>"),
    submenu("Programs",         "appmenu"),
    menuentry("Lock screen",    "ioncore.exec_on(_, 'xlock')"),
    menuentry("Help",           "mod_query.query_man(_)"),
    menuentry("About Ion",      "mod_query.show_about_ion(_)"),
    submenu("Styles",           "stylemenu"),
    submenu("Session",          "sessionmenu"),
})

...

```

#### С update-menus

*   Расскомментируйте ion3 в /etc/update-menus.conf
*   Выполните update-menus от имени суперпользователя (root)
*   Измените ваш cfg_menus.lua включенный файл xdg-menu.lua и добавьте меню в mainmenu.

Например:

```
...

dopath("/var/cache/xdg-menu/ion3/xdg-menu.lua")

-- Main menu
defmenu("mainmenu", {
    submenu("XDG Menu",         "<NAME-OF-FIRST-MENU-IN-xdg-menu.lua-FILE>"),
    submenu("Programs",         "appmenu"),
    menuentry("Lock screen",    "ioncore.exec_on(_, 'xlock')"),
    menuentry("Help",           "mod_query.query_man(_)"),
    menuentry("About Ion",      "mod_query.show_about_ion(_)"),
    submenu("Styles",           "stylemenu"),
    submenu("Session",          "sessionmenu"),
})

...

```

### FluxBox

#### С xdg_menu

```
$ xdg_menu --format fluxbox  --root-menu /etc/xdg/menus/arch-applications.menu >~/.fluxbox/my-menu

```

Измените файл меню, чтобы включить сгенерированное меню.

Например добавьте строку:

```
      [include] (my-menu)

```

#### С update-menus

*   Расскоментируйте fluxbox in /etc/update-menus.conf
*   Выполните update-menus от имени суперпользователя (root)
*   измените файл меню, чтобы включить сгенерированное меню.

Например добавьте строку:

```
      [include] (/var/cache/xdg-menu/fluxbox/boxrc)

```

### OpenBox

#### С xdg_menu

Сгенерируйте меню

```
$ xdg_menu --format openbox3 --root-menu /etc/xdg/menus/arch-applications.menu > xdg-menu.xml

```

и вручную добавьте его в свой menu.xml. Например, положите xdg-menu.xml в menu.xml и добавьте:

```
<menu id="Applications" />

```

в root-menu.

#### Как pipe menu

Использование xdg_open как pipe menu, дает дополнительное преимущество получить меню, которое автоматически обновляется при установке новых приложений.

Добавьте следующее, где-то, внутри вашего menu.xml между вашими тэгами root menu

```
<menu id="applications" label="Applications" execute="xdg_menu --format openbox3-pipe --root-menu /etc/xdg/menus/arch-applications.menu" />

```

Очень простой пример:

```
<?xml version="1.0" encoding="UTF-8"?>

<openbox_menu xmlns="http://openbox.org/3.4/menu">

<menu id="root-menu" label="Openbox 3">
  <menu id="applications" label="Applications" execute="xdg_menu --format openbox3-pipe --root-menu /etc/xdg/menus/arch-applications.menu" />
  <separator />
  <item label="Log Out">
    <action name="Exit">
      <prompt>yes</prompt>
    </action>
  </item>
</menu>

</openbox_menu>

```

#### С update-menus

*   Расcкоментируйте openbox in /etc/update-menus.conf
*   Выполните update-menus от имени суперпользователя (root)
*   измените ваш файл menu.xml чтобы включить сгенерированное меню.

Например, добавить следующее в root-menu:

```
<menu id="xdg-menu" label="XDG Menu" execute="cat /var/cache/xdg-menu/openbox/menu.xml"/>

```

### Twm

#### С xdg_menu

Используйте

```
$ xdg_menu --format twm --root-menu /etc/xdg/menus/arch-applications.menu >my-twm-menu

```

и добавить его в twmrc вручную. В случае с производным twm препроцессингом m4 таким как vtwm или ctwm он может быть включен путем добавления

```
sinclude(`/PATH/TO/my-twm-menu')

```

в *twmrc.

#### С update-menus

*   Расcкоментируйте twm in /etc/update-menus.conf
*   Добавьте в файл меню приложений /etc/X11/twm/system.twmrc (добавьте следующую строку:

```
 "apps"          f.menu "Applications"

```

в defops menu)

*   Выполните update-menus от имени суперпользователя (root)
*   Выполните twm -f /var/cache/xdg-menu/twm/twmrc

(Вы также можете добавить другие настройки в /etc/X11/twm/system.twmrc.)

### WindowMaker

#### С xdg_menu

Используйте

```
$ xdg_menu --format WindowMaker --root-menu /etc/xdg/menus/arch-applications.menu >my-wm-menu

```

и добавьте

```
#include "my-wm-menu"

```

в ваш файл меню WindowMaker.

Вы можете также использовать WPrefs "Application Menu Definitions", и добавить команду XDG в качестве параметра в объект "Generated Submenu".

#### С update-menus

*   Расcкоментируйте WindowMaker in /etc/update-menus.conf
*   Выполните update-menus от имени суперпользователя (root)
*   Добавьте

```
#include "/var/cache/xdg-menu/WindowMaker/wmrc"

```

в ваш файл меню.

### Fvwm2

#### С xdg_menu

Сгенерируйте меню

```
$ xdg_menu --format fvwm2 --root-menu /etc/xdg/menus/arch-applications.menu >fvwm2-menu

```

и добавить меню в главное меню

```
read fvwm2-menu

AddToMenu MenuFvwmRoot  "Root Menu"             Title
+                       "&0\. XDG Menu"          Popup xdg_menu

```

#### С update-menus

*   Расcкоментируйте fvwm2 in /etc/update-menus.conf
*   Выполните update-menus от имени суперпользователя (root)
*   измените ваш файл .fvwm2rc чтобы включить сгенерированное меню. Например:

```
AddToMenu MenuFvwmRoot  "Root Menu"             Title
+                       "&0\. XDG Menu"          Popup xdg_menu

```

```
read /var/cache/xdg-menu/fvwm2/fvwm2rc

```

### BlackBox

#### С xdg_menu

```
$ xdg_menu --format blackbox  --root-menu /etc/xdg/menus/arch-applications.menu >my-menu

```

Измените файл меню, чтобы включить сгенерированное меню.

Например добавьте строку:

```
[include] (my-menu)

```

#### С update-menus

*   Расcкоментируйте blackbox in /etc/update-menus.conf
*   Выполните update-menus от имени суперпользователя (root)
*   Измените файл меню, чтобы включить сгенерированное меню.

Например добавьте строку:

```
[include] (/var/cache/xdg-menu/blackbox/boxrc)

```

## Смотрите также

*   [Sawfish#Menus](/index.php/Sawfish#Menus "Sawfish")
*   [https://github.com/gapan/xdgmenumaker](https://github.com/gapan/xdgmenumaker)