Related articles

*   [TeX Live](/index.php/TeX_Live "TeX Live")
*   [TeX Live and CJK](/index.php/TeX_Live_and_CJK "TeX Live and CJK")
*   [LaTeX](/index.php/LaTeX "LaTeX")

Frequently asked qustions about TeX, TeXLive.

## Contents

*   [1 General questions](#General_questions)
    *   [1.1 Q: How can I access Tex Live documentation?](#Q:_How_can_I_access_Tex_Live_documentation.3F)
    *   [1.2 Q: I want LaTeX to do something special, and I am pretty sure someone before me had to have the same problem.](#Q:_I_want_LaTeX_to_do_something_special.2C_and_I_am_pretty_sure_someone_before_me_had_to_have_the_same_problem.)
    *   [1.3 Q: I want to read more! More! I said more!](#Q:_I_want_to_read_more.21_More.21_I_said_more.21)
*   [2 Tricks with LaTeX](#Tricks_with_LaTeX)
    *   [2.1 Q: I need/want to use some funky bibliography/references format.](#Q:_I_need.2Fwant_to_use_some_funky_bibliography.2Freferences_format.)
*   [3 TeXlive directory structure and important files](#TeXlive_directory_structure_and_important_files)
    *   [3.1 Q: What's up with all these dirs /usr/share/{texmf,texmf-dist,texmf-var,texmf-config}?](#Q:_What.27s_up_with_all_these_dirs_.2Fusr.2Fshare.2F.7Btexmf.2Ctexmf-dist.2Ctexmf-var.2Ctexmf-config.7D.3F)
    *   [3.2 Q: I want to have some configuration app!](#Q:_I_want_to_have_some_configuration_app.21)
    *   [3.3 Q: I want to edit textfiles! Where are some configuration files?](#Q:_I_want_to_edit_textfiles.21_Where_are_some_configuration_files.3F)
*   [4 Common problems with TeXlive](#Common_problems_with_TeXlive)
    *   [4.1 Q: I just updated texlive and it stopped working.](#Q:_I_just_updated_texlive_and_it_stopped_working.)
    *   [4.2 Q: I want use ConTeXt.](#Q:_I_want_use_ConTeXt.)
    *   [4.3 Q: pdftex and/or dvips uses bitmap fonts instead of type1 postscript fonts](#Q:_pdftex_and.2For_dvips_uses_bitmap_fonts_instead_of_type1_postscript_fonts)
*   [5 Useful apps to use with (any TeX installation)](#Useful_apps_to_use_with_.28any_TeX_installation.29)
    *   [5.1 Q: Editors?](#Q:_Editors.3F)
    *   [5.2 Q: Pictures with LaTeX labels?](#Q:_Pictures_with_LaTeX_labels.3F)
    *   [5.3 Q: Pictures with LaTeX labels - I want GUI! - I want pictures fast!](#Q:_Pictures_with_LaTeX_labels_-_I_want_GUI.21_-_I_want_pictures_fast.21)

## General questions

### Q: How can I access Tex Live documentation?

**A:** You can try searching for the package with `texdoc`:

```
texdoc <packagename>

```

Alternatively, you can search for documentation on [CTAN](http://ctan.org/search/).

### Q: I want LaTeX to do something special, and I am pretty sure someone before me had to have the same problem.

**A:** There is an excellent [TeX FAQ](http://www.tex.ac.uk/faq) on the web. Typical LaTeX problems (special headers, different page layout, tricks with tables, etc.) are all covered there. Searchable!

### Q: I want to read more! More! I said more!

**A:** Andy Roberts (arooaroo) has a couple of tricks on his website [Getting to grips with LaTeX](http://www.andy-roberts.net/misc/latex/index.html), which has been used as a basis for [LaTeX wikibook](http://en.wikibooks.org/wiki/LaTeX). You could also check out [The not so Short Introduction to LaTeX](http://www.ctan.org/tex-archive/info/lshort/) which is available in many languages.

## Tricks with LaTeX

### Q: I need/want to use some funky bibliography/references format.

**A:** Biblatex which is in [texlive-bibtexextra](https://www.archlinux.org/packages/?name=texlive-bibtexextra) is then the thing you are looking for. Some templates for specialized publishers (e.g. the IEEE, some universities, etc.) are included in the [texlive-publishers](https://www.archlinux.org/packages/?name=texlive-publishers) package.

## TeXlive directory structure and important files

### Q: What's up with all these dirs /usr/share/{texmf,texmf-dist,texmf-var,texmf-config}?

**A:** TeX uses several "source trees"; they have the same internal structure, and can "overlap". This is to allow users to modify files provided system-wide without having to access files they're not supposed to access. Here's the portion of the main config file which lists all these dirs with some explanations ($SELFAUTODIR=/usr/share):

```
% The tree containing the runtime files closely related to the specific
% program version used:
TEXMFMAIN = $SELFAUTODIR/texmf
% The main distribution tree:
TEXMFDIST = $SELFAUTODIR/texmf-dist
% A place for local additions to a "standard" texmf tree.
% This tree is not used for local configuration maintained by
% texconfig, it uses TEXMFCONFIG below.
TEXMFLOCAL = $SELFAUTODIR/texmf-local
% TEXMFSYSVAR, where texconfig-sys stores variable runtime data.
TEXMFSYSVAR = $SELFAUTODIR/texmf-var
% TEXMFSYSCONFIG, where texconfig-sys stores configuration data.
TEXMFSYSCONFIG = $SELFAUTODIR/texmf-config
% User texmf trees are allowed as follows.
TEXMFHOME = $HOME/texmf
% TEXMFVAR, where texconfig stores variable runtime data.
TEXMFVAR = $HOME/.texmf-var
% TEXMFCONFIG, where texconfig stores configuration data.
TEXMFCONFIG = $HOME/.texmf-config

```

Note that they are searched in the reverse order that they are listed above (I think). So when some problems pops up, search the trees in the proper order ;)

One more remark: if you install something just for you, it should go to your home texmf tree. However, on desktops, you might not want to clutter your home dir; then it should go to texmf-local tree (which should be writable by the "tex" group).

### Q: I want to have some configuration app!

**A:** Run

```
texconfig

```

Careful! When you run this as a user, you modify settings for that user. If you want to modify system-wide settings, run

```
texconfig-sys

```

as root instead.

### Q: I want to edit textfiles! Where are some configuration files?

**A:** Keeping in mind the above directory structure (<texmfroot> refers to one of the dirs above), here you go: The main config file:

```
<texmfroot>/web2c/texmf.cnf

```

List of formats generated:

```
<texmfroot>/web2c/fmtutil.cnf

```

Settings with which are e.g. bitmap fonts generated

```
<texmfroot>/web2c/mktex.cnf

```

Which and how type1 fonts are used instead of metafont generated bitmap ones?

```
<texmfroot>/web2c/updmap.cfg

```

## Common problems with TeXlive

### Q: I just updated texlive and it stopped working.

**A:** While this can be caused by many things, the most common reason for troubles of this sort is the following mechanism of how texlive works: there can be more than one "tree of tex files" which are put "on top of each other" as far as TeX is concerned (see question 3.1 above), and so there can be more copies of "the same" config file around on the disk, and only one of them is used. In particular, if a user makes some config changes, or generates some formats, the resulting "changes" are saved in the local user's tree ({{ic|~/.texlive/texmf-{var,config}}}), and while these exist, they are **always** preferred over the system files. This implies that even if the system files are updated on texlive update, when a user runs tex, it still uses the "old" files that are in `~/.texlive`.

Hence, if you suspect that this might be the cause of the problem, you can

*   backup your `~/.texlive` dir somewhere and try again. If the problem persists, with big probability it's a problem with some `texlive-*` package.
*   there is a tool with which one can check which file with a particular name is "seen" by TeX. Namely

```
 kpsewhich <filename>

```

returns the full path to the file of that name that TeX would use.

Finally, the most usual troubles that span from this behavior are:

*   after upgrade, TeX "stops working" with the following error message:

```
 Fatal format file error; I'm stymied.

```

What one should understand is that the TeX system "precompiles" formats (that is, takes the macros which constitute for instance the LaTeX format, and creates a binary thing (file latex.fmt), which is then used when you call "latex <somefile>"). Now when the tex binary itself is updated, all the precompiled formats need to be recompiled as well. While [pacman](/index.php/Pacman "Pacman") does that for you for system-wide formats, the info above implies that if a user (or some program like LyX) ever compiled the formats by himself, that user needs to recompile the formats manually. The command for that is

```
 fmtutil --all

```

(as a user). (By the way, the location of `*.fmt` files is `<texmfroot>/texmf-var/web2c`.) The other option is to delete the `*.fmt` files from the local tree (`~/.texlive/texmf-var/web2c/*.fmt`) and use the system-wide generated formats (which can be regenerated with `sudo fmtutil-sys --all`).

*   after upgrade, some fonts stop being used properly; or there is an error that TeX cannot find some font. This is related to the question 4.4 below - you most probably have a local `updmap.cfg` file (check by `kpsewhich updmap.cfg`) which doesn't reflect changes in `*.map` files and fonts which came with the upgrade. In this case, apply the methods from the question 4.4.

### Q: I want use ConTeXt.

**A:** (English) ConTeXt should be enabled automatically. Remember that the ruby wrapper to be used with ConTeXt is

```
texexec

```

If ConTeXt is not enabled (or you want to use localized version), use

```
texconfig

```

to edit the configuration file with formats, and uncomment the appropriate lines. To set up the new MarkIV implementation of ConTeXt, see [http://wiki.contextgarden.net/Running_Mark_IV](http://wiki.contextgarden.net/Running_Mark_IV)

### Q: pdftex and/or dvips uses bitmap fonts instead of type1 postscript fonts

i.e. "when I zoom my PDF/ps file, fonts are really pixelated" a.k.a. "everytime I run tex, it takes a long time because it generates fonts with metafont" a.k.a. "at the end of my log file generated by pdftex I see that it includes *.pk fonts instead of *.pfb"

**A:** This takes a bit of time to explain. Now it is important that you understand how the system works, so that you know what you are doing.

Files which tell pdftex/dvips which fonts are to be included as type1 fonts (instead of traditional bitmap fonts) have suffix .map and reside somewhere in `<texmfroot>/fonts/map/{pdftex,dvips}/updmap/{pdftex.map,psfonts.map`}. First of all, you need to find out the name of the map file you want. The log for my TeX compilation gave me the error "Font rtxr at 540 not found", so I typed `locate rtxr` and got, among others, `/usr/share/texmf-dist/fonts/afm/public/txfonts/rtxr.afm`. This tells me the font package is `txfonts`.

You **do not** want to edit these mapfiles manually; they're good for checking if your favorite type1 font which causes trouble is sitting there properly.

*   These files are automatically generated, when you run

```
$ updmap

```

as user, or

```
# updmap-sys

```

as root for system-wide changes

What you need to do to have your favorite fonts (for instance kpfonts or txfonts) properly used as type1 fonts in pdf and ps files is to locate the .map file that goes with the package (e.g. kpfonts.map; you do not need to actually *do* anything with the file, just know that it is there somewhere), edit `updmap.cfg` by running

```
updmap --edit

```

as user (or `updmap-sys --edit` as root) and add the line

```
Map kpfonts.map

```

or the line

```
MixedMap kpfonts.map

```

(MixedMap indicates that fonts are also available as bitmap fonts.), and exit the editor. At this point, you should see the messages which indicate that updmap is regenerating {pdftex,psfonts}.map files.

(Alternatively, just run `updmap --enable Map=kpfonts`, or (as root) `updmap-sys --enable Map=kpfonts`, if you just want to add one map without going into an editor.)

This should be sufficient, and your next run of pdftex/dvips should be already including the type1 versions of fonts.

## Useful apps to use with (any TeX installation)

### Q: Editors?

**A:** See [List of applications/Documents#Scientific_documents](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents") for a long list of options.

### Q: Pictures with LaTeX labels?

**A:** Apart from some latex in-source macros (which are a bit of a PITA to write), there are excellent "picture programming languages" [metapost](http://cm.bell-labs.com/who/hobby/MetaPost.html) and its (more-less) successor [asymptote](http://asymptote.sourceforge.net). They are pretty powerful, but have similar approach as tex itself - you write down what you want to have and how are the things related, and compiler then produces the picture. The target format is postscript for metapost; and eps/pdf/png for asymptote.

Even closer incorporated to TeX itself - i.e. to Plain TeX, LaTeX or Context, there are layers for each of this formats - is the relatively new PGF package with its language named [TIKZ](http://www.fauskes.net/pgftikzexamples/).

The Python library [PyX](http://pyx.sourceforge.net/) (named python-pyx in AUR) gives the possibillity to use Python to program pictures, and it uses TeX for the typesetting.

Last but not least: [PSTricks](http://tug.org/PSTricks/main.cgi/), which gives an interface for direct inclusion of Postscript-code into TeX ([ps2pdf](http://pages.cs.wisc.edu/~ghost/doc/AFPL/6.50/Ps2pdf.htm)). There are some hurdles to climb if you want to have pdf-output, because PSTricks is not compatible to pdftex.

### Q: Pictures with LaTeX labels - I want GUI! - I want pictures fast!

**A:** The "grandfather" of vector editors - xfig is able to produce some output relevant to tex. I had relatively good experience with [ipe](http://tclab.kaist.ac.kr/ipe/) recently (saves eps/pdf). Inkscape is a good choice too.