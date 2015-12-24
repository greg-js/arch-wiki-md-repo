# Fonts

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Infinality](/index.php/Infinality "Infinality")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts")

From [Wikipedia](https://en.wikipedia.org/wiki/Computer_font "wikipedia:Computer font"):

_A computer font (or font) is an electronic data file containing a set of glyphs, characters, or symbols such as dingbats._

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
    *   [4.1 Braille](#Braille)
    *   [4.2 International users](#International_users)
        *   [4.2.1 Arabic & Urdu](#Arabic_.26_Urdu)
        *   [4.2.2 Persian](#Persian)
        *   [4.2.3 Burmese](#Burmese)
        *   [4.2.4 Chinese, Japanese, Korean, Vietnamese](#Chinese.2C_Japanese.2C_Korean.2C_Vietnamese)
            *   [4.2.4.1 Pan-CJK](#Pan-CJK)
            *   [4.2.4.2 (Mainly) Chinese](#.28Mainly.29_Chinese)
            *   [4.2.4.3 Japanese](#Japanese)
            *   [4.2.4.4 Korean](#Korean)
        *   [4.2.5 Cyrillic](#Cyrillic)
        *   [4.2.6 Greek](#Greek)
        *   [4.2.7 Hebrew](#Hebrew)
        *   [4.2.8 Indic](#Indic)
        *   [4.2.9 Khmer](#Khmer)
        *   [4.2.10 Lao](#Lao)
        *   [4.2.11 Meroitic (Egyptian Hieroglyphs)](#Meroitic_.28Egyptian_Hieroglyphs.29)
        *   [4.2.12 Sinhala](#Sinhala)
        *   [4.2.13 Thai](#Thai)
        *   [4.2.14 Tibetan](#Tibetan)
    *   [4.3 Math](#Math)
    *   [4.4 Microsoft fonts](#Microsoft_fonts)
    *   [4.5 Apple OS X fonts](#Apple_OS_X_fonts)
    *   [4.6 Monospaced](#Monospaced)
        *   [4.6.1 TrueType](#TrueType)
        *   [4.6.2 Bitmap](#Bitmap)
    *   [4.7 Sans-serif](#Sans-serif)
    *   [4.8 Script](#Script)
    *   [4.9 Serif](#Serif)
    *   [4.10 Unsorted](#Unsorted)
*   [5 Fallback font order with X11](#Fallback_font_order_with_X11)
*   [6 Font alias](#Font_alias)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 List all installed fonts](#List_all_installed_fonts)
    *   [7.2 Set terminal font on-the-fly](#Set_terminal_font_on-the-fly)
    *   [7.3 Application-specific font cache](#Application-specific_font_cache)
*   [8 See also](#See_also)

## Font formats

Most computer fonts used today are in either _bitmap_ or _outline_ data formats.

Bitmap fonts

Consist of a matrix of dots or pixels representing the image of each glyph in each face and size.

Outline or _vector_ fonts

Use Bézier curves, drawing instructions and mathematical formulae to describe each glyph, which make the character outlines scalable to any size.

### Common extensions

*   `bdf` and `bdf.gz` – bitmap fonts, _b_itmap _d_istribution _f_ormat and gzip compressed `bdf`
*   `pcf` and `pcf.gz` – bitmaps, _p_ortable _c_ompiled _f_ont and gzip compressed `pcf`
*   `psf`, `psfu`, `psf.gz` and `psfu.gz` – bitmaps, _P_C _s_creen _f_ont, _P_C _s_creen _f_ont _U_nicode and the gzipped versions (not compatible with X.Org)
*   `pfa` and `pfb` – outline fonts, _P_ostScript _f_ont _A_SCII and _P_ostScript _f_ont _b_inary. PostScript fonts carry built-in printer instructions.
*   `ttf` – outline, _T_rue_T_ype _f_ont. Originally designed as a replacement for the PostScript fonts.
*   `otf` – outline, _O_pen_T_ype _f_ont. TrueType with PostScript typographic instructions.

For most purposes, the technical differences between TrueType and OpenType can be ignored, some fonts with a `ttf` extension are actually OpenType fonts.

### Other formats

The typesetting application, _TeX,_ and its companion font software, _Metafont,_ render characters using their own methods. Some of the file extensions used for fonts by these two programs are `*pk`, `*gf`, `mf` and `vf`.

_FontForge,_ a font editing application, can store fonts in its native text-based format, `sfd`, _s_pline _f_ont _d_atabase.

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

The family name of a font file can be aquired with the use of `fc-query` for example: `fc-query -f '%{family[0]}\n' /path/to/file`. The formatting is described in the FcPatternFormat(3) manual.

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

For Xserver to load fonts directly (as opposed to the use of a _font server_) the directory for your newly added font must be added with a FontPath entry. This entry is located in the _Files_ section [of your Xorg configuration file](/index.php/Xorg#Configuration "Xorg") (e.g. `/etc/X11/xorg.conf` or `/etc/xorg.conf`). See [#Older applications](#Older_applications) for more detail.

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

**Note:** This section is about the [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"). For an alternative console solutions offering more features (full Unicode fonts, modern graphics adapters etc.), see [fbterm](/index.php/Fbterm "Fbterm"), [KMSCON](/index.php/KMSCON "KMSCON") or similar projects.

By default, the [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") uses the kernel built-in font with a [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437") character set,<sup>[[1]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/tty/vt/Makefile#n4)</sup> but this can be easily changed.

The [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") uses UTF-8 encoding by default, but because the standard VGA-compatible framebuffer is used, a console font is limited to either a standard 256, or 512 glyphs. If the font has more than 256 glyphs, the number of colours is reduced from 16 to 8\. In order to assign correct symbol to be displayed to the given Unicode value, a special translation map, often called _unimap_, is needed. Nowadays most of the console fonts have the _unimap_ built-in, historically it had to be loaded separately.

The [kbd](https://www.archlinux.org/packages/?name=kbd) package provides tools to change virtual console font and font mapping. Available fonts are saved in the `/usr/share/kbd/consolefonts/` directory, those ending with _.psfu_ or _.psfu.gz_ have a Unicode translation map built-in.

Keymaps, the connection between the key pressed and the character used by the computer, are found in the subdirectories of `/usr/share/kbd/keymaps/`, see [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") for details.

**Note:** Replacing the font can cause issues with programs that expect a standard VGA-style font, such as those using line drawing graphics.

### Previewing and testing

**Tip:** An organized library of images for previewing is available: [Linux console fonts screenshots](http://alexandre.deverteuil.net/pages/consolefonts/).

The available glyphs or letters in the font can also be viewed as a table with using _showconsolefont_:

```
$ showconsolefont

```

The _setfont_ utility may be used to temporarily change the font, so that the user can consider its permanent use. Just pass the name of the font (they are located in `/usr/share/kbd/consolefonts/`). For example:

```
$ setfont lat2-16 -m 8859-2

```

Note that the font name is case-sensitive, so type it _exactly_ as you see it. If the newly changed font is not suitable, a return to the default font with the following command (even if the console display is totally unreadable, this command will still work, just type the command "blindly"):

```
$ setfont

```

**Note:** _setfont_ only works on the console currently being used. Any other consoles, active or inactive, remain unaffected.

### Persistent configuration

The `FONT` variable in `/etc/vconsole.conf` is used to set the font at boot, persistently for all consoles. See `man 5 vconsole.conf` for details.

For displaying characters such as _Č, ž, đ, š_ or _Ł, ę, ą, ś_ using the font `lat2-16.psfu.gz`:

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

### Braille

*   [ttf-ubraille](https://www.archlinux.org/packages/?name=ttf-ubraille) - Font containing Unicode symbols for _braille_

### International users

Applications and browsers select and display fonts depending upon fontconfig preferences and available font glyph for Unicode text. To list installed fonts for a particular language, issue a command `fc-list :lang="two letter language code"`. For instance, to list installed Arabic fonts or fonts supporting Arabic glyph:

 `$ fc-list -f '%{file}\n' :lang=ar` 

```
/usr/share/fonts/TTF/FreeMono.ttf
/usr/share/fonts/TTF/DejaVuSansCondensed.ttf
/usr/share/fonts/truetype/custom/DroidKufi-Bold.ttf
/usr/share/fonts/TTF/DejaVuSansMono.ttf
/usr/share/fonts/TTF/FreeSerif.ttf

```

To properly render fonts for multilingual websites like Wikipedia or this Arch Linux wiki, install one of the following sets of packages:

*   Google's [Noto](http://www.google.com/get/noto/) is a font family that aims to support all languages. [Install](/index.php/Install "Install") it with the [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts), [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) and [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji) packages.
*   An alternative set of fonts which has a good coverage of languages is [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont) with [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) and [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk).

#### Arabic & Urdu

*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/)<sup><small>AUR</small></sup> - Fonts by King Fahd Glorious Quran Printing Complex in al-Madinah al-Munawwarah
*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/)<sup><small>AUR</small></sup> - A classical Arabic typeface in Naskh style poineered by Amiria Press
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/)<sup><small>AUR</small></sup> - Unicode Arabic font from SIL
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/)<sup><small>AUR</small></sup> - Unicode Arabic font from SIL
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/)<sup><small>AUR</small></sup> - Collection of free Arabic fonts
*   [ttf-urdufonts](https://aur.archlinux.org/packages/ttf-urdufonts/)<sup><small>AUR</small></sup> - Urdu fonts (Jameel Noori Nastaleeq (+kasheeda), Nafees Web Naskh, PDMS Saleem Quran Font) and font configuration to set Jameel Noori Nastaleeq as default font for Urdu

#### Persian

*   [ttf-irfonts](https://aur.archlinux.org/packages/ttf-irfonts/)<sup><small>AUR</small></sup> - Official I.R. Iran Supreme Council of Information and Communication Technology (SCICT) standard persian fonts series
*   [ttf-borna](https://aur.archlinux.org/packages/ttf-borna/)<sup><small>AUR</small></sup> - Borna Rayaneh Persian B font series
*   [ttf-x2](https://aur.archlinux.org/packages/ttf-x2/)<sup><small>AUR</small></sup> - X Series 2 fonts are built on freely available fonts and extended to support Persian, Arabic, Urdu, Pashto, Dari, Uzbek, Kurdish, Uighur, old Turkish (Ottoman) and modern Turkish (Roman).
*   [ttf-iran-nastaliq](https://aur.archlinux.org/packages/ttf-iran-nastaliq/)<sup><small>AUR</small></sup> - An Unicode calligraphic font published by the High Council of Informatics of Iran

#### Burmese

*   [ttf-my-paduk](https://aur.archlinux.org/packages/ttf-my-paduk/)<sup><small>AUR</small></sup> - Padauk font for Myanmar/Birmania
*   [ttf-myanmar3](https://aur.archlinux.org/packages/ttf-myanmar3/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-myanmar3)]</sup> - Font for Myanmar/Burmese script
*   [ttf-myanmar-fonts](https://aur.archlinux.org/packages/ttf-myanmar-fonts/)<sup><small>AUR</small></sup> - 121 Fonts from myordbok.com

#### Chinese, Japanese, Korean, Vietnamese

##### Pan-CJK

*   [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) - Large collection of fonts which comprehensively support Simplified Chinese, Traditional Chinese, Japanese, and Korean, with a consistent design and look.

##### (Mainly) Chinese

*   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts) - Simplified Chinese OpenType/CFF fonts
*   [adobe-source-han-sans-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-tw-fonts) - Traditional Chinese OpenType/CFF fonts
*   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - A Sans-Serif style high quality CJKV outline font.
*   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - Hei Ti Style (sans-serif) Chinese Outline font embedded with bitmapped Song Ti (also supporting Japanese (partial) and Korean characters).
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - _Kaiti_ (brush stroke) Unicode font (enabling anti-aliasing is suggested)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - _Mingti_ (printed) Unicode font
*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - _New Sung_ font, previously is ttf-fireflysung package
*   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - Bitmapped Song Ti (serif) Chinese font
*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Chinese and Vietnamese TrueType font
*   [ttf-i.bming](https://aur.archlinux.org/packages/ttf-i.bming/)<sup><small>AUR</small></sup> - CJK serif font that emphasis on an old-style typeface
*   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/)<sup><small>AUR</small></sup> - Kai and Song traditional Chinese font from the Ministry of Education of Taiwan

##### Japanese

*   [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) - Japanese OpenType/CFF fonts
*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - Formal style Japanese Gothic (sans-serif) and Mincho (serif) fonts set; one of the highest quality open source font. Default of openSUSE-ja.
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - Japanese free TrueType font. This is outdated and not maintained any more, but may be defined as a fallback font on several environments.
*   [ttf-hanazono](https://www.archlinux.org/packages/?name=ttf-hanazono) - A free Japanese kanji font, style Mincho (serif).
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/)<sup><small>AUR</small></sup> - Japanese Gothic fonts. Default of Debian/Fedora/Vine Linux
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/)<sup><small>AUR</small></sup> - Modern Gothic style Japanese outline fonts. It includes all of Japanese Hiragana/Katakana, Basic Latin, Latin-1 Supplement, Latin Extended-A, IPA Extensions and most of Japanese Kanji, Greek, Cyrillic, Vietnamese with 7 weights (proportional) or 5 weights (monospace).
*   [ttf-ipa-mona](https://aur.archlinux.org/packages/ttf-ipa-mona/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-ipa-mona)]</sup>, [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/)<sup><small>AUR</small></sup> - Japanese fonts to show [2channel Shift JIS art](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art") properly.

##### Korean

*   [adobe-source-han-sans-kr-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-kr-fonts) - Korean OpenType/CFF fonts
*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - Collection of Korean TrueType fonts
*   [ttf-alee](https://aur.archlinux.org/packages/ttf-alee/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-alee)]</sup> - Set of free Hangul TrueType fonts
*   [ttf-unfonts-core](https://aur.archlinux.org/packages/ttf-unfonts-core/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-unfonts-core)]</sup> - Un fonts (default Baekmuk fonts may be unsatisfactory)
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/)<sup><small>AUR</small></sup> - Nanum series TrueType fonts
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/)<sup><small>AUR</small></sup> - Nanum series fixed width TrueType fonts

#### Cyrillic

_Also see [#Monospaced](#Monospaced), [#Sans-serif](#Sans-serif) and [#Serif](#Serif)_

*   [font-arhangai](https://aur.archlinux.org/packages/font-arhangai/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/font-arhangai)]</sup> - Mongolian Cyrillic
*   [otf-russkopis](https://aur.archlinux.org/packages/otf-russkopis/)<sup><small>AUR</small></sup> - A free OpenType cursive font for Cyrillic script
*   [ttf-paratype](https://aur.archlinux.org/packages/ttf-paratype/)<sup><small>AUR</small></sup> - Font family by ParaType: sans, serif, mono, extended cyrillic and latin, OFL license
*   [ttf-pingwi-typography](https://aur.archlinux.org/packages/ttf-pingwi-typography/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-pingwi-typography)]</sup> - PingWi Typography (PWT) fonts

#### Greek

Almost all Unicode fonts contain the Greek character set (polytonic included). Some additional font packages, which might not contain the complete Unicode set but utilize high quality Greek (and Latin, of course) typefaces are:

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/)<sup><small>AUR</small></sup> - Selection of OpenType fonts from the Greek Font Society
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/)<sup><small>AUR</small></sup> - Professional TrueType fonts from Magenta

#### Hebrew

*   [culmus](https://aur.archlinux.org/packages/culmus/)<sup><small>AUR</small></sup> - Nice collection of free Hebrew fonts

#### Indic

*   [ttf-freebanglafont](https://www.archlinux.org/packages/?name=ttf-freebanglafont) - Font for Bangla
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - Indic OpenType Fonts collection (containing ttf-freebanglafont)

(This one contains a "look of disapproval" that might be more to your liking than the [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) one mentioned elsewhere in this document)

*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/)<sup><small>AUR</small></sup> - Indic TrueType fonts from Fedora Project (containing Oriya Fonts and more)
*   [ttf-devanagarifonts](https://aur.archlinux.org/packages/ttf-devanagarifonts/)<sup><small>AUR</small></sup> - Devanagari TrueType fonts (contains 283 fonts)
*   [ttf-gujrati-fonts](https://aur.archlinux.org/packages/ttf-gujrati-fonts/)<sup><small>AUR</small></sup> - TTF Gujarati fonts (Avantika,Gopika,Shree768)
*   [ttf-gurmukhi-fonts_sikhnet](https://aur.archlinux.org/packages/ttf-gurmukhi-fonts_sikhnet/)<sup><small>AUR</small></sup> - TrueType Gurmukhi fonts (gurbaniwebthick,prabhki)
*   [ttf-gurmukhi_punjabi](https://aur.archlinux.org/packages/ttf-gurmukhi_punjabi/)<sup><small>AUR</small></sup> - TTF Gurmukhi / Punjabi (contains 252 fonts)
*   [ttf-kannada-font](https://aur.archlinux.org/packages/ttf-kannada-font/)<sup><small>AUR</small></sup> - Kannada, the language of Karnataka state in India
*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/)<sup><small>AUR</small></sup> - Tamil Unicode fonts

#### Khmer

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - Font covering glyphs for Khmer language
*   [Hanuman](https://www.google.com/fonts/specimen/Hanuman) ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>)

#### Lao

*   [ttf-lao](https://aur.archlinux.org/packages/ttf-lao/)<sup><small>AUR</small></sup> - Lao TTF font (Phetsarath_OT)
*   [ttf-lao-fonts](https://aur.archlinux.org/packages/ttf-lao-fonts/)<sup><small>AUR</small></sup> - Lao TTF fonts, both Unicode and non-Unicode for Windows

#### Meroitic (Egyptian Hieroglyphs)

*   [ttf-aegyptus](https://aur.archlinux.org/packages/ttf-aegyptus/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-aegyptus)]</sup> - Font for Egyptian Hieroglyphs (part of Unicode Fonts for Ancient Scripts)

#### Sinhala

*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/)<sup><small>AUR</small></sup> - Sinhala Unicode font

#### Thai

*   [ttf-tlwg](https://www.archlinux.org/packages/?name=ttf-tlwg) - Collection of scalable Thai fonts

#### Tibetan

*   [ttf-tibetan-machine](https://www.archlinux.org/packages/?name=ttf-tibetan-machine) - Tibetan Machine TTFont

### Math

*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Mathematica fonts by Wolfram Research, Inc.
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/)<sup><small>AUR</small></sup> - MathType fonts
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/)<sup><small>AUR</small></sup>, [otf-cm-unicode](https://aur.archlinux.org/packages/otf-cm-unicode/)<sup><small>AUR</small></sup> - [Computer Modern](https://en.wikipedia.org/wiki/Computer_Modern "wikipedia:Computer Modern") (of TeX fame)
*   [otf-xits](https://aur.archlinux.org/packages/otf-xits/)<sup><small>AUR</small></sup> - An OpenType implementation of [STIX Fonts](https://en.wikipedia.org/wiki/STIX_Fonts_project "wikipedia:STIX Fonts project") with math support

### Microsoft fonts

See [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts").

### Apple OS X fonts

*   [ttf-mac-fonts](https://aur.archlinux.org/packages/ttf-mac-fonts/)<sup><small>AUR</small></sup> - Mac OS X TrueType fonts

### Monospaced

Here are some suggestions. Every user has their own favorite, so experiment to find yours. If you are in a hurry, you read Dan Benjamin's blog post: [_Top 10 Programming Fonts_](http://hivelogic.com/articles/top-10-programming-fonts).

Here is a long list of fonts by Trevor Lowing: [http://www.lowing.org/fonts/](http://www.lowing.org/fonts/).

A comparison with images on Slant: [What are the best programming fonts?](http://www.slant.co/topics/67/~what-are-the-best-programming-fonts)

And a Stack Overflow question with some images: [Recommended fonts for programming](http://stackoverflow.com/questions/4689/recommended-fonts-for-programming)

#### TrueType

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   Anka/Coder ([ttf-anka-coder](https://aur.archlinux.org/packages/ttf-anka-coder/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-anka-coder)]</sup>)
*   [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>)
*   [Bitstream Vera Mono](https://en.wikipedia.org/wiki/Bitstream_Vera "wikipedia:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera))
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)<sup><small>AUR</small></sup>) - Windows programming font
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   Cousine ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/)<sup><small>AUR</small></sup> or [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>) - Chrome/Chromium OS replacement for Courier New (metric-compatible)
*   [DejaVu Sans Mono](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans Mono](https://en.wikipedia.org/wiki/Droid_(font) "wikipedia:Droid (font)") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>)
*   [Envy Code R](https://damieng.com/blog/2008/05/26/envy-code-r-preview-7-coding-font-released) ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/)<sup><small>AUR</small></sup>)
*   Fantasque Sans Mono ([ttf-fantasque-sans](https://aur.archlinux.org/packages/ttf-fantasque-sans/)<sup><small>AUR</small></sup> or [ttf-fantasque-sans-git](https://aur.archlinux.org/packages/ttf-fantasque-sans-git/)<sup><small>AUR</small></sup>)
*   [FreeMono](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>) - Excellent programming font
*   [Inconsolata-g](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)<sup><small>AUR</small></sup>) - adds some programmer-friendly modifications
*   [Liberation Mono](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Replacement for Courier New, based on Cousine (metric-compatible)
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (included in package [jre](https://aur.archlinux.org/packages/jre/)<sup><small>AUR</small></sup>)
*   [Monaco](https://en.wikipedia.org/wiki/Monaco_(typeface) "wikipedia:Monaco (typeface)") ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)<sup><small>AUR</small></sup>) - Popular programming font on OSX/Textmate
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/)<sup><small>AUR</small></sup>)
*   [Source Code Pro](https://en.wikipedia.org/wiki/Source_Code_Pro "wikipedia:Source Code Pro") ([adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts))

#### Bitmap

*   Default 8x16
*   Dina ([dina-font](https://www.archlinux.org/packages/?name=dina-font))
*   [Gohu](http://font.gohu.org/) ([gohufont](https://aur.archlinux.org/packages/gohufont/)<sup><small>AUR</small></sup>)
*   Lime ([artwiz-fonts](https://www.archlinux.org/packages/?name=artwiz-fonts))
*   [ProFont](https://en.wikipedia.org/wiki/ProFont "wikipedia:ProFont") ([profont](https://www.archlinux.org/packages/?name=profont))
*   [Proggy Programming Fonts](https://en.wikipedia.org/wiki/Proggy_Programming_Fonts "wikipedia:Proggy Programming Fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/)<sup><small>AUR</small></sup>)
*   Proggy opti cyrillic ([proggyopticyr-font](https://aur.archlinux.org/packages/proggyopticyr-font/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/proggyopticyr-font)]</sup>)
*   Tamsyn ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font))
*   [Terminus](http://terminus-font.sourceforge.net/) ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font))
*   [Tewi](https://github.com/lucy/tewi-font) ([bdf-tewi-git](https://aur.archlinux.org/packages/bdf-tewi-git/)<sup><small>AUR</small></sup>)
*   Unifont (glyphs like (look of disapproval)) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont))

### Sans-serif

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/)<sup><small>AUR</small></sup>, included in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-sil-fonts)]</sup>)
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   Arimo ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/)<sup><small>AUR</small></sup> or [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>) - Chrome/Chromium OS replacement for Arial (metric-compatible)
*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)<sup><small>AUR</small></sup>)
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)<sup><small>AUR</small></sup>)
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) "wikipedia:Corbel (typeface)") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)<sup><small>AUR</small></sup>)
*   [DejaVu Sans](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans](https://en.wikipedia.org/wiki/Droid_(font) "wikipedia:Droid (font)") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>)
*   [FreeSans](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) "wikipedia:Impact (typeface)") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   [Liberation Sans](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) Replacement for Arial, based on Arimo (metric-compatible)
*   [Linux Biolinum](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine))
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>) - 3 major variations: normal, narrow, and caption - Unicode: Latin, Cyrillic
*   [Source Sans Pro](https://en.wikipedia.org/wiki/Source_Sans_Pro "wikipedia:Source Sans Pro") ([adobe-source-sans-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-sans-pro-fonts))
*   [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) "wikipedia:Tahoma (typeface)") ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/)<sup><small>AUR</small></sup>)
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   [Ubuntu-Title](https://en.wikipedia.org/wiki/Ubuntu-Title "wikipedia:Ubuntu-Title") ([ttf-ubuntu-title](https://aur.archlinux.org/packages/ttf-ubuntu-title/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-ubuntu-title)]</sup>)
*   [Ubuntu Font Family](https://en.wikipedia.org/wiki/Ubuntu_Font_Family "wikipedia:Ubuntu Font Family") ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)

### Script

*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)

### Serif

*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) "wikipedia:Cambria (typeface)") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)<sup><small>AUR</small></sup>)
*   [Charis](https://en.wikipedia.org/wiki/Charis_SIL "wikipedia:Charis SIL") ([ttf-charis](https://aur.archlinux.org/packages/ttf-charis/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-charis)]</sup>, included in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-sil-fonts)]</sup>) - Unicode: Latin, Cyrillic
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) "wikipedia:Constantia (typeface)") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)<sup><small>AUR</small></sup>)
*   [DejaVu Serif](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Doulos](https://en.wikipedia.org/wiki/Doulos_SIL "wikipedia:Doulos SIL") ([ttf-sil-doulos](https://aur.archlinux.org/packages/ttf-sil-doulos/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-sil-doulos)]</sup>, included in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-sil-fonts)]</sup>) - Unicode: Latin, Cyrillic
*   [Droid Serif](https://en.wikipedia.org/wiki/Droid_(font) "wikipedia:Droid (font)") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), included in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>)
*   [FreeSerif](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Gentium](https://en.wikipedia.org/wiki/Gentium "wikipedia:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium), included in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-sil-fonts)]</sup>) - Unicode: Latin, Greek, Cyrillic, Phonetic Alphabet
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) "wikipedia:Georgia (typeface)") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   [Liberation Serif](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Replacement for Times New Roman, based on Tinos (metric-compatible)
*   [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode: Latin, Greek, Cyrillic, Hebrew
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>)
*   Tinos ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/)<sup><small>AUR</small></sup> or [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup>) - Chrome/Chromium OS replacement for Times New Roman (metric-compatible)

### Unsorted

*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)<sup><small>AUR</small></sup> — a huge collection of free fonts (including ubuntu, inconsolata, droid, etc.) - Note: Your font dialog might get very long as >100 fonts will be added.
*   [ttf-mph-2b-damase](https://www.archlinux.org/packages/?name=ttf-mph-2b-damase) — Covers full plane 1 and several scripts
*   [ttf-symbola](https://www.archlinux.org/packages/?name=ttf-symbola) — Provides emoji and many many other symbols
*   [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-sil-fonts)]</sup> — Gentium, Charis, Doulos, Andika and Abyssinica from SIL
*   [font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf) — X.Org Luxi fonts
*   [ttf-cheapskate](https://www.archlinux.org/packages/?name=ttf-cheapskate) — Font collection from _dustismo.com_
*   [ttf-isabella](https://aur.archlinux.org/packages/ttf-isabella/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-isabella)]</sup> — Calligraphic font based on the _Isabella Breviary_ of 1497
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) — Junius font containing almost complete medieval latin script glyphs
*   arkpandorafonts [ttf-arkpandora](https://aur.archlinux.org/packages/ttf-arkpandora/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-arkpandora)]</sup> — Alternative to Arial and Times New Roman fonts
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) — IBM Courier and Adobe Utopia sets of [PostScript fonts](https://en.wikipedia.org/wiki/PostScript_fonts "wikipedia:PostScript fonts")

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

You can add a section for Sans-serif and monospace as well. For more informations, have a look at the fontconfig manual.

## Font alias

There are several font aliases which represent other fonts in order that applications may use similar fonts. The most common aliases are: `serif` for a font of the serif type (e.g. DejaVu Serif); `sans-serif` for a font of the sans-serif type (e.g. DejaVu Sans); and `monospace` for a monospaced font (e.g. DejaVu Sans Mono). However, the fonts which these aliases represent may vary and the relationship is often not shown in font management tools, such as those found in [KDE](/index.php/KDE "KDE") and other [desktop environments](/index.php/Desktop_environments "Desktop environments").

To reverse an alias and find which font it is representing, run:

```
$ fc-match monospace
DejaVuSansMono.ttf: "DejaVu Sans Mono" "Book"

```

In this case, `DejaVuSansMono.ttf` is the font represented by the monospace alias.

## Tips and tricks

### List all installed fonts

You can use the following command to list all installed fonts that are available on your system.

```
$ fc-list

```

### Set terminal font on-the-fly

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Which terminals specifically support this method? Where is the documentation for the escape codes? (Discuss in [Talk:Fonts#](https://wiki.archlinux.org/index.php/Talk:Fonts))

For terminal emulators that use `Xresources`, fonts can be set by using escape sequences. Specifically, echo `\033]710;$font\007` to change the normal font (`*font` in `~/.Xresources`), and replace `710` with `711`, `712`, and `713` to change the `*boldFont`, `*italicFont`, and `*boldItalicFont`, respectively.

`$font` can be anything the terminal emulator will support.

### Application-specific font cache

Matplotlib ([python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib) or [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)) uses its own font cache, so after updating fonts, be sure to remove `$HOME/.matplotlib/fontList.cache`, `$HOME/.cache/matplotlib/fontList.cache`, `$HOME/.sage/matplotlib-1.2.1/fontList.cache`, etc. so it will regenerate its cache and find the new fonts [[4]](http://matplotlib.1069221.n5.nabble.com/getting-matplotlib-to-recognize-a-new-font-td40500.html).

## See also

*   [State of Text Rendering](http://behdad.org/text/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fonts&oldid=413203](https://wiki.archlinux.org/index.php?title=Fonts&oldid=413203)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Fonts](/index.php/Category:Fonts "Category:Fonts")