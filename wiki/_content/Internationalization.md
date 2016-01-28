# Internationalization

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This is the main article on the internationalization of an Arch Linux installation. It is meant to offer guidance, as well as crosslink other relevant articles, to customize settings of an Arch Linux installation to work with any supported language.

The article makes use of subpages for instructions specific for languages:

<table class="mw-prefixindex-list-table">

<tbody>

<tr>

<td>[Internationalization/Indic](/index.php/Internationalization/Indic "Internationalization/Indic")</td>

<td>[Internationalization/Japanese](/index.php/Internationalization/Japanese "Internationalization/Japanese")</td>

<td>[Internationalization/Korean](/index.php/Internationalization/Korean "Internationalization/Korean")</td>

</tr>

<tr>

<td>[Internationalization/Korean (한국어)](/index.php/Internationalization/Korean_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Internationalization/Korean (한국어)")</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Fonts](#Fonts)
*   [2 Locale](#Locale)
*   [3 Keyboard layouts](#Keyboard_layouts)
*   [4 Input methods in Xorg](#Input_methods_in_Xorg)
    *   [4.1 GTK immodule](#GTK_immodule)
        *   [4.1.1 Disabling GTK IM modules (without uninstalling)](#Disabling_GTK_IM_modules_.28without_uninstalling.29)
    *   [4.2 QT immodule (> QT 4.0.0)](#QT_immodule_.28.3E_QT_4.0.0.29)
        *   [4.2.1 Disabling QT IM modules (without uninstalling)](#Disabling_QT_IM_modules_.28without_uninstalling.29)
*   [5 See also](#See_also)

## Fonts

For the list of available font packages in Arch Linux see the [Fonts](/index.php/Fonts "Fonts") article.

## Locale

See [Locale](/index.php/Locale "Locale").

## Keyboard layouts

See [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Input methods in Xorg

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** A brief introduction of _input methods_ should be added, similar to [Internationalization/Korean#Input_in_Xorg](/index.php/Internationalization/Korean#Input_in_Xorg "Internationalization/Korean"). (Discuss in [Talk:Internationalization#](https://wiki.archlinux.org/index.php/Talk:Internationalization))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Does the subsection structure still fit and is appropriate for the main article? Can you help with integrating the comments referred to in [ArchWiki:Requests#Input_methods](/index.php/ArchWiki:Requests#Input_methods "ArchWiki:Requests") to improve the article? (Discuss in [Talk:Internationalization#](https://wiki.archlinux.org/index.php/Talk:Internationalization))

*   [gcin](/index.php/Gcin "Gcin")
*   [fcitx](/index.php/Fcitx "Fcitx")
*   [SCIM](/index.php/SCIM "SCIM") with the x11 FrontEnd module
*   [uim](/index.php/Input_Japanese_using_uim "Input Japanese using uim") (Japanese)
*   [IBus](/index.php/IBus "IBus")
*   [Dasom](/index.php/Dasom "Dasom")

### GTK immodule

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

 `application --gtk-debug modules` 

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

*   [Free Standards Group OpenI18N](http://www.openi18n.org/)
*   [XSETTINGS 0.5 Specification](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html)
*   [Running and Debugging GTK+ Applications](http://library.gnome.org/devel/gtk/unstable/gtk-running.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Internationalization&oldid=411217](https://wiki.archlinux.org/index.php?title=Internationalization&oldid=411217)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internationalization](/index.php/Category:Internationalization "Category:Internationalization")

Hidden categories:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")
*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")