[TeX Live](https://www.tug.org/texlive/) is an "easy way to get up and running with the [TeX](https://en.wikipedia.org/wiki/TeX "wikipedia:TeX") document production system. It provides a comprehensive TeX system with binaries for most flavors of Unix, including GNU/Linux, and also Windows. It includes all the major TeX-related programs, macro packages, and fonts that are free software, including support for many languages around the world."

TeX Live is one of the most popular distributions for [LaTeX](https://en.wikipedia.org/wiki/LaTeX "wikipedia:LaTeX"), [ConTeXt](https://en.wikipedia.org/wiki/ConTeXt "wikipedia:ConTeXt") and friends.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Manual installation](#Manual_installation)
*   [2 Usage](#Usage)
*   [3 Important information](#Important_information)
    *   [3.1 Paper size](#Paper_size)
    *   [3.2 Error with "formats not generated" upon update](#Error_with_.22formats_not_generated.22_upon_update)
    *   [3.3 Fonts](#Fonts)
*   [4 TeXLive Local Manager](#TeXLive_Local_Manager)
*   [5 Install .sty files](#Install_.sty_files)
    *   [5.1 Manual Installation](#Manual_Installation_2)
    *   [5.2 Using PKGBUILDs](#Using_PKGBUILDs)
*   [6 Updating babelbib language definitions](#Updating_babelbib_language_definitions)

## Installation

The TeX Live packages are arranged into two groups in the [official repositories](/index.php/Official_repositories "Official repositories"):

*   [texlive-most](https://www.archlinux.org/groups/x86_64/texlive-most/) includes TeX Live applications.
*   [texlive-lang](https://www.archlinux.org/groups/x86_64/texlive-lang/) provides various character sets and non-English features.

The essential package [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) contains the basic texmf-dist tree, while [texlive-bin](https://www.archlinux.org/packages/?name=texlive-bin) contains the binaries, libraries, and the texmf tree. [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) is based on the “medium” install scheme of the upstream distribution. All other packages are based on the eponymous collections in TeX Live. To determine which CTAN packages are included in each package, lookup the files:

```
 /var/lib/texmf/arch/installedpkgs/<package>_<revnr>.pkgs

```

**Note:** [texlive-langextra](https://www.archlinux.org/packages/?name=texlive-langextra) provides language support for African, Arabic, Armenian, Croatian, Hebrew, Indic, Mongolian, Tibetan and Vietnamese.

### Manual installation

See the [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Custom_installation_with_TeX_Live) and [TeX Live Guide](https://tug.org/texlive/doc/texlive-en/texlive-en.html#x1-140003). For programs that require TeX Live to be installed (e.g. kile) you can use the [texlive-dummy](https://aur.archlinux.org/packages/texlive-dummy/) package.

## Usage

You can test your installation with

```
$ tex '\empty Hello world!\bye'
$ pdftex '\empty Hello world!\bye'

```

You should get a DVI or a PDF file accordingly.

You will probably want a [TeX editor](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents"). There are also a few online solutions that let you create TeX-based documents without TeX Live. See the [LaTeX wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Online_solutions).

## Important information

*   The [biber](https://www.archlinux.org/packages/?name=biber) utility used to handle biblatex bibliography is provided as a separate package.

*   The way to handle font mappings for updmap was improved in September 2009, and installation should now be much more reliable than in the past. In the meantime, if you encounter error messages about unavailable map files, simply remove them by hand from the `updmap.cfg` file (ideally using `updmap-sys --edit`). You can also run `updmap-sys --syncwithtrees` to automatically comment out outdated map lines from the config file.

*   The ConTeXt formats (for MKII and MKIV) are not automatically generated upon installation. See [the ConTeXT wiki](http://wiki.contextgarden.net) for instructions on how to do this.

*   The packages containing the documentation and sources are **no longer available** in official repositories. You can locally build them with [tllocalmgr](#TeXLive_Local_Manager). You can also consult documentation online at [https://tug.org/texlive/Contents/live/doc.html](https://tug.org/texlive/Contents/live/doc.html) or on CTAN. Another possibility is using the online documentation at `http://texdoc.net/pkg/packagename` which resolves to the relevant pdf for `packagename`, similar to the command line tool `texdoc` (which is useless without locally installed documentation).

*   TeX Live (upstream) now provides a tool for incremental updates of CTAN packages. On that basis, we also plan to update our packages on a regular basis (we have written tools that almost automate that task).

*   Some tools and utilities included in TeX Live rely on [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), [perl](https://www.archlinux.org/packages/?name=perl), [python2](https://www.archlinux.org/packages/?name=python2), and [ruby](https://www.archlinux.org/packages/?name=ruby).

*   For help and information about TeX Live see: [https://tug.org/texlive/doc.html](https://tug.org/texlive/doc.html) and [https://tug.org/texlive/doc/texlive-en/texlive-en.html](https://tug.org/texlive/doc/texlive-en/texlive-en.html)

*   System-wide configuration files are under `/usr/share/texmf-config`. User-specific ones should be put under `~/.texlive/texmf-config`. `$TEXMFHOME` is `~/texmf` and `$TEXMFVAR` is `~/.texlive/texmf-var`.

*   A skeleton of a local texmf tree is at `/usr/local/share/texmf`: this directory is writable for members of the group **tex**.

### Paper size

If you would like to set the default page size to something other than A4 (such as "Letter"), run the `texconfig` command. This command is also capable of changing other useful settings.

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

## TeXLive Local Manager

[texlive-localmanager-git](https://aur.archlinux.org/packages/texlive-localmanager-git/) is a utility which allows to conveniently manage a TeX Live installation on Arch Linux. See [Usage](https://git.archlinux.org/users/remy/texlive-localmanager.git/tree/tllocalmgr#n809) for details.

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

If you have the very specific problem of babelbib not having the latest language definitions that you need, and you do not want to recompile everything, you can get them manually from [https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/](https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/) and put them in `/usr/share/texmf-dist/tex/latex/babelbib/`. For example:

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