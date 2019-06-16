Related articles

*   [Category:Accessibility](/index.php/Category:Accessibility "Category:Accessibility")
*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [Install from SSH](/index.php/Install_from_SSH "Install from SSH")
*   [General recommendations](/index.php/General_recommendations "General recommendations")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Úvod](#Úvod)
    *   [1.1 Predstavenie](#Predstavenie)
    *   [1.2 Licencia](#Licencia)
    *   [1.3 The Arch Way](#The_Arch_Way)
    *   [1.4 O tomto sprievodcovi](#O_tomto_sprievodcovi)

## Úvod

### Predstavenie

Vitajte. Tento dokument vás prevedie procesom inštalácie [Arch Linux-u](/index.php/Arch_Linux "Arch Linux"); jednoduchej, na hardvér nenáročnej Linuxovej distribúcie cielenej na kompetentných používateľov. Tento sprievodca je zacielený na nových používateľov, ale snaží sa slúžiť ako referencia a informatívny základ pre všetkých.

Pred inštaláciou je dobré prezrieť si [FAQ](/index.php/FAQ "FAQ").

**Hlavné myšlienky distribúcie Arch Linux**

*   [Jednoduchý](/index.php/The_Arch_Way_(Slovensk%C3%BD) "The Arch Way (Slovenský)") dizajn a filozofia
*   [Všetky softvérové balíky](https://www.archlinux.org/packages/?q=) kompilované pre architektúry i686 a x86_64
*   Init skripty na [BSD štýl](/index.php/Arch_boot_process "Arch boot process"), používajúce jeden centralizovaný konfiguračný súbor
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"): Jednoduchý a dynamický skript na vytváranie initramfs
*   [Pacman](/index.php/Pacman "Pacman") správca balíkov je nenáročný a agilný a používa málo pamäte
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System"): Ports-inšpirovaný systém pre kompilovanie balíkov, poskytujúci jednoduchý framework pre vytváranie inštalovateľných Arch balíkov zo zdrojového kódu
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"): poskytuje tisícky build scriptov poskytnuté užívateľmi a príležitosť zdieľať vaše vlastné

### Licencia

Arch Linux, pacman, dokumentácia, a skripty sú chránené copyrightom ©2002-2007 by Judd Vinet, ©2007-2011 by Aaron Griffin a sú licencované [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### The Arch Way

***Dizajnové princípy za Arch Linux-om sú zacielené na [jednoduchosť](/index.php/The_Arch_Way "The Arch Way").***

'Jednoduchý', v tomto kontexte, znamená 'bez zbytočných prídavkov, modifikácií, alebo komplikácií. V skratke: elegantný, minimalistický prístup.

**Zopár myšlienok keď uvažujeme o jednoduchosti:**

*   *" 'Jednoduchý' je definované z technického pohľadu, nie pohľadu používania. Je lepšie byť technicky elegantný s náročnejším procesom učenia sa, ako byť jednoduchý na používanie a technicky [na horšej úrovni]." -Aaron Griffin*
*   *Entia non sunt multiplicanda praeter necessitatem* alebo "Entity by nemali byť zbytočne viacnásobné." -Occamova britva. Termín *britva* referuje na zbavenie sa zbytočných komplikácií, aby sa dospelo k tomu najjednoduchšiemu vysvetleniu, metóde alebo teórii.
*   *"Tá výnimočná súčasť [mojej metódy] je jej jednoduchosť."* - Bruce Lee

### O tomto sprievodcovi

Komunitou spravovaná [Arch Wiki](/index.php/Main_page_(Slovensk%C3%BD) "Main page (Slovenský)") je vynikajúci zdroj informácií a mala by byť prvým miestom kde hľadať odpovede. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), a [[1]](https://bbs.archlinux.org/forums) sú taktiež dostupné ak riešenie problému nie je dostupné inde. Taktiež určite používajte `man` stránky pre akýkoľvek príkaz, ktorý dobre nepoznáte; tieto obvykle zobrazí príkaz `man *príkaz*`.

**Note:** Presné nasledovanie tohto sprievodcu je potrebné pre úspešnú inštaláciu Arch Linux-u, takže *prosím* prečítajte si ho poriadne. Je odporúčané kompletne prečítať celú sekciu <u>predtým</u> ako vykonáte obsiahnuté inštrukcie.

Tento sprievodca je rozdelený do 3 hlavných častí:

*   [Časť I: Príprava inštalácie](/index.php/Beginners%27_Guide/Preparation "Beginners' Guide/Preparation")
*   [Časť II: Inštalácia základného systému](/index.php/Beginners%27_Guide/Installation "Beginners' Guide/Installation")
*   [Časť III: Po inštalácii](/index.php/Beginners%27_Guide/Post-Installation "Beginners' Guide/Post-Installation")