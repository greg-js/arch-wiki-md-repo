[Anki](http://ankisrs.net/) is an [SRS](https://en.wikipedia.org/wiki/Spaced_repetition "wikipedia:Spaced repetition") (Spaced Repetition System), a program which allows you to create, manage and review [flashcards](https://en.wikipedia.org/wiki/Flashcard "wikipedia:Flashcard"). Because spaced repetition algorithms are a lot more efficient than traditional study methods, you can either greatly decrease your time spent studying, or greatly increase the amount you learn. Anki is very flexible and also allows the creation of templates. Android and iOS apps are available and synchronization between devices is supported.

This guide shows you how to install Anki.

## Contents

*   [1 Installation](#Installation)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Kanji stroke support](#Kanji_stroke_support)
    *   [2.2 Asian language support](#Asian_language_support)
*   [3 See also](#See_also)

## Installation

For the latest version of *Anki* [install](/index.php/Install "Install") the [anki](https://aur.archlinux.org/packages/anki/) package.

If you prefer to use Anki version 1, [install](/index.php/Install "Install") the [anki12](https://aur.archlinux.org/packages/anki12/) package. If you prefer to use Anki version 2.0, [install](/index.php/Install "Install") the [anki20-bin](https://aur.archlinux.org/packages/anki20-bin/) package.

**Note:** Both version 1 and 2.0 still rely on [QtWebKit for Qt 4](https://www.archlinux.org/todo/phasing-out-qtwebkit/). The [anki](https://aur.archlinux.org/packages/anki/) package uses QTWebEngine but is in *alpha*.

## Tips and tricks

### Kanji stroke support

[Install](/index.php/Install "Install") the [kanjistrokeorders-ttf](https://aur.archlinux.org/packages/kanjistrokeorders-ttf/) package if you want to display kanji stroke orders in Anki. You have to select this font inside Anki in your deck properties after installation.

### Asian language support

[Install](/index.php/Install "Install") the [mecab-ipadic](https://aur.archlinux.org/packages/mecab-ipadic/) package and the [kakasi](https://www.archlinux.org/packages/?name=kakasi) package.

Launch Anki, and inside Anki use "File->Download->Shared Plugin" to download and install the "Japanese Support" plugin, restart.

After creating a new deck, you need to select "Japanese" as the deck model in "deck properties" to have Japanese support. Make sure that the Japanese Support plugin is installed, otherwise you cannot select "Japanese" as the model.

## See also

*   [Mnemosyne](/index.php/Mnemosyne "Mnemosyne") - another open-source flashcard program using spaced repetition