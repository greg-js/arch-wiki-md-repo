# Internationalization/Japanese

Related articles

*   [Internationalization](/index.php/Internationalization "Internationalization")
*   [Input Japanese using uim](/index.php/Input_Japanese_using_uim "Input Japanese using uim")

This document provides instructions on how to set up a Japanese language environment on an Arch linux installation. This document will not cover setting up Japanese input on the console.

## Contents

*   [1 Fonts](#Fonts)
    *   [1.1 Sans-serif](#Sans-serif)
    *   [1.2 Serif (and Sans-serif)](#Serif_.28and_Sans-serif.29)
*   [2 Locale](#Locale)
*   [3 Input in Xorg](#Input_in_Xorg)
    *   [3.1 Input Method Framework](#Input_Method_Framework)
    *   [3.2 Input method](#Input_method)
        *   [3.2.1 Mozc](#Mozc)
        *   [3.2.2 libkkc](#libkkc)
        *   [3.2.3 SKK](#SKK)
        *   [3.2.4 Google CGI API for Japanese input](#Google_CGI_API_for_Japanese_input)
        *   [3.2.5 Anthy](#Anthy)

## Fonts

_see also [Fonts](/index.php/Fonts "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") for configuration or more detail._

To use any Japanese input method, you need to have Japanese fonts installed.

Recommended Japanese fonts are as follows.

#### Sans-serif

*   [adobe-source-han-sans](https://github.com/adobe-fonts/source-han-sans) || [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) or [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts)

NaN

#### Serif (and Sans-serif)

*   [IPA fonts](http://ossipedia.ipa.go.jp/ipafont/) || [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont)

NaN

If you want to show [2channel Shift JIS art](http://en.wikipedia.org/wiki/2channel_Shift_JIS_art) properly, use one of the following fonts:

*   ipamona font (AUR: [ttf-ipa-mona](https://aur.archlinux.org/packages/ttf-ipa-mona/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ttf-ipa-mona)]</sup>)
*   Monapo font (AUR: [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/)<sup><small>AUR</small></sup>)

## Locale

_See [locale](/index.php/Locale "Locale") for detail_

You should have `ja_JP.UTF-8` enabled in `/etc/locale.gen`.

## Input in Xorg

### Input Method Framework

Input method (IM) frameworks act as frontends to various input methods and libraries, allowing the user to switch between different languages with ease.

You can use the following frameworks:

*   [Fcitx](/index.php/Fcitx "Fcitx")
*   [IBus](/index.php/IBus "IBus")
*   [uim](/index.php/Input_Japanese_using_uim "Input Japanese using uim")

See each articles for detail.

**Note:** [SCIM](/index.php/SCIM "SCIM") is dead project. You should not use it.

### Input method

#### Mozc

_Available IM Frameworks: Fcitx, IBus, uim_

_See [Mozc](/index.php/Mozc "Mozc")_

[Mozc](http://code.google.com/p/mozc/) is a Japanese Input Method Editor (IME) designed for multi-platform such as Chromium OS, Windows, Mac and Linux which originates from [Google Japanese Input](http://www.google.com/intl/ja/ime/).

Custom package [mozc-ut](https://aur.archlinux.org/packages/mozc-ut/)<sup><small>AUR</small></sup> comes with [Mozc UT dictionary](http://www.geocities.jp/ep3797/mozc_01.html). The dictionary adds over 350,000 words into original.

#### libkkc

_Available IM Frameworks: Fcitx, IBus_

[libkkc](https://bitbucket.org/libkkc/) provides a converter from Japanese Kana-string to Kana-Kanji-mixed-string. It was named after kkc.el in GNU Emacs, a simple Kana Kanji converter, while libkkc tries to convert sentences in a bit more complex way using N-gram language models. It is developed by a Red Hat engineer.

Install [fcitx-kkc](https://www.archlinux.org/packages/?name=fcitx-kkc) (for Fcitx) or [ibus-kkc](https://www.archlinux.org/packages/?name=ibus-kkc) (for IBus).

#### SKK

_Available IM Frameworks: Fcitx, IBus, uim_

[SKK](http://openlab.jp/skk/index.html) (Simple Kana to Kanji conversion program) is a Japanese input method on Emacs. It was designed by Dr. Masahiko Sato (Professor Emeritus, Kyoto University) (old link) and created in 1987\. A unique feature of SKK is that it converts words one by one (single-word conversion), without analyzing syntax or grammar.

Install [skk-jisyo](https://www.archlinux.org/packages/?name=skk-jisyo) and [fcitx-skk](https://www.archlinux.org/packages/?name=fcitx-skk) (for Fcitx) or [ibus-skk](https://www.archlinux.org/packages/?name=ibus-skk) (for IBus). uim supports SKK itself.

#### Google CGI API for Japanese input

_Available IM Framewworks: uim_

[Google CGI API for Japanese Input](http://www.google.co.jp/ime/cgiapi.html) (Google-CGIAPI-Jp) is CGI service to provide Japanese conversion on the Internet by Google. It can be used on [web browser](http://www.google.com/transliterate). Its conversion engine seems to be equivalent to Google Japanese Input, so conversion quality is probably better than Mozc.

**Note:** This service sends/receives preedits and candidates as plain text (as of 2012-09).

You can use it via uim. Choose "Google-CGIAPI-Jp" on uim-im-switcher-gtk/gtk3/qt4 or uim-pref-gtk/gtk3/qt4.

#### Anthy

Anthy is factually dead project.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Internationalization/Japanese&oldid=406955](https://wiki.archlinux.org/index.php?title=Internationalization/Japanese&oldid=406955)"