This is the main article on [internationalization](https://en.wikipedia.org/wiki/Internationalization_and_localization "wikipedia:Internationalization and localization") (often also referred to as i18n). It is meant to offer guidance, as well as crosslink other relevant articles, to customize settings of an Arch Linux installation to work with any supported language.

The article makes use of subpages for instructions specific for languages:

*   [/Indic](/index.php/Internationalization/Indic "Internationalization/Indic")
*   [/Japanese](/index.php/Internationalization/Japanese "Internationalization/Japanese")
*   [/Korean](/index.php/Internationalization/Korean "Internationalization/Korean")
*   [/Sinhalese](/index.php/Internationalization/Sinhalese "Internationalization/Sinhalese")

## Contents

*   [1 Fonts](#Fonts)
*   [2 Locale](#Locale)
*   [3 Keyboard layouts](#Keyboard_layouts)
*   [4 Input method frameworks](#Input_method_frameworks)
    *   [4.1 Input method engines](#Input_method_engines)
    *   [4.2 GTK IM-module](#GTK_IM-module)
        *   [4.2.1 Disabling GTK IM modules (without uninstalling)](#Disabling_GTK_IM_modules_.28without_uninstalling.29)
    *   [4.3 QT immodule (> QT 4.0.0)](#QT_immodule_.28.3E_QT_4.0.0.29)
        *   [4.3.1 Disabling QT IM modules (without uninstalling)](#Disabling_QT_IM_modules_.28without_uninstalling.29)
*   [5 See also](#See_also)

## Fonts

For the list of available font packages in Arch Linux see the [Fonts](/index.php/Fonts "Fonts") article.

## Locale

See [Locale](/index.php/Locale "Locale").

## Keyboard layouts

See [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Input method frameworks

[Input method](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") (IM) frameworks act as front-ends to various input methods and libraries, allowing the user to switch between different languages with ease.

*   [Fcitx](/index.php/Fcitx "Fcitx")
*   [gcin](/index.php/Gcin "Gcin")
*   **Hime** — A GTK2+/GTK3+ based universal input method platform.

	[http://hime-ime.github.io/](http://hime-ime.github.io/) || [hime-git](https://aur.archlinux.org/packages/hime-git/)

*   [IBus](/index.php/IBus "IBus") – Input Bus for Linux.
*   [SCIM](/index.php/SCIM "SCIM") with the x11 FrontEnd module
*   [uim](/index.php/Uim "Uim")

Unmaintained:

*   [Dasom](/index.php/Dasom "Dasom")
*   [Nimf](/index.php/Nimf "Nimf")

See also [Wikipedia:List of input methods for Unix platforms](https://en.wikipedia.org/wiki/List_of_input_methods_for_Unix_platforms "wikipedia:List of input methods for Unix platforms").

### Input method engines

| Language | Back-end | [Fcitx](/index.php/Fcitx "Fcitx") | [IBus](/index.php/IBus "IBus") | [SCIM](/index.php/SCIM "SCIM") | [uim](/index.php/Uim "Uim") | [gcin](/index.php/Gcin "Gcin") | Hime |
| Chinese | [libchewing](https://www.archlinux.org/packages/?name=libchewing) | [fcitx-chewing](https://www.archlinux.org/packages/?name=fcitx-chewing) | [ibus-chewing](https://www.archlinux.org/packages/?name=ibus-chewing) | [scim-chewing](https://www.archlinux.org/packages/?name=scim-chewing) | - | optdepends | optdepends |
| [libgooglepinyin](https://www.archlinux.org/packages/?name=libgooglepinyin) | [fcitx-googlepinyin](https://www.archlinux.org/packages/?name=fcitx-googlepinyin) | [ibus-googlepinyin](https://www.archlinux.org/packages/?name=ibus-googlepinyin) | - | - | - | - |
| [libpinyin](https://www.archlinux.org/packages/?name=libpinyin) | [fcitx-libpinyin](https://www.archlinux.org/packages/?name=fcitx-libpinyin) | [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) | - | - | - | - |
| [sunpinyin](https://www.archlinux.org/packages/?name=sunpinyin) | [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin) | [ibus-sunpinyin](https://www.archlinux.org/packages/?name=ibus-sunpinyin) | - | - | - | - |
| [Rime](/index.php/Rime "Rime") | [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime) | [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime) | - | - | - | - |
| Japanese | [anthy](https://www.archlinux.org/packages/?name=anthy) | [fcitx-anthy](https://www.archlinux.org/packages/?name=fcitx-anthy) | [ibus-anthy](https://www.archlinux.org/packages/?name=ibus-anthy) | [scim-anthy](https://www.archlinux.org/packages/?name=scim-anthy) | optdepends | optdepends | optdepends |
| [libkkc](https://www.archlinux.org/packages/?name=libkkc) | [fcitx-kkc](https://www.archlinux.org/packages/?name=fcitx-kkc) | [ibus-kkc](https://www.archlinux.org/packages/?name=ibus-kkc) | - | - | - | - |
| [Mozc](/index.php/Mozc "Mozc") | [fcitx-mozc](https://www.archlinux.org/packages/?name=fcitx-mozc) | [ibus-mozc](https://aur.archlinux.org/packages/ibus-mozc/) | - | [uim-mozc](https://aur.archlinux.org/packages/uim-mozc/) | - | - |
| [skk-jisyo](https://www.archlinux.org/packages/?name=skk-jisyo) | [fcitx-skk](https://www.archlinux.org/packages/?name=fcitx-skk) | [ibus-skk](https://www.archlinux.org/packages/?name=ibus-skk) | - | built-in | - | - |
| Korean | [libhangul](https://www.archlinux.org/packages/?name=libhangul) | [fcitx-hangul](https://www.archlinux.org/packages/?name=fcitx-hangul) | [ibus-hangul](https://www.archlinux.org/packages/?name=ibus-hangul) | [scim-hangul](https://www.archlinux.org/packages/?name=scim-hangul) | - | - | - |

### GTK IM-module

*   [scim](/index.php/Scim "Scim") with the socket FrontEnd module binds to the GTK Im-Module
*   [uim](/index.php/Input_Japanese_using_uim "Input Japanese using uim") (Japanese)
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Disabling GTK IM modules (without uninstalling)

First some background information on how GTK loads and selects IM modules:

*   Specifying an IM module

1.  GTK_IM_MODULE environment variable
    1.  GTK_IM_MODULE="scim" gedit
2.  XSETTINGS value of Gtk/IMModule

*   File listing possible IM modules

1.  GTK_IM_MODULE_FILE environment variable
2.  RC files
3.  /etc/gtk-2.0/gtk.immodules

If no IM module is specified (either via GTK_IM_MODULE or in XSETTINGS), then GTK will automatically choose a suitable immodule from an internal listing (GTK_IM_MODULE_FILE... etc). This chosen IM module will depend on the software installed, and will be picked in a completely arbirtrary order.

For a listing of installed GTK+ immodules, see

*   "/usr/lib/gtk-2.0/modules/"
*   "/usr/lib/gtk-2.0/2.10.0/immodules/"

XSETTINGS provides a common API to configure common desktop settings. Similar database configuration systems such as gnome-config, GConf, liproplist and the kde configuration system already exist, however XSETTINGS unifies these systems. XSETTINGS daemons, such as gnome-settings-daemon from gnome, xfce-mcs-manager from xfce4, and other from openbox, etc, push desktop-environment-specific data to the XSETTINGS database. Technically, XSETTINGS is a simple storage medium intended to store only strings, integers and colors. When an XSETTINGS manager quits, the clients restore all settings to their default values.

The if GTK+ has debugging enabled, the loaded modules can be seen by

```
application --gtk-debug modules

```

Otherwise, the modules can be seen by scanning the linked libraries in gdb after attaching to the process.

To prevent GTK+ from loading any IM modules

*   set GTK_IM_MODULE to the empty string
*   set GTK_IM_MODULE to "gtk-im-context-simple"

### QT immodule (> QT 4.0.0)

*   [scim](/index.php/Scim "Scim") with the socket FrontEnd module binds to the QT Im-Module
*   [uim](/index.php/Input_Japanese_using_uim "Input Japanese using uim") (Japanese)
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Disabling QT IM modules (without uninstalling)

QT will load the IM module specified in QT_IM_MODULE, and if unset attempt to fall back on XIM.

1.  QT_IM_MODULE environment variable
2.  XIM

To disable input method module loading in QT, export QT_IM_MODULE="simple".

## See also

*   [Gentoo wiki](https://wiki.gentoo.org/wiki/Localization "gentoo:Localization")
*   [Fedora wiki](https://fedoraproject.org/wiki/I18N/InputMethods)
*   [Free Standards Group OpenI18N](http://www.openi18n.org/)
*   [XSETTINGS 0.5 Specification](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html)
*   [Running and Debugging GTK+ Applications](http://library.gnome.org/devel/gtk/unstable/gtk-running.html)