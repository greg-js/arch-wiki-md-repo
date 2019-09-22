Udover de herunder dækkede spørgsmål finder kan du finde mange oplysninger på flg. sider:

*   [The Arch Way (Dansk)](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)") der fortæller om baggrunden og filosofien bag Arch Linux
*   [Arch Linux (Dansk)](/index.php/Arch_Linux_(Dansk) "Arch Linux (Dansk)") der i korte træk beskriver Arch Linux

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Generelt](#Generelt)
    *   [1.1 Jeg er total Linux-nybegynder. Skal jeg bruge Arch?](#Jeg_er_total_Linux-nybegynder._Skal_jeg_bruge_Arch?)
    *   [1.2 Hvornår kommer der en ny udgave?](#Hvornår_kommer_der_en_ny_udgave?)
    *   [1.3 Arch har brug for mere/mindre omtale (f.eks. reklamer)](#Arch_har_brug_for_mere/mindre_omtale_(f.eks._reklamer))
    *   [1.4 Arch har brug for mere dokumentation](#Arch_har_brug_for_mere_dokumentation)
    *   [1.5 Hvorfor er Arch så langsom? Jeg troede, at den skulle være hurtig!](#Hvorfor_er_Arch_så_langsom?_Jeg_troede,_at_den_skulle_være_hurtig!)
    *   [1.6 Hvorfor er min internetforbindelse så langsom sammenlignet med andre operativsystemer?](#Hvorfor_er_min_internetforbindelse_så_langsom_sammenlignet_med_andre_operativsystemer?)
*   [2 Pakkehåndtering](#Pakkehåndtering)
    *   [2.1 Jeg har fundet en fejl ved pakken X. Hvad skal jeg gøre?](#Jeg_har_fundet_en_fejl_ved_pakken_X._Hvad_skal_jeg_gøre?)
    *   [2.2 Kommer Arch til at have en database for Pacman?](#Kommer_Arch_til_at_have_en_database_for_Pacman?)
    *   [2.3 Pacman er langsom! Hvordan kan initierende starttid forbedres?](#Pacman_er_langsom!_Hvordan_kan_initierende_starttid_forbedres?)
    *   [2.4 Arch-pakker burde benytte et unikt navn på filendelser. -.pkg.tar.gz er alt for langt og/eller forvirrende](#Arch-pakker_burde_benytte_et_unikt_navn_på_filendelser._-.pkg.tar.gz_er_alt_for_langt_og/eller_forvirrende)
    *   [2.5 Pacman har brug for et bibliotek, så andre programmer let kan få adgang til pakkeinformation](#Pacman_har_brug_for_et_bibliotek,_så_andre_programmer_let_kan_få_adgang_til_pakkeinformation)
    *   [2.6 Hvorfor har Pacman ingen grafisk brugerflade 'frontend'?](#Hvorfor_har_Pacman_ingen_grafisk_brugerflade_'frontend'?)
    *   [2.7 Pacman har brug for funktionen X !](#Pacman_har_brug_for_funktionen_X_!)
    *   [2.8 Arch har brug for en stabil version!](#Arch_har_brug_for_en_stabil_version!)
    *   [2.9 Hvad er forskellen mellem alle disse software-kilder?](#Hvad_er_forskellen_mellem_alle_disse_software-kilder?)
    *   [2.10 Hvorfor har Arch ingen dokumentation og info-sider med i deres pakker?](#Hvorfor_har_Arch_ingen_dokumentation_og_info-sider_med_i_deres_pakker?)
    *   [2.11 Jeg har lige installeret pakken X. Hvordan starter jeg det?](#Jeg_har_lige_installeret_pakken_X._Hvordan_starter_jeg_det?)
*   [3 Installation](#Installation)
    *   [3.1 Arch har brug for et bedre eller et grafisk installationsprogram!](#Arch_har_brug_for_et_bedre_eller_et_grafisk_installationsprogram!)

# Generelt

## Jeg er total Linux-nybegynder. Skal jeg bruge Arch?

Der har været megen debat om netop dette emne. Arch er rettet mod mere erfarne Linux-brugere, men mange føler, at Arch er et godt sted at begynde. Hvis du er begynder og ønsker at bruge Arch, er du hermed advaret - du MÅ være villig til at lære. Før du stiller spørgsmål, bør du selv søge efter svar ved at 'google', søge på wikien og i forum (og læse tidligere FAQ). Hvis du gør det, skal det nok gå. Vid også, at mange mennesker gider ikke svare på de samme basale spørgsmål igen og igen, så det er det miljø, du udsætter dig selv for. Der er en årsag til, at alt dette blev oprettet/gjort tilgængeligt for dig.

## Hvornår kommer der en ny udgave?

Arch Linux udkommer ikke med specifikke intervaller. Normalt kommer der kun en ny udgave, hvis der er lavet en større ændring i installationsprogrammet, eller hvis noget er sket, der gør det vanskeligt at opdatere fra en tidligere udgave ved at køre en 'pacman -Syu'.

Nye udgivelser er ikke særligt vigtige i Arch, da den løbende opdatering gør nye udgivelser forældede, så snart en pakke er opdateret. Hvis du vil have den sidste nye udgave af Arch Linux, er det ikke nødvendigt at geninstallere. Du kører simpelthen kommandoen 'pacman -Syu', og dit system bliver identisk med det, du ville få ud af en helt ny installation.

Af den samme grund er nye udgaver af Arch Linux typisk ikke fulde af nye og spændende ting. Alt 'nyt og spændende' udgives efterhånden som pakkerne opdateres, og kan hentes øjeblikkeligt med 'pacman -Syu'.

## Arch har brug for mere/mindre omtale (f.eks. reklamer)

Arch får masser af omtale, som det er. Målet er ikke, at Arch Linux skal være stor. Målet er, at det skal være veludført. Lad det vokse naturligt. At prøve på at få det til at 'blive stort i en fart' vil kun give problemer.

Man skal dog heller ikke begrænse den naturlige vækst. Flere brugere betyder, at flere udviklere arbejder på Arch Linux. Dette kan så forårsage nogle organisatoriske spørgsmål i 'toppen', men det tager vi fat på, når den tid kommer.

## Arch har brug for mere dokumentation

Det er i grunden rigtigt, så det står dig frit for at bidrage. Dokumentation kommer ikke af ingenting. Efter at have søgt i fora og Wiki, og du ikke kan finde, det dokumentation du har brug for, så prøv at oprette det. Start en side i wikien, og lav en tråd om det i forum. Der er højst sandsynligt folk med erfaring på det område, eller i det mindste nogle, der er villige til at hjælpe. Hvis der ikke er nogen, så mist ikke modet. Når du er færdig med din dokumentation, er der sikkert andre, der opfatter det som en utrolig værdifuld ressource.

**Der er altid brug for dokumentation - bidrag til wikien**.

## Hvorfor er Arch så langsom? Jeg troede, at den skulle være hurtig!

Der er to almindelige årsager til, at dit system er langsommere, end det burde være. Først skal du sikre dig, at 'loopback' (lo i /etc/rc.conf) er aktiveret. Bagefter skal du sikre dig, at dit 'hostname' er sat korrekt i /etc/hosts (f.eks. at det matcher 'hostname' i rc.conf. Begge kan forårsage, at programmer starter meget langsomt op.

## Hvorfor er min internetforbindelse så langsom sammenlignet med andre operativsystemer?

Er dit netværk sat rigtigt op? Har du dobbelttjekket din /etc/rc.conf, /etc/hosts og /etc/resolv.conf?

# Pakkehåndtering

## Jeg har fundet en fejl ved pakken X. Hvad skal jeg gøre?

Først skal du finde ud af, om fejlen er noget, der kan rettes af Arch-holdet. Nogle gange er det ikke (det Firefox-crash kan være Mozilla-holdets skyld) - dette kaldes en 'upstream error'. Hvis det er et Arch-problem, kan du gøre følgende:

1.  Søg i forum efter information. Se om der er andre, der har bemærket fejlen.
2.  Søg på [https://bugs.archlinux.org/](https://bugs.archlinux.org/), for at se, om fejlen allerede er rapporteret
3.  Informér pakkevedligeholderen (Package Maintainer). Prøv en 'pacman -Qi <pakkenavn>" for at få denne information.
4.  Send en fejlrapport med detaljeret information til [https://bugs.archlinux.org](https://bugs.archlinux.org).
5.  Opret en tråd i forum, hvor du detaljeret beskriver fejlen, og at du har sendt en fejlrapport, Dette forhindrer at mange andre rapporterer den samme fejl.

## Kommer Arch til at have en database for Pacman?

Måske. Emnet diskuteres.
[https://bbs.archlinux.org/viewtopic.php?t=11193](https://bbs.archlinux.org/viewtopic.php?t=11193)
[https://bbs.archlinux.org/viewtopic.php?t=10898](https://bbs.archlinux.org/viewtopic.php?t=10898)
Kig også på[FS#5328.](https://bugs.archlinux.org/task/5328.)

## Pacman er langsom! Hvordan kan initierende starttid forbedres?

Se indslaget ovenfor om en database-backend for Pacman. Kun den første Pacman-kørsel efter boot burde være lidt langsom. Derefter er tingene generelt cachede. Stadig, for nogle mennesker, er den initierende starttid et problem. Der er diskussioner i gang omkring dette emne.
Hvis du har [ReiserFS](/index.php?title=ReiserFS&action=edit&redlink=1 "ReiserFS (page does not exist)"), er der nogle fragmenteringsproblemer, som unødvendigt sløver Pacman.
Siden version 2.9.6, bundler Pacman-pakken et bash-script, der hedder <tt>pacman-optimize</tt>, der burde hjælpe de, der oplever dårlige opstartstider. Se også [afsnittet om at forbedre ydelsen af Pacman](/index.php/Improve_pacman_performance "Improve pacman performance").

## Arch-pakker burde benytte et unikt navn på filendelser. -.pkg.tar.gz er alt for langt og/eller forvirrende

Dette har været diskuteret på Arch mailing-lister. nogle foreslog filendelsen -.pac. Så vidt vides, er der for tiden ingen planer om at ændre filendelsen på pakker. Som en af Arch-udviklerne - Tobias Kieslich - siger det: "En pakke **er** en 'gzippet tarball'! Og den kan åbnes, undersøges og manipuleres med ethvert tar-dueligt program. Ydermere er mime-typen automatisk korrekt genkendt af de fleste programmer."

## Pacman har brug for et bibliotek, så andre programmer let kan få adgang til pakkeinformation

Siden version 3.0.0 har Pacman været 'front-end' til Arch Linux pakkehåndtering 'libalpm'. Dette bibliotek tillader at andre 'frontends' skrives (f.eks. en grafisk brugerflade).

## Hvorfor har Pacman ingen grafisk brugerflade 'frontend'?

Har du læst [The Arch Way](/index.php/The_Arch_Way "The Arch Way") og [Arch Linux](/index.php/Arch_Linux "Arch Linux")?
Basalt set er svaret, at Arch-holdet vil ikke tilbyde det. Du kan frit anvende en af de, der er udviklet af brugere. Der er en fin liste i link-sektionen på [Getting involved](/index.php/Getting_involved "Getting involved"). Der er også et udvalg på siden over [grafiske brugerflader til Pacman](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends"). Når dette Pacman-bibliotek laves, lettes integrationen mellem Arch-pakker og 'frontends'.

## Pacman har brug for funktionen X !

Har du læst [The Arch Way](/index.php/The_Arch_Way "The Arch Way") og [Arch Linux](/index.php/Arch_Linux "Arch Linux")?
Filosofien bag Arch er, "Hold det Enkelt".
Hvis du tror, at din idé har nogle fortrin - og den ikke modstrider dette enkle krav - så hold dig endelig ikke tilbage for at diskutere det på [forum](https://bbs.archlinux.org/).

Dog er den bedste måde, at få tilføjet en egenskab til Pacman eller Arch Linux, at implementere det selv. Der er intet, der siger, at dt bliver officielt accepteret, men andre vil bedømme og teste dine anstrengelser.

## Arch har brug for en stabil version!

Man skal aldrig sige aldrig. Nogle af de mange diskussioner om emnet:
[https://bbs.archlinux.org/viewtopic.php?t=11288](https://bbs.archlinux.org/viewtopic.php?t=11288)
[https://archlinux.org/pipermail/arch/2007-November/016048.html](https://archlinux.org/pipermail/arch/2007-November/016048.html)

## Hvad er forskellen mellem alle disse software-kilder?

Se [Official repositories](/index.php/Official_repositories "Official repositories").

## Hvorfor har Arch ingen dokumentation og info-sider med i deres pakker?

Med det formål at være enkel og letvægt er disse ikke særligt brugbare dele af Linux-systemet udeladt. For eksempel ting som /usr/doc og info-siderne til fordel for man-sider. Dette har været oppe at vende mange gange - prøv at læse nogle tidligere diskussioner omkring dette:
[https://www.archlinux.org/pipermail/arch/2005-April/004194.html](https://www.archlinux.org/pipermail/arch/2005-April/004194.html)
[https://bbs.archlinux.org/viewtopic.php?id=14527](https://bbs.archlinux.org/viewtopic.php?id=14527)

## Jeg har lige installeret pakken X. Hvordan starter jeg det?

Hvis du bruger et skrivebordsmiljø som KDE eller GNOME, skulle programmet automatisk vise sig i din menu.
Hvis du forsøger at køre programmet fra en terminal - og ikke kender dets binære navn - prøv at køre en 'pacman -Ql <pakkenavn> | grep bin'.
Et almindeligt problem for pakker som Firefox og OpenOffice er, at de installeres til /opt, som ikke er i din $PATH. Du kan tage udgangspunkt i /etc/profile eller logout/login for at rette dette.

# Installation

## Arch har brug for et bedre eller et grafisk installationsprogram!

Diskussionen om et bedre installationsprogram er en subjektiv mening. Den bedste måde at komme om ved dette er, at tilpasse installationsprogrammet til [filosofien](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)") bag Arch Linux. Hvis opfattelsen af et bedre installationsprogram understøttes af mere konkrete argumenter, kan yderligere udvikling tages op til debat. Da der ikke skal installeres særligt ofte (Se afsnittet ovenfor om [rullende udgivelser](#Hvorn.C3.A5r_kommer_der_en_ny_udgave.3F)), er det ikke særligt højt prioriteret af hverken brugere eller udviklere.
Der er dog to uofficielle metoder:
[Archie Live CD](http://archie.dotsrc.org/) med XFCE (Flere er under udvikling) og [Arch_Linux_Office_Install_CD](http://user-contributions.org/wikis/userwiki/index.php?) med KDE.