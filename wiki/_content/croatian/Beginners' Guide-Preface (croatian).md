**Tip:** Ovo je dio višestraničnog članka vodiča za početnike. **[Klikni ovdje](/index.php/Beginners%27_guide_(Hrvatski) "Beginners' guide (Hrvatski)")** ukoliko želiš pročitati vodič u cijelosti.

## Contents

*   [1 Predgovor](#Predgovor)
    *   [1.1 Uvod](#Uvod)
    *   [1.2 Licenca](#Licenca)
    *   [1.3 Put Archa](#Put_Archa)
    *   [1.4 O ovom vodiču](#O_ovom_vodi.C4.8Du)

## Predgovor

### Uvod

Dobrodošli! Ovaj vodič će te voditi kroz proces instalacije sustava [Arch Linux](/index.php/Arch_Linux_(Hrvatski) "Arch Linux (Hrvatski)"): jednostavne distribucije [GNU](/index.php?title=GNU_Project_(Hrvatski)&action=edit&redlink=1 "GNU Project (Hrvatski) (page does not exist)")/Linuxa stvorene za sposobne korisnike. Vodičem se cilja na nove Arčere, ali se pokušava i stvoriti snažna informacijska podloga za sve korisnike.

Prije instalacije bi bilo dobro proletjeti kroz [često postavljena pitanja](/index.php/FAQ_(Hrvatski) "FAQ (Hrvatski)").

**Istaknimo neke značajke distribucije Arch Linuxa:**

*   [Jednostavan](/index.php/The_Arch_Way_(Hrvatski) "The Arch Way (Hrvatski)") dizajn i filozofija
*   [Svi paketi](https://www.archlinux.org/packages/?q=) su kompilirani i za [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) i za [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") arhitekture
*   Inicijalizacijske skripte u [BSD stilu](/index.php?title=Arch_Boot_Process_(Hrvatski)&action=edit&redlink=1 "Arch Boot Process (Hrvatski) (page does not exist)"), koristeći jednu centraliziranu konfiguracijsku datoteku
*   [mkinitcpio (Hrvatski)](/index.php?title=Mkinitcpio_(Hrvatski)&action=edit&redlink=1 "Mkinitcpio (Hrvatski) (page does not exist)") je jednostavan i dinamičan stvaraoc [initramfsa](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Upravitelj paketima](https://en.wikipedia.org/wiki/Package_manager je agilan i lak kao perce, s vrlo skromnim zauzećem memorije
*   [Paketni sustav Archa](/index.php?title=Arch_Build_System_(Hrvatski)&action=edit&redlink=1 "Arch Build System (Hrvatski) (page does not exist)"): sustav stvaranja paketa koji pruža jednostavnu okolinu za stvaranje instalacijskih Arch paketa putem izvornog koda
*   [Korisnički repozitorij Archa](/index.php?title=Arch_User_Repository_(Hrvatski)&action=edit&redlink=1 "Arch User Repository (Hrvatski) (page does not exist)"): pruža tisuće i tisuće korisničkih instalacijskih skripti te priliku za dijeljenje vlastitih

### Licenca

Arch Linux, pacman, documentation, and scripts are Copyright © 2002-2007 by Judd Vinet, Copyright © 2007-2011 by Aaron Griffin and are licensed under the [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### Put Archa

***Principi dizajna Archa su tu da ga održe [jednostavnim](/index.php/The_Arch_Way_(Hrvatski) "The Arch Way (Hrvatski)").***

'Jednostavan', u ovom kontekstu, znači 'bez nepotrebnih dodataka, modifikacija ili komplikacija'. Ukratko: elegantan, minimalistički pristup.

**Tijekom razmišljanja o jednostavnosti valja imati na umu:**

*   *" 'Jednostavnost' je definirana iz tehničkog gledišta, a ne korisničkog. Bolje je biti tehnički elegantan uz veće zahtjeve znanja nego biti jednostavan za koristiti i tehnički [inferioran]." -Aaron Griffin*
*   *Entia non sunt multiplicanda praeter necessitatem* ili "Entiteti se ne bi smjeli nepotrebno množiti." -Occamova oštrica. Pojam *oštrica* odnosi se na čin uklanjanja nepotrebnih komplikacija da bi se stiglo do najjednostavnijeg objašnjenja, metode ili teorije.
*   *"Nevjerojatnost [moje metode] leži u njenoj jednostavnosti. Visine uglađenosti uvijek vode ka jednostavnosti."* - Bruce Lee

### O ovom vodiču

[Arch wiki](/index.php/Main_page_(Hrvatski) "Main page (Hrvatski)") je održavan putem zajednice te je odličan izvor s kojim se uvijek može pokušati konzultirati pri prvim suočavanjem s nekim problemom. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanal ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) i [forumi](https://bbs.archlinux.org/) su isto dostupni ukoliko se traženi odgovor ne može naći igdje drugdje. Svakako provjeri i `man` stranice bilo koje naredbe s kojom imaš problema; to se obično može učiniti pozivanjem `man *naredbe*`.

**Note:** Usko pratiti ovaj vodič od ključne je važnosti kako bi se moglo doći do ispravno konfiguriranog sustava Arch Linux, tako da ga valja pročitati temeljito. Preporuča se pročitati svaki sekciju u potpunosti <u>prije</u> implementacije koraka navedenih u njoj.

**[Vodič za početnike](/index.php/Beginners%27_Guide_(Hrvatski) "Beginners' Guide (Hrvatski)")**

* * *

**Predgovor** >> [Priprema](/index.php/Beginners%27_Guide/Preparation_(Hrvatski) "Beginners' Guide/Preparation (Hrvatski)") >> [Instalacija](/index.php/Beginners%27_Guide/Installation_(Hrvatski) "Beginners' Guide/Installation (Hrvatski)") >> [Nakon instalacije](/index.php/Beginners%27_Guide/Post-Installation_(Hrvatski) "Beginners' Guide/Post-Installation (Hrvatski)") >> [Bilješke](/index.php/Beginners%27_Guide/Extra_(Hrvatski) "Beginners' Guide/Extra (Hrvatski)")