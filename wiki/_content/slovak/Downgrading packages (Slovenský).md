Nasledujúci text popisuje postup pre downgrade balíčku na staršiu než aktuálnu verziu. Tento postup nieje doporučovaný a je nevyhnutný výhradne v prípade zanesenia chýb do aktuálnej verzie.

**Poznámka vývojára:**

Dôkladne zvážte svoje dôvody k downgrade. Ak je dôvodom chyba, pomôžte prosím týmu Arch linuxu i upstream vývojárom tým, že obetujete pár minút tvorbou bug reportu. Nakoľko Arch linux je rolling release distribúcia, budete nepretržite pracovať s novými verziami balíčkov a čas od času narážať na chyby v nich.

My i upstream vývojári oceňujeme toto úsilie. Ušetrí nám hodiny testovania, a pomôže nám vydávať stabilnejší software.

## Contents

*   [1 Dôvody](#D.C3.B4vody)
*   [2 Detaily](#Detaily)
*   [3 Ako na downgrade balíčku](#Ako_na_downgrade_bal.C3.AD.C4.8Dku)
*   [4 Nájdenie staršej verzie](#N.C3.A1jdenie_star.C5.A1ej_verzie)
    *   [4.1 Out-Of-Sync Mirrory](#Out-Of-Sync_Mirrory)
    *   [4.2 ARM](#ARM)
    *   [4.3 Kompilácia balíčku](#Kompil.C3.A1cia_bal.C3.AD.C4.8Dku)
*   [5 Doplňujúce informácie](#Dopl.C5.88uj.C3.BAce_inform.C3.A1cie)
*   [6 Ignorovanie závislostí](#Ignorovanie_z.C3.A1vislost.C3.AD)
*   [7 Ako zabrániť upgradu konkrétneho balíčku](#Ako_zabr.C3.A1ni.C5.A5_upgradu_konkr.C3.A9tneho_bal.C3.AD.C4.8Dku)
*   [8 Návrat do stabilného stavu](#N.C3.A1vrat_do_stabiln.C3.A9ho_stavu)
*   [9 Pozri ja](#Pozri_ja)

## Dôvody

Downgrading je proces, pri ktorom je odinštalovaná aktuálna verzia balíčku a nahradená bezprostredne predošlou či ľubovoľnou staršou verziou.

Medzi dôvody okrem iného patrí: aktuálna verzia obsahuje chybu, neobsahuje požadovanú funkcionalitu alebo ide o experimentálnu verziu balíčku a užívateľ považuje za jednoduchšie vrátiť sa ku staršej verzii než čakať na vydanie novej.

Tento proces môže potenciálne viesť k downgradu iných balíčkov. Po inštalácii veľkého množstva testovacích či experimentálnych balíčkov a rozsiahlejších zmenách konfigurácie môže byť jednoduchšie reinštalovať systém než pokúšať sa o downgrade.

## Detaily

Nutno pamätať na nasledujúce fakty. Je potreba prehodnotiť závislosti každého balíčku nakoľko funkcionalita požadovaných závislostí sa môže s každou verziou meniť. Úspešné riešenie preto musí zahrnovať i downgrade závislých balíčkov.

Ďalej je nutné uistiť sa, že dané balíčky neboli odstránené zo systému, prípadne že sú dostupné z iných zdrojov. Rolling release systém repozitárov Arch Linuxu je aktualizovaný automaticky bez zálohy starších verzií balíčkov.

Zvýšená opatrnosť je nutná pri zmene konfiguračných súborov a skriptov. V súčastnosti je možne spoľahnúť sa na pacman za predpokladu, že neboli obídené niektoré z jeho ochranných mechanizmov.

Vývojári pracujú na koncepte Arch Rollback Mechine, ktorý čaká na zapracovanie do nástroju pacman. Až sa tak stane, bude táto činnosť kompletne automatizovaná. Dovtedy, postupujte podľa nasledujúcich inštrukcií.

## Ako na downgrade balíčku

*   Q: Použil som **pacman -Syu** a balíček XYZ bol upgradovaný z verzie M na verziu N. Tento balíček nefunguje správne. Ako sa môžem vráti späť k verzii M.
*   A: Za predpokladu, že cache balíčkov nebola zmazaná pomocou **pacman -Scc**, mali by byť staršie verzie balíčku v **/var/cache/pacman/pkg**. Takýto balíček môže byť znovu nainštalovaný pomocou **pacman -U pkgname-olderpkgver.pkg.tar.gz**. Ak tento balíček leží v inom adresári, je nutné zadať plnú cestu k nemu.

Tento proces odstráni aktuálnu verziu balíčku a nahradí ju zvolenou verziou zo všetkými jej závislosťami.

**Note:** Pri zmene fundamentálnych častí systému, môže nastať situácia v ktorej je potreba nahradiť desiatky balíčkov ich staršou verziou. Tieto balíčky nemusia byť dostupné a bude nutné ich znovu obstarať ručne, balíček po balíčku. Zo vzrastajúcim počtom závislostí sa tiež zvyšuje riziko zavlečenia nežiaducej verzie iného balíčku.

V repozitári AUR existuje balíček [downgrade](https://aur.archlinux.org/packages.php?ID=31937) ktorý automatizuje popisovaný postup. Tento jednoduchý bash script prehľadá lokálnu cache spolu s [A.R.M.](/index.php/Downgrade#ARM "Downgrade") v snahe nájsť staršie verzie balíčkov. Následne stačí zvoliť ktorý balíček nainštalovať. Pre viac informácií použite **downgrade --help**.

## Nájdenie staršej verzie

Existujú tri spôsoby ako postupovať.

#### Out-Of-Sync Mirrory

Ak lokálna cache neobsahuje požadovanú verziu balíčku, je možne, že niektorý s mirrorov je [neaktualizovaný](http://users.archlinux.de/~gerbra/mirrorcheck.html) a obsahuje balíček v požadovanej verzii.

Tiež je vhodné skontrolovať mirror ktorý balíčky archivuje:

*   [http://schlunix.org/?page_id=11](http://schlunix.org/?page_id=11)

#### ARM

Archív [Arch Rollback Machine (ARM)](http://arm.konnichi.com/) zaznamenáva snímky repozitárov od 1\. novembra 2009.

Pre záujemcov o aktuality projektu ARM je tu oznámenie a [diskusia](https://bbs.archlinux.org/viewtopic.php?id=53665)

Cieľom bolo navrhnúť systém URL tak, aby umožňovali rollback celého systému pomocou nástrojov wget a pacman do stavu v konkrétny deň. K ručnému vyhľadaniu je možné použiť [ARM vyhľadávanie](http://arm.konnichi.com/search/).

#### Kompilácia balíčku

V najhoršom prípade, ak nieje možné obstarať pôvodný balíček, je nutné ho znovu skompilovať. K tomu je potrebné upraviť súbor PKGBUILD požadovaného balíčku tak aby používal staršie verzie zdrojov. Tiež je možné vyhľadať balíček na [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/).

*   V detailoch balíčkov kliknite na _SVN Entries_ a zvoľte _log_.
*   Vyhľadajte požadovanú verziu, kliknite na _path_.
*   Stiahnite súbory z tohto adresára.
*   Zostavte balíček pomocou makepkg.

## Doplňujúce informácie

Bežný spôsob ako konfigurovať správu balíčkov je úprava súboru `/etc/pacman.conf` (typicky vyžaduje oprávnenia superužívateľa). Síce je možné konfiguráciu spravovať priamo z GUI, pomocou nástrojov ako je napríklad Shaman, čas od času je lepšie učiniť tak z terminálu. Doporučuje sa pri tejto príležitosti vyčistiť konfiguračný súbor od nahromadených nečistôt.

Najčastejšie sú upravované lokácie repozitárov, v ktorých pacman hľadá balíčky. Zakomentovaním existujúcich repozitárov, pomocou znaku '#' na začiatku riadku, sa repozitár stane pre systém správy balíčkov nedostupným.

Napríklad, pre pridanie repozitáru ARM stačí zakomentovať pôvodný zdroj a pridať nový v nasledujúcom formáte:

```
[core]
#Server=[http://mirrors.gigenet.com/archlinux/core/os/i686](http://mirrors.gigenet.com/archlinux/core/os/i686)
Server=[http://arm.konnichi.com/2009/11/01/core/os/i686](http://arm.konnichi.com/2009/11/01/core/os/i686)

```

V tomto príklade dátum určuje dostupné balíčky ku dňu 1\. novembra 2009\. Repozitáre ARM nie sú ničím iným, než snímkom oficiálnych repozitárov. Pre tieto účely stačí upraviť `/etc/pacman.d/mirrorlist` a umiestniť ARM na prvú pozíciu.

Napríklad pre synchronizáciu všetkých balíčkov s [http://arm.konnichi.com/2009/11/01/$repo/os/i686](http://arm.konnichi.com/2009/11/01/$repo/os/i686):

```
pacman -Syy  # obnoví databázu balíčkov
pacman -Suu  # downgraduje všetky balíčky, ktoré mali v daný deň nižšiu verziu

```

Samotný tento postup nezaručuje bezproblémový rollback nakoľko sa môžu vyskytnúť konflikty medzi verziami. Tiež môže byť užitočné navštíviť globálny mirror, napríklad [http://arm.konnichi.com/core/os/i686](http://arm.konnichi.com/core/os/i686) (pozor na absenciu dátumu).

## Ignorovanie závislostí

*   Q: V downgrade balíčku my bránia jeho závislosti, je možné ich ignorovať?
*   A: Ignorovať závislosti balíčku je možné pomocou prepínaču '-d' takto **pacman -Ud pkgpkgname-olderpkgver.pkg.tar.gz**. Ignorovanie závislostí môže spôsobiť nestabilitu systému.

## Ako zabrániť upgradu konkrétneho balíčku

*   Q: Ako zabrániť upgradu balíčku po downgrade?
*   A: Pomocou premennej "IgnorePkg" v súbore `/etc/pacman.conf`.

`"IgnorePkg = package1 package2 ..."` v súbore `pacman.conf` zabráni upgrade konkrétnych balíčkov pri upgrade systému pomocou --sysupgrade.

## Návrat do stabilného stavu

*   Q: Je možné vrátiť systém do podoby v ktorej bol včera?
*   A: S použitím pravidelných snímkov disku je to jednoduché.

Pre tvorbu a správu snímkov disku je možné použiť logical volume manager ([LVM](/index.php/LVM "LVM")). LVM poskytuje snímky súborového systému na úrovni jadra systémom copy-on-write a, na rozdiel od plnohodnotnej zálohy, šetrí voľným miestom obzvlášť za predpokladu, že zálohované súbory niesu modifikované. Často je tak možné vytvoriť snímok systému s kapacitou napríklad 35 gigabajtov iba s 2GB voľného miesta, vzhľadom k faktu, že pacman -Sy pravdepodobne nemodifikuje viac nez 2 gigabajty. Ak je systém po downgrade v nežiaducom stave, je možné sa pohodlne vrátiť k niektorému zo starších snímkov systému.

## Pozri ja

*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [LVM](/index.php/LVM "LVM") - Ako vytvoriť snímok a ako sa vrátiť do stavu v histórii.