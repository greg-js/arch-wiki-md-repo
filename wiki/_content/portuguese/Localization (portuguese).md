Este é o artigo principal sobre [localização](https://en.wikipedia.org/wiki/pt:Internacionaliza%C3%A7%C3%A3o_(inform%C3%A1tica) (muitas vezes também conhecido como l10n). Destina-se a oferecer orientação, bem como reticulação de outros artigos relevantes, para personalizar as configurações de uma instalação do Arch Linux para trabalhar com qualquer idioma suportado.

O artigo faz uso de subpáginas para instruções específicas para idiomas:

*   [Localization/Chinese](/index.php/Localization/Chinese "Localization/Chinese")
*   [Localization/Indic](/index.php/Localization/Indic "Localization/Indic")
    *   [Localization/Sinhalese](/index.php/Localization/Sinhalese "Localization/Sinhalese")
*   [Localization/Japanese](/index.php/Localization/Japanese "Localization/Japanese")
*   [Localization/Korean](/index.php/Localization/Korean "Localization/Korean")

Subpáginas sem uma contraparte em inglês:

*   [ru:Localization/Russian](https://wiki.archlinux.org/index.php/Localization/Russian_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:Localization/Russian")
*   [sk:Localization/Slovak](https://wiki.archlinux.org/index.php/Localization/Slovak_(Slovensk%C3%BD) "sk:Localization/Slovak")

## Contents

*   [1 Fontes](#Fontes)
*   [2 Locale](#Locale)
*   [3 Layouts de teclado](#Layouts_de_teclado)
*   [4 Métodos de entrada](#M.C3.A9todos_de_entrada)
    *   [4.1 Mecanismos de método de entrada](#Mecanismos_de_m.C3.A9todo_de_entrada)
    *   [4.2 Método de GTK IM](#M.C3.A9todo_de_GTK_IM)
        *   [4.2.1 Desabilitando módulos de GTK IM (sem desinstalar)](#Desabilitando_m.C3.B3dulos_de_GTK_IM_.28sem_desinstalar.29)
    *   [4.3 QT immodule (> QT 4.0.0)](#QT_immodule_.28.3E_QT_4.0.0.29)
        *   [4.3.1 Desabilitando módulos QT IM (sem desinstalar)](#Desabilitando_m.C3.B3dulos_QT_IM_.28sem_desinstalar.29)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Fontes

For the list of available font packages in Arch Linux see the [Fonts](/index.php/Fonts "Fonts") article.

## Locale

See [Locale](/index.php/Locale "Locale").

## Layouts de teclado

See [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Métodos de entrada

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

	[https://gitlab.com/hodong/nimf](https://gitlab.com/hodong/nimf) || [nimf-git](https://aur.archlinux.org/packages/nimf-git/)

*   **[SCIM](/index.php/SCIM "SCIM")** — The Smart Common Input Method platform.

	[https://github.com/scim-im/scim](https://github.com/scim-im/scim) || [scim](https://www.archlinux.org/packages/?name=scim)

*   **[uim](/index.php/Uim "Uim")** — Multilingual input method framework to provide simple, easily extensible and high code-quality input method development platform, and useful input method environment for users of desktop and embedded platforms.

	[https://github.com/uim/uim](https://github.com/uim/uim) || [uim](https://www.archlinux.org/packages/?name=uim)

Unmaintained:

*   **[Dasom](/index.php/Dasom "Dasom")** — Multilingual input method framework.

	[https://dasom-im.github.io/](https://dasom-im.github.io/) || [dasom-git](https://aur.archlinux.org/packages/dasom-git/)

See also [Wikipedia:List of input methods for Unix platforms](https://en.wikipedia.org/wiki/List_of_input_methods_for_Unix_platforms "wikipedia:List of input methods for Unix platforms").

### Mecanismos de método de entrada

| Language | Back-end | [Fcitx](/index.php/Fcitx "Fcitx") | [IBus](/index.php/IBus "IBus") | [SCIM](/index.php/SCIM "SCIM") | [uim](/index.php/Uim "Uim") | [gcin](/index.php/Gcin "Gcin") | Hime |
| Vietnamese | [UniKey](http://www.unikey.org/linux.php) | [fcitx-unikey](https://www.archlinux.org/packages/?name=fcitx-unikey) | [ibus-unikey](https://www.archlinux.org/packages/?name=ibus-unikey) | [scim-unikey](https://github.com/scim-im/scim-unikey) | - | - | - |
| Others | [m17n-lib](https://www.archlinux.org/packages/?name=m17n-lib) | [fcitx-m17n](https://www.archlinux.org/packages/?name=fcitx-m17n) | [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) | [scim-m17n](https://www.archlinux.org/packages/?name=scim-m17n) | depends |  ? |  ? |

### Método de GTK IM

*   [SCIM](/index.php/SCIM "SCIM") with the socket FrontEnd module binds to the GTK Im-Module
*   [uim](/index.php/Uim "Uim")
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Desabilitando módulos de GTK IM (sem desinstalar)

First some background information on how GTK loads and selects IM modules:

*   Specifying an IM module

1.  `GTK_IM_MODULE` environment variable
    1.  GTK_IM_MODULE="scim" gedit
2.  `XSETTINGS` value of Gtk/IMModule

*   File listing possible IM modules

1.  `GTK_IM_MODULE_FILE` environment variable
2.  RC files
3.  `/etc/gtk-2.0/gtk.immodules`

If no IM module is specified (either via GTK_IM_MODULE or in XSETTINGS), then GTK will automatically choose a suitable immodule from an internal listing (GTK_IM_MODULE_FILE... etc). This chosen IM module will depend on the software installed, and will be picked in a completely arbirtrary order.

For a listing of installed GTK+ immodules, see

*   `/usr/lib/gtk-2.0/modules/`
*   `/usr/lib/gtk-2.0/2.10.0/immodules/`

XSETTINGS provides a common API to configure common desktop settings. Similar database configuration systems such as gnome-config, GConf, liproplist and the kde configuration system already exist, however XSETTINGS unifies these systems. XSETTINGS daemons, such as gnome-settings-daemon from gnome, xfce-mcs-manager from xfce4, and other from openbox, etc, push desktop-environment-specific data to the XSETTINGS database. Technically, XSETTINGS is a simple storage medium intended to store only strings, integers and colors. When an XSETTINGS manager quits, the clients restore all settings to their default values.

The if GTK+ has debugging enabled, the loaded modules can be seen by

```
$ *application* --gtk-debug modules

```

Otherwise, the modules can be seen by scanning the linked libraries in gdb after attaching to the process.

To prevent GTK+ from loading any IM modules

*   set `GTK_IM_MODULE` to the empty string
*   set `GTK_IM_MODULE` to "gtk-im-context-simple"

### QT immodule (> QT 4.0.0)

*   [SCIM](/index.php/SCIM "SCIM") with the socket FrontEnd module binds to the QT IM-Module
*   [uim](/index.php/Uim "Uim")
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Desabilitando módulos QT IM (sem desinstalar)

QT will load the IM module specified in `QT_IM_MODULE`, and if unset attempt to fall back on XIM.

1.  `QT_IM_MODULE` environment variable
2.  XIM

To disable input method module loading in QT, [export](/index.php/Export "Export") `QT_IM_MODULE="simple"`.

## Veja também

*   [Gentoo wiki](https://wiki.gentoo.org/wiki/Localization "gentoo:Localization")
*   [Fedora wiki](https://fedoraproject.org/wiki/I18N/InputMethods "fedora:I18N/InputMethods")
*   [Free Standards Group OpenI18N](http://www.openi18n.org/)
*   [XSETTINGS 0.5 Specification](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html)
*   [Running and Debugging GTK+ Applications](http://library.gnome.org/devel/gtk/unstable/gtk-running.html)