[dmenu](http://tools.suckless.org/dmenu) er en hurtig og letvægtig dynamisk menu til X. Den læser tilfældig tekst fra standard input (stdin) og konstruerer en menu med et punkt per linje. Brugeren kan da vælge et punkt, ved brug af piletasterne eller ved at taste en del af navnet, og linjen printes til standard output (stdout). dmenu_run er et omslag (wrapper), der udgives sammen med dmenu distributionen, som gør det muligt at anvende dmenu som en programstarter (application launcher).

## Contents

*   [1 Installation](#Installation)
*   [2 Konfiguration](#Konfiguration)
*   [3 Mærkelig segmenteringsfejl (segfault)](#M.C3.A6rkelig_segmenteringsfejl_.28segfault.29)
*   [4 Understøttelse af flere skrifttyper](#Underst.C3.B8ttelse_af_flere_skrifttyper)
*   [5 Eksterne ressourcer](#Eksterne_ressourcer)

## Installation

Det er nemt at installere dmenu:

```
# pacman -S dmenu

```

og programstarteren køres således:

```
$ dmenu_run

```

## Konfiguration

Nu vil du formentlig gerne forbinde kommandoen `dmenu_run` til en kombination af tastetryk, altså oprette en genvejstast til programstarteren. Dette kan gøres gennem konfiguration af din window manager eller dit desktop environment, eller ved hjælp af et program som [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys). Se [Hotkeys](/index.php/Hotkeys "Hotkeys") artiklen for mere information og undersøg eventuelt også artiklen hørende til din window manager eller dit desktop environment. Derudover er det rart at have dmenu [Prelink](/index.php/Prelink "Prelink")'et.

## Mærkelig segmenteringsfejl (segfault)

Hvis udførelse af `dmenu_run` resulterer i en fejl lignende denne:

```
$ dmenu_run
/usr/bin/dmenu_run: line 15: 1879 Segmentation fault           dmenu "$@" < "$cache"

```

og `dmenu` bryder sammen som følger:

```
$ echo "blahblahblah" | dmenu
no locale support
Segmentation fault

```

Vær sikker på at miljøvariablen `$LANG` er sat til noget gyldigt, f.eks. "en_US.UTF-8" eller "da_DK.UTF-8", i /etc/locale.conf.

Husk at værdien af `$LANG` skal udkommenteres i /etc/locale.gen og genereres via `locale-gen`.

## Understøttelse af flere skrifttyper

dmenu kan tilrettes (patches) således at det er muligt at anvende flere skrifttyper, hvilket ellers ikke ser ud til at være muligt. Den tilrettede udgave kan findes i [AUR](https://aur.archlinux.org/packages/dmenu-xft/). Ved brug af denne udgave kan skrifttyper som f.eks. Droid Sans Mono vælges:

```
$ dmenu_run -fn 'Droid Sans Mono-9'

```

## Eksterne ressourcer

*   [dmenu](http://tools.suckless.org/dmenu) – Den officielle dmenu hjemmeside.
*   [Yeganesh](http://dmwit.com/yeganesh) – et lille omslag (wrapper) der ordner kommandoer ud fra deres popularitet.
*   [dmenu-launch (AUR)](https://aur.archlinux.org/packages.php?ID=33379) – En simpel demnu-baseret programstarter, som kan køre programfiler og XDG genveje.
*   [Dmenu Hacking thread](https://bbs.archlinux.org/viewtopic.php?id=80145) – Dmenu hacking tråd på Arch Linux forummet.