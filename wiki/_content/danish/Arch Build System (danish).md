Related articles

*   [AUR_Trusted_User_Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines")
*   [AUR](/index.php/AUR "AUR")
*   [AUR Q & A](/index.php/AUR_Q_%26_A "AUR Q & A")
*   [Aurbuild](/index.php/Aurbuild "Aurbuild")

## Contents

*   [1 Hvad er ABS?](#Hvad_er_ABS?)
    *   [1.1 Hvad er et 'ports'-lignende system?](#Hvad_er_et_'ports'-lignende_system?)
    *   [1.2 **ABS** er et lignende koncept.](#ABS_er_et_lignende_koncept.)
    *   [1.3 Hurtig gennemgang](#Hurtig_gennemgang)
    *   [1.4 Er det det hele?](#Er_det_det_hele?)
    *   [1.5 ABS - Systemoversigt](#ABS_-_Systemoversigt)
*   [2 Hvorfor skulle jeg bruge ABS?](#Hvorfor_skulle_jeg_bruge_ABS?)
*   [3 Kom igang! Installér pakker](#Kom_igang!_Installér_pakker)
*   [4 /etc/abs.conf](#/etc/abs.conf)
*   [5 Opret ABS-træet](#Opret_ABS-træet)
*   [6 /etc/makepkg.conf](#/etc/makepkg.conf)
*   [7 ABS-træet](#ABS-træet)
    *   [7.1 Opret en mappe til bygning af pakker](#Opret_en_mappe_til_bygning_af_pakker)
*   [8 Byggefunktionen - traditionel metode](#Byggefunktionen_-_traditionel_metode)
*   [9 Byggefunktionen - ABS-måden](#Byggefunktionen_-_ABS-måden)
*   [10 Yderligere ABS-information](#Yderligere_ABS-information)

#### Hvad er ABS?

ABS er en forkortelse af Arch Build System - eller på dansk Archs byggesystem. Det er et 'ports'-lignende system til at bygge software fra **kilden**.
Hvor Pacman er det specialiserede værktøj i Arch Linux til at håndtere binære pakker (inklusiv pakker, der er bygget med ABS ), er ABS det specialiserede værktøj til at kompilere fra en kilde til en installérbar pkg.tar.gz-pakke.

##### Hvad er et 'ports'-lignende system?

'Ports' er et system, anvendt af FreeBSD, der lader **kilde**-pakker blive downloadet, udpakket, tilrettet, kompileret og installeret. *En 'port' er blot en lille mappe på brugerens computer med et navn, der svarer til det software der installeres. Denne mappe indeholder nogle få filer med instruktioner for download og installation af en pakke fra en kilde*, typisk ved at navigere til mappen - eller porten - og udføre kommandoerne *make* og *make install*. Systemet vil så downloade, kompilere og installere det ønskede software.

##### **ABS** er et lignende koncept.

**ABS** laves ud fra et mappetræ, (**ABS-træet**), der findes under /var/abs, som indeholder mange undermapper. Hver mappe i sin kategori og alle navngivet af deres respective byggebare pakke.
Du kan kalde enhver undermappe - med navn efter pakken - for et ABS. Det samme som man vilde kalde en 'port'. Disse **ABS**-er - eller undermapper **indeholder hverken software-pakken eller kilden**, men nærmere en **PKGBUILD**-fil (og somme tider andre filer). En PKGBUILD er en simpel tekstfil, der indeholder instruktioner til kompilering og pakning, så vel som en URL til det tar-arkiv, som skal downloades. *Den vigtigste komponent i ABS er PKGBUILD.*

##### Hurtig gennemgang

Kør kommandoen *abs* som 'root' for at oprette ABS-træet. Hvis du f.eks. vil bygge editoren Nano fra **kilden**, skal du kopiere filen /var/abs/core/base/nano til en byggemappe. Gå ind i byggemappen og kør en **makepkg**. Så enkelt er det.
'Makepkg' vil forsøge at læse og eksekvere de instruktioner, der findes i PKGBUILD-filen. Tar-arkivet fra kilden downloades, udpakkes og kompileres i henhold til de 'CFLAGS', der angives i /etc/makepkg.conf og til sidst klemmes ind i en pakke med fil-endelsen .pkg.tar.gz, som det instrueres i filen PKGBUILD.
Installation er så nemt, som at køre en *pacman -U nano.pkg.tar.gz*, eller lav pakken og installér den rent med Pacman. Alt med kun én kommando.
Fjernelse af pakken håndteres også af Pacman.

Filen PKGBUILD og andre filerkan selvfølgelig tilpasses som du ønsker, og du kan vælge at benytte 'makepkg'-funktionen i ABS til at lave egne brugertilpassede pakker fra kilder udenfor selve ABS-træet.(Se en prototype på en PKGBUILD og installationsfile under /var/abs/core/)

* * *

Med **ABS-træet** på plads har en Arch Linux-bruger, der vil kompilere fra kilde, alle tilgængelige pakker ved hånden.

##### Er det det hele?

Ikke helt endnu!

*   Du kan også benytte ABS-værktøjet **[makepkg](/index.php/Makepkg "Makepkg")** til - sammen med dine egne tilpassede PKGBUILDs - til at oprette pakker til dig selv, eller til at dele med fællesskabet. Igen er resultatet - *foo*.pkg.tar.gz-pakkerne - rent installeres med Pacman.
*   ABS-værktøjerne lader dig benytte Arch Linux-brugernes software-kilde [AUR](/index.php/AUR_Brugervejledning "AUR Brugervejledning") (**A**rch **U**ser **R**epository), der er fyldt med allerede færdige PKGBUILDs til din bekvemmelighed.

##### ABS - Systemoversigt

'ABS' kan benyttes som en 'paraply'-terminologi, da det inkluderer - og er afhængig af - flere andre komponenter. Derfor henviser 'ABS' til følgende strukur og værktøjer - selv om det ikke er helt teknisk korrekt - som et komplet værktøjssæt:

*   **ABS-træet:** Mappestrukturen i ABS under /var/abs/. Det indeholder mange undermapper, navngivet af alle tilgængelige Arch linux software-pakker - men ikke selve pakkerne.
*   **ABS:** De faktiske mapper navngivet til det byggebare software og indeholdende PKGBUILD.
*   **PKGBUILDs:** Tekstfiler der ligger under ABS-mapperne med instruktioner til bygning af pakker og kildernes URL.
*   **[AUR](/index.php/AUR "AUR"):** 'Arch Linux-brugernes software-kilde der indeholder PKGBUILDs fra brugerne til software, der måske ikke er tilgængelige som officielle Arch Linux-pakker.
*   **makepkg:** Skal-kommando der læser PKGBUILDs, kompilerer kilderne og opretter .pkg.tar.gz-arkiver.
*   **Pacman:** Pacman er helt udenfor, men bliver nødvendigvis kaldt af scriptet 'makepkg' eller manuelt, til installation eller fjernelse af de byggede pakker eller til at hente afhængigheder.

#### Hvorfor skulle jeg bruge ABS?

**A**rch **B**ygge**S**ystem (ABS) anvendes til:

*   At lave nye pakker fra kilde af software, der endnu ikke er tilgængelig. (Se [hvordan du laver pakker til Arch Linux](/index.php/Creating_packages "Creating packages"))
*   Bygge og dele disse pakker via [AUR](/index.php/AUR_Brugervejledning "AUR Brugervejledning")
*   Tilpas eksisterende pakker, så de passer til dit behov (aktivere eller deaktivere valgmuligheder)
*   Genopbyg hele dit system med dine kompileringsflag (a la FreeBSD)
*   Bygge og installere din egen tilpassede kerne. (Se [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation"))
*   Få kernemoduler til at virke med din brugertilpassede kerne.

ABS er ikke nødvendig for at bruge Arch Linux - men det er nyttigt til forskellige kompileringsopgaver.

Denne vejledning forsøger at give dig et overblik over ABS og Arch Linux-pakker. Det er ikke en komplet reference-guide!
Hvis du vil vide mere, skulle du prøve at kigge på *man*-siderne.

#### Kom igang! Installér pakker

For at benytte ABS skal du først installere **csup** og **wget**. Dette gøres med

```
pacman -S csup wget

```

#### /etc/abs.conf

Redigér /etc/abs.conf til at inkludere dine software-kilder:

```
nano /etc/abs.conf

```

Fjern udråbstegnet '!' foran de passende software-kilder som f.eks.:

```
REPOS=(core extra community !testing)

```

#### Opret ABS-træet

Som 'root' køres:

```
abs

```

Dit ABS-træ er nu oprettet under /var/abs. Bemærk de passende grene på ABS-træet nu eksisterer og svarer til dem du specificerede i /etc/abs/abs.conf.

*Kommandoen **abs** bør også benyttes til regelmæssigt at synkronisere og opdatere dit ABS-træ.*

#### /etc/makepkg.conf

Redigér filen /etc/makepkg.conf for at angive miljøvariabler og 'CFLAGS':

```
nano /etc/makepkg.conf

```

#### ABS-træet

Når du kører **abs** for første gang, synkroniseres ABS-træet med Ardh-serveren ved hjælp af 'cvs'-systemet. Hvad er så ABS-træet helt specifikt? Det findes under /var/abs, og ser såledesud:

```
|-
| -- core/
|-
|     ||-- autoconf/
|-
|     ||-- automake/
|-
|     ||-- ...
|-
| -- devel/
|-
| -- ...
|-
| -- extra/
|-
|      || -- daemons/
|-
|      ||      || -- acpid/
|-
|      ||      ||      || -- PKGBUILD
...    ...    ...    ...

```

ABS-træet har altså nøjagtigt den samme struktur som pakkedatabasen:

*   Første mappebane repræsenterer kategorier.
*   Anden mappebane repræsenterer selve ABS-erne, hvis navne svarer til de pakker du vil bygge.
*   PKGBUILD-filerne indeholder alt nødvendig information omkring pakken.
*   Endvidere kan en ABS-mappe indeholde rettelser og/eller andre filer, der er nødvendige for at bygge pakken.

*Det er vigtigt at forstå, at selve pakkens kildekode ikke findes i ABS-mappen.* I stedet for indeholder **PKGBUILD**-filen en URL fra hvilken ABS automatisk vil downloade.

##### Opret en mappe til bygning af pakker

Du skal oprette en mappe til bygning af pakker, hvor den faktiske kompilering finder sted. I denne mappe kan du gøre alt, og du bør aldrig ændre ABS-træet ved at bygge inde i det. Det er god praksis at benytte din egen hjemmemappe, selv om mange Arch Linux-brugere foretrækker at oprette en *local*-mappe under /var/abs/ ejet af normal bruger. Kopiér en ABS fra træet (var/abs/branch/category/*pakkenavn*) til byggemappen */søgesti/til/byggemappe/*.

Opret din byggemappe:

```
mkdir /home/dit-brugernavn/abs/local

```

BEMÆRK: Den første download af ABS-træet er den største. Derefter er det kun nødvendigt med mindre opdateringer, så vær ikke bange, hvis du kun har en 56k-tilslutning. Der er kun tale om tekstfiler, som er komprimerede under overførslen.

Nu hvor vi ved, hvad et ABS-træ er - hvordan kan vi så bruge det?

#### Byggefunktionen - traditionel metode

Hvis du ikke kender til at kompilere fra kilde, skal du vide, at de fleste pakker (dog ikke alle) kan bygges fra kilde på denne **traditionelle måde**:

*   Download kildens tar-arkiv fra en ekstern server med en web-browser, ftp, wget eller andre metoder.
*   Pak kildefilen ud som eks.:

```
 tar -xzf foo-0.99.tar.gz
 tar -xjf foo-0.99.tar.bz2

```

*   Gå ind i mappen:

 `cd foo-0.99` 

*   konfigurér pakken. Generelt er der et lille script ved navn `configure` i kildemappen, der benyttes til at konfigurere pakken (tilføje eller fjerne understøttelse for noget, vælge destination for installation osv.). Scriptet tjekker også, om din computer har det nødvendige software for pakken. Det kan køres med:

```
./configure <valgmulighed>

```

Du skulle først prøve valgmuligheden 'help', for bedre at forstå, hvordan det virker:

```
./configure --help

```

Hvis ikke valgmuligheden --prefix sættes i scriptet, vil de **fleste** scripts benytte /usr/local som sti til installationen, mens andre benytter /usr. For en bedre konsistens tilrådes generelt at sætte valgmuligheden --prefix=/usr/local. Det er god praksis at installere personlige programmer i /usr/local, og at have dem, der vedligeholdes af distributionen, anbragt i /usr. Dette tilsikrer, at personlige programmer kan sameksistere med dem, der håndteres af ditributionens pakkehåndtering - i Arch Linux' tilfælde er det **Pacman**.

```
./configure --prefix=/usr/local

```

*   Kompiler kilderne:

```
make

```

*   Installér

```
make install

```

*   Afinstallering udføres ved at gå ind i kildemappen og køre:

```
make uninstall

```

Dog burde du altid læse filen `INSTALL`, for at se, hvordan pakken skal bygges og installeres! **Ikke alle pakker anvender systemet `configure; make; make install`!**

*Den her beskrevne måde at kompilere kilde-tar-arkiver kan selvfølgelig stadig benyttes i Arch Linux, men ABS tilbyder et strømlinet, enkelt og elegant alternativ, som du vil se.*

#### Byggefunktionen - ABS-måden

ABS er et elegant værktøj, der yder en stærk assistance og tilpasningsmuligheder til byggeprocessen, samt opretter en pakkefil til installation. ABS-metoden involverer kopiering af en ABS fra træet til en byggemappe og køre en 'makepkg'. I vores eksempel vil vi bygge pakken *slim* display-håndtering.

*   1\. Kopiér *slim* ABS fra træet til en byggemappe:

```
cp -r /var/abs/extra/x11/slim /home/dit-brugernavn/abs/local

```

*   2\. Navigér til byggemappen:

```
cd /home/dit-brugernavn/abs/local/slim

```

*   3\. Kør kommandoen *makepkg*, der automatisk downloader tar-arkivet fra kilden, pakker ud, kompilerer og opretter filen slim.pkg.tar.gz Valgmuligheden -i kalder Pacman til automatisk at installere den resulterende pakkefil slim.pkg.tar.gz:

```
makepkg -i

```

Det var det! Du har lige bygget *slim* fra kilde og installeret det rent på dit system med Pacman. At fjerne pakken håndteres også af Pacman:

```
pacman -R slim

```

Alternativt kan du køre 'makepkg' uden valgmuligheden '-i' og installere pakken manuelt med Pacman:

```
pacman -U slim.pkg.tar.gz

```

*   *ABS-metoden tilføjer noget bekvemmelighed og automatisering, mens det stadig er fuldstændigt gennemskueligt og fastholder fuld kontrol over bygge- og installations-funktioner, ved at inkludere dem i PKGBUILDs.*

Se artiklen [Creating packages](/index.php/Creating_packages "Creating packages") (Engelsk) for en komplet oversigt over eksempler på PKGBUILDs.

#### Yderligere ABS-information

*   [Makepkg](/index.php/Makepkg "Makepkg")
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Safe Cflags](/index.php/Safe_Cflags "Safe Cflags")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")