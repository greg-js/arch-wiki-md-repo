# LilyPond

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Lilypond is a Free Software score writing application. Its input is a plain text file in the lilypond music writing format, and its output is in either postscript or Portable Document Format.

## Contents

*   [1 Installation](#Installation)
*   [2 Example Score](#Example_Score)
*   [3 Tweaking](#Tweaking)
    *   [3.1 Which editor to use?](#Which_editor_to_use.3F)
    *   [3.2 Speed up writing notes](#Speed_up_writing_notes)
    *   [3.3 More useful info](#More_useful_info)

## Installation

[Install](/index.php/Install "Install") [lilypond](https://www.archlinux.org/packages/?name=lilypond) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Example Score

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

## Tweaking

### Which editor to use?

*   VIM

Vim with the possibilities of compiling the code within the program along with syntax coloring tools and indenting. First install the [vim](/index.php/Vim "Vim") editor, then go to this Lilypond website [[1]](http://lilypond.org/doc/v2.11/Documentation/user/lilypond-program/Vim-mode) and follow the instructions on how to enable the vim mode.

The next thing you need to do is enable the syntaxes. To do so edit `~/.vimrc` with your favorite editor and after editing your file should look like this:

 `~/.vimrc` 

```
set runtimepath+=/usr/share/lilypond/2.12.3/vim/ 
syntax on		" Turn on colors
filetype plugin on	" Enables the ftplugin options
set autoindent		" Automaticaly indent while writing.
```

Now when you edit a `*.ly` file you can compile your code with `F5` button, open PDF viewer with `F6` and play midi with `F4` (using timidity). A configuration file is in `/usr/share/lilypond/2.12.3/vim/ftplugin/lilypond.vim` which is easy to customize.

Click-and-point using evince. [[2]](https://github.com/markk/textedit-ly)

*   Frescobaldi

You can find it in [AUR](/index.php/AUR "AUR").

*   jEdit with lilyPondTools plugin.

[Install](/index.php/Install "Install") [jedit](https://www.archlinux.org/packages/?name=jedit) from the [official repositories](/index.php/Official_repositories "Official repositories").

Open jEdit and go to _Plugins > Plugin Manager_. Select the _Install_ tab and click on _LilyPondTools_. Hit the _Install_ button.

### Speed up writing notes

LilyComp [[3]](http://lilycomp.sourceforge.net/) can be used to speed up writing notes. It requires [python](/index.php/Python "Python") and tk. Lines 67 and 68 in `lilycomp.py` should be edited to enable `deutsch.ly` dictionary for sharp and flat symbols. It uses absolute notation (\relative is not used.)

### More useful info

*   For JEdit: Under plugins install _LookAndFeel_. You can find good stuff under Visual.

For better usability my settings are: under _Global Options > Docking_ put the _Console_ and _Error List_ to _right_ and _LilyPond PDF preview_ to _bottom_ under _Docking_ position. Then under _View_ push _Alternate docked window placement_ and _Alternate tool bar placement_ buttons.

*   For a tutorial on how to use this software visit LilyPond [[4]](http://lilypond.org/) website.

Retrieved from "[https://wiki.archlinux.org/index.php?title=LilyPond&oldid=360427](https://wiki.archlinux.org/index.php?title=LilyPond&oldid=360427)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Applications](/index.php/Category:Applications "Category:Applications")