This article covers [spell checking](https://en.wikipedia.org/wiki/Spell_checker "wikipedia:Spell checker") and [grammar checking](https://en.wikipedia.org/wiki/Grammar_checker "wikipedia:Grammar checker") software.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Spell checkers](#Spell_checkers)
    *   [1.1 Language-specific](#Language-specific)
    *   [1.2 Enchant](#Enchant)
    *   [1.3 Applications](#Applications)
*   [2 Grammar checkers](#Grammar_checkers)
    *   [2.1 Applications](#Applications_2)

## Spell checkers

*   **[GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell "wikipedia:GNU Aspell")** — Spell checker designed to eventually replace Ispell, see also [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1) and the [info document](http://aspell.net/man-html/index.html).

	[http://aspell.net/](http://aspell.net/) || [aspell](https://www.archlinux.org/packages/?name=aspell), [dictionaries](https://www.archlinux.org/packages/?q=aspell-)

*   **[Hunspell](https://en.wikipedia.org/wiki/Hunspell "wikipedia:Hunspell")** — Spell checker and morphological analyzer library and program, see also [hunspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hunspell.1).

	[https://hunspell.github.io/](https://hunspell.github.io/) || [hunspell](https://www.archlinux.org/packages/?name=hunspell), [dictionaries](https://www.archlinux.org/packages/?q=hunspell-)

*   **[Ispell](https://en.wikipedia.org/wiki/Ispell "wikipedia:Ispell")** — Interactive spell-checking program for Unix, see also [ispell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ispell.1).

	[https://www.cs.hmc.edu/~geoff/ispell.html](https://www.cs.hmc.edu/~geoff/ispell.html) || [ispell](https://www.archlinux.org/packages/?name=ispell)

### Language-specific

*   **Hspell** — Hebrew spell-checker

	[http://www.ivrix.org.il/projects/spell-checker/](http://www.ivrix.org.il/projects/spell-checker/) || [hspell](https://www.archlinux.org/packages/?name=hspell)

*   **Voikko** — Finnish spelling and grammar checker, hyphenator and collection of related linguistic data

	[https://voikko.sourceforge.net](https://voikko.sourceforge.net) || [libvoikko](https://www.archlinux.org/packages/?name=libvoikko)

### Enchant

[Enchant](https://en.wikipedia.org/wiki/Enchant_(software) is a wrapper library for generic spell checking, developed as part of [AbiWord](/index.php/AbiWord "AbiWord"), supporting all above spell checkers apart from Ispell.

Enchant is available as the [enchant](https://www.archlinux.org/packages/?name=enchant) package. For its usage and ordering file, see [enchant-2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/enchant-2.1).

Enchant is used by many applications through the following [GTK](/index.php/GTK "GTK") libraries:

*   **gspell** — Flexible API to implement spell checking in GTK+ applications.

	[https://wiki.gnome.org/Projects/gspell](https://wiki.gnome.org/Projects/gspell) || [gspell](https://www.archlinux.org/packages/?name=gspell)

*   **GtkSpell** — Provides word-processor-style highlighting and replacement of misspelled words in a GtkTextView widget.

	[http://gtkspell.sourceforge.net/](http://gtkspell.sourceforge.net/) || [gtkspell](https://www.archlinux.org/packages/?name=gtkspell), [gtkspell3](https://www.archlinux.org/packages/?name=gtkspell3)

### Applications

[Firefox](/index.php/Firefox "Firefox"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium "Chromium") and [LibreOffice](/index.php/LibreOffice "LibreOffice") can all use system-wide installed Hunspell dictionaries as well as dictionaries/other spell checkers installed through their own extension systems. See the following sections:

*   [Firefox#Spell checking](/index.php/Firefox#Spell_checking "Firefox")
*   [Thunderbird#Spell checking](/index.php/Thunderbird#Spell_checking "Thunderbird")
*   [LibreOffice#Spell checking](/index.php/LibreOffice#Spell_checking "LibreOffice")

[AbiWord](/index.php/AbiWord "AbiWord") and [Gedit](/index.php/Gedit "Gedit") use Enchant.

## Grammar checkers

*   **LanguageTool** — Open source language checker, written in [Java](/index.php/Java "Java").

	[https://www.languagetool.org](https://www.languagetool.org) || [languagetool](https://www.archlinux.org/packages/?name=languagetool)

*   **Style and Diction** — Diction identifies wordy and commonly misused phrases. Style analyses surface characteristics of a document.

	[https://www.gnu.org/software/diction/](https://www.gnu.org/software/diction/) || [diction](https://aur.archlinux.org/packages/diction/)

### Applications

[Firefox](/index.php/Firefox "Firefox"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium "Chromium") and [LibreOffice](/index.php/LibreOffice "LibreOffice") all support grammar checking only through extensions. For LibreOffice, see [LibreOffice#Grammar checking](/index.php/LibreOffice#Grammar_checking "LibreOffice").

[AbiWord](/index.php/AbiWord "AbiWord") has a built-in grammar checker, see [AbiWord#Grammar checking](/index.php/AbiWord#Grammar_checking "AbiWord").