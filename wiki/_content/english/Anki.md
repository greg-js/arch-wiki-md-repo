[Anki](http://ankisrs.net/) is a [spaced repetition](https://en.wikipedia.org/wiki/Spaced_repetition "wikipedia:Spaced repetition") system (SRS), a program which allows you to create, manage and review [flashcards](https://en.wikipedia.org/wiki/Flashcard "wikipedia:Flashcard"). Anki is very flexible and also allows the creation of templates. Apps for Android and iOS as well as a web interface can be used to interact with the user's flashcard database. Anki supports [addons](https://ankiweb.net/shared/addons/), written in [python](/index.php/Python "Python").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Flashcards](#Flashcards)
    *   [2.1 Older versions](#Older_versions)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Kanji stroke support](#Kanji_stroke_support)
    *   [3.2 Asian language support](#Asian_language_support)
    *   [3.3 Self-hosted sync server](#Self-hosted_sync_server)
    *   [3.4 Dark theme](#Dark_theme)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [anki](https://www.archlinux.org/packages/?name=anki) package. Or, for the development version, install the [anki-git](https://aur.archlinux.org/packages/anki-git/) package.

By default, cards are synchronized using anki's web server, but you can use your own [anki-sync-server](https://aur.archlinux.org/packages/anki-sync-server/).

## Flashcards

Flashcards can be obtained by:

*   Creating them inside Anki, organized in decks and possibly tagged. Cards can contain audio, pictures and even [TeX](/index.php/TeX "TeX") formulas;
*   Downloading them, grouped in an existing [shared deck](https://ankiweb.net/shared/decks/) (e.g. top 1000 words in a language);
*   Generating them as a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values "wikipedia:Comma-separated values") that will be imported in Anki.

### Older versions

If you prefer to use version 1.2, [install](/index.php/Install "Install") the [anki12](https://aur.archlinux.org/packages/anki12/) package, or if you prefer to use version 2.0, [install](/index.php/Install "Install") the [anki20-bin](https://aur.archlinux.org/packages/anki20-bin/) package.

**Warning:** Versions before 2.1 use [QtWebKit for Qt 4](https://www.archlinux.org/todo/phasing-out-qtwebkit/), which is considered insecure.

## Tips and tricks

### Kanji stroke support

[Install](/index.php/Install "Install") the [kanjistrokeorders-ttf](https://aur.archlinux.org/packages/kanjistrokeorders-ttf/) package if you want to display kanji stroke orders in Anki. You have to select this font inside Anki in your deck properties after installation.

### Asian language support

[Install](/index.php/Install "Install") the [mecab-ipadic](https://aur.archlinux.org/packages/mecab-ipadic/) package and the [kakasi](https://www.archlinux.org/packages/?name=kakasi) package.

Launch Anki, and inside Anki use *File > Download > Shared Plugin* to download and install the "Japanese Support" plugin, restart.

After creating a new deck, you need to select "Japanese" as the deck model in "deck properties" to have Japanese support. Make sure that the Japanese Support plugin is installed, otherwise you cannot select "Japanese" as the model.

### Self-hosted sync server

AnkiWeb is a proprietary service. If you prefer a self-hosted free (as in freedom) alternative, you can use [anki-sync-server](https://github.com/tsudoko/anki-sync-server). One tutorial how to set it up is available [here](http://genedan.com/no-127-ankisyncd-a-custom-sync-server-for-anki-2-1/).

### Dark theme

Anki UI may me unreadable with dark GTK theme. You may want to install an addon to fix that (e.g. [1496166067](https://ankiweb.net/shared/info/1496166067) and *View > Nigh mode > Enable night mode*).

## Troubleshooting

If Anki core dumps at launch with error "qt: No suitable graphics backend found" the following [may resolve](https://anki.tenderapp.com/discussions/ankidesktop/34554-instalation-not-run-after-install):

```
echo auto > ~/.local/share/Anki2/gldriver

```

## See also

*   [Mnemosyne](/index.php/Mnemosyne "Mnemosyne") - another open-source flashcard program using spaced repetition