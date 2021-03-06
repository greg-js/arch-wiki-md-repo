Related articles

*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console")
*   [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts")

From [Wikipedia:Computer font](https://en.wikipedia.org/wiki/Computer_font "wikipedia:Computer font"): "A computer font (or font) is an electronic data file containing a set of glyphs, characters, or symbols such as dingbats."

Note that certain font licenses may impose some legal limitations.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Font formats](#Font_formats)
    *   [1.1 Bitmap formats](#Bitmap_formats)
    *   [1.2 Outline formats](#Outline_formats)
    *   [1.3 Other formats](#Other_formats)
*   [2 Installation](#Installation)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 Creating a package](#Creating_a_package)
    *   [2.3 Manual installation](#Manual_installation)
    *   [2.4 Older applications](#Older_applications)
    *   [2.5 Pango Warnings](#Pango_Warnings)
*   [3 Font packages](#Font_packages)
    *   [3.1 Bitmap](#Bitmap)
    *   [3.2 Latin script](#Latin_script)
        *   [3.2.1 Families](#Families)
        *   [3.2.2 Monospaced](#Monospaced)
        *   [3.2.3 Sans-serif](#Sans-serif)
        *   [3.2.4 Serif](#Serif)
        *   [3.2.5 Unsorted](#Unsorted)
    *   [3.3 Non-latin scripts](#Non-latin_scripts)
        *   [3.3.1 Ancient Scripts](#Ancient_Scripts)
        *   [3.3.2 Arabic](#Arabic)
        *   [3.3.3 Braille](#Braille)
        *   [3.3.4 Chinese, Japanese, Korean, Vietnamese](#Chinese,_Japanese,_Korean,_Vietnamese)
            *   [3.3.4.1 Pan-CJK](#Pan-CJK)
            *   [3.3.4.2 Chinese](#Chinese)
            *   [3.3.4.3 Japanese](#Japanese)
            *   [3.3.4.4 Korean](#Korean)
            *   [3.3.4.5 Vietnamese](#Vietnamese)
        *   [3.3.5 Cyrillic](#Cyrillic)
        *   [3.3.6 Greek](#Greek)
        *   [3.3.7 Hebrew](#Hebrew)
        *   [3.3.8 Indic](#Indic)
        *   [3.3.9 Khmer](#Khmer)
        *   [3.3.10 Mongolic and Tungusic](#Mongolic_and_Tungusic)
        *   [3.3.11 Persian](#Persian)
        *   [3.3.12 Tai–Kadai](#Tai–Kadai)
        *   [3.3.13 Tibeto-Burman](#Tibeto-Burman)
    *   [3.4 Emoji and symbols](#Emoji_and_symbols)
    *   [3.5 Math](#Math)
    *   [3.6 Other operating system fonts](#Other_operating_system_fonts)
*   [4 Fallback font order with X11](#Fallback_font_order_with_X11)
*   [5 Font alias](#Font_alias)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 List all installed fonts](#List_all_installed_fonts)
    *   [6.2 List installed fonts for a particular language](#List_installed_fonts_for_a_particular_language)
    *   [6.3 List installed fonts for a particular Unicode character](#List_installed_fonts_for_a_particular_Unicode_character)
    *   [6.4 Set terminal font on-the-fly](#Set_terminal_font_on-the-fly)
    *   [6.5 Application-specific font cache](#Application-specific_font_cache)
    *   [6.6 Force color emoji](#Force_color_emoji)
*   [7 See also](#See_also)

## Font formats

Most computer fonts used today are in either *bitmap* or *outline* data formats.

	Bitmap fonts

	Consist of a matrix of dots or pixels representing the image of each glyph in each face and size.

	Outline or *vector* fonts

	Use Bézier curves, drawing instructions and mathematical formulae to describe each glyph, which make the character outlines scalable to any size.

### Bitmap formats

*   [Bitmap Distribution Format](https://en.wikipedia.org/wiki/Glyph_Bitmap_Distribution_Format "wikipedia:Glyph Bitmap Distribution Format") (BDF) by Adobe
*   [Portable Compiled Format](https://en.wikipedia.org/wiki/Portable_Compiled_Format "wikipedia:Portable Compiled Format") (PCF) by Xorg
*   [PC Screen Font](https://en.wikipedia.org/wiki/PC_Screen_Font "wikipedia:PC Screen Font") (PSF) used by the Kernel for console fonts, not supported by Xorg (for Unicode PSF files the extension is `psfu`)

These formats can also be gzipped. See [#Bitmap](#Bitmap) for the available bitmap fonts.

### Outline formats

*   [PostScript fonts](https://en.wikipedia.org/wiki/PostScript_fonts "wikipedia:PostScript fonts") by Adobe – has various formats, e.g: Printer Font ASCII (PFA) and Printer Font Binary (PFB)
*   [TrueType](https://en.wikipedia.org/wiki/TrueType "wikipedia:TrueType") by Apple and Microsoft (file extension: `ttf`)
*   [OpenType](https://en.wikipedia.org/wiki/OpenType "wikipedia:OpenType") by Microsoft, built on TrueType (file extensions: `otf`, `ttf`)

For most purposes, the technical differences between TrueType and OpenType can be ignored.

### Other formats

The typesetting application [TeX](/index.php/TeX "TeX") and its companion font software, *Metafont,* traditionally renders characters using its own methods. Some file extensions used for fonts from these two programs are `*pk`, `*gf`, `mf` and `vf`. Modern versions can also use TrueType and OpenType fonts.

[FontForge](https://fontforge.github.io/en-US/) ([fontforge](https://www.archlinux.org/packages/?name=fontforge)), a font editing application, can store fonts in its native text-based format, `sfd`, *s*pline *f*ont *d*atabase.

The [SVG](http://www.w3.org/TR/SVG/fonts.html) format also has its own font description method.

## Installation

There are various methods for installing fonts.

### Pacman

Fonts and font collections in the enabled repositories can be installed using [pacman](/index.php/Pacman "Pacman").

Available fonts may be found by [querying packages](/index.php/Pacman#Querying_package_databases "Pacman") (e.g. for `font` or `ttf`).

### Creating a package

You should give pacman the ability to manage your fonts, which is done by creating an Arch package. These can also be shared with the community in the [AUR](/index.php/AUR "AUR"). The packages to install fonts are particularly similar; simply taking an existing [package](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/adobe-source-code-pro-fonts) as template should work well. To learn about how to modify it for your font, please refer to [Creating packages](/index.php/Creating_packages "Creating packages").

The family name of a font file can be aquired with the use of `fc-query` for example: `fc-query -f '%{family[0]}
' /path/to/file`. The formatting is described in [FcPatternFormat(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/FcPatternFormat.3).

### Manual installation

The recommended way of adding fonts that are not in the repositories to your system is described in [#Creating a package](#Creating_a_package). This gives pacman the ability to remove or update them at a later time. Fonts can alternately be installed manually as well.

To install fonts system-wide (available for all users), move the folder to the `/usr/share/fonts` directory. The files need to be readable by every user, use [chmod](/index.php/Chmod "Chmod") to set the correct permissions (i.e. at least `0444` for files and `0555` for directories). To install fonts for only a single user, use `~/.local/share/fonts/` (`~/.fonts/` is now deprecated).

For Xserver to load fonts directly (as opposed to the use of a *font server*) the directory for your newly added font must be added with a FontPath entry. This entry is located in the *Files* section [of your Xorg configuration file](/index.php/Xorg#Configuration "Xorg") (e.g. `/etc/X11/xorg.conf` or `/etc/xorg.conf`). See [#Older applications](#Older_applications) for more detail.

Then update the fontconfig font cache: (usually unnecessary as software using the fontconfig library does this)

```
$ fc-cache

```

### Older applications

With older applications that do not support fontconfig (e.g. GTK 1.x applications, and `xfontsel`) the index will need to be created in the font directory:

```
$ mkfontscale
$ mkfontdir

```

Or to include more than one folder with one command:

```
$ for dir in /font/dir1/ /font/dir2/; do xset +fp $dir; done && xset fp rehash

```

Or if fonts were installed in a different sub-folders under the e.g. `/usr/share/fonts`:

```
$ for dir in * ; do if [  -d  "$dir"  ]; then cd "$dir";xset +fp "$PWD" ;mkfontscale; mkfontdir;cd .. ;fi; done && xset fp rehash

```

At times the X server may fail to load the fonts directory and you will need to rescan all the `fonts.dir` files:

```
# xset +fp /usr/share/fonts/misc # Inform the X server of new directories
# xset fp rehash                # Forces a new rescan

```

To check that the font(s) is included:

```
$ xlsfonts | grep fontname

```

**Note:** Many packages will automatically configure Xorg to use the font upon installation. If that is the case with your font, this step is not necessary.

This can also be set globally in `/etc/X11/xorg.conf` or `/etc/X11/xorg.conf.d`.

Here is an example of the section that must be added to `/etc/X11/xorg.conf`. Add or remove paths based on your particular font requirements.

```
# Let X.Org know about the custom font directories
Section "Files"
    FontPath    "/usr/share/fonts/100dpi"
    FontPath    "/usr/share/fonts/75dpi"
    FontPath    "/usr/share/fonts/cantarell"
    FontPath    "/usr/share/fonts/cyrillic"
    FontPath    "/usr/share/fonts/encodings"
    FontPath    "/usr/share/fonts/misc"
    FontPath    "/usr/share/fonts/truetype"
    FontPath    "/usr/share/fonts/TTF"
    FontPath    "/usr/share/fonts/util"
EndSection

```

### Pango Warnings

When [Pango](http://www.pango.org/) is in use on your system it will read from [fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig) to sort out where to source fonts.

```
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='common'
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='latin'

```

If you are seeing errors similar to this and/or seeing blocks instead of characters in your application then you need to add fonts and update the font cache. This example uses the [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) fonts to illustrate the solution (after successful installation of the package) and runs as root to enable them system-wide.

 `# fc-cache` 
```
/usr/share/fonts: caching, new cache contents: 0 fonts, 3 dirs
/usr/share/fonts/TTF: caching, new cache contents: 16 fonts, 0 dirs
/usr/share/fonts/encodings: caching, new cache contents: 0 fonts, 1 dirs
/usr/share/fonts/encodings/large: caching, new cache contents: 0 fonts, 0 dirs
/usr/share/fonts/util: caching, new cache contents: 0 fonts, 0 dirs
/var/cache/fontconfig: cleaning cache directory
fc-cache: succeeded

```

You can test for a default font being set like so:

 `$ fc-match` 
```
LiberationMono-Regular.ttf: "Liberation Mono" "Regular"

```

## Font packages

This is a selective list that includes many font packages from the [AUR](/index.php/AUR "AUR") along with those in the official repositories. Fonts are tagged "Unicode" if they have wide Unicode support, see the project or Wikipedia pages for detail.

The [Archfonts Python script](https://github.com/ternstor/distrofonts) can be used to generate an overview of all the TTF fonts found in the official repositories / the AUR (the image generation is done using [ttf2png](https://aur.archlinux.org/packages/ttf2png/)).

### Bitmap

**Note:** [pango](https://www.archlinux.org/packages/?name=pango) 1.44 [dropped support for FreeType in favor of HarfBuzz](https://blogs.gnome.org/mclasen/2019/05/25/pango-future-directions/) thus [losing support for traditional BDF/PCF bitmap fonts](https://blogs.gnome.org/mclasen/2019/08/07/pango-1-44-wrap-up/), so applications like e.g. [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) will not work with such fonts anymore, showing rectangles instead of glyphs. See [FS#63297](https://bugs.archlinux.org/task/63297), [Pango issue #386](https://gitlab.gnome.org/GNOME/pango/issues/386) and [HarfBuzz issue #1897](https://github.com/harfbuzz/harfbuzz/issues/1897).

*   Default 8x16
*   [Berry](https://github.com/seraxis/pcf-spectrum-berry) ([pcf-spectrum-berry](https://aur.archlinux.org/packages/pcf-spectrum-berry/)) - 8px
*   [Dina](http://www.dcmembers.com/jibsen/download/61/) ([dina-font](https://www.archlinux.org/packages/?name=dina-font)) – 6pt, 8pt, 9pt, 10pt, monospaced, based on Proggy
*   [Efont](http://openlab.jp/efont/unicode/) ([efont-unicode-bdf](https://aur.archlinux.org/packages/efont-unicode-bdf/)) – 10px, 12px, 14px, 16px, 24px, normal, bold and italic
*   [Gohu](http://font.gohu.org/) ([gohufont](https://aur.archlinux.org/packages/gohufont/)) – 11px, 14px, normal and bold
*   [Lime](http://artwizaleczapka.sourceforge.net/) ([artwiz-fonts](https://aur.archlinux.org/packages/artwiz-fonts/))
*   [ProFont](http://tobiasjung.name/profont/) ([ttf-profont-iix](https://aur.archlinux.org/packages/ttf-profont-iix/)) – 10px, 11px, 12px, 15px, 17px, 22px, 29px, normal
*   [Proggy](https://en.wikipedia.org/wiki/Proggy_programming_fonts "wikipedia:Proggy programming fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/)) – has different variants
*   [Tamsyn](http://www.fial.com/~scott/tamsyn-font/) ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font))
*   [Terminus](http://terminus-font.sourceforge.net/) ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font))
*   [Tewi](https://github.com/lucy/tewi-font) ([bdf-tewi-git](https://aur.archlinux.org/packages/bdf-tewi-git/))
*   [Unifont](http://unifoundry.com/unifont.html) ([most extensive](https://en.wikipedia.org/wiki/Unicode_font#Comparison_of_fonts "wikipedia:Unicode font") Unicode coverage of any font) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont))

Works with pango 1.44:

*   [Terminus](http://terminus-font.sourceforge.net/) ([terminus-font-otb](https://www.archlinux.org/packages/?name=terminus-font-otb)) - OpenType Bitmap (OTB) variant of Terminus
*   [ProFont](http://tobiasjung.name/profont/) ([profont-otb](https://aur.archlinux.org/packages/profont-otb/)) - OpenType Bitmap (OTB) variant of ProFont
*   [Misc Fixed](https://xorg.freedesktop.org/releases/individual/font/) [xorg-fonts-misc-otb](https://aur.archlinux.org/packages/xorg-fonts-misc-otb/)
*   More [otb](https://aur.archlinux.org/packages/?O=0&SeB=n&K=-otb&outdated=&SB=n&SO=a&PP=50&do_Search=Go) fonts on AUR

### Latin script

#### Families

*   [Luxi fonts](https://en.wikipedia.org/wiki/Luxi_fonts "wikipedia:Luxi fonts") ([font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf)) – X.Org Luxi fonts
*   [Bitstream Vera](https://en.wikipedia.org/wiki/Bitstream_Vera "wikipedia:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera)) – serif, sans-serif, and monospace
*   [Courier Prime](https://quoteunquoteapps.com/courierprime/) ([ttf-courier-prime](https://aur.archlinux.org/packages/ttf-courier-prime/)) – Courier font alternative optimized for screenplays
*   [Croscore fonts](https://en.wikipedia.org/wiki/Croscore_fonts "wikipedia:Croscore fonts") ([ttf-croscore](https://www.archlinux.org/packages/?name=ttf-croscore)) – Google's substitute for Windows' Arial, Times New Roman, and Courier New
*   [DejaVu fonts](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) – Bitstream Vera modified for greater Unicode coverage
*   [Droid](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)) – default font for older Android versions
*   [Roboto](https://en.wikipedia.org/wiki/Roboto "wikipedia:Roboto") ([ttf-roboto](https://www.archlinux.org/packages/?name=ttf-roboto)) – default font for newer Android versions
*   [Google Noto](https://en.wikipedia.org/wiki/Noto_fonts "wikipedia:Noto fonts") ([noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts)) – Unicode
*   [Liberation fonts](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) – free metric-compatible substitute for the Arial, Arial Narrow, Times New Roman and Courier New fonts found in Windows and Microsoft Office products
*   [IBM Plex](https://en.wikipedia.org/wiki/IBM_Plex "wikipedia:IBM Plex") ([ttf-ibm-plex](https://www.archlinux.org/packages/?name=ttf-ibm-plex)) – serif, sans-serif, condensed sans-serif and monospace with true italics
*   [Ubuntu Font Family](https://en.wikipedia.org/wiki/Ubuntu_Font_Family "wikipedia:Ubuntu Font Family") ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts") ([ttf-ms-win10](https://aur.archlinux.org/packages/ttf-ms-win10/)) – Windows 10 fonts

Legacy Microsoft font packages:

*   [Microsoft fonts](http://corefonts.sourceforge.net/) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)) – Andalé Mono, Courier New, Arial, Arial Black, Comic Sans, Impact, Lucida Sans, Microsoft Sans Serif, Trebuchet, Verdana, Georgia, Times New Roman
*   Vista fonts ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)) – Consolas, Calibri, Candara, Corbel, Cambria, Constantia

#### Monospaced

For more monospaced fonts see [#Bitmap](#Bitmap) and [#Families](#Families).

*   [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [Cascadia Code](https://github.com/microsoft/cascadia-code) ([ttf-cascadia-code](https://www.archlinux.org/packages/?name=ttf-cascadia-code)) – with programming ligatures
*   [Envy Code R](https://damieng.com/blog/2008/05/26/envy-code-r-preview-7-coding-font-released) ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/))
*   Fantasque Sans Mono ([ttf-fantasque-sans-mono](https://www.archlinux.org/packages/?name=ttf-fantasque-sans-mono), [otf-fantasque-sans-mono](https://www.archlinux.org/packages/?name=otf-fantasque-sans-mono))
*   [Fira Mono](https://en.wikipedia.org/wiki/Fira_Sans "wikipedia:Fira Sans") ([ttf-fira-mono](https://www.archlinux.org/packages/?name=ttf-fira-mono), [otf-fira-mono](https://www.archlinux.org/packages/?name=otf-fira-mono)) – designed for Firefox OS
*   [Fira Code](https://github.com/tonsky/FiraCode) ([ttf-fira-code](https://www.archlinux.org/packages/?name=ttf-fira-code), [otf-fira-code](https://www.archlinux.org/packages/?name=otf-fira-code)) – with programming ligatures
*   [FreeMono](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)) - Unicode
*   [Hack](https://sourcefoundry.org/hack/) ([ttf-hack](https://www.archlinux.org/packages/?name=ttf-hack)) - an open source monospaced font, used as the default in KDE Plasma
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - inspired by Consolas
*   [Inconsolata-g](https://leonardo-m.livejournal.com/77079.html) ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - adds some programmer-friendly modifications
*   [Iosevka](https://be5invis.github.io/Iosevka/) ([ttf-iosevka](https://aur.archlinux.org/packages/ttf-iosevka/)) – slender sans-serif and slab-serif typeface inspired by Pragmata Pro, M+ and PF DIN Mono, designed to be the ideal font for programming; it supports programming ligatures and over 2000 latin, greek, cyrillic, phonetic and PowerLine glyphs
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (included in package [jre](https://aur.archlinux.org/packages/jre/))
*   [Menlo](https://en.wikipedia.org/wiki/Menlo_(typeface) (derivative: [ttf-meslo](https://aur.archlinux.org/packages/ttf-meslo/)) - default monospaced font of OS X
*   [Monaco](https://en.wikipedia.org/wiki/Monaco_(typeface) ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)) - proprietary font designed by Apple for OS X
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))
*   [Mononoki](https://madmalik.github.io/mononoki) ([ttf-mononoki](https://aur.archlinux.org/packages/ttf-mononoki/))
*   [Source Code Pro](https://en.wikipedia.org/wiki/Source_Code_Pro "wikipedia:Source Code Pro") ([adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

Relevant websites:

*   [Dan Benjamin's Top 10 Programming Fonts](http://hivelogic.com/articles/top-10-programming-fonts).
*   [Trevor Lowing's font list](http://www.lowing.org/fonts/)
*   [Slant: What are the best programming fonts?](https://www.slant.co/topics/67/~what-are-the-best-programming-fonts)
*   [Stack Overflow: Recommended fonts for programming](https://stackoverflow.com/questions/4689/recommended-fonts-for-programming)

#### Sans-serif

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/))
*   [FreeSans](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)) - Unicode
*   [Inter UI](https://github.com/rsms/inter) ([inter-font](https://www.archlinux.org/packages/?name=inter-font)) – designed for user interfaces
*   [Jost*](https://indestructibletype.com/Jost.html) ([otf-jost](https://aur.archlinux.org/packages/otf-jost/)) - An open-source typeface based on [Futura](https://en.wikipedia.org/wiki/Futura_(typeface) "wikipedia:Futura (typeface)")
*   [Linux Biolinum](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) – free substitute for Times New Roman
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - 3 major variations: normal, narrow, and caption - Unicode: Latin, Cyrillic
*   [Source Sans Pro](https://en.wikipedia.org/wiki/Source_Sans_Pro "wikipedia:Source Sans Pro") ([adobe-source-sans-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-sans-pro-fonts))
*   [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))

#### Serif

*   [Bodoni*](https://indestructibletype.com/Bodoni.html) ([otf-bodoni](https://aur.archlinux.org/packages/otf-bodoni/)) - An open-source [Bodoni](https://en.wikipedia.org/wiki/Bodoni "wikipedia:Bodoni") revival
*   [EB Garamond](https://github.com/octaviopardo/EBGaramond12) ([ebgaramond-otf](https://aur.archlinux.org/packages/ebgaramond-otf/)) - An open-source [Garamond](https://en.wikipedia.org/wiki/Garamond "wikipedia:Garamond") revival
*   [FreeSerif](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)) - Unicode
*   [Gentium](https://en.wikipedia.org/wiki/Gentium "wikipedia:Gentium") ([gentium-plus-font](https://www.archlinux.org/packages/?name=gentium-plus-font)) - Unicode: Latin, Greek, Cyrillic, Phonetic Alphabet
*   [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode: Latin, Greek, Cyrillic, Hebrew

#### Unsorted

*   [ttf-cheapskate](https://aur.archlinux.org/packages/ttf-cheapskate/) - Font collection from *dustismo.com*
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) - Junius font containing almost complete medieval latin script glyphs
*   [ttf-mph-2b-damase](https://aur.archlinux.org/packages/ttf-mph-2b-damase/) - Covers full plane 1 and several scripts
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) - IBM Courier and Adobe Utopia sets of [PostScript fonts](https://en.wikipedia.org/wiki/PostScript_fonts "wikipedia:PostScript fonts")
*   [all-repository-fonts](https://aur.archlinux.org/packages/all-repository-fonts/) - Meta package for all fonts in the official repositories.
*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) - a huge collection of free fonts (including Ubuntu, Inconsolata, Roboto, etc.) - Note: Your font dialog might get very long as >100 fonts will be added.

### Non-latin scripts

#### Ancient Scripts

*   [ttf-ancient-fonts](https://aur.archlinux.org/packages/ttf-ancient-fonts/) - Font containing Unicode symbols for Aegean, Egyptian, Cuneiform, Anatolian, Maya, and Analecta scripts

#### Arabic

*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/) - A classical Arabic typeface in Naskh style poineered by Amiria Press
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/) - Collection of free Arabic fonts
*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - Fonts by King Fahd Glorious Quran Printing Complex in al-Madinah al-Munawwarah
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - Unicode Arabic font from [SIL](https://en.wikipedia.org/wiki/SIL_International "wikipedia:SIL International")
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - Unicode Arabic font from SIL (Alternative for Traditional Arabic font)

#### Braille

*   [ttf-ubraille](https://aur.archlinux.org/packages/ttf-ubraille/) - Font containing Unicode symbols for *braille*

#### Chinese, Japanese, Korean, Vietnamese

##### Pan-CJK

*   Adobe Source Han fonts - Large collection of fonts which comprehensively support Simplified Chinese, Traditional Chinese, Japanese, and Korean, with a consistent design and look.
    *   [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) - Sans fonts
    *   [adobe-source-han-serif-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-otc-fonts) - Serif fonts
*   [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) - Large collection of fonts which comprehensively support Simplified Chinese, Traditional Chinese, Japanese, and Korean, with a consistent design and look. It is currently a rebadged version of [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts).

##### Chinese

*   adobe source han fonts
    *   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts) - Simplified Chinese OpenType/CFF Sans fonts
    *   [adobe-source-han-sans-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-tw-fonts) - Traditional Chinese OpenType/CFF Sans fonts
    *   [adobe-source-han-serif-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-cn-fonts) - Simplified Chinese OpenType/CFF Serif fonts
    *   [adobe-source-han-serif-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-tw-fonts) - Traditional Chinese OpenType/CFF Serif fonts
*   noto Chinese fonts
    *   [noto-fonts-sc](https://aur.archlinux.org/packages/noto-fonts-sc/) - Noto CJK-SC fonts for Simplified Chinese
    *   [noto-fonts-tc](https://aur.archlinux.org/packages/noto-fonts-tc/) - Noto CJK-TC fonts for Traditional Chinese
*   wqy fonts
    *   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - WenQuanYi Micro Hei font family (also known as Hei, Gothic or Dotum) is a sans-serif style derived from Droid Sans Fallback, it offers high quality CJK outline font and it is extremely compact (~5M).
    *   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - Hei Ti Style (sans-serif) Chinese Outline font embedded with bitmapped Song Ti (also supporting Japanese (partial) and Korean characters).
    *   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - Bitmapped Song Ti (serif) Chinese font.
*   arphic fonts
    *   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - *Kaiti* (brush stroke) Unicode font (enabling anti-aliasing is suggested)
    *   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - *Mingti* (printed) Unicode font
*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - *New Sung* font, previously is ttf-fireflysung package
*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Chinese and Vietnamese ttf fonts
*   Standart fonts of the Republic of China ministry of education in Taiwan
    *   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/) - Kai and Song traditional Chinese font from the Ministry of Education of Taiwan
    *   [ttf-twcns-fonts](https://aur.archlinux.org/packages/ttf-twcns-fonts/) Chinese TrueType fonts by Ministry of Education of Taiwan government, support CNS11643 standard, including Kai and Sung fontface.
*   Windows Chinese fonts
    *   [ttf-ms-win8-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win8-zh_cn/) - windows8 simple Chinese fonts。
    *   [ttf-ms-win8-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win8-zh_tw/) - windows8 traditional Chinese fonts。
    *   [ttf-ms-win10-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win10-zh_cn/) - windows10 simple Chinese fonts。
    *   [ttf-ms-win10-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win10-zh_tw/) - windows10 traditional Chinese fonts。
*   [ttf-i.bming](https://aur.archlinux.org/packages/ttf-i.bming/) - CJK serif font that emphasis on an old-style typeface.

##### Japanese

*   [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) - Japanese OpenType/CFF fonts
*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - Formal style Japanese Gothic (sans-serif) and Mincho (serif) fonts set; one of the highest quality open source font. Default of openSUSE-ja.
*   [ttf-hanazono](https://www.archlinux.org/packages/?name=ttf-hanazono) - A free Japanese kanji font, style Mincho (serif).
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - Japanese free TrueType font. This is outdated and not maintained any more, but may be defined as a fallback font on several environments.
*   [ttf-koruri](https://aur.archlinux.org/packages/ttf-koruri/) - Japanese TrueType font obtained by mixing [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) and Open Sans
*   [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - Japanese fonts to show [2channel Shift JIS art](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art") properly.
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) - Modern Gothic style Japanese outline fonts. It includes all of Japanese Hiragana/Katakana, Basic Latin, Latin-1 Supplement, Latin Extended-A, IPA Extensions and most of Japanese Kanji, Greek, Cyrillic, Vietnamese with 7 weights (proportional) or 5 weights (monospace).
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - Japanese Gothic fonts. Default of Debian/Fedora/Vine Linux

##### Korean

*   [adobe-source-han-sans-kr-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-kr-fonts) - Korean OpenType/CFF fonts
*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - Collection of Korean TrueType fonts
*   [spoqa-han-sans](https://aur.archlinux.org/packages/spoqa-han-sans/) - Source Han Sans customized by Spoqa
*   [ttf-d2coding](https://aur.archlinux.org/packages/ttf-d2coding/) - D2Coding fixed width TrueType font made by Naver
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) - Nanum series TrueType fonts
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) - Nanum series fixed width TrueType fonts
*   [ttf-kopub](https://aur.archlinux.org/packages/ttf-kopub/)/[otf-kopub](https://aur.archlinux.org/packages/otf-kopub/) - Korean TrueType/OpenType fonts by Korea Publisher Society
*   [ttf-kopubworld](https://aur.archlinux.org/packages/ttf-kopubworld/)/[otf-kopubworld](https://aur.archlinux.org/packages/otf-kopubworld/) - Multilingual (Korean, Yethangul, Chinese extended, Japanese, Latin extended, Cyrillic, Arabic, Hebrew, Devanagari) TrueType/OpenType fonts by Korea Publisher Society
*   [ttf-unfonts-core-ibx](https://aur.archlinux.org/packages/ttf-unfonts-core-ibx/) - A collection of Korean TrueType fonts by KLDP

##### Vietnamese

*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Vietnamese TrueType font for chữ Nôm characters

#### Cyrillic

See also [#Latin script](#Latin_script).

*   [ttf-paratype](https://aur.archlinux.org/packages/ttf-paratype/) - Font family by ParaType: sans, serif, mono, extended cyrillic and latin, OFL license
*   [otf-russkopis](https://aur.archlinux.org/packages/otf-russkopis/) - A free OpenType cursive font for Cyrillic script

#### Greek

Almost all Unicode fonts contain the Greek character set (polytonic included). Some additional font packages, which might not contain the complete Unicode set but utilize high quality Greek (and Latin, of course) typefaces are:

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/) - Selection of OpenType fonts from the Greek Font Society
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/) - Professional TrueType fonts from Magenta

#### Hebrew

*   [opensiddur-hebrew-fonts](https://aur.archlinux.org/packages/opensiddur-hebrew-fonts/) - Large collection of Open-source licensed Hebrew fonts. There are also few Latin, Greek, Cyrillic, Arabic, and Amharic.
*   [culmus](https://aur.archlinux.org/packages/culmus/) - Nice collection of free Hebrew fonts

#### Indic

*   [ttf-freebanglafont](https://aur.archlinux.org/packages/ttf-freebanglafont/) - Font for Bangla
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - Indic OpenType Fonts collection (containing ttf-freebanglafont), provides the character [U+0CA0](http://www.fileformat.info/info/unicode/char/ca0/index.htm) "ಠ"
*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/) - Indic TrueType fonts from Fedora Project (containing Oriya Fonts and more)
*   [ttf-devanagarifonts](https://aur.archlinux.org/packages/ttf-devanagarifonts/) - Devanagari TrueType fonts (contains 283 fonts)
*   [ttf-gurmukhi-fonts_sikhnet](https://aur.archlinux.org/packages/ttf-gurmukhi-fonts_sikhnet/) - TrueType Gurmukhi fonts (gurbaniwebthick,prabhki)
*   [ttf-gurmukhi_punjabi](https://aur.archlinux.org/packages/ttf-gurmukhi_punjabi/) - TTF Gurmukhi / Punjabi (contains 252 fonts)
*   [ttf-gujrati-fonts](https://aur.archlinux.org/packages/ttf-gujrati-fonts/) - TTF Gujarati fonts (Avantika,Gopika,Shree768)
*   [ttf-kannada-font](https://aur.archlinux.org/packages/ttf-kannada-font/) - Kannada, the language of Karnataka state in India
*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - Sinhala Unicode font
*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - Tamil Unicode fonts
*   [ttf-urdufonts](https://aur.archlinux.org/packages/ttf-urdufonts/) - Urdu fonts (Jameel Noori Nastaleeq (+kasheeda), Nafees Web Naskh, PDMS Saleem Quran Font) and font configuration to set Jameel Noori Nastaleeq as default font for Urdu
*   [fonts-smc-malayalam](https://aur.archlinux.org/packages/fonts-smc-malayalam/) - Malayalam Unicode Fonts released by 'Swathanthra Malayalam Computing' (contains 11 fonts).

#### Khmer

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - Font covering glyphs for Khmer language
*   [Hanuman](https://www.google.com/fonts/specimen/Hanuman) ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

#### Mongolic and Tungusic

*   [ttf-abkai](https://aur.archlinux.org/packages/ttf-abkai/) - Fonts for Sibe, Manchu and Daur scripts (incomplete, currently in development)

#### Persian

*   [persian-fonts](https://aur.archlinux.org/packages/persian-fonts/) - Meta package for installing all Persian fonts in AUR.
*   [borna-fonts](https://aur.archlinux.org/packages/borna-fonts/) - Borna Rayaneh Co. Persian B font series.
*   [iran-nastaliq-fonts](https://aur.archlinux.org/packages/iran-nastaliq-fonts/) - A free Unicode calligraphic Persian font.
*   [iranian-fonts](https://aur.archlinux.org/packages/iranian-fonts/) - Iranian-Sans and Iranian-Serif Persian font family.
*   [ir-standard-fonts](https://aur.archlinux.org/packages/ir-standard-fonts/) - Iran Supreme Council of Information and Communication Technology (SCICT) standard Persian fonts.
*   [persian-hm-ftx-fonts](https://aur.archlinux.org/packages/persian-hm-ftx-fonts/) - A Persian font series derived from X Series 2, Metafont and FarsiTeX fonts with Kashida feature.
*   [persian-hm-xs2-fonts](https://aur.archlinux.org/packages/persian-hm-xs2-fonts/) - A Persian font series derived from X Series 2 fonts with Kashida feature.
*   [sina-fonts](https://aur.archlinux.org/packages/sina-fonts/) - Sina Pardazesh Co. Persian font series.
*   [gandom-fonts](https://aur.archlinux.org/packages/gandom-fonts/), [parastoo-fonts](https://aur.archlinux.org/packages/parastoo-fonts/), [sahel-fonts](https://aur.archlinux.org/packages/sahel-fonts/), [samim-fonts](https://aur.archlinux.org/packages/samim-fonts/), [shabnam-fonts](https://aur.archlinux.org/packages/shabnam-fonts/), [tanha-fonts](https://aur.archlinux.org/packages/tanha-fonts/), [vazir-fonts](https://aur.archlinux.org/packages/vazir-fonts/), [vazir-code-fonts](https://aur.archlinux.org/packages/vazir-code-fonts/) - Beautiful Persian fonts made by Saber RastiKerdar.
*   [ttf-yas](https://aur.archlinux.org/packages/ttf-yas/) - The Yas Persian font series (with **hollow zero**).
*   [ttf-x2](https://aur.archlinux.org/packages/ttf-x2/) - Free fonts with support for Persian, Arabic, Urdu, Pashto, Dari, Uzbek, Kurdish, Uighur, old Turkish (Ottoman) and modern Turkish (Roman).

#### Tai–Kadai

*   [fonts-tlwg](https://aur.archlinux.org/packages/fonts-tlwg/) - Collection of scalable Thai fonts
*   [ttf-lao](https://aur.archlinux.org/packages/ttf-lao/) - Lao TTF font (Phetsarath_OT)
*   [ttf-lao-fonts](https://aur.archlinux.org/packages/ttf-lao-fonts/) - Lao TTF fonts, both Unicode and non-Unicode for Windows

#### Tibeto-Burman

*   [ttf-tibetan-machine](https://www.archlinux.org/packages/?name=ttf-tibetan-machine) - Tibetan Machine TTFont
*   [ttf-myanmar-fonts](https://aur.archlinux.org/packages/ttf-myanmar-fonts/) - 121 Fonts from myordbok.com

### Emoji and symbols

A section of the Unicode standard is designated for pictographic characters called "emoji".

*   [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji) - Google's own emoji font, like on Android or Google Hangouts.
*   [ttf-symbola](https://aur.archlinux.org/packages/ttf-symbola/) - provides many Unicode symbols, including emoji, in outline style.
*   [ttf-joypixels](https://www.archlinux.org/packages/?name=ttf-joypixels) - Unicode 12 compliant Emoji font (formerly EmojiOne)
*   [ttf-twemoji-color](https://aur.archlinux.org/packages/ttf-twemoji-color/) - Twitter's open-sourced emoji glyphs.

[Kaomoji](https://en.wikipedia.org/wiki/Emoticon#Japanese_style "wikipedia:Emoticon") are sometimes referred to as "Japanese emoticons" and are composed of characters from various character sets, including CJK and Indic fonts. For example, the following set of packages covers most of existing kaomoji: [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts), [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming), and [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf).

**Note:** [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) implements a subset of emojis in outline style, which leads to emoji being rendered in a mix of styles when installed at the same time as any of the above.

### Math

*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Mathematica fonts by Wolfram Research, Inc.
*   [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) and [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra) contain many math fonts such as Latin Modern Math and [STIX Fonts](https://en.wikipedia.org/wiki/STIX_Fonts_project "wikipedia:STIX Fonts project"). See [TeX Live#Making fonts available to Fontconfig](/index.php/TeX_Live#Making_fonts_available_to_Fontconfig "TeX Live") for configuration.
*   [otf-stix](https://aur.archlinux.org/packages/otf-stix/) - A standalone, more recent version of STIX
*   [otf-latin-modern](https://www.archlinux.org/packages/?name=otf-latin-modern), [otf-latinmodern-math](https://www.archlinux.org/packages/?name=otf-latinmodern-math) - Improved version of Computer Modern fonts as used in LaTeX
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/), [otf-cm-unicode](https://aur.archlinux.org/packages/otf-cm-unicode/) - [Computer Modern](https://en.wikipedia.org/wiki/Computer_Modern "wikipedia:Computer Modern") (of TeX fame)
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/) - MathType fonts

### Other operating system fonts

*   [ttf-mac-fonts](https://aur.archlinux.org/packages/ttf-mac-fonts/) - Apple MacOS TrueType fonts

See [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts"), which lists available alternatives for [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts").

## Fallback font order with X11

Fontconfig automatically chooses a font that matches the current requirement. That is to say, if one is looking at a window containing English and Chinese for example, it will switch to another font for the Chinese text if the default one does not support it.

Fontconfig lets every user configure the order they want via `$XDG_CONFIG_HOME/fontconfig/fonts.conf`. If you want a particular Chinese font to be selected after your favorite Serif font, your file would look like this:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<alias>
   <family>serif</family>
   <prefer>
     <family>Your favorite Latin Serif font name</family>
     <family>Your Chinese font name</family>
   </prefer>
 </alias>
</fontconfig>

```

**Tip:** If you use a Chinese locale, set `LC_LANG` to `und` to make this work. Otherwise both English and Chinese text will be rendered in the Chinese font.

You can add a section for sans-serif and monospace as well. For more information, have a look at the fontconfig manual.

See also [Font configuration#Replace or set default fonts](/index.php/Font_configuration#Replace_or_set_default_fonts "Font configuration").

## Font alias

There are several font aliases which represent other fonts in order that applications may use similar fonts. The most common aliases are: `serif` for a font of the serif type (e.g. DejaVu Serif); `sans-serif` for a font of the sans-serif type (e.g. DejaVu Sans); and `monospace` for a monospaced font (e.g. DejaVu Sans Mono). However, the fonts which these aliases represent may vary and the relationship is often not shown in font management tools, such as those found in [KDE](/index.php/KDE "KDE") and other [desktop environments](/index.php/Desktop_environments "Desktop environments").

To reverse an alias and find which font it is representing, run:

 `$ fc-match monospace` 
```
DejaVuSansMono.ttf: "DejaVu Sans Mono" "Book"

```

In this case, `DejaVuSansMono.ttf` is the font represented by the monospace alias.

## Tips and tricks

### List all installed fonts

You can use the following command to list all installed Fontconfig fonts that are available on your system.

```
$ fc-list

```

### List installed fonts for a particular language

Applications and browsers select and display fonts depending upon fontconfig preferences and available font glyph for Unicode text. To list installed fonts for a particular language, issue a command `fc-list :lang="*two letter language code*"`. For instance, to list installed Arabic fonts or fonts supporting Arabic glyph:

 `$ fc-list -f '%{file}
' :lang=ar` 
```
/usr/share/fonts/TTF/FreeMono.ttf
/usr/share/fonts/TTF/DejaVuSansCondensed.ttf
/usr/share/fonts/truetype/custom/DroidKufi-Bold.ttf
/usr/share/fonts/TTF/DejaVuSansMono.ttf
/usr/share/fonts/TTF/FreeSerif.ttf
```

### List installed fonts for a particular Unicode character

To search for monospace fonts supporting a particular Unicode codepoint:

```
$ fc-match -s monospace:charset=1F4A9

```

### Set terminal font on-the-fly

For terminal emulators that use [X resources](/index.php/X_resources "X resources"), e.g. [xterm](/index.php/Xterm "Xterm") or [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode"), fonts can be set by using escape sequences. Specifically, `echo -e "\033]710;$font\007"` to change the normal font (`*font` in `~/.Xresources`), and replace `710` with `711`, `712`, and `713` to change the `*boldFont`, `*italicFont`, and `*boldItalicFont`, respectively.

`$font` uses the same syntax as in `~/.Xresources` and can be anything the terminal emulator will support. (Example: `xft:dejavu sans mono:size=9`)

### Application-specific font cache

Matplotlib ([python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib) or [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)) uses its own font cache, so after updating fonts, be sure to remove `~/.matplotlib/fontList.cache`, `~/.cache/matplotlib/fontList.cache`, `~/.sage/matplotlib-1.2.1/fontList.cache`, etc. so it will regenerate its cache and find the new fonts [[1]](http://matplotlib.1069221.n5.nabble.com/getting-matplotlib-to-recognize-a-new-font-td40500.html).

### Force color emoji

If the default font includes some emoji characters, they will be used over the characters provided by a dedicated emoji font, resulting in inconsistent display. To override this behavior, the following fontconfig snippet can be added to `/etc/fonts/conf.d/90-emoji.conf`, using the [ttf-joypixels](https://www.archlinux.org/packages/?name=ttf-joypixels) font as an example:

```
<fontconfig>
    <match>
        <test name="family">
            <string>sans-serif</string>
        </test>
        <edit mode="prepend" name="family" binding="strong">
            <string>JoyPixels</string>
        </edit>
    </match>
    <match>
        <test name="family">
            <string>serif</string>
        </test>
        <edit mode="prepend" name="family" binding="strong">
            <string>JoyPixels</string>
        </edit>
    </match>
</fontconfig>

```

## See also

*   [State of Text Rendering](http://behdad.org/text/)
*   [Font Library](https://fontlibrary.org/en) - Fonts under Free licenses
*   [Fonts on screenshots.debian.net](https://screenshots.debian.net/packages?search=fonts&show=with)