## Contents

*   [1 O tomto dokumente](#O_tomto_dokumente)
*   [2 Bootovacia konzola](#Bootovacia_konzola)
*   [3 Nastavenie slovenského prostredia (Locale)](#Nastavenie_slovensk.C3.A9ho_prostredia_.28Locale.29)
*   [4 Klávesnica](#Kl.C3.A1vesnica)
*   [5 Fonty](#Fonty)
*   [6 Externé zdroje](#Extern.C3.A9_zdroje)

## O tomto dokumente

Tento dokument ponúka informácie o tom, ako nastaviť v Arch linuxe slovenské prostredie.

```
OpenI18N Diagram:
[http://www.openi18n.org/images/openi18n_diagram.png](http://www.openi18n.org/images/openi18n_diagram.png)

```

## Bootovacia konzola

V Súbore /etc/locale.gen odkomentujte znakovu sadu:

```
sk_SK   ISO-8859-2
# ak pouzivame UTF, mozeme odkomentovat i viac znakovych sad
sk_SK.UTF-8    UTF-8

```

Potom ich vygenerujeme:

```
locale-gen

```

V súbore /etc/rc.conf doplňte:

```
LOCALE="sk_SK.utf8"
TIMEZONE="Europe/Bratislava"

```

Ak chcete mať slovenskú klávesnicu aj pod konzolou, doplňte aj:

```
KEYMAP="sk-qwerty.map.gz"

```

## Nastavenie slovenského prostredia (Locale)

(a) Pre všetkých použivateľov: V súbore /etc/profile prepíšte:

```
export LANG="sk_SK.utf8"
export LC_ALL="sk_SK.utf8"

```

(b) Len pre konkrétneho používateľa: Vytvorte v domovskom adresári ($HOME) súbor .profile s týmto obsahom:

```
export LANG="sk_SK.utf8"
export LC_ALL="sk_SK.utf8"

```

## Klávesnica

Pre xorg7, v súbore /etc/X11/xorg.conf napíšte:

(a) Ak chcete **iba** slovenskú klávesnicu:

```
Option "XkbLayout"  "sk"
Option "XkbVariant" "qwerty"

```

(b) Ak chcete aj **US** aj **SK** klávesnicu:

```
Option "XkbLayout"  "us,sk"
Option "XkbVariant" ",qwerty"
Option "XkbOptions" "grp:alt_shift_toggle"

#pri prepinani zapne SCROLL LOCK a vypne CAPS LOCK.
Option "XKbOptions" "grp:alt_shift_toggle,grp_led:scroll,ctrl:nocaps,compose:ralt"

```

Poznámka: Uvedený príklad umožní slovenskú klávesnicu typu QWERTY.

Poznámka: Option "XkbRules" musí byť nastavený na hodnotu "xorg" (nie "xfree86").

## Fonty

Pre X postačia klasické fonty:

```
xorg-fonts-type1, xorg-fonts-100dpi (resp. 75dpi), xorg-fonts-misc, zíde sa i ttf-ms-fonts

```

## Externé zdroje

*   [Free Standards Group OpenI18N](http://www.openi18n.org/)