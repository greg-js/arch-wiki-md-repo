Related articles

*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [Fonts](/index.php/Fonts "Fonts")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")

This article explains how to install TrueType Microsoft fonts and emulate Windows' font rendering.

**Tip:** See [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts") for alternatives.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Using fonts from a Windows partition](#Using_fonts_from_a_Windows_partition)
    *   [1.2 Extracting fonts from a Windows ISO](#Extracting_fonts_from_a_Windows_ISO)
    *   [1.3 Current packages](#Current_packages)
    *   [1.4 Legacy packages](#Legacy_packages)
*   [2 Fontconfig rules useful for MS Fonts](#Fontconfig_rules_useful_for_MS_Fonts)
*   [3 Windows 8](#Windows_8)

## Installation

### Using fonts from a Windows partition

If there is a Windows partition mounted, its fonts can be used by linking to them.

*For example, if the Windows C:\ partition is mounted at `/windows`:*

```
# ln -s /windows/Windows/Fonts /usr/share/fonts/WindowsFonts

```

Then regenerate the fontconfig cache:

```
# fc-cache -f

```

Alternatively, copy the Windows fonts to `/usr/share/fonts`:

```
# mkdir /usr/share/fonts/WindowsFonts
# cp /windows/Windows/Fonts/* /usr/share/fonts/WindowsFonts
# chmod 755 /usr/share/fonts/WindowsFonts/*

```

Then regenerate the fontconfig cache:

```
# fc-cache -f

```

### Extracting fonts from a Windows ISO

The fonts can also be found in a Windows ISO file.

Extract the `/sources/install.esd` file in the ISO and look for a `Windows/Fonts` directory within this file. The format of this file is ESD *(Windows Electronic Software Download)* and it can be extracted with [p7zip](/index.php/P7zip "P7zip").

### Current packages

**Note:** These packages do **require access to a Windows 7/8/10 and/or a Office 2007** setup or installation media, consult corresponding [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for details.

*   [ttf-office-2007-fonts](https://aur.archlinux.org/packages/ttf-office-2007-fonts/) — Office 2007 fonts
*   [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/) — Windows 7 fonts
*   [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) — Windows 8.1 fonts
*   [ttf-ms-win10](https://aur.archlinux.org/packages/ttf-ms-win10/) — Windows 10 fonts

### Legacy packages

**Note:** The fonts provided by these packages are out-of-date and are missing modern hinting instructions and the full character sets. It is recommended to use the above packages.

[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) includes:

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono")
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial")
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black")
*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans")
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New")
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) "wikipedia:Georgia (typeface)")
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) "wikipedia:Impact (typeface)")
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans")
*   [Lucida Console](https://en.wikipedia.org/wiki/Lucida_Console "wikipedia:Lucida Console")
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif")
*   ~~[Symbol](https://en.wikipedia.org/wiki/Symbol_(typeface) "wikipedia:Symbol (typeface)")~~
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman")
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS")
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana")
*   [Webdings](https://en.wikipedia.org/wiki/Webdings "wikipedia:Webdings")
*   [Wingdings](https://en.wikipedia.org/wiki/Wingdings "wikipedia:Wingdings")

**Warning:** According to [original Microsoft's End User License Agreement](http://web.archive.org/web/20020227054122/www.microsoft.com/typography/fontpack/eula.htm), there are *some* legal limitations when using the above fonts.

You can also obtain [ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/) which, as you might expect, contains [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) "wikipedia:Tahoma (typeface)").

[ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/) includes:

*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri")
*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) "wikipedia:Cambria (typeface)")
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara")
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas")
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) "wikipedia:Constantia (typeface)")
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) "wikipedia:Corbel (typeface)")

## Fontconfig rules useful for MS Fonts

Often websites specify the fonts using generic names (helvetica, courier, times or times new roman) a rule in fontconfig replaces this fonts with (ugly) free fonts:

```
/etc/fonts/conf.d/30-metric-aliases-free.conf

```

to make full use of the MS fonts it is necessary to create a rule mapping those generic names to MS specific fonts contained in the various packages above:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
       <alias binding="same">
         <family>Helvetica</family>
         <accept>
         <family>Arial</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Times</family>
         <accept>
         <family>Times New Roman</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Courier</family>
         <accept>
         <family>Courier New</family>
         </accept>
       </alias>
</fontconfig>

```

It is also useful to associate serif,sans-serif,monospace fonts in your favourite browser to MS fonts.

## Windows 8

The [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) split package is intended as a more up-to-date replacement for [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/), [ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/) and [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/).

Although it provides newer versions of the fonts, it **cannot automatically download the fonts** due to license issues .

**Note:** usage of Microsoft fonts outside running Windows system is prohibited by EULA (although in certain countries EULA is invalid). Please consult Microsoft license before using fonts.

You can acquire fonts from an installed and fully updated Windows 8.1 system. Any edition of *Windows 8.1 build **Windows 8.1 6.3.9600.17238*** will work.

On the installed Windows 8.1 system fonts are usually located in `[%WINDIR%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\Fonts` and license file is `[%SYSTEM32%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\license.rtf`.

You need the files listed in the `source=()` array. Place them in the same directory as this [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") file, then run [makepkg](/index.php/Makepkg "Makepkg").

`makepkg --pkg ttf-ms-win8` will make just the Windows 8.1 core fonts package which should cover even more than [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).