Najprv si prečítajte [The Arch Way](/index.php/The_Arch_Way "The Arch Way") a [Arch Linux](/index.php/Arch_Linux "Arch Linux"). Všetky tri obsahujú nemalé množstvo informácií o Arch Linuxe.

## Contents

*   [1 Q) Som úplný začiatočník v Linuxe. Mal by som používať Arch?](#Q)_Som_úplný_začiatočník_v_Linuxe._Mal_by_som_používať_Arch?)
*   [2 Q) Našiel som chybu v balíčku X, čo by som mal urobiť?](#Q)_Našiel_som_chybu_v_balíčku_X,_čo_by_som_mal_urobiť?)
*   [3 Q) Bude mať Arch databázu pre pacman?](#Q)_Bude_mať_Arch_databázu_pre_pacman?)
*   [4 Q) Pacman je pomalý! Ako by sa mohli zlepšiť počiatočné časy spustenia?](#Q)_Pacman_je_pomalý!_Ako_by_sa_mohli_zlepšiť_počiatočné_časy_spustenia?)
*   [5 Q) Balíčky Archu majú dodržiavať dohodu o jedinečných názvoch, ale .pkg.tar.gz je príliš dlhé a mätúce](#Q)_Balíčky_Archu_majú_dodržiavať_dohodu_o_jedinečných_názvoch,_ale_.pkg.tar.gz_je_príliš_dlhé_a_mätúce)
*   [6 Q) Pacman potrebuje knižnicu, aby ostatné aplikácie mohli mať ľahko prístup k informáciám o balíčku](#Q)_Pacman_potrebuje_knižnicu,_aby_ostatné_aplikácie_mohli_mať_ľahko_prístup_k_informáciám_o_balíčku)
*   [7 Q) Pacman potrebuje grafické rozhranie](#Q)_Pacman_potrebuje_grafické_rozhranie)
*   [8 Q) Pacman potrebuje vlastnosť (fičúru) X!](#Q)_Pacman_potrebuje_vlastnosť_(fičúru)_X!)
*   [9 Q) Arch potrebuje lepší inštalátor. Možno grafický (GUI) inštalátor.](#Q)_Arch_potrebuje_lepší_inštalátor._Možno_grafický_(GUI)_inštalátor.)
*   [10 Q) Arch potrebuje viac tlače (t.j. reklamy)](#Q)_Arch_potrebuje_viac_tlače_(t.j._reklamy))
*   [11 Q) Arch potrebuje menej tlače](#Q)_Arch_potrebuje_menej_tlače)
*   [12 Q) Arch potrebuje viac vývojárov](#Q)_Arch_potrebuje_viac_vývojárov)
*   [13 Q) Arch potrebuje vetvu stabilných balíčkov](#Q)_Arch_potrebuje_vetvu_stabilných_balíčkov)
*   [14 Q) Arch potrebuje viac dokumentácie](#Q)_Arch_potrebuje_viac_dokumentácie)
*   [15 Q) Arch potrebuje byť priateľskejší k nováčikom](#Q)_Arch_potrebuje_byť_priateľskejší_k_nováčikom)
*   [16 Q) Nováčikovia sú otravní. Nech idú preč.](#Q)_Nováčikovia_sú_otravní._Nech_idú_preč.)
*   [17 Q) Arch potrebuje právnickú osobu (firmu) ktorá by ho kryla](#Q)_Arch_potrebuje_právnickú_osobu_(firmu)_ktorá_by_ho_kryla)

## Q) Som úplný začiatočník v Linuxe. Mal by som používať Arch?

**A)** Táto otázka bola (a stále je) dosť diskutovaná. Arch je určený pokročilejším používateľom Linuxu, ale niektorí ľudia cítia, že "Arch je dobré miesto na začatie". Ak ste začiatočník a chcete používať Arch, varujeme vás, že MUSÍTE mať vôľu učiť sa. Prv než budete klásť akékoľvek otázky, urobte vlastný nezávislý prieskum cez google, prehľadajte Wiki, a hľadajte na fóre (a čítajte minulé otázky FAQ). Ak to urobíte, mali by ste byť OK. Taktiež majte na pamäti, že mnoho ľudí nechce stále dookola odpovedať na tie isté základné otázky, takže sa vystavujete tomuto prostrediu. Existuje dôvod prečo tieto prostriedky boli vytvorené/urobené dostupnými pre vás.

## Q) Našiel som chybu v balíčku X, čo by som mal urobiť?

**A)** Najprv potrebujete zistiť, či táto chyba je niečo, čo môže tím Archu opraviť. Niekedy nie je (to že padá firefox môže byť dôsledkom chyby tímu Mozilla) - toto sa nazýva *upstream error* (protiprúdová chyba). Ak to je problém Archu, je séria krokov ktoré môžete vykonať:

1.  Hľadajte informácie na fórach. Pozrite, či si to nevšimol aj niekto iný.
2.  Oznámte to udržiavateľovi balíčka. Pre túto informáciu skúste `pacman -Qi <názov balíčka>`.
3.  Odošlite správu o chybe s detailnými informáciami na [https://bugs.archlinux.org](https://bugs.archlinux.org)
4.  Napíšte príspevok do fóra ak chcete, kde podrobne opíšete problém a skutočnosť, že ste už o tom podali správu. Toto pomôže mnohým ľuďom, aby neposielali správu o tej istej chybe.

## Q) Bude mať Arch databázu pre pacman?

**A)** Možno. O tejto otázke prebieha diskusia. [https://bbs.archlinux.org/viewtopic.php?t=11193](https://bbs.archlinux.org/viewtopic.php?t=11193) [https://bbs.archlinux.org/viewtopic.php?t=10898](https://bbs.archlinux.org/viewtopic.php?t=10898)

## Q) Pacman je pomalý! Ako by sa mohli zlepšiť počiatočné časy spustenia?

**A)** Pozri predošlú otázku ohľadne databázového pozadia (back-endu) pre pacman. Iba prvé spustenie pacmanu po nabootovaní by malo byť pomalé. Potom už sú vo všeobecnosti veci cachované. I tak však je počiatočný stav spustenia pre niektorých problémom. Tento problém sa rozoberá v diskusii. Ak ste na ReiserFS, sú tu záležitosti týkajúce sa fragmentácie, ktoré spomaľujú pacmana viac než treba. Pozrite si na pomoc toto vlákno: [https://bbs.archlinux.org/viewtopic.php?t=11840](https://bbs.archlinux.org/viewtopic.php?t=11840)

Od verzie 2.9.6, balíček pacman obsahuje bash skript s názvom `pacman-optimize` ktorý by mal pomôcť každému, kto zažíva pomalé časy spustenia.

## Q) Balíčky Archu majú dodržiavať dohodu o jedinečných názvoch, ale .pkg.tar.gz je príliš dlhé a mätúce

**A)** O tom sa diskutovalo na poštovom zozname Archu. Niektorí navrhovali príponu súboru .pac. Pokiaľ viem, momentálne nie je žiadny plán meniť príponu balíčkov. Ako to povedal jeden z vývojarov Archu, Tobias Kieslich, "Balíček **je** gzipovaný tarball! A môže byť otvorený, prezeraný a manipulovaný akoukoľvek aplikáciou schopnou tar-u. Naviac, väčšina aplikácií správne detekuje mime-typ."

## Q) Pacman potrebuje knižnicu, aby ostatné aplikácie mohli mať ľahko prístup k informáciám o balíčku

**A)** Na knižnici pre pacman sa pracuje.

## Q) Pacman potrebuje grafické rozhranie

**A)** Čítali ste [The Arch Way](/index.php/The_Arch_Way "The Arch Way") a [Arch Linux](/index.php/Arch_Linux "Arch Linux")? Odpoveď je v podstate že vývojový tím Archu ho nebude poskytovať. Kľudne môžete použiť jeden z dostupných poskytovanými používateľmi. V časti odkazy je ich pekný zoznam [Getting involved](/index.php/Getting_involved "Getting involved"). Keď už bude knižnica pre pacman hotová, bude pre rozličné grafické rozhrania omnoho ľahšie interagovať s balíčkami Archu. A mimochodom: toto nie je otázka ale oznamovacia veta. ;-)

## Q) Pacman potrebuje vlastnosť (fičúru) X!

**A)** Čítali ste [The Arch Way](/index.php/The_Arch_Way "The Arch Way") a [Arch Linux](/index.php/Arch_Linux "Arch Linux")? Filozofia Archu je "Čím Jednoduchšie". Ak si myslíte, že váš nápad je opodstatnený a neprotirečí tomuto jednoduchému mottu, tak potom o tom kľudne diskutujte na [Arch fóre](https://bbs.archlinux.org/) Taktiež asi budete chcieť sa pozrieť [sem](https://bugs.archlinux.org), je to miesto na požiadavky vlastností ak ich považujete za dôležité.

## Q) Arch potrebuje lepší inštalátor. Možno grafický (GUI) inštalátor.

**A)** Diskusia o "lepšom" inštalátorovi je subjektívny názor. Najlepším spôsobom ako sa vysporiadať s týmito otázkami je prispôsobiť insštalátor "spôsobu archu". Ak tento názor na lepší inštalátor bude podložený konkrétnejšími argumentami, možno že sa bude brať do úvahy pri ďalšom vývoji inštalátora. *Windows používa textovo založený inštalátor, FWIW*

## Q) Arch potrebuje viac tlače (t.j. reklamy)

**A)** Archu sa dostáva veľa tlače tak ako je. Cieľom Arch Linuxu nie je byť veľký. Cieľom je byť dobre urobený. Nech rast nastáva prirodzene. Snažiť sa nútiť ho rásť príliš rýchlo len spôsobí problémy.

## Q) Arch potrebuje menej tlače

**A)** Podobne k tomu čo je uvedené vyššie, nesnažte sa obmedziť prirodzený rast. Viac používateľov môže znamenať viac vývojárov čo budú pracovať na Arch Linuxe. Toto síce môže spôsobiť nejaké organizačné problémy na "vrchu", ale s nimi sa bude zaoberať keď nastanú.

## Q) Arch potrebuje viac vývojárov

**A)** Možné to je. Cíťte sa slobodný dobrovoľne obetovať váš čas! Navštívte fóra, irc kanály, poštové zoznamy, a pozrite čo je treba urobiť. Vždy je potreba dokumentácie, pozri [DocumentRequests](/index.php/DocumentRequests "DocumentRequests") či sa niečo nechystá.

## Q) Arch potrebuje vetvu stabilných balíčkov

**A)** KOMENTÁR: "Stručne, pre mňa je Arch dosť pevný ako skala."

REAKCIA: To záleží na type práce na ktorú často používame náš stroj. Napríklad, pri kancelárskej práci nechceme aby naša tlačiareň prestala fungovať alebo pri multimedálnej aby CD sa prestalo napaľovať. Alebo webovské vyvíjanie nášho ftp klienta. Momentálne som znechutený z KDE-3.4 keď som stratil všetky svoje záložky v kbear (ftp). Nová záložka sa nedá uložiť.

RIEŠENIE: Existuje **release** **repo** čo funguje ako stabilné, avšak nemá všetky balíčky. Avšak uvažuje sa o doplnení všetkých (kde, gnome, atď).
[ftp://ftp.archlinux.org/release/os/i686/](ftp://ftp.archlinux.org/release/os/i686/)

Viac si prečítajte:
[https://bbs.archlinux.org/viewtopic.php?t=11288](https://bbs.archlinux.org/viewtopic.php?t=11288)

## Q) Arch potrebuje viac dokumentácie

**A)** Dokumentácia sa neobjavuje **ex-nihilo**. Po prehľadaní fóra, a wiki, ak nemôžete nájsť potrebnú dokumentáciu, pokúste sa ju vytvoriť. Začnite stránku na wiki, a pošlite ohľadom toho príspevok na fóra. Možno ostatní ľudia majú v danej oblasti skúsenosti, alebo sú aspoň ochotní pomôcť. Ak nikto nepomôže, nebuďte sklamaný. Keď dokončíte svoju dokumentáciu, ostatní ju pravdepodobne budú považovať za extrémne hodnotný zdroj. Vždy je potreba pre dokumentáciu, pozri [DocumentRequests](/index.php/DocumentRequests "DocumentRequests") či sa niečo nechystá.

## Q) Arch potrebuje byť priateľskejší k nováčikom

**A)** Prv než začneme diskusiu o priateľskosti k nováčikom, je treba si najprv definovať čo to je "priateľskejší k nováčikom". Prosím, pozrite si otázku ohľadne lepšieho inštalátora.

## Q) Nováčikovia sú otravní. Nech idú preč.

**A)** <Filozofická diskusia> Časťou toho, že sme ľudia je akceptovať tiež iných ľudí. </Filozofická diskusia>

Najlepším spôsobom ako sa vysporiadať s nováčikmi je dopredu ich neodsudzovať. Niekto môže mať spoločný problém, dokonca aj keď si prečítali dokumentáciu; každému niečo ujde. Kričať na nich nepomôže. Použite svoje najlepšie správanie a ignorujte ľudí ktorých nemáte radi namiesto začatia boja.

Nováčikom najlepšie pomôžete ak ich budete viesť k nájdeniu správnych informácii. Obzvlášť nováčikovia prechádzajúci z Windowsu môžu mať ťažké chvíľky nájsť informácie; nie vždy sú na tom mieste kde by ich čakali. Porovnajte si to s nájdením správneho slova pri učení sa cudzieho jazyka: môžete sa opýtať učiteľa, aby vám správne preložil dané slovo, ale vždy zabudnete čo to slovo znamená. Avšak, keď si ho vyhľadáte sami v slovníku, už ho nikdy nezabudnete.

## Q) Arch potrebuje právnickú osobu (firmu) ktorá by ho kryla

**A)** <sem vložte informácie>