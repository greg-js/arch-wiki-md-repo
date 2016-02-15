This page explains how setup your Arch installation in order to input Indic languages.

## Fonts

The following packages provide fonts for a variety of Indic scripts,

*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf)
*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/)

## Locale

Setting up the locale will ensure that applications use appropriate localizations when available. Setup your locale by following instructions [here](/index.php/Locale "Locale").

## Ibus

Since, Keyboards with Indic layouts are extremely rare, you are likely to want to use transliteration. The package [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) provides transliteration schemes for Sanskrit, Assamese, Bengali, Burmese, Gujarati, Hindi, Kannada, Kashmiri, Maithili, Malayalam, Marathi, Nepali, Punjabi, Sindhi, Tamil, Telugu & Tibetan amongst others.

*   [Install](/index.php/Install "Install") the [ibus](https://www.archlinux.org/packages/?name=ibus) and [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) packages
*   Start Ibus-daemon:

```
# ibus-daemon &

```

*   Add input methods by clicking on 'Preferences' under the system-tray icon, or via:

```
# ibus-setup

```