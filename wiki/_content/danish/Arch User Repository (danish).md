Related articles

*   [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [AUR Q & A](/index.php/AUR_Q_%26_A "AUR Q & A")
*   [Aurbuild](/index.php/Aurbuild "Aurbuild")
*   [Pacman (Dansk)](/index.php/Pacman_(Dansk) "Pacman (Dansk)")
*   [Main page (Dansk)](/index.php/Main_page_(Dansk) "Main page (Dansk)")

[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) er en fællesskabsdrevet softwarekilde til Arch Linux' brugere. Denne artikel viser den alm. bruger, hvordan man tilgår kilden, og hvordan man arbejder med den.

## Contents

*   [1 Brugeren og AUR](#Brugeren_og_AUR)
    *   [1.1 Dele 'PKGBUILDs' i 'UNSUPPORTED'](#Dele_.27PKGBUILDs.27_i_.27UNSUPPORTED.27)
    *   [1.2 [community]](#.5Bcommunity.5D)
    *   [1.3 Afstemning](#Afstemning)
*   [2 Hvordan bruges AUR](#Hvordan_bruges_AUR)
    *   [2.1 Brug af pakker fra UNSUPPORTED](#Brug_af_pakker_fra_UNSUPPORTED)
    *   [2.2 Anvendelse af fakeroot](#Anvendelse_af_fakeroot)
    *   [2.3 Sende pakker til UNSUPPORTED](#Sende_pakker_til_UNSUPPORTED)
    *   [2.4 Vedligehold af pakker i UNSUPPORTED](#Vedligehold_af_pakker_i_UNSUPPORTED)
*   [3 AUR-scripts til download og vedligehold](#AUR-scripts_til_download_og_vedligehold)
    *   [3.1 List over AUR-scripts](#List_over_AUR-scripts)

## Brugeren og AUR

Den almindelige bruger spiller en vigtig rolle i AUR. Uden støtte, involvering og deltagelse af en stor del af brugerskaren, kan AUR ikke opfylde dets formål. Levetiden for en AUR-pakke begynder og ender med brugeren, og kræver at brugeren tager del på flere områder.

### Dele 'PKGBUILDs' i 'UNSUPPORTED'

Brugere kan **dele PKGBUILDs** (scripts til at bygge pakker) ved hjælp af området UNSUPPORTED (ikke-understøttet) i AUR. UNSUPPORTED indeholder ingen binære pakker, men lader brugeren oploade pakker, som så kan downloades af andre brugere. En facilitet til kommentarer lader brugere komme med forslag og tilbagemeldinger (feedback) til bidragyderen omkring eventuelle forbedringer. Et nyt markeringssystem lader 'Trusted Users' (TUs (betroede brugere)) markere pakkerne som kontrollerede for ondsindet kode. Disse PKGBUILDs er imidlertid helt uofficielle, og er ikke blevet gennemgående testede, så de benyttes på eget ansvar.

Der er endnu ikke nogen officiel mekanisme til at downloade materiale til pakkebygning fra UNSUPPORTED, men der findes nogle få scripts her på wiki.

### [community]

Software-kilden [community] er et supplement til kilderne [extra] og [core], hvor de mest populære pakker fra UNSUPPORTED vedligeholdes af en gruppe af betroede brugere på vegne af brugerne. I modsætning til UNSUPPORTED indeholder [community] binære pakker, der kan installeres direkte med Pacman, og byggefilerne kan tilligemed tilgås med [ABS](/index.php/ABS "ABS"). Nogle af disse pakker opnår eventuelt at blive overført til software-kilderne [core] eller [extra], hvis udviklerne finder dem afgørende for distributionen.

Brugere kan tilgå AUR-software-kilden [community] ved at tilføje/afkommentere denne linje i filen /etc/pacman.conf:

```
Include = /etc/pacman.d/community

```

Hvis `/etc/pacman.d/community` ikke findes, skal den oprettes og indeholde flg.:

```
[community]
Server = ftp://ftp.archlinux.org/community/os/i686/
```

**BEMÆRK:** Udskift servernavnet med en anden server, da der har været nogle [flaskehalsproblemer](https://www.archlinux.org/news/302/).

Brugere kan også få adgang til byggefilerne i [community] ved at redigere filen `/etc/abs.conf` således:

 `REPOS=(core extra community)` 

### Afstemning

En af de nemme aktiviteter for **alle** Arch Linux-brugere er at søge i AUR og **stemme** på deres favoritpakker ved hjælp af online-brugerfladen. Alle pakker er valgbare, hvor en betroet bruger kan indlemme den i [community], og stemmetallet er en af overvejelserne i denne process - så det er i alles interesse at stemme!

## Hvordan bruges AUR

### Brug af pakker fra UNSUPPORTED

Følg disse trin, for at installere en pakke fra UNSUPPORTED:

*   Find programmet i AUR med [søgefunktionen](https://aur.archlinux.org/packages.php) (i dette eksempel anvender vi pakkenavnet 'foo') og klik på pakkenavnet i listen over søgeresultater. Dette bringer os frem til pakkens informationsside. I venstre side kan du se 2 links ved siden af hinanden:

 ` Tarball :: Files ` 

*   Klik på `Tarball` for at downloade de nødvendige byggefiler til din harddisk. Denne pakke skulle så hedde `foo.tar.gz`, hvis den ellers er korrekt indsendt.
*   Kopiér tar-arkivet `foo.tar.gz` til en byggemappe (f.eks. `/var/abs/local` eller `~/builds`) og pak den ud. Det skulle så oprette en ny mappe (`/var/abs/local/foo` eller `~/builds/foo`), der indeholder de filer, der er nødvendige for at bygge pakken.
*   **VIGTIGT**: Skift til den nyoprettede mappe, hvor du omhyggeligt tjekker PKGBUILD og enhver .install-fil for ondsindede kommandoer - hvis du er det mindste i tvivl, så byg **IKKE** pakken, men søg råd og vejledning i fora og på mailing-lister.
*   Det foreslås, at du benytter `fakeroot`, når du bygger pakker (se nedenfor). Når du så har tjekket integriteten i filerne, kan du ganske enkelt køre kommandoen `makepkg` som almindelig bruger indeni byggemappen. Kildefilen downloades, verificeres og bygges som normalt.
*   Kommandoen 'makepkg' opretter så et tar-arkiv ved navn foo.pkg.tar.gz, der kan installeres med Pacman:

```
 `pacman -U foo.pkg.tar.gz`

```

**Bemærk**: Det ovenfor beskrevne er en kort gennemgang af pakkebygningsprocessen. Et kig på siden [ABS](/index.php/ABS "ABS") giver dig alle detaljer, og anbefales på det kraftigste - specielt for førstegangs-pakkere.

### Anvendelse af `fakeroot`

`fakeroot` giver simpelthen en almindelig bruger de rettigheder, der er nødvendige for at bygge pakker i byggemiljøet, **uden** at kunne foretage ændringer på det bredere system. I det tilfælde, at byggeprocessen forsøger at ændre filer udenfor byggemiljøet, genereres en fejl, og pakkebygningen mislykkes. Dette er ganske nyttigt for at tjekke kvalitet, sikkerhed og integritet i PKGBUILDs til distribution. Som standard er `export USE_FAKEROOT="y"` inkluderet i filen `/etc/makepkg.conf`, så medmindre du har slået det fra, er det allerede aktiveret.

### Sende pakker til UNSUPPORTED

Efter at have logget ind på AUR web-brugerfladen, kan en bruger [indsende](https://aur.archlinux.org/pkgsubmit.php) et g-zippet tar-arkiv (tar.gz) af en mappe, der indeholder byggefilerne til en pakke. Mappen inde i tar-arkivet skal indeholde en PKGBUILD, alle .install-filer, rettelser osv. (ABSOLUT ingen binære filer). Eksempler på, hvordan sådan en mappe skal se ud, kan findes i /var/abs.

Bemærk at dette er et g-zippet tar-arkiv, hvor vi som eksempel forestiller os, at du vil oploade en fil ved navn 'libfoo'. For at oprette filen, skulle det gerne se nogenlunde sådan ud (bemærk tar-valgmuligheden -zcvvf):

```
   $ ls -a libfoo
   . .. PKGBUILD libfoo.install
   $ tar -zcvvf libfoo.tar.gz libfoo
   a libfoo
   a libfoo/PKGBUILD
   a libfoo/libfoo.install

```

Når du vil sende en pakke ind, skal du være opmærksom på de følgende regler:

*   Søg først efter pakken på [extra], [core], UNSUPPORTED og [community]. Hvis pakken på en eller anden måde allerede findes i en af disse software-kilder, send den IKKE ind. Hvis den eksisterende pakke har fejl, eller den mangler en eller anden funktion, så send en fejlrapport [her](https://bugs.archlinux.org/)).
*   Kontrollér omhyggeligt, at det du oploader, er korrekt. Alle bidragydere skal læse og fastholde [Arch Linux' pakkestandarder](/index.php/Arch_packaging_standards "Arch packaging standards"), når de skriver PKGBUILDs. Dette er yderst vigtigt for den jævne kørsel og den generelle succes i AUR. Husk på, at du får ingen ros eller vinder respekt hos dine ligemænd, ved at spilde deres tid med en dårlig PKGBUILD.
*   Pakker, der indeholder binære filer eller er dårligt skrevet, kan slettes uden varsel.
*   Hvis du på nogen måde er usikker omkring pakken (eller bygge-/indsendelses-processen), kan du sende din PKGBUILD til 'AUR Mailing List' eller AUR'tråden på forum til et offentligt eftersyn, før du føjer den til AUR.
*   Vær sikker på at pakken er nyttig. Er der brug for pakken? Er den ekstremt specialiseret? Hvis mere en blot nogle få mennesker kan finde pakken brugbar, er den egnet til indsendelse.
*   Få lidt erfaring, før du sender pakker ind. Byg et par pakker for at lære processen, og så kan du sende ind.
*   Hvis du indsender en package.tar.gz med en fil ved navn 'package' i den, vil du få en fejl: 'Could not change to directory /home/aur/unsupported/package/package'. Du kan ændre navnet 'package' til noget andet - f.eks. 'package.rc' - for at løse dette problem. Når pakken installeres i pakkemappen ændre pakkens navn tilbage til 'package'.

### Vedligehold af pakker i UNSUPPORTED

*   Tjek for tilbagemeldinger og kommentarer fra andre brugere. Prøv ligeledes at indlemme enhver forbedring, de foreslår - tag det som en læreproces!
*   Vær venlig IKKE blot at indsende pakker, for så blot at glemme alt om dem! Det er brugerens arbejde at vedligeholde pakken ved at tjekke for opdateringer og at forbedre PKGBUILDs, så længe de findes i UNSUPPORTED.
*   Hvis du - af en eller anden årsag - ikke kan/vil vedligeholde pakken, skal du framelde dig på AUR web-brugerfladen og/eller sende en meddelelse til AUR Mailing List.

## AUR-scripts til download og vedligehold

### List over AUR-scripts

1.  aur-sync (Perl) - for at downloade alle AUR tar-arkiver
2.  aur-install (bash)
3.  aurup (bash) - for at oploade pakker til AUR
4.  aurscripts (bash):
    1.  aurcreate - opret rene pakker for opload til AUR
    2.  aurdownload - download og udpak pakker fra AUR
    3.  aurupdate - opdatér pakkeversion (hvis specificeret) og md5-summe
5.  autoaur (bash, afhængig af 'aurscripts', opdaterer automatisk alle dine pakker installerede fra AUR)
6.  [yaourt](http://archlinux.fr/yaourt-en) (bash, en 'indpakning' til 'srcpac' med AUR-understøttelse og mere)
7.  [aurbuild](/index.php/Aurbuild "Aurbuild") (Python, *stoppet*)
8.  qpkg (Python, virker også med ikke-AUR programmer, *stoppet*)
9.  autarchy (bash) - til at oprette et tar-arkiv med alle filer krævet af PKGBUILD (bedre end 'aurcreate')

Alle disse scripts kan findes i UNSUPPORTED.