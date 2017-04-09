[Anki](http://ankisrs.net/) is an [SRS](https://en.wikipedia.org/wiki/Spaced_repetition "wikipedia:Spaced repetition") (Spaced Repetition System), a program which allows you to create, manage and review [flashcards](https://en.wikipedia.org/wiki/Flashcard "wikipedia:Flashcard"). Because spaced repetition algorithms are a lot more efficient than traditional study methods, you can either greatly decrease your time spent studying, or greatly increase the amount you learn. Anki is very flexible and also allows the creation of templates. Android and iOS apps are available and synchronization between devices is supported.

This guide shows you how to install Anki.

## Contents

*   [1 Installation](#Installation)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Kanji Stroke Support](#Kanji_Stroke_Support)
    *   [2.2 Asian Language Support](#Asian_Language_Support)
*   [3 See also](#See_also)

## Installation

If you prefer to use Anki version 1, install [anki12](https://aur.archlinux.org/packages/anki12/) from the [AUR](/index.php/AUR "AUR").

If you prefer to use Anki version 2.0, install [anki20-bin](https://aur.archlinux.org/packages/anki20-bin/) from the [AUR](/index.php/AUR "AUR").

**Note:** Both packages still rely on [QtWebKit for Qt 4](https://www.archlinux.org/todo/phasing-out-qtwebkit/).

## Tips and tricks

### Kanji Stroke Support

Install [kanjistrokeorders-ttf](https://aur.archlinux.org/packages/kanjistrokeorders-ttf/) from the [AUR](/index.php/AUR "AUR") if you want to display kanji stroke orders in Anki. You have to select this font inside Anki in your deck properties after installation.

### Asian Language Support

Install [mecab-ipadic](https://aur.archlinux.org/packages/mecab-ipadic/) from the [AUR](/index.php/AUR "AUR").

Install [kakasi](https://www.archlinux.org/packages/?name=kakasi) from the [Official repositories](/index.php/Official_repositories "Official repositories").

Launch Anki, and inside Anki use "File->Download->Shared Plugin" to download and install the "Japanese Support" plugin, restart.

After creating a new deck, you need to select "Japanese" as the deck model in "deck properties" to have Japanese support. Make sure that the Japanese Support plugin is installed, otherwise you cannot select "Japanese" as the model.

## See also

*   [Mnemosyne](/index.php/Mnemosyne "Mnemosyne") - another open-source flashcard program using spaced repetition