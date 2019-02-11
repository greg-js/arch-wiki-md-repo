Deze pagina vat de overeenkomsten en de verschillen samen tussen Arch en andere distributies. De vraag komt vaak voor en daarom is het aardig om een standaard antwoord te hebben. Nota bene: de beste manier om Arch te vergelijken met andere distributies is om het te installeren en zelf uit te proberen. Arch heeft een geweldige gebruikersgemeenschap die altijd bereid is om nieuwe gebruikers te helpen. De samenvattingen hieronder zijn alleen bedoeld om je genoeg informatie te geven om te beslissen of Arch echt voor jou is.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Arch vs Gentoo](#Arch_vs_Gentoo)
*   [2 Arch vs Crux](#Arch_vs_Crux)
*   [3 Arch vs Sorcerer/Lunar-linux/Sourcemage](#Arch_vs_Sorcerer/Lunar-linux/Sourcemage)
*   [4 Arch vs grafische distributies](#Arch_vs_grafische_distributies)
*   [5 Arch vs Slackware](#Arch_vs_Slackware)
*   [6 Arch vs Debian](#Arch_vs_Debian)
*   [7 Arch vs Ubuntu](#Arch_vs_Ubuntu)
*   [8 Arch vs RPM-gebaseerde distributies](#Arch_vs_RPM-gebaseerde_distributies)
*   [9 Arch vs Fedora](#Arch_vs_Fedora)
*   [10 Arch vs Mandriva](#Arch_vs_Mandriva)
*   [11 Arch vs SuSE](#Arch_vs_SuSE)
*   [12 Arch vs Frugalware](#Arch_vs_Frugalware)

## Arch vs Gentoo

Omdat Arch als binaries verspreid wordt, neemt het veel minder tijd in dan Gentoo. Gentoo heeft meer pakketten. Arch ondersteunt zowel binary's als broncode. PKGBUILD's zijn makkelijk te maken dan ebuilds. Gentoo ondersteunt meerdere architecturen omdat de pakketten gecompileerd worden voor een specifieke architectuur, terwijl Arch er alleen is voor de i686 en de x64\. Er is geen bewijs dat Gentoo sneller is dan Arch.

## Arch vs Crux

Arch Linux is een afstammeling van Crux. Judd vatte eens de verschillen zo samen:

	"I used Crux before starting Arch. Arch started out as Crux, pretty much. Then I wrote pacman and makepkg to replace my bash pseudo packaging scripts (I built Arch as an LFS system to begin). So the two are completely separate distros, but technically, they're almost the same. We have dependency support (officially) for example, although Crux has a community that provides other features. CLC's prt-get will do rudimentary dependency logic. Crux gets to ignore lots of problems we have too, since it's a very minimalistic package set, basically what Per uses and nothing else."

Zie [deze forumpost](https://bbs.archlinux.org/viewtopic.php?t=3608&start=270#133721) voor de impressie van een gebruiker van beide distributies.

## Arch vs Sorcerer/Lunar-linux/Sourcemage

Sorcerer/Lunar-linux/Sourcemage (SLS) zijn source-code distributies, zoals Gentoo, en zijn allemaal aan elkaar gerelateerd. SLS distributies gebruiken een simpele groep script-files om de omschrijving van de pakketten te maken, en ze gebruiken een globaal configuratie bestand voor het compileer-proces, net zoals Arch's ABS systeem. De SLS utilties doen een volledige dependency check, package tracking. Er zijn geen binary pakketten voor een distributie van de SLS familie, hoewel ze wel alle eerdere versies van pakketten makkelijk kunnen installeren.

De installatie bestaat uit een basissysteem (wat veel lijkt op Arch's: geoptimaliseerd voor i686, CLI en ncurses menus en alleen basis-tools), vervolgens wordt het basis systeem (optioneel) opnieuw gehercompileerd. Er is geen standaard Windowmanager/Desktop environment/Desktop manager en tijdens de basis-installatie wordt er geen Xserver geinstalleerd. Er wordt overigens wel een optie aangeboden om een alternatieve Xserver te installeren (Xorg 6.8 of 7, Xfree86)

SLS heeft een zeer ingewikkelde geschiedenis. Zie ook [http://wiki.sourcemage.org/Our_History](http://wiki.sourcemage.org/Our_History)

Lunar Linux: [http://lunar-linux.org/](http://lunar-linux.org/) SourceMage: [http://www.sourcemage.org/](http://www.sourcemage.org/) Sorcerer: [http://sorcerer.berlios.de/](http://sorcerer.berlios.de/)

## Arch vs grafische distributies

De grafische distributies hebben veel overeenkomsten en Arch verschilt veel met ze. Arch is gebaseerd op tekst en georiënteerd op de commandolijn. Arch is een betere distributie als je echt Linux wilt leren. Grafisch gebaseerde distributies komen meestal met GUI installaties (zoals Fedora's Anacaonda) en GUI systeem configuratiegereedschap (zoals SuSe's Yast). De specifieke verschillen tussen de distributies worden hieronder beschreven.

## Arch vs Slackware

Slackware en Arch zijn allebei "eenvoudige" distributies. Ze gebruiken allebei BSD-achtige initscripts. Arch komt met een veel robuuster package beheersysteem dan Slackware. Met pacman is het mogelijk eenvoudig automatische systeem-upgrades uit te voeren. Slackware wordt gezien als wat meer conservatief in de manier waarop nieuwe versies worden uitgebracht, er wordt gekozen voor pakketten waarvan bewezen is dat ze stabiel zijn. Arch is veel meer "bleeding edge" in dit opzicht. Arch is er alleen voor de i686 terwijl Slackware ook draait op i486 systemen. Arch is een goed systeem voor Slackware gebruikers die een robuuster package beheersysteem willen of meer huidige pakketten.

## Arch vs Debian

Arch is eenvoudiger dan Debian. Arch heeft minder pakketten. Arch heeft betere ondersteuning voor het maken van de eigen pakketten dan Debian. Arch is wat toleranter als het gaat on niet vrije programmatuur volgens GNU. Arch is geoptimaliseerd en dus sneller dan Debian (geen bewijs). Arch's pakketten zijn meer "bleeding edge" dan Debian's pakketten (Arch current bevat vaak nieuwere pakketten dan Debian unstable!).

## Arch vs Ubuntu

Arch is in principe simpeler dan Ubuntu. Als je graag je eigen kernels compileert, de laatste nieuwe "bleeding edge" CVS-only projecten uitprobeert of af en toe graag een programma compileert, dan is Arch beter voor jou. Als je graag snel en zonder veel gepruts aan de slag wilt, dan is Ubuntu beter voor jou. In het algemeen verkiezen ontwikkelaars en personen die graag dingen uitproberen meestal Arch boven Ubuntu.

## Arch vs RPM-gebaseerde distributies

RPM-paketten zijn op veel plaatsen verkrijgbaar, maar pakketten van een derde hebben vaak problemen met dependencies, zoals het vereisen van een oude versie van een bibliotheek. Er is ook verwarring tussen RPM-paketten voor Redhat vs. RPM-paketten voor Mandrake. Pacman is veel krachtiger en betrouwbaarder dan RPM.

## Arch vs Fedora

Fedora is een afstammeling van Red-Hat en is daardoor altijd één van de meest populaire distributies geweest. Daardoor heeft Fedora een grote community en vele prefab pakketten en is er veel hulp aanwezig. Zoals elke RPM-gebaseerde distributie is de package management een probleem. Fedora gebruikt Yum als een front-end voor het beheren van RPMs. Jammer genoeg was tot Fedora Core 5 de integratie van Yum niet goed genoeg. Fedora is een innovatieve distributie en heeft veel harten gewonnen door de integratie van SELinux en GCJ gecompileerde pakketten, zodat Sun's Java Runtime niet meer nodig is. Fedora is bekend om het feit dat men niet probeert om het mp3 formaat te ondersteunen (door problemen met patenten)

## Arch vs Mandriva

Mandrive (voormalig Mandrake) is bekend vanwege zijn installatieprocedure en het feit dat de distributie erg veel voor de gebruiker doet, wat na een tijd als irritant ervaren kan worden. Een ander probleem is dat Mandriva een RPM-gebaseerde distributie is. Arch is een distributie die de gebruiker vrij laat en de gebruiker meer zelf laat doen. Bij Arch leert men iets van het systeem.

## Arch vs SuSE

Suse draait om het configuratiegereedschap Yast. Het is de plaats waar de meeste gebruikers al het configuratiewerk kunnen doen. Arch heeft niet zo'n mogelijkheid, omdat het tegen [The Arch Way](/index.php/The_Arch_Way "The Arch Way") ingaat. Suse wordt daarom gezien als beter geschikt voor gebruikers met minder ervaring of zij die een simpeler leven willen, waarin alles gewoon werkt na het installeren. Suse heeft standaard na het installeren geen ondersteuning voor mp3's, maar deze functionaliteit kan op een later tijdstip eenvoudig worden toegevoegd met Yast.

## Arch vs Frugalware

Arch is een text-gebaseerde en op de command-line georiëteerde distributie. Frugalware is een distributie die gebaseerd is op Slackware. Frugalware heeft een betere ondersteuning voor talen. Ook heeft Frugalware meer lokale documentatie. Frugalware claimt sneller te zijn dan Arch. Beide gebruiken pacman, maar de pakketten zijn niet uitwisselbaar.