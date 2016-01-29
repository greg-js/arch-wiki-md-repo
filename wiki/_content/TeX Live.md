# TeX Live

Related articles

*   [TeX Live FAQ](/index.php/TeX_Live_FAQ "TeX Live FAQ")
*   [TeX Live and CJK](/index.php/TeX_Live_and_CJK "TeX Live and CJK")
*   [Ooolatex](/index.php/Ooolatex "Ooolatex")
*   [List of applications/Documents#Scientific_documents](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents")

[TeX Live](https://www.tug.org/texlive/) is an "easy way to get up and running with the [TeX](https://en.wikipedia.org/wiki/TeX "wikipedia:TeX") document production system. It provides a comprehensive TeX system with binaries for most flavors of Unix, including GNU/Linux, and also Windows. It includes all the major TeX-related programs, macro packages, and fonts that are free software, including support for many languages around the world."

TeX Live is one of the most popular distribution for [LaTeX](https://en.wikipedia.org/wiki/LaTeX "wikipedia:LaTeX"), [ConTeXt](https://en.wikipedia.org/wiki/ConTeXt "wikipedia:ConTeXt") and friends.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 texlive-most](#texlive-most)
    *   [1.2 texlive-lang](#texlive-lang)
    *   [1.3 Manual installation](#Manual_installation)
*   [2 Usage](#Usage)
*   [3 Important information](#Important_information)
    *   [3.1 Paper Size](#Paper_Size)
    *   [3.2 Error with "formats not generated" upon update](#Error_with_.22formats_not_generated.22_upon_update)
    *   [3.3 Fonts](#Fonts)
*   [4 TeXLive Local Manager](#TeXLive_Local_Manager)
    *   [4.1 Recent "langukenglish" errors](#Recent_.22langukenglish.22_errors)
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

### texlive-most

| 

*   [texlive-core](https://www.archlinux.org/packages/?name=texlive-core)
*   [texlive-bibtexextra](https://www.archlinux.org/packages/?name=texlive-bibtexextra)
*   [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra)
*   [texlive-formatsextra](https://www.archlinux.org/packages/?name=texlive-formatsextra)
*   [texlive-games](https://www.archlinux.org/packages/?name=texlive-games)

 | 

*   [texlive-genericextra](https://www.archlinux.org/packages/?name=texlive-genericextra)
*   [texlive-htmlxml](https://www.archlinux.org/packages/?name=texlive-htmlxml)
*   [texlive-humanities](https://www.archlinux.org/packages/?name=texlive-humanities)
*   [texlive-latexextra](https://www.archlinux.org/packages/?name=texlive-latexextra)
*   [texlive-music](https://www.archlinux.org/packages/?name=texlive-music)

 | 

*   [texlive-pictures](https://www.archlinux.org/packages/?name=texlive-pictures)
*   [texlive-plainextra](https://www.archlinux.org/packages/?name=texlive-plainextra)
*   [texlive-pstricks](https://www.archlinux.org/packages/?name=texlive-pstricks)
*   [texlive-publishers](https://www.archlinux.org/packages/?name=texlive-publishers)
*   [texlive-science](https://www.archlinux.org/packages/?name=texlive-science)

 |

### texlive-lang

*   [texlive-langchinese](https://www.archlinux.org/packages/?name=texlive-langchinese)
*   [texlive-langcyrillic](https://www.archlinux.org/packages/?name=texlive-langcyrillic)
*   [texlive-langgreek](https://www.archlinux.org/packages/?name=texlive-langgreek)
*   [texlive-langjapanese](https://www.archlinux.org/packages/?name=texlive-langjapanese)
*   [texlive-langkorean](https://www.archlinux.org/packages/?name=texlive-langkorean)
*   [texlive-langextra](https://www.archlinux.org/packages/?name=texlive-langextra)

**Note:** [texlive-langextra](https://www.archlinux.org/packages/?name=texlive-langextra) provides language support for African, Arabic, Armenian, Croatian, Hebrew, Indic, Mongolian, Tibetan and Vietnamese.

### Manual installation

See the [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Custom_installation_with_TeX_Live) and [TeX Live Guide](https://tug.org/texlive/doc/texlive-en/texlive-en.html#x1-140003). For programs that require TeX Live to be installed (e.g. kile) you can use the [texlive-dummy](https://aur.archlinux.org/packages/texlive-dummy/)<sup><small>AUR</small></sup> package.

## Usage

You can test your installation with

```
$ tex '\empty Hello world!\bye'
$ pdftex '\empty Hello world!\bye'

```

You should get a DVI or a PDF file accordingly.

You will probably want a [TeX editor](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents").

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Wikibooks:LaTeX/Installation#Online_solutions](https://en.wikibooks.org/wiki/LaTeX/Installation#Online_solutions "wikibooks:LaTeX/Installation").**

**Notes:** Inappropriate here (Discuss in [Talk:TeX Live#LaTeX merge](https://wiki.archlinux.org/index.php/Talk:TeX_Live#LaTeX_merge))

There are also a few online solutions that let you create TeX-based documents without TeX Live:

*   **Authorea** — Online collaborative editor for scientific, academic, and technical documents.

NaN

*   **ShareLaTeX** — An open source online LaTeX editor. You can either run your own local version where you can host, edit, collaborate in real-time, and compile your LaTeX documents, or simply use the version hosted on the official website.

NaN

*   **Overleaf** — (Previously writeLaTeX) Online collaborative LaTeX editor with integrated real-time preview.

NaN

*   **cloudTeX** — Social TeX in the cloud.

NaN

*   **Papeeria** — Online LaTeX editor.

NaN

Find more on the [LaTeX wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Online_solutions).

## Important information

*   The way to handle font mappings for updmap was improved in September 2009, and installation should now be much more reliable than in the past. In the meantime, if you encounter error messages about unavailable map files, simply remove them by hand from the `updmap.cfg` file (ideally using `updmap-sys --edit`). You can also run `updmap-sys --syncwithtrees` to automatically comment out outdated map lines from the config file.

*   The ConTeXt formats (for MKII and MKIV) are not automatically generated upon installation. See [the ConTeXT wiki](http://wiki.contextgarden.net) for instructions on how to do this.

*   The packages containing the documentation and sources are **no longer available** in official repositories. You can locally build them with [tllocalmgr](#TeXLive_Local_Manager). You can also consult documentation online at [https://tug.org/texlive/Contents/live/doc.html](https://tug.org/texlive/Contents/live/doc.html) or on CTAN. Another possibility is using the online documentation at `http://texdoc.net/pkg/packagename` which resolves to the relevant pdf for `packagename`, similar to the command line tool `texdoc` (which is useless without locally installed documentation).

*   TeX Live (upstream) now provides a tool for incremental updates of CTAN packages. On that basis, we also plan to update our packages on a regular basis (we have written tools that almost automate that task).

*   Some tools and utilities included in TeX Live rely on [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), [perl](https://www.archlinux.org/packages/?name=perl), and [ruby](https://www.archlinux.org/packages/?name=ruby).

*   For help and information about TeX Live see: [https://tug.org/texlive/doc.html](https://tug.org/texlive/doc.html) and [https://tug.org/texlive/doc/texlive-en/texlive-en.html](https://tug.org/texlive/doc/texlive-en/texlive-en.html)

*   System-wide configuration files are under `/usr/share/texmf-config`. User-specific ones should be put under `~/.texlive/texmf-config`. `$TEXMFHOME` is `~/texmf` and `$TEXMFVAR` is `~/.texlive/texmf-var`.

*   A skeleton of a local texmf tree is at `/usr/local/share/texmf`: this directory is writable for members of the group **tex**.

### Paper Size

If you would like to set the default page size to something other than A4 (such as "Letter"), run the following command:

```
$ texconfig

```

This command is also capable of changing other useful settings.

### Error with "formats not generated" upon update

See [this bug report](https://bugs.archlinux.org/task/16467). (**Note that if you do not use the experimental engine _LuaTeX_, you can ignore this.**) This situation typically occurs when the configuration files `language.def` and/or `language.dat` for hyphenation patterns contain references to files from earlier releases of `texlive-core`, in particular to the latest experimental hyphenation patterns for German, whose file name changes frequently. Currently they should point to `dehyph{n,t}-x-2009-06-19.tex`.

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

The TeXLive Local Manager is a utility provided by Firmicus which allows to conveniently manage a TeX Live installation on Arch Linux. See [texlive-localmanager-git](https://aur.archlinux.org/packages/texlive-localmanager-git/)<sup><small>AUR</small></sup> in the [AUR](/index.php/AUR "AUR").

```
Usage: tllocalmgr  
       tllocalmgr [options] [command] [args]

       Running tllocalmgr alone starts the TeXLive local manager shell 
       for Arch Linux. This shell is capable of command-line completion!
       There you can look at the available updates with the command 'status' 
       and you can install individual CTAN packages using 'install' or 'update'
       under $TEXMFLOCAL. This is done by creating a package texlive-local-<pkg>
       and installing it with pacman. Note that this won’t interfere with your 
       standard texlive installation, but files under $TEXMFLOCAL will take
       precedence.  

       Here are the commands available in the shell:

Commands:       
              status   --   Current status of TeXLive installation
           shortinfo * --   Print a one-liner description of CTAN packages
                info * --   Print info on CTAN packages
              update * --   Locally update CTAN packages
             install * --   Locally install new CTAN packages
          installdoc * --   Locally install documentation of CTAN packages
          installsrc * --   Locally install sources of CTAN packages
           listfiles * --   List all files in CTAN packages
              search * --   Search info on CTAN packages
         searchfiles * --   Search for files in CTAN packages
             texhash   --   Refresh the TeX file database
               clean   --   Clean local build tree
                help   --   Print helpful information
                quit   --   Quit tllocalmgr

        The commands followed by * take one of more package names as arguments.
        Note that these can be completed automatically by pressing TAB.

        You can also run tllocalmgr as a standard command-line program, with
        one of the above commands as argument, then the corresponding task will
        be performed and the program will exit (except when the command is 'status').

        tllocalmgr accepts the following options:

Options:     --help          Shows this help
             --version       Show the version number
             --forceupdate   Force updating the TeXLive database
             --skipupdate    Skip updating the TeXLive database
             --localsearch   Search only installed packages
             --location      #TODO?
             --mirror        CTAN mirror to use (default is mirror.ctan.org)
             --nocolor       #TODO

```

### Recent "langukenglish" errors

For problems involving this error when trying to run `tllocalmgr` commands,

```
Can't get object for collection-langukenglish at /usr/bin/tllocalmgr line 103

```

See ary0's solution at the AUR: [texlive-localmanager](https://aur.archlinux.org/packages/texlive-localmanager/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/texlive-localmanager)]</sup>. In summary, edit `/usr/share/texmf-var/arch/tlpkg/TeXLive/Arch.pm` and remove "langukenglish" from the section of the file shown here:

```
my @core_colls =
qw/ basic context genericrecommended fontsrecommended langczechslovak
langdutch langfrench langgerman langitalian langpolish langportuguese
langspanish **langukenglish** latex latexrecommended luatex mathextra metapost
texinfo xetex /;

```

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

Normally, new .sty files go in `/usr/share/texmf-dist/tex/latex/<package name>/*`. Create this directory if you do not have it. This directory will automatically be searched when *tex is executed. Further discussion can be found here: [https://bbs.archlinux.org/viewtopic.php?id=85757](https://bbs.archlinux.org/viewtopic.php?id=85757)

### Using PKGBUILDs

To install a LaTeX package on a global level, you should use a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for the sake of simplifying maintenance. Examples can be found in the [AUR](/index.php/AUR "AUR"), e.g. [texlive-gantt](https://aur.archlinux.org/packages/texlive-gantt/)<sup><small>AUR</small></sup>.

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=TeX_Live&oldid=411508](https://wiki.archlinux.org/index.php?title=TeX_Live&oldid=411508)"