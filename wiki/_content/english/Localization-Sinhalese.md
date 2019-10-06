This article describes how to get [Sinhalese](https://en.wikipedia.org/wiki/Sinhalese_language "wikipedia:Sinhalese language") Unicode support and Sinhalese Unicode input to work using [IBus](/index.php/IBus "IBus") (sayura-ibus) or [scim](/index.php/Scim "Scim") (sayura-scim).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Fonts](#Fonts)
    *   [1.1 Guide to install Sinhala Unicode Font](#Guide_to_install_Sinhala_Unicode_Font)
*   [2 Locale](#Locale)
*   [3 Input methods](#Input_methods)
    *   [3.1 iBus](#iBus)
    *   [3.2 FCITX](#FCITX)
*   [4 See also](#See_also)

## Fonts

For Sinhala support, you can install any of these [fonts](/index.php/Fonts "Fonts"):

*   [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts) - Noto Sans Sinhala, a sans serif font.
*   [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts) - FreeSerif, a serif font.
*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - LKLUG, a serif font.

### Guide to install Sinhala Unicode Font

Download [http://sinhala.sourceforge.net/files/lklug.ttf](http://sinhala.sourceforge.net/files/lklug.ttf) and place it in `/usr/share/fonts`.

Then Run the following command

```
fc-cache -fv

```

And proceed to the below steps..

## Locale

Edit /etc/locale.gen. Uncomment following line

```
si_LK UTF-8

```

Run following program

```
locale-gen

```

Immediately you'll be able to read Sinhala Unicode in your programs (If not You may need to restart the relavent programs. eg: Firefox)

## Input methods

### iBus

For Sinhala support on [ibus](https://www.archlinux.org/packages/?name=ibus) install the following package

*   [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) - M17N engine for IBus

Logout from the current session and log in again after installing. After that, Sinhala input methods should be available on input method configuration panel.

### FCITX

The only packaged fcitx based [input method](/index.php/Input_method "Input method") for Sinhalese is [fcitx-sayura](https://www.archlinux.org/packages/?name=fcitx-sayura) for [Fcitx](/index.php/Fcitx "Fcitx").

While there are also [ibus-sayura](https://github.com/pravins/ibus-sayura) and [scim-sayura](https://www.sayura.net/im/), they are no longer in the [AUR](/index.php/AUR "AUR") (albeit they can still be found in the [AUR archive](/index.php/AUR_archive "AUR archive")).

## See also

*   [sinhala linux](http://sinhala.sourceforge.net/) - **Official Homepage**
*   [sayura-scim](http://www.sayura.net/im/) - **Official Homepage**
*   [LKLUG](http://www.lug.lk/) - **Lanka Linux User Group (Sinhala Linux Mailing List)**
*   [Sinhala Unicode Group (සිංහල යුනිකෝඩ් සමූහය)](http://groups.google.com/group/Sinhala-Unicode)
*   [Enabling Unicode Sinhala in GNU/Linux HOWTO](http://www.nongnu.org/sinhala/doc/howto/sinhala-howto.html)