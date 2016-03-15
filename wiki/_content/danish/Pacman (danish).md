| **Summary**  |
| Pacman er Arch Linux' pakkehåndtering. Pakkehåndtering benyttes til at installere, opdatere og fjerne software. Denne artikel dækker grundlæggende brug og fejlsøgning. |
| **Den danske forside her på wiki** |
| [Main Page (Dansk)](/index.php/Main_Page_(Dansk) "Main Page (Dansk)") |

Programmet til pakkehåndtering - **Pacman** - er et af de store lyspunkter i Arch Linux. Det kombinerer et simpelt binært pakkeformat med et letanvendeligt pakkebygningssystem (se evt. [makepkg (Dansk)](/index.php?title=Makepkg_(Dansk)&action=edit&redlink=1 "Makepkg (Dansk) (page does not exist)") og [ABS (Dansk)](/index.php/ABS_(Dansk) "ABS (Dansk)")). **Pacman** muliggør en nem håndtering af programpakker, hvadenten de kommer fra de officielle Arch Linux softwarekilder, eller de kommer fra brugernes selvbyggede pakker.

Pacman kan holde et system opdateret ved at synkronisere dets pakkeliste med hovedserveren. Denne server-/klient-model tillader dig også at hente og installere pakker - komplet med alle afhængigheder - med en enkelt kommando.

## Contents

*   [1 Konfiguration](#Konfiguration)
*   [2 Anvendelse](#Anvendelse)
    *   [2.1 Installere og fjerne pakker](#Installere_og_fjerne_pakker)
    *   [2.2 Opgradering af systemet](#Opgradering_af_systemet)
    *   [2.3 Forespørgsler i pakkedatabasen](#Foresp.C3.B8rgsler_i_pakkedatabasen)
    *   [2.4 Anden anvendelse](#Anden_anvendelse)
*   [3 Konfiguration](#Konfiguration_2)
    *   [3.1 Generelle valgmuligheder](#Generelle_valgmuligheder)
    *   [3.2 Softwarekilder](#Softwarekilder)
    *   [3.3 Fejl](#Fejl)
*   [4 Relaterede links](#Relaterede_links)

## Konfiguration

Pacmans konfiguration er placeret i `/etc/pacman.conf`. Det er her brugeren konfigurerer programmet til at virke på den ønskede måde. Dybdegående information om konfigurationsfilen kan findes i [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html)

## Anvendelse

For virkelig at lære, hvad Pacman er i stand til, burde du læse [man pacman](https://archlinux.org/pacman/pacman.8.html). Denne artikel viser kun et lille udsnit af de operationer, der kan udføres.

### Installere og fjerne pakker

Før du installerer og opgraderer pakker er det en god idé at synkronisere den lokale database med software-kilden.

```
# pacman -Sy

```

eller

```
# pacman --sync --refresh

```

For at installere eller opgradere en enkelt eller flere pakker (inklusiv afhængigheder) bruges følgende kommando:

```
# pacman -S pakkenavn_1 pakkenavn_2

```

Hvis der er flere versioner af en pakke i forskellige softwarekilder (f.eks. 'Extra' og 'Testing'), kan du angive, hvilken der skal installeres:

```
# pacman -S extra/pakkenavn
# pacman -S testing/pakkenavn

```

For at fjerne en enkelt pakke **uden** at fjerne pakkens afhængigheder:

```
# pacman -R pakkenavn

```

For at fjerne en pakke **med** de af dens afhængingheder som ikke benyttes af en anden installeret pakke:

```
# pacman -Rs pakkenavn

```

For at fjerne en pakke **uden** at tjekke afhængigheder:

```
# pacman -Rd pakkenavn

```

### Opgradering af systemet

**Pacman** kan opdatere alle pakker i systemet med kun én kommando.
*Dette kan tage et stykke tid, afhængigt af hvor up-to-date dit system er:*

```
# pacman -Su

```

Den bedste valgmulighed er imidlertid at synkronisere databaserne **og** opdatere dit system på én gang med:

```
# pacman -Syu

```

**Note:** Da Arch er en distribution med en rullende udgivelse, er det ikke altid så ligetil at opdatere systemet som ved punktudgivne distributioner. Desforuden er pacman ikke en "skyd-og-glem" pakkehåndtering. Derfor er det ofte forvirrende for nye brugere at vedligeholde et Arch-system (som gentagne forumdiskussioner indikerer.) Læs venligst den følgende sektion *grundigt* inden du fortsætter.

Pacman er et stærkt pakkehåndteringsværktøj, men forsøger ikke at "gøre alting". Læs [Arch-metoden](/index.php/The_Arch_Way "The Arch Way") hvis dette forvirrer dig. Istedet bør brugere være agtpågivende og tage ansvar for at vedligeholde deres eget system. Når man udfører en systemopdatering (`pacman -Syu`), for eksempel, **er det yderst vigtigt at brugere læser al den information som pacman giver og bruge almindelig fornuft.**

I stedet for at opdatere så snart en opdatering er tilgængelig, bør brugere indse at en opdatering til en *nødvendig* pakke kan have uforudsete konsekvenser. Dette betyder at det ikke er klogt at opdatere `xorg-server` hvis man f.eks. skal lave en vigtig præsentation. Man bør hellere opdatere i sin fritid og være forberedt på at håndtere ethvert problem som opstår som følge af opdateringen.

Derefter er et besøg af [Arch Linux' hjemmeside](https://archlinux.org/) altid på sin plads. Når en opdatering kræver brugerindblanding er der ofte et indlæg på hjemmesiden. Normalt vil der også være folk i forum som skriver kort efter pakkerne når deres filspejle, med detajler om løsninger til problemerne.

Når en opdatering udføres, læs venligst de meddelelser som udskrives af pacman. Dem som laver pakkerne beskriver ofte ændringerne og forventede problemer, og henviser brugere til den rette wikiside eller ressource. Endelig husk, **læs altid al information som udskrives af pacman!**

**Tip:** Husk på at det pacman udskriver, placeres i en logfil i `/var/log/pacman.log`.

### Forespørgsler i pakkedatabasen

**Pacman** kan søge i pakkedatabasen og lave en liste over pakker. Du kan angive en del af pakkenavnet, for at søge efter alle pakker, der matcher søgestrengen:

```
$ pacman -Ss pakke

```

For kun at søge i de installerede pakker:

```
$ pacman -Qs pakke

```

Hvis du kender navnet på den pakke, du søger efter, kan du hente information om pakken. Bemærk at kommandoen *-Qi* (Query info = forespørgselsinformation) giver mere information end *-Si* (sync info = synkroniseringsinformation), hvis pakken er installeret.

```
$ pacman -Si pakke
$ pacman -Qi pakke

```

Få en liste over filer indeholdt i en pakke:

```
$ pacman -Ql pakke

```

Få en liste over filer, der ikke længere benyttes af nogen for tiden installerede pakker:

```
$ pacman -Qe 

```

Du kan også se hvilken pakke en fil tilhører med:

```
$ pacman -Qo /søgesti/til/fil

```

**Tip:** Du kan også finde ud af hvilken pakke en fil der ikke er installeret tilhører ved at installere **pkgtools** fra [community]

### Anden anvendelse

**Pacman** er et temmelig vidtrækkende værktøj til pakkehåndtering.

Her er et lille udsnit af de andre muligheder:

*   Download en pakke **uden** at installere den:

```
# pacman -Sw pakkenavn

```

*   Installér en lokal pakke (ikke fra softwarekilde):

```
# pacman -U /søgesti/til/pakke/pakkenavn-version.pkg.tar.gz

```

*   Ryd pakke-cachen fuldstændigt (`/var/cache/pacman/pkg`):

```
# pacman -Scc

```

*   Geninstallér en pakke, der ikke kan fjernes pga. afhængighedsproblemer:

```
# pacman -S --force pakkenavn

```

For en mere detaljeret liste over parametre henvises til `pacman --help` eller `man pacman`.

## Konfiguration

Pacman's konfigurationsfil findes i `/etc/pacman.conf`. Mere dybtgående information om konfigurationsfilen findes i `man pacman.conf`.

### Generelle valgmuligheder

Generelle valgmuligheder findes i sektionen [options]. Læs man-siden eller kig i standardudgaven af pacman.conf efter information om, hvad der kan gøres her:

### Softwarekilder

I denne sektion angives, hvilke af de softwarekilder, der henvises til i `/etc/pacman.conf`, der skal benyttes. Disse findes på lister i `/etc/pacman.d/`. Softwarekilderne kan angives direkte, eller du kan inkludere dem fra en anden fil. Filerne i denne mappe inkluderer **community**, **core**, **extra** og **testing**. Det er vigtigt at redigere hver af disse filer, for at inkludere de software-kilder du ønsker. Det følgende er et eksempel på de officielle softwarekilder, der har adskillige [serverspejle](/index.php/Mirrors "Mirrors"). Undgå at bruge ftp.archlinux.org på grund af [flaskehalsproblemer](https://www.archlinux.org/news/302/).

```
[navn på software-kilde]
Server = ftp://server.net/repo

```

```
[core]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/core

```

**Bemærk** vær forsigtig med at benytte software-kilderne **testing**.

### Fejl

Hvis du får fejlen **not found in sync db** er det sikkert fordi pakken ikke kan findes, da software-kilden ikke er sat rigtigt op:

## Relaterede links

[Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")
[Colored Pacman output](/index.php/Colored_Pacman_output "Colored Pacman output")
[Downgrade packages](/index.php/Downgrade_packages "Downgrade packages")
[Editing pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html)
[Redownloading all installed packages](/index.php/Redownloading_all_installed_packages "Redownloading all installed packages")
[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
[Local repository HOW-TO](/index.php/Local_repository_HOW-TO "Local repository HOW-TO")
[Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync")
[Howto Upgrade via Home Network](/index.php/Howto_Upgrade_via_Home_Network "Howto Upgrade via Home Network") (Network Shared Pacman Cache)
[Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")
[Pacman Aliases (for bash)](/index.php/Pacman_Aliases "Pacman Aliases")