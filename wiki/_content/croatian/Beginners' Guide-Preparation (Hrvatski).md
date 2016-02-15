**Tip:** Ovo je dio višestraničnog članka vodiča za početnike. **[Klikni ovdje](/index.php/Beginners%27_Guide_(Hrvatski) "Beginners' Guide (Hrvatski)")** ukoliko želiš pročitati vodič u cijelosti.

## Contents

*   [1 Priprema](#Priprema)
    *   [1.1 Dohvati najnoviji instalacijski medij](#Dohvati_najnoviji_instalacijski_medij)
        *   [1.1.1 Instaliraj putem mreže](#Instaliraj_putem_mre.C5.BEe)
        *   [1.1.2 CD instalator](#CD_instalator)
        *   [1.1.3 Flash-memorija odnosno USB-disk](#Flash-memorija_odnosno_USB-disk)
            *   [1.1.3.1 *nix metoda](#.2Anix_metoda)
    *   [1.2 Bootaj instalator Arch Linuxa](#Bootaj_instalator_Arch_Linuxa)
        *   [1.2.1 Bootaj s medija](#Bootaj_s_medija)
        *   [1.2.2 Dizanje operacijskog sustava](#Dizanje_operacijskog_sustava)
        *   [1.2.3 Izmjena rasporeda tipaka](#Izmjena_rasporeda_tipaka)
        *   [1.2.4 Dokumentacija](#Dokumentacija)

## Priprema

**Note:** Ako želiš instalirati na drugu particiju unutar postojeće distribucije GNU/Linuxa ili interaktivnog CD-okruženja, pogledaj [ovaj wiki članak](/index.php?title=Install_from_Existing_Linux_(Hrvatski)&action=edit&redlink=1 "Install from Existing Linux (Hrvatski) (page does not exist)"). To može biti korisno pogotovo ako želiš instalirati Arch putem VNC-a ili SSH-a s udaljenog računala. Idući tekst pretpostavlja konvencionalan način instalacije.

### Dohvati najnoviji instalacijski medij

Može dohvatiti službeni instalacijski medij Arch Linuxa [ovdje](https://archlinux.org/download/).

*   I jezgrena (lokalna, Core) i mrežna (Netinstall) CD-slika pruža samo pakete potrebne za stvaranje **osnovnog sustava Arch Linux**. _Primijeti da osnovni sustav ne sadrži grafičko sučelje, već se sastoji samo od niza GNU-alata (kompilator, asembler, linker, biblioteke, ljuska i korisnički programi), Linux-kernela, pacmana (Archevog upravitelja paketima) i nekoliko dodatnih biblioteka i modula._
*   Jezgrene slike se mogu koristiti i za lokalnu i mrežnu instalaciju.
*   Mrežne slike su manje i ne sadrže ikakve pakete; cijeli se sustav dohvaća putem Interneta.
*   [Često postavljena pitanja o Arch64](/index.php?title=Arch64_FAQ_(Hrvatski)&action=edit&redlink=1 "Arch64 FAQ (Hrvatski) (page does not exist)") ti mogu pomoći da se odlučiš između 32 i 64-bitnih verzija. CD s dualnom arhitekturom sadrži pakete za obje arhitekture tako da ga možeš koristiti za instalaciju Archa i na 32 i na 64-bitnim računalima.

#### Instaliraj putem mreže

Umjesto zapisivanja boot-medija na optički disk ili USB-disk, alternativno možeš bootati ISO-sliku putem mreže. Ovo funkcionira najbolje ako već imaš postavljen server. Pogledaj [ovaj članak](/index.php?title=Install_Arch_from_network_(via_PXE)_(Hrvatski)&action=edit&redlink=1 "Install Arch from network (via PXE) (Hrvatski) (page does not exist)") za više informacija, a zatim nastavi na [bootanje instalatora Arch Linuxa](#Bootaj_instalator_Arch_Linuxa).

#### CD instalator

Sprži ISO-sliku na CD ili DVD-medij te zatim nastavi na [bootanje instalatora Arch Linuxa](#Bootaj_instalator_Arch_Linuxa).

**Note:** Kvaliteta optičkih pogona i medija jako varira. Korištenje spore brzine zapisivanja na medij je preporučeno za pouzdan prijenos informacija bez grešaka. Mnogi korisnici preporučuju brzine malene poput 4x ili 2x. Ako imaš problema s čitanjem medija, pokušaj pržiti ISO-sliku na najmanjoj mogućoj brzini koju tvoj sustav podržava.

#### Flash-memorija odnosno USB-disk

Pogledaj [instaliranje s USB-diska](/index.php?title=Install_from_a_USB_flash_drive_(Hrvatski)&action=edit&redlink=1 "Install from a USB flash drive (Hrvatski) (page does not exist)") za detaljnije informacije.

Ova metoda će raditi s bilo kojim tipom flash-medija kojeg ti BIOS podržava, bilo da se radi o čitaču kartica ili USB-portu.

Primijeti da će svi podaci sa prijenosnog medija biti zauvijek izbrisani!

##### *nix metoda

**Warning:** Valja oprezno odabrati odredište zapisa ISO-slike, jer će `dd` bez ikakvih problema zapisivati na bilo koje odredište koje mu daš, čak i ako je to tvoj hard disk (što može dovesti to potencijalnog gubitka podataka ili korupcije datotečnog sustava).

Ubaci flash-uređaj u računalo, otkrij put koji vodi do njega i zapiši ISO-sliku tamo koristeći program `dd`:

 `# dd if=archlinux-2011.08.19-''{core|netinstall}''-''{i686|x86_64|dual}''.iso of=/dev/sd''x''` 

gdje je `if=` put do ISO-slike i `of=` tvoj flash-uređaj. Pobrini se da koristiš `/dev/sd**x**`, a ne `/dev/sd**x1**`. Bit će ti potreban flash-uređaj dovoljno velikog kapaciteta da na njega može stati ISO-slika.

Za provjeru da je slika uspješno zapisana na uređaj, zapamti broj blokova koji je pročitan i zapisan te učini iduće:

 ` # dd if=/dev/sd''x'' count=''broj_blokova'' status=noxfer | md5sum` 

Vraćeni md5sum bi trebao biti identičan [md5sumi skinute archlinux slike (2011.08.19)](https://www.archlinux.org/iso/2011.08.19/md5sums.txt); oba bi trebala biti identična md5sumi slike navedenoj u md5sums datoteci. Tipično će sve to izgledati ovako:

Zapiši ISO na uređaj:

 `$ [sudo] dd if=archlinux-2011.08.19-core-i686.iso of=/dev/sdc` 

```
 744973+0 records in
 744973+0 records out
 381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s

```

Provjeri je li sve uspješno zapisano:

 `$ [sudo] dd if=/dev/sdc count=744973 status=noxfer | md5sum` 

```
 4850d533ddd343b80507543536258229  -
 744973+0 records in
 744973+0 records out
```

Nastavi s [bootanjem instalatora Arch Linuxa](#Bootaj_instalator_Arch_Linuxa).

### Bootaj instalator Arch Linuxa

**Tip:** Memorijski zahtjevi za običnu instalaciju su 64MB RAM-a.

**Tip:** Tijekom procesa, automatski brisač ekrana se možda upali. U tom slučaju možeš pritisnuti Alt tipku da bi bez opasnosti vratio natrag uobičajeni ekran.

#### Bootaj s medija

Ubaci pripremljeni CD ili flash-medij i bootaj s njega. Možda ćeš trebati promijeniti redoslijed boot izvora u BIOS-u računala. To se obično radi tako da prilikom BIOS POST (Power On Self-Test) faze pritisneš ključnu tipku (poput DEL, F1, F2, F11 ili F12).

**Main Menu:** Glavni meni bi sada trebao biti prikazan. Odaberi svoj izbor tako da koristiš tipke sa strelicama i tipku [Enter]. Meniji malčice variraju ovisno o korištenoj ISO-slici.

#### Dizanje operacijskog sustava

Odaberi "Boot Arch Linux" iz glavnog menija i pritisni [Enter] kako bi instalacija započela. Sustav će sada učitati i prikazati naredbeni redak ljuske. Automatski ćeš biti u ulozi administratorskog korisnika _root_.

**Note:** Korisnici koji žele instalaciju Arch Linuxa napraviti putem SSH-konekcije s udaljenog računala sada mogu napraviti neke male izmjene kako bi omogućili direktne SSH-konekcije u interaktivno CD-okruženje. Ako te to zanima, pogledaj [ovaj članak](/index.php?title=Install_from_SSH_(Hrvatski)&action=edit&redlink=1 "Install from SSH (Hrvatski) (page does not exist)").

Ako koristiš Intel video čipset i ekran postane prazan tijekom procesa bootanja, problem je najvjerojatnije postavka moda kernela. Moguće rješenje je rebootanje i pritisak <Tab> tipke na GRUB-meniju da bi omogućio kernel-opcije. Na kraj linije kernela dodaj jedan prazan znak [space] i zatim:

```
i915.modeset=0

```

Alternativno, dodaj:

```
video=SVIDEO-1:d

```

Nakon te izmjene, jednostavno pritisni [Enter] da bi bootanje s tim izmjenama započelo.

Pogledaj [članak o Intelu](/index.php?title=Intel_(Hrvatski)&action=edit&redlink=1 "Intel (Hrvatski) (page does not exist)") za više informacija.

#### Izmjena rasporeda tipaka

Ako želiš koristiti hrvatski raspored tipaka (ili neki drugi koji nije SAD-ov), možeš interaktivno odabrati svoj raspored i font konzole idućom naredbom:

 `# km` 

ili možeš koristiti loadkey naredbu:

 `# loadkeys _raspored_` 

gdje je _raspored_ raspored tvoje tipkovnice poput `hr` ili `be-latin1`.

#### Dokumentacija

Službeni vodič za instalaciju se nalazi odmah na interaktivnom sustavu! Možeš mu pristupiti tako da skočiš na drugu virtualnu konzolu (<ALT>+F2), ulogiraš se kao root i zatim izvršiš naredbu `/usr/bin/less` upisujući sljedeće:

 `# less /usr/share/aif/docs/official_installation_guide_en` 

`less` će ti omogućiti da listaš kroz dokument.

Promijeni natrag na tty1 s <ALT>+F1 da bi pratio ostatak instalacijskog procesa. (Skoči natrag na tty2 bilo kada ako želiš pogledati službeni vodič tijekom procesa instalacije.)

**Tip:** Valja primijetiti da službeni vodič pokriva samo instalaciju i konfiguraciju osnovnog sustava. Nakon što je to instalirano, preporučamo da se vratiš natrag na wiki i čitaš o tome kako nastaviti.

**[Vodič za početnike](/index.php/Beginners%27_Guide_(Hrvatski) "Beginners' Guide (Hrvatski)")**

* * *

[Predgovor](/index.php/Beginners%27_Guide/Preface_(Hrvatski) "Beginners' Guide/Preface (Hrvatski)") >> **Priprema** >> [Instalacija](/index.php/Beginners%27_Guide/Installation_(Hrvatski) "Beginners' Guide/Installation (Hrvatski)") >> [Nakon instalacije](/index.php/Beginners%27_Guide/Post-Installation_(Hrvatski) "Beginners' Guide/Post-Installation (Hrvatski)") >> [Bilješke](/index.php/Beginners%27_Guide/Extra_(Hrvatski) "Beginners' Guide/Extra (Hrvatski)")