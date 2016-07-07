From [Wikipedia](https://en.wikipedia.org/wiki/Computer_font "wikipedia:Computer font"): "A computer font (or font) is an electronic data file containing a set of glyphs, characters, or symbols such as dingbats."

Note that certain font licenses may impose some legal limitations.

## Contents

*   [1 Font formats](#Font_formats)
    *   [1.1 Common extensions](#Common_extensions)
    *   [1.2 Other formats](#Other_formats)
*   [2 Installation](#Installation)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 Creating a package](#Creating_a_package)
    *   [2.3 Manual installation](#Manual_installation)
    *   [2.4 Older applications](#Older_applications)
    *   [2.5 Pango Warnings](#Pango_Warnings)
*   [3 Console fonts](#Console_fonts)
    *   [3.1 Previewing and testing](#Previewing_and_testing)
    *   [3.2 Persistent configuration](#Persistent_configuration)
*   [4 Font packages](#Font_packages)
    *   [4.1 Ancient Scripts](#Ancient_Scripts)
    *   [4.2 Braille](#Braille)
    *   [4.3 Emoji and symbols](#Emoji_and_symbols)
        *   [4.3.1 Arabic & Urdu](#Arabic_.26_Urdu)
        *   [4.3.2 Burmese](#Burmese)
        *   [4.3.3 Chinese, Japanese, Korean, Vietnamese](#Chinese.2C_Japanese.2C_Korean.2C_Vietnamese)
            *   [4.3.3.1 Pan-CJK](#Pan-CJK)
            *   [4.3.3.2 (Mainly) Chinese](#.28Mainly.29_Chinese)
            *   [4.3.3.3 Japanese](#Japanese)
            *   [4.3.3.4 Korean](#Korean)
        *   [4.3.4 Cyrillic](#Cyrillic)
        *   [4.3.5 Greek](#Greek)
        *   [4.3.6 Hebrew](#Hebrew)
        *   [4.3.7 Indic](#Indic)
        *   [4.3.8 Khmer](#Khmer)
        *   [4.3.9 Lao](#Lao)
        *   [4.3.10 Persian](#Persian)
        *   [4.3.11 Sinhala](#Sinhala)
        *   [4.3.12 Thai](#Thai)
        *   [4.3.13 Tibetan](#Tibetan)
    *   [4.4 Math](#Math)
    *   [4.5 Metric-compatible fonts](#Metric-compatible_fonts)
    *   [4.6 Apple OS X fonts](#Apple_OS_X_fonts)
    *   [4.7 Monospaced](#Monospaced)
        *   [4.7.1 TrueType](#TrueType)
        *   [4.7.2 Bitmap](#Bitmap)
    *   [4.8 Sans-serif](#Sans-serif)
    *   [4.9 Script](#Script)
    *   [4.10 Serif](#Serif)
    *   [4.11 Unsorted](#Unsorted)
*   [5 Fallback font order with X11](#Fallback_font_order_with_X11)
*   [6 Font alias](#Font_alias)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 List all installed fonts](#List_all_installed_fonts)
    *   [7.2 Lists installed fonts for a particular language](#Lists_installed_fonts_for_a_particular_language)
    *   [7.3 Set terminal font on-the-fly](#Set_terminal_font_on-the-fly)
    *   [7.4 Application-specific font cache](#Application-specific_font_cache)
*   [8 See also](#See_also)

## Font formats

Most computer fonts used today are in either *bitmap* or *outline* data formats.

	Bitmap fonts

	Consist of a matrix of dots or pixels representing the image of each glyph in each face and size.

	Outline or *vector* fonts

	Use Bézier curves, drawing instructions and mathematical formulae to describe each glyph, which make the character outlines scalable to any size.

### Common extensions

*   `bdf` and `bdf.gz` – bitmap fonts, *b*itmap *d*istribution *f*ormat and gzip compressed `bdf`
*   `pcf` and `pcf.gz` – bitmaps, *p*ortable *c*ompiled *f*ont and gzip compressed `pcf`
*   `psf`, `psfu`, `psf.gz` and `psfu.gz` – bitmaps, *P*C *s*creen *f*ont, *P*C *s*creen *f*ont *U*nicode and the gzipped versions (not compatible with X.Org)
*   `pfa` and `pfb` – outline fonts, *P*ostScript *f*ont *A*SCII and *P*ostScript *f*ont *b*inary. PostScript fonts carry built-in printer instructions.
*   `ttf` – outline, *T*rue*T*ype *f*ont. Originally designed as a replacement for the PostScript fonts.
*   `otf` – outline, *O*pen*T*ype *f*ont. TrueType with PostScript typographic instructions.

For most purposes, the technical differences between TrueType and OpenType can be ignored, some fonts with a `ttf` extension are actually OpenType fonts.

### Other formats

The typesetting application, *TeX,* and its companion font software, *Metafont,* render characters using their own methods. Some of the file extensions used for fonts by these two programs are `*pk`, `*gf`, `mf` and `vf`.

*FontForge,* a font editing application, can store fonts in its native text-based format, `sfd`, *s*pline *f*ont *d*atabase.

The [SVG](http://www.w3.org/TR/SVG/fonts.html) format also has its own font description method.

## Installation

There are various methods for installing fonts.

### Pacman

Fonts and font collections in the enabled repositories can be installed using [pacman](/index.php/Pacman "Pacman"). Available fonts may be found by using:

```
$ pacman -Ss font

```

Or to search for `ttf` fonts only:

```
$ pacman -Ss ttf

```

### Creating a package

You should give pacman the ability to manage your fonts, which is done by creating an Arch package. These can also be shared with the community in the [AUR](/index.php/AUR "AUR"). Here is an example of how to create a basic package. To learn more about building packages, read [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

The family name of a font file can be aquired with the use of `fc-query` for example: `fc-query -f '%{family[0]}
' /path/to/file`. The formatting is described in the FcPatternFormat(3) manual.

 `PKGBUILD` 
```
pkgname=fontname-fonts
pkgver=1.0
pkgrel=1
pkgdesc="Some description"
arch=(any)
depends=(fontconfig xorg-font-utils)
source=("http://someurl.org/$pkgname.tar.bz2")
install=$pkgname.install

package() {
  install -Dm644 $pkgname/font.otf "$pkgdir"/usr/share/fonts/family_name/font.otf
  install -Dm644 $pkgname/font_bold.otf "$pkgdir"/usr/share/fonts/family_name/font_bold.otf
}

```
 `fontname-fonts.install` 
```
post_install() {
  fc-cache -s
}

post_upgrade() {
  post_install
}

post_remove() {
  post_install
}

```

### Manual installation

The recommended way of adding fonts that are not in the repositories to your system is described in [#Creating a package](#Creating_a_package). This gives pacman the ability to remove or update them at a later time. Fonts can alternately be installed manually as well.

To install fonts system-wide (available for all users), move the folder to the `/usr/share/fonts/` directory. The files need to be readable by every user, use [chmod](/index.php/Chmod "Chmod") to set the correct permissions (i.e. at least `0444` for files and `0555` for directories). To install fonts for only a single user, use `~/.local/share/fonts` (`~/.fonts/` is now deprecated).

For Xserver to load fonts directly (as opposed to the use of a *font server*) the directory for your newly added font must be added with a FontPath entry. This entry is located in the *Files* section [of your Xorg configuration file](/index.php/Xorg#Configuration "Xorg") (e.g. `/etc/X11/xorg.conf` or `/etc/xorg.conf`). See [#Older applications](#Older_applications) for more detail.

Then update the fontconfig font cache: (usually unnecessary as software using the fontconfig library do this.)

```
$ fc-cache

```

### Older applications

With older applications that do not support fontconfig (e.g. GTK+ 1.x applications, and `xfontsel`) the index will need to be created in the font directory:

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
$ for dir in * ; do if [  -d  "$dir"  ]; then cd "$dir";xset +fp "$PWD" ;mkfontscale; mkfontdir;cd .. ;fi; done && xset fp rehash

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

```
# fc-cache
/usr/share/fonts: caching, new cache contents: 0 fonts, 3 dirs
/usr/share/fonts/TTF: caching, new cache contents: 16 fonts, 0 dirs
/usr/share/fonts/encodings: caching, new cache contents: 0 fonts, 1 dirs
/usr/share/fonts/encodings/large: caching, new cache contents: 0 fonts, 0 dirs
/usr/share/fonts/util: caching, new cache contents: 0 fonts, 0 dirs
/var/cache/fontconfig: cleaning cache directory
fc-cache: succeeded

```

You can test for a default font being set like so:

```
# fc-match
LiberationMono-Regular.ttf: "Liberation Mono" "Regular"

```

## Console fonts

**Note:** This section is about the [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"). For alternative console solutions offering more features (full Unicode fonts, modern graphics adapters etc.), see [fbterm](/index.php/Fbterm "Fbterm"), [KMSCON](/index.php/KMSCON "KMSCON") or similar projects.

By default, the [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") uses the kernel built-in font with a [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437") character set, but this can be easily changed.

The [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") uses UTF-8 encoding by default, but because the standard VGA-compatible framebuffer is used, a console font is limited to either a standard 256, or 512 glyphs. If the font has more than 256 glyphs, the number of colours is reduced from 16 to 8\. In order to assign correct symbol to be displayed to the given Unicode value, a special translation map, often called *unimap*, is needed. Nowadays most of the console fonts have the *unimap* built-in, historically it had to be loaded separately.

The [kbd](https://www.archlinux.org/packages/?name=kbd) package provides tools to change virtual console font and font mapping. Available fonts are saved in the `/usr/share/kbd/consolefonts/` directory, those ending with *.psfu* or *.psfu.gz* have a Unicode translation map built-in.

Keymaps, the connection between the key pressed and the character used by the computer, are found in the subdirectories of `/usr/share/kbd/keymaps/`, see [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") for details.

**Note:** Replacing the font can cause issues with programs that expect a standard VGA-style font, such as those using line drawing graphics.

### Previewing and testing

**Tip:** An organized library of images for previewing is available: [Linux console fonts screenshots](http://alexandre.deverteuil.net/pages/consolefonts/).

The available glyphs or letters in the font can also be viewed as a table with using *showconsolefont*:

```
$ showconsolefont

```

The *setfont* utility may be used to temporarily change the font, so that the user can consider its permanent use. Just pass the name of the font (they are located in `/usr/share/kbd/consolefonts/`). For example:

```
$ setfont lat2-16 -m 8859-2

```

Note that the font name is case-sensitive, so type it *exactly* as you see it. If the newly changed font is not suitable, a return to the default font with the following command (even if the console display is totally unreadable, this command will still work, just type the command "blindly"):

```
$ setfont

```

**Note:** *setfont* only works on the console currently being used. Any other consoles, active or inactive, remain unaffected.

### Persistent configuration

The `FONT` variable in `/etc/vconsole.conf` is used to set the font at boot, persistently for all consoles. See `man 5 vconsole.conf` for details.

For displaying characters such as *Č, ž, đ, š* or *Ł, ę, ą, ś* using the font `lat2-16.psfu.gz`:

 `/etc/vconsole.conf` 
```
...
FONT=lat2-16
FONT_MAP=8859-2
```

It means that second part of ISO/IEC 8859 characters are used with size 16\. You can change font size using other values (e.g. `lat2-08`). For the regions determined by 8859 specification, look at the [Wikipedia table](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_Parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859").

To use the specified font in early userspace, use the `consolefont` hook in `/etc/mkinitcpio.conf`. See [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") for more information.

If the fonts seems to not change on boot, or change only temporarily, it is most likely that they got reset when graphics driver was initialized and console was switched to framebuffer. To avoid this, load your graphics driver earlier. See for example [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"), [[2]](https://bbs.archlinux.org/viewtopic.php?id=145765) or other ways to setup your framebuffer before `/etc/vconsole.conf` is applied.

## Font packages

This is a selective list that includes many font packages from the [AUR](/index.php/AUR "AUR") along with those in the official repositories. Fonts are tagged "Unicode" if they have wide Unicode support, see the project or Wikipedia pages for detail.

Github user Ternstor has created a python script that generates HTML documents with PNG images of all the fonts in the AUR and the official repositories: [[3]](https://github.com/ternstor/distrofonts/blob/master/archfonts.py).

### Ancient Scripts

*   [ttf-ancient-fonts](https://aur.archlinux.org/packages/ttf-ancient-fonts/) - Font containing Unicode symbols for Aegean, Egyptian, Cuneiform, Anatolian, Maya, and Analecta scripts

### Braille

*   [ttf-ubraille](https://www.archlinux.org/packages/?name=ttf-ubraille) - Font containing Unicode symbols for *braille*

### Emoji and symbols

A section of the Unicode standard is designated for picotographic characters called "emoji".

*   [emojione-color-font](https://aur.archlinux.org/packages/emojione-color-font/) - a complete, independent, open-source emoji set focused on design correctness
*   [twemoji-color-font](https://aur.archlinux.org/packages/twemoji-color-font/) - Twitter's open-sourced emoji glyphs
*   [ttf-symbola](https://www.archlinux.org/packages/?name=ttf-symbola) - provides many Unicode symbols, including emoji, in outline style
*   [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji) - Google's own emoji font, like on Android or Google Hangouts. Some newer additions to Unicode appear to render poorly with Noto fonts.

[Kaomoji](https://en.wikipedia.org/wiki/Emoticon#Japanese_style "wikipedia:Emoticon") are sometimes referred to as "Japanese emoticons" and are composed of characters from various character sets, including CJK and Indic fonts. For example, the following set of packages covers most of existing kaomoji: [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming), and [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf).

#### Arabic & Urdu

*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/) - A classical Arabic typeface in Naskh style poineered by Amiria Press
*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - Fonts by King Fahd Glorious Quran Printing Complex in al-Madinah al-Munawwarah
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/) - Collection of free Arabic fonts
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - Unicode Arabic font from SIL
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - Unicode Arabic font from SIL
*   [ttf-urdufonts](https://aur.archlinux.org/packages/ttf-urdufonts/) - Urdu fonts (Jameel Noori Nastaleeq (+kasheeda), Nafees Web Naskh, PDMS Saleem Quran Font) and font configuration to set Jameel Noori Nastaleeq as default font for Urdu

#### Burmese

*   [ttf-my-paduk](https://aur.archlinux.org/packages/ttf-my-paduk/) - Padauk font for Myanmar/Birmania
*   [ttf-myanmar-fonts](https://aur.archlinux.org/packages/ttf-myanmar-fonts/) - 121 Fonts from myordbok.com

#### Chinese, Japanese, Korean, Vietnamese

##### Pan-CJK

*   [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) - Large collection of fonts which comprehensively support Simplified Chinese, Traditional Chinese, Japanese, and Korean, with a consistent design and look. It is currently a rebadged version of [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts).
*   [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) - Large collection of fonts which comprehensively support Simplified Chinese, Traditional Chinese, Japanese, and Korean, with a consistent design and look.

##### (Mainly) Chinese

*   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts) - Simplified Chinese OpenType/CFF fonts
*   [adobe-source-han-sans-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-tw-fonts) - Traditional Chinese OpenType/CFF fonts
*   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - A Sans-Serif style high quality CJKV outline font.
*   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - Hei Ti Style (sans-serif) Chinese Outline font embedded with bitmapped Song Ti (also supporting Japanese (partial) and Korean characters).
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - *Kaiti* (brush stroke) Unicode font (enabling anti-aliasing is suggested)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - *Mingti* (printed) Unicode font
*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - *New Sung* font, previously is ttf-fireflysung package
*   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - Bitmapped Song Ti (serif) Chinese font
*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Chinese and Vietnamese TrueType font
*   [ttf-i.bming](https://aur.archlinux.org/packages/ttf-i.bming/) - CJK serif font that emphasis on an old-style typeface
*   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/) - Kai and Song traditional Chinese font from the Ministry of Education of Taiwan

##### Japanese

*   [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) - Japanese OpenType/CFF fonts
*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - Formal style Japanese Gothic (sans-serif) and Mincho (serif) fonts set; one of the highest quality open source font. Default of openSUSE-ja.
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - Japanese free TrueType font. This is outdated and not maintained any more, but may be defined as a fallback font on several environments.
*   [ttf-hanazono](https://www.archlinux.org/packages/?name=ttf-hanazono) - A free Japanese kanji font, style Mincho (serif).
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - Japanese Gothic fonts. Default of Debian/Fedora/Vine Linux
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) - Modern Gothic style Japanese outline fonts. It includes all of Japanese Hiragana/Katakana, Basic Latin, Latin-1 Supplement, Latin Extended-A, IPA Extensions and most of Japanese Kanji, Greek, Cyrillic, Vietnamese with 7 weights (proportional) or 5 weights (monospace).
*   [ttf-koruri](https://aur.archlinux.org/packages/ttf-koruri/) - Japanese TrueType font obtained by mixing [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) and Open Sans
*   [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - Japanese fonts to show [2channel Shift JIS art](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art") properly.

##### Korean

*   [adobe-source-han-sans-kr-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-kr-fonts) - Korean OpenType/CFF fonts
*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - Collection of Korean TrueType fonts
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) - Nanum series TrueType fonts
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) - Nanum series fixed width TrueType fonts
*   [ttf-d2coding](https://aur.archlinux.org/packages/ttf-d2coding/) - D2Coding fixed width TrueType font made by Naver
*   [spoqa-han-sans](https://aur.archlinux.org/packages/spoqa-han-sans/) - Source Han Sans customized by Spoqa

#### Cyrillic

See also [#Monospaced](#Monospaced), [#Sans-serif](#Sans-serif) and [#Serif](#Serif).

*   [otf-russkopis](https://aur.archlinux.org/packages/otf-russkopis/) - A free OpenType cursive font for Cyrillic script
*   [ttf-paratype](https://aur.archlinux.org/packages/ttf-paratype/) - Font family by ParaType: sans, serif, mono, extended cyrillic and latin, OFL license

#### Greek

Almost all Unicode fonts contain the Greek character set (polytonic included). Some additional font packages, which might not contain the complete Unicode set but utilize high quality Greek (and Latin, of course) typefaces are:

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/) - Selection of OpenType fonts from the Greek Font Society
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/) - Professional TrueType fonts from Magenta

#### Hebrew

*   [culmus](https://aur.archlinux.org/packages/culmus/) - Nice collection of free Hebrew fonts

#### Indic

*   [ttf-freebanglafont](https://www.archlinux.org/packages/?name=ttf-freebanglafont) - Font for Bangla
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - Indic OpenType Fonts collection (containing ttf-freebanglafont)

	(This one contains a "look of disapproval" that might be more to your liking than the [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) one mentioned elsewhere in this document)

*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/) - Indic TrueType fonts from Fedora Project (containing Oriya Fonts and more)
*   [ttf-devanagarifonts](https://aur.archlinux.org/packages/ttf-devanagarifonts/) - Devanagari TrueType fonts (contains 283 fonts)
*   [ttf-gujrati-fonts](https://aur.archlinux.org/packages/ttf-gujrati-fonts/) - TTF Gujarati fonts (Avantika,Gopika,Shree768)
*   [ttf-gurmukhi-fonts_sikhnet](https://aur.archlinux.org/packages/ttf-gurmukhi-fonts_sikhnet/) - TrueType Gurmukhi fonts (gurbaniwebthick,prabhki)
*   [ttf-gurmukhi_punjabi](https://aur.archlinux.org/packages/ttf-gurmukhi_punjabi/) - TTF Gurmukhi / Punjabi (contains 252 fonts)
*   [ttf-kannada-font](https://aur.archlinux.org/packages/ttf-kannada-font/) - Kannada, the language of Karnataka state in India
*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - Tamil Unicode fonts

#### Khmer

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - Font covering glyphs for Khmer language
*   [Hanuman](https://www.google.com/fonts/specimen/Hanuman) ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

#### Lao

*   [ttf-lao](https://aur.archlinux.org/packages/ttf-lao/) - Lao TTF font (Phetsarath_OT)
*   [ttf-lao-fonts](https://aur.archlinux.org/packages/ttf-lao-fonts/) - Lao TTF fonts, both Unicode and non-Unicode for Windows

#### Persian

*   [ttf-irfonts](https://aur.archlinux.org/packages/ttf-irfonts/) - Iran Supreme Council of Information and Communication Technology (SCICT) standard Persian fonts series.
*   [ttf-borna](https://aur.archlinux.org/packages/ttf-borna/) - Borna Rayaneh Persian B font series.
*   [ttf-sina](https://aur.archlinux.org/packages/ttf-sina/) - Sina Pardazesh Persian font series.
*   [ttf-x2](https://aur.archlinux.org/packages/ttf-x2/) - Free fonts with support for Persian, Arabic, Urdu, Pashto, Dari, Uzbek, Kurdish, Uighur, old Turkish (Ottoman) and modern Turkish (Roman).
*   [ttf-iran-nastaliq](https://aur.archlinux.org/packages/ttf-iran-nastaliq/) - A free Unicode calligraphic Persian font created by Iran Supreme Council of Information and Communication Technology (SCICT).
*   [ttf-vazir](https://aur.archlinux.org/packages/ttf-vazir/), [ttf-samim](https://aur.archlinux.org/packages/ttf-samim/), [ttf-tanha](https://aur.archlinux.org/packages/ttf-tanha/), [ttf-shabnam](https://aur.archlinux.org/packages/ttf-shabnam/), [ttf-gandom](https://aur.archlinux.org/packages/ttf-gandom/), [ttf-parastoo](https://aur.archlinux.org/packages/ttf-parastoo/) - Beautiful Persian fonts made by Ali Rasti Kerdar.
*   [ttf-persian-hm-xs2](https://aur.archlinux.org/packages/ttf-persian-hm-xs2/) - An improved and corrected font series derived from [ttf-x2](https://aur.archlinux.org/packages/ttf-x2/) Persian font series with Kashida feature.
*   [ttf-persian-hm-ftx](https://aur.archlinux.org/packages/ttf-persian-hm-ftx/) - An improved and corrected font series derived from [ttf-x2](https://aur.archlinux.org/packages/ttf-x2/) Persian font series, Metafont and FarsiTeX fonts with Kashida feature.

#### Sinhala

*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - Sinhala Unicode font

#### Thai

*   [ttf-tlwg](https://www.archlinux.org/packages/?name=ttf-tlwg) - Collection of scalable Thai fonts

#### Tibetan

*   [ttf-tibetan-machine](https://www.archlinux.org/packages/?name=ttf-tibetan-machine) - Tibetan Machine TTFont

### Math

*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Mathematica fonts by Wolfram Research, Inc.
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/) - MathType fonts
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/), [otf-cm-unicode](https://aur.archlinux.org/packages/otf-cm-unicode/) - [Computer Modern](https://en.wikipedia.org/wiki/Computer_Modern "wikipedia:Computer Modern") (of TeX fame)
*   [otf-latin-modern](https://aur.archlinux.org/packages/otf-latin-modern/), [otf-latinmodern-math](https://aur.archlinux.org/packages/otf-latinmodern-math/) - Improved version of Computer Modern fonts as used in LaTeX
*   [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) and [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra) contain many math fonts such as Latin Modern Math and [STIX Fonts](https://en.wikipedia.org/wiki/STIX_Fonts_project "wikipedia:STIX Fonts project"). See [TeX Live#Fonts](/index.php/TeX_Live#Fonts "TeX Live") for configuration.
*   [otf-xits](https://aur.archlinux.org/packages/otf-xits/) - An OpenType implementation of [STIX Fonts](https://en.wikipedia.org/wiki/STIX_Fonts_project "wikipedia:STIX Fonts project") with support for maths written from right to left.

### Metric-compatible fonts

See [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts"), which lists available alternatives for [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts").

### Apple OS X fonts

*   [ttf-mac-fonts](https://aur.archlinux.org/packages/ttf-mac-fonts/) - Mac OS X TrueType fonts

### Monospaced

Here are some suggestions. Every user has their own favorite, so experiment to find yours. If you are in a hurry, you read Dan Benjamin's blog post: [*Top 10 Programming Fonts*](http://hivelogic.com/articles/top-10-programming-fonts).

Here is a long list of fonts by Trevor Lowing: [http://www.lowing.org/fonts/](http://www.lowing.org/fonts/).

A comparison with images on Slant: [What are the best programming fonts?](http://www.slant.co/topics/67/~what-are-the-best-programming-fonts)

And a Stack Overflow question with some images: [Recommended fonts for programming](http://stackoverflow.com/questions/4689/recommended-fonts-for-programming)

#### TrueType

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [Bitstream Vera Mono](https://en.wikipedia.org/wiki/Bitstream_Vera "wikipedia:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera))
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)) - Windows programming font
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Cousine ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/) or [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS replacement for Courier New (metric-compatible)
*   [DejaVu Sans Mono](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans Mono](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [Envy Code R](https://damieng.com/blog/2008/05/26/envy-code-r-preview-7-coding-font-released) ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/))
*   Fantasque Sans Mono ([ttf-fantasque-sans](https://aur.archlinux.org/packages/ttf-fantasque-sans/) or [ttf-fantasque-sans-git](https://aur.archlinux.org/packages/ttf-fantasque-sans-git/))
*   [FreeMono](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Excellent programming font
*   [Inconsolata-g](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - adds some programmer-friendly modifications
*   [Liberation Mono](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Replacement for Courier New, based on Cousine (metric-compatible)
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (included in package [jre](https://aur.archlinux.org/packages/jre/))
*   [Monaco](https://en.wikipedia.org/wiki/Monaco_(typeface) ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)) - Popular programming font on OSX/Textmate
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))
*   [Source Code Pro](https://en.wikipedia.org/wiki/Source_Code_Pro "wikipedia:Source Code Pro") ([adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts))

#### Bitmap

*   Default 8x16
*   Dina ([dina-font](https://www.archlinux.org/packages/?name=dina-font))
*   [Gohu](http://font.gohu.org/) ([gohufont](https://aur.archlinux.org/packages/gohufont/))
*   Lime ([artwiz-fonts](https://www.archlinux.org/packages/?name=artwiz-fonts))
*   [ProFont](https://en.wikipedia.org/wiki/ProFont "wikipedia:ProFont") ([profont](https://www.archlinux.org/packages/?name=profont))
*   [Proggy Programming Fonts](https://en.wikipedia.org/wiki/Proggy_Programming_Fonts "wikipedia:Proggy Programming Fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/))
*   Tamsyn ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font))
*   [Terminus](http://terminus-font.sourceforge.net/) ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font))
*   [Tewi](https://github.com/lucy/tewi-font) ([bdf-tewi-git](https://aur.archlinux.org/packages/bdf-tewi-git/))
*   Unifont (glyphs like (look of disapproval)) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont))

### Sans-serif

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/))
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Arimo ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/) or [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS replacement for Arial (metric-compatible)
*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [DejaVu Sans](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSans](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Sans](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) Replacement for Arial, based on Arimo (metric-compatible)
*   [Linux Biolinum](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine))
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - 3 major variations: normal, narrow, and caption - Unicode: Latin, Cyrillic
*   [Source Sans Pro](https://en.wikipedia.org/wiki/Source_Sans_Pro "wikipedia:Source Sans Pro") ([adobe-source-sans-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-sans-pro-fonts))
*   [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Ubuntu Font Family](https://en.wikipedia.org/wiki/Ubuntu_Font_Family "wikipedia:Ubuntu Font Family") ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### Script

*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### Serif

*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [DejaVu Serif](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Serif](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSerif](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Gentium](https://en.wikipedia.org/wiki/Gentium "wikipedia:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium)) - Unicode: Latin, Greek, Cyrillic, Phonetic Alphabet
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Serif](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Replacement for Times New Roman, based on Tinos (metric-compatible)
*   [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode: Latin, Greek, Cyrillic, Hebrew
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Tinos ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/) or [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS replacement for Times New Roman (metric-compatible)

### Unsorted

*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) - a huge collection of free fonts (including ubuntu, inconsolata, droid, etc.) - Note: Your font dialog might get very long as >100 fonts will be added.
*   [ttf-mph-2b-damase](https://www.archlinux.org/packages/?name=ttf-mph-2b-damase) - Covers full plane 1 and several scripts
*   [font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf) - X.Org Luxi fonts
*   [ttf-cheapskate](https://www.archlinux.org/packages/?name=ttf-cheapskate) - Font collection from *dustismo.com*
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) - Junius font containing almost complete medieval latin script glyphs
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) - IBM Courier and Adobe Utopia sets of [PostScript fonts](https://en.wikipedia.org/wiki/PostScript_fonts "wikipedia:PostScript fonts")
*   [all-repository-fonts](https://aur.archlinux.org/packages/all-repository-fonts/) - Meta package for all fonts in the official repositories.

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

You can add a section for sans-serif and monospace as well. For more informations, have a look at the fontconfig manual.

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

You can use the following command to list all installed fonts that are available on your system.

```
$ fc-list

```

### Lists installed fonts for a particular language

Applications and browsers select and display fonts depending upon fontconfig preferences and available font glyph for Unicode text. To list installed fonts for a particular language, issue a command `fc-list :lang="two letter language code"`. For instance, to list installed Arabic fonts or fonts supporting Arabic glyph:

 `$ fc-list -f '%{file}
' :lang=ar` 
```
/usr/share/fonts/TTF/FreeMono.ttf
/usr/share/fonts/TTF/DejaVuSansCondensed.ttf
/usr/share/fonts/truetype/custom/DroidKufi-Bold.ttf
/usr/share/fonts/TTF/DejaVuSansMono.ttf
/usr/share/fonts/TTF/FreeSerif.ttf

```

### Set terminal font on-the-fly

For terminal emulators that use `Xresources`, fonts can be set by using escape sequences. Specifically, echo `\033]710;$font\007` to change the normal font (`*font` in `~/.Xresources`), and replace `710` with `711`, `712`, and `713` to change the `*boldFont`, `*italicFont`, and `*boldItalicFont`, respectively.

`$font` can be anything the terminal emulator will support.

### Application-specific font cache

Matplotlib ([python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib) or [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)) uses its own font cache, so after updating fonts, be sure to remove `$HOME/.matplotlib/fontList.cache`, `$HOME/.cache/matplotlib/fontList.cache`, `$HOME/.sage/matplotlib-1.2.1/fontList.cache`, etc. so it will regenerate its cache and find the new fonts [[4]](http://matplotlib.1069221.n5.nabble.com/getting-matplotlib-to-recognize-a-new-font-td40500.html).

## See also

*   [State of Text Rendering](http://behdad.org/text/)