Related articles

*   [TeX Live FAQ](/index.php/TeX_Live_FAQ "TeX Live FAQ")
*   [TeX Live and CJK](/index.php/TeX_Live_and_CJK "TeX Live and CJK")

According to [Wikipedia](https://en.wikipedia.org/wiki/TeX_Live "wikipedia:TeX Live"):

	**TeX Live** is a free software distribution for the [TeX](https://en.wikipedia.org/wiki/TeX "wikipedia:TeX") typesetting system that includes major TeX-related programs, macro packages, and fonts.

TeX Live includes the [tex(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tex.1) and [pdftex(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdftex.1) programs, the [LaTeX](https://en.wikipedia.org/wiki/LaTeX "wikipedia:LaTeX") and [ConTeXt](https://en.wikipedia.org/wiki/ConTeXt "wikipedia:ConTeXt") TeX macro packages and the [XeTeX](https://en.wikipedia.org/wiki/XeTeX "wikipedia:XeTeX") and [LuaTeX](https://en.wikipedia.org/wiki/LuaTeX "wikipedia:LuaTeX") TeX engines.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 tllocalmgr](#tllocalmgr)
    *   [1.2 Package documentation](#Package_documentation)
    *   [1.3 Manual installation](#Manual_installation)
*   [2 Usage](#Usage)
    *   [2.1 texmf trees and Kpathsea](#texmf_trees_and_Kpathsea)
*   [3 Important information](#Important_information)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Changing default paper size](#Changing_default_paper_size)
    *   [4.2 Making fonts available to Fontconfig](#Making_fonts_available_to_Fontconfig)
    *   [4.3 Updating babelbib language definitions](#Updating_babelbib_language_definitions)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Error with "formats not generated" upon update](#Error_with_.22formats_not_generated.22_upon_update)
*   [6 See also](#See_also)

## Installation

*   The [texlive-most](https://www.archlinux.org/groups/x86_64/texlive-most/) group contains most TeX Live packages.
    *   [texlive-core](https://www.archlinux.org/packages/?name=texlive-core), the essential package, based on the *medium* upstream install scheme (all other packages are based on the upstream collections). The package includes [pacman hooks](/index.php/Pacman_hook "Pacman hook") to automate *mktexlsr*, *fmtutil* and *updmap*.[[1]](https://git.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/texlive-core)
    *   [texlive-bin](https://www.archlinux.org/packages/?name=texlive-bin) contains the binaries and libraries (it is a dependency of [texlive-core](https://www.archlinux.org/packages/?name=texlive-core)).
*   The [texlive-lang](https://www.archlinux.org/groups/x86_64/texlive-lang/) group contains packages providing character sets and features for non-English languages.
    *   [texlive-langextra](https://www.archlinux.org/packages/?name=texlive-langextra) provides language support for African, Arabic, Armenian, Croatian, Hebrew, Indic, Mongolian, Tibetan and Vietnamese.
*   The [biber](https://www.archlinux.org/packages/?name=biber) utility used to handle [biblatex](https://ctan.org/pkg/biblatex) bibliography is provided as a separate package.

To determine which [CTAN](https://www.ctan.org/) packages are included in each *texlive-* package, look up the files `/var/lib/texmf/arch/installedpkgs/<package>_<revnr>.pkgs`.

**Note:** Some tools and utilities included in TeX Live rely on [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), [perl](https://www.archlinux.org/packages/?name=perl), [python2](https://www.archlinux.org/packages/?name=python2), or [ruby](https://www.archlinux.org/packages/?name=ruby).

**Tip:** You may want to install a [TeX editor](/index.php/List_of_applications/Documents#TeX_editors "List of applications/Documents").

### tllocalmgr

The `tllocalmgr` utility, provided by [texlive-localmanager-git](https://aur.archlinux.org/packages/texlive-localmanager-git/), lets you install (and update) packages from CTAN as [pacman](/index.php/Pacman "Pacman") packages, see [its usage](https://git.archlinux.org/users/remy/texlive-localmanager.git/tree/tllocalmgr#n809) (`-h`) for details.

### Package documentation

The packages in the official repositories do not contain the documentation or source files of font/macro packages.

For offline access with `texdoc` you can either [install](/index.php/Install "Install") the whole TeX Live documentation and source files with [texlive-most-doc](https://aur.archlinux.org/packages/texlive-most-doc/) or install documentation of specific packages with *tllocalmgr*.

You can also access the documentation online at:

*   [https://tug.org/texlive/Contents/live/doc.html](https://tug.org/texlive/Contents/live/doc.html)
*   [https://ctan.org/](https://ctan.org/) – the cen­tral place for all kinds of ma­te­rial around TeX
*   [http://texdoc.net/](http://texdoc.net/) (`http://texdoc.net/pkg/*packagename*` directly yields the relevant PDF)

### Manual installation

Alternatively you can install TeX Live with the upstream installer, which is packaged as [texlive-installer](https://aur.archlinux.org/packages/texlive-installer/). For more information, see the [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Custom_installation_with_TeX_Live "wikibooks:LaTeX/Installation") and the [TeX Live Guide](https://tug.org/texlive/doc/texlive-en/texlive-en.html#x1-140003).

## Usage

**Note:**

*   While [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) provides the [tlmgr](https://www.tug.org/texlive/tlmgr.html) script in *TEXMFDIST* it is broken. For package installations you can use [tllocalmgr](#tllocalmgr) instead.
*   The [texconfig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/texconfig.1) command is mostly broken because it partially depends on *tlmgr* ([FS#59094](https://bugs.archlinux.org/task/59094)). The interactive mode of `texconfig` requires [dialog](https://www.archlinux.org/packages/?name=dialog).

See the following resources:

*   [Wikibooks:LaTeX](https://en.wikibooks.org/wiki/LaTeX "wikibooks:LaTeX")
*   [The Not So Short In­tro­duc­tion to LaTeX 2ε](https://tobi.oetiker.ch/lshort/lshort.pdf)
*   [Getting to Grips with LaTeX – Andrew Roberts](https://www.andy-roberts.net/writing/latex)
*   [The TeX FAQ](https://texfaq.org/)

### texmf trees and Kpathsea

texmf trees (*texmf* stands for TeX and [Metafont](https://en.wikipedia.org/wiki/Metafont "wikipedia:Metafont")) should follow the [TeX Directory Structure](https://tug.org/tds/), or files may not be found.[[2]](https://www.tug.org/texlive/doc/texlive-en/texlive-en.html#x1-110002.3)

TeX Live uses the [Kpathsea](https://tug.org/texinfohtml/kpathsea.html) library to lookup paths by filename across multiple texmf trees and the current working directory.

Kpathsea searches the following variables in the reverse order (later trees override earlier ones).

| Variables | Arch default  | Used by [[3]](https://www.tug.org/texlive/doc/texlive-en/texlive-en.html#x1-110002.3) |
| TEXMFDIST | /usr/share/texmf-dist | files of the original distribution |
| TEXMFLOCAL | /usr/local/share/texmf:/usr/share/texmf | administrators for system-wide installation of additional or updated macros, fonts, etc. |
| TEXMFSYSVAR | /var/lib/texmf | updmap and fmtutil (user mode) to store (cached) runtime data |
| TEXMFSYSCONFIG | /etc/texmf | updmap and fmtutil (user mode) to store modified configuration data |
| TEXMFHOME | ~/texmf | users for their own individual installations of additional or updated macros, fonts, etc. |
| TEXMFVAR | ~/.texlive/texmf-var | updmap and fmtutil (sys mode) to store (cached) runtime data |
| TEXMFCONFIG | ~/.texlive/texmf-config | updmap and fmtutil (sys mode) to store modified configuration data |
| TEXMFCACHE | $TEXMFSYSVAR;$TEXMFVAR | ConTeXt MkIV and LuaLaTeX to store (cached) runtime data |

1.  The default values are defined in `/etc/texmf/web2c/texmf.cnf`[[4]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/texmf.cnf?h=packages/texlive-core), they can be overridden with [environment variables](/index.php/Environment_variables "Environment variables").

Kpathsea provides the [kpsewhich(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/kpsewhich.1) command to lookup paths. When run with the `-var` argument it can also print the values of variables.

Kpathsea uses filename databases (`ls-R`) to speed up searches in system-wide texmf trees (configured with the *TEXMFDBS* variable). This means that when system-wide file trees are changed, [mktexlsr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mktexlsr.1) or `texhash` (a symlink) need to be run as [root](/index.php/Root_user "Root user"). Fortunately the [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) automates this with a [pacman hook](/index.php/Pacman_hook "Pacman hook") targeting all default system-wide texmf trees but `/usr/local/share/texmf`.[[5]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/mktexlsr.hook?h=packages/texlive-core) So as long as you install system-wide packages via [pacman](/index.php/Pacman "Pacman") you should not need to run *mktexlsr* or *texhash* at all.

## Important information

*   The ConTeXt formats (for Mark II and IV) are not automatically generated upon installation. See [the ConTeXT wiki](http://wiki.contextgarden.net) for instructions on how to do this.
*   TeX Live (upstream) now provides a tool for incremental updates of CTAN packages. On that basis, we also plan to update our packages on a regular basis (we have written tools that almost automate that task).
*   The way to handle font mappings for [updmap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updmap.1) was improved in September 2009, and installation should now be much more reliable than in the past. In the meantime, if you encounter error messages about unavailable map files, simply remove them by hand from the `updmap.cfg` file (ideally using `updmap-sys --edit`). You can also run `updmap-sys --syncwithtrees` to automatically comment out outdated map lines from the config file.

## Tips and tricks

### Changing default paper size

It is currently impossible to set the default page size, because the Arch package removes the tool necessary for this, see [FS#59094](https://bugs.archlinux.org/task/59094).

Usually, you would run the `texconfig` command, which is also capable of changing other useful settings.

### Making fonts available to Fontconfig

By default, the fonts that come with the various TeX Live packages are not automatically available to [Fontconfig](/index.php/Fontconfig "Fontconfig"). If you want to use them with, say XeTeX or [LibreOffice](/index.php/LibreOffice "LibreOffice"), the easiest approach is to make symlinks as follows:

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

### Updating babelbib language definitions

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

## Troubleshooting

### Error with "formats not generated" upon update

See [FS#16467](https://bugs.archlinux.org/task/16467). (Note that if you do not use the experimental engine *LuaTeX*, you can ignore this.) This situation typically occurs when the configuration files `language.def` and/or `language.dat` for hyphenation patterns contain references to files from earlier releases of [texlive-core](https://www.archlinux.org/packages/?name=texlive-core), in particular to the latest experimental hyphenation patterns for German, whose file name changes frequently. Currently they should point to `dehyph{n,t}-x-2009-06-19.tex`.

To solve this, you need to either remove these files: `/etc/texmf/tex/generic/config/language.{def,dat}` or update them using the newest version under: `/usr/share/texmf/tex/generic/config/language.{def,dat}` and then run

```
# fmtutil-sys --missing

```

## See also

*   [TeX Live documentation](https://tug.org/texlive/doc.html)
*   [The TeX Live Guide](https://tug.org/texlive/doc/texlive-en/texlive-en.html) (not completely applicable)
*   [TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/)