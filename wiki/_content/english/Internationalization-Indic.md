Related articles

*   [Internationalization](/index.php/Internationalization "Internationalization")

This page explains how setup your Arch installation in order to input [Indic languages](https://en.wikipedia.org/wiki/Indo-Aryan_languages "wikipedia:Indo-Aryan languages").

## Fonts

The following packages provide fonts for a variety of Indic scripts,

*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf)
*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/)

## Locale

Setting up the locale will ensure that applications use appropriate localizations when available. Setup your locale by following instructions [here](/index.php/Locale "Locale"). ```

## IME

Since, keyboards with Indic layouts are extremely rare, you are likely to want to use transliteration. IME tools will help you accomplish this. There are several choices to try out (which allow you to use input methods especially those defined in the m17n project). The m17n project (see [m17n-db](https://www.archlinux.org/packages/?name=m17n-db), [[1]](http://git.savannah.nongnu.org/cgit/m17n/m17n-db.git/tree/MIM) [[2]](http://www.nongnu.org/m17n/) and [[3]](https://lists.nongnu.org/mailman/listinfo/m17n-list)) provides transliteration schemes for Sanskrit, Assamese, Bengali, Burmese, Gujarati, Hindi, Kannada, Kashmiri, Maithili, Malayalam, Marathi, Nepali, Punjabi, Sindhi, Tamil, Telugu & Tibetan amongst others. So modules which allow a given IME to use [m17n-db](https://www.archlinux.org/packages/?name=m17n-db) merit installation. For example, if you're installing [ibus](https://www.archlinux.org/packages/?name=ibus), do install [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) as well.

[Internationalization](/index.php/Internationalization "Internationalization") has a good list of IME-s. The following support m17n-db input methods:

*   [IBus](/index.php/IBus "IBus")
*   [Fcitx](/index.php/Fcitx "Fcitx")