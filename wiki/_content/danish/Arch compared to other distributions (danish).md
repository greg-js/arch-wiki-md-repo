Related articles

*   [Arch Linux (Dansk)](/index.php/Arch_Linux_(Dansk) "Arch Linux (Dansk)")
*   [The Arch Way (Dansk)](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)")

Denne side forsøger at drage sammenligninger mellem Arch Linux og andre populære GNU/Linux-distributioner og <tt>UNIX</tt>-lignende operativsystemer. De følgende opsummeringer er korte beskrivelser som kan hjælpe med at beslutte om Arch Linux vil dække dine behov. Selvom gennemgange og beskrivelser kan være nyttige, er førstehåndsoplevelser uanfægteligt den bedste måde til at sammenligne distributioner.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Kildebaserede](#Kildebaserede)
    *   [1.1 Gentoo Linux](#Gentoo_Linux)
    *   [1.2 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer/Lunar-Linux/Source_Mage)
*   [2 Minimalistiske](#Minimalistiske)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 Generelle](#Generelle)
    *   [3.1 Debian GNU/Linux](#Debian_GNU/Linux)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Frugalware](#Frugalware)
*   [4 Begyndervenlige](#Begyndervenlige)
    *   [4.1 Ubuntu](#Ubuntu)
    *   [4.2 Mandriva](#Mandriva)
    *   [4.3 openSUSE](#openSUSE)
    *   [4.4 PCLinuxOS](#PCLinuxOS)
*   [5 *BSD'erne](#*BSD'erne)
    *   [5.1 FreeBSD](#FreeBSD)
    *   [5.2 NetBSD](#NetBSD)
    *   [5.3 OpenBSD](#OpenBSD)
*   [6 Eksterne links](#Eksterne_links)

## Kildebaserede

Kildebaserede distributioner er meget portable, giver en fordel ved at kontrollere og kompilere hele operativsystemet og alle programmer til én speciel maskine og brugsmønster, med ulempen at det tager meget tid at kompilere kildekode. Archs grundsystem og alle pakker er kompileret til i686 og x86_64 arkitekturerne, og giver en potentielt hastighedsforøgelse over i386/i486/i586 binære distributioner, med en yderligere fordel ved hurtige installationer.

### Gentoo Linux

Både Arch Linux og Gentoo Linux er udgivet rullende, hvor pakker bliver tilgængelige i distributionen kort tid efter de er udgivet af udvikleren. Gentoo's pakker og grundsystem bygges direkte fra kildekoden ifølge brugerangivne 'USE flags'. Arch giver et *ports*-lignende system til at bygge pakker fra kildekode, selvom Arch's grundsystem er designet til at installeres som forudbygget binær i686/x86_64\. Dette gør generelt Arch hurtigere at bygge og opdatere, og tillader Gentoo at være mere systematisk tilpasningsvenligt. Arch understøtter i686 og x86_64 hvor Gentoo officielt understøtter x86, ppc, sparc, alpha, amd64, arm, mips, s390, sh og itanium arkitekturer. Fordi både Gentoo og Arch installationer kun inkluderer et grundsystem, er begge anset for at være meget tilpasningsvenlige. Gentoo-brugere vil generelt føle sig til rette med de fleste aspekter af Arch.

### Sorcerer/Lunar-Linux/Source Mage

Sorcerer/Lunar-Linux/Source Mage (SLS) er alle kildebaserede distributioner som oprindeligt var beslægtet med hinanden. SLS distributioner benytter et enkelt sæt af scriptfiler til at lave pakkebeskrivelser, og bruger en global konfigurationsfil til at konfigurere kompilationsprocessen, i stil med [Arch's byggesystem](/index.php/Arch_Build_System_(Dansk) "Arch Build System (Dansk)"). Værktøjerne i SLS tjekker alle afhængigheder, inklusiv behandling af valgfri funktionalitet, pakkehåndtering, fjernelse og opgradering. Der er ingen binære pakker til nogle af SLS familien, selvom de alle giver mulighed for let at rulle tilbage til en tidligere installeret pakke.

Installationsprocessen involverer at konfigurere et enkelt grundsystem fra kommadoprompten med ncurses-menuer, derefter valgfrit genkompilere grundsystemet. I lighed med Arch er der ingen standard WM/DE/DM, og Xorg er ikke inkluderet i grundinstallationen. Flere X-server alternativer er tilgængelige (X.Org 6.8 eller 7, XFree86.)

SLS har en meget kompliceret historie. Måske kan den bedste beskrivelse findes her (engelsk): [SourceMage's wiki](http://wiki.sourcemage.org/SourceMage/History).

## Minimalistiske

De minimalistiske distributioner er rimelig sammenlignende med Arch, med flere ligheder. Alle er anset for 'enkle' fra et teknisk standpunkt.

### LFS

LFS (Linux From Scratch) eksisterer kun som dokumentation. Bogen instruerer brugeren i hvorledes man kan erhverve sig det minimale pakkesæt til et funktionelt GNU/Linux-system, og hvordan man manuelt kan kompilere, patche og konfigurere det fra bunden. LFS er så minimalt som det bliver, og giver en glimrende og lærerig proces ved at bygge og tilpasse et grundsystem. Arch tilbyder de selvsamme pakker, plus et BSD-lignende *init*, et par ekstra værktøjer og den kraftfulde [pacman](/index.php/Pacman_(Dansk) "Pacman (Dansk)") pakkehåndtering som grundsystem allerede kompileret til i686 og x86_64\. LFS tilbyder ingen online softwarekilder; kildekode skal manuelt hentes, kompileret og installeret med **make**. (Flere manuelle metoder til pakkehåndtering eksisterer, og flere er nævnt i LFS Hints.) Sammen med det minimale Arch grundsystem, vedligeholder Arch-fællesskabet og udviklere tusindvis af binære pakker som kan installeres via packam såvel som [PKGBUILD](/index.php/PKGBUILD_(Dansk) "PKGBUILD (Dansk)") scripts til at bruge sammen med [Arch's byggesystem](/index.php/Arch_Build_System_(Dansk) "Arch Build System (Dansk)"). Arch inkluderer også værktøjet [makepkg](/index.php?title=Makepkg_(Dansk)&action=edit&redlink=1 "Makepkg (Dansk) (page does not exist)") til hurtigt at bygge eller tilrette `.pkg.tar.xz` pakker, klar til installation af pacman. Judd Vinet byggede Arch fra bunden, og skrev derefter pacman i C. Historisk blev Arch sommetider ganske enkelt morsomt beskrevet som "Linux med en god pakkehåndtering".

### CRUX

Arch er uafhængigt udviklet, blev bygget fra grunden og er ikke baseret på nogen anden GNU/Linux-distribution. Før han lavede Arch, beundrede og brugte Judd Vinet CRUX - en minimalistisk distribution skabt af Per Lidén. Oprindeligt inspireret af idéer fælles med CRUX, blev Arch bygget op fra grunden, og pacman blev skrevet i C. De to deler nogle gennemgående principper: f.eks. er begge arkitekturoptimerede, minimalistiske og K.I.S.S.-orienterede. Begge kommer med et *ports*-lignende system, benytter *BSD-agtige opstartsfiler og i lighed med *BSD giver begge et minimalt grundmiljø til at bygge op. Arch har pacman, som håndterer binære pakker i systemet og arbejder let sammen med [Arch's byggesystem](/index.php/Arch_Build_System_(Dansk) "Arch Build System (Dansk)"). CRUX bruger et fællesskabsbidraget system kaldet prt-get, som, i kombination med dets eget ports-system, håndterer afhængighedesløsning, men bygger alle pakker fra kildekode (selvom CRUX' grundsystem er i686 binær.) Arch understøtter officielt x86_64 og i686, hvorimod CRUX kun er til i686.

Arch benytter et rullende udgivelsessystem og har et stort udvalg af binære pakker i softwarekilderne udover [Arch's brugerkilder](/index.php/Arch_User_Repository_(Dansk) "Arch User Repository (Dansk)"). CRUX giver et mere slankt officielt understøttet ports-system udover en mindre fællesskabsdrevet softwarekilde.

### Slackware

*   Slackware og Arch er ret ens, idet begge er enkle distributioner med fokus på elegance og minimalisme.

*   Slackware er berømt for dens mangel på *branding* og rene pakker uden modificering, lige fra kernen. Arch retter typisk kun pakker for at undgå alvorlige brug eller for at sikre at pakkerne vil kompilere ordentligt.

*   Slackware benytter *BSD-agtige opstartsfiler, Arch benytter [systemd](/index.php/Systemd "Systemd").

*   Arch leverer et pakkehåndteringssystem med [pacman](/index.php/Pacman_(Dansk) "Pacman (Dansk)") som til forskel fra Slackware's standardværktøjer, giver automatisk afhængighedsløsning og tillader mere automatiserede systemopgraderinger. Slackwarebrugere foretrækker typisk deres metode med manuel afhængighedsløsning, og citerer det niveau af kontrol det giver dem, udover Slackware's glimrende lager af præinstallerede softwarebiblioteker og afhængigheder.

*   Arch er en rullende udgivelse, mens Slackware har en mere konservativ udgivelsescyklus, hvor der foretrækkes brugte stabile pakker. Arch er mere 'dugfrisk' i denne sammenhæng.

*   Arch Linux tilbyder tusinder af binære pakker indenfor dets officielle softwarekilder, hvor Slackware's softwarekilder er mere sparsomme.

*   Arch tilbyder [Arch's byggesystem](/index.php/Arch_Build_System_(Dansk) "Arch Build System (Dansk)"), et ægte *ports*-lignende system og også [Arch's brugerkilder](/index.php/Arch_User_Repository_(Dansk) "Arch User Repository (Dansk)"), en meget stor samling af PKGBUILDs bidraget af brugere. Slackware tilbyder et lignende, men mindre system på [slackbuilds.org](http://www.slackbuilds.org) som er et semiofficiel kilde med *Slackbuilds*, som er lignende Arch's PKGBUILDs. Slackwarebrugere vil generelt føle sig til rette ved de fleste aspekter af Arch Linux.

## Generelle

Disse distributioner har en lang række fordele og styrker, og kan tjene de fleste opgaver til et operativsystem.

### Debian GNU/Linux

*   Debian er et meget større projekt og fællesskab og har både stabile, test, og ustabile grene, med mere end 30.000 binære pakker. Arch 'deler' ikke pakkerne op i "-dev" og "-common" som Debian gør, og derfor vil Arch's softwarekilder synes mindre.

*   Debian har en mere stædig tilgang til fri software. Arch er mildere når det kommer til 'ikke-frie' pakker som defineret af GNU. Debians designtilgang fokuserer mere på stabilitet og streng testning. Arch har større fokus på filosofien med enkelthed, minimalisme og at tilbyde dugfrisk software. Arch's pakker er nyere end Debian Stable og Testing, typisk omkring samme version som Debian Unstable.

*   Både Debian og Arch tilbyder gode pakkehåndteringssystemer.

*   Arch udgives rullende, hvorimod Debian Stable udgives med "frosne" pakker.

*   Debian er tilgængeligt til mange arkitekturer, inklusiv alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 og sparc, hvorimod Arch kun er til i686 og x86_64, med udgaver til Arm (f.eks. til Rasperry Pi) lavet af fællesskabet.

*   Arch giver en mere ligefrem understøttelse til at bygge tilrettede, installerbare pakker fra udefrakommende kilder, med et *ports*-lignende pakkebygningssystem. Debian tilbyder intet *ports*-system, men hviler i stedet på dets kæmpe lagre af binære softwarepakker.

*   Installationen af Arch tilbyder kun en minimal grundinstallation, med en transparent systemkonfiguration, hvorimod Debians metode tilbyder en mere automatisk konfigurationstilgang sammen med flere alternative metoder til installationen.

*   Debian bruger SysVinit som standard, selvom både systemd og upstart er tilgængelige til installation for brugerne, hvorimod Arch benytter [systemd](/index.php/Systemd "Systemd") som standard for bedre ydelse generelt.

*   Arch holder rettelser til et minimum, deraf undgås problemer som udvikleren ikke kan gennemgå.

### Fedora

*   Fedora er udgivet af fællesskabet, men samtidig bakket op af Red Hat; Det er ofte præsenteret som en testudgave med det nyeste nye; Fedoras pakker og projekter migrerer til RHEL og nogle bliver engang adopteret af andre distributioner. Arch bliver også vurderet som relativt nyt, selvom det er rullende udgivet og ikke er testgrenen af en anden distribution.

*   Fedora har et stort fællesskab, mange forudbyggede pakker og glimrende understøttelse. Fedoras pakker er af typen RPM, og bruger pakkehåndteringen YUM, og et officielt grafisk pakkeværktøj (PackageKit) er også tilgængeligt. Arch bruger [pacman](/index.php/Pacman_(Dansk) "Pacman (Dansk)") til at håndtere enkle komprimerede pakker.

*   Fedora nægter at inkludere understøttelse af MP3 og andet media pga. dedikation til kun at inkludere fri software, selvom tredjeparts pakkekilder er tilgængelige for sådanne pakker. Arch er mere overbærende i forhold til holdningen til MP3 og andet media.

*   Fedora tilbyder flere installationsmuligheder, inklusiv en grafisk installation såvel som en minimal mulighed. Fedora "spins" giver valg af forskellige skrivebordsmiljøer, hver især med en vifte af standardpakker. Arch, på den anden side, leverer blot en række scripts til at lette processen i at installere et minimalt basissystem.

*   Fedora har en planlagt udgivelsescyklus, men understøtter officielt opdatering til nye udgivelser via deres FedUp værktøj. Arch er rullende udgivet.

*   Arch-projektet er rettet mod letvægtselegance hvor Fedora fokuserer mere på fællesskabsudvikling og systemisk innovation. Både Arch's og Fedoras fællesskaber er stærkt opmuntrede til at bidrage til projektudvikling.

*   Fedora har fortjent meget erkendelse fra fællesskabet for integration af SELinux, GCJ kompilerede pakker (for at fjerne behovet for Sun's JRE), og produktive bidrag til softwareudviklere; Red Hats, og derfor også Fedoras udviklere, bidrager den største del til Linux kernen i forhold til noget andet projekt.

*   Arch Linux leverer hvad der er bredt anset for at være den mest dybdegående og omfattende distributionswiki. Fedora's wiki er brugt i den originale forstand af ordet "wiki," eller en måde at udveksle information hurtigt mellem udviklere, testere og brugere. Den er ikke tiltænkt at blive benyttet som en vidensbase ligesom Arch's. Fedoras wiki ligner en fejldatabase eller en firmawiki.

### Frugalware

*   Arch er tekstbaseret og kommandolinjeorienteret.

*   Frugalware understøtter ikke JFS-filsystemet som standard.

*   Både Arch og Frugalware er fremhævet som optimerede til i686.

*   Arch er et fundamentalt anderledes system, som installeres som et minimalt grundsystem og udvides med pacman efter brugerens valg og behov. Frugalware installeres fra DVD, med standard software og skrivebordsmiljø forudvalgt for brugeren.

*   Frugalware har en planlagt udgivelsescyklus. Igen, Arch er mere fokuseret på enkelthed, minimalisme, kode-korrekthed og at have de nyeste pakker med en rullende udgivelsesmodel.

## Begyndervenlige

De begyndervenlige distributioner har en del til fælles, men Arch er temmelig forskellig til sammenligning. Arch kan være et bedre valg hvis du ønsker at lære om GNU/Linux ved at bygge op fra en minimal installation, da Arch's grundsystem indeholde meget få pakker i forhold til de begyndervenlige distributioner. Enkelte forskelle mellem distributionerne er beskrevet nedenfor.

### Ubuntu

*   Ubuntu er en yderst populær Debian-baseret distribution kommercielt sponsoreret af Canonical Ltd., mens Arch er et uafhængigt udviklet bygget fra bunden.

*   Begge projekter har meget forskellige mål, og er rettet mod forskellige brugergrupper. Arch er designet til brugere som ønsker en gør-det-selv tilgang, hvor Ubuntu giver et autokonfigureret system som mere skal være en distribution til "alle". Hvis du ønsker at komme op at køre hurtigt, og ikke rode meget runt med indmaden i systemet, er Ubuntu bedre egnet. Arch præsenteres som et meget mere minimalistisk design fra grundinstallationen og fremefter, og afhænger meget af at brugeren tilpasser det til sine specielle behov. Generelt vil udviklere og folk som kan lide at pille ved småting kunne lide Arch bedre end Ubuntu, selvom mange Arch-brugere begyndte med at bruge Ubuntu for senere at migrere til Arch.

*   Nuværende Ubuntu udvikling og markedsføring synes at fokusere stærkt på markedet for berøringsfølsomme skærme, hvorimod Arch udvikling er mere fokuseret på en brugercentrisk model som giver fællesskabet magt til at skabe tilrettede løsninger.

*   Ubuntu laver en udgivelse hver 6\. måned, hvorimod Arch udgives løbende, med et nyt *snapshot* udgivet hver måned.

*   Arch tilbyder et *ports*-lignende byggesystem, [Arch's byggesystem](/index.php/Arch_Build_System_(Dansk) "Arch Build System (Dansk)"), men Ubuntu gør ikke.

*   De to fællesskaber er derudover også forskellige på nogle punkter. Arch-fællesskabet er meget mindre og brugere opfordres stærkt til at være pro-aktive; en større procentdel bidrager til distributionen. Som kontrast er Ubuntu-fællesskabet relativt stort og kan derfor klare at en langt større del af brugerne ikke bidrager aktivt til udvikling, pakning eller vedligeholdelse af softwarekilder.

### Mandriva

Mandriva Linux (tidligere Mandrake Linux) startede i 1998 med målsætningen at gøre GNU/Linux letanvendeligt for enhver. Det er RPM-baseret og bruger pakkehåndteringen 'urpmi'. Igen, Arch tager en enklere tilgang ved at være tekstbaseret og bruge mere manuel konfiguration og er målrettet mere mod øvede og avancerede brugere.

### openSUSE

openSUSE er centreret omkring pakkeformatet RPM og dets velansete grafiske konfigurationsværktøj YaST2, som er et 1-stops værksted for de fleste brugeres konfigurationsbehov, inklusiv pakkehåndtering. Arch tilbyder ikke sådan en facilitet da det går imod [Arch-metoden](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)"). openSUSE er derfor bredt anset for at være mere hensigtsmæssig for nybegyndere, eller de som ønsker en mere et mere grafisk orienteret miljø, autokonfiguration og forventer funktionalitet ud af boksen.

### PCLinuxOS

PCLinuxOS er en populær Mandriva-baseret distribution som tilbyder et komplet skrivebordsmiljø, designet til brugervenlighed og er beskrevet som "enkelt", selvom dets definition af enkelthed er meget forskellig fra Arch-definitionen. Arch er designet som et enkelt grundsystem som kan tilrettes fra bunden og opad, og er målrettet erfarne brugere. PCLOS bruger pakkehåndteringen apt som indvikler til RPM-pakker. Arch bruger dets eget uafhængigt udviklede pakkehåndtering [pacman](/index.php/Pacman_(Dansk) "Pacman (Dansk)") med `.pkg.tar.xz` pakker. PCLOS er meget grafisk drevet, med grafiske værktøjer til konfiguration af hardware, og pakkehåndteringsforsiden Synaptic, og påstår at have lidt til ingen afhængighed af kommandolinjen. Arch er kommandolinjeorienteret og designet til mere enkelte tilgange til systemkonfiguration, administration og vedligeholdelse. PCLOS anbefaler 256 MiB RAM som minimumskrav til systemet. Værende mere letvægt, kan Arch køre på systemer med mindre hukommelse, og kræver blot 64 MiB RAM til en grundinstallation, og vil køre gnidningsfrit på moderne systemer.

## *BSD'erne

*BSD'erne deller samme oprindelse og nedstammer direkte fra arbejde gjort på UC Berkeley for at skabe et frit redistribuerbart, gratis, <tt>UNIX</tt> system. De er ikke GNU/Linux-distributioner, men rettere <tt>UNIX</tt>-lignende operativsystemer. Selvom Arch og *BSD'erne deler konceptet med et tæt integreret grundsystem og et *ports*-system, sammen med et lignende opstartsfil, er de overhovedet ikke beslægtede fra et kodesynspunkt. *BSD'erne kommer fra den oprindelige AT&T <tt>UNIX</tt> kildekode og har en ægte <tt>UNIX</tt>-arv. For at lære mere om *BSD-varianterne, besøg leverandørens side.

### FreeBSD

Både Arch og [FreeBSD](http://www.freebsd.org/about.html) tilbyder software som kan hentes som binær eller kompileres med et *ports*-system. Begge deler et ens opstartssystem. Som andre *BSD'er er FreeBSD's grundsystem udviklet fundamentalt som et komplet system, med hver applikation 'porteret' til FreeBSD og sikret at den virker i processen. Derimod eksisterer GNU/Linux-distributioner som Arch Linux som amalgamer kombineret fra mange separate kilder. Både Arch og FreeBSD bruger `/etc/rc.conf` som en central konfigurationsfil. FreeBSD's licens er generelt mere beskyttende overfor programmøren i modsætning til GPL'en som beskytter kildekoden selv. Arch er udgivet under GPL'en. I FreeBSD, i lighed med Arch, er beslutninger delegeret til dig, den øvede bruger. Dette kan være den mest interessante sammenligning til Arch siden de går hoved-mod-hoved i pakkemodernitet og har en nogenlunde stor, smart, aktiv, ingen-nonsens fællesskab. Begge systemer deler mange ligheder og FreeBSD-bruger vil generelt føle sig godt tilpas med de fleste aspekter af Arch.

### NetBSD

NetBSD er et frit, sikkert og meget portabelt <tt>UNIX</tt>-lignende *open-source* operativsystem tilgængelig til over 50 platforme, fra 64-bit Opteron-maskiner og skrivebordssystemer til håndholdte og indbyggede enheder. Dets rene design og avancerede funktioner gør det glimrende i både produktions- og udviklingsmiljøer, og det er brugerunderstøttet med komplet kildekode. Mange applikationer er let tilgængelige gennem *pkgsrc*, NetBSD's pakkesamling. Arch kan måske ikke køre på et utal af enheder som NetBSD gør, men til almindelige skrivebordscomputere kan det nok tilbyde flere programmer. Derudover er standardmetoden som *pksrc* benytter til at installere pakker, at hente kildekoden og kompilere den, hvorimod Arch tilbyder binære pakker. Arch deler nogle ligheder med NetBSD: begge bruger `/etc/rc.conf` som en primær konfigurationsfil, både kræver manuel konfiguration, de er minimalistiske og letvægt, begge tilbyder *ports*-systemer såvel som binære og begge har aktive, ingen-nonsens fællesskaber. Arch låner også fra *BSD til dets init systemkoncept.

### OpenBSD

OpenBSD projektet producerer et frit, multiplatforms 4.4BSD-baseret <tt>UNIX</tt>-lignende operativsystem. Indsatsen fokuserer på portabilitet, standardisering, kode-korrekthed, proaktiv sikkerhed og integreret kryptografi. I modsætning fokuserer Arch mere på enkelthed, elegance, minimalisme og spritnyt software. OpenBSD er selvbeskrevet som "måske nr. 1 sikkerheds OS."

I lighed med Arch tilbyder OpenBSD en lille, elegant grundinstallation og benytter et *ports*-system og pakkesystemer som tillader let installation og administration af programmer som ikke er del af grundoperativsystemet. I modsætning til et GNU/Linux system som Arch, men tilfælles med andre BSD-baserede operativsystemer, er OpenBSD's kerne og brugerprogrammer, såsom skal og almindelige værktøjer (som ls, cp, cat og ps,) udviklet sammen i en enkelt kildekodesamling.

## Eksterne links

*   [DistroWatch.com](http://distrowatch.com/)