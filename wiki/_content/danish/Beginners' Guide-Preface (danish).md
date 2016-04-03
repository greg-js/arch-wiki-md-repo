**Bemærk:** Dette er en del af en flersides artikel til Begynderguiden. **[Klik her](/index.php/Beginners%27_guide_(Dansk) "Beginners' guide (Dansk)")** hvis du hellere vil læse guiden i sin helhed.

## Contents

*   [1 Forord](#Forord)
    *   [1.1 Introduktion](#Introduktion)
    *   [1.2 Licens](#Licens)
    *   [1.3 Arch-metoden](#Arch-metoden)
    *   [1.4 Om denne guide](#Om_denne_guide)

## Forord

### Introduktion

Dette dokument vil guide dig igennem installation og konfiguration af [Arch Linux](/index.php/Arch_Linux_(Dansk) "Arch Linux (Dansk)"); en simpel, letvægts GNU/Linux distribution målrettet erfarne brugere. Denne guide er rettet mod nye brugere af Arch Linux, men tilstræber at være en stærk reference og en basis for indlæring for alle.

**Arch Linux distributions højdepunkter:**

*   [Simpel](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)") design og filosofi
*   [Alle pakker](https://www.archlinux.org/packages/?q=) kompileret til i686- og x86_64-arkitekturene
*   [BSD stil](/index.php?title=Arch_Boot_Process_(Dansk)&action=edit&redlink=1 "Arch Boot Process (Dansk) (page does not exist)") opstartsscripts, med en centraliseret konfigurationsfil
*   [mkinitcpio](/index.php/Mkinitcpio_(Dansk) "Mkinitcpio (Dansk)"): En simpel og dynamisk initramfs-skaber
*   [Pacman](/index.php/Pacman_(Dansk) "Pacman (Dansk)") pakkehåndtering er letvægt og hurtigt, med et minimalt hukommelsesforbrug
*   [Arch byggesystem](/index.php/Arch_Build_System_(Dansk) "Arch Build System (Dansk)"): Et *ports*-lignende pakkebygningssystem; giver en simpel metode til at skabe pakker til Arch Linux
*   [Arch brugerpakkelager](/index.php/Arch_User_Repository_(Dansk) "Arch User Repository (Dansk)"): Tilbyder tusindvis af brugerbidragede pakkescripts samt muligheden for at dele dine egne

### Licens

Arch Linux, Pacman, dokumentationen og scripts er copyright ©2002-2007 Judd Vinet, ©2007-2011 Aaron Griffin, og er licenserede under [GNU General Public License v2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### Arch-metoden

***Designprincipperne bag Arch Linux har til mål at holde det [enkelt](/index.php/The_Arch_Way_(Dansk) "The Arch Way (Dansk)")***

'Enkelt,' i denne sammenhæng, har betydningen 'uden unødige tilføjelser, ændringer eller komplikationer.' Kort fortalt; en elegant, minimalistisk tilgang.

**Nogle tanker som du kan holde fast i, når du overvejer enkelthed:**

*   *" 'Enkelt' defineres ud fra et teknisk standpunkt og ikke i brugsøjemed. Det er bedre at være teknisk elegant med en højere indlæringskurve, end at være letanvendelig og teknisk noget juks." -Aaron Griffin*
*   *Entia non sunt multiplicanda praeter necessitatem* eller "Enheder skal ikke multiplikeres unødigt." -Occams barberblad. Med *barberblad* menes handlingen at barbere unødvendige forudsætninger og komplikationer væk for at opnå den enkleste forklaring, metode eller teori.

### Om denne guide

Den fællesdrevne [Arch wiki](/index.php/Main_page_(Dansk) "Main page (Dansk)") er en glimrende ressource og bør konsulteres først ved problemer. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanalen ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), og [forum](https://bbs.archlinux.org/) er også tilgængelige hvis svaret ikke kan findes andre steder. Derudover bør du tjekke `man`-siden til enhver kommando du ikke kender.

**Bemærk:** At følge denne guide er essentielt for at installere et rigtigt konfigureret Arch Linux system, så læs den *venligst* grundigt. Det er stærkt anbefalet at læse hver sektion helt <u>før</u> du udfører opgaverne deri.

Guiden er opdelt i fire hoveddele:

*   [Del I: Forbered installationen](/index.php/Beginners%27_Guide/Preparation_(Dansk)#Forbered_installationen "Beginners' Guide/Preparation (Dansk)")
*   [Del II: Installer grundsystemet](/index.php/Beginners%27_Guide/Installation_(Dansk)#Installer_grundsystemet "Beginners' Guide/Installation (Dansk)")
*   [Del III: Efter installationen](/index.php?title=Beginners%27_Guide/Post-Installation_(Dansk)&action=edit&redlink=1 "Beginners' Guide/Post-Installation (Dansk) (page does not exist)")
*   [Del IV: Ekstra](/index.php?title=Beginners%27_Guide/Post-Installation_(Dansk)&action=edit&redlink=1 "Beginners' Guide/Post-Installation (Dansk) (page does not exist)")

**[Begynderguiden](/index.php/Beginners%27_Guide_(Dansk) "Beginners' Guide (Dansk)")**

* * *

**Forord** >> [Forbered installationen](/index.php/Beginners%27_Guide/Preparation_(Dansk) "Beginners' Guide/Preparation (Dansk)") >> [Installer grundsystemet](/index.php/Beginners%27_Guide/Installation_(Dansk) "Beginners' Guide/Installation (Dansk)") >> [Efter installationen](/index.php?title=Beginners%27_Guide/Post-Installation_(Dansk)&action=edit&redlink=1 "Beginners' Guide/Post-Installation (Dansk) (page does not exist)") >> [Yderligere læsning](/index.php?title=Beginners%27_Guide/Extra_(Dansk)&action=edit&redlink=1 "Beginners' Guide/Extra (Dansk) (page does not exist)")