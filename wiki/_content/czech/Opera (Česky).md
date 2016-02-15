[Opera](http://www.opera.com) je plně vybavený webový prohlížeč od Norské společnosti Opera Software ASA. Má uzavřený zdrojový kód, ale někteří lidé raději říkají, že je **"free as parking"**.

## Contents

*   [1 Proč bych měl používat Operu?](#Pro.C4.8D_bych_m.C4.9Bl_pou.C5.BE.C3.ADvat_Operu.3F)
*   [2 Proč bych NEMĚL používat Operu?](#Pro.C4.8D_bych_NEM.C4.9AL_pou.C5.BE.C3.ADvat_Operu.3F)
*   [3 Jak nainstalovat Operu?](#Jak_nainstalovat_Operu.3F)
    *   [3.1 Opera a fonty od Microsoftu](#Opera_a_fonty_od_Microsoftu)
    *   [3.2 Různé vychytávky](#R.C5.AFzn.C3.A9_vychyt.C3.A1vky)

## Proč bych měl používat Operu?

*   Je rychlá a odlehčená.
*   Podporuje standardy.
*   Je velice dobře přizpůsobitelná.
*   Ihned po instalaci umožňuje prohlížení webu, gesta myší, blokování reklam, zabudovaný je mailový klient, bittorent klient a IRC klient. A další...
*   Je profesionální: **žádný nabobtnalý kód, žádné úniky paměti, žádné mrznutí, žádné pády**.

## Proč bych NEMĚL používat Operu?

*   Není [svobodná](http://www.gnu.org/philosophy/free-sw.html). Je to [proprietární software](http://en.wikipedia.org/wiki/Proprietary_software).
*   Je to [Qt](http://en.wikipedia.org/wiki/Qt_(toolkit)) aplikace, což znamená, že pokud nepoužíváte [KDE (Česky)](/index.php/KDE_(%C4%8Cesky) "KDE (Česky)"), tak vyžaduje dodatečné knihovny, čímž zabírá další paměť.
*   Některé webové stránky se nezobrazují korektně, protože nedbají na standardy (Opera se drží standardů).

## Jak nainstalovat Operu?

```
# pacman -S opera

```

### Opera a fonty od Microsoftu

Pokud jste měli nainstalovaný balíček ttf-ms-fonts v době instalace Opery, Opera použije tyto fonty, které se Vám nemusí líbit. Aby Opera používala defaultní fonty z Gnome, či jakékoli jiné, které jsou Vaše defaultní, odinstalujte balíček ttf-ms-fonts, a nainstalujte Operu znova.

Fonty se dají také nastavit v Tools -> Preferences -> Advanced -> Fonts
(Nástroje -> Nastavení -> Pokročilé volby -> Písma)

### Různé vychytávky

*   K odstranění icony v systémovém panelu, spusťte Operu s volbou _-notrayicon_.
*   Aby menu vypadalo pěkne, nainstalujte polymer:

```
# pacman -S polymer

```

následně spusťte **qtconfig** (bude umístěn v /opt/qt/bin) a nastavte _polymer_ téma pro Qt applikace.

*   Naneštěstí Opera těžce závisí na fontech z Windows. Ujistěte se, že máte nainstalován balíček _ttf-ms-fonts_, nebo (ještě lépe) zkopírované truetype fonty z Windows, například v /usr/share/fonts/TTF.
*   K vylepšení výkonu flash pluginu v Opeře, před spuštěním Opery prosťe spusťte:

```
# export OPERAPLUGINWRAPPER_PRIORITY=0

```

Můžete si ještě tuto proměnnou definovat v souboru /etc/profile.