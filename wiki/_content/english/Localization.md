This is the main article on [localization](https://en.wikipedia.org/wiki/Internationalization_and_localization "wikipedia:Internationalization and localization") (often also referred to as l10n). It is meant to offer guidance, as well as cross-link other relevant articles, to customize settings of an Arch Linux installation to work with any supported language.

The article makes use of subpages for instructions specific for languages:

*   [/Chinese](/index.php/Localization/Chinese "Localization/Chinese")
*   [/Indic](/index.php/Localization/Indic "Localization/Indic")
    *   [/Sinhalese](/index.php/Localization/Sinhalese "Localization/Sinhalese")
*   [/Japanese](/index.php/Localization/Japanese "Localization/Japanese")
*   [/Korean](/index.php/Localization/Korean "Localization/Korean")

Subpages without an English counterpart:

*   [ru:Localization/Russian](https://wiki.archlinux.org/index.php/Localization/Russian_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:Localization/Russian")
*   [sk:Localization/Slovak](https://wiki.archlinux.org/index.php/Localization/Slovak_(Slovensk%C3%BD) "sk:Localization/Slovak")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Fonts](#Fonts)
*   [2 Locale](#Locale)
*   [3 Keyboard layouts](#Keyboard_layouts)
*   [4 Input methods](#Input_methods)
    *   [4.1 Input method engines](#Input_method_engines)
    *   [4.2 GTK IM-module](#GTK_IM-module)
        *   [4.2.1 Disabling GTK IM modules (without uninstalling)](#Disabling_GTK_IM_modules_(without_uninstalling))
    *   [4.3 QT immodule (> QT 4.0.0)](#QT_immodule_(>_QT_4.0.0))
        *   [4.3.1 Disabling QT IM modules (without uninstalling)](#Disabling_QT_IM_modules_(without_uninstalling))
*   [5 See also](#See_also)

## Fonts

For the list of available font packages in Arch Linux see the [Fonts](/index.php/Fonts "Fonts") article.

## Locale

See [Locale](/index.php/Locale "Locale").

## Keyboard layouts

See [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Input methods

From [Fedora:I18N/InputMethods](https://fedoraproject.org/wiki/I18N/InputMethods "fedora:I18N/InputMethods"):

	An [input method](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") (IM) is a way to input a certain set of characters and symbols, usually because a keyboard does not directly support them.

Most input methods are part of an **IM framework**, which lets the user easily switch between multiple input methods. These input methods are either included with the framework or packaged separately. Programs implementing input methods are called **IM engines**. The input methods available for a language are listed in the respective language subpage.

The available IM frameworks are:

*   **[Fcitx](/index.php/Fcitx "Fcitx")** — Input method framework with extension support.

	[https://fcitx-im.org/](https://fcitx-im.org/) || [fcitx](https://www.archlinux.org/packages/?name=fcitx)

*   **[gcin](/index.php/Gcin "Gcin")** — Input method server supporting various input methods.

	[http://hyperrate.com/dir.php?eid=67](http://hyperrate.com/dir.php?eid=67) || [gcin](https://www.archlinux.org/packages/?name=gcin)

*   **Hime** — Universal input method platform.

	[https://hime-ime.github.io/](https://hime-ime.github.io/) || [hime-git](https://aur.archlinux.org/packages/hime-git/)

*   **[IBus](/index.php/IBus "IBus")** — Intelligent Input Bus, a next generation input framework.

	[https://github.com/ibus/ibus/wiki](https://github.com/ibus/ibus/wiki) || [ibus](https://www.archlinux.org/packages/?name=ibus)

*   **[Nimf](/index.php/Nimf "Nimf")** — A multilingual input method framework which inherits [Dasom](/index.php/Dasom "Dasom").

	[https://gitlab.com/nimf-i18n/nimf](https://gitlab.com/nimf-i18n/nimf) || [nimf](https://aur.archlinux.org/packages/nimf/)

*   **[SCIM](/index.php/SCIM "SCIM")** — The Smart Common Input Method platform.

	[https://github.com/scim-im/scim](https://github.com/scim-im/scim) || [scim](https://www.archlinux.org/packages/?name=scim)

*   **[uim](/index.php/Uim "Uim")** — Multilingual input method framework to provide simple, easily extensible and high code-quality input method development platform, and useful input method environment for users of desktop and embedded platforms.

	[https://github.com/uim/uim](https://github.com/uim/uim) || [uim](https://www.archlinux.org/packages/?name=uim)

Unmaintained:

*   **[Dasom](/index.php/Dasom "Dasom")** — Multilingual input method framework.

	[https://dasom-im.github.io/](https://dasom-im.github.io/) || [dasom-git](https://aur.archlinux.org/packages/dasom-git/)

See also [Wikipedia:List of input methods for Unix platforms](https://en.wikipedia.org/wiki/List_of_input_methods_for_Unix_platforms "wikipedia:List of input methods for Unix platforms").

### Input method engines

| Language | Back-end | [Fcitx](/index.php/Fcitx "Fcitx") | [IBus](/index.php/IBus "IBus") | [SCIM](/index.php/SCIM "SCIM") | [uim](/index.php/Uim "Uim") | [gcin](/index.php/Gcin "Gcin") | Hime |
| Vietnamese | [UniKey](http://www.unikey.org/linux.php) | [fcitx-unikey](https://www.archlinux.org/packages/?name=fcitx-unikey) | [ibus-unikey](https://www.archlinux.org/packages/?name=ibus-unikey) | [scim-unikey](https://github.com/scim-im/scim-unikey) | - | - | - |
| Others | [m17n-lib](https://www.archlinux.org/packages/?name=m17n-lib) | [fcitx-m17n](https://www.archlinux.org/packages/?name=fcitx-m17n) | [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) | [scim-m17n](https://aur.archlinux.org/packages/scim-m17n/) | depends | ? | ? |

### GTK IM-module

*   [SCIM](/index.php/SCIM "SCIM") with the socket FrontEnd module binds to the GTK Im-Module
*   [uim](/index.php/Uim "Uim")
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Disabling GTK IM modules (without uninstalling)

First some background information on how GTK loads and selects IM modules:

*   Specifying an IM module

1.  `GTK_IM_MODULE` environment variable
    1.  GTK_IM_MODULE="scim" gedit
2.  `XSETTINGS` value of Gtk/IMModule

*   File listing possible IM modules

1.  `GTK_IM_MODULE_FILE` environment variable
2.  RC files
3.  `/etc/gtk-2.0/gtk.immodules`

If no IM module is specified (either via GTK_IM_MODULE or in XSETTINGS), then GTK will automatically choose a suitable immodule from an internal listing (GTK_IM_MODULE_FILE... etc). This chosen IM module will depend on the software installed, and will be picked in a completely arbitrary order.

For a listing of installed GTK immodules, see

*   `/usr/lib/gtk-2.0/modules/`
*   `/usr/lib/gtk-2.0/2.10.0/immodules/`

XSETTINGS provides a common API to configure common desktop settings. Similar database configuration systems such as gnome-config, GConf, liproplist and the kde configuration system already exist, however XSETTINGS unifies these systems. XSETTINGS daemons, such as gnome-settings-daemon from gnome, xfce-mcs-manager from xfce4, and other from openbox, etc, push desktop-environment-specific data to the XSETTINGS database. Technically, XSETTINGS is a simple storage medium intended to store only strings, integers and colors. When an XSETTINGS manager quits, the clients restore all settings to their default values.

The if GTK has debugging enabled, the loaded modules can be seen by

```
$ *application* --gtk-debug modules

```

Otherwise, the modules can be seen by scanning the linked libraries in gdb after attaching to the process.

To prevent GTK from loading any IM modules

*   set `GTK_IM_MODULE` to the empty string
*   set `GTK_IM_MODULE` to "gtk-im-context-simple"

### QT immodule (> QT 4.0.0)

*   [SCIM](/index.php/SCIM "SCIM") with the socket FrontEnd module binds to the QT IM-Module
*   [uim](/index.php/Uim "Uim")
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Disabling QT IM modules (without uninstalling)

QT will load the IM module specified in `QT_IM_MODULE`, and if unset attempt to fall back on XIM.

1.  `QT_IM_MODULE` environment variable
2.  XIM

To disable input method module loading in QT, [export](/index.php/Export "Export") `QT_IM_MODULE="simple"`.

## See also

*   [Gentoo wiki](https://wiki.gentoo.org/wiki/Localization "gentoo:Localization")
*   [Fedora wiki](https://fedoraproject.org/wiki/I18N/InputMethods "fedora:I18N/InputMethods")
*   [Free Standards Group OpenI18N](http://www.openi18n.org/)
*   [XSETTINGS Specification](https://specifications.freedesktop.org/xsettings-spec/xsettings-latest.html)
*   [Running and Debugging GTK Applications](https://developer.gnome.org/gtk3/unstable/gtk-running.html)