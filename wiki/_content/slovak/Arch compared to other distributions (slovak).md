Táto stránka zhrňuje niektoré podobnosti a rozdiely medzi Archom a ostatnými distribúciami. Táto otázka sa opakovane objavuje a bolo by pekné mať štandardné reakcie. Prosím, majte na pamäti: najlepším spôsobom ako porovnať Arch s ostatnými distribúciami je, že si ho nainštalujete a vyskúšate sami. Arch má vynikajúcu používateľskú komunitu, ktorá vždy rada ochotne pomôže novým používateľom. Účelom zhrnutí uvedených nižšie je iba dať vám dostatok informácií, aby ste sa rozhodli, či je Arch naozaj pre vás.

## Contents

*   [1 Arch vs Gentoo](#Arch_vs_Gentoo)
*   [2 Arch vs Slackware](#Arch_vs_Slackware)
*   [3 Arch vs Debian](#Arch_vs_Debian)
*   [4 Arch vs Ubuntu](#Arch_vs_Ubuntu)
*   [5 Arch vs Crux](#Arch_vs_Crux)
*   [6 Arch vs Grafické distribúcie](#Arch_vs_Grafick.C3.A9_distrib.C3.BAcie)
*   [7 Arch vs Distribúcie založené na RPM](#Arch_vs_Distrib.C3.BAcie_zalo.C5.BEen.C3.A9_na_RPM)
*   [8 Arch vs Fedora](#Arch_vs_Fedora)
*   [9 Arch vs Mandrake](#Arch_vs_Mandrake)
*   [10 Arch vs SuSE](#Arch_vs_SuSE)
*   [11 Arch vs Frugalware](#Arch_vs_Frugalware)

## Arch vs Gentoo

Keďže Arch distribuuje binárky, je omnoho menej náročný na čas než Gentoo. Gentoo má viac balíčkov. Arch umožňuje aj binárnu aj zdrojovo založenú distribúciu. Je ľahšie vytvoriť PKGBUILD než ebuild. Gentoo je prenosnejší hneď od výroby, keďže balíčky sa budú kompilovať k vašej konkrétnej architektúre, zatiaľčo Arch je iba i686 (aj keď používateľmi založené vedľajšie projekty i586 a x64 sú vo vývoji). Nie je žiadny dokumentovaný dôkaz, že Gentoo je nejako rýchlejší než Arch.

## Arch vs Slackware

Slackware a Arch sú oba 'jednoduché' distribúcie. Obidva používajú init skripty v štýle BSD. Arch dodáva omnoho mohutnejší systém spravovania balíčkov 'pacman', ktorý na rozdiel od štandardných nástrojov Slackwareu, umožňuje jednoduché automatické upgrady systému. Slackware sa považuje za konzervatívnejší vo svojich cykloch vydávania, uprednostňujúc osvedčené stabilné balíčky. Arch je v tomto smere omnoho viac progresívnejší. Arch je len i686, kdežto Slackware môže bežať aj na systémoch i486\. Arch je veľmi dobrý systém pre používateľov Slacku ktorí chcú mohutnejšie spravovanie balíčkov alebo novšie balíčky.

## Arch vs Debian

Arch je jednoduchší než Debian. Arch má menej balíčkov. Arch poskutuje lepšiu podporu pre budovanie vašich vlastných balíčkov než akú poskytuje Debian. Arch je zhovievavejší čo sa týka 'non-free' balíčka ako je definované v GNU. Arch je optimalizovaný pre i686 a preto rýchlejší než Debian. Balíčky Archu sú novšie než balíčky Debianu (Arch current je často aktuálnejší než Debian unstable!)

## Arch vs Ubuntu

Arch má jednoduchší základ než Ubuntu. Ak chcete kompilovať svoje vlastné jadrá, vyskúšajte najnovšie projekty CVS, alebo sem-tam vybudujte program zo zdroja, Arch je vhodnejší. Ak však chcete rýchlo nainštalovať a hneď používať a nechcete sa pohrávať s črevami systému, tak je pre vás vhodnejší Ubuntu. Vo všeobecnosti, vývojárom a kutilom sa bude pravdepodobne viac páčiť Arch než Ubuntu.

## Arch vs Crux

Arch Linux pochádza z Crux-u. Judd raz zhrnul ich rozdiely takto:

	"Používal som Crux predtým, než som začal s Archom. Arch začal v podstate ako Crux. Potom som napísal pacmana a makepkg, aby som nahradil svoje bash pseudo balíčkové skripty (vybudoval som Arch na začiatok ako LFS systém). Takže tieto sú dve úplne odlišné samostatné distribúcie, ale technicky sú takmer rovnaké. Máme napríklad (oficiálne) podporu závislostí, hoci Crux má komunitu, ktorá poskytuje iné aspekty. Prt-get z dielňe CLC bude robiť elementárnu závislostnú logiku. Crux tiež ignoruje mnoho problémov ktoré máme, keďže je to veľmi minimalisticá sada balíčkov, v podstate čo používa Per a nič viac."

## Arch vs Grafické distribúcie

Grafické distribúcie majú mnoho podobností, a Arch je od každej z nich veľmi odlišný. Arch je textovo založený a orientovaný na príkazový riadok. Arch je lepšia distribúcia ak sa chcete skutočne naučiť Linux. Graficky založené distribúcie sa zvyknú vydávať s grafickými (GUI) inštalátormi (napr. Anaconda vo Fedore) a s GUI nástrojmi na konfiguráciu systému (napr. Yast v SuSe). Konkrétne rozdiely medzi distribúciami sú popísané nižšie.

## Arch vs Distribúcie založené na RPM

Balíčky RPM sú dostupné z mnoho, mnoho miest, avšak balíčky tretej strany majú často problémy so závislosťami, ako napríklad vyžadovanie staršej verzie nejakej knižnice. Taktiež je zmätok medzi RPM balíčkami pre Red Hat a RPM balíčkami pre Mandrake. (Tieto problémy som mal ako nováčik Linuxu s Mandrake 8.2, a možno už neodrážajú súčasný stav.) Pacman dokáže oveľa viac a je spoľahlivejší než RPM.

## Arch vs Fedora

Fedora je vedľajším produktom distribúcie RedHat a už dlhší čas je sústavne jedna z najpopulárnejších distribúcií až dodnes. Z tohto dôvodu existuje početná komunita, množstvo pred-vyrobených balíčkov a podpora. Tak ako všetky distribúcie založené na RPM, spravovanie balíčkov je problém. Fedora dodala Yum ako front-end na spravovanie a získavanie RPM balíčkov a stanovenie ich závislostí. Tomuto systému chýba solídna integrácia yum-u a veľké časti Fedori stále používajú zastaralý a chybný systém up2date/anaconda/rpm. Fedora však inovuje a nedávno si vyslúžila pochvalu za integráciu SELinux a GCJ kompilovaných balíčkov, aby odstránila potrebu pre JRE od Sun-u. Fedora, ako je už notoricky známe, sa nesnaží podporovať mediálny formát mp3 kvôli patentovým otázkam.

## Arch vs Mandrake

Mandrake, hoci je slávny vďaka svojmu inštalátorovi, je veľmi ruky-zväzujúca distribúcia, ktorá po nejakom čase môže byť otravná. Ďalším problémom je to, že je to distribúcia založená na RPM, ako bolo popísané vyššie. Arch umožňuje viac slobody a menej zväzovania rúk. S ním sa skutočne učíte.

## Arch vs SuSE

Suse sa točí okolo svojho konfiguračného nástroja Yast, ktorý sa považuje za dobrý. Tento je pre konfiguračné požiadavky väčšiny používateľov obchod na jedno zastavenie. Arch neponúka takýto nástroj, keďže je to proti [The Arch Way](/index.php/The_Arch_Way "The Arch Way"). Suse sa preto považuje za vhodnejšie pre menej skúsených používateľov, alebo pre tých, ktorí chcú jednoduchší život s očakávanou funkčnosťou hneď od výroby. Suse neponúka podporu mp3 hneď po inštalácii. Avšak môže sa ľahko pridať neskôr cez Yast.

## Arch vs Frugalware

Arch je textovo založený a orientovaný na príkazový riadok. (Používateľ sa chce niečo naučiť.) Frugalware je akoby Arch ktorý sa chce stať podobný SuSe/Mandrive ? (Používateľ chce používať pracovnú plochu resp. pre menej skúsených používateľov.) Oba používajú pacman. Sú balíčky kompatibilné ?