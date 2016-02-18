## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Стили](#.D0.A1.D1.82.D0.B8.D0.BB.D0.B8)
    *   [2.1 KDE4 Oxygen](#KDE4_Oxygen)
    *   [2.2 QtCurve](#QtCurve)
*   [3 Theme Engines](#Theme_Engines)
    *   [3.1 GTK-QT-Engine](#GTK-QT-Engine)
        *   [3.1.1 Make it work with OpenOffice](#Make_it_work_with_OpenOffice)
    *   [3.2 QGtkStyle](#QGtkStyle)
        *   [3.2.1 Having trouble making your Qt applications use QGtkStyle?](#Having_trouble_making_your_Qt_applications_use_QGtkStyle.3F)
*   [4 Other Tricks](#Other_Tricks)
    *   [4.1 Файловые диалоги KDE для GTK2 приложения](#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.B5_.D0.B4.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8_KDE_.D0.B4.D0.BB.D1.8F_GTK2_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.2 Использование своих стилей GTK](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B2.D0.BE.D0.B8.D1.85_.D1.81.D1.82.D0.B8.D0.BB.D0.B5.D0.B9_GTK)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 How do I set styles for each toolkit?](#How_do_I_set_styles_for_each_toolkit.3F)
        *   [5.1.1 Стили KDE3 и QT3](#.D0.A1.D1.82.D0.B8.D0.BB.D0.B8_KDE3_.D0.B8_QT3)
        *   [5.1.2 Стили QT4](#.D0.A1.D1.82.D0.B8.D0.BB.D0.B8_QT4)
        *   [5.1.3 Стили GTK2](#.D0.A1.D1.82.D0.B8.D0.BB.D0.B8_GTK2)
        *   [5.1.4 Стили GTK1](#.D0.A1.D1.82.D0.B8.D0.BB.D0.B8_GTK1)
    *   [5.2 Темы не работают в GTK приложениях](#.D0.A2.D0.B5.D0.BC.D1.8B_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82_.D0.B2_GTK_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.D1.85)

# Введение

Программы, основанные на [Qt](http://ru.wikipedia.org/wiki/Qt) и [GTK+](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") используют разные способы отображения графического интерфейса. Они используют различные темы, стили, иконки и многие другие вещи, так что выглядят довольно непохоже. Эта статья поможет Вам сделать Ваши Qt и GTK+ приложения выглядящими более одинаково и интегрированно.

*   **Тема** - Набор стилей, тема иконок и цветовая схема.
*   **Стиль** - Graphical layout; look.
*   **Тема иконок** - Глобальный набор иконок.
*   **Цветовая схема** - Глобальный набор цветов, используемый в сочетании со стилем.

# Стили

Здесь описываются стили, созданные для интеграции Qt и GTK+ приложений. С ними, Вы можете сделать так, чтобы Ваши приложения выглядели одинаково, не зависимо от тулкита, на котором они написаны.

## KDE4 Oxygen

Версия для QT4 устанавливается вместе с [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)"). Версия для [GTK+](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)"), которая называется [oxygen-molecule-theme](https://aur.archlinux.org/packages/oxygen-molecule-theme/), доступна в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

## QtCurve

Доступный для *qt4* (kde4), *qt3* (kde3), и *gtk2* (gnome) через **[extra]** репозиторий, этот стиль также достаточно популярен. Вы можете установить его, используя pacman.

```
# pacman -S qtcurve-gtk2 qtcurve-kde3 qtcurve-kde4

```

# Theme Engines

A Theme Engine can be thought of as a thin layer API which translates themes (excluding icons) between one or more toolkits. These engines add some extra code in the process and it is arguable that this kind of a solution is not as elegant and optimal as using native styles.

## GTK-QT-Engine

This one is for use by GTK+ applications running in KDE, which basically means this is for KDE. It applies all Qt settings (styles, fonts, not icons though) to the GTK+ applications and uses the style plug-ins directly. Please note that there are rendering issues with some Qt styles.

```
# pacman -S gtk-qt-engine

```

You can access it from:

	*Control Center (kcontrol) --> Appearance & Themes --> GTK Styles and Fonts*

If you want to remove it entirely and every trace of it, you should delete the following files:

*   ~/.gtkrc2.0-kde
*   ~/.kde/env/gtk-qt-engine.rc.sh
*   ~/gtk-qt-engine.rc

### Make it work with OpenOffice

Вставьте (пользователем root):

```
export SAL_GTK_USE_PIXMAPPAINT=1

```

в /etc/profile. В systemsettings (KDE4) удостоврьтесь, что "use my KDE style in GTK applications" выбрано в Appearance > GTK styles and fonts.

## QGtkStyle

This is a Qt style which intends to make applications blend perfectly into the GNOME desktop environment by using GTK to render all components. To use this style you must have at least GTK+ 2.0 and Qt 4.3, although Qt 4.4 or higher is preferred.

**Обратите внимание:** Начиная с версии 4.5 этот стиль включён в Qt. Вам не надо устанавливать этот пакет самому.

### Having trouble making your Qt applications use QGtkStyle?

Qt won't apply QGtkStyle correctly if GTK is using the [GTK-QT-Engine](/index.php/Uniform_Look_for_QT_and_GTK_Applications#GTK-QT-Engine "Uniform Look for QT and GTK Applications"). Qt determines whether the [GTK-QT-Engine](/index.php/Uniform_Look_for_QT_and_GTK_Applications#GTK-QT-Engine "Uniform Look for QT and GTK Applications") is in use by reading the GTK configuration files listed in the environmental variable **GTK2_RC_FILES**. If the environmental variable is not set properly, Qt assumes you are using the [GTK-QT-Engine](/index.php/Uniform_Look_for_QT_and_GTK_Applications#GTK-QT-Engine "Uniform Look for QT and GTK Applications"), sets QGtkStyle to use the style GTK style *Clearlooks*, and outputs an error message:

```
QGtkStyle cannot be used together with the GTK_Qt engine.

```

Пользователи [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)") и других неGNOME окружений могут встретить эту проблему. Вот её решение:

*   Tell Qt where to look for your GTK configuration file by adding the following to your `.xinitrc` file:
    *   To add multiple paths, separate them with colons.
    *   The $HOME part will expand to be path to your user's home directory. Using the ~ shortcut won't work.

 `.xinitrc` 
```
...
export GTK2_RC_FILES="$HOME/.gtkrc-2.0"
...
```

*   В `.gtkrc-2.0` вы должны указать тему GTK. Например:
    *   This is usually done for you by an [application which sets GTK2 Styles](/index.php/Uniform_Look_for_QT_and_GTK_Applications#.D0.A1.D1.82.D0.B8.D0.BB.D0.B8_GTK2 "Uniform Look for QT and GTK Applications")

 `.gtkrc-2.0` 
```
...
gtk-theme-name="Crux"
...
```

However it seems in sume cases those tools insert only an include directive like

 `.gtkrc-2.0` 
```
...
include "/usr/share/themes/SomeTheme/gtk-2.0/gtkrc"
...
```
which apparently is not recognized by all versions of QGtkStyle. You can hotfix this problem by inserting the gtk-theme-name manually in your .gtkrc-2.0 like above, note however that Gtk2-style-change applications might overwrite that change when you use them.

Чтобы выбрать тему GTK для Qt приложений введите:

```
qtconfig

```

# Other Tricks

## Файловые диалоги KDE для GTK2 приложения

KGtk is a wrapper script that LD_PRELOAD to force KDE file dialogs (open, save, etc) in GTK2 apps. Если вы используете KDE и предпочитаете нативные файловые диалоги, тогда установите kgtk из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). После установки вы сможете запускать GTK2 приложения через kgtk-wrapper двумя способами (в примерах — gimp):

*   Запуская kgtk-wrapper напрямую используя GTK2 приложение как аргумент.

```
/usr/local/bin/kgtk-wrapper gimp

```

*   Создав символическую ссылку на kgtk используя имя вашего GTK2 приложения. Тогда вы сможете запускать /usr/local/bin/gimp, когда захотите запустить gimp с файловыми диалогами KDE.

```
ln -s /usr/local/bin/kgtk-wrapper /usr/local/bin/gimp
/usr/local/bin/gimp

```

## Использование своих стилей GTK

Вы можете использовать свои стили для определённых приложений GTK. Для этого: GTK2_RC_FILES=/path/to/theme/gtk-2.0/gtkrc имя_приложения

Например:

```
GTK2_RC_FILES=/usr/share/themes/QtCurve/qtk-2.0/gtkrc firefox

```

Так запустится firefox с темой QtCurve.

# Решение проблем

## How do I set styles for each toolkit?

You can use the following methods to change the theme used in each environment.

#### Стили KDE3 и QT3

*   Control Center (kcontrol) --> Appearance & Themes --> Style --> Widget Style
*   kde-config --style [название стиля]
*   /opt/qt/bin/qtconfig

#### Стили QT4

*   /usr/bin/qtconfig

#### Стили GTK2

*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)
*   [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)
*   [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)
*   [gtk2_prefs](https://www.archlinux.org/packages/?name=gtk2_prefs)
*   [Базовая настройка темы](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.91.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.82.D0.B5.D0.BC.D1.8B "GTK+ (Русский)")

#### Стили GTK1

*   switch (gtk-theme-switch package)

## Темы не работают в GTK приложениях

If the style or theme engine you setup isn't showing in your GTK apps, тогда возможно ваши файлы настроек GTK почему-то не загружаются. Вы можете проверить где ваша система предполагает увидеть эти файлы, для этого введите:

```
$ export | grep gtk

```

Обычно файлы такие: ~/.gtkrc для GTK1, ~/.gtkrc2.0 или ~/.gtkrc2.0-kde для GTK2.

Новые версии gtk-qt-engine используют ~/.gtkrc2.0-kde and set the export variable in ~/.kde/env/gtk-qt-engine.rc.sh. Если вы недавно удалили gtk-qt-engine и пытаетесь поставить тему GTK, вам надо удалить ~/.kde/env/gtk-qt-engine.rc.sh и перезагрузиться. Doing this will ensure that GTK looks for it's settings in the standard ~/.gtkrc2.0 instead of ~/.gtkrc2.0-kde