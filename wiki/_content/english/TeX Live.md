Related articles

*   [TeX Live FAQ](/index.php/TeX_Live_FAQ "TeX Live FAQ")
*   [TeX Live and CJK](/index.php/TeX_Live_and_CJK "TeX Live and CJK")
*   [List of applications/Documents#TeX editors](/index.php/List_of_applications/Documents#TeX_editors "List of applications/Documents")

According to [Wikipedia](https://en.wikipedia.org/wiki/TeX_Live "wikipedia:TeX Live"):

	**TeX Live** is a free software distribution for the [TeX](https://en.wikipedia.org/wiki/TeX "wikipedia:TeX") typesetting system that includes major TeX-related programs, macro packages, and fonts.

TeX Live includes the [tex(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tex.1) and [pdftex(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdftex.1) programs, the [LaTeX](https://en.wikipedia.org/wiki/LaTeX "wikipedia:LaTeX") and [ConTeXt](https://en.wikipedia.org/wiki/ConTeXt "wikipedia:ConTeXt") TeX macro packages and the [XeTeX](https://en.wikipedia.org/wiki/XeTeX "wikipedia:XeTeX") and [LuaTeX](https://en.wikipedia.org/wiki/LuaTeX "wikipedia:LuaTeX") TeX engines.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 TeXLive Local Manager](#TeXLive_Local_Manager)
    *   [1.2 Manual installation](#Manual_installation)
*   [2 Usage](#Usage)
    *   [2.1 CTAN](#CTAN)
    *   [2.2 texmf trees](#texmf_trees)
*   [3 Important information](#Important_information)
    *   [3.1 Paper size](#Paper_size)
    *   [3.2 Error with "formats not generated" upon update](#Error_with_.22formats_not_generated.22_upon_update)
    *   [3.3 Fonts](#Fonts)
*   [4 Install .sty files](#Install_.sty_files)
    *   [4.1 Manual Installation](#Manual_Installation_2)
    *   [4.2 Using PKGBUILDs](#Using_PKGBUILDs)
*   [5 Updating babelbib language definitions](#Updating_babelbib_language_definitions)
*   [6 See also](#See_also)

## Installation

The TeX Live packages are arranged into two [package groups](/index.php/Package_group "Package group"):

*   [texlive-most](https://www.archlinux.org/groups/x86_64/texlive-most/) includes TeX Live applications.
*   [texlive-lang](https://www.archlinux.org/groups/x86_64/texlive-lang/) provides various character sets and non-English features.

The essential package [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) contains the basic *TEXMFDIST* tree, while [texlive-bin](https://www.archlinux.org/packages/?name=texlive-bin) contains the binaries and libraries. [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) is based on the "medium" install scheme of the upstream distribution. All other packages are based on the eponymous collections in TeX Live. To determine which CTAN packages are included in each package, look up the files `/var/lib/texmf/arch/installedpkgs/<package>_<revnr>.pkgs`.

The [texlive-langextra](https://www.archlinux.org/packages/?name=texlive-langextra) package provides language support for African, Arabic, Armenian, Croatian, Hebrew, Indic, Mongolian, Tibetan and Vietnamese.

You additionally may want to install a [TeX editor](/index.php/List_of_applications/Documents#TeX_editors "List of applications/Documents").

### TeXLive Local Manager

[texlive-localmanager-git](https://aur.archlinux.org/packages/texlive-localmanager-git/) is a utility which allows to conveniently manage a TeX Live installation on Arch Linux. See [Usage](https://git.archlinux.org/users/remy/texlive-localmanager.git/tree/tllocalmgr#n809) for details.

### Manual installation

Alternatively you can install TeX Live with the upstream installer, which is packaged as [texlive-installer](https://aur.archlinux.org/packages/texlive-installer/). For more information, see the [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Custom_installation_with_TeX_Live "wikibooks:LaTeX/Installation") and the [TeX Live Guide](https://tug.org/texlive/doc/texlive-en/texlive-en.html#x1-140003).

## Usage

### CTAN

[CTAN](https://www.ctan.org/) is the cen­tral place for all kinds of ma­te­rial around TeX.

### texmf trees

See the [TeX Live Guide](https://www.tug.org/texlive/doc/texlive-en/texlive-en.html#x1-110002.3) and the [TeX Directory Structure](https://tug.org/tds/).

The following table lists the texmf trees in the reverse order they are searched (later trees override earlier ones).

| Variables | Arch default [[1]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/texmf.cnf?h=packages/texlive-core) | Description |
| TEXMFDIST | /usr/share/texmf-dist | files of the original distribution |
| TEXMFLOCAL | /usr/local/share/texmf:/usr/share/texmf | used by administrators for system-wide installation of additional or updated macros, fonts, etc. |
| TEXMFSYSVAR | /var/lib/texmf | used by [updmap-sys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updmap-sys.1) and [fmtutil-sys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fmtutil-sys.1) to store (cached) runtime data |
| TEXMFSYSCONFIG | /etc/texmf | used by [updmap-sys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updmap-sys.1) and [fmtutil-sys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fmtutil-sys.1) to store modified configuration data |
| TEXMFHOME | ~/texmf | used by users for their own individual installations of additional or updated macros, fonts, etc. |
| TEXMFVAR | ~/.texlive/texmf-var | used by [updmap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updmap.1) and [fmtutil(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fmtutil.1) to store (cached) runtime data |
| TEXMFCONFIG | ~/.texlive/texmf-config | used by [updmap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updmap.1) and [fmtutil(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fmtutil.1) to store modified configuration data |
| TEXMFCACHE | $TEXMFSYSVAR;$TEXMFVAR | used by ConTEXt MkIV and LuaLATEX to store (cached) runtime data |

The default values are defined in `/etc/texmf/web2c/texmf.cnf`, they can be overridden with [environment variables](/index.php/Environment_variables "Environment variables").

You can also find out the value of a variable with `kpsewhich -var *VARIABLE*`.

## Important information

*   The [biber](https://www.archlinux.org/packages/?name=biber) utility used to handle [biblatex](https://ctan.org/pkg/biblatex) bibliography is provided as a separate package.
*   The way to handle font mappings for [updmap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updmap.1) was improved in September 2009, and installation should now be much more reliable than in the past. In the meantime, if you encounter error messages about unavailable map files, simply remove them by hand from the `updmap.cfg` file (ideally using `updmap-sys --edit`). You can also run `updmap-sys --syncwithtrees` to automatically comment out outdated map lines from the config file.
*   The ConTeXt formats (for Mark II and IV) are not automatically generated upon installation. See [the ConTeXT wiki](http://wiki.contextgarden.net) for instructions on how to do this.
*   The packages containing the documentation and sources are **no longer available** in official repositories. You can locally build them with [tllocalmgr](#TeXLive_Local_Manager). You can also consult documentation online at [https://tug.org/texlive/Contents/live/doc.html](https://tug.org/texlive/Contents/live/doc.html) or on CTAN. Another possibility is using the online documentation at `http://texdoc.net/pkg/packagename` which resolves to the relevant pdf for `packagename`, similar to the command line tool `texdoc` (which is useless without locally installed documentation). The documentation is now contained in [texlive-most-doc](https://aur.archlinux.org/packages/texlive-most-doc/).
*   TeX Live (upstream) now provides a tool for incremental updates of CTAN packages. On that basis, we also plan to update our packages on a regular basis (we have written tools that almost automate that task).
*   Some tools and utilities included in TeX Live rely on [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), [perl](https://www.archlinux.org/packages/?name=perl), [python2](https://www.archlinux.org/packages/?name=python2), and [ruby](https://www.archlinux.org/packages/?name=ruby).
*   For help and information about TeX Live see: [https://tug.org/texlive/doc.html](https://tug.org/texlive/doc.html) and [https://tug.org/texlive/doc/texlive-en/texlive-en.html](https://tug.org/texlive/doc/texlive-en/texlive-en.html)

### Paper size

It is currently impossible to set the default page size, because the Arch package removes the tool necessary for this, see [FS#59094](https://bugs.archlinux.org/task/59094).

Usually, you would run the `texconfig` command, which is also capable of changing other useful settings.

### Error with "formats not generated" upon update

See [this bug report](https://bugs.archlinux.org/task/16467). (**Note that if you do not use the experimental engine *LuaTeX*, you can ignore this.**) This situation typically occurs when the configuration files `language.def` and/or `language.dat` for hyphenation patterns contain references to files from earlier releases of `texlive-core`, in particular to the latest experimental hyphenation patterns for German, whose file name changes frequently. Currently they should point to `dehyph{n,t}-x-2009-06-19.tex`.

To solve this, you need to either remove these files: `/usr/share/texmf-config/tex/generic/config/language.{def,dat}` or update them using the newest version under: `/usr/share/texmf/tex/generic/config/language.{def,dat}` and then run

```
# fmtutil-sys --missing

```

### Fonts

By default, the fonts that come with the various TeX Live packages are not automatically available to Fontconfig. If you want to use them with, say XeTeX or [LibreOffice](/index.php/LibreOffice "LibreOffice"), the easiest approach is to make symlinks as follows:

```
 ln -s /usr/share/texmf-dist/fonts/opentype/public/<some_fonts_you_want> ~/.fonts/OTF/ (or TTF or Type1) 

```

To make them available to fontconfig, run:

```
 fc-cache ~/.fonts
 mkfontscale ~/.fonts/OTF (or TTF or Type1) 
 mkfontdir ~/.fonts/OTF (or TTF or Type1)

```

Alternatively, [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) contains the file `/etc/fonts/conf.avail/09-texlive-fonts.conf` that contains a list of the font directories used by TeX Live. You can use this file with:

 `# ln -s /etc/fonts/conf.avail/09-texlive-fonts.conf /etc/fonts/conf.d/09-texlive-fonts.conf` 

And then update fontconfig:

 `# fc-cache && mkfontscale && mkfontdir` 
**Note:** This may cause conflicts with XeTeX/XeLaTeX if the same fonts are (separately) available to both TeX and Fontconfig, i.e. if multiple copies of the same font are available on the search path.

## Install .sty files

TeX Live (and teTeX) uses its own directory indexes (files named `ls-R`), and you need to refresh them after you copy something into one of the TeX trees. Or TeX can not see them. Magic command:

 `# mktexlsr` 

or

 `# texhash` 

or

 `# texconfig[-sys] rehash` 

A command line program to search through these indexes is

```
kpsewhich

```

Hence you can check that TeX can find a particular file by running

```
kpsewhich <filename.sty>

```

The output should be the full path to that file.

Alternatively, sty files that are intended only for a particular user should go in the `~/texmf/` tree. For instance, the latex package wrapfig consists of the file `wrapfig.sty` and would go in `~/texmf/tex/latex/wrapfig/wrapfig.sty`. There is no need to run `mktexlsr` or equivalent because `~/texmf` is searched every time tex is run.

### Manual Installation

You should **not** manually install files into `/usr/share/texmf-dist/tex/latex/<package name>/*`. Instead, install local *.sty* files in `TEXMFLOCAL`, if they should be available to all users, or into `TEXMFHOME`, if they are specific to you. Use `kpsewhich -var TEXMFLOCAL` to get the local directory and install into `<local directory>/tex/latex/<package name>/`. The `TEXMFHOME` directory will automatically be searched when TeX tools are executed. If you use `TEXMFLOCAL`, you need to update the database as described above in order for the files to be found.

### Using PKGBUILDs

To install a LaTeX package on a global level, you should use a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for the sake of simplifying maintenance. Examples can be found in the [AUR](/index.php/AUR "AUR"), e.g. [texlive-gantt](https://aur.archlinux.org/packages/texlive-gantt/).

## Updating babelbib language definitions

If you have the very specific problem of [babelbib](https://www.ctan.org/pkg/babelbib) not having the latest language definitions that you need, and you do not want to recompile everything, you can get them manually from [https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/](https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/) and put them in `/usr/share/texmf-dist/tex/latex/babelbib/`. For example:

```
# cd /usr/share/texmf-dist/tex/latex/babelbib/ 
# wget [https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/romanian.bdf](https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/romanian.bdf)
# wget [...all-other-language-files...]
# wget [https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/babelbib.sty](https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/babelbib.sty)

```

Afterwards, you need to run `texhash` to update the TeX database:

```
# texhash

```

## See also

*   [The TeX Live Guide](https://www.tug.org/texlive/doc/texlive-en/texlive-en.html)
*   [Wikibooks:LaTeX](https://en.wikibooks.org/wiki/LaTeX "wikibooks:LaTeX")
*   [The Not So Short In­tro­duc­tion to LaTeX 2ε](https://tobi.oetiker.ch/lshort/lshort.pdf)