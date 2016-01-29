# TeX Live and CJK

The below tutorial guides you through getting your Tex to work with the Cyberbit font. If you do not much care what font you use, just make sure you have the texlive-langcjk package installed, and add this to your preamble:

```
\usepackage[encapsulated]{CJK}
\usepackage{ucs}
\usepackage[utf8x]{inputenc}
% use one of bsmi(trad Chinese), gbsn(simp Chinese), min(Japanese), mj(Korean); see:
% /usr/share/texmf-dist/tex/latex/cjk/texinput/UTF8/*.fd
\newcommand{\cntext}[1]{\begin{CJK}{UTF8}{gbsn}#1\end{CJK}}

```

and then encapsulate your CJK in \cntext.

```
\cntext{我的中文寫得很好。}

```

## Contents

*   [1 Goals](#Goals)
*   [2 Prerequisites](#Prerequisites)
*   [3 The steps](#The_steps)
*   [4 Remarks](#Remarks)

## Goals

This Tutorial is supposed to explain how to configure your [TeX Live](/index.php/TeX_Live "TeX Live") Installation to successfully include CJK (Chinese, Japanese and Korean) Characters in your compiled TeX-files. This tutorial is based on the [Kile-HowTo on CJK Support](http://kile.sourceforge.net/Documentation/html/cjk.html). The problem with the kile-tutorial (which nevertheless is very good) is the loose definition of the file and folder structure (for it is, as I think, written to be used for any TeX-distribution). Long story short, using the kile-tutorial, it might take you a couple of hours to find the appropriate places to store and configure your CJK-installation (at least when using TeXlive). Hope this helps you to avoid this hassle.

## Prerequisites

First, you need a working [TeXlive installation](/index.php/TeX_Live "TeX Live"), including the [texlive-langcjk](https://www.archlinux.org/packages/?name=texlive-langcjk) package. (In case you haven't done so already, use [pacman](/index.php/Pacman "Pacman") to install them) and [appropriate fonts](/index.php/Fonts "Fonts"). This are the prerequisites on the TeX-part. Needless to say, you should have chosen a character encoding for your system which can deal with complex characters (like UTF8) and some kind of input method for these, like [Scim](/index.php/Scim "Scim").

## The steps

1.  Download and configure a CJK Font for your TeXlive distribution. Like done in the kile-tutorial we use the Cyberbit font. Create an empty folder, download the [Zip-file](ftp://ftp.netscape.com/pub/communicator/extras/fonts/windows/Cyberbit.ZIP) and unpack it into the folder. Then rename the file named `Cyberbit.ttf` to `cyberbit.ttf` and download [this file](http://delloye.free.fr/Unicode.sfd) into the same folder. Using the command
    `$ ttf2tfm cyberbit.ttf -w cyberbit@Unicode@`
    you create some dozens (if not hundreds) of *.tfm files and their corresponding *.enc files.
2.  Now, we need folders in the TeXlive-filetree to copy the *.tfm and the *.enc files to their right places. (in the following I presume you have superuser-rights and are in the folder containing the *.tfm and *.enc files.)
    `$ mkdir /usr/share/texmf-dist/fonts/tfm/cyberbit
    $ chmod 755 /usr/share/texmf-dist/fonts/tfm/cyberbit
    $ cp *.tfm /usr/share/texmf-dist/fonts/tfm/cyberbit/
    $ chmod 644 /usr/share/texmf-dist/fonts/tfm/cyberbit/*
    $ mkdir /usr/share/texmf-dist/fonts/enc/pdftex/cyberbit
    $ chmod 755 /usr/share/texmf-dist/fonts/enc/pdftex/cyberbit
    $ cp *.enc /usr/share/texmf-dist/fonts/enc/pdftex/cyberbit/
    $ chmod 644 /usr/share/texmf-dist/fonts/enc/pdftex/cyberbit/*`
3.  Next, we need to install a map file connecting the *.enc files to the font. Download [cyberbit.map](http://delloye.free.fr/cyberbit.map).
    1.  In case the folder `/usr/share/texmf-config/pdftex/config/` does not exist, create it:
        `$ mkdir /usr/share/texmf-config/pdftex
        $ mkdir /usr/share/texmf-config/pdftex/config
        $ chmod -R 755 /usr/share/texmf-config/pdftex`
    2.  Then copy the .map file into that folder:
        `$ cp cyberbit.map /usr/share/texmf-config/pdftex/config/
        $ chmod 644 /usr/share/texmf-config/pdftex/config/cyberbit.map`
4.  Then we need a file named c70cyberbit.fd you can download [here](http://delloye.free.fr/c70cyberbit.fd).
    1.  Create an appropriate folder (again, if it does not exist):
        `$ mkdir /usr/share/texmf-dist/tex/misc
        $ chmod 755 /usr/share/texmf-dist/tex/misc`
    2.  And copy the file into it:
        `$ cp c70cyberbit.fd /usr/share/texmf-dist/tex/misc/
        $ chmod 644 /usr/share/texmf-dist/tex/misc/c70cyberbit.fd`
5.  The font itself is still missing in the TeX-distribution tree:
    `$ cp cyberbit.ttf /usr/share/texmf-dist/fonts/truetype/
    $ chmod 644 /usr/share/texmf-dist/fonts/truetype/cyberbit.ttf`
6.  To make sure that TeX will find the font, we have to add the truetype-folder into the TeX-config. To do so, edit `/usr/share/texmf/web2c/texmf.cnf` and look for an entry called "TTFONTS", which should look like this:
    `TTFONTS = .;$TEXMF/fonts/truetype//;$OSFONTDIR/TTF//`
    Although maybe not very elegant, I added `/usr/share/texmf-dist/fonts/truetype//` to the end of the line, so that TeX will find the font for sure:
    `TTFONTS = .;$TEXMF/fonts/truetype//;$OSFONTDIR/TTF//;/usr/share/texmf-dist/fonts/truetype//`
7.  Although I am not sure we really need this, I created a file called "pdftex.cfg" in the folder `/usr/share/texmf-config/pdftex/config/` and added a line saying:
    `map +cyberbit.map`
8.  TeX still does not know that it should by now be able to handle CJK input, until we edit `/usr/share/texmf/fonts/map/ttf2pk/config/ttfonts.map` to include the following lines (if they already exist, all you have to do is to uncomment them):
    `cyberb@Unicode@ cyberbit.ttf
    cyberbit@Unicode@ cyberbit.ttf`
9.  To finish the configuration, run
    `$ texhash`

Hopefully this tutorial will spare you the hours of work I spent configuring CJK in TeX.

## Remarks

This procedure was tested with the following packages:
extra/texlive-core 2008.11906-1
extra/texlive-langcjk 2008.10331-1
And simplified Chinese characters.

Retrieved from "[https://wiki.archlinux.org/index.php?title=TeX_Live_and_CJK&oldid=376447](https://wiki.archlinux.org/index.php?title=TeX_Live_and_CJK&oldid=376447)"