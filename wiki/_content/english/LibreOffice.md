Related articles

*   [Apache OpenOffice](/index.php/Apache_OpenOffice "Apache OpenOffice")

From [Home - LibreOffice](https://www.libreoffice.org/):

	LibreOffice is the free power-packed Open Source personal productivity suite for Windows, Macintosh and Linux, that gives you six feature-rich applications for all your document production and data processing needs: Writer, Calc, Impress, Draw, Math and Base.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Theme](#Theme)
    *   [2.1 Disable startup logo](#Disable_startup_logo)
*   [3 Extension management](#Extension_management)
*   [4 Language aids](#Language_aids)
    *   [4.1 Spell checking](#Spell_checking)
    *   [4.2 Hyphenation rules](#Hyphenation_rules)
    *   [4.3 Thesaurus](#Thesaurus)
    *   [4.4 Grammar checking](#Grammar_checking)
    *   [4.5 Offline help for en-US](#Offline_help_for_en-US)
*   [5 Installing macros](#Installing_macros)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Font substitution](#Font_substitution)
    *   [6.2 Anti-aliasing](#Anti-aliasing)
    *   [6.3 Hanging when using NFSv3 shares](#Hanging_when_using_NFSv3_shares)
    *   [6.4 LibreOffice does not detect my certificates](#LibreOffice_does_not_detect_my_certificates)
    *   [6.5 Run .pps files in edit mode (without slideshow)](#Run_.pps_files_in_edit_mode_(without_slideshow))
    *   [6.6 Media support](#Media_support)
    *   [6.7 Default paper size in Writer and Draw](#Default_paper_size_in_Writer_and_Draw)
    *   [6.8 LibreOffice toolbars unreadable with dark themes](#LibreOffice_toolbars_unreadable_with_dark_themes)
    *   [6.9 LibreOffice toolbars unreadable with dark Breeze/Plasma 5 theme](#LibreOffice_toolbars_unreadable_with_dark_Breeze/Plasma_5_theme)
    *   [6.10 LibreOffice Math formula editor unreadable with dark theme](#LibreOffice_Math_formula_editor_unreadable_with_dark_theme)
    *   [6.11 AutoText expected default behaviour not functional in system locales other than en_US](#AutoText_expected_default_behaviour_not_functional_in_system_locales_other_than_en_US)
    *   [6.12 LibreOffice freezes](#LibreOffice_freezes)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") one of the following packages:

*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) is the stable maintenance branch, for conservative users.
*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) is the feature branch, with new program enhancements for early adopters or power users.

**Note:**

*   In the past, the installation of at least 1 language pack was required. Currently, LibreOffice detects your system defaults; manual installation of a language pack is no longer mandatory. See [help.libreoffice.org](https://help.libreoffice.org/Scalc/cui/ui/optlanguagespage/ignorelanguagechange#User_interface) for additional information.
*   If you want the UK-English language pack, install [libreoffice-fresh-en-gb](https://www.archlinux.org/packages/?name=libreoffice-fresh-en-gb), not [libreoffice-fresh-uk](https://www.archlinux.org/packages/?name=libreoffice-fresh-uk) (Ukrainian) or [libreoffice-fresh-br](https://www.archlinux.org/packages/?name=libreoffice-fresh-br) (Breton)!
*   For SDK install [libreoffice-fresh-sdk](https://www.archlinux.org/packages/?name=libreoffice-fresh-sdk).
*   For Qt and GTK visual integration, see [#Theme](#Theme).

Check the optional dependencies pacman displays. If you use HSQLDB Embedded in LibreOffice Base, you must install a [Java Runtime Environment](/index.php/Java "Java"). You may need [hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/) to use [some modules](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) in LibreOffice Base.

## Theme

LibreOffice includes support for [GTK](/index.php/GTK "GTK") and [Qt](/index.php/Qt "Qt") theme integration. See also [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

LibreOffice will try to autodetect the most suitable VCL UI interface based on your desktop environment. To force the use of a certain VCL UI interface, use one of the `SAL_USE_VCLPLUGIN=gen`, `SAL_USE_VCLPLUGIN=kde5`, or `SAL_USE_VCLPLUGIN=gtk3` [environment variables](/index.php/Environment_variables "Environment variables"). These variables can be uncommented in `/etc/profile.d/libreoffice-fresh.sh` or `/etc/profile.d/libreoffice-still.sh`.

**Note:**

*   When using the [LXDE](/index.php/LXDE "LXDE") desktop environment, setting `SAL_USE_VCLPLUGIN` in `/etc/profile.d/libreoffice-fresh.sh` has no effect since the `SAL_USE_VCLPLUGIN` [environment variable](/index.php/Environment_variable "Environment variable") is afterwards set to `gtk` by the script `/usr/bin/startlxde`. In order to use `gtk3` toolkit with [LXDE](/index.php/LXDE "LXDE") the `SAL_USE_VCLPLUGIN` [environment variable](/index.php/Environment_variable "Environment variable") needs to be set after launching the desktop environment. [upstream bug](https://sourceforge.net/p/lxde/bugs/868/)
*   In LibreOffice 6.4, the `kde5` backend will be [renamed](https://gerrit.libreoffice.org/plugins/gitiles/core/+/2113f3e7ee0ca5c07f224a54b627777b3a7b5fb0%5E%21/) to `kf5`.

However, if it looks like it is using Windows 95/98 icons, go to *Tools > Options...* in the menus (which presents the Options Dialog), then select *LibreOffice > Accessibility* and uncheck "Automatically detect high-contrast mode of operating system".

If that does not work immediately, you may need to change the icon set that is in use; this is also in the Options Dialog, under *LibreOffice > View* with two pop-up boxes for "Icon size and style" (the latter pop-up box should be changed to something other than "High-contrast").

### Disable startup logo

If you prefer to disable the startup logo, open `/etc/libreoffice/sofficerc`, find the `Logo=` line and set `Logo=0`.

**Note:** This variable is unrelated with the Logo scripting support.

## Extension management

The following additional extensions are available:

*   [libreoffice-extension-texmaths](https://www.archlinux.org/packages/?name=libreoffice-extension-texmaths)
*   [libreoffice-extension-writer2latex](https://www.archlinux.org/packages/?name=libreoffice-extension-writer2latex)

For more extensions, check the [AUR](/index.php/AUR "AUR"), the built-in LibreOffice Extension manager, or [libreplanet](https://libreplanet.org/wiki/Group:OpenOfficeExtensions/List).

## Language aids

### Spell checking

For spell checking, please make sure [hunspell](https://www.archlinux.org/packages/?name=hunspell) is properly installed; this should be the case for both *still* and *fresh* LibreOffice versions. Then install a language dictionary for hunspell like [hunspell-en_US](https://www.archlinux.org/packages/?name=hunspell-en_US) for American English or [hunspell-de](https://www.archlinux.org/packages/?name=hunspell-de) for German. Then enable the Writing aids by selecting the check-box in *Tools > Options > Language Settings > Writing Aids > Hunspell SpellChecker* after restarting LibreOffice.

	Finnish

Unlike other languages, Finnish dictionaries use different naming. These four packages should be installed (in this order): [libvoikko](https://www.archlinux.org/packages/?name=libvoikko), [malaga](https://aur.archlinux.org/packages/malaga/), [voikko-fi](https://aur.archlinux.org/packages/voikko-fi/), [hfstospell](https://aur.archlinux.org/packages/hfstospell/) and [voikko-libreoffice](https://aur.archlinux.org/packages/voikko-libreoffice/).

	Greek

Project [Orthos](https://sourceforge.net/projects/orthos-spell/?source=directory) provides more complete Greek spell checkers as Libreoffice extensions. Package [libreoffice-extension-orthos-greek-dictionary](https://aur.archlinux.org/packages/libreoffice-extension-orthos-greek-dictionary/) provides a Greek-only spelling dictionary, while [libreoffice-extension-orthos-greek-english-dictionary](https://aur.archlinux.org/packages/libreoffice-extension-orthos-greek-english-dictionary/) provides one that bundles Greek and US English.

### Hyphenation rules

For hyphenation rules, you will need [hyphen](https://www.archlinux.org/packages/?name=hyphen) and a language hyphen rule set ([hyphen-en](https://www.archlinux.org/packages/?name=hyphen-en) for English, [hyphen-de](https://www.archlinux.org/packages/?name=hyphen-de) for German, etc).

### Thesaurus

For the thesaurus option, you will need [libmythes](https://www.archlinux.org/packages/?name=libmythes) and a mythes language thesaurus (like [mythes-en](https://www.archlinux.org/packages/?name=mythes-en) for English, [mythes-de](https://www.archlinux.org/packages/?name=mythes-de) for German, etc).

	Greek

For Greek, instead of [mythes-el](https://aur.archlinux.org/packages/mythes-el/) you may want to try out [libreoffice-extension-orthos-greek-thesaurus](https://aur.archlinux.org/packages/libreoffice-extension-orthos-greek-thesaurus/), which includes more words.

### Grammar checking

For grammar checking, several tools are available. The most common is [LanguageTool](https://www.languagetool.org/). While the [languagetool](https://www.archlinux.org/packages/?name=languagetool) is available, it is not packaged as a LibreOffice extension. It is thus recommended to install the LibreOffice extension manually or with [libreoffice-extension-languagetool](https://aur.archlinux.org/packages/libreoffice-extension-languagetool/) instead. Even though the extension comes bundled with LanguageTool, this does not conflict with [languagetool](https://www.archlinux.org/packages/?name=languagetool).

After this extension has been installed, please make sure you have a [Java](/index.php/Java "Java") 8 runtime installed ([jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk)). Indeed, Languagetool uses Java and may slow down or briefly hang LibreOffice, particularly while opening documents. Fortunately this is usually only when initially opening a document and is usually not apparent otherwise. Once installed, you want to enable it as the default environment for LibreOffice. To do that go to "Tools" --> "Options" --> "Advanced" and select the appropiate JRE (it will be shown as 1.8.0) then press "Ok". You will be prompted to restart the LibreOffice suite. Once restarted you will be able to install Languagetools without trouble.

Other grammar tools can also be found on the [LibrePlanet extension page](https://libreplanet.org/wiki/Group:OpenOfficeExtensions/List), on the [official LibreOffice Extensions website](https://extensions.libreoffice.org/) or [OpenOffice's Website](https://www.openoffice.org/lingucomponent/grammar.html). Please note all OpenOffice extensions are guaranteed to work with LibreOffice.

	French

French-speaking users are advantaged here: they do not need to install LanguageTool nor Java. Dicollecte provides a nice Python extension, specifically designed for Frenchs. You can install it [from the website](https://www.dicollecte.org/grammalecte/telecharger.php) or via [libreoffice-extension-grammalecte-fr](https://aur.archlinux.org/packages/libreoffice-extension-grammalecte-fr/). In any case, this extensions also comes with the French dictionaries otherwise provided by [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr).

### Offline help for en-US

As of version 5.2.2, [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) provides the offline help files for en-US. Help files for different locales is provided by the appropriate libreoffice language package, (i.e., [libreoffice-fresh-en-za](https://www.archlinux.org/packages/?name=libreoffice-fresh-en-za) provides the help files for en-ZA locales).

## Installing macros

If you intend to use macros, you must have a Java Runtime Environment enabled.

The default path for macros in Arch Linux is different from most Linux distributions. Its location is: `~/.config/libreoffice/4/user/Scripts/`.

## Troubleshooting

A general way to track down problems is the safe mode in LibreOffice:

```
$ libreoffice --safe-mode

```

### Font substitution

These settings can be changed in the LibreOffice options. From the drop-down menu, select *Tools > Options > LibreOffice > Fonts*. Check the box that says *Apply Replacement Table*. Type `Andale Sans UI` in the font box and choose your desired font for the *Replace with* option. When done, click the *checkmark*. Then choose the *Always* and *Screen only* options in the box below. Click OK. You will then need to go to *Tools > Options > LibreOffice > View*, and uncheck "Use system font for user interface". If you use a non-antialised font, such as Arial, you will also need to uncheck "Screen font antialiasing" before menu fonts render correctly.

### Anti-aliasing

Execute:

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

To make the change persistent, add `Xft.lcdfilter: lcddefault` to your `~/.Xresources` file, and make sure to run `$ xrdb -merge ~/.Xresources` ([source](https://bugs.launchpad.net/ubuntu/+source/cairo/+bug/271283/comments/23)). See [X resources](/index.php/X_resources "X resources") for more details.

If this does not work, you can also try adding `Xft.lcdfilter: lcddefault` to your `~/.Xdefaults`. If you do not have this file, you will have to create it.

### Hanging when using NFSv3 shares

If LibreOffice hangs when trying to open or save a document located on a NFSv3 share, try prepending the following lines with a `#` in `/usr/lib/libreoffice/program/soffice`:

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

To avoid overwriting on update you can copy `/usr/lib/libreoffice/program/soffice` in `/usr/local/bin`. Original post [here](http://195.110.9.173/computing/debian/bugs/openoffice-over-nfs.jspx).

### LibreOffice does not detect my certificates

If you cannot see the certificates when trying to sign a document, you will need to have the certificates configured in Mozilla Firefox (or Thunderbird). If after that LibreOffice still does not show them, set the `MOZILLA_CERTIFICATE_FOLDER` environment variable to point to your Mozilla Firefox (or Thunderbird) folder:

```
export MOZILLA_CERTIFICATE_FOLDER=$HOME/.mozilla/firefox/XXXXXX.default/

```

[Certificate detection](https://wiki.openoffice.org/wiki/Certificate_Detection).

### Run .pps files in edit mode (without slideshow)

The only solution is to rename the `.pps` file to `.ppt`.

Add the following script to your home directory and use it to open every .pps file. Very useful to open `.pps` files received by email without the need to save them.

```
#!/bin/bash

f=$(mktemp --suffix .ppt)
cp "$1" "${f}" && libreoffice "${f}" && rm -f "${f}"

```

### Media support

If embedded videos are just gray boxes, make sure to have installed the [GStreamer plugins](/index.php/GStreamer#Installation "GStreamer") required.

### Default paper size in Writer and Draw

If the default paper size in blank Writer and Draw documents is persistently incorrect for your locale, try installing the [libpaper](https://www.archlinux.org/packages/?name=libpaper) optional dependency and either updating `/etc/papersize` (for a system-wide change) or exporting the `PAPERSIZE` environment variable (for a user change) with your preferred paper size. See [papersize(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/papersize.5).

**Note:** [libpaper](https://www.archlinux.org/packages/?name=libpaper) defaults to **Letter** paper size if nothing else has been set.

### LibreOffice toolbars unreadable with dark themes

See [https://bugs.documentfoundation.org/show_bug.cgi?id=94632](https://bugs.documentfoundation.org/show_bug.cgi?id=94632)

To use toolbar icons compatible with dark themes, set [environment variable](/index.php/Environment_variable "Environment variable") `VCL_ICONS_FOR_DARK_THEME=1`

As an alternative workaround, run *libreoffice* with a light theme (e.g. with environment variable `GTK_THEME=Adwaita:light`).

### LibreOffice toolbars unreadable with dark Breeze/Plasma 5 theme

If you do not want to install [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) change the icon style in *Tools > Options > LibreOffice > View > Icon Style* to a readable one provided by LibreOffice.

Otherwise [install](/index.php/Install "Install") the Breeze theme for [GTK](/index.php/GTK "GTK"), [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk), and, if using a LibreOffice version < 5.3.0, the Breeze dark icons for LibreOffice, [libreoffice-breeze-icons](https://aur.archlinux.org/packages/libreoffice-breeze-icons/).

Just enable "Breeze Dark" or another readable icon style in *Tools > Options > LibreOffice > View > Icon Style* then.

If that is not enough, ensure that LibreOffice starts using the `gtk` interface - see [#Theme](#Theme).

If this still does not work correctly, try using the `gen` interface instead. [[1]](https://bbs.archlinux.org/viewtopic.php?id=206813)

### LibreOffice Math formula editor unreadable with dark theme

Text in formula editor is also unreadable if a dark theme is in use. There is an ongoing [bug report](https://bugs.documentfoundation.org/show_bug.cgi?id=90297).

Some have had success with overriding text color in LibreOffice preferences, but that changes text color everywhere, such as the document itself, which is still white.

Only workaround known is to override the theme to a light one (e.g. `GTK_THEME=Adwaita:light`).

### AutoText expected default behaviour not functional in system locales other than en_US

If expected default AutoText behaviour is not present (for example, typing `fn` in a document in Writer and then pressing the `F3` key does not result in the automatic insertion of a numbered function) when the system locale is not `en_US` you need to add the default `en_US` AutoText templates to your AutoText path. To do this, go to *Tools > AutoText*, then click on *Path...* and add the following path to the list: `/usr/lib/libreoffice/share/autotext/en-US`. AutoText should now work as expected by default.

### LibreOffice freezes

Disable OpenCL and/or OpenGL by setting the [environment variable](/index.php/Environment_variable "Environment variable") `SAL_DISABLE_OPENCL=1` and/or `SAL_DISABLEGL=1`. The LibreOffice safe mode also offers the option to disable both.

## See also

*   [Libreoffice Extensions](https://extensions.libreoffice.org/extensions)
*   [Libreoffice Templates](https://extensions.libreoffice.org/templates)
*   [Wikipedia:LibreOffice](https://en.wikipedia.org/wiki/LibreOffice "wikipedia:LibreOffice")