**[CDM](http://cdm.ghost1227.com)** je minimalistická, přesto plně vybavená náhrada přihlašovacích manažerů, jako je [SLiM](/index.php/SLiM "SLiM"),[GDM](/index.php/GDM "GDM") a [Qingy](/index.php/Qingy "Qingy"), která poskytuje rychlý, na dialozích založený přihlašovací systém bez nutnosti použít X Window System nebo nestabilní Qingy. CDM je napsáno je v čistém bash, nemá žádné závislosti, podporuje víceuživatelská sezení a umožňuje spouštět prakticky každé DE/WM.

Balíček je dostupný v repozitáři [AUR](https://aur.archlinux.org/packages.php?K=cdm).

## Contents

*   [1 Konfigurace](#Konfigurace)
*   [2 Spouštění X](#Spou.C5.A1t.C4.9Bn.C3.AD_X)
*   [3 Vlastní příkazy](#Vlastn.C3.AD_p.C5.99.C3.ADkazy)
*   [4 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)

## Konfigurace

CDM lze konfigurovat editací souboru `/etc/cdmrc`. Je plně zdokumentován a snadný k pochopení.

Před startem CDM by mělo být minimálně nastaveno toto:

```
wmbinlist=(awesome openbox-session **startkde startxfce4 gnome-session**)

wmdisplist=(Awesome Openbox **KDE Xfce Gnome**)

```

A jakékoliv další DE/WM, které používáte.

## Spouštění X

Přihlašte se do konzole a vyberte si z menu preferované sezení (nebo konzoli, je-li dostupná).

Další uživatelé se mohou přihlásit přepnutím na tty1 (ctrl+alt+f1). Pokud je uživatel již přihlášen, CDM automaticky aktivuje jeho již existující sezení.

## Vlastní příkazy

**Note:** CDM má nyní možnost povolit zabudovanou podporu vypnutí PC, nicméně tato sekce je ponechána jako návod.

Pokud chcete přidat příkaz, jako je např. vypnutí PC, který potřebuje parametry, je třeba příkaz uložit jako spustitelný skript a tento skript s celou cestou přidat na řádek wmbinlist v souboru *./etc/cdmrc. Např. vypnutí PC:

*   /script/shutdown

```
#!/bin/bash

shutdown -h now

```

*   /etc/cdmrc

```
wmbinlist=( ... /script/shutdown ... )

```

## Další zdroje

[Homepage (standardní)](http://cdm.ghost1227.com) / [Homepage (grafická)](http://cdm.ghost1227.com/X11)

[The Console Display Manager](https://bbs.archlinux.org/viewtopic.php?id=84408) - vlákno Archlinux fóra, týkající se CDM

[Balíček Aur](https://aur.archlinux.org/packages.php?ID=31879)