Ссылки по теме

*   [Единый вид приложений Qt и GTK](/index.php/%D0%95%D0%B4%D0%B8%D0%BD%D1%8B%D0%B9_%D0%B2%D0%B8%D0%B4_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9_Qt_%D0%B8_GTK "Единый вид приложений Qt и GTK")
*   [Qt (Русский)](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")
*   [GNU Project](/index.php/GNU_Project "GNU Project")
*   [GTK+/Development](/index.php/GTK%2B/Development "GTK+/Development")

**Состояние перевода:** На этой странице представлен перевод статьи [GTK+](/index.php/GTK%2B "GTK+"). Дата последней синхронизации: 26 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=GTK%2B&diff=0&oldid=422340).

C [сайта GTK+](http://www.gtk.org):

	*GTK+, или GIMP Toolkit - это мультиплатформенный инструментарий для разработки графического пользовательского интерфейса. Offering a complete set of widgets, GTK+ is suitable for projects ranging from small one-off tools to complete application suites.*

GTK+, GIMP Toolkit, изначально сделан [проектом GNU](/index.php/GNU_Project "GNU Project") для [GIMP](/index.php/GIMP "GIMP"), но теперь это очень популярный инструмент связанный с многими языками. Эта статья будет исследовать инструменты, используемые для настройки GTK+ тем, стилей, иконок, шрифтов и размеров шрифтов, а также подробную ручную настройку.

## Contents

*   [1 Установка](#Установка)
*   [2 Темы](#Темы)
    *   [2.1 GTK+ и Qt](#GTK+_и_Qt)
*   [3 Средства настройки](#Средства_настройки)
*   [4 Настройка](#Настройка)
    *   [4.1 Базовая настройка темы](#Базовая_настройка_темы)
    *   [4.2 Вариант тёмной темы](#Вариант_тёмной_темы)
    *   [4.3 Горячие клавиши](#Горячие_клавиши)
    *   [4.4 Задержка меню GNOME](#Задержка_меню_GNOME)
    *   [4.5 Уменьшить размер виджетов](#Уменьшить_размер_виджетов)
    *   [4.6 Место запуска выбора файла](#Место_запуска_выбора_файла)
    *   [4.7 Наследие поведения скроллбара](#Наследие_поведения_скроллбара)
    *   [4.8 Отключить наложение скролбара](#Отключить_наложение_скролбара)
        *   [4.8.1 Удалить наложенные показателя скролбара](#Удалить_наложенные_показателя_скролбара)
*   [5 GTK+ и HTML с Broadway](#GTK+_и_HTML_с_Broadway)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 Различные темы приложений между GTK+ 2 и GTK+ 3](#Различные_темы_приложений_между_GTK+_2_и_GTK+_3)
    *   [6.2 Тема не применяется к root-приложениям](#Тема_не_применяется_к_root-приложениям)
    *   [6.3 Клиентские декорации](#Клиентские_декорации)
    *   [6.4 Седиль ç/Ç вместо ć/Ć (характерно в основном для Французского языка)](#Седиль_ç/Ç_вместо_ć/Ć_(характерно_в_основном_для_Французского_языка))
    *   [6.5 Подавить предупреждение о accessibility bus](#Подавить_предупреждение_о_accessibility_bus)
    *   [6.6 Не соответствует цвет фона в строке заголовка (TitleBar)](#Не_соответствует_цвет_фона_в_строке_заголовка_(TitleBar))
    *   [6.7 Неправильный фокус событий в тайловых оконных менеджерах](#Неправильный_фокус_событий_в_тайловых_оконных_менеджерах)
    *   [6.8 Поддержка эскизов для диалога файлов GTK + 2](#Поддержка_эскизов_для_диалога_файлов_GTK_+_2)
*   [7 Примеры](#Примеры)
*   [8 Смотрите также](#Смотрите_также)

## Установка

Две версии GTK+ в настоящее время доступны в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Они могут быть [установлены](/index.php/Install "Install") со следующими пакетами:

*   **GTK+ 3.x** доступен с пакетом [gtk3](https://www.archlinux.org/packages/?name=gtk3).
*   **GTK+ 2.x** доступен с пакетом [gtk2](https://www.archlinux.org/packages/?name=gtk2).
*   **GTK+ 1.x** доступен с пакетом [gtk](https://aur.archlinux.org/packages/gtk/).

## Темы

В GTK+ 2, тема по умолчанию *Raleigh*, но Arch Linux имеет пользовательский файл настроек `/usr/share/gtk-2.0/gtkrc`, который устанавливает тему по умолчанию *Adwaita*. В GTK+ 3, тема по умолчанию *Adwaita*, но также включены темы*HighContrast* и *Raleigh*.

Чтобы установить определенную тему, вы можете задать переменные среды.

*   Для GTK+ 2, используйте переменную среду `GTK2_RC_FILES` например:

```
$ GTK2_RC_FILES=/usr/share/themes/Industrial/gtk-2.0/gtkrc gimp

```

	запустит GIMP с Industrial theme.

*   Для GTK+ 3, используйте переменную среду `GTK_THEME` например:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

	Будет запущен GNOME Калькулятор с тёмным вариантом темы Adwaita.

Другие темы могут быть установлены из официальных репозиториев или из [AUR](/index.php/AUR "AUR").

**С поддержкой обеих GTK+ 2 и GTK+ 3:**

*   **Breeze** — GTK+ версия тем виджетов KDE's по умолчанию.

	[https://quickgit.kde.org/?p=breeze-gtk.git](https://quickgit.kde.org/?p=breeze-gtk.git) || [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk)

*   **Deepin** — Тема по умолчанию для рабочего стола Deepin.

	[https://gitcafe.com/Deepin/deepin-gtk-theme](https://gitcafe.com/Deepin/deepin-gtk-theme) || [deepin-gtk-theme](https://www.archlinux.org/packages/?name=deepin-gtk-theme)

*   **GNOME Standard Themes** — Тема по умолчанию для Рабочего стола GNOME. Включает: *Adwaita*, *HighContrast*

	[https://github.com/GNOME/gnome-themes-standard](https://github.com/GNOME/gnome-themes-standard) || [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard)

*   **MATE Themes** — Тема по умолчанию для Рабочего стола MATE. Включает: *BlackMATE*, *BlueMenta*, *Blue-Submarine*, *ContrastHigh*, *ContrastHighInverse*, *GreenLaguna*, *Green-Submarine*, *Menta*, *TraditionalGreen*, *TraditionalOk*, *TraditionalOkTest*

	[https://github.com/mate-desktop/mate-themes](https://github.com/mate-desktop/mate-themes) || [mate-themes](https://www.archlinux.org/packages/?name=mate-themes)

*   **MATE Themes Extras** — Коллекция GTK2/3 тем для Рабочего стола MATE. Включает: *DeLorean-Dark*, *DeLorean*, *GnomishBeige*

	[https://github.com/NiceandGently/mate-themes-extras](https://github.com/NiceandGently/mate-themes-extras) || [mate-themes-extras](https://www.archlinux.org/packages/?name=mate-themes-extras)

*   **Numix** — Плоская и легкая тема с современным видом (GNOME, Openbox, Unity, Xfce).

	[https://numixproject.org/](https://numixproject.org/) || [numix-themes](https://www.archlinux.org/packages/?name=numix-themes)

*   **Arc** — Плоская тема с современным дизайном и прозрачными элементами.

	[https://github.com/horst3180/Arc-theme](https://github.com/horst3180/Arc-theme) || [gtk-theme-arc-git](https://aur.archlinux.org/packages/gtk-theme-arc-git/)

*   **Ceti-2** — Тема для GTK 3, GTK 2 и Gnome-Shell.

	[http://horst3180.deviantart.com/art/Ceti-2-Theme-489193140](http://horst3180.deviantart.com/art/Ceti-2-Theme-489193140) || [ceti-2-themes](https://aur.archlinux.org/packages/ceti-2-themes/)

*   **Clearlooks-Phénix** — GTK3 тема визуально близкая к Clearlooks.

	[https://github.com/jpfleury/clearlooks-phenix](https://github.com/jpfleury/clearlooks-phenix) || [clearlooks-phenix-gtk-theme](https://aur.archlinux.org/packages/clearlooks-phenix-gtk-theme/)

*   **Gnome-breeze** — Тема GTK создана в соответствии с новой Plasma 5 Breeze.

	[https://github.com/dirruk1/gnome-breeze](https://github.com/dirruk1/gnome-breeze) || [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/)

*   **Greybird** — Серая и синяя тема Xfce, используемая по умолчанию в Xubuntu 12.04.

	[http://shimmerproject.org/our-projects/greybird/](http://shimmerproject.org/our-projects/greybird/) || [xfce-theme-greybird](https://aur.archlinux.org/packages/xfce-theme-greybird/)

*   **Orion** — Современная, светлая тема GTK.

	[http://deviantart.com/view/281431756](http://deviantart.com/view/281431756) || [gtk-theme-orion](https://aur.archlinux.org/packages/gtk-theme-orion/)

*   **Vertex** — Тема для GTK 3, GTK 2, Gnome-Shell и Cinnamon.

	[http://horst3180.deviantart.com/art/Vertex-Theme-470663601](http://horst3180.deviantart.com/art/Vertex-Theme-470663601) || [vertex-themes](https://aur.archlinux.org/packages/vertex-themes/)

*   **Zukitwo** — Темы для GTK, gnome-shell и др.

	[http://gnome-look.org/content/show.php/Zukitwo?content=140562](http://gnome-look.org/content/show.php/Zukitwo?content=140562) || [zukitwo-themes](https://aur.archlinux.org/packages/zukitwo-themes/)

**Поддерживается только GTK+ 2:**

*   **GTK+ Engines** — Движок тем для GTK+ 2\. Включает: *Clearlooks*, *Crux*, *Industrial*, *Mist*, *Redmond*, *ThinIce*

	[https://github.com/GNOME/gtk-engines](https://github.com/GNOME/gtk-engines) || [gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines)

*   **Xfce Gtk+ Engine** — Xfce Gtk+-2.0 движок и темы

	[http://git.xfce.org/xfce/gtk-xfce-engine/](http://git.xfce.org/xfce/gtk-xfce-engine/) || [gtk-xfce-engine](https://www.archlinux.org/packages/?name=gtk-xfce-engine)

*   **Oxygen-Gtk** — Порт стандартных тем KDE виджетов (Oxygen) в GTK2

	[https://projects.kde.org/projects/playground/artwork/oxygen-gtk/](https://projects.kde.org/projects/playground/artwork/oxygen-gtk/) || [oxygen-gtk2](https://www.archlinux.org/packages/?name=oxygen-gtk2)

*   **Aurora Gtk Engine** — Последний участник семейства Clearlooks.

	[http://gnome-look.org/content/show.php/Aurora+Gtk+Engine?content=56438](http://gnome-look.org/content/show.php/Aurora+Gtk+Engine?content=56438) || [gtk-engine-aurora](https://aur.archlinux.org/packages/gtk-engine-aurora/)

*   **Openbox Themes** — Различные темы для Оконного менеджера Openbox.

	[https://www.debian.org/](https://www.debian.org/) || [openbox-themes](https://www.archlinux.org/packages/?name=openbox-themes)

*   **QtCurve** — Настраиваемый набор стилей виджетов для KDE и Gtk.

	[https://projects.kde.org/projects/playground/base/qtcurve](https://projects.kde.org/projects/playground/base/qtcurve) || [qtcurve-gtk2](https://www.archlinux.org/packages/?name=qtcurve-gtk2)

Есть ряд дополнительных тем GTK+ в [AUR](/index.php/AUR "AUR"): [поиск gtk-theme](https://aur.archlinux.org/packages.php?K=gtk-theme), [поиск gtk2-theme](https://aur.archlinux.org/packages.php?K=gtk2-theme), [поиск gtk3-theme](https://aur.archlinux.org/packages.php?K=gtk3-theme).

**Примечание:**

*   Так как GTK+ 3 быстро меняется, GTK+ 3 темы требуют переработки после выпуска GTK+ 3\. По этой причине, не все темы GTK+ 3, могут выглядеть как предполагалось при использовании последней GTK + 3 версии.
*   Некоторые темы могут потребовать [librsvg](https://www.archlinux.org/packages/?name=librsvg) для правильного отображения, но не все указывают его в качестве зависимости. Попробуйте установить его, если выбранная тема выглядит сломанной.
*   Некоторые темы не могут использоваться для отображения панели "как есть" (

светлый текст на светлом фоне), так что вам нужно использовать предоставленный [фон панели](http://i.imgur.com/QmeyN.png).

### GTK+ и Qt

Если у вас есть GTK+ и Qt (KDE) приложения на рабочем столе, то вы знаете, что их внешность не сочетается/не совпадает.Если вы хотите, чтобы ваши стили GTK+ соответствовали вашим стилям Qt прочитайте [различный вид GTK+ 2 и GTK+ 3 приложений](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform look for Qt and GTK applications (Русский)").

## Средства настройки

Большинство крупных [окружений рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") предоставляют инструменты для настройки тем GTK+, иконок, шрифта и размера шрифта, и управляют этими настройками с помощью [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html):

*   Если вы используете [Cinnamon](/index.php/Cinnamon "Cinnamon"), используйте Themes tool (*cinnamon-settings themes*): идите в *Параметры > Параметры системы > Оформление*.
*   Если вы используете [Enlightenment](/index.php/Enlightenment "Enlightenment"): идите в *Settings > All > Look > Application Theme*.
*   Если вы используете [GNOME](/index.php/GNOME "GNOME"), используйте Gnome Tweak Tool (*gnome-tweak-tool*): установите [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool), идите в *GNOME Tweak Tool > Внешний вид*.
*   Если вы используете [MATE](/index.php/MATE "MATE"), используйте Appearance Preferences tool (*mate-appearance-properties*): идите в *Система > Параметры > Внешний вид*.
*   Если вы используете [Xfce](/index.php/Xfce "Xfce"), используйте Appearance tool: идите *Настройки > Внешний вид*.
*   Если вы используете [Openbox](/index.php/Openbox "Openbox"), идите в *obconf > Тема* или lxappearance с установленным lxappearance-obconf, тогда *lxappearance-obconf > Рамка окна > Тема*.

Другие графические инструменты, как правило перезаписывают [файлы настроек](#Настройка).

**Поддерживаются оба GTK+ 2 и GTK+ 3:**

*   **KDE GTK Configurator** — Приложение, которое позволяет изменять стиль и шрифт GTK+2 и Gtk+3 приложений.

	[https://projects.kde.org/kde-gtk-config](https://projects.kde.org/kde-gtk-config) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

	После установки, `kde-gtk-config` также можно найти в *System Settings > Application Appearance > GTK*.

*   **LXAppearance** — независимая от Окружения рабочего стола утилита настройки GTK+2 и GTK+3, от проекта LXDE (не требует других частей LXDE).

	[http://wiki.lxde.org/en/LXAppearance](http://wiki.lxde.org/en/LXAppearance) || [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)

**Поддерживается только GTK+ 2:**

*   **GTK-KDE4** — Приложение, которое позволяет изменять стиль и шрифт GTK+2 приложений в KDE4.

	[http://kde-look.org/content/show.php?content=74689](http://kde-look.org/content/show.php?content=74689) || [gtk-kde4](https://aur.archlinux.org/packages/gtk-kde4/)

	После установки, `gtk-kde4` также можно найти в *System Settings > Lost and Found > GTK style*.

*   **GTK+ Change Theme** — Маленькая программа, которая позволяет изменять вашу GTK+ 2.0 тему (считается лучшей альтернативой *switch2*).

	[http://plasmasturm.org/code/gtk-chtheme/](http://plasmasturm.org/code/gtk-chtheme/) || [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)

*   **GTK+ Preference Tool** — Переключает GTK+ темы и меняет шрифт.

	[http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool](http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool) || [gtk2_prefs](https://aur.archlinux.org/packages/gtk2_prefs/)

*   **GTK+ Theme Switch** — Простой переключатель GTK+ тем.

	[http://muhri.net/nav.php3?node=gts](http://muhri.net/nav.php3?node=gts) || [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)

## Настройка

Параметры GTK+ могут быть вручную заданы в файлах настройки, но окружение рабочего стола и приложения могут переопределить эти параметры. В зависимости от версии GTK+, эти файлы находятся по пути:

*   GTK+ 2 конкрентного пользователя: `~/.gtkrc-2.0` или `~/.config/gtkrc-2.0`
*   GTK+ 2 всей системы: `/etc/gtk-2.0/gtkrc`
*   GTK+ 3 конкрентного пользователя: `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, или `$HOME/.config/gtk-3.0/settings.ini` если не установлена `$XDG_CONFIG_HOME`
*   GTK+ 3 всей системы: `/etc/gtk-3.0/settings.ini`

**Примечание:**

*   Смотрите [GTK+ 3 свойства *GtkSettings*](http://library.gnome.org/devel/gtk3/stable/GtkSettings.html#GtkSettings.properties) (и [GTK+ 2 свойства](http://library.gnome.org/devel/gtk2/stable/GtkSettings.html#GtkSettings.properties)) в справочном руководстве программирования GTK+, для полного перечня поддерживаемых в настоящее время вариантов настройки GTK+.
*   Некоторые настройки, описанных ниже (например `gtk-icon-sizes`) являются устаревшими и игнорируется с GTK+ 3.10.
*   При редактировании файлов настроек GTK+, только вновь запущенные приложения будет отображать изменения.

### Базовая настройка темы

Для ручного изменения темы GTK+, иконок, шрифтов и размера шрифтов, добавьте следующие файлы настроек, например:

**GTK+ 2:**

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Adwaita"
gtk-theme-name = "Adwaita"
gtk-font-name = "DejaVu Sans 11"
```

**GTK+ 3:**

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings]
gtk-icon-theme-name = Adwaita
gtk-theme-name = Adwaita
gtk-font-name = DejaVu Sans 11
```

**Примечание:** Название темы значков определено в файле индекса темы, а *не* в имени своего каталога.

### Вариант тёмной темы

Некоторые темы GTK+ 3 содержат тёмный вариант темы, но он используется только когда приложение запрашивает именно его. Чтобы использовать вариант темной темы со всеми GTK+ 3 приложениями, установите:

```
gtk-application-prefer-dark-theme = true

```

### Горячие клавиши

Keyboard shortcuts (otherwise known as *accelerators* in GTK+) may be changed by hovering the mouse over the respective menu item, and pressing the desired key combination. To enable this feature, set:

```
gtk-can-change-accels = 1

```

### Задержка меню GNOME

Этот параметр управляет задержкой между "указыванием мыши" на меню и "открытием меню". Эта задержка измеряется в миллисекундах.

```
gtk-menu-popup-delay = 0

```

### Уменьшить размер виджетов

Если у вас небольшой экран, или вы просто не любите большие иконки и виджеты, вы можете изменить их размер.

Для того чтобы иконки были без текста в панели инструментов ([(допустимые значения)](https://developer.gnome.org/gtk3/stable/gtk3-Standard-Enumerations.html#GtkToolbarStyle)), используйте

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

Чтобы использовать меньшие иконки:

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

Или, чтобы удалить иконки из кнопок полностью:

```
gtk-button-images = 0

```

Вы также можете удалить из меню иконки:

```
gtk-menu-images = 0

```

Смотрите также [[1]](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/) и [[2]](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812).

### Место запуска выбора файла

Чтобы открывать диалог "выбор файла" (например при открытии/сохранении) в **текущем рабочем каталоге** а не в **последнем** (recent) месте (обычно **текущий-рабочий-каталог** это **домашний каталог**), сделайте следующее:

Для **GTK+ 3**

Измените DConf с *gsettings*:

```
$ gsettings set org.gtk.Settings.FileChooser startup-mode cwd

```

Для **GTK+ 2**:

Измените файл настроек `~/.config/gtk-2.0/gtkfilechooser.ini`:

 `~/.config/gtk-2.0/gtkfilechooser.ini`  `StartupMode=cwd` 

### Наследие поведения скроллбара

**Примечание:** Этот параметр не повиновался всеми приложениями GTK+.

**Совет:** Наследство поведения прокрутки может быть надежно достигнуто, просто используя правую кнопку мыши вместо левой кнопки мыши.

До GTK+ 3.6, щелчёк в обе стороны от ползунка сдвинет прокрутку в направлении щелчка, примерно на одну страницу. Так GTK+ 3.6, слайдер сразу перейдёт к позиции мыши. Такое поведение можно отменить в некоторых приложениях путем создания файла с содержимым, приведенным ниже:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false

```

### Отключить наложение скролбара

С GTK+ 3.15, наложения полосы прокрутки по умолчанию включено, что означает, что полосы прокрутки будут показываться только при наведении курсора мыши на GTK+ 3 приложение. Такое поведение можно отменить, установив следующую переменную окружения: `GTK_OVERLAY_SCROLLING=0`.

Смотрите [Переменные окружения#Графические приложения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Графические_приложения "Environment variables (Русский)").

#### Удалить наложенные показателя скролбара

Позиции наложения прокрутки обозначены тонкими пунктирными линиями в окне приложения. Эти пунктирные линии будут присутствовать, даже если накладка прокрутка отключена с помощью переменной сред, которая обсуждались в предыдущем разделе. Для удаления индикаторных линий, создайте следующий файл:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Remove dotted lines from GTK+ 3 applications */
.undershoot.top, .undershoot.right, .undershoot.bottom, .undershoot.left { background-image: none; }

```

## GTK+ и HTML с Broadway

GDK Broadway обеспечивает поддержку для отображения GTK+ приложений в веб-браузере, используя HTML5 и веб-соккеты. [[3]](https://developer.gnome.org/gtk3/3.8/gtk-broadway.html)

При использовании broadwayd, укажите номер дисплея для использования с префиксом двоеточие, похожий на X. На дисплее по умолчанию номер 1.

```
$ display_number=:5

```

Запустите его.

```
$ broadwayd $display_number 

```

Порт используемый по умолчанию

```
port = 8080 + ($display_number - 1)

```

Укажите ваш браузер [http://localhost:port](http://localhost:port)

Запускаемые приложения

```
$ GDK_BACKEND=broadway BROADWAY_DISPLAY=$display_number *<<app>>*

```

В качестве альтернативы, можно установить адрес и порт

```
$ broadwayd --port $port_number --address $address $display_number

```

## Решение проблем

### Различные темы приложений между GTK+ 2 и GTK+ 3

В общем, если выбранная тема имеет поддержку как для GTK+ 2 и GTK+ 3, тема будет применяться для всех GTK+ 2 и GTK+ 3 приложений. Если выбранная тема имеет поддержку только GTK+ 2, будет использоваться для GTK+ 2 приложений, и GTK+ тема по умолчанию будет использоваться для GTK+ 3 приложений. Если выбранная тема имеет поддержку только GTK+ 3, то будет использована для GTK+ 3 приложений, и GTK+ тема по умолчанию будет использоваться для GTK+ 2 приложений. Таким образом, для согласования тем приложений, лучше использовать тему, которая имеет поддержку как GTK+ 2 так и GTK+ 3.

Вы можете найти установленные темы на вашей системе с поддержкой обоих версий GTK+ 2 и GTK+ 3, используя эту команду (не работает с именами, содержащими пробелы):

```
find $(find ~/.themes /usr/share/themes/ -wholename "*/gtk-3.0" | sed -e "s/^\(.*\)\/gtk-3.0$/\1/") -wholename "*/gtk-2.0" | sed -e "s/.*\/\(.*\)\/gtk-2.0/\1"/

```

### Тема не применяется к root-приложениям

Пользовательский файл темы (`$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, `~/.gtkrc-2.0`) не может быть прочитан другими аккаунтами, выбранная тема не будет применяться к [приложениям X запущенных от root](/index.php/Running_X_apps_as_root "Running X apps as root"). Возможное решение включает в себя:

*   Настройку файла темы для всей системы: `/etc/gtk-3.0/settings.ini` (GTK+ 3) или `/etc/gtk-2.0/gtkrc` (GTK+ 2)
*   Создание символьной ссылки, т.е.

```
# ln -s /home/[Имя_Пользователя]/.gtkrc-2.0 /root/.gtkrc-2.0

```

*   Смена темы от root

```
# gksu lxappearance

```

*   Используйте настройки демона (это в большинстве окружений рабочего стола). Вариант desktop-agnostic использует [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html) доступный в [AUR](/index.php/AUR "AUR") [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/).

### Клиентские декорации

С версии GTK 3.12 введены [Клиентские декорации](http://blogs.gnome.org/mclasen/2013/12/05/client-side-decorations-in-themes/), которые действуют в титлбаре от оконного менеджера. Это может решить такие вопросы как [двойной титл-бар](http://redmine.audacious-media-player.org/boards/1/topics/1135), нет титл-бара вообще, или [двойная тень](https://github.com/chjj/compton/issues/189) с включенным композитингом.

Чтобы удалить тень и зазор вокруг окон (например, в сочетании с тайловым оконным менеджером), создайте следующий файл:

 `~/.config/gtk-3.0/gtk.css` 
```
.window-frame, .window-frame:backdrop {
 box-shadow: 0 0 0 black;
 border-style: none;
 margin: 0;
 border-radius: 0;
}

.titlebar {
 border-radius: 0;
}

.window-frame.csd.popup {
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2), 0 0 0 1px rgba(0, 0, 0, 0.13);
}

.header-bar {
  background-image: none;
  background-color: #ededed;
  box-shadow: none;
}
/* You may want to use this if you don't like the double title.
GtkLabel.title {
    opacity: 0;
}*/

```

Чтобы настроить кнопки на панели заголовка, используйте опцию `gtk-decoration-layout`. [[4]](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-decoration-layout) Приведенный ниже пример удаляет все кнопки:

 `~/.config/gtk-3.0/settings.ini`  `gtk-decoration-layout=menu:` 

### Седиль ç/Ç вместо ć/Ć (характерно в основном для Французского языка)

Смотрите [[5]](https://bugs.launchpad.net/ubuntu/+source/gtk+2.0/+bug/518056), и [[6]](https://bugs.launchpad.net/ubuntu/+source/gtk+2.0/+bug/518056/comments/37) для решения проблемы с использованием Xcompose (US international layout).

### Подавить предупреждение о accessibility bus

Если вы не используете функции [Gnome Accessibility](https://wiki.gnome.org/Accessibility) (специальных возможностей),вы можете получать такие предупреждения :

```
WARNING **: Couldn't connect to accessibility bus:

```

вы можете подавить предупреждение, запуская программу с `NO_AT_BRIDGE=1` или установить в качестве [глобальной переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)")

### Не соответствует цвет фона в строке заголовка (TitleBar)

Если вы используете [оконный менеджер](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") который использует тему декорации окон, которая имитирует цвет темой фона GTK+, вы можете обнаружить, что цвет заголовка окна больше не совпадает полностью с цветом приложений в некоторых приложениях GTK+ 3\. В качестве обходного пути, создайте следующий файл:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Always use background color */
GtkWindow {
    background-color: @theme_bg_color;
}

/* Fix tooltip background override */
.tooltip {
    background-color: rgba(0, 0, 0, 0.8);
}

.tooltip * {
    background-color: transparent;
}

/* Fix Nautilus desktop window background override */
NautilusWindow {
     background-color: transparent; 
}

```

### Неправильный фокус событий в тайловых оконных менеджерах

**Примечание:** Это отключит поддержку Сенсорного экрана для приложений GTK3\. [[7]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c14)

[Определите](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_переменных "Environment variables (Русский)") `GDK_CORE_DEVICE_EVENTS=1` для использования стиля ввода GTK2, вместо xinput2\. [[8]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c10)

### Поддержка эскизов для диалога файлов GTK + 2

Установите [gtk2-patched-filechooser-icon-view](https://aur.archlinux.org/packages/gtk2-patched-filechooser-icon-view/) чтобы получить возможность просмотра файлов в виде миниатюр, вместо списка, в файловом браузере GTK +.

## Примеры

Пример настройки GTK+ 2:

 `~/.gtkrc-2.0` 
```
# GTK theme
include "/usr/share/themes/Clearlooks/gtk-2.0/gtkrc"

# Font
style "myfont" {
    font_name = "DejaVu Sans 8"
}
widget_class "*" style "myfont"
gtk-font-name = "DejaVu Sans 8"

# Icon theme
gtk-icon-theme-name = "Tango"

# Toolbar style
gtk-toolbar-style = GTK_TOOLBAR_ICONS
```

GTK+ 3 пример настройки конвертации GTK+ 2.x в GTK+ 3.x с [lxappearance](https://www.archlinux.org/packages/?name=lxappearance):

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings] 
gtk-theme-name=TraditionalOk
gtk-icon-theme-name=Fog
gtk-font-name=Luxi Sans 12
gtk-cursor-theme-name=mate
gtk-cursor-theme-size=24
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_LARGE_TOOLBAR
gtk-button-images=1
gtk-menu-images=1
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb
```

## Смотрите также

*   [Официальный сайт GTK+ (Англ.)](http://www.gtk.org/)
*   [Статья на Википедии о GTK+ (Рус.)](https://en.wikipedia.org/wiki/ru:GTK%2B "wikipedia:ru:GTK+")
*   [Руководство GTK+ 2.0 (Англ.)](http://developer.gnome.org/gtk-tutorial/stable/)
*   [Справочное руководство GTK+ 3 (Англ.)](http://developer.gnome.org/gtk3/stable/)
*   [Руководство gtkmm (Англ.)](http://developer.gnome.org/gtkmm-tutorial/stable/)
*   [Справочное руководство gtkmm (Англ.)](http://developer.gnome.org/gtkmm/stable/)