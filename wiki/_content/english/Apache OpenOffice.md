**Note:** Official support for [OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org") was dropped in favor of [LibreOffice](/index.php/LibreOffice "LibreOffice"), the "Document Foundation" fork of the project, which also includes enhancements and additional features. See [Dropping Oracle OpenOffice (arch-general)](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html).

From [Why Apache OpenOffice](http://why.openoffice.org/):

	Apache OpenOffice is the leading open-source office software suite for word processing, spreadsheets, presentations, graphics, databases and more. It is available in many languages and works on all common computers. It stores all your data in an international open standard format and can also read and write files from other common office software packages. It can be downloaded and used completely free of charge for any purpose.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Microsoft fonts](#Microsoft_fonts)
    *   [1.2 Extension management and spell checking](#Extension_management_and_spell_checking)
        *   [1.2.1 Spellchecker](#Spellchecker)
        *   [1.2.2 Other extensions installed by default](#Other_extensions_installed_by_default)
    *   [1.3 Installing macros](#Installing_macros)
    *   [1.4 Install TrueType fonts](#Install_TrueType_fonts)
*   [2 Theme](#Theme)
    *   [2.1 KDE4/Qt4 look and feel](#KDE4/Qt4_look_and_feel)
        *   [2.1.1 Use different configuration from general theme](#Use_different_configuration_from_general_theme)
*   [3 Speed up OpenOffice](#Speed_up_OpenOffice)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Font substitution](#Font_substitution)
    *   [4.2 Anti-aliasing](#Anti-aliasing)
    *   [4.3 Spell checking problems](#Spell_checking_problems)
    *   [4.4 Dark GTK themes, icons and GTK-Qt Engine](#Dark_GTK_themes,_icons_and_GTK-Qt_Engine)
    *   [4.5 Hanging when using NFSv3 shares](#Hanging_when_using_NFSv3_shares)
    *   [4.6 Fixing Java framework error](#Fixing_Java_framework_error)
    *   [4.7 OpenOffice does not detect my certificates](#OpenOffice_does_not_detect_my_certificates)

## Installation

[Install](/index.php/Install "Install") the [openoffice](https://aur.archlinux.org/packages/openoffice/) package. It is recommended to also install [Java](/index.php/Java "Java").

### Microsoft fonts

Official Microsoft fonts are useful to prevent pagination problems. Check the [MS Fonts](/index.php/MS_Fonts "MS Fonts") wiki page.

### Extension management and spell checking

The Arch package is now shipped with some dictionaries. Check *Extension manager* if your language is already there simply by loading up any OpenOffice program (Writer for example) and access the *Extension Manager* from the Tools menu. From there enter the following location to install a spell check dictionary:

```
/usr/lib/openoffice/share/extension/install/

```

**Note:** If you installed LibreOffice, the path will be `/usr/lib/libreoffice/share/extensions/` instead and extensions are currently all already known to the system.

Alternatively, there are several ways to accomplish this:

*   Use the *Extension manager* from OpenOffice menu for download and installation - installs only for the user into his `~/.openoffice.org/3/user/uno_packages/cache`
*   Download the extension and install it using `/usr/lib/openoffice/program/unopkg add extension` for the user
*   Download the extension and install it using `/usr/lib/openoffice/program/unopkg add --shared extension` for every user on the system (requires root permission)

#### Spellchecker

For spellchecking you will need [hunspell](https://www.archlinux.org/packages/?name=hunspell) and dictionary for hunspell (like [hunspell-en_US](https://www.archlinux.org/packages/?name=hunspell-en_US), [hunspell-de](https://www.archlinux.org/packages/?name=hunspell-de), etc), for hyphenation rules you will need [hyphen](https://www.archlinux.org/packages/?name=hyphen) ([hyphen-en](https://www.archlinux.org/packages/?name=hyphen-en), [hyphen-de](https://www.archlinux.org/packages/?name=hyphen-de), etc) and for a thesaurus, [libmythes](https://www.archlinux.org/packages/?name=libmythes).

#### Other extensions installed by default

*   **pdfimport.oxt** - Ability to import PDF files in Draw and Impress
*   **presenter-screen.oxt** - When using two displays this plugin provides more control over slideshow
*   **sun-presentation-minimizer.oxt** - Reduce file size of current presentation
*   **wiki-publisher.oxt** - Allows to create Wiki articles on MediaWiki servers without having to know the syntax of the MediaWiki markup language

### Installing macros

In most Linux distros, the default path for macros is:

```
~/.openoffice.org/3/user/Scripts/

```

The path for this directory in Arch Linux is:

```
~/.config/.openoffice.org/3/user/Scripts/

```

Macros are not guaranted to work in both OpenOffice and LibreOffice, but it is possible to choose a common directory for them. Choose the path in *Tools > Options > LibreOffice/OpenOffice > Paths* The default path for LibreOffice macros in Arch Linux is:

```
~/.config/libreoffice/4/user/Scripts/

```

**Note:** If you intend to use macros, you must have a Java Runtime Environment. This behaviour is a default, but disabling it [speeds up](#Speed_up_OpenOffice) the loading time.

### Install TrueType fonts

To add fonts to those already available in OpenOffice, run `spadmin`.

## Theme

OpenOffice supports to use several toolkits for drawing and integrates into different desktop environments in a clean way. To choose by hand, you need to set the `OOO_FORCE_DESKTOP` environment variable. Its possible values are *gnome* and *kde4*.

To configure the look for anytime OpenOffice gets started, you can export the `OOO_FORCE_DESKTOP` variable in `/etc/profile.d/openoffice.sh`, or in `/usr/bin/soffice`. Alternatively you can put the variable in any OpenOffice desktop file in `Exec` line between `Exec` and the command, then copy them to `$XDG_DATA_HOME/applications` in order to prevent overwriting on update.

### KDE4/Qt4 look and feel

Check [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for a broad application, general tips and other methods to achieve it.

#### Use different configuration from general theme

Do **not** select *Use my KDE style in GTK applications*. Instead choose a native syle and font for GTK 2 applications.

Use a program like [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme) to select a style (in general different from KDE) and a font (may be the same as your KDE general system font). There are also other GTK engine packages available.

There are two relevant parts of the OpenOffice options dialog, *View* and *Fonts*:

*   **View**
    *   Set scale to 100%
    *   Set use system font OFF (otherwise replacement table will not be used)
    *   Set antialiasing OFF

*   **Fonts**
    *   Select *Use replacement table*
    *   Replace *Andale Sans UI* (you **must** type this in -- it is not in the drop down list) with another font (your KDE system font or another if this looks bad)
    *   Press the tick symbol to update the list
    *   Select *Always* and *Screen only*
    *   Press *OK*

When choosing fonts for OpenOffice note that the poor font rendering engine included in the package may not render a particular font in the same way as other apps on the desktop.

## Speed up OpenOffice

Some settings may improve OpenOffice's loading time and responsiveness. However, some also increase RAM usage, so use them carefully. They can all be accessed under *Tools > Options*.

*   Under *Memory*:
    *   Reduce the number of *Undo > Number of steps* to a figure lower than 100, to something like 40 or 50 steps
    *   Under *Graphics cache*, set *Use for OpenOffice* to 128 MB (up from the original 20MB).
    *   Set *Memory per object* to 20MB (up from the default 5MB)
    *   If you use OpenOffice often, check *OpenOffice Quickstarter*
*   Under *Java*, uncheck Use a Java runtime environment

**Note:** For a list of functionality which depends on OpenOffice Java support, see this page: [http://wiki.services.openoffice.org/wiki/Java](http://wiki.services.openoffice.org/wiki/Java).

## Troubleshooting

### Font substitution

These settings can be changed in the OpenOffice options. From the drop-down menu, select *Tools > Options > OpenOffice > Fonts*. Check the box that says *Apply Replacement Table*. Type `Andale Sans UI` in the font box and choose your desired font for the *Replace with* option. When done, click the *checkmark*. Then choose the *Always* and *Screen only* options in the box below. Click OK. You will then need to go to *Tools > Options > OpenOffice > View*, and uncheck *Use system font for user interface*. If you use a non-antialised font, such as Arial, you will also need to uncheck *Screen font antialiasing* before menu fonts render correctly.

### Anti-aliasing

Execute:

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

To make the change persistent, add `Xft.lcdfilter: lcddefault` to your `~/.Xresources` file[[1]](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19).

If this does not work, make sure you are running `$ xrdb -merge ~/.Xresources` every time you launch [Xorg](/index.php/Xorg "Xorg"). If you do not have this file, you will have to create it.

### Spell checking problems

As of OpenOffice 3.0.0-2, various dictionaries may be buggy due to a character encoding problem. To solve this issue, follow the following instructions.

Find where the particular openoffice distribution places its dictionary files; e.g., `pacman -Ql openoffice-base`. Most distibutions follow the convention of installing these to `/usr/lib/openoffice/share/extension/install`. Once the directory has been found, assign it to a shell variable:

```
droot="/usr/lib/openoffice/share/extension/install"

```

Install [unzip](https://www.archlinux.org/packages/?name=unzip) and [zip](https://www.archlinux.org/packages/?name=zip) packages in order to be able to extract and compress the dictionary files.

For reference, get a list of languages whose dictionary files are packaged with the base distribution:

```
cd "$droot" && ls | sed -rn 's,^dict-(..)\.oxt$,\1,p'

```

Define a list of languages whose dictionary files are to be fixed:

```
lang="en es"

```

Extract the target languages' dictionary files and convert the erroneous encoding to *UTF-8*:

```
tmp="/tmp/dictfix-$USER-$$"

mkdir "$tmp"
cd "$tmp"

for i in $lang; do
    i="$droot/dict-$i.oxt"
    unzip "$i" -d oxt.tmp
    iconv -f ISO-8859-15 -t UTF-8 oxt.tmp/dictionaries.xcu > dict.tmp
    mv dict.tmp oxt.tmp/dictionaries.xcu
    (cd oxt.tmp && zip -r "$i" .)
done

rm -rf "$tmp"
```

Finally, use the OpenOffice extension manager (available through the *Tools* menu) to install the dictionary from the resulting `dict-*xx*.oxt` file(s).

### Dark GTK themes, icons and GTK-Qt Engine

Older OpenOffice/LibreOffice versions would start in *High Contrast Mode* if you use dark [GTK](/index.php/GTK "GTK") themes. This might prevent you from changing *High Contrast Icons* or Calc cell background coloring is completely disabled.

In newer version of OpenOffice / LibreOffice ( > 3.2.x), possible solutions may be:

*   You could manually configure UI colors via *Tools > Options > Appearance*, yet Impress and Calc may stay dark.
*   Another solution is to disable *Automatically detect high-contrast mode of operation system* in *LibreOffice > Accessibility* (> LO 4.1.x).

Now the colors can be configured in *Options > Appearance* and the selection of another iconset is possible again.

### Hanging when using NFSv3 shares

If OpenOffice hangs when trying to open/save a document located on a NFSv3 share, try prepending the following lines with a `#` in `/usr/lib/openoffice/program/soffice`.:

```
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

If you wish to avoid `/usr/lib/openoffice/program/soffice` overwriting on update just copy it in `/usr/local/bin`. Original post [here](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx).

### Fixing Java framework error

You may get the following error when you try to run OpenOffice:

```
[Java framework] Error in function createSettingsDocument (elements.cxx).
javaldx failed!

```

If so, give yourself ownership of `~/.config/` like so:

```
# chown -vR username:users ~/.config

```

[Post on Arch Linux Forums.](https://bbs.archlinux.org/viewtopic.php?id=93168)

### OpenOffice does not detect my certificates

If you cannot see the certificates when trying to sign a document, you will need to have the certificates configured in Firefox (or Thunderbird). If after that OpenOffice still does not show them, set the `MOZILLA_CERTIFICATE_FOLDER` environment variable pointing to your Firefox (or Thunderbird) folder.

```
export MOZILLA_CERTIFICATE_FOLDER=$HOME/.mozilla/firefox/XXXXXX.default/

```

See more about [certificate detection](http://wiki.openoffice.org/wiki/Certificate_Detection).