| **Вцілому**  |
| В цій статті детально описується налаштування тем для GTK+ на QT застосунках щоб забезпечити єдиний стиль. Ця стаття охоплює налаштування, движки тем, хитрощі та пошук несправностей. |
| **Пов’язані** |
| [[[GTK+](/index.php/GTK%2B_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "GTK+ (Українська)")]] |

## Contents

*   [1 Вступ](#.D0.92.D1.81.D1.82.D1.83.D0.BF)
*   [2 Стилі](#.D0.A1.D1.82.D0.B8.D0.BB.D1.96)
    *   [2.1 Зміна стилів](#.D0.97.D0.BC.D1.96.D0.BD.D0.B0_.D1.81.D1.82.D0.B8.D0.BB.D1.96.D0.B2)
    *   [2.2 KDE4 Oxygen](#KDE4_Oxygen)
    *   [2.3 QtCurve](#QtCurve)
    *   [2.4 Інше](#.D0.86.D0.BD.D1.88.D0.B5)
*   [3 Двигун Тем](#.D0.94.D0.B2.D0.B8.D0.B3.D1.83.D0.BD_.D0.A2.D0.B5.D0.BC)
    *   [3.1 Двигуни GTK-QT](#.D0.94.D0.B2.D0.B8.D0.B3.D1.83.D0.BD.D0.B8_GTK-QT)
        *   [3.1.1 Заставити працювати з OpenOffice](#.D0.97.D0.B0.D1.81.D1.82.D0.B0.D0.B2.D0.B8.D1.82.D0.B8_.D0.BF.D1.80.D0.B0.D1.86.D1.8E.D0.B2.D0.B0.D1.82.D0.B8_.D0.B7_OpenOffice)
    *   [3.2 QGtkStyle](#QGtkStyle)
        *   [3.2.1 Having trouble making your Qt applications use QGtkStyle?](#Having_trouble_making_your_Qt_applications_use_QGtkStyle.3F)
*   [4 Other Tricks](#Other_Tricks)
    *   [4.1 KDE file dialogs for GTK2 apps](#KDE_file_dialogs_for_GTK2_apps)
    *   [4.2 Using custom GTK style](#Using_custom_GTK_style)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 How do I set styles for each toolkit?](#How_do_I_set_styles_for_each_toolkit.3F)
        *   [5.1.1 KDE3 and QT3 styles](#KDE3_and_QT3_styles)
        *   [5.1.2 QT4 styles](#QT4_styles)
        *   [5.1.3 GTK2 styles](#GTK2_styles)
        *   [5.1.4 GTK1 styles](#GTK1_styles)
    *   [5.2 Themes not working in GTK apps](#Themes_not_working_in_GTK_apps)

# Вступ

Програми основані на [Qt](http://uk.wikipedia.org/wiki/Qt)- та [GTK+](/index.php/GTK%2B_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "GTK+ (Українська)") використовують різні інструментарій віджет для відображення графічного інтерфейсу користувача. Між іншим кожен з них іде за замовчуванням з разнити темами, стилями та наборами значків, так що "зовнішній вигляд" істотно відрізняються. Ця стаття допоможе тобі зробити вигляд застосунків Qt та GTK+ подібними для більш раціонального та "інтегрованого" робочого столу.

_"Qt (вимовляється як "кюте") крос-платформний фреймвок для розробки застосунків, який широко використовується для розробки програм GUI (в даному випадку він відомий як інструментарій віджетів), і зазвичай використовується для розробки не-GUI програм таких як консолі інструменти і сервери."_

*   **Тема** - Колекція стилів, теми значків і теми кольору.
*   **Стиль** - Графічний макет; вигляд.
*   **Тема значків** - Набір глобальних значків.
*   **Тема кольору** - Набір глобальних кольорів які використовуються у поєднанні зі стилем.

# Стилі

Тут описуються стилі, створені для інтеграції застосунків Qt та GTK+. З їх допомогою ви можете мати один вид для всіх додатків незалежно від інструментарію з допомогою яких вони були написані.

## Зміна стилів

Для зміни стилю в Qt3 і застосунуках в KDE3:

	_Центр керування (kcontrol) --> Вигляд і Теми --> Стиль_

Для зміни стилю застосунків Qt3 з зовні KDE3

	_Qt Налаштування (qt3config) --> Вигляд --> Вибір стилю GUI_

Для зміни стилю застосунків Qt4 і KDE4 в KDE4:

	_Системне настроювання (systemsettings) --> Вигляд --> Стиль_

Для зміни стилю застосунків Qt4 ззовні KDE4

	_Qt Налаштування (qtconfig) --> Вигляд --> Вибір стилю GUI_

Для зміни стилю GTK+ версії 2 в KDE3:

```
# pacman -S gtk-chtheme

```

Запустіть, і ви матимене можливість змінити стиль. Ви також можете змінити шрифти. Будьласка зазначте, будь-які відкриті прогами треба буде перезавантажити для того, щоб новий вигляд набув чинності. Крім того, ви можете зробити те ж саме з двигуном, що згадуються нижче.

## KDE4 Oxygen

QT4 встановлюється з KDE.

Є також програма GTK+, що називається [oxygen-molecule](http://kde-look.org/content/show.php?content=103741) і вона доступна з репозиторію [oxygen-molecule-theme](https://aur.archlinux.org/packages/oxygen-molecule-theme/) AUR. Її ціль забезпечити однаковий вигляд застосунків GTK+ під час використання під оточенням робочого столу KDE, і використовує залежність gtk-engine-pixbuf, що також доступна з [gtk-engine-pixbuf](https://aur.archlinux.org/packages/gtk-engine-pixbuf/) AUR.

Хоча пекети AUR надає деякі швидкі та дастітні інструкції для закінчення встановлення, завантажте [oxygen-molecule](http://kde-look.org/content/show.php?content=103741) з KDE-look для додаткової документації та різновидів.

## QtCurve

Доступно для _qt4_ (kde4), _qt3_ (kde3), і _gtk2_ (gnome) в репозиторії **[extra]**, цей високо-налаштовувальний стиль найбільш відомий округлювач (?)all-rounder). Він має багато управлінь для разних варіантів, починаючи з появи кнопки на формі слайдера. Ви можете встановити його використовуючи pacman.

```
# pacman -S qtcurve-gtk2 qtcurve-kde3 qtcurve-kde4

```

## Інше

Подібні набори стилів є ті, які схожі один на другого - написані і приготовані для Qt і GTK+ - але не обов’язково від одного і того ж розробника. Ви мабуть маєте зробити деякі мінімальні налагодження, щоб зробити їх вигляд однаковим. нижче список:

*   klearlooks (qt3); clearlooks (gtk2)

# Двигун Тем

Двигун тем може бути розглянуто як тонкий шар API, який переводить теми (виключаючи значки) між одним або декількома інструментаріями. Ці двигуни додати додатковий код в процесі, і можна стверджувати, що такого роду рішення не так елегантно і оптимальної як за допомогою власних стилів.

## Двигуни GTK-QT

Двигуни GTK-QT для використання застосунків GTK+ що працюють в KDE, що просто означає, що це для KDE. Вони додають всі налаштунки Qt (стилі, шрифти, але не значки) в застосунки GTK+ і використовують плагіни стилів напряму. Зверніть увагу, що існують пролеми рендерингу з деякими стилями Qt.

```
# pacman -S gtk-qt-engine

```

Ви можете отримати доступ до них тут:

	_Центр управління (kcontrol) --> Зовнішній вигляд і Теми --> Стилі GTK і Шрифти_

Якщо ви хочете видалити його повністю, і всі його файли, видаліть наступне:

*   ~/.gtkrc2.0-kde
*   ~/.kde/env/gtk-qt-engine.rc.sh
*   ~/gtk-qt-engine.rc

### Заставити працювати з OpenOffice

Встановіть (як root):

```
export SAL_GTK_USE_PIXMAPPAINT=1

```

в /etc/profile. В KDE4 в системному настроюванні, переконайтесь що "використовувати мій стиль KDE в застосунках GTK" вибрано в Зовнішній вигляд > стилі і шрифти GTK.

## QGtkStyle

This is a Qt style which intends to make applications blend perfectly into the GNOME desktop environment by using GTK to render all components. To use this style you must have at least GTK+ 2.0 and Qt 4.3, although Qt 4.4 or higher is preferred.

**Note:** Beginning with version 4.5 this style is included in Qt. You do not have to install this package yourself.

### Having trouble making your Qt applications use QGtkStyle?

Qt won't apply QGtkStyle correctly if GTK is using the [GTK-QT-Engine](/index.php/Uniform_Look_for_QT_and_GTK_Applications#GTK-QT-Engine "Uniform Look for QT and GTK Applications"). Qt determines whether the [GTK-QT-Engine](/index.php/Uniform_Look_for_QT_and_GTK_Applications#GTK-QT-Engine "Uniform Look for QT and GTK Applications") is in use by reading the GTK configuration files listed in the environmental variable **GTK2_RC_FILES**. If the environmental variable is not set properly, Qt assumes you are using the [GTK-QT-Engine](/index.php/Uniform_Look_for_QT_and_GTK_Applications#GTK-QT-Engine "Uniform Look for QT and GTK Applications"), sets QGtkStyle to use the style GTK style _Clearlooks_, and outputs an error message:

```
QGtkStyle cannot be used together with the GTK_Qt engine.

```

Users of [Openbox](/index.php/Openbox "Openbox") and other non-GNOME environments may encounter this probem. Here is a solution:

*   Tell Qt where to look for your GTK configuration file by adding the following to your `.xinitrc` file:
    *   To add multiple paths, separate them with colons.
    *   The $HOME part will expand to be path to your user's home directory. Using the ~ shortcut won't work.

 `.xinitrc` 

```
...
export GTK2_RC_FILES="$HOME/.gtkrc-2.0"
...
```

*   In `.gtkrc-2.0` you must specify a GTK theme. For example:
    *   This is usually done for you by an [application which sets GTK2 Styles](/index.php/Uniform_Look_for_QT_and_GTK_Applications#GTK2_styles "Uniform Look for QT and GTK Applications")

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

To choose your GTK theme for QT apps you must run:

```
qtconfig

```

# Other Tricks

## KDE file dialogs for GTK2 apps

KGtk is a wrapper script that LD_PRELOAD to force KDE file dialogs (open, save, etc) in GTK2 apps. If you use KDE and prefer its file dialogs over GTK's then you can install kgtk from AUR. Once installed you can run GTK2 applications with kgtk-wrapper in 2 ways (using gimp in the examples).

Calling kgtk-wrapper directly and using the GTK2 binary as an arguement

```
/usr/local/bin/kgtk-wrapper gimp

```

OR

Creating a symbolic link to kgtk using the name of the GTK2 binary. Then you can run /usr/local/bin/gimp when you want to run gimp with KDE dialogs.

```
ln -s /usr/local/bin/kgtk-wrapper /usr/local/bin/gimp
/usr/local/bin/gimp

```

## Using custom GTK style

You can use custom styles for specific GTK2 applications. For this, use GTK2_RC_FILES=/path/to/theme/gtk-2.0/gtkrc appname

For example:

```
GTK2_RC_FILES=/usr/share/themes/QtCurve/qtk-2.0/gtkrc firefox

```

It will launch firefox with QtCurve theme.

# Troubleshooting

## How do I set styles for each toolkit?

You can use the following methods to change the theme used in each environment.

#### KDE3 and QT3 styles

*   Control Center (kcontrol) --> Appearance & Themes --> Style --> Widget Style
*   kde-config --style [name of style]
*   /opt/qt/bin/qtconfig

#### QT4 styles

*   /usr/bin/qtconfig

#### GTK2 styles

*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)
*   [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)
*   [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)
*   [gtk2_prefs](https://www.archlinux.org/packages/?name=gtk2_prefs)
*   [Manual configuration](/index.php/GTK%2B#GTK.2B_2.x "GTK+")

#### GTK1 styles

*   switch (gtk-theme-switch package)

## Themes not working in GTK apps

If the style or theme engine you setup isn't showing in your GTK apps then it's likely your GTK settings files aren't being loaded for some reason. You can check where your system expects to find these files by doing the following..

```
$ export | grep gtk

```

Usually the expected files should be ~/.gtkrc for GTK1, ~/.gtkrc2.0 or ~/.gtkrc2.0-kde for GTK2

Newer versions of gtk-qt-engine use ~/.gtkrc2.0-kde and set the export variable in ~/.kde/env/gtk-qt-engine.rc.sh If you recently removed gtk-qt-engine and are trying to set a GTK theme then you must remove ~/.kde/env/gtk-qt-engine.rc.sh and reboot. Doing this will ensure that GTK looks for it's settings in the standard ~/.gtkrc2.0 instead of ~/.gtkrc2.0-kde