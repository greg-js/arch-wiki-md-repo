**Tip:** To część wielostronicowego artykułu Przewodnik Początkującego. **[Kliknij tutaj](/index.php/Beginners%27_Guide_(Polski) "Beginners' Guide (Polski)")** jeśli wolisz czytać przewodnik w całości.

## Contents

*   [1 Wstęp](#Wst.C4.99p)
    *   [1.1 Wprowadzenie](#Wprowadzenie)
    *   [1.2 Licencja](#Licencja)
    *   [1.3 Droga Archa](#Droga_Archa)
    *   [1.4 O tym przewodniku](#O_tym_przewodniku)

## Wstęp

### Wprowadzenie

Witaj. Ten artykuł przeprowadzi Cię przez proces instalacji systemu [Arch Linux_(Polski)](/index.php/Arch_Linux_(Polski) "Arch Linux (Polski)"): prostej, lekkiej dystrybucji [GNU](http://pl.wikipedia.org/wiki/Projekt_GNU)/Linux skierowanej do doświadczonych użytkowników. Ten przewodnik przeznaczony jest dla początkujących użytkowników Archa, może być jednak bazą informacji dla wszystkich.

Przed instalacją radzimy przejrzeć [FAQ](/index.php/FAQ "FAQ").

**Główne cechy dystrybucji Arch Linux:**

*   [Prosta](/index.php/The_Arch_Way_(Polski) "The Arch Way (Polski)") konstrukcja i filozofia
*   [Wszystkie pakiety](https://www.archlinux.org/packages/?q=) skompilowane dla architektur [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) oraz [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64")
*   Model [ciągłego wydania](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release"), pozwalający na jednorazową instalację i łatwą aktualizację zainstalowanego oprogramowania do ostatniej stabilnej wersji
*   Skrypty startowe w [stylu BSD](/index.php?title=Arch_Boot_Process_(Polski)&action=edit&redlink=1 "Arch Boot Process (Polski) (page does not exist)")
*   [Mkinitcpio](/index.php?title=Mkinitcpio_(Polski)&action=edit&redlink=1 "Mkinitcpio (Polski) (page does not exist)") to prosty i dynamiczny kreator [initramfs](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Menedżer pakietów](https://en.wikipedia.org/wiki/Package_manager jest lekki i zwinny, zachowując niskie zużycie pamięci
*   [Arch Build System](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)"): Podobny do portów system budowania pakietów, dostarczający prostego frameworka do tworzenia binarnych pakietów Archa z kodu źródłowego
*   [Arch User Repository](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)"): oferuje wiele tysięcy skryptów do budowania pakietów nadesłanych przez użytkowników i możliwość dzielenia się własnymi

### Licencja

Arch Linux, pacman, dokumentacja i skrypty są objęte licencją [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html). Copyright © 2002-2007 by Judd Vinet, Copyright © 2007-2011 by Aaron Griffin.

### Droga Archa

***Główne cele stojące za Archem mają na celu utrzymanie jego [prostoty](/index.php/The_Arch_Way_(Polski) "The Arch Way (Polski)").***

'Prostota', w tym kontekście, znaczy 'bez zbędnych dodatków, modyfikacji czy komplikacji'. W skrócie: eleganckie, minimalistyczne podejście.

### O tym przewodniku

[Arch Install Scripts](https://github.com/falconindy/arch-install-scripts) to zbiór skryptów [Basha](/index.php?title=Bash_(Polski)&action=edit&redlink=1 "Bash (Polski) (page does not exist)"), które upraszczają instalację Archa. Ten przewodnik podsumowuje podstawowy proces instalacji z użyciem tych skryptów.

**Note:** AIF (the Arch Installation Framework) nie jest dołączony do obrazów instalacyjnych ze względu na brak wsparcia (zobacz [https://www.archlinux.org/news/install-media-20120715-released/](https://www.archlinux.org/news/install-media-20120715-released/) po więcej informacji).

Utrzymywana przez społeczność [Arch wiki](/index.php/Main_Page_(Polski) "Main Page (Polski)") to znakomite źródło i w razie problemów należy się do niej odwołać. Kanał [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) i [forum](https://bbs.archlinux.org/) są dostępne, jeśli odpowiedź nie może być znaleziona w innym miejscu. Oprócz tego, sprawdź strony `man` każdej komendy, której nie znasz; zwykle można je wywołać poleceniem `man *komenda*`.

**Note:** Dokładne podążanie za tym poradnikiem jest niezbędne, aby zainstalować poprawnie skonfigurowany system Arch Linux, więc przeczytaj go dokładnie. Zaleca się, abyś przeczytał(a) każdą sekcję w całości <u>przed</u> wykonaniem zawartych w niej poleceń.

Ten poradnik jest podzielony na 5 głównych części:

*   [Część I: Przygotowanie](/index.php/Beginners%27_Guide/Preparation_(Polski)#Przygotowanie "Beginners' Guide/Preparation (Polski)")
*   [Część II: Instalacja](/index.php/Beginners%27_Guide/Installation_(Polski)#Instalacja "Beginners' Guide/Installation (Polski)")
*   [Część III: Po instalacji](/index.php/Beginners%27_Guide/Post-Installation_(Polski)#Post-Installation "Beginners' Guide/Post-Installation (Polski)")
*   [Część IV: Extra](/index.php/Beginners%27_Guide/Extra_(Polski)#Extra "Beginners' Guide/Extra (Polski)")
*   [Część V: Appendix](/index.php/Beginners%27_Guide/Extra_(Polski)#Appendix "Beginners' Guide/Extra (Polski)")