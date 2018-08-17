[Mnemosyne](http://mnemosyne-proj.org) is an open-source, cross-platform flashcard program that uses a [spaced repetition](https://en.wikipedia.org/wiki/Spaced_repetition "wikipedia:Spaced repetition") algorithm for maximizing learning efficiency.

It is inspired by the proprietary [SuperMemo](http://www.supermemo.com) and comparable to [Anki](/index.php/Anki "Anki"), but with a stronger focus on a minimalist, distraction-free UI and simple but flexible work-flow.

Mnemosyne is written in Python 2 and uses the [Qt](/index.php/Qt "Qt") toolkit.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Configuring](#Configuring)
        *   [1.1.1 Size of mathematical formulae](#Size_of_mathematical_formulae)
*   [2 Other Resources](#Other_Resources)
*   [3 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") the [mnemosyne](https://aur.archlinux.org/packages/mnemosyne/) package.

### Configuring

Most of the options in Mnemosyne are available directly in the user interface. A few infrequently-used options are accessible through a config file located at `~/.config/mnemosyne/config.py`.

##### Size of mathematical formulae

If you would like to decrease the rendering resolution of mathematical formulae (default 200 dpi, which is rather large on most screens) to better fit with normal text, open the file `~/.config/mnemosyne/config.py` and decrease the number following the -D option in the line that looks like:

```
dvipng = "dvipng -D 200 -T tight tmp.dvi"

```

## Other Resources

The Mnemosyne website offers:

*   Official [documentation](http://mnemosyne-proj.org/help/index.php)
*   User-contributed [plugins](http://mnemosyne-proj.org/old/taxonomy/term/10)
*   User-contributed sets of cards

## See Also

*   [Anki](/index.php/Anki "Anki") - another open-source flashcard program using spaced repetition