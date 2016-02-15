_Omdat er veel verwarring is over de officiële repository's, zal dit artikel proberen om wat duidelijkheid te scheppen:_

## Contents

*   [1 Historische achtergrond](#Historische_achtergrond)
*   [2 Lijst van repository's](#Lijst_van_repository.27s)
    *   [2.1 [core]](#.5Bcore.5D)
    *   [2.2 [extra]](#.5Bextra.5D)
    *   [2.3 [community]](#.5Bcommunity.5D)
    *   [2.4 [testing]](#.5Btesting.5D)
    *   [2.5 [unsupported]](#.5Bunsupported.5D)

## Historische achtergrond

Het overgrote gedeelte van de splitsingen in de repository's bestaat omdat dit vroeger zo was. Oorspronkelijk, toen Arch Linux nog maar door een aantal gebruikers werd gebruikt, was er slechts één repository, dat [official] heette (nu [core]). Toen bevatte [official] eigenlijk alleen de pakketten die Judd Vinet's voorkeur hadden. Het was ontworpen om slechts één programma van elk type te bevatten -- één browser, één desktopomgeving, etcetera.

Er waren toen gebruikers, die Judd's pakketselectie niet beviel. Omdat [Arch Build System](/index.php/Arch_Build_System "Arch Build System") erg makkelijk te gebruiken is, maakten ze zelf pakketten. Deze pakketten gingen in een repository, genoemd [unofficial] en werden onderhouden door andere ontwikkelaars als Judd. Uiteindelijk werden beide repository's door de ontwikkelaars als even goed ondersteund gezien, waardoor de namen [official] en [unofficial] niet langer pasten. De repository's [official] en [unofficial] werden vervolgens hernoemd naar [current] en [extra], rond het uitkomen van versie 0.5 van Arch Linux.

Kort na de 2007.8.1 versie werdt [current] hernoemt naar [core], om verwarring over de inhoud van de repository te voorkomen. De repository's zijn nu min of meer gelijk in de ogen van de ontwikkelaars en de gebruikers, maar [core] verschilt op een aantal punten. Het grootste verschil is dat pakketten, die voor de installatie-CD's worden gebruikt, alleen van [core] worden gehaald. Deze repository geeft nog steeds een compleet Linux systeem, hoewel het niet het Linux systeem zal zijn dat je wilt.

Rond versie 0.5 of 0.6 kwamen de ontwikkelaars erachter dat er een grote hoeveelheid pakketten waren, die ze niet wilden onderhouden. Eén van de ontwikkelaars (Xentac) richtte toen het "Trusted User Repository" op, wat een onofficieel repository was, waar vertrouwde gebruikers de pakketten konden plaatsen, die ze gemaakt hadden. Er was ook een [staging] repository, waaruit de Arch Linux ontwikkelaars pakketten konden promoveren naar de officiële repository's, maar verder waren de ontwikkelaars en de vertrouwde gebruikers min of meer gescheiden.

Dit werkte een tijdje, maar niet toen de vertrouwde gebruikers verveeld raakten met hun repository's en niet toen de niet vertrouwde gebruikers hun zelfgemaakte pakketten wilden delen. Dit leed tot de ontwikkeling van [AUR](https://aur.archlinux.org/) (Arch User Repository). De vertrouwde gebruikers (ook wel TU's genoemd) werden in een meer hechte groep samengevoegd, die nu samen de [community] repository onderhouden. De TU's zijn nog steeds een andere groep dan de Arch Linux ontwikkelaars en er is niet veel communicatie tussen hen. Wel is het zo dat populaire pakketten, in sommige gevallen, nog steeds worden gepromoveerd van [community] naar [extra]. [AUR](https://aur.archlinux.org/) staat niet vertrouwde gebruikers ook toe om hun PKGBUILDS in te sturen, zodat andere gebruikers deze kunnen gebruiken als ze willen. Deze pakketten worden niet ondersteund en de pakketten worden soms het [unsupported] repository genoemd, hoewel er geen binaire pakketten worden verspreid. TU's kunnen pakketten "adopteren" van unsupported in [community] als ze dat willen omdat het pakket populair is of als ze geinteresseerd zijn in het onderhouden van dat pakket.

## Lijst van repository's

### [core]

Het [core] repository kan worden gevonden in _core/os/i686_ of _core/os/x86_64_ op je favoriete spiegelserver. Het bevat Arch's core pakketten en een aantal extra softwarepakketten, die je voorzien van een volledig functioneel basis-systeem.

_De installatie-CD bevat simpelweg een installatiescript en een momentopname van de inhoud van het [core] repository._

### [extra]

Het [extra] repository kan worden gevonden in _extra/os/i686_ of _extra/os/x86_64_ op je favoriete spiegelserver. Het bevat alle pakketten die niet in [core] passen. Voorbeeld: X.org, window managers, web servers, mediaspelers, programmeertalen als Python, Ruby en Perl en nog veel meer.

### [community]

Het [community] repository kan worden gevonden in _community/os/i686_ of _community/os/x86_64_ op je favoriete spiegelserver. Deze repository wordt onderhouden door de TU's (Trusted Users, oftewel vertrouwde gebruikers), en is onderdeel van het _Arch User Repository (AUR)_. Het bevat pakketten van _AUR_, die genoeg stemmen hebben en geadopteerd zijn door een _TU_.

### [testing]

Het [testing] repository kan worden gevonden in _testing/os/i686_ of _testing/os/x86_64_ op je favoriete spiegelserver. Deze repository is speciaal, omdat het pakketten bevat, die kandidaat zijn voor de repository's [core] of [extra]. Nieuwe pakketten gaan in [testing] als:

*   er van wordt verwacht dat ze iets vernielen tijdens updaten en eerst moeten worden getest
*   ze afhankelijk zijn van andere pakketten, die eerst opnieuw moeten worden gebouwd. In dit geval worden alle pakketten die opnieuw moeten worden gebouwd, eerst in [testing] gezet, en worden pas naar de originele repository's gezet, als alle pakketten opnieuw gebouwd zijn.

[testing] is het enige repository die botsingen in de namen van pakketten kan hebben met elk van de andere officiële repository's. Indien geactiveerd, moet [testing] de eerste repository zijn in je _pacman.conf_ bestand.

Wees voorzichtig als je [testing] activeert. Je systeem kan breken (in de zin van niet functioneel worden) als je een update uitvoert met [testing] geactiveerd. Alleen ervaren gebruikers zouden [testing] moeten gebruiken.

### [unsupported]

Het [unsupported] repository is eigenlijk helemaal geen repository. Het verwijst naar een database van door gebruikers ingestuurde bouw-scripts, beter bekend als PKGBUILDS, maar bevat geen gebouwde pakketten, waardoor het geen echte repository is. Gebruikers kunnen geen pakketten downloaden of installeren uit [unsupported] met behulp van [pacman](/index.php/Pacman "Pacman"). Ze moeten de PKGBUILDS handmatig downloaden en de binaries zelf compileren, of één van de populaire [AUR helpers](/index.php/AUR_helpers "AUR helpers") gebruiken, om deze taak te automatiseren.