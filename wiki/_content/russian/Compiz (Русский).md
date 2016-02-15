Compiz это [композитный оконный менеджер](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager"). Он представляет собой самостоятельный оконный менеджер и не может использоваться совместно с другими оконными менеджерами, такими как [Openbox](/index.php/Openbox "Openbox"), [Fluxbox](/index.php/Fluxbox "Fluxbox"), [Enlightenment](/index.php/Enlightenment "Enlightenment"). Пользователи, которые не хотят расставаться со своим оконным менеджером, но желающие добавить к нему пару эффектов, могут использовать в этих целях [Xcompmgr](/index.php/Xcompmgr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xcompmgr (Русский)").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Установка из [community]](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.B7_.5Bcommunity.5D)
    *   [1.2 Перечень пакетов по группам](#.D0.9F.D0.B5.D1.80.D0.B5.D1.87.D0.B5.D0.BD.D1.8C_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2_.D0.BF.D0.BE_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B0.D0.BC)
    *   [1.3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [2 Запуск Compiz Fusion](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Compiz_Fusion)
    *   [2.1 Вручную (с "fusion-icon")](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E_.28.D1.81_.22fusion-icon.22.29)
    *   [2.2 Вручную (без "fusion-icon")](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E_.28.D0.B1.D0.B5.D0.B7_.22fusion-icon.22.29)
    *   [2.3 KDE](#KDE)
        *   [2.3.1 Автостарт (с "fusion-icon")](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.28.D1.81_.22fusion-icon.22.29)
        *   [2.3.2 Автостарт (без "fusion-icon")](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.28.D0.B1.D0.B5.D0.B7_.22fusion-icon.22.29)
            *   [2.3.2.1 Метод 1 - Автозапуск с помощью ссылки](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_1_-_.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)
            *   [2.3.2.2 Метод 2 - Экспорт KDEWM (Предпочтительный Метод)](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_2_-_.D0.AD.D0.BA.D1.81.D0.BF.D0.BE.D1.80.D1.82_KDEWM_.28.D0.9F.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.9C.D0.B5.D1.82.D0.BE.D0.B4.29)
            *   [2.3.2.3 Метод 3 - Использование KDE 4 System Settings](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_3_-_.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_KDE_4_System_Settings)
    *   [2.4 GNOME](#GNOME)
        *   [2.4.1 Альтернативная сессия для GNOME (предпочтительный метод для опытных пользователей Compiz/Dock)](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D1.8F_.D0.B4.D0.BB.D1.8F_GNOME_.28.D0.BF.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4_.D0.B4.D0.BB.D1.8F_.D0.BE.D0.BF.D1.8B.D1.82.D0.BD.D1.8B.D1.85_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_Compiz.2FDock.29)
        *   [2.4.2 Автостарт (без "fusion-icon") (Предпочтительный метод)](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.28.D0.B1.D0.B5.D0.B7_.22fusion-icon.22.29_.28.D0.9F.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4.29)
        *   [2.4.3 Автостарт (без "fusion-icon") (в сессии gnome3 fallback mode)](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.28.D0.B1.D0.B5.D0.B7_.22fusion-icon.22.29_.28.D0.B2_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8_gnome3_fallback_mode.29)
        *   [2.4.4 Автостарт (без "fusion-icon", Gnome до 2.24)](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.28.D0.B1.D0.B5.D0.B7_.22fusion-icon.22.2C_Gnome_.D0.B4.D0.BE_2.24.29)
        *   [2.4.5 Автостарт (с "fusion-icon")](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.28.D1.81_.22fusion-icon.22.29_2)
    *   [2.5 XFCE](#XFCE)
        *   [2.5.1 Автостарт в Xfce (без "fusion-icon")](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.D0.B2_Xfce_.28.D0.B1.D0.B5.D0.B7_.22fusion-icon.22.29)
        *   [2.5.2 Автостарт в Xfce (с "fusion-icon")](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.D0.B2_Xfce_.28.D1.81_.22fusion-icon.22.29)
            *   [2.5.2.1 Метод 1:](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_1:)
            *   [2.5.2.2 Метод 2:](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_2:)
            *   [2.5.2.3 Метод 3:](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4_3:)
    *   [2.6 Как Самостоятельный (Standalone) Менеджер Окон](#.D0.9A.D0.B0.D0.BA_.D0.A1.D0.B0.D0.BC.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.28Standalone.29_.D0.9C.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D0.9E.D0.BA.D0.BE.D0.BD)
        *   [2.6.1 Добавление root menu](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_root_menu)
        *   [2.6.2 Разрешить пользователям выключение/перезагрузку](#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B8.D1.82.D1.8C_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F.D0.BC_.D0.B2.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5.2F.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D1.83)
*   [3 Разное](#.D0.A0.D0.B0.D0.B7.D0.BD.D0.BE.D0.B5)
    *   [3.1 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_2)
    *   [3.2 Использование compiz-manager](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_compiz-manager)
    *   [3.3 Использование gtk-window-decorator](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_gtk-window-decorator)
    *   [3.4 gconf: Дополнительные Настройки Compiz](#gconf:_.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_Compiz)
    *   [3.5 Keyboard Shortcuts](#Keyboard_Shortcuts)
    *   [3.6 ATI R600/R700 Notes](#ATI_R600.2FR700_Notes)
*   [4 Additional Resources](#Additional_Resources)

## Установка

Базовая установка может быть осуществлена из репозитория [community].

### Установка из [community]

Убедитесь, что репозиторий [community] доступен в `/etc/pacman.conf`.

Вы можете установить полный набор compiz-fusion, используя следующую команду:

```
# pacman -S compiz-fusion

```

Эта команда установит ВСЁ, но, возможно, вы захотите установить compiz отдельно для gnome или отдельно для KDE...

Для установки compiz на базе gtk (для gnome) воспользуйтесь следующей командой:

```
# pacman -S compiz-fusion-gtk

```

Если же вы желаете установить compiz на базе kde (для K Desktop Environment), Вам нужна следующая команда:

```
# pacman -S compiz-fusion-kde 

```

Для самостоятельного выбора устанавливаемых пакетов вам может пригодиться перечень пакетов из каждой группы:

**Обратите внимание:** Для установки в других окружениях рабочего стола вы можете воспользоваться разделом по настройке Compiz в качестве автономного оконного менеджера [below](/index.php/Compiz#As_a_Standalone_Window_Manager "Compiz").

### Перечень пакетов по группам

	Полный набор compiz-fusion (compiz-fusion)

	ccsm, compiz-core, compiz-fusion-plugins-extra, compiz-fusion-plugins-main, compizconfig-backend-gconf, compizconfig-backend-kconfig, emerald, emerald-themes, fusion-icon

	KDE compiz-fusion (compiz-fusion-kde)

	ccsm, compiz-fusion-plugins-extra, compiz-fusion-plugins-main, compizconfig-backend-kconfig, emerald, emerald-themes, fusion-icon

	GTK (Gnome) compiz-fusion (compiz-fusion-gtk)

	ccsm, compiz-fusion-plugins-extra, compiz-fusion-plugins-main, compizconfig-backend-gconf, emerald, emerald-themes, fusion-icon

	Маленькие группы

	compiz-decorator-gtk, compiz-decorator-kde, compiz-manager

*   ccsm или "CompizConfig settings manager" - это GUI-приложение для настройки всех плагинов Compiz.
*   [Emerald](/index.php/Emerald "Emerald") - это имеющий несколько зависимостей декоратор окон для compiz-а.
*   fusion-icon располагается в трее в виде иконки и позволяет запустить compiz, ccsm или сменить WM / Window Decorator (декоратор окон).
*   compiz-manager предназначен для удобной настройки сессии.
*   compiz-decorator-gtk и compiz-decorator-kde являются альтернативами для emerald и используются для оформления окон, настраиваются с помощью инструментов вашего окружения рабочего стола.

### Настройка

	Активируйте важные плагины!

	Прежде чем вы начнёте что-либо делать, необходимо включить несколько важных плагинов, предоставляющих базовые возможности для работы с окнами. В противном случае, пока будет активен compiz, вы не сможете перемещать окна, изменять размеры и закрывать их. Прежде всего, это "Оформление окна" (Window Decoration) из раздела "Эффекты" (Effects), а также "Переместить окно" (Move Window) и "Изменение размеров окна" (Resize Window) из раздела "Управление Окнами" (Window Management). Для включения этих и других плагинов можно использовать ccsm.

	Запустите CompizConfig Settings Manager (Менеджер настроек CompizConfig):

	`$ ccsm`

	Включение: просто поставьте метки рядом с теми плагинами, которые хотите активировать.

	Note: В то время, как за внешний вид окон и их содержимое отвечают [GTK+](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") и/или [Qt](https://en.wikipedia.org/wiki/Qt_(toolkit) "wikipedia:Qt (toolkit)"), за обрамление окон будет отвечать плагин Window Decoration. Для спользования плагина необходимо убедиться в том, что соответствующие пакеты установлены. В зависимости от установленных пакетов, у вас будет выбор среди нескольких декораторов окон. Наиболее популярные из них - [Emerald](/index.php/Emerald "Emerald"), kde-window-decorator и gtk-window-decorator. Предпочтительнее использовать [Emerald](/index.php/Emerald "Emerald"), поскольку он имеет преимущества при управлениии экраном compiz и широкие возможности в реализации функции прозрачности. Для выбора декоратора, используемого по умолчанию, напишите соответствующую команду в поле "Command" раздела настроек плагина "Window Decoration".

	Для назначения emerald в качестве декоратора

	 `emerald --replace` 

	Для назначения kde-window-decorator в качестве декоратора, используемого вместо Emerald-а

	 `kde4-window-decorator --replace` 

	compiz-decorator-gtk вместо Emerald-а

	 `gtk-window-decorator --replace` 

	Совместимость

	[compiz-check](http://forlong.blogage.de/entries/pages/Compiz-Check) это скрипт, выполняющий несколько тестов compiz, он может помочь в настройке. Доступен в [aur](https://aur.archlinux.org/packages.php?ID=17163).

**Обратите внимание:** compiz-check в настоящее время не развивается, поэтому информация, полученная с его помощью, может быть не достоверной.

## Запуск Compiz Fusion

### Вручную (с "fusion-icon")

Запустите Compiz Fusion. В трее должна появиться иконка:

```
$ fusion-icon

```

Нажмите правой кнопкой мыши на иконке в панели и выберите пункт 'выбор оконного менеджера'('select window manager'). Выберите "Compiz", если он ещё не выбран.

Если и это не помогло, то можно запустить compiz-fusion, используя следующую дополнительную команду для замены Вашего декоратора окон стандартным декоратором Сompiz (Emerald):

```
$ emerald --replace

```

### Вручную (без "fusion-icon")

Запустите Compiz следующей командой (она заменит Ваш используемый оконный менежджер):

```
$ compiz --replace ccp &

```

Краткий обзор параметров командной строки compiz:

*   --indirect-rendering: использовать indirect-rendering (AIGLX)
*   --loose-binding: может помочь при проблемах с производительностью (nVidia?)
*   --replace: заменить используемый оконный менеджер
*   --keep-window-hints: сохранить настройки оконного менеджера gnome для возможности просмотра, ...
*   --sm-disable: отключить session-management
*   ccp: команда "ccp" загрузит последние настройки конфигурации ccsm (CompizConfig Settings Manager), в противном случае Compiz будет загружаться без настроек и у вас не будет возможности перетаскивать, разворачивать/сворачивать, или перемещать окна.

### KDE

#### Автостарт (с "fusion-icon")

В своей директории автозапуска для KDE (как правило находится в `~/.kde/Autostart`), создайте символическую ссылку, указывающую на исполняемый файл fusion-icon:

```
$ ln -s /usr/bin/fusion-icon ~/.kde/Autostart/fusion-icon

```

При следующем запуске KDE, fusion-icon будет запущен автоматически.

**Обратите внимание:** Этот метод более медленный, так как KDE сначала загрузит свой менеджер окон (KWin), и только потом будет запущен fusion-icon, который запустит оконный менеджер Compiz взамен KWin. Естественно, на это понадобится некоторое время, поскольку для использования Compiz будут загружаться два оконных менеджера. Читайте далее для ознакомления с другими методами.

#### Автостарт (без "fusion-icon")

##### Метод 1 - Автозапуск с помощью ссылки

**Обратите внимание:** Не создавайте compiz.desktop если хотите установить compiz-decorator-gtk; это приведет к конфликту файлов.

*   Вы можете запускать Compiz Fusion из директории автозапуска KDE после логина, для этого необходимо добавить в нее файл compiz.desktop. Если он отсутствует - создайте файл `~/.kde/Autostart/compiz.desktop` следующего содержания:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=Compiz
Exec=/usr/bin/compiz ccp --replace
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=compiz
# autostart phase
X-GNOME-Autostart-Phase=WindowManager
X-GNOME-Provides=windowmanager
# name we put on the WM spec check window
X-GNOME-WMName=Compiz
# back compat only
X-GnomeWMSettingsLibrary=compiz

```

**Обратите внимание:** Если `compiz.desktop` уже существует, то, возможно, вам прийдется добавить "--replace" и/или "ccp" в переменную Exec. Без "--replace", Compiz не загрузится, поскольку при запуске обнаружит запущенным другой оконный менеджер. Без "ccp", Compiz не загрузит настройки плагинов, включенных ранее через CompizConfig Settings Manager (ccsm) и вам не удастся управлять окнами приложений.

*   Этот метод также будет более медленный, поскольку KDE сначала загрузит оконный менеджер используемый по умолчанию (KWin), затем будет запущен fusion-icon, который загрузит менеджер окон Compiz взамен - KWin. Естественно, на загрузку двух оконных менеджеров, будет затрачено время, хотя дальше работать будет один Compiz. Следующий метод лишен этой проблемы.

}}

*   Если вы дополнительно хотите использовать приложение `fusion-icon` - запустите _fusion-icon_. Если при запущеном _fusion-icon_ вы выйдите из системы, KDE при следующем входе в систему восстановит сессию и, при включенном параметре, снова запустит _fusion-icon_. Если _fusion-icon_ не отображается, убедитесь, что в файле`~/.kde/share/config/ksmserverrc` имеется следующая строка:

```
loginMode=restorePreviousLogout

```

**Обратите внимание:** Это специфический параметр KDE, позволяющий при следующем входе в систему восстанавливать любые приложения, которые были открыты во время выхода (а не только fusion-icon).

##### Метод 2 - Экспорт KDEWM (Предпочтительный Метод)

**Обратите внимание:** Использование данного метода позволит загружать Compiz-Fusion в качестве оконного менеджера по умолчанию без предварительной загрузки KWin. Этот метод автоматической загрузки Compiz-Fusion быстрее предыдущих методов, поскольку позволяет избежать предварительной загрузки оконного менеджера KDE по умолчанию (KWin). При этом методе также отсутствуют раздражающие мерцания экрана, возникающие при использовании метода описаного выше (При переключении с kwin на Compiz во время загрузки рабочего стола KDE).

Необходимо в терминале от имени root выполнить небольшой скрипт. Он позволит вам загрузить compiz непосредственно через `export KDEWM="compiz --replace ccp --sm-disable"`.

```
$ echo "compiz --replace ccp --sm-disable &" > /usr/bin/compiz-fusion

```

**Обратите внимание:** Если строка не сработает - убедитесь, что пакет "fusion-icon" установлен и далее, в качестве замены, выполните следующий код:

```
$ echo "fusion-icon &" > /usr/bin/compiz-fusion

```

Прежде чем использовать эту строку - убедитесь в правильности выполнения всех предыдущих действий.

Убедитесь, что файл `/usr/bin/compiz-fusion` является исполняемым (+x).

```
$ chmod a+x /usr/bin/compiz-fusion

```

Выберите один из следующих вариантов:

	1) Compiz только для одного вашего пользователя --> Отредактируйте файл `~/.kde4/env/compiz.sh` и добавьте следующую строку, теперь KDE (с помощью только что созданного скрипта) будет загружать compiz вместо KWin.

	 `KDEWM="compiz-fusion"` 

	2) Compiz общесистемно --> Отредактируйте файл `/usr/env/compiz.sh` и добавьте следующую строку, теперь KDE (с помощью только что созданного скрипта) будет загружать compiz вместо KWin.

	 `KDEWM="compiz-fusion"` 

**Обратите внимание:** Если, по какой-либо причине, указанные способы не будут работать, попробуйте использовать замену предложенную ранее

**Обратите внимание:** Если метод все еще не работает - воспользуйтесь еще одним способом для достижения цели. Добавьте строку `export KDEWM="compiz-fusion"` в файл `~/.bashrc` нужного пользователя.

**Обратите внимание:** При дополнительном использовании дирректории `/usr/local/bin` -способ может не работать. В этом случае в скрипте необходимо указывать полный путь: `export KDEWM="/usr/local/bin/compiz-fusion"` 

##### Метод 3 - Использование KDE 4 System Settings

Зайдите в Параметры Системы (System Settings) --> Приложения По Умолчанию (Default Applications) --> Диспетчер Окон (Window Manager) --> Использовать другой диспетчер окон (Use a different window manager)

Если нужно запустить compiz с возможностью выбора пользователем "Compiz custom" (при запуске из терминала fusion-icon будет виден вывод командной строки с запуком compiz). Создайте файл с именем "compiz-kde-launcher" в дирректории /usr/bin. Сделайте файл исполняемым: "chmod +x /usr/bin/compiz-kde-launcher". Пример compiz-kde-launcher:

```
 #!/bin/bash
 LIBGL_ALWAYS_INDIRECT=1
 compiz --replace ccp &
 wait

```

### GNOME

Если установлен [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"), понадобится либо включить Fallback Mode, либо удалить _gnome-shell_.

**Обратите внимание:** Если выбрать сессию Compiz/Cairo-Dock как описано ниже, режим Fallback Mode, возможно, и не понадобится

#### Альтернативная сессия для GNOME (предпочтительный метод для опытных пользователей Compiz/Dock)

Для добавления дополнительных пунктов в диалоговом меню выбора сессии GNOME можно установить пакет [gnome-session-compiz](https://aur.archlinux.org/packages/gnome-session-compiz/). Данный способ не требует обязательного использования fallback mode и/или изменения важных системных файлов/настроек. Кроме того, будет возможность переключаться между сессиями GNOME Shell и Compiz/Cairo-Dock. Если у вас что-то не заработает, всегда можно будет вернуться к сессии GNOME.

Чтобы метод заработал, возможно понадобится [создать новые профили](#Configuration) для Compiz и Cairo-Dock (Панель задач/Панель) (у некоторых ccsm в GNOME Shell заработал нормально).

При данном методе будут полностью заменены оконный менеджер и панель GNOME (они не будут запускаться вообще, вместо замены или выключения как было ранее). Поэтому, прежде чем переходить к этой сессии, нужно будет настроить соответствующие/альтернативные программы в Cairo-Dock:

*   Добавить иконку Меню Приложений в Cairo-Dock и назначить для него сочетание клавиш.
*   Для удобства присвоить сочетания клавиш ALT+F1 и ALT+F2 для Remap Application Menu.
*   При необходимости добавить в док иконки Clock, WiFi, NetSpeed.
*   Добить кнопку выхода:
    *   Установить команду для выхода "gnome-session-quit --logout"
    *   Установить команду для выключения "gnome-session-quit --power-off"
*   Добавить в Cairo-Dock значек Старая Область Уведомлений (systray).

#### Автостарт (без "fusion-icon") (Предпочтительный метод)

Этот метод использует спецификации [freedesktop.org](http://standards.freedesktop.org/desktop-entry-spec/latest/) для запуска Compiz путем указания его в качестве оконного менеджера по умолчанию с помощью GConf. Благодаря Desktop Entry появилась возможность выбора Compiz в качестве оконного менеджера прямо из GDM.

**1)** При отсутствии (хотя он должен быть), создайте файл `/usr/share/applications/compiz.desktop` со следующим содержимым:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=Compiz
Exec=/usr/bin/compiz ccp  #Make sure ccp is included so that Compiz loads your previous settings.
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=compiz
# autostart phase
##-> the folloing line cause gnome-session warning and slow startup, so try not to enable this
# X-GNOME-Autostart-Phase=WindowManager 
X-GNOME-Provides=windowmanager
# name we put on the WM spec check window
X-GNOME-WMName=Compiz
# back compat only
X-GnomeWMSettingsLibrary=compiz

```

**Обратите внимание:** Если `compiz.desktop` файл существует, убедитесь, что в строку переменной Exec добавлен параметр "ccp". Параметр "ccp" позволит Compiz загрузить предварительно сохраненные настройки, в противном случае будет полностью отсутствовать функциональность.

Если указанный выше способ не работает (хотя и должен), к примеру появились проблемы с производительностью или обновлением окон, попробуйте использовать:

 `Exec=/usr/bin/compiz ccp --indirect-rendering` 

или

 `Exec=/usr/bin/compiz --replace --sm-disable --ignore-desktop-hints ccp --indirect-rendering` 

вместо

 `Exec=/usr/bin/compiz ccp` 

Некоторые пользователи замечают "лаги" в течении 4-10 секунд после логина через менеджер входа. В качестве решения приведите команду запуска к виду:

 `Exec=bash -c 'compiz ccp decoration --sm-client-id $DESKTOP_AUTOSTART_ID'` 

Решение предложено [на форуме](https://bbs.archlinux.org/viewtopic.php?pid=655237#p655237). При необходимости также можно добавить указанные выше параметры.

**2)** Для установки, с помощью GConf, некоторых параметров можно, либо в окне терминала использовать команду gconftool-2, либо все настроить в графическом режиме с помощью Configuration Editor (gconf-editor). Далее все настройки предлагается выполнять с помощью командной строки, но по ним понятно какие именно изменения следует выполнять в случае использования gconf-editor:

**Обратите внимание:** Поскольку все настройки относятся к обычному пользователю, то и последующее конфигурирование следует выполнять из под учетной записи обычного пользователя. GConf не будет работать под учетной записью root.

```
gconftool-2 --set -t string /desktop/gnome/session/required_components/windowmanager compiz

```

Нижеидущие команды не являются обязательными и в большинстве случаев в них нет необходимости (начиная с GNOME 2.12 соответствующие ключи являются устаревшими). Но если вышеприведенной команды оказалось не достаточно, то можно воспользоваться и этим вариантом.

```
gconftool-2 --set -t string /desktop/gnome/applications/window_manager/current /usr/bin/compiz
gconftool-2 --set -t string /desktop/gnome/applications/window_manager/default /usr/bin/compiz

```

#### Автостарт (без "fusion-icon") (в сессии gnome3 fallback mode)

Отредактируйте файл `/usr/share/gnome-session/sessions/gnome-fallback.session`:

В строке **RequiredComponents** замените свой менеджер окон (gnome-shell,metacity...) на _compiz_.

Замените строку _DefaultProvider-windowmanager_ на _DefaultProvider-windowmanager=compiz_

Вот часть моего `gnome-fallback.session`:

```
RequiredComponents=compiz;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=compiz
DefaultProvider-notifications=notification-daemon

```

**Обратите внимание:** Вместо gnome-panel, в качестве панели, используется avant-window-navigator. Я использую gnome3 fallback mode с compiz, в compiz выбран gtk-window-decorator, и автоматически запускается avant-window-navigator

#### Автостарт (без "fusion-icon", Gnome до 2.24)

Это способ, применяющийся при использовании GDM (возможно и KDM).

Создайте файл `/usr/local/bin/compiz-start-boot` со следующим содержимым:

```
#!/bin/bash
export WINDOW_MANAGER="compiz ccp"
exec gnome-session

```

и сделайте его исполняемым: (`chmod +x /usr/local/bin/compiz-start-boot`). Далее создайте файл: `/etc/X11/sessions/Compiz.desktop` содержащий следующие строки:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Name=Compiz on GNOME
Exec=/usr/local/bin/compiz-start-boot
Icon=
Type=Application

```

В качестве сессии для Gnome выберите Compiz, и войдите.

#### Автостарт (с "fusion-icon")

Для автоматического запуска Compiz fusion при запуске сессии, войдите в Система -> Параметры -> Запускаемые приложения (System > Preferences > Startup Applications). Далее нажмите на кнопку "Добавить" ("Add").

Затем, в появившемся окне, заполните следующие поля:

Name (Имя):

```
Compiz Fusion

```

Command (Команда):

```
fusion-icon

```

Comment (Комментарий): (Добавьте любой или оставьте поле пустым)

**Обратите внимание:** Вместо "fusion-icon" можно использовать команду "compiz --replace ccp", в этом случае Сompiz будет запускаться без fusion-icon. Параметр ccp укажет Сompiz на необходимость загрузки с параметрами, предварительно сконфигурированными с помощью CompizConfig Settings Manager (ccsm).

По окончании - нажмите "Добавить" ("Add"). Теперь Compiz будет доступен в списке запускаемых при старте приложений. Он должен быть активирован (рядом с названием должна стоять галочка). Для отключения Compiz и возврата к Metacity (при следующем входе) достаточно будет просто снять эту галочку.

Для того, чтоб fusion-icon смог загрузить декоратор окон, необходимо в терминале, с помощью gconftool-2, выполнить следующие настройки.

```
gconftool-2 --type bool --set /apps/metacity/general/compositing_manager false

```

**Обратите внимание:** Этот метод является более медленным, так как Gnome вначале будет запускать свой оконный менеджер (Metacity), потом будет запущена программа fusion-icon, которая, в качестве оконного менеджера, загрузит Compiz вместо Metacity. В итоге на загрузку Compiz будет затрачено больше времени, так фактически будут загружаться два оконных менеджера. Первый метод является предпочтительным и лишен этого недостатка.

### XFCE

#### Автостарт в Xfce (без "fusion-icon")

Этот метод реализует запуск Compiz напрямую через менеджер сессий XFCE и без запуска Xfwm.

Пожалуйста, обратите внимание на изменения конфигурационных xml-файлов для версий XFCE более поздних чем 4.2

Для установки менеджера сессий выполните от root следующую команду:

```
# pacman -S xfce4-session

```

Теперь необходимо настроить дефолтную/отказоустойчивую сессию XFCE.

Отредактируйте следующий файл:

```
# nano ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Или, для того, чтоб применить изменения ко всем пользователям XFCE (необходимы права root):

```
# nano /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Замените команду запуска xfwm,

```
 <property name="Client0_Command" type="array">
   <value type="string" value="xfwm4"/>
 </property>

```

на такую:

```
 <property name="Client0_Command" type="array">
   <value type="string" value="compiz"/>
   <value type="string" value="ccp"/>
 </property>

```

**Обратите внимание:** Параметр ccp укажет Сompiz на необходимость загрузки с параметрами, предварительно сконфигурированными с помощью CompizConfig Settings Manager (ccsm).

Во избежание изменения параметров сессии по умолчанию, добавьте следующий код:

```
 <property name="general" type="empty">
   ...
   ...
   <property name="SaveOnExit" type="bool" value="false"/>
 </property>

```

Для удаления сохраненных сессий, выполните:

```
rm -r ~/.cache/sessions

```

#### Автостарт в Xfce (с "fusion-icon")

##### Метод 1:

Сначала будет загружен Xfwm, а затем его заменит Compiz.

Откройте Настройки (XFCE Settings Manager) & Сеансы и Запуск (Sessions & Startup). Кликните по вкладке Автозапуск Приложений (Application Autostart).

Добавьте:

```
  Имя (Name:) Compiz Fusion

```

```
  Команда (Command:) fusion-icon

```

**Обратите внимание:** Вместо "fusion-icon" можно использовать "compiz --replace ccp", в этом случае compiz будет загружен без запуска fusion-icon. Параметр ccp укажет Сompiz на необходимость загрузки с параметрами, предварительно сконфигурированными с помощью CompizConfig Settings Manager (ccsm).

**Обратите внимание:** Поскольку при данном подходе будут грузиться несколько оконных менеджеров, использовать этот метод не желательно. В остальных методах автостарта XFCE будут рассмотрены варианты загрузки только Compiz-а без запуска Xfwm.

##### Метод 2:

Отредактируйте файл (для изменения настроек одного конкретного пользователя):

```
nano ~/.config/xfce4-session/xfce4-session.rc

```

Или для применения изменений ко всем пользователям XFCE (требуются права root):

```
# nano /etc/xdg/xfce4-session/xfce4-session.rc

```

Добавьте следующее:

```
[Failsafe Session]
Client0_Command=fusion-icon

```

Если имеется, то закоментируйте: Client0_Command=xfwm4.

Теперь, при отсутствии сохраненных сессий, xfce вместо Xfwm будет загружать Compiz.

Для предотвращения изменения сессии по умолчанию, можно добавить следующее:

```
[General]
AutoSave=false
SaveOnExit=false

```

Для удаления сохраненных сеансов:

```
rm -r ~/.cache/sessions

```

##### Метод 3:

Убедитесь в существовании файла:

```
~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

При его отсутствии выполните:

```
cp /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

И откройте его для редактирования:

```
nano ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Или для применения изменений ко всем пользователям XFCE (требуются права root):

```
# nano /etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml

```

Приведите Client0_Command к следующему виду:

```
<property name="Client0_Command" type="array">
    <value type="string" value="fusion-icon"/>
    <value type="string" value="--force-compiz"/>
</property>

```

Вместо **--force-compiz** можно использовать **compiz --replace --sm-disable --ignore-desktop-hints ccp**.

Добавьте, если отсутствует, **SaveOnExit property** и установите его значение в **false**:

```
<property name="general" type="empty">
   <property name="FailsafeSessionName" type="string" value="Failsafe"/>
   <property name="SessionName" type="string" value="Default"/>
   <property name="SaveOnExit" type="bool" value="false"/>
 </property>

```

по окончании удалите все старые сессии xfce4:

```
rm -r ~/.cache/sessions

```

Теперь xfce4 вместо Xfwm будет загружать compiz.

### Как Самостоятельный (Standalone) Менеджер Окон

Для использования compiz-fusion будет достаточно пакета compiz-core. Однако потребуются другие дополнительные пакеты, такие как ccsm и emerald (или другой декоратор окон). Позже, в любое время, можно будет доустановить пакеты fusion-icon, compiz-fusion-plugins-main, compiz-fusion-plugins-extra и другие.

Для автостарта compiz-fusion отредактируйте ~/.xinitrc:

```
exec compiz ccp

```

**Обратите внимание:** Вы также можете добавить дополнительные [параметры командной строки](/index.php/Compiz_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E_.28.D0.B1.D0.B5.D0.B7_.22fusion-icon.22.29 "Compiz (Русский)") в свой ~/.xinitrc

Или для использования fusion-icon, настройте ~/.xinitrc так:

```
exec fusion-icon

```

Но, скорее всего, вам понадобятся дополнительные приложения (например панель) для удобной работы. Для автозапуска просто добавьте их в свой ~/.xinitrc таким образом:

```
tint2 &
cairo-dock &
exec fusion-icon 

```

**Обратите внимание:** В первый раз добавьте в список автозапуска эмулятор терминала, дополнительные сведения по [настройке](/index.php/Compiz_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Compiz (Русский)") compiz.

Альтернативный метод, используется скрипт под названием **start-fusion.sh**:

```
#!/bin/sh
# добавить больше приложений или запустить другую панель, трей из pypanel, bmpanel, stalonetray
xfce4-panel&
fusion-icon

```

Если этот скрипт не заработает или появятся проблемы с **dbus**, используйте другой скрипт:

```
#!/bin/sh
cd /home/<yourusername>
#
/usr/bin/X :0.0 -br -audit 0 -nolisten tcp vt7 &
#
export DISPLAY=:0.0
#
sleep 1
#
compiz-manager decoration move resize > /tmp/compiz.log 2>&1 &
# добавить больше приложений или запустить другую панель, трей из pypanel, bmpanel, stalonetray
xfce4-panel&
fusion-icon

```

Сделайте его исполняемым:

```
chmod +x start-fusion.sh

```

И добавьте в свой ~/.xinitrc следующее:

```
exec /path/to/file/start-fusion.sh

```

Не бойтесь использовать много панелей, трей, или запускать большое количество приложений. Для получения дополнительной информации обратитесь к [этому разделу форума](https://bbs.archlinux.org/viewtopic.php?id=51282).

#### Добавление root menu

Для добавления root menu в стиле Openbox, Fluxbox, Blackbox и др. вам понадобится установить пакет [compiz-deskmenu](https://aur.archlinux.org/packages/compiz-deskmenu/), из AUR. После перезапуска Compiz-Fusion у вас появится возможность вызывать меню запуска приложений кликом средней кнопки мыши по рабочему столу.

Если автоматически не заработает - запустите менеджер настроек CompizConfig, в разделе Общие (General Settings) выберите меню Команды (Commands), в одноименной вкладке проверьте, чтоб имелась команда запуска Compiz-Deskmenu, и, соответствующая ей, комбинация клавиш Control+Space.

Если и дальще не будет работать - войдите в меню Переключатель Рабочих Мест (Viewport Switcher), и установите "Plugin for initiate action" в значение: core.

**Обратите внимание:** Для версий 0.8.2+: будет 'commands' вместо 'core', и "Action name for initiate" в run_command0_key

В качестве альтернативы можно использовать [mygtkmenu](https://aur.archlinux.org/packages/mygtkmenu/), расположенный в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

#### Разрешить пользователям выключение/перезагрузку

Изучите страницу [Разрешить пользователям выключение системы](/index.php/%D0%A0%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B8%D1%82%D1%8C_%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8F%D0%BC_%D0%B2%D1%8B%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Разрешить пользователям выключение системы"). При использовании PolicyKit можно добавить команду выключения во вкладке ccsm->General->Commands и назначить для нее горячую клавишу. Или же создать ярлык с командой выключения.

## Разное

### Настройка

[Для нормального использования вам понадобится настроить поведение окон!](/index.php/Compiz_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Compiz (Русский)")

### Использование compiz-manager

Для использования compiz-manager, его сначала нужно установить из репозитория community:

```
pacman -S compiz-manager

```

Compiz-manager, установливается в `/usr/bin/compiz-manager`, и является просто оболочкой для Compiz со всеми его настройками. Например, запустите

```
compiz-manager 

```

и, в выводе консоли, получите дополнительную информацию. Его можно использовать во всех сценариях запускающих Compiz. Очень просто!

### Использование gtk-window-decorator

Для того, чтобы использовать gtk-window-decorator нужно установить пакет _compiz-decorator-gtk_ и, в качестве декоратора окон, вместо "Emerald" выбрать "GTK Window Decorator", сам выбор можно осуществить с помощью fusion-icon или любой другой программы, которая используется вами для настройки compiz.

### gconf: Дополнительные Настройки Compiz

Для получения от Compiz дополнительных результатов можно воспользоваться _gconf-editor_:

```
$ gconf-editor

```

Note that now compiz-core isn't built with gconf support; It is now built with gconf support through compiz-decorator-gtk. So, you need to install it if you want to use gconf-editor to edit your Compiz configuration. The Compiz gconf configuration is located in in the key **apps** > **compiz** > **general** > **allscreens** > **options**.

"Active plugins" is where you specify the plugins you would like to use. Simply edit the key and add a value(refer to the key **apps** > **compiz** > **plugins** to see possible values). Plugins I’ve found useful are screenshot, png, fade, and minimize. Please do not remove those enabled by default.

### Keyboard Shortcuts

Default plugin keyboard shortcuts (plugins have to be activated!):

*   Switch windows: `Alt+Tab`
*   Switch desktops on cube: `Ctrl+Alt+Left/Right Arrow`
*   Move window: `Alt+left-click`
*   Resize window: `Alt+right-click`

A more detailed list can be found under [CommonKeyboardShortcuts](http://wiki.compiz-fusion.org/CommonKeyboardShortcuts) in the Compiz wiki or you can always just look at your plugin's configuration (ccsm).

### ATI R600/R700 Notes

While using fusion-icon you shouldn't experience any problems because it takes care of everything for you, but if you are using one of the autostart methods that don't involve fusion-icon you will run into trouble. For example when using the Xfce autostart method without fusion icon you must edit ~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml per the instructions above. However, if you follow the directions above explicity you will find that compiz does not load. You must instead make your xfce4-session.xml file look like this

```
<property name="Client0_Command" type="array">
 <value type="string" value="LIBGL_ALWAYS_INDIRECT=1"/>
 <value type="string" value="compiz"/>
 <value type="string" value="--sm-disable"/>
 <value type="string" value="--ignore-desktop-hints"/>
 <value type="string" value="ccp"/>
 <value type="string" value="--indirect-rendering"/>
</property>

```

This example targeted Xfce specifically, but it can be adapted to any desktop environment. It's just a matter of figuring out how to add it to the proper config file. The key thing is the required command which if typed on a command line would look like this

```
LIBGL_ALWAYS_INDIRECT=1 compiz --sm-disable --ignore-desktop-hints ccp --indirect-rendering

```

This is how Xfce's session manager interprets the above XML code. Notice that you don't need --replace because you are not first loading xfwm and then compiz.

## Additional Resources

*   [Compiz Website](http://compiz.org) -- including wiki and forum