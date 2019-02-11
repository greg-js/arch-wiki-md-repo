Related articles

*   [Internationalization](/index.php/Internationalization "Internationalization")
*   [Input Japanese using uim](/index.php/Input_Japanese_using_uim "Input Japanese using uim")

This article describes how to set up a Japanese language environment. It does not cover setting up Japanese input on the console.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Fonts](#Fonts)
    *   [1.1 Sans-serif](#Sans-serif)
    *   [1.2 Serif (and Sans-serif)](#Serif_(and_Sans-serif))
*   [2 Locale](#Locale)
*   [3 Input methods](#Input_methods)
    *   [3.1 Anthy](#Anthy)
    *   [3.2 libkkc](#libkkc)
    *   [3.3 Mozc](#Mozc)
    *   [3.4 SKK](#SKK)
    *   [3.5 Google CGI API for Japanese input](#Google_CGI_API_for_Japanese_input)
*   [4 See also](#See_also)

## Fonts

*See also [Fonts#Japanese](/index.php/Fonts#Japanese "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") for configuration or more detail.*

To use any Japanese input method, you need to have Japanese fonts installed.

Recommended Japanese fonts are as follows.

#### Sans-serif

*   [adobe-source-han-sans](https://github.com/adobe-fonts/source-han-sans) || [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) or [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts)

	Open-source OTF fonts developed by Adobe.

#### Serif (and Sans-serif)

*   [IPA fonts](http://ossipedia.ipa.go.jp/ipafont/) || [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont)

	An open source OTF font set including sans-serif (Gothic) and serif (Mincho) glyphs provided by Information-technology Promotion Agency, Japan (IPA).

If you want to show [2channel Shift JIS art](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art") properly, use one of the following fonts:

*   ipamona font (AUR: [ttf-ipa-mona](https://aur.archlinux.org/packages/ttf-ipa-mona/))
*   Mona font (AUR: [ttf-mona](https://aur.archlinux.org/packages/ttf-mona/))
*   Monapo font (AUR: [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/))

## Locale

*See [locale](/index.php/Locale "Locale") for details.*

You should have `ja_JP.UTF-8` enabled in `/etc/locale.gen`.

## Input methods

The following [input method](/index.php/Input_method "Input method") (IM) engines are available for Japanese:

| Back-end | [Fcitx](/index.php/Fcitx "Fcitx") | [IBus](/index.php/IBus "IBus") | [SCIM](/index.php/SCIM "SCIM") | [uim](/index.php/Uim "Uim") | [gcin](/index.php/Gcin "Gcin") | [hime-git](https://aur.archlinux.org/packages/hime-git/) |
| [Anthy](#Anthy) | [fcitx-anthy](https://www.archlinux.org/packages/?name=fcitx-anthy) | [ibus-anthy](https://www.archlinux.org/packages/?name=ibus-anthy) | [scim-anthy](https://www.archlinux.org/packages/?name=scim-anthy) | built-in | built-in | built-in |
| [libkkc](#libkkc) | [fcitx-kkc](https://www.archlinux.org/packages/?name=fcitx-kkc) | [ibus-kkc](https://www.archlinux.org/packages/?name=ibus-kkc) | – | – | – | – |
| [Mozc](/index.php/Mozc "Mozc") | [fcitx-mozc](https://www.archlinux.org/packages/?name=fcitx-mozc) | [ibus-mozc](https://aur.archlinux.org/packages/ibus-mozc/) | – | [uim-mozc](https://aur.archlinux.org/packages/uim-mozc/) | – | – |
| [SKK](#SKK) | [fcitx-skk](https://www.archlinux.org/packages/?name=fcitx-skk) | [ibus-skk](https://www.archlinux.org/packages/?name=ibus-skk) | – | built-in | – | – |

### Anthy

[Anthy](https://en.wikipedia.org/wiki/Anthy "wikipedia:Anthy") can convert Hiragana to Kanji. While Anthy is supported by all IM frameworks, it is effectively dead (its last release was 2009).[[1]](https://osdn.net/projects/anthy/)

[Install](/index.php/Install "Install") [anthy](https://www.archlinux.org/packages/?name=anthy) and the engine for your framework.

### libkkc

[libkkc](https://github.com/ueno/libkkc) ([libkkc](https://www.archlinux.org/packages/?name=libkkc)) provides a converter from Japanese Kana-string to Kana-Kanji-mixed-string. It was named after kkc.el in GNU Emacs, a simple Kana Kanji converter, while libkkc tries to convert sentences in a bit more complex way using N-gram language models. It is developed by a Red Hat engineer.

[Install](/index.php/Install "Install") the engine for your framework.

### Mozc

[Mozc](/index.php/Mozc "Mozc") is a Japanese Input Method Editor (IME) designed for multi-platform such as Chromium OS, Windows, Mac and Linux which originates from [Google Japanese Input](http://www.google.com/intl/ja/ime/).

Custom package [mozc-ut2](https://aur.archlinux.org/packages/mozc-ut2/) comes with [Mozc UT dictionary](http://www.geocities.jp/ep3797/mozc_01.html). The dictionary adds over 350,000 words into original.

See the article for the installation procedure.

### SKK

[SKK](https://github.com/ueno/libskk) (Simple Kana to Kanji conversion program) is a Japanese input method on Emacs. It was designed by Dr. Masahiko Sato (Professor Emeritus, Kyoto University) (old link) and created in 1987\. A unique feature of SKK is that it converts words one by one (single-word conversion), without analyzing syntax or grammar.

[Install](/index.php/Install "Install") the SKK dictionaries ([skk-jisyo](https://www.archlinux.org/packages/?name=skk-jisyo)) and the engine for your framework.

### Google CGI API for Japanese input

*Available IM frameworks: uim*

[Google CGI API for Japanese Input](http://www.google.co.jp/ime/cgiapi.html) (Google-CGIAPI-Jp) is CGI service to provide Japanese conversion on the Internet by Google. It can be used on [web browser](http://www.google.com/transliterate). Its conversion engine seems to be equivalent to Google Japanese Input, so conversion quality is probably better than Mozc.

**Note:** This service sends/receives preedits and candidates as plain text (as of 2012-09).

You can use it via uim. Choose "Google-CGIAPI-Jp" on uim-im-switcher-gtk/gtk3/qt4 or uim-pref-gtk/gtk3/qt4.

## See also

*   [Gentoo:How to read and write in Japanese](https://wiki.gentoo.org/wiki/How_to_read_and_write_in_Japanese "gentoo:How to read and write in Japanese")