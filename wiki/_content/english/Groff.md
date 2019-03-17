Related articles

*   [Man page](/index.php/Man_page "Man page")

According to [Wikipedia](https://en.wikipedia.org/wiki/Groff_(software) "wikipedia:Groff (software)"):

	**Groff (GNU troff)** is a typesetting system that reads plain text mixed with formatting commands and produces formatted output.

Output may be [PostScript](/index.php/PostScript "PostScript") or PDF, html, or ASCII/UTF8 for display at the terminal. Formatting commands may be either low-level typesetting requests (“primitives”) or macros from a supplied set. Users may also write their own macros. All three may be combined. Using groff may be a solid alternative to [TeX_Live](/index.php/TeX_Live "TeX Live") due to small size and native language.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Package documentation](#Package_documentation)
*   [2 Usage](#Usage)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Adding support for cyrillic fonts](#Adding_support_for_cyrillic_fonts)
*   [4 See also](#See_also)

## Installation

You may find groff package already installed on your system as it is a part of [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group in core repository. Otherwise install it with pacman as usual.

### Package documentation

Groff's detailed documentation and usage examples are available via [info](/index.php/Info "Info") package:

```
 info groff

```

Manpages also contain general information, use:

```
 man groff

```

You can also access the documentation online at:

*   [https://www.gnu.org/software/groff/groff.html#documentation](https://www.gnu.org/software/groff/groff.html#documentation)

## Usage

Groff is a powerful and yet lightweight easy to use system. You can see an example of document created in groff [here](https://www.troff.org/TheGroffFriendsHowto.pdf).

This was made with **-me** macros, however, groff has several built-in macros as well.

You may be interested in using **ms** for not complicated tasks or **mom** to produce scientific papers. See:

```
 man 7 groff_ms
 man 7 groff_mom

```

See the following resources for feature information:

*   [The Groff and Friends HOWTO](https://www.troff.org/TheGroffFriendsHowto.pdf)
*   [Creating Documents in Groff or LaTeX](http://etutorials.org/Linux+systems/red+hat+linux+bible+fedora+enterprise+edition/Part+II+Using+Red+Hat+Linux/Chapter+6+Publishing+with+Red+Hat+Linux/Creating+Documents+in+Groff+or+LaTeX/)
*   [Mom macros examples](https://www.schaffter.ca/mom/mom-04.html#examples)

## Tips and tricks

### Adding support for cyrillic fonts

If you see inappropriate symbols when output documents with cyrillic fonts to ps or pdf, make following steps:

*   Download type1 fonts with cyrillic support (for example from [here](ftp://ftp.kapella.gpi.ru/pub/cyrillic/psfonts) Arial, Times, Courier, read README.html)
*   Place your cyrillic type1 fonts into `/usr/share/fonts/gsfonts` -- this is default folder for ghostscript to find fonts
*   Change ghostscript fontmap file to associate default fonts with cyrillic ones in `/usr/share/ghostscript/%YOUR_VERSION%/Resource/Init/Fontmap.GS`

```
 cd `/usr/share/ghostscript/%YOUR_VERSION%/Resource/Init/`
 cp Fontmap.GS Fontmap.GS.backup
 vim Fontmap.GS

```

*   Use '%' to comment lines with default associations. Place below new aliases, as follows:

```
 %/Times-Roman /NimbusRoman-Regular ;
 /Times-Roman  /TimesNRCyrMT ;
 /TimesNRCyrMT (times8.pfb) ;

```

Where '(times8.pfb)' is a name of your copied type1 font.

*   From now on you can prepend your default groff command with [iconv](/index.php/Iconv "Iconv") prefix to print cyrillic symbols in ps files:

```
 iconv -f utf-8 -t koi8-r test.ms | groff -ms -Tps > test.ps && ps2pdf test.ps test.pdf

```

## See also

*   [Groff parser and template engines for Rails](https://github.com/guillermo/groff)
*   [Mom macros](http://pipeline.lbl.gov/code/3rd_party/licenses.win/groff/1.19.2/html/mom/toc.html)
*   [Mom macros full manual](https://tools.ietf.org/doc/groff/html/mom/toc.html)