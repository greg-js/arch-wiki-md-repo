# Sinhala Unicode Support

This page explains how to get the Sinhala unicode support and sinhala unicode input to work using [IBus](/index.php/IBus "IBus") (sayura-ibus) or [scim](/index.php/Scim "Scim") (sayura-scim).

## Contents

*   [1 Sinhala Unicode Font](#Sinhala_Unicode_Font)
*   [2 Guide to install Sinhala Unicode Font](#Guide_to_install_Sinhala_Unicode_Font)
*   [3 Enabling Sinhala Locale](#Enabling_Sinhala_Locale)
*   [4 Sinhala Unicode Input Support](#Sinhala_Unicode_Input_Support)
    *   [4.1 sayura-ibus](#sayura-ibus)
    *   [4.2 sayura-scim](#sayura-scim)
    *   [4.3 scim configuration](#scim_configuration)
*   [5 Further Reading and More Information](#Further_Reading_and_More_Information)

## Sinhala Unicode Font

Install [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) from the [AUR](/index.php/AUR "AUR").

## Guide to install Sinhala Unicode Font

Download and Install **[lklug.ttf](http://sinhala.sourceforge.net/files/lklug.ttf)** Sinhala Unicode font file

```
sudo pacman -S wget
sudo wget -P /usr/share/fonts [http://sinhala.sourceforge.net/files/lklug.ttf](http://sinhala.sourceforge.net/files/lklug.ttf)

```

Then Run the following command

```
fc-cache -fv

```

And proceed to the below steps..

## Enabling Sinhala Locale

Edit /etc/locale.gen. Uncomment following line

```
si_LK UTF-8

```

Run following program

```
locale-gen

```

Immediately you'll be able to read Sinhala Unicode in your programs (If not You may need to restart the relavent programs. eg: Firefox)

## Sinhala Unicode Input Support

### sayura-ibus

Install [ibus-sayura](https://aur.archlinux.org/packages/ibus-sayura/) from the AUR. For more information about see [IBus](/index.php/IBus "IBus").

### sayura-scim

Install [scim-sayura](https://aur.archlinux.org/packages/scim-sayura/) from the AUR.

### scim configuration

More about [scim](/index.php/Scim "Scim") can be found [here](/index.php/Scim "Scim"). To enable scim add following lines to /etc/profile

```
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="scim"
export QT_IM_MODULE="scim"

```

## Further Reading and More Information

*   [sinhala linux](http://sinhala.sourceforge.net/) - **Official Homepage**
*   [sayura-scim](http://www.sayura.net/im/) - **Official Homepage**
*   [LKLUG](http://www.lug.lk/) - **Lanka Linux User Group (Sinhala Linux Mailing List)**
*   [Sinhala Unicode Group (සිංහල යුනිකෝඩ් සමූහය)](http://groups.google.com/group/Sinhala-Unicode)
*   [Enabling Unicode Sinhala in GNU/Linux HOWTO](http://www.nongnu.org/sinhala/doc/howto/sinhala-howto.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sinhala_Unicode_Support&oldid=392661](https://wiki.archlinux.org/index.php?title=Sinhala_Unicode_Support&oldid=392661)"