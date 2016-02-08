# LibreOffice

From [Home - LibreOffice](http://www.libreoffice.org/):

	_LibreOffice is the free power-packed Open Source personal productivity suite for Windows, Macintosh and Linux, that gives you six feature-rich applications for all your document production and data processing needs: Writer, Calc, Impress, Draw, Math and Base. [Support](http://www.libreoffice.org/get-help/) and [documentation](http://www.libreoffice.org/get-help/documentation/) is free from our large, dedicated community of users, contributors and developers. [You, too, can also get involved!](http://www.libreoffice.org/get-involved/)_

## Contents

*   [1 LibreOffice in Arch Linux](#LibreOffice_in_Arch_Linux)
*   [2 Installation](#Installation)
*   [3 Theme](#Theme)
    *   [3.1 Firefox themes](#Firefox_themes)
    *   [3.2 Disable startup logo](#Disable_startup_logo)
*   [4 Extension management](#Extension_management)
*   [5 Language aids](#Language_aids)
    *   [5.1 Spell checking](#Spell_checking)
    *   [5.2 Hyphenation rules](#Hyphenation_rules)
    *   [5.3 Thesaurus](#Thesaurus)
    *   [5.4 Grammar checking](#Grammar_checking)
    *   [5.5 Offline help for en-US](#Offline_help_for_en-US)
*   [6 Installing macros](#Installing_macros)
*   [7 Speed up LibreOffice](#Speed_up_LibreOffice)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Font substitution](#Font_substitution)
    *   [8.2 Anti-aliasing](#Anti-aliasing)
    *   [8.3 Hanging when using NFSv3 shares](#Hanging_when_using_NFSv3_shares)
    *   [8.4 LibreOffice does not detect my certificates](#LibreOffice_does_not_detect_my_certificates)
    *   [8.5 Run .pps files in edit mode (without slideshow)](#Run_.pps_files_in_edit_mode_.28without_slideshow.29)
    *   [8.6 Application Error (not starting)](#Application_Error_.28not_starting.29)
    *   [8.7 Exit while pushing the save button](#Exit_while_pushing_the_save_button)
    *   [8.8 Media support](#Media_support)
    *   [8.9 Default paper size in Writer and Draw](#Default_paper_size_in_Writer_and_Draw)

## LibreOffice in Arch Linux

Official support for [OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org") was dropped in favor of LibreOffice, the "Document Foundation" fork of the project, which also includes enhancements and additional features. See [Dropping Oracle OpenOffice (arch-general)](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html).

## Installation

[Install](/index.php/Install "Install") one of the following packages from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) is the feature branch, with new program enhancements.
*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) is the maintenance branch.

**Note:**

*   In the past, the installation of at least 1 language pack was required. Currently, LibreOffice detects your system defaults; manual installation of a language pack is no longer mandatory. See [help.libreoffice.org](https://help.libreoffice.org/Scalc/cui/ui/optlanguagespage/ignorelanguagechange#User_interface) for additional information.
*   If you want the UK-English language pack, install [libreoffice-fresh-en-GB](https://www.archlinux.org/packages/?name=libreoffice-fresh-en-GB), not [libreoffice-fresh-uk](https://www.archlinux.org/packages/?name=libreoffice-fresh-uk) (Ukrainian) or [libreoffice-fresh-br](https://www.archlinux.org/packages/?name=libreoffice-fresh-br) (Breton)!
*   For SDK install [libreoffice-fresh-sdk](https://www.archlinux.org/packages/?name=libreoffice-fresh-sdk).
*   For Qt and GTK+ visual integration, see [#Theme](#Theme).

Check the optional dependencies pacman displays. If you want to use LibreOffice Base, you must install a Java Runtime Environment: see [Java](/index.php/Java "Java"). You may need [hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/) to use [some modules](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) in LibreOffice Base.

## Theme

LibreOffice includes support for [GTK+](/index.php/GTK%2B "GTK+") and [Qt](/index.php/Qt "Qt") theme integration. See also [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

As of LibreOffice v3.5.x toolkit libraries are checked in the following order:

```
gtk > kde4 > generic

```

To force the use of a certain VCL UI interface, use one of the `SAL_USE_VCLPLUGIN=gen`, `SAL_USE_VCLPLUGIN=kde4`, `SAL_USE_VCLPLUGIN=gtk` or `SAL_USE_VCLPLUGIN=gtk3` [environment variables](/index.php/Environment_variables "Environment variables"). These variables can be uncommented in `/etc/profile.d/libreoffice-fresh.sh` or `/etc/profile.d/libreoffice-still.sh`.

**Note:** The new GTK3 UI is experimental and will only be available if you enable "experimental features" in LibreOffice main configuration dialog.

However, if it looks like it is using Windows 95/98 icons, go to _Tools > Options..._ in the menus (which presents the Options Dialog), then select _LibreOffice > Accessibility_ and uncheck "Automatically detect high-contrast mode of operating system".

If that does not work immediately, you may need to change the icon set that is in use; this is also in the Options Dialog, under _LibreOffice > View_ with two pop-up boxes for "Icon size and style" (the latter pop-up box should be changed to something other than "High-contrast").

### Firefox themes

LibreOffice 4.x series is able to use Firefox themes. Enter LibreOffice options and choose _Personalization > Select Theme_, then paste the URL of your favourite one. A convenient button in the dialog box lets you open the browser.

Themes can be found on [Mozilla's theme repository](https://addons.mozilla.org/en-US/firefox/themes/).

### Disable startup logo

If you prefer to disable the startup logo, open `/etc/libreoffice/sofficerc`, find the `Logo=` line and set `Logo=0`.

**Note:** This variable is unrelated with the Logo scripting support.

## Extension management

The following additional extensions are available in the [official repositories](/index.php/Official_repositories "Official repositories"):

*   [libreoffice-extension-texmaths](https://www.archlinux.org/packages/?name=libreoffice-extension-texmaths)
*   [libreoffice-extension-writer2latex](https://www.archlinux.org/packages/?name=libreoffice-extension-writer2latex)

For more extensions, check the [AUR](/index.php/AUR "AUR"), the built-in LibreOffice Extension manager, or [libreplanet](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List).

## Language aids

### Spell checking

For spell checking, please make sure [hunspell](https://www.archlinux.org/packages/?name=hunspell) is properly installed; this should be the case for both still and fresh LibreOffice versions. Then install a language dictionary for hunspell like [hunspell-en](https://www.archlinux.org/packages/?name=hunspell-en) for English, [hunspell-de](https://www.archlinux.org/packages/?name=hunspell-de) for German, etc. Then enable the Writing aids by selecting the check-box in _Tools -> Options -> Language Settings -> Writing Aids -> Hunspell SpellChecker_.

	Finnish

Unlike other languages, Finnish dictionaries use different naming. These four packages should be installed (in this order): [malaga](https://aur.archlinux.org/packages/malaga/), [suomi-malaga-voikko](https://aur.archlinux.org/packages/suomi-malaga-voikko/), [hfstospell](https://aur.archlinux.org/packages/hfstospell/), [libvoikko](https://www.archlinux.org/packages/?name=libvoikko) and [voikko-libreoffice](https://aur.archlinux.org/packages/voikko-libreoffice/).

### Hyphenation rules

For hyphenation rules, you will need [hyphen](https://www.archlinux.org/packages/?name=hyphen) and a language hyphen rule set ([hyphen-en](https://www.archlinux.org/packages/?name=hyphen-en) for English, [hyphen-de](https://www.archlinux.org/packages/?name=hyphen-de) for German, etc).

### Thesaurus

For the thesaurus option, you will need [libmythes](https://www.archlinux.org/packages/?name=libmythes) and a mythes language thesaurus (like [mythes-en](https://www.archlinux.org/packages/?name=mythes-en) for English, [mythes-de](https://www.archlinux.org/packages/?name=mythes-de) for German, etc).

### Grammar checking

For grammar checking, several tools are available. The most common is [LanguageTool](https://www.languagetool.org/). While the [languagetool](https://www.archlinux.org/packages/?name=languagetool) is available in the [official repositories](/index.php/Official_repositories "Official repositories"), the later is not packaged as a LibreOffice extension. It is thus recommended to install it with via the [AUR](/index.php/AUR "AUR") package [libreoffice-extension-languagetool](https://aur.archlinux.org/packages/libreoffice-extension-languagetool/) instead. Even if this AUR package comes bundled with LanguageTool, this does not conflict with the one in the official repositories. In the future, it could even be possible to make that AUR package depend on the official [languagetool](https://www.archlinux.org/packages/?name=languagetool) package.

After this package has been installed, please make sure you have a [Java](/index.php/Java "Java") runtime installed. Indeed, Languagetool uses Java and may slow down or briefly hang LibreOffice, particularly while opening documents. Fortunately this is usually only when initially opening a document and is usually not apparent otherwise.

Other grammar tools can also be found on the [LibrePlanet extension page](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List), on the [official LibreOffice Extensions website](http://extensions.libreoffice.org/) or [OpenOffice's Website](http://lingucomponent.openoffice.org/grammar.html). Please note all OpenOffice extensions are guaranteed to work with LibreOffice.

	French

French-speaking users are advantaged here: they do not need to install LanguageTool nor Java. Dicollecte provides a nice Python extension, specifically designed for Frenchs. You can install it [from the website](http://www.dicollecte.org/grammalecte/telecharger.php) or via this [AUR](/index.php/AUR "AUR") package: [libreoffice-extension-grammalecte-fr](https://aur.archlinux.org/packages/libreoffice-extension-grammalecte-fr/). In any case, this extensions also comes with the French dictionaries otherwise provided by [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr).

### Offline help for en-US

As of version 5.2.2, [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) provides the offline help files for en-US. Help files for different locales is provided by the appropriate libreoffice language package, (i.e., [libreoffice-fresh-en-ZA](https://www.archlinux.org/packages/?name=libreoffice-fresh-en-ZA) provides the help files for en-ZA locales).

## Installing macros

If you intend to use macros, you must have a Java Runtime Environment enabled. A Java Runtime Environment is enabled by default, but disabling it [speeds up the program](#Speed_up_LibreOffice).

The default path for macros in Arch Linux is different from most Linux distributions. Its location is:

```
~/.config/libreoffice/4/user/Scripts/

```

## Speed up LibreOffice

Some settings may improve LibreOffice's loading time and responsiveness. However, some also increase RAM usage, so use them carefully. They can all be accessed under _Tools > Options_.

*   Under _Memory_:
    *   Reduce the number of Undo steps to a figure lower than 100, to something like 20 or 30 steps
    *   Under _Graphics cache_, set Use for LibreOffice to 128 MB (up from the original 20 MB)
    *   Set _Memory per object_ to 20 MB (up from the default 5 MB).
    *   If LibreOffice is used often, check _Enable systray Quickstarter_
*   Under _Advanced_, uncheck _Use a Java runtime environment_

**Note:** For a list of functionality written in Java only, see: [https://wiki.documentfoundation.org/Development/Java](https://wiki.documentfoundation.org/Development/Java).

## Troubleshooting

### Font substitution

These settings can be changed in the LibreOffice options. From the drop-down menu, select _Tools > Options > LibreOffice > Fonts_. Check the box that says _Apply Replacement Table_. Type `Andale Sans UI` in the font box and choose your desired font for the _Replace with_ option. When done, click the _checkmark_. Then choose the _Always_ and _Screen only_ options in the box below. Click OK. You will then need to go to _Tools > Options > LibreOffice > View_, and uncheck "Use system font for user interface". If you use a non-antialised font, such as Arial, you will also need to uncheck "Screen font antialiasing" before menu fonts render correctly.

### Anti-aliasing

Execute:

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

To make the change persistent, add `Xft.lcdfilter: lcddefault` to your `~/.Xresources` file, and make sure to run `$ xrdb -merge ~/.Xresources` ([source](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19). See [X resources](/index.php/X_resources "X resources") for more details.

If this does not work, you can also try adding `Xft.lcdfilter: lcddefault` to your `~/.Xdefaults`. If you do not have this file, you will have to create it.

### Hanging when using NFSv3 shares

If LibreOffice hangs when trying to open or save a document located on a NFSv3 share, try prepending the following lines with a `#` in `/usr/lib/libreoffice/program/soffice`:

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

To avoid overwriting on update you can copy `/usr/lib/libreoffice/program/soffice` in `/usr/local/bin`. Original post [here](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx).

### LibreOffice does not detect my certificates

If you cannot see the certificates when trying to sign a document, you will need to have the certificates configured in Mozilla Firefox (or Thunderbird). If after that LibreOffice still does not show them, set the `MOZILLA_CERTIFICATE_FOLDER` environment variable to point to your Mozilla Firefox (or Thunderbird) folder:

```
export MOZILLA_CERTIFICATE_FOLDER=$HOME/.mozilla/firefox/XXXXXX.default/

```

[Certificate detection](http://wiki.openoffice.org/wiki/Certificate_Detection).

### Run .pps files in edit mode (without slideshow)

The only solution is to rename the `.pps` file to `.ppt`.

Add the following script to your home directory and use it to open every .pps file. Very useful to open `.pps` files received by email without the need to save them.

```
#!/bin/bash

f=$(mktemp)
cp "$1" "${f}.ppt" && libreoffice "${f}.ppt" && rm -f "${f}.ppt"

```

### Application Error (not starting)

When using a different GTK theme than _Adwaita_, LibreOffice may fail to start:

```
(soffice:2148): GLib-GObject-CRITICAL **: g_value_set_boxed: assertion 'G_VALUE_HOLDS_BOXED (value)' failed

(soffice:2148): GLib-GObject-WARNING **: gtype.c:4268: type id '0' is invalid

(soffice:2148): GLib-GObject-WARNING **: can't peek value table for type '<invalid>' which is not currently referenced
Application Error

```

See [FS#46614](https://bugs.archlinux.org/task/46614).

### Exit while pushing the save button

Try either of the following workarounds:

*   Delete the `~/.config/libreoffice` folder. It will erase all the settings linked to LibreOffice and so, LibreOffice will recreate them on the next launch.

*   Go to menu Tools > Options > LibreOffice > General and check `Use LibreOffice dialogs`.

*   The GTK3 integration provided by `libvclplug_gtk3lo.so` has been identified as the cause of this problem. [[1]](https://forums.opensuse.org/showthread.php/510439-LibreOffice-crashes-when-saving) See [#Theme](#Theme) to use a different VCL, such as `gtk`.

### Media support

If embedded videos are just gray boxes, make sure to have installed the [GStreamer plugins](/index.php/GStreamer#Current_version_plugins "GStreamer") required.

### Default paper size in Writer and Draw

If the default paper size in blank Writer and Draw documents is persistently incorrect for your locale, try installing the [libpaper](https://www.archlinux.org/packages/?name=libpaper) optional dependency and either updating `/etc/papersize` (for a system-wide change) or exporting the `PAPERSIZE` environment variable (for a user change) with your preferred paper size.

**Note:** [libpaper](https://www.archlinux.org/packages/?name=libpaper) defaults to **Letter** paper size if nothing else has been set.

Retrieved from "[https://wiki.archlinux.org/index.php?title=LibreOffice&oldid=419494](https://wiki.archlinux.org/index.php?title=LibreOffice&oldid=419494)"