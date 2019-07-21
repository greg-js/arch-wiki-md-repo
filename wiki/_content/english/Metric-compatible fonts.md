Related articles

*   [Fonts](/index.php/Fonts "Fonts")
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts")

**Metric-compatible fonts** are fonts that match the metrics (i.e. glyph dimensions) of another font (often generics such as Helvetica, Times or Courier). Due to their matching metrics, replacing a font with a [metric-compatible](https://en.wikipedia.org/wiki/metric-compatible "wikipedia:metric-compatible") alternative does not change the formatting of the document or a web page. Such fonts are often developed for FOSS systems to display pages correctly.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 List of metric-compatible fonts](#List_of_metric-compatible_fonts)
*   [2 Generic Families](#Generic_Families)
    *   [2.1 PostScript](#PostScript)
        *   [2.1.1 Garamond](#Garamond)
    *   [2.2 Microsoft](#Microsoft)
*   [3 Metric-compatible font projects](#Metric-compatible_font_projects)
    *   [3.1 TeX Gyre](#TeX_Gyre)
    *   [3.2 GNU FreeFont](#GNU_FreeFont)
    *   [3.3 Liberation](#Liberation)
    *   [3.4 Google](#Google)
        *   [3.4.1 Chrome OS](#Chrome_OS)
        *   [3.4.2 Noto](#Noto)
    *   [3.5 Other metric-compatible fonts](#Other_metric-compatible_fonts)
        *   [3.5.1 Selawik](#Selawik)
        *   [3.5.2 Wine Tahoma](#Wine_Tahoma)
*   [4 Example configuration](#Example_configuration)
    *   [4.1 Example for binding method](#Example_for_binding_method)
    *   [4.2 Example for prefer method](#Example_for_prefer_method)
*   [5 See also](#See_also)

## List of metric-compatible fonts

In the following table, commonly-specified families are shown in **bold**. This table is roughly based on [fontconfig](/index.php/Fontconfig "Fontconfig")'s [<tt>30-metric-aliases.conf</tt>](https://cgit.freedesktop.org/fontconfig/tree/conf.d/30-metric-aliases.conf) and Wikipedia pages for individual fonts.

<caption>"Core fonts for the web" compatibilities</caption>
| [PostScript](#PostScript) | [URW](#PostScript) | [GUST](#TeX_Gyre) | [GNU](#GNU_FreeFont) | [Microsoft](#Microsoft) | [Liberation](#Liberation) | [CrOS](#Chrome_OS) | StarOffice |
| **Helvetica** | Nimbus Sans, A030 | TeX Gyre Heros | FreeSans | **Arial** | Liberation Sans | Arimo | Albany |
| **Times** | Nimbus Roman | TeX Gyre Termes | FreeSerif | **Times New Roman** | Liberation Serif | Tinos | Thorndale |
| **Courier** | Nimbus Mono | TeX Gyre Cursor | FreeMono | **Courier New** | Liberation Mono | Cousine | Cumberland |
| **Helvetica Condensed** | Nimbus Sans Narrow | TeX Gyre Heros Cn | **Arial Narrow** | Liberation Sans Narrow |
 **Georgia** | Gelasio |
| Wingdings (PS3) | URWDings, New Dingbats | **Wingdings** |

<caption>Microsoft Office fonts</caption>
| [Microsoft](#Microsoft) | [CrOS](#Chrome_OS) |
| **Cambria** | Caladea |
| **Calibri** | Carlito |
| **Symbol** | SymbolNeu |

<caption>Microsoft UI fonts</caption>
| [Microsoft](#Microsoft) | FOSS |
| **Segoe UI** | [Selawik](#Selawik) |
| **Tahoma** | [Wine Tahoma](#Wine_Tahoma) |

<caption>Other PostScript core families</caption>
| [PostScript](#PostScript) | [URW](#PostScript) | [GUST](#TeX_Gyre) | [Windows](#Microsoft) |
| ITC Avant Garde Gothic | URW Gothic | TeX Gyre Adventor | **Century Gothic** |
| ITC Bookman | Bookman URW | TeX Gyre Bonum | Bookman Old Style |
| ITC Zapf Chancery | Chancery URW, Z003 | TeX Gyre Chorus | Monotype Corsiva |
| **Palatino** | Palladio URW, P052 | TeX Gyre Pagella | Palatino Linotype, Book Antiqua |
| New Century Schoolbook | Century SchoolBook URW, C059 | TeX Gyre Schola | Century Schoolbook |
| ITC Zapf Dingbats | Dingbats, D050000L |

<caption>PostScript 3 Fonts</caption>
| [PostScript](#PostScript) | [URW](#PostScript) |
| **Optima** | URW Classico |
| Antique Olive | Antique Olive |
| **Univers** | URW Classic Sans, U001 |
| Clarendon Bold Condensed | Clarendon URW Bold Condensed, C011 Bold Condensed |
| Coronet | Coronet |
| Letter Gothic | Letter Gothic |
| Marigold | Mauritius |
| Albertus | Algiers, A028 |
| **Garamond** | Garamond No. 8 |

## Generic Families

### PostScript

The PostScript language defines [35 core fonts](https://en.wikipedia.org/wiki/PostScript_fonts#Core_Font_Set "wikipedia:PostScript fonts") in PostScript 2\. URW released open-source versions/clones of these 35 fonts for [w:ghostscript](https://en.wikipedia.org/wiki/ghostscript "w:ghostscript"), available as [gsfonts](https://www.archlinux.org/packages/?name=gsfonts). Projects including GUST's [TeX Gyre](#TeX_Gyre) and [GNU FreeFont](#GNU_FreeFont) release enhanced versions of these fonts.

PostScript 3 defines an additional 101 fonts, many of which are made available by URW under the [AFPL](https://en.wikipedia.org/wiki/Aladdin_Free_Public_License "wikipedia:Aladdin Free Public License") in [GhostPDL](https://ghostscript.com/doc/pcl/urwfonts/). The AFPL bars commercial use. Many of the dual font names are caused by [a batch update](http://git.ghostscript.com/?p=ghostpdl.git;a=commit;h=6f1da3c990ab7de4c3218bf8beff21f19449b284).

#### Garamond

URW's Garamond No.8 only provides one optical size (8pt). You may use [EB Garamond](https://en.wikipedia.org/wiki/EB_Garamond "wikipedia:EB Garamond") for more OpenType features, including the 12pt size.

### Microsoft

Microsoft bundles a number of fonts with Microsoft Windows and Microsoft Office. While some of these fonts are just a cheaper version (or look-alike) of corresponding PostScript families, Cambria and Calibri (default font since MS Office 2007) are independent from other families. Microsoft used to provide many core fonts in its [Core fonts for the Web](https://en.wikipedia.org/wiki/Core_fonts_for_the_Web "wikipedia:Core fonts for the Web") project. Although this project is later unavailable on Microsoft's site, the license terms that allow these fonts to be distributed from third-party sites make packages like [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) possible. See also [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts").

Prior to the introduction to Arial and Times New Roman, Microsoft used two bitmap fonts called Helv and Tms Rmn in Windows 1.0, each being unlicensed imitations of better-known fonts already covered here. They were later renamed [MS Sans Serif](https://en.wikipedia.org/wiki/MS_Sans_Serif "wikipedia:MS Sans Serif") and [MS Serif](https://en.wikipedia.org/wiki/MS_Serif "wikipedia:MS Serif") starting with Windows 3.1, and MS Sans Serif was eventually vectorized into "Microsoft Sans Serif." Documents using these fonts are rare, but user interfaces that use Microsoft Sans Serif can occasionally be found in [Mono](/index.php/Mono "Mono") libgdiplus applications. It is generally safe to assume these fonts are metric-compatible with Helvetica and Times when trying to replace them.

## Metric-compatible font projects

### TeX Gyre

[TeX Gyre](http://www.gust.org.pl/projects/e-foundry/tex-gyre/) ([tex-gyre-fonts](https://www.archlinux.org/packages/?name=tex-gyre-fonts)) is a remake and extension of the 35 base PostScript fonts distributed with Ghostscript 4.00\. The project provides TeX support and also the cross-platform OpenType format of the fonts. A related project, [TeX Gyre Math](http://www.gust.org.pl/projects/e-foundry/tg-math), provides corresponding mathematical OpenType fonts.

### GNU FreeFont

[GNU FreeFont](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)) is an outline family intended to cover as much of the UCS charset as possible. Most of the Latin characters [are from](https://www.gnu.org/software/freefont/sources/) [URW](#PostScript) (Nimbus) fonts. This set of fonts is released under GPL v3+ + FE.

### Liberation

[Liberation fonts](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") provides four families Liberation Sans, Liberation Serif, and Liberation Mono, intended to be metric-compatible with common Microsoft Windows fonts. Since version 2.0.0, this set of fonts is released under SIL OFL, and is based on [#Chrome OS](#Chrome_OS) core fonts. They are available as [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

Older, GPL-licensed versions of this font is based on Ascender Corporation's fonts, which is licensed by Red Hat, Inc. These versions of Liberation also includes Liberation Sans Narrow, which corresponds to Arial Narrow. This one font is available as [ttf-liberation-sans-narrow](https://aur.archlinux.org/packages/ttf-liberation-sans-narrow/).

### Google

Google provides a high number of [fonts](https://www.google.com/fonts), including different metric-compatible font families.

[Gelasio](http://sorkintype.com/fonts.html#gel) ([ttf-gelasio-ib](https://aur.archlinux.org/packages/ttf-gelasio-ib/)), the Google alternative for Georgia, can be found on [FontLibrary](https://fontlibrary.org/en/font/gelasio) under SIL OFL.

#### Chrome OS

Google ships open-source metric-compatible fonts with its operating system, Chrome OS, under the Apache License 2.0\. CrOS core (croscore, [ttf-croscore](https://www.archlinux.org/packages/?name=ttf-croscore)) is a collection of Arimo (sans), Tinos (serif) and Cousine (mono), also licensed from Ascender Corporation. A set of extra fonts, CrOS extra (crosextra) provides Carlito ([ttf-carlito](https://www.archlinux.org/packages/?name=ttf-carlito)) and Caladea ([ttf-caladea](https://www.archlinux.org/packages/?name=ttf-caladea)) to match default fonts for Microsoft Word.

Since glyph mappings from [Symbol](https://en.wikipedia.org/wiki/Symbol_(typeface)#HTML are usually implemented in browsers, Google no longer ships SymbolNeu in croscore > 1.23.0\. You can get this font from [croscorefonts-1.23.0.tar.gz](https://gsdview.appspot.com/chromeos-localmirror/distfiles/croscorefonts-1.23.0.tar.gz).

#### Noto

[Google's Noto Fonts](https://www.google.com/get/noto/) are available via [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts). They are licensed under SIL OFL. Noto Fonts are designed to supplement glyph coverage for Roboto ([ttf-roboto](https://www.archlinux.org/packages/?name=ttf-roboto)), the standard typeface for Android, and are vertically (i.e. same line height for the same font size) metric-compatible with Roboto.

### Other metric-compatible fonts

#### Selawik

[Selawik](https://github.com/Microsoft/Selawik) ([ttf-selawik](https://aur.archlinux.org/packages/ttf-selawik/)) is Microsoft's open-source alternative to its [Segoe UI](https://en.wikipedia.org/wiki/Segoe_UI "wikipedia:Segoe UI") font. Unfortunately it does not match Segoe UI's kerning parameters. It was developed for use in the WinJS framework, which is now abandoned.

#### Wine Tahoma

The [Wine](/index.php/Wine "Wine") project developed a metric-compatible font to replace Microsoft's [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) "wikipedia:Tahoma (typeface)"), available as [ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/). Its name in TTF data is simply "Tahoma", so there is no configuration needed.

## Example configuration

For font consistency, all applications should be set to use the serif, sans-serif, and monospace aliases, which are mapped to particular fonts by fontconfig. [Font configuration#Replace or set default fonts](/index.php/Font_configuration#Replace_or_set_default_fonts "Font configuration") explains two ways to achieve the configuration, both are covered with an example for metric-compatible fonts below.

### Example for binding method

The following example configuration uses the [#Liberation](#Liberation) fonts.

 `/etc/fonts/local.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <match target="pattern">
        <test qual="any" name="family"><string>serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Serif</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>sans-serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Sans</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>monospace</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Mono</string></edit>
    </match>
</fontconfig>
```

### Example for prefer method

The following example configuration uses the [#Chrome OS](#Chrome_OS) fonts, adding additional aliases for other fonts frequently required to refer.

 `/etc/fonts/local.conf` 
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- Prefer fonts for generics -->
  <alias>
    <family>serif</family>
    <prefer><family>Tinos</family></prefer>
  </alias>
  <alias>
    <family>sans-serif</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>sans</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer><family>Cousine</family></prefer>
  </alias>

  <!-- Map specific families to CrOS ones -->
  <match>
    <test name="family"><string>Arial</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Helvetica</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Verdana</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Tahoma</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Times New Roman</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Tinos</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Times</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Tinos</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Consolas</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Cousine</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Courier New</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Cousine</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Calibri</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Carlito</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Cambria</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Caladea</string>
    </edit>
  </match> 
</fontconfig>
```

## See also

*   [Debian Wiki - Substituting Calibri and Cambria fonts](https://wiki.debian.org/SubstitutingCalibriAndCambriaFonts "debian:SubstitutingCalibriAndCambriaFonts")