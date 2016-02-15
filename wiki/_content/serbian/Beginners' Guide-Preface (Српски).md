**Tip:** Ovo je deo Uputstva za pocetnike koji se sastoji iz vise strana. **[Kliknite ovde](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)")** ako zelite da citate uputstvo u celosti.

## Contents

*   [1 Predgovor](#Predgovor)
    *   [1.1 Uvod](#Uvod)
    *   [1.2 Licenca](#Licenca)
    *   [1.3 Arch nacin](#Arch_nacin)
    *   [1.4 O ovom uputstvu](#O_ovom_uputstvu)

## Predgovor

### Uvod

Dobrodosli. Ovaj dokument ce vas voditi kroz proces instaliranja [Arch Linux](/index.php/Arch_Linux "Arch Linux")-a: jednostavne, lake [GNU](/index.php/GNU_Project "GNU Project")/Linux distribucije namenjene kompetentnim korisnicima. Ovo uputstvo je namenjeno novim Arch korisnicima, ali tezi ka tome da bude jaka referenca i izvor informacija za sve.

Preporucujemo vam da predjete [Cesto postavljana pitanja](/index.php?title=FAQ_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "FAQ (Српски) (page does not exist)") pre instalacije.

**Prednosti Arch Linux distribucije:**

*   [Jednostavan](/index.php/The_Arch_Way_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "The Arch Way (Српски)") dizajn i filozofija
*   [Svi paketi](https://www.archlinux.org/packages/?q=) su kompajlirani za [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") i [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") arhitekture
*   [Rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") model, koji omogucava da samo jednom instalirate sistem, a zatim ga azurirate u kontinuitetu i na taj nacin uvek imate najskorije stabilne verzije instaliranog softvera
*   [BSD stil](/index.php?title=Arch_Boot_Process_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Arch Boot Process (Српски) (page does not exist)") init skripti koji zastupa jedan centralizovani fajl za podesavanja
*   [mkinitcpio (Српски)](/index.php?title=Mkinitcpio_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Mkinitcpio (Српски) (page does not exist)") je jednostavan i dinamicki [initramfs](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd") kreator
*   [Pacman (Српски)](/index.php/Pacman_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Pacman (Српски)") [paket menadzer](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") je lagan i brz, sa vrlo malim memorijskim otiskom
*   [Arch Build System (Српски)](/index.php?title=Arch_Build_System_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Arch Build System (Српски) (page does not exist)"): Sistem za izgradnju paketa po ugledu na portove koji pruza jednostavan radni okvir za pravljenje Arch paketa iz izvornog koda.
*   [Arch User Repository (Српски)](/index.php/Arch_User_Repository_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Arch User Repository (Српски)"): pruza vise hiljada korisnickih skripti za izgradnju i mogucnost da podelite vase

### Licenca

Arch Linux, pacman, dokumentacija i skripte su Copyright © 2002-2007 by Judd Vinet, Copyright © 2007-2011 by Aaron Griffin i licencirani pod [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### Arch nacin

_**Dizajn principi iza Arch-a imaju za cilj da ga ucine [jednostavnim](/index.php/The_Arch_Way_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "The Arch Way (Српски)").**_

'Jednostavan', u ovom kontekstu, bi znacilo 'bez bespotrebnih dodataka, modifikacija ili komplikacija'. Ukratko; elegantan, minimalisticki pristup.

**Kada razmatrate jednostavnost, imajte sledece na umu:**

*   _" 'Jednostavno' je definisano sa tehnicke tacke gledista, a ne sa tacke gledista upotrebljivosti. Bolje je biti tehnicki elegantan sa visom krivom ucenja, nego biti lak za koriscenje i tehnicki [inferioran]." -Aaron Griffin_
*   _Entia non sunt multiplicanda praeter necessitatem_ ili "Entitete ne bi trebalo umnozavati bespotrebno." -Occam's razor. Termin _razor_ se odnosi na cin uklanjanja (brijanja) bespotrebnih komplikacija da se dodje do najjednostavnijeg objasnjenja, metode ili teorije.
*   _"Izuzetni deo [moje metode] lezi u jednostavnosti.. Visina kultivacije uvek tezi ka jednostavnosti."_ - Bruce Lee

### O ovom uputstvu

Odrzavan od strane zajednice, [Arch wiki](/index.php/Main_Page_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Main Page (Српски)") je odlican izvor za resavanje problema. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanali ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) i ([irc://irc.freenode.net/#archlinux-rs](irc://irc.freenode.net/#archlinux-rs)), i [forumi](https://bbs.archlinux.org/) su takodje na raspolaganju ukoliko ne mozete da pronadjete odgovor. Posetite i `man` stranice za komande sa kojima niste upoznati; to mozete uciniti sa `man "komandom`_._

**Note:** Pazljivo pracenje ovog uputstva je od kljucnog znacaja kako bi ste uspesno instalirali i podesili Arch Linux sistem, pa vas "molimo" da ga detaljno procitate. Jako je preporucljivo da procitate svaku sekciju u celosti <u>pre</u> obavljanja posla koji sekcija opisuje.

Uputstvo je podeljeno u 5 glavnih delova:

*   [Deo I: Priprema](/index.php/Beginners%27_Guide/Preparation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)#Preparation "Beginners' Guide/Preparation (Српски)")
*   [Deo II: Instalacija](/index.php/Beginners%27_Guide/Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)#Installation "Beginners' Guide/Installation (Српски)")
*   [Deo III: Nakon instalacije](/index.php/Beginners%27_Guide/Post-Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)#Post-Installation "Beginners' Guide/Post-Installation (Српски)")
*   [Part IV: Dodaci](/index.php/Beginners%27_Guide/Extra_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)#Extra "Beginners' Guide/Extra (Српски)")
*   [Deo V: Prilog](/index.php/Beginners%27_Guide/Extra_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)#Appendix "Beginners' Guide/Extra (Српски)")

**[Beginners' Guide (Српски)](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)")**

* * *

**Predgovor** >> [Priprema](/index.php/Beginners%27_Guide/Preparation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Preparation (Српски)") >> [Instalacija](/index.php/Beginners%27_Guide/Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Installation (Српски)") >> [Nakon instalacije](/index.php/Beginners%27_Guide/Post-Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Post-Installation (Српски)") >> [Dodaci/Prilog](/index.php/Beginners%27_Guide/Extra_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Extra (Српски)")