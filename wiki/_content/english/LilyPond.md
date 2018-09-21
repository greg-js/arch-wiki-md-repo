[LilyPond](http://lilypond.org/) is a free score writing application. Its input is a plain text file in the LilyPond music writing format, and its output is in either PostScript or PDF.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Front-ends](#Front-ends)
*   [2 Usage](#Usage)
*   [3 Text editor support](#Text_editor_support)
    *   [3.1 Emacs lilypond-mode](#Emacs_lilypond-mode)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lilypond](https://www.archlinux.org/packages/?name=lilypond) package.

### Front-ends

*   **[Denemo](https://en.wikipedia.org/wiki/Denemo "wikipedia:Denemo")** — Supports keyboard, MIDI and acoustic input, written in C.

	[http://denemo.org/](http://denemo.org/) || [denemo](https://aur.archlinux.org/packages/denemo/)

*   **[Frescobaldi](https://en.wikipedia.org/wiki/Frescobaldi_(software) "wikipedia:Frescobaldi (software)")** — Provides music view with two-way point & click, MIDI capturing and playback, written in Python with PyQt.

	[http://www.frescobaldi.org/index.html](http://www.frescobaldi.org/index.html) || [frescobaldi](https://aur.archlinux.org/packages/frescobaldi/)

## Usage

Create a test file like:

 `test.ly` 
```
{
 c' e' g' e'
}

```

To compile it, use:

```
$ lilypond test.ly

```

It will create `test.pdf` and `test.ps` files that contain your score.

LilyPond provides [musicxml2ly(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/musicxml2ly.1) to convert [MusicXML](https://en.wikipedia.org/wiki/MusicXML "wikipedia:MusicXML") to the LilyPond format.

For more information, see `info lilypond`, [lilypond(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lilypond.1) and the [documentation](http://lilypond.org/manuals.html).

## Text editor support

LilyPond comes with modes for [Emacs](/index.php/Emacs "Emacs") and [Vim](/index.php/Vim "Vim"), see the [documentation](http://lilypond.org/doc/Documentation/usage/text-editor-support).

For Vim see the filetype plugin `/usr/share/vim/vimfiles/ftplugin/lilypond.vim` for the available key mappings.

### Emacs `lilypond-mode`

[lilypond](https://www.archlinux.org/packages/?name=lilypond) package installs some [Emacs](/index.php/Emacs "Emacs") files including `/usr/share/emacs/site-lisp/lilypond-mode.el`.

To use `lilypond-mode`, firstly **M-x load-library <RET> lilypond-mode <RET>** then again **M-x lilypond-mode <RET>**.

## See also

*   [Wikipedia:LilyPond](https://en.wikipedia.org/wiki/LilyPond "wikipedia:LilyPond")
*   [List of applications/Multimedia#Scorewriters](/index.php/List_of_applications/Multimedia#Scorewriters "List of applications/Multimedia")