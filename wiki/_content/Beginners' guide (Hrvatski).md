# Beginners' guide (Hrvatski)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**Tip:** Ovaj je vodič dostupan još i u verziji sa više individualnih stranica. Ako ga želite pratiti na taj način, započnite sa vodičem za početnike **[ovdje](/index.php/Beginners%27_Guide/Preface_(Hrvatski) "Beginners' Guide/Preface (Hrvatski)")**.

<table style="margin-left: 5px; padding: 5px; border-spacing: 0px 4px; float: right; clear: right; width: 25%;" cellpadding="0">

<tbody>

<tr style="text-align: center; border-bottom: 5px #08c solid;">

<th style="background: #333; color: white; padding: 3px;">**Summary** <sup>[help replacing me](/index.php/Help_talk:Style/Article_summary_templates#Replacing_Article_summaries_with_Related_articles "Help talk:Style/Article summary templates")</sup></th>

</tr>

<tr>

<td style="text-align: left; padding: 3px">Pruža vrlo detaljan vodič kroz instalaciju, konfiguraciju i korištenje potpuno funkcionalnog sustava Arch Linux.</td>

</tr>

<tr style="text-align: center; height: 1.5em; border-bottom: 5px #08c solid;">

<th style="background: #333; color: white; padding: 2px;">**Povezano**</th>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[Category:Accessibility (Hrvatski)](/index.php?title=Category:Accessibility_(Hrvatski)&action=edit&redlink=1 "Category:Accessibility (Hrvatski) (page does not exist)")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[Official Arch Linux Install Guide (Hrvatski)](/index.php?title=Official_Arch_Linux_Install_Guide_(Hrvatski)&action=edit&redlink=1 "Official Arch Linux Install Guide (Hrvatski) (page does not exist)")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[Install from SSH (Hrvatski)](/index.php?title=Install_from_SSH_(Hrvatski)&action=edit&redlink=1 "Install from SSH (Hrvatski) (page does not exist)")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[General Recommendations (Hrvatski)](/index.php?title=General_Recommendations_(Hrvatski)&action=edit&redlink=1 "General Recommendations (Hrvatski) (page does not exist)")</td>

</tr>

<tr>

<td style="text-align: left; padding: 3px">[General Troubleshooting (Hrvatski)](/index.php?title=General_Troubleshooting_(Hrvatski)&action=edit&redlink=1 "General Troubleshooting (Hrvatski) (page does not exist)")</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Predgovor](#Predgovor)
    *   [1.1 Uvod](#Uvod)
    *   [1.2 Licenca](#Licenca)
    *   [1.3 Put Archa](#Put_Archa)
    *   [1.4 O ovom vodiču](#O_ovom_vodi.C4.8Du)
*   [2 Priprema](#Priprema)
    *   [2.1 Dohvati najnoviji instalacijski medij](#Dohvati_najnoviji_instalacijski_medij)
        *   [2.1.1 Instaliraj putem mreže](#Instaliraj_putem_mre.C5.BEe)
        *   [2.1.2 CD instalator](#CD_instalator)
        *   [2.1.3 Flash-memorija odnosno USB-disk](#Flash-memorija_odnosno_USB-disk)
            *   [2.1.3.1 *nix metoda](#.2Anix_metoda)
    *   [2.2 Bootaj instalator Arch Linuxa](#Bootaj_instalator_Arch_Linuxa)
        *   [2.2.1 Bootaj s medija](#Bootaj_s_medija)
        *   [2.2.2 Dizanje operacijskog sustava](#Dizanje_operacijskog_sustava)
        *   [2.2.3 Izmjena rasporeda tipaka](#Izmjena_rasporeda_tipaka)
        *   [2.2.4 Dokumentacija](#Dokumentacija)
*   [3 Instalacija](#Instalacija)
    *   [3.1 Odaberi instalacijski izvor](#Odaberi_instalacijski_izvor)
        *   [3.1.1 Konfiguriraj mrežu (mrežna instalacija)](#Konfiguriraj_mre.C5.BEu_.28mre.C5.BEna_instalacija.29)
            *   [3.1.1.1 Postavi ADSL most u interaktivnom okruženju (neobavezno)](#Postavi_ADSL_most_u_interaktivnom_okru.C5.BEenju_.28neobavezno.29)
            *   [3.1.1.2 Postavi bežičnu mrežu unutar interaktivnog okruženja (neobavezno)](#Postavi_be.C5.BEi.C4.8Dnu_mre.C5.BEu_unutar_interaktivnog_okru.C5.BEenja_.28neobavezno.29)
    *   [3.2 Postavi hardversko vrijeme](#Postavi_hardversko_vrijeme)
        *   [3.2.1 Dual boot](#Dual_boot)
    *   [3.3 Pripremi tvrdi disk](#Pripremi_tvrdi_disk)
        *   [3.3.1 Particioniranje tvrdih diskova (opće informacije)](#Particioniranje_tvrdih_diskova_.28op.C4.87e_informacije.29)
            *   [3.3.1.1 Tip particije](#Tip_particije)
            *   [3.3.1.2 Swap particija](#Swap_particija)
            *   [3.3.1.3 Particijski raspored](#Particijski_raspored)
            *   [3.3.1.4 Koliko velike moraju biti moje particije?](#Koliko_velike_moraju_biti_moje_particije.3F)
        *   [3.3.2 Ručno particioniranje tvrdog diska (pomoću cfdisk)](#Ru.C4.8Dno_particioniranje_tvrdog_diska_.28pomo.C4.87u_cfdisk.29)
        *   [3.3.3 Creating filesystems (general information)](#Creating_filesystems_.28general_information.29)
            *   [3.3.3.1 Filesystem types](#Filesystem_types)
            *   [3.3.3.2 A note on journaling](#A_note_on_journaling)
        *   [3.3.4 Manually configure block devices, filesystems and mountpoints](#Manually_configure_block_devices.2C_filesystems_and_mountpoints)
    *   [3.4 Select Packages](#Select_Packages)
    *   [3.5 Install Packages](#Install_Packages)
    *   [3.6 Configure the System](#Configure_the_System)
        *   [3.6.1 Can the installer handle this more automatically?](#Can_the_installer_handle_this_more_automatically.3F)
        *   [3.6.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [3.6.2.1 LOCALIZATION section](#LOCALIZATION_section)
            *   [3.6.2.2 HARDWARE section](#HARDWARE_section)
            *   [3.6.2.3 NETWORKING section](#NETWORKING_section)
            *   [3.6.2.4 DAEMONS section](#DAEMONS_section)
                *   [3.6.2.4.1 General information](#General_information)
        *   [3.6.3 /etc/fstab](#.2Fetc.2Ffstab)
        *   [3.6.4 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
        *   [3.6.5 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [3.6.6 /etc/resolv.conf](#.2Fetc.2Fresolv.conf)
        *   [3.6.7 /etc/hosts](#.2Fetc.2Fhosts)
        *   [3.6.8 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [3.6.9 Pacman Mirror](#Pacman_Mirror)
        *   [3.6.10 Root password](#Root_password)
        *   [3.6.11 Done](#Done)
    *   [3.7 Install Bootloader](#Install_Bootloader)
    *   [3.8 Reboot](#Reboot)
*   [4 Nakon instalacije](#Nakon_instalacije)
    *   [4.1 Nadogradnja](#Nadogradnja)
        *   [4.1.1 Configure the network (if necessary)](#Configure_the_network_.28if_necessary.29)
            *   [4.1.1.1 Wired LAN](#Wired_LAN)
            *   [4.1.1.2 Wireless LAN](#Wireless_LAN)
            *   [4.1.1.3 Proxy Server](#Proxy_Server)
            *   [4.1.1.4 Analog Modem, ISDN, and DSL (PPPoE)](#Analog_Modem.2C_ISDN.2C_and_DSL_.28PPPoE.29)
        *   [4.1.2 Update, Sync, and Upgrade the system with pacman](#Update.2C_Sync.2C_and_Upgrade_the_system_with_pacman)
            *   [4.1.2.1 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
            *   [4.1.2.2 Package Repositories](#Package_Repositories)
            *   [4.1.2.3 AUR](#AUR)
        *   [4.1.3 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
        *   [4.1.4 rankmirrors](#rankmirrors)
            *   [4.1.4.1 Mirrorcheck for up-to-date packages](#Mirrorcheck_for_up-to-date_packages)
        *   [4.1.5 Get familiar with pacman](#Get_familiar_with_pacman)
        *   [4.1.6 Update the System](#Update_the_System)
            *   [4.1.6.1 Ignoring Packages](#Ignoring_Packages)
            *   [4.1.6.2 The Arch rolling release model](#The_Arch_rolling_release_model)
    *   [4.2 Adding a User](#Adding_a_User)
        *   [4.2.1 Deleting the user account](#Deleting_the_user_account)
*   [5 Extras](#Extras)
    *   [5.1 Create DVD and CDROM symlinks](#Create_DVD_and_CDROM_symlinks)
    *   [5.2 Sudo](#Sudo)
    *   [5.3 Sound](#Sound)
    *   [5.4 **G**raphical **U**ser **I**nterface](#Graphical_User_Interface)
        *   [5.4.1 Install X](#Install_X)
        *   [5.4.2 Install video driver](#Install_video_driver)
            *   [5.4.2.1 NVIDIA Graphics Cards](#NVIDIA_Graphics_Cards)
            *   [5.4.2.2 ATI Graphics Cards](#ATI_Graphics_Cards)
        *   [5.4.3 Install input drivers](#Install_input_drivers)
        *   [5.4.4 Configure X (Optional)](#Configure_X_.28Optional.29)
            *   [5.4.4.1 Non-US keyboard](#Non-US_keyboard)
        *   [5.4.5 Testing X](#Testing_X)
            *   [5.4.5.1 Message bus](#Message_bus)
            *   [5.4.5.2 Start X](#Start_X)
            *   [5.4.5.3 In case of errors](#In_case_of_errors)
            *   [5.4.5.4 Need Help?](#Need_Help.3F)
        *   [5.4.6 Install Fonts](#Install_Fonts)
        *   [5.4.7 Choose and install a graphical interface](#Choose_and_install_a_graphical_interface)
        *   [5.4.8 Methods for starting your Graphical Environment](#Methods_for_starting_your_Graphical_Environment)
            *   [5.4.8.1 Manually](#Manually)
            *   [5.4.8.2 Automatically](#Automatically)
*   [6 Bilješke](#Bilje.C5.A1ke)

## Predgovor

### Uvod

Dobrodošli! Ovaj vodič će te voditi kroz proces instalacije sustava [Arch Linux](/index.php/Arch_Linux_(Hrvatski) "Arch Linux (Hrvatski)"): jednostavne distribucije [GNU](/index.php?title=GNU_Project_(Hrvatski)&action=edit&redlink=1 "GNU Project (Hrvatski) (page does not exist)")/Linuxa stvorene za sposobne korisnike. Vodičem se cilja na nove Arčere, ali se pokušava i stvoriti snažna informacijska podloga za sve korisnike.

Prije instalacije bi bilo dobro proletjeti kroz [često postavljena pitanja](/index.php/FAQ_(Hrvatski) "FAQ (Hrvatski)").

**Istaknimo neke značajke distribucije Arch Linuxa:**

*   [Jednostavan](/index.php/The_Arch_Way_(Hrvatski) "The Arch Way (Hrvatski)") dizajn i filozofija
*   [Svi paketi](https://www.archlinux.org/packages/?q=) su kompilirani i za [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") i za [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") arhitekture
*   Inicijalizacijske skripte u [BSD stilu](/index.php?title=Arch_Boot_Process_(Hrvatski)&action=edit&redlink=1 "Arch Boot Process (Hrvatski) (page does not exist)"), koristeći jednu centraliziranu konfiguracijsku datoteku
*   [mkinitcpio (Hrvatski)](/index.php?title=Mkinitcpio_(Hrvatski)&action=edit&redlink=1 "Mkinitcpio (Hrvatski) (page does not exist)") je jednostavan i dinamičan stvaraoc [initramfsa](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Upravitelj paketima](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") imena [Pacman (Hrvatski)](/index.php?title=Pacman_(Hrvatski)&action=edit&redlink=1 "Pacman (Hrvatski) (page does not exist)") je agilan i lak kao perce, s vrlo skromnim zauzećem memorije
*   [Paketni sustav Archa](/index.php?title=Arch_Build_System_(Hrvatski)&action=edit&redlink=1 "Arch Build System (Hrvatski) (page does not exist)"): sustav stvaranja paketa koji pruža jednostavnu okolinu za stvaranje instalacijskih Arch paketa putem izvornog koda
*   [Korisnički repozitorij Archa](/index.php?title=Arch_User_Repository_(Hrvatski)&action=edit&redlink=1 "Arch User Repository (Hrvatski) (page does not exist)"): pruža tisuće i tisuće korisničkih instalacijskih skripti te priliku za dijeljenje vlastitih

### Licenca

Arch Linux, pacman, documentation, and scripts are Copyright © 2002-2007 by Judd Vinet, Copyright © 2007-2011 by Aaron Griffin and are licensed under the [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### Put Archa

_**Principi dizajna Archa su tu da ga održe [jednostavnim](/index.php/The_Arch_Way_(Hrvatski) "The Arch Way (Hrvatski)").**_

'Jednostavan', u ovom kontekstu, znači 'bez nepotrebnih dodataka, modifikacija ili komplikacija'. Ukratko: elegantan, minimalistički pristup.

**Tijekom razmišljanja o jednostavnosti valja imati na umu:**

*   _" 'Jednostavnost' je definirana iz tehničkog gledišta, a ne korisničkog. Bolje je biti tehnički elegantan uz veće zahtjeve znanja nego biti jednostavan za koristiti i tehnički [inferioran]." -Aaron Griffin_
*   _Entia non sunt multiplicanda praeter necessitatem_ ili "Entiteti se ne bi smjeli nepotrebno množiti." -Occamova oštrica. Pojam _oštrica_ odnosi se na čin uklanjanja nepotrebnih komplikacija da bi se stiglo do najjednostavnijeg objašnjenja, metode ili teorije.
*   _"Nevjerojatnost [moje metode] leži u njenoj jednostavnosti. Visine uglađenosti uvijek vode ka jednostavnosti."_ - Bruce Lee

### O ovom vodiču

[Arch wiki](/index.php/Main_Page_(Hrvatski) "Main Page (Hrvatski)") je održavan putem zajednice te je odličan izvor s kojim se uvijek može pokušati konzultirati pri prvim suočavanjem s nekim problemom. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanal ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) i [forumi](https://bbs.archlinux.org/) su isto dostupni ukoliko se traženi odgovor ne može naći igdje drugdje. Svakako provjeri i `man` stranice bilo koje naredbe s kojom imaš problema; to se obično može učiniti pozivanjem `man _naredbe_`.

**Note:** Usko pratiti ovaj vodič od ključne je važnosti kako bi se moglo doći do ispravno konfiguriranog sustava Arch Linux, tako da ga valja pročitati temeljito. Preporuča se pročitati svaki sekciju u potpunosti <u>prije</u> implementacije koraka navedenih u njoj.

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

## Instalacija

**Note:** Ukoliko pristupaš Internetu putem HTTP ili FTP posrednika te istovremeno želiš koristiti DHCP za konfiguraciju mrežnog sučelja, možda ćeš unutar ljuske morati postaviti varijable okruženja `http_proxy` i/ili `ftp_proxy` prije pokretanja `/arch/setup` kao što je navedeno niže:

```
export http_proxy=http://<http_adresa_posrednika>:<port_posrednika>
export ftp_proxy=ftp://<ftp_adresa_posrednika>:<port_posrednika>
```

Kao root, pokreni instalacijsku skriptu s početne virtualne konzole tty1:

 `# /arch/setup` 

Na ekranu bi se trebalo prikazati instalacijsko okruženje Arch Linuxa.

### Odaberi instalacijski izvor

Nakon pozdrava dobrodošlice, od tebe će se tražiti instalacijski izvor. Odaberi prikladan izvor za željeni tip instalacije. Ukoliko koristiš medij za mrežnu instalaciju (Netinstall), brzine i stanja zrcalnih repozitorija možeš provjeriti [ovdje](https://www.archlinux.de/?page=MirrorStatus).

*   Ukoliko odabereš jezgrenu instalaciju i želiš koristiti pakete s CD-a, odaberi CD-ROM kao izvor instalacije.
*   Alternativno, ili ukoliko koristiš medij za mrežnu instalaciju, odaberi NET i pogledaj sekciju [Konfiguriraj mrežu](#Configure_Network_.28Netinstall.29).

Dijalog odabira izvora će te zatražiti da odabereš repozitorije koje želiš koristiti. U slučaju nedoumice, uz 'core' odaberi 'extra' i 'community' repozitorije. U slučaju da koristiš 64-bitnu instalaciju Archa, za kompatibilnost s nekim 32-bitnim softverom ćeš možda još htjeti uključiti i '[multilib](/index.php/Multilib "Multilib")' repozitorij.

**Warning:** Samo uključi 'testing' repozitorije ukoliko znaš što radiš - korištenje tih repozitorija često stvara probleme. U tom slučaju moraš znati kako unazaditi verzije paketa i ući u svoju Arch instalaciju koristeći interaktivni CD.

#### Konfiguriraj mrežu (mrežna instalacija)

Imat ćeš priliku ručno učitati mrežne drivere, ukoliko to želiš. UDev je sposoban učitati potrebne module, pa možeš prepostaviti da je to već učinio. Možeš to provjeriti pritiskanjem <Alt>+F3 i pokretanjem **ip addr**. Kada je to gotovo, vrati se na početnu virtualnu konzolu tty1 pritiskom na <Alt>+F1.

Na idućem ekranu odaberi postavljanje mrežnih opcija _Setup Network_. Bit će prikazana dostupna sučelja. Ukoliko je navedeno sučelje i HWaddr (**H**ard**W**are **addr**ess), tada je tvoj modul već učitan. Ukoliko sučelje nije navedeno, možeš ga pokrenuti unutar instalacije ili ručno putem druge virtualne konzole. Odaberi svoje sučelje za nastavak.

Instalacija će te zatim upitati želiš li koristiti DHCP. Odabiranjem "Yes" će se pokrenuti **dhcpcd** da otkrije dostupan gateway i zatraži IP-adresu; odabiranjem "No" ćeš morati ručno upisati mrežne postavke poput IP-adrese, maske i DNS-servera. Nakon toga se vraćaš u instalacijski meni mrežne instalacije _Net Installation Menu_.

Odaberi _Choose Mirror_ te odaberi FTP ili HTTP zrcalni repozitorij. Zatim se vrati na glavni meni.

**Tip:** Za postizanje najvećih brzina skidanja podataka, valja odabrati zrcalne repozitorije koji su unutar zemlje u kojoj se nalaziš i koji se serviraju putem poslužitelja za koje znaš da su pouzdani (poput sveučilišta).

**Note:** ftp.archlinux.org je ograničen na 50KB/s i stoga ga valja izbjegavati.

##### Postavi ADSL most u interaktivnom okruženju (neobavezno)

(Samo ukoliko imaš modem ili usmjeritelj u mostovnom modu rada za spajanje na svog Internet-poslužitelja.)

Skoči na drugu virtualnu konzolu (<Alt>+F2), ulogiraj se kao root i pokreni:

 `# pppoe-setup` 

Ako je sve dobro konfigurirano, na kraju ćeš se moći spojiti na svojeg Internet-poslužitelja idućim programom:

 `# pppoe-start` 

Vrati se na prvu virtualnu konzolu (<ALT>+F1) te nastavi s [postavljanjem vremena](#Postavi_hardversko_vrijeme).

##### Postavi bežičnu mrežu unutar interaktivnog okruženja (neobavezno)

(Samo ukoliko ti je potrebna bežična mreža za nastavak instalacijskog procesa.)

Driveri i uslužni programi za bežičnu mrežu su sada dostupni unutar interaktivnog okruženja instalacijskog medija. Dobro poznavanje bežičnog hardvera će biti ključno za uspješnu konfiguraciju. Primijeti da će iduća brzinska procedura, pokrenuta _na ovoj točci instalacije_, inicijalizirati tvoj bežični hardver samo tako da bude mogao biti korišten _tijekom instalacijskog procesa_. Čitavu ćeš proceduru (ili neku sličnu njoj) morati ponoviti jednom kada zaista instaliraš i pokreneš lokalni sustav.

Primijeti i da su ovi koraci neobavezni ukoliko bežična konekcija nije potrebna: bežičnu funkcionalnost uvijek možeš uključiti kasnije.

**Note:** Idući primjeri koriste wlan0 kao sučelje i "linksys" kao ESSID. Nemoj ih zaboraviti izmijeniti ovisno o svojoj konkretnoj situaciji.

Osnovna je procedura ovakva:

*   Prebaci se na slobodnu virtualnu konzolu, npr. <ALT>+F3
*   Ulogiraj se kao root
*   (neobavezno) Saznaj koje bežično sučelje koristiš:

```
# lspci | grep -i net

```

*   Pobrini se da je udev učitao driver i da je driver stvorio iskoristivo bežično kernel-sučelje `/usr/sbin/iwconfig`:

 `# iwconfig` 

```
 lo no wireless extensions.
 eth0 no wireless extensions.
 wlan0    unassociated  ESSID:""
          Mode:Managed  Channel=0  Access Point: Not-Associated
          Bit Rate:0 kb/s   Tx-Power=20 dBm   Sensitivity=8/0
          Retry limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

`wlan0` je dostupno bežično sučelje u ovom primjeru.

**Note:** Ako ne vidiš ispis sličan ovome, tada tvoj bežični driver nije učitan. Ako je to slučaj, morat ćeš učitati driver ručno. Pogledaj [postavljanje bežične mreže](/index.php?title=Wireless_Setup_(Hrvatski)&action=edit&redlink=1 "Wireless Setup (Hrvatski) (page does not exist)") za više informacija.

*   Pokreni sučelje s:

 `# ip link set wlan0 up` 

Malen postotak bežičnih čipseta zahtijevaju i firmware zajedno s odgovarajućim driverom. Ako bežični čipset zahtijeva firmware, vjerojatno ćeš prilikom pokretanja sučelja primiti ovakvu grešku:

 `# ip link set wlan0 up`  `SIOCSIFFLAGS: No such file or directory` 

U slučaju nedoumice, pokreni `/usr/bin/dmesg` da bi potražio zahtjev za firmwareom unutar dnevnika kernela. Primjer ispisa od Intelovog čipseta koji zahtijeva firmware od kernela prilikom pokretanja sustava:

 `$ dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Ako nema takvog ispisa, može se zaključiti da bežični čipset sustava ne zahtijeva firmware.

**Note:** Paketi firmwarea bežičnih čipseta (za kartice koje ih zahtijevaju) su već instalirane u /lib/firmware unutar interaktivne CD-okoline **ali moraju biti eksplicitno instalirani na tvoj stvarni sustav kako bi pružili bežičnu funkcionalnost nakon što ga resetiraš!** Izbor paketa i instalacija je obrađena kasnije u ovom vodiču. Pobrini se da instaliraš i bežični modul i bežični firmware prilikom koraka odabiranja paketa! Pogledaj [postavljanje bežične mreže](/index.php?title=Wireless_Setup_(Hrvatski)&action=edit&redlink=1 "Wireless Setup (Hrvatski) (page does not exist)") u slučaju nedoumica o tome zahtijeva li tvoj čipset instalaciju firmwarea ili ne. To je vrlo čest izvor greški.

*   Ako je ESSID zaboravljen ili nepoznat, iskoristi `/sbin/iwlist <interface> scan` da bi pretražio obližnje mreže:

 `# iwlist wlan0 scan` 

```
Cell 01 - Address: 04:25:10:6B:7F:9D
                    Channel:2
                    Frequency:2.417 GHz (Channel 2)
                    Quality=31/70  Signal level=-79 dBm  
                    Encryption key:off
                    ESSID:"dlink"
                    Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s
                    Bit Rates:6 Mb/s; 9 Mb/s; 12 Mb/s; 18 Mb/s; 24 Mb/s
                              36 Mb/s; 48 Mb/s; 54 Mb/s

```

*   Ako koristiš WPA enkripciju:

Koristiti WPA enkripciju zahtijeva da ključ bude kriptiran i spremljen u datoteku zajedno s ESSID-om, za kasnije korištenje putem aplikacije `wpa_supplicant`. Zato je potrebno napraviti par dodatnih koraka:

Pošto želimo pojednostaviti i napraviti sigurnosnu pohranu bivših postavki, preimenuj postojeću datoteku `wpa_supplicant.conf`:

 `# mv /etc/wpa_supplicant.conf /etc/wpa_supplicant.conf.original` 

Koristeći `wpa_passphrase`, upiši ime svoje bežične mreže i WPA ključ koji će biti kriptiran i spremljen u `/etc/wpa_supplicant.conf`.

Idući primjer kriptira ključ "my_secret_passkey" bežične mreže "linksys", generira novu konfiguracijsku datoteku (`/etc/wpa_supplicant.conf`) i zapisuje kriptirani ključ u datoteku:

 `# wpa_passphrase linksys "my_secret_passkey" > /etc/wpa_supplicant.conf` 

Provjeri [WPA Supplicant](/index.php?title=WPA_Supplicant_(Hrvatski)&action=edit&redlink=1 "WPA Supplicant (Hrvatski) (page does not exist)") za više informacija.

**Note:** `/etc/wpa_supplicant.conf` je spremljen u obliku običnog teksta. Ovo nije rizik u instalacijskom okruženju, ali nakon pokretanja instaliranog sustava i rekonfiguracije WPA, nemoj zaboraviti promijeniti dopuštenja datoteke `/etc/wpa_supplicant.conf` (npr. `chmod 0600 /etc/wpa_supplicant.conf` da je učiniš čitljivom samo administratorskom računu root).

*   Asociraj svoju bežičnu karticu s uređajem pristupne točke kojeg želiš koristiti. Ovisno o tipu enkripcije (bez enkripcije, WEP ili WPA), procedura je drugačija. Moraš znati ime odabrane bežične mreže (ESSID).

<table border="1">

<tbody>

<tr>

<th>Enkripcija</th>

<th>Naredba</th>

</tr>

<tr>

<td>Bez enkripcije</td>

<td>`iwconfig wlan0 essid "linksys"`</td>

</tr>

<tr>

<td>WEP s hex ključem</td>

<td>`iwconfig wlan0 essid "linksys" key "0241baf34c"`</td>

</tr>

<tr>

<td>WEP s ASCII lozinkom</td>

<td>`iwconfig wlan0 essid "linksys" key "s:pass1"`</td>

</tr>

<tr>

<td>WPA</td>

<td>`wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf`</td>

</tr>

</tbody>

</table>

**Note:** Proces mrežne konekcije može biti automatiziran kasnije koristeći Archev network daemon, [netcfg](/index.php?title=Netcfg_(Hrvatski)&action=edit&redlink=1 "Netcfg (Hrvatski) (page does not exist)"), [wicd](/index.php?title=Wicd_(Hrvatski)&action=edit&redlink=1 "Wicd (Hrvatski) (page does not exist)"), ili neki drugi mrežni upravitelj po tvome izboru.

*   Nakon korištenja odgovarajuće metode asocijacije, pričekaj par trenutaka i potvrdi da je asocijacija s uređajem pristupne točke uspješna koristeći iduću naredbu:

 `# iwconfig wlan0` 

Ispis bi trebao pokazati bežičnu mrežu asociranu sa sučeljem.

*   Pošalji zahtijev za IP-adresom koristeći `/sbin/dhcpcd <sučelje>`, npr.:

 `# dhcpcd wlan0` 

*   Za kraj, pobrini se da možeš komunicirati s ostatkom Interneta koristeći `/bin/ping`:

 `$ ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=49 time=87.7 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=49 time=87.0 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=49 time=94.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 87.052/89.812/94.634/3.430 ms

```

Sada bi trebala postojati ispravna mrežna konekcija. U slučaju problema pogledaj detaljnu stranicu [postavljanja bežične mreže](/index.php?title=Wireless_Setup_(Hrvatski)&action=edit&redlink=1 "Wireless Setup (Hrvatski) (page does not exist)").

Vrati se na tty1 s <ALT>+F1 te nastavi sa [postavljanjem hardverskog vremena](#Postavi_hardversko_vrijeme).

### Postavi hardversko vrijeme

Postavi mod rada harverskog sata. Ako odabrani mod ne odgovara postavci drugih postojećih instaliranih operacijskih sustava, prebrisat će ih i uzrokovati pomicanje vremena na tim sustavima.

*   [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") (preporučeno)

**Note:** Korištenje UTC-a za hardverski sat ne znači da će vrijeme biti prikazano kao UTC u softveru.

*   **localtime** (ne preporuča se) - Korišteno u Windowsima. Ako je vrijeme postavljeno na localtime, Linux neće primijetiti periode ljetnog računanja vremena.

**Warning:** Ako koristiš _localtime_, postoji šansa pojavljivanja nekih poznatih i nepopravljivih bugova.

**Note:** Bilo koja druga vrijednost rezultirat će u ostavljanju hardverskog sata onakvim kakav jest (što je korisno za virtualizaciju).

#### Dual boot

Ako dual-bootaš Windowse na svom računalu, imaš dvije opcije:

*   Postavi Arch Linux na _localtime_, a zatim kasnije (u [konfiguraciji sustava](#Konfiguriraj_sustav)) izbaci `hwclock` iz `DAEMONS` liste u `/etc/rc.conf` (Windowsi će se pobrinuti o izmjenama hardverskog sata). Ne preporuča se.
*   Postavi Arch Linux na UTC i natjeraj Windowse da isto koriste UTC (potreban je brza izmjena registryja, pogledaj [ovu stranicu](https://help.ubuntu.com/community/UbuntuTime#Make%20Windows%20use%20UTC) za upute). Također, ne dozvoli Windowsima da sinkroniziraju svoje vrijeme s Internetom, jer će to ponovno promijeniti hardverski sat u _localtime_ mod. Ako želiš takvu funkcionalnost (sinkronizaciju s NTP-serverima), možeš koristiti **openntpd** na svom Arch-sustavu. Preporučeno.

### Pripremi tvrdi disk

**Warning:** Particioniranje tvrdih diskova može uništiti podatke. Strogo je preporučeno da se prije ikakvih daljnjih koraka napravi sigurnosna pohrana svih važnih podataka.

**Note:** Particioniranje može biti učinjeno prije inicijalizacije instalacije Archa, koristeći [GParted](http://gparted.sourceforge.net/download.php) ili druge dostupne alate. Ako je ciljni disk već bo particioniran na željeni način, nastavi s [postavljanjem montažnih točaka datotečnog sustava](#Postavi_monta.C5.BEne_to.C4.8Dke_datote.C4.8Dnog_sustava).

Verificiraj trenutni disk koristeći `/sbin/fdisk` s `-l` (malo slovo L) zastavicom.

Otvori novu virtualnu konzolu (<ALT>+F3) i upiši:

 `# fdisk -l` 

Zapamti koje ćeš diskove i particije koristiti prilikom instalacije Archa.

Skoči natrag na instalacijsku skriptu (<ALT>+F1).

Odaberi prvi unos u meniju "Prepare Hard Drive".

*   Opcija 1: Automatska priprema (Izbriše ČITAV tvrdi disk i automatski postavi particije)

Automatska priprema dijeli disk prema idućoj konfiguraciji:

*   ext2 /boot particija preporučene veličine 100MB.
*   swap particija preporučene veličine 256MB.
*   Različite / i /home particije, gdje su dostupni datotečni sustavi među ext2, ext3, ext4, reiserfs, xfs i jfs, ali svakako primijeti da **i / i /home dijele identičan tip datotečnog sustava** ukoliko odabereš automatsku pripremu diska.

Ponavljamo upozorenje: automatska će priprema **u potpunosti izbrisati sadržaj odabranog diska**. Pažljivo pročitaj upozorenje prikazano u instalacijskom procesu i pobrini se da zaista odabireš željen uređaj.

*   Opcija 2: Ručno particioniranje tvrdih diskova (s cfdisk) - preporučeno.

Ova će opcija dopustiti najdetaljnije rješenje particioniranja za tvoje osobne potrebe.

*   Opcija 3: Ručno konfiguriraj block uređaje, datotečne sustave i montažne točke

Ako je ovo odabrtano, sustav će ispisati koje je datotečne sustave i montažne točke pronašao, a zatim te pitati želiš li ih koristiti.

*   Opcija 4: Obrat zadnjih promjena datotečnog sustava

_Na ovoj točci, napredniji korisnici GNU/Linuxa koji su upoznati s ručnim particioniranjem mogu preskočiti niže na [odabir paketa](#Odaberi_pakete)._

**Note:** Ako instaliraš sustav na USB-memoriju, pogledaj [ovu stranicu](/index.php?title=Installing_Arch_Linux_on_a_USB_key_(Hrvatski)&action=edit&redlink=1 "Installing Arch Linux on a USB key (Hrvatski) (page does not exist)").

#### Particioniranje tvrdih diskova (opće informacije)

##### Tip particije

Particioniranje tvrdog diska definira specifična područja (particije) unutar diska koja će se pojedinačno ponašati kao odvojeni diskovi i unutar kojih može biti stvoren (formatiran) datotečni sustav.

Postoje tri tipa diskovnih particija:

*   Primarna (Primary)
*   Proširena (Extended)
    *   Logička (Logical)

**Primarne** particije mogu biti bootabilne i limitirane su na **četiri particije po disku ili raid jedinici**. Ako shema particioniranja zahtijeva više od četiri particije, potrebno je stvoriti jednu **proširenu** particiju koja će sadržavati proizvoljan broj **logičkih** particija.

Proširene particije nisu iskoristive same po sebi; one su jednostavno ogrtač oko skupine logičkih particija. Tvrdi disk može sadržavati samo jednu proširenu particiju, koja zatim može biti podijeljena na logičke particije. Primijeti da se **proširena** particija smatra i **primarnom** particijom, tako da stvaranje proširene particije znači da su dostupne još samo tri primarne na tom istom disku. Ipak, najveći broj logičkih particija unutar proširene ne postoji: može ih biti koliko god želiš.

##### Swap particija

Swap particija je mjesto na disku gdje se sprema virtualni RAM, što dopušta kernelu da lako koristi diskovnu pohranu za podatke koji ne stranu u fizički RAM.

Povijesno, opće pravilo za swap particije je bilo "dva puta veći kapacitet od fizičkog RAM-a". Danas, nakon što su računala poprimila mnogo veće memorijske kapacitete, to pravilo je sve manje i manje korišteno. Na računalima s manje od 512 MB RAM-a, to 2x pravilo je u redu. Ako pak računalo pruža velike količine RAM-a (preko 1024 MB), moguće je imati manju swap particiju ili čak u potpunosti zanemariti stvaranje i korištenje swap particije, pošto je opcija stvaranja [swap datoteke](/index.php?title=HOW_TO:_Create_swap_file_(Hrvatski)&action=edit&redlink=1 "HOW TO: Create swap file (Hrvatski) (page does not exist)") uvijek moguća. Na računalima s više od 2 GB RAM-a u pravilu nije uopće potrebno stvarati swap particiju.

U ovom primjeru ćemo koristiti swap particiju kapaciteta 1 GB.

**Note:** Ako koristiš opciju hiberniranja računala, potrebna ti je swap particija barem jednake veličine kao i fizički RAM. Neki Arčeri čak preporučaju učiniti je 10-15% većom, u slučaju loših sektora.

##### Particijski raspored

Raspored particija na disku je jedna vrlo osobna stvar koja varira od jednog naprednog korisnika do drugog. Nečiji izbor može ovisiti o potrebama i zahtjevima. Ako želiš dual-bootati Arch Linux i Windows pogledaj [Windows i Arch dual-boot](/index.php?title=Windows_and_Arch_Dual_Boot_(Hrvatski)&action=edit&redlink=1 "Windows and Arch Dual Boot (Hrvatski) (page does not exist)").

Kandidati za posebne particije:

**/** (root) _Korijenska particija je primarna particija koja sadrži sve ostale; vrh hijerarhije. Svi direktoriji i datoteke se nalaze unutar korijenskog direktorija "/", čak ako se nalaze na drugačijim fizičkim uređajima. Sadržaj korijenske particije mora biti dovoljan da bi se sustav bootao, obnovio i/ili popravio. Neki direktoriji pod / su sami kandidati za posebne particije. (Pogledaj upozorenje niže.)_

**/boot** _Ovaj direktorij sadrži kernel, ramdisk slike, bootloader konfiguracijsku datoteku i bootloader razine. /boot sadrži i podatke koji se koriste prije nego kernel krene pokretati korisničke programe. To može uključivati sačuvane master boot sektore i datoteke rasporeda sektora._

**Warning:** Osim /boot, direktoriji važni za bootanje su: '_**/bin', '/etc', '/lib', i '/sbin'. Zato se ne smiju nalaziti na particijama na kojima se ne nalazi /.**_

**/home** _Sadrži poddirektorije, svaki imenovan po jednom korisniku, za pohranu raznih osobnih podataka kao i konfiguracijskih datoteka specifičnih za svakog korisnika._

**/usr** _Dok je root primarna particija, /usr je sekundarna hijerarhija za podatke svih korisnika sustava, što uključuje većinu višekorisničkih aplikacija. /usr sadrži dijeljene podatke koji se mogu samo čitati i ne smiju prebrisivati (osim u slučaju nadogradnje sustava)._

**Warning:** Zasebna /usr particija će uzrokovati neke probleme s udevom i pokvarit će [systemd](/index.php?title=Systemd_(Hrvatski)&action=edit&redlink=1 "Systemd (Hrvatski) (page does not exist)"). [izvor](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken)

**/tmp** _direktorij za programe koji zahtijevaju privremene datoteke poput '.lck' datoteke, koje se mogu koristiti da bi spriječile postojanje više instanci istog programa sve dok neki zadatak ne bude gotov, nakon čega se '.lck' datoteka briše. Programi ne smiju pretpostavljati da se sadržaj direktorija /tmp očuva između pokretanja tih programa; sadržaj tog direktorija se obično obriše prilikom svakog bootanja sustava._

**/var** _sadrži podatke koji variraju: administratorske zapise, pacmanov cache i slično. Sve što se inače zapisivalo u /usr tijekom rada sustava danas se zapisuje unutar /var._

_**Postoji nekoliko prednosti ukoliko se koristi više particija umjesto jedne jedine:**_:

*   Sigurnost: Svaka particija može biti konfigurirana u `/etc/fstab` kao 'nosuid', 'nodev', 'noexec', 'readonly', itd.
*   Stabilnost: Korisnik ili pokvareni program može potpuno prebrisati particiju smećem ako imaju dozvolu da to očine. Kritični programi koji se nalaze na drugačijim particijama, ostaju neoštećeni.
*   Brzina: Particija na koju se prečesto zapisuje može postati fragmentirana. (Dobra metoda za zaobilazak fragmentacije je ta da se pobrineš da particija nikada ne bude u opasnosti da joj nedostaje prostora.) Druge particije ostaju nefragmentirane i može ih se zasebno defragmentirati.
*   Integritet: Ako jedna particija postane koruptirana, druge su još uvijek sigurne.

U ovom primjeru ćemo koristiti različite particije za /, /var, /home i swap particiju.

**Note:** `/var` sadrži mnogo malenih datoteka. To se mora uzeti u obzir prilikom odabira tipa datotečnog sustava za nju (ako se uopće odlučiš dodijeliti /var posebnu particiju).

##### Koliko velike moraju biti moje particije?

Dati odgovor na to pitanje znači poznavati individualne potrebe osobe koja pitanje postavlja. Možda želiš imati samo korijensku particiju i swap-particiju, ili samo korijensku particiju bez ikakvih dodatnih. Radi što boljeg izbora, upoznaj se s idućim primjerima:

*   Korijenska particija (/) će sadržavati /usr direktorij, koji može postati poprilično velik, ovisno o tome koliko se softvera instalira. 15 do 20 GB bi trebalo bitit dovoljno velikoj većini korisnika.
*   /var će sadržavati, među ostalim, [ABS](/index.php?title=ABS_(Hrvatski)&action=edit&redlink=1 "ABS (Hrvatski) (page does not exist)")-stablo i pacmanov međuspremnik. Držati pakete u međuspremniku je korisno: pruža mogućnost reverzija nadogradnja paketa ukoliko je to potrebno. /var ima običaj rasti veličinom s vremenom; pacmanov međuspremnik pogotovo, ali može se izbrisati ukoliko je to potrebno. Ako koristiš SSD, možeš staviti /var na tvrdi disk, a / i /home na SSD kako ne bi dolazilo do nepotrebnih zapisa i čitanja sa SSD-ja. 8 do 12 GB bi trebalo biti dovoljno za jedno kućno računalo, ovisno o tome koliko softvera planiraš instalirati. Serveri imaju relativno veće /var direktorije.
*   /home je tipično mjesto gdje leže korisnički podaci, podaci skinuti s Interneta i multimedija. Upravo zato je /home tipično najveći direktorij na disku. Nemoj zaboraviti kako će svi podatci na /home particiji ostati netaknuti ukoliko odlučiš reinstalirati Arch Linux (dokle god imaš posebnu /home particiju).
*   Dodatnih 25% prostora dodanih svakoj particiji je dobra praksa, radi neočekivanih slučajeva ili oprezne mjere protiv fragmentacije.

_Ako pratiš gornja pravila, jedan tipični sustav će imati korijensku particiju / veličine 15 GB, /var particiju veličine 10 GB, swap particiju veličine 1 GB i /home particiju veličine preostalog dijela diska._

#### Ručno particioniranje tvrdog diska (pomoću cfdisk)

Start by creating the primary partition that will contain the **root**, (/) filesystem.

Choose **N**ew -> 'Primary' and enter the desired size for root (/). Put the partition at the beginning of the disk.

Also choose the **T**ype by designating it as '83 Linux'. The created / partition shall appear as sda1 in our example.

Now create a primary partition for /var, designating it as **T**ype '83 Linux'. The created /var partition shall appear as sda2.

Next, create a partition for swap. Select an appropriate size and specify the **T**ype as '82 (Linux swap / Solaris)'. The created swap partition shall appear as sda3.

Lastly, create a partition for your /home directory. Choose another primary partition and set the desired size.

Likewise, select the **T**ype as '83 Linux'. The created /home partition shall appear as sda4.

Example:

```
Name    Flags     Part Type    FS Type           [Label]         Size (MB)
-------------------------------------------------------------------------
sda1               Primary     Linux                             15440 #root
sda2               Primary     Linux                             10256 #/var
sda3               Primary     Linux swap / Solaris              1024  #swap
sda4               Primary     Linux                             140480 #/home

```

Choose **W**rite and type '**yes'**. Beware that this operation may destroy data on your disk. Choose **Q**uit to leave the partitioner. Choose 'Done' to leave this menu and continue with "Set Filesystem Mountpoints".

**Note:** Since the latest developments of the Linux kernel which include the libata and PATA modules, all IDE, SATA and SCSI drives have adopted the sd_x_ naming scheme. This is perfectly normal and should not be a concern.

#### Creating filesystems (general information)

##### Filesystem types

Again, a filesystem type is a very subjective matter which comes down to personal preference. Each has its own advantages, disadvantages, and unique idiosyncrasies. Here is a very brief overview of supported filesystems:

1.  [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") _Second Extended Filesystem_- Old, mature GNU/Linux filesystem. Very stable, but _without journaling support_ or barriers, which can result in data loss in a power loss or system crash. May be inconvenient for root (/) and /home, due to very long fsck's. _An ext2 filesystem can easily be converted to ext3._
2.  [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") _Third Extended Filesystem_- Essentially the ext2 system, but with journaling support and write barriers. ext3 is backward compatible with ext2\. Extremely stable and mature.
3.  [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") _Fourth Extended Filesystem_- Backward compatible with ext2 and ext3\. Introduces support for volumes with sizes up to 1 exabyte and files with sizes up to 16 terabytes. Increases the 32,000 subdirectory limit in ext3 to 64,000\. Offers online defragmentation ability.
4.  [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") (V3)- Hans Reiser's high-performance journaling FS uses a very interesting method of data throughput based on an unconventional and creative algorithm. ReiserFS is touted as very fast, especially when dealing with many small files. ReiserFS is fast at formatting, yet comparatively slow at mounting. Quite mature and stable. ReiserFS (V3) is not actively developed at this time. Generally regarded as a good choice for /var.
5.  [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) "wikipedia:JFS (file system)") - IBM's **J**ournaled **F**ile**S**ystem- The first filesystem to offer journaling. JFS had many years of use in the IBM AIX® OS before being ported to GNU/Linux. JFS currently uses the least CPU resources of any GNU/Linux filesystem. Very fast at formatting, mounting and fsck's, and very good all-around performance, especially in conjunction with the deadline I/O scheduler. (See [JFS](/index.php/JFS "JFS").) Not as widely supported as ext or ReiserFS, but very mature and stable.
6.  [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") - Another early journaling filesystem originally developed by Silicon Graphics for the IRIX OS and ported to GNU/Linux. XFS offers very fast throughput on large files and large filesystems. Very fast at formatting and mounting. Generally benchmarked as slower with many small files, in comparison to other filesystems. XFS is very mature and offers online defragmentation ability.
7.  [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") - Also known as "Better FS" is a new filesystem with substantial new and powerful features similar to Sun/Oracle's excellent [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS"). These include snapshots, multi-disk striping and mirroring (basically software raid without mdadm), checksums, incremental backup, and on-the-fly compression (which can give a significant performance boost as well as save space), and more. It is still considered "unstable" as of January 2011, but has been merged into the mainline kernel under experimental status. Btrfs looks to be the future of linux filesystems, and is now offered as a root filesystem choice in all major distribution installers.

**Warning:** Btrfs has no fsck utility yet, so if any corruption occurs you cannot repair the filesystem.

*   JFS and XFS filesystems cannot be _shrunk_ by disk utilities (such as _gparted_ or _parted magic_)

##### A note on journaling

All above filesystems, except ext2, utilize [journaling](http://en.wikipedia.org/wiki/Journaling_file_system). Journaling file systems are fault-resilient file systems that use a journal to log changes before they are committed to the file system to avoid metadata corruption in the event of a crash. Note that not all journaling techniques are alike; specifically, only ext3 and ext4 offer _data-mode journaling_, (though, not by default), which journals _both_ data _and_ meta-data (but with a significant speed penalty). The others only offer _ordered-mode journaling_, which journals meta-data only. While all will return your filesystem to a valid state after recovering from a crash, _data-mode journaling_ offers the greatest protection against file system corruption and data loss but can suffer from performance degradation, as all data is written twice (first to the journal, then to the disk). Depending upon how important your data is, this may be a consideration in choosing your filesystem type.

#### Manually configure block devices, filesystems and mountpoints

Specify each partition and corresponding mountpoint to your requirements. Recall that partitions end in a number. Therefore, **sda** is not itself a partition, but rather, signifies an entire drive.

Choose and create the filesystem (format the partition) for / by selecting **yes**. You will now be prompted to add any additional partitions. In our example, sda2 and sda4 remain. For sda2, choose a filesystem type and mount it as /var. Finally, choose the filesystem type for sda4, and mount it as /home.

**Note:** If you have not created and do not need a separate /boot partition, you may safely ignore the warning that it does not exist.

Return to the Main Menu.

### Select Packages

All packages during installation are from the [core] repository. They are further divided into **base**, and **base-devel**. Package information and brief descriptions are available [here](https://www.archlinux.org/packages/?repo=Core&arch=i686&limit=all&sort=pkgname).

First, select the package category:

**Note:** For expedience, all packages in **base** are selected by default. Use the space-bar to select and de-select packages.

*   base: Packages from the [core] repo to provide the minimal base environment. Always select this and do not remove any packages from it, as all packages in Arch Linux assume that _base_ is always installed.
*   base-devel: Extra tools from [core] such as `make`, and `automake`. Most beginners should choose to install it, as many will probably need it later.

After category selection, you will be presented with the full lists of packages, allowing you to fine-tune your selections. Use the space bar to select and unselect.

**Note:** If connection to a wireless network is required, remember to select and install the **wireless_tools** package. Some wireless interfaces also need [**ndiswrapper**](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration") and/or a specific [**firmware**](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration"). If you plan to use WPA encryption, you will need [**wpa_supplicant**](/index.php/WPA_supplicant "WPA supplicant"). The [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") page will help you choose the correct packages for your wireless device. Also strongly consider installing **[netcfg](/index.php/Netcfg "Netcfg")**, which will help you set up your network connection and profiles after you reboot into your new system.

After selecting the needed packages, leave the selection screen and continue to the next step, **Install Packages**.

### Install Packages

_Install Packages_ will install the selected packages to your new system. If you selected a CD-ROM/USB as the source, package versions from the CD-ROM/USB will be installed. If you opted for a netinstall, fresh packages will be downloaded from the Internet and installed.

**Note:** In some installers, you will be asked if you wish to keep the packages in the pacman cache. If you choose "yes", you will have the flexibility to [downgrade](/index.php/Downgrade "Downgrade") packages to previous versions in the future, so this is recommended (you can always clear the cache in the future).

### Configure the System

**Tip:** Closely following and understanding these steps is of key importance to ensure a properly configured system.

At this stage of the installation, you will configure the primary configuration files of your Arch Linux base system.

Now you will be asked which text editor you want to use; choose [nano](/index.php/Nano "Nano"), [joe](http://joe-editor.sourceforge.net/) or [vi](/index.php/Vim "Vim"). `nano` is generally considered the easiest of the three. Please see the related wiki pages of the editor you wish to use for instructions on how to use them. You will be presented with a menu including the main configuration files for your system.

**Note:** It is very important at this point to edit, or at least verify by opening, every configuration file. The installer script relies on your input to create these files on your installation. A common error is to skip over these critical steps of configuration.

#### Can the installer handle this more automatically?

Hiding the process of system configuration is in direct opposition to **[The Arch Way](/index.php/The_Arch_Way "The Arch Way")**. While it is true that recent versions of the kernel and hardware probing tools offer excellent hardware support and auto-configuration, Arch presents the user all pertinent configuration files during installation for the purposes of _transparency and system resource control_. By the time you have finished modifying these files to your specifications, you will have learned the simple method of manual Arch Linux system configuration and become more familiar with the base structure, leaving you better prepared to use and maintain your new installation productively.

#### /etc/rc.conf

Arch Linux uses the file `/etc/rc.conf` as the principal location for system configuration. This one file contains a wide range of configuration information, principally used at system startup. As its name directly implies, it also contains settings for and invokes the `/etc/rc*` files, and is, of course, sourced _by_ these files.

##### LOCALIZATION section

LOCALE

This sets your system locale, which will be used by all i18n-aware applications and utilities. You can get a list of the available locales by running `locale -a` from the command line. This setting's default is usually fine for US English users. However if you experience any problems such as some characters not printing right and being replaced by squares you may want to go back and replace "en_US.utf8" with just "en_US".

DAEMON_LOCALE

Specifies whether or not to use the daemon locale (with "yes" or "no"). Will use the environment variable $LOCALE as the value of the locale if specified as "yes", otherwise will use the C locale (if left at the default value of "no").

HARDWARECLOCK

Specifies whether the hardware clock, which is synchronized on boot and on shutdown, stores **UTC** time, or **local time**. See [Set Clock](#Set_Clock).

TIMEZONE

Specify your time zone. (All available zones are under `/usr/share/zoneinfo/`).

KEYMAP

The available keymaps are in `/usr/share/kbd/keymaps`. Please note that this setting is only valid for your TTYs, not any graphical window managers or **X**.

CONSOLEFONT 

Available console fonts reside under `/usr/share/kbd/consolefonts/` if you must change. The default (blank) is safe.

CONSOLEMAP 

Defines the console map to load with the setfont program at boot. Possible maps are found in `/usr/share/kbd/consoletrans`, if needed. The default (blank) is safe.

USECOLOR 

Select "yes" if you have a color monitor and wish to have colors in your consoles.

**Example for LOCALIZATION:**

```
LOCALE="en_US.utf8"
DAEMON_LOCALE="no"
HARDWARECLOCK="UTC"
TIMEZONE="US/Eastern"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

```

##### HARDWARE section

MODULES 

Specify additional MODULES if you know that an important module is missing. For example, if you will be using loopback filesystems, add "loop". Note that normally all needed modules are automatically loaded by udev, so you will rarely need to add something here.

**Example for HARDWARE:**

```
# Scan hardware and load required modules at boot
MODULES=()

```

##### NETWORKING section

HOSTNAME

Set your hostname to your liking. This is the name of your computer. Whatever you put here, also put it in `/etc/hosts`.

**Example:**

```
HOSTNAME="arch"

```

interface

Specify the ethernet interface you want to be used for connecting to your local network.

address

If you want to use a static IP for your computer, specify it here. **Leave this blank for DHCP.**

netmask

Optional, defaults to _255.255.255.0_. If you want to use a custom netmask, specify it here. **Leave this blank for DHCP.**

broadcast

Optional. If you want to use a custom broadcast address, specify it here. **Leave this blank for DHCP.**

gateway

If you set a static IP in "address", enter the IP address of the default gateway (eg. your modem/router) here. **Leave this blank for DHCP.**

NETWORK_PERSIST 

Setting this to "yes" will skip network shutdown. This is required if your root device is on NFS.

NETWORKS

This is an optional setting to be enabled only if using the [netcfg](/index.php/Netcfg "Netcfg") package with optional _dialog_ package. Enable these netcfg profiles at boot-up. These are useful if you happen to need more advanced network features than the simple network service supports, such as multiple network configurations (ie, laptop users).

**Example with Static IP:**

```
HOSTNAME=arch
interface=eth0
address=192.168.1.100
netmask=255.255.255.0
broadcast=192.168.1.255
gateway=192.168.1.1
#NETWORKS=(main)
```

**Example with Dynamic IP (DHCP):**

```
HOSTNAME=arch
interface=eth0
address=
netmask=
broadcast=
gateway=
#NETWORKS=(main)
```

**Other notes**

When using a static IP, modify `/etc/resolv.conf` to specify the DNS servers of choice. Please see the [section below](#.2Fetc.2Fresolv.conf) regarding this file.

**Note:** Connecting to a wireless network automatically requires a few more steps and may require you to set up a network manager such as [netcfg](/index.php/Netcfg "Netcfg") or [wicd](/index.php/Wicd "Wicd"). Please see the [Wireless Setup](/index.php/Wireless_network_configuration#Part_II:_Wireless_management "Wireless network configuration") page for more information

**Tip:** If using a non-standard MTU size (a.k.a. jumbo frames) is desired AND the installation machine hardware supports them, see the [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames") wiki article for further configuration.

##### DAEMONS section

This array simply lists the names of those scripts contained in `/etc/rc.d/` which are to be started during the boot process, and the order in which they start. Asynchronous initialization by backgrounding is also supported and useful for speeding up boot:

```
DAEMONS=(network @syslog-ng netfs @crond)

```

*   If a script name is prefixed with a bang (!), it is not executed.
*   If a script is prefixed with an "at" symbol (@), it shall be executed in the background; the startup sequence will not wait for successful completion of each daemon before continuing to the next. (Useful for speeding up system boot). Do not background daemons that are needed by other daemons. For example "mpd" depends on "network", therefore backgrounding network may cause mpd to break.
*   Edit this array whenever new system services are installed, if starting them automatically during boot is desired.

**Note:** This "BSD-style" init, is the Arch way of handling what other distributions handle with various symlinks to an /etc/init.d/ directory.

###### General information

The [daemons](/index.php/Daemons "Daemons") line need not be changed at this time, but it is useful to explain what daemons are, as they will be addressed later in this guide.

A [daemon](https://en.wikipedia.org/wiki/Daemon_(computing) "wikipedia:Daemon (computing)") is a program that runs in the background, waiting for events to occur and offering services. A good example is a web server that waits for a request to deliver a page (e.g.: httpd) or an SSH server waiting for a user login (e.g.: sshd). While these are full-featured applications, there are also daemons whose work is not that visible. Examples are a daemon which writes messages into a log file (e.g. syslog, metalog), and a daemon which provides a graphical login (e.g.: gdm, kdm). All these programs can be added to the daemons line and will be started when the system boots. Useful daemons will be presented during this guide.

**Tip:** All Arch daemon scripts reside under /etc/rc.d/

#### /etc/fstab

The [fstab](https://en.wikipedia.org/wiki/fstab "wikipedia:fstab") (for **f**ile **s**ystems **tab**le) is part of the system configuration listing all available disks and disk partitions, and indicating how they are to be initialized or otherwise integrated into the overall system's filesystem. The `/etc/fstab` file is most commonly used by the **mount** command. The mount command takes a filesystem on a device, and adds it to the main system hierarchy that you see when you use your system. **mount -a** is called from `/etc/rc.sysinit`, about 3/4 of the way through the boot process, and reads `/etc/fstab` to determine which options should be used when mounting the specified devices therein. If **noauto** is appended to a filesystem in `/etc/fstab`, **mount -a** will not mount it at boot.

_An example of `/etc/fstab`_

```
# <file system>                            <dir>     <type>  <options>            <dump> <pass>
shm                                        /dev/shm  tmpfs   nodev,nosuid         0      0
tmpfs                                      /tmp      tmpfs   nodev,noexec,nosuid  0      0
UUID=0ddfbb25-9b00-4143-b458-bc0c45de47a0  /         ext4    defaults             0      1
UUID=da6e64c6-f524-4978-971e-a3f5bd3c2c7b  /var      ext4    defaults             0      2
UUID=440b5c2d-9926-49ae-80fd-8d4b129f330b  none      swap    defaults             0      0
UUID=95783956-c4c6-4fe7-9de6-1883a92c2cc8  /home     ext4    defaults             0      2

```

**Note:** See the [fstab article](/index.php/Fstab "Fstab") for more information and performance tweaks such as "noatime" or "relatime".

<file system>

Describes the block device or remote filesystem to be mounted. For regular mounts, this field will contain a link to a block device node (as created by mknod which is called by udev at boot) for the device to be mounted; for instance, `/dev/cdrom` or `/dev/sda1`.

**Note:** If your system has more than one hard drive, the installer will default to using UUID rather than the sd_x_ naming scheme, for consistent device mapping. **[Utilizing UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") has several advantages and may also be preferred to avoid issues if hard disks are added to the system in the future.** Due to active developments in the kernel and also udev, the ordering in which drivers for storage controllers are loaded may change randomly, yielding an unbootable system/kernel panic. Nearly every motherboard has several controllers (onboard SATA, onboard IDE), and due to the aforementioned development updates, `/dev/sda` may become `/dev/sdb` on the next reboot. For more information, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

<dir>

Describes the mount point for the filesystem. For swap partitions, this field should be specified as 'none'; (Swap partitions are not actually mounted.)

<type>

Describes the type of the filesystem. The Linux kernel supports many filesystem types. (For the filesystems currently supported by the running kernel, see `/proc/filesystems`). An entry 'swap' denotes a file or partition to be used for swapping. An entry 'ignore' causes the line to be ignored. This is useful to show disk partitions which are currently unused.

<options>

Describes the mount options associated with the filesystem. It is formatted as a comma-separated list of options with no intervening spaces. It contains at least the type of mount plus any additional options appropriate to the filesystem type. For documentation on the available options for non-nfs file systems, see mount(8).

<dump>

Used by the dump(8) command to determine which filesystems are to be dumped. dump is a backup utility. If the fifth field is not present, a value of zero is returned and dump will assume that the filesystem does not need to be backed up. _Note that dump is not installed by default._

<pass>

Used by the fsck(8) program to determine the order in which filesystem checks are done at boot time. The root filesystem should have the highest priority with <pass> of 1, and other filesystems you want to have checked should have a <pass> of 2\. Filesystems with 0 <pass> will not be checked. Filesystems within a drive will be checked sequentially, but filesystems on different drives will be checked at the same time to utilize parallelism available in the hardware. If the sixth field is not present or zero, a value of zero is returned and fsck will assume that the filesystem does not need to be checked.

*   For more information, see [fstab](/index.php/Fstab "Fstab").

#### [/etc/mkinitcpio.conf](/index.php/Mkinitcpio "Mkinitcpio")

**Note:** Most users will not need to modify this file at this time, but please read the following explanatory information.

This file allows further fine-tuning of the initial ram filesystem, or initramfs, (also historically referred to as the initial ramdisk or "initrd") for your system. The initramfs is a gzipped image that is read by the kernel during boot. The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem. This means it has to load any modules that are required for devices like IDE, SCSI, or SATA drives (or USB/FW, if you are booting from a USB/FW drive). Once the initrramfs loads the proper modules, either manually or through udev, it passes control to the kernel and your boot continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem. It does not need to contain every module you would ever want to use. The majority of common kernel modules will be loaded later on by udev, during the init process.

**mkinitcpio** is the next generation of **initramfs creation**. It has many advantages over the old **mkinitrd** and **mkinitramfs** scripts.

*   It uses **glibc** and **busybox** to provide a small and lightweight base for early userspace.
*   It can use **udev** for hardware autodetection at runtime, thus preventing numerous unnecessary modules from being loaded.
*   Its hook-based init script is easily extendable with custom hooks, which can easily be included in pacman packages without having to modifiy mkinitcpio itself.
*   It already supports **lvm2**, **dm-crypt** for both legacy and luks volumes, **raid**, **swsusp** and **TuxOnIce** resuming and booting from **usb mass storage** devices.
*   Many features can be configured from the kernel command line without having to rebuild the image.
*   The **mkinitcpio** script makes it possible to include the image in a kernel, thus making a self-contained kernel image is possible.
*   Its flexibility makes recompiling a kernel unnecessary in many cases.

If using RAID or LVM on the root filesystem, the appropriate HOOKS must be configured. See the wiki pages for [LVM/RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") and [Configuring mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio") for more information. If using a non-US keyboard. add the `keymap` hook to load your local keymap during boot. Add the `usbinput` hook if using a USB keyboard (otherwise, if boot fails for some reason you will be asked to enter root's password for system maintenance but will be unable to do so). Remember to add the `usb` hook when installing arch on an external hard drive, Comfact Flash, or SD card, which is connected via usb, e.g.:

```
HOOKS="base udev autodetect pata scsi sata usb filesystems keymap usbinput"

```

If you need support for booting from USB devices, FireWire devices, PCMCIA devices, NFS shares, software RAID arrays, LVM2 volumes, encrypted volumes, or DSDT support, configure your HOOKS accordingly.

#### /etc/modprobe.d/modprobe.conf

This file can be used to set special configuration options for the kernel modules. It is unnecessary to configure this file in the example. The article on [kernel modules](/index.php/Kernel_modules "Kernel modules") has more information.

#### /etc/resolv.conf

**Note:** If you are using DHCP, you may safely ignore this file, as by default, it will be dynamically created and destroyed by the dhcpcd daemon. You may change this default behavior if you wish. See the [network](/index.php/Network#For_DHCP_IP "Network") and [resolv.conf](/index.php/Resolv.conf "Resolv.conf") pages for more information.

The _resolver_ is a set of routines in the C library that provide access to the Internet Domain Name System (DNS). One of the main functions of DNS is to translate domain names into IP addresses, to make the Web a friendlier place. The resolver configuration file, or `/etc/resolv.conf`, contains information that is read by the resolver routines the first time they are invoked by a process.

If you use a static IP, set your DNS servers in `/etc/resolv.conf` (nameserver <ip-address>). You may have as many as you wish.

An example, using OpenDNS:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

If you are using a router, you may specify your DNS servers in the router itself, and merely point to it from your `/etc/resolv.conf`, using your router's IP (which is also your gateway from `/etc/rc.conf`). Example:

```
nameserver 192.168.1.1

```

If using **DHCP**, you may also specify your DNS servers in the router, or allow automatic assignment from your ISP, if your ISP is so equipped.

#### /etc/hosts

This file associates IP addresses with hostnames and aliases, one line per IP address. For each host a single line should be present with the following information:

```
<IP-address> <hostname> [aliases...]

```

Add your _hostname_, coinciding with the one specified in `/etc/rc.conf`, as an alias, so that it looks like this:

```
127.0.0.1   localhost.localdomain   localhost **yourhostname**

```

**Warning:** This format, **including the "localhost" and your actual host name**, is required for program compatibility! So, if you have named your computer "arch", then that line above should look like this:

```
127.0.0.1   localhost.localdomain   localhost arch

```

Errors in this entry may cause poor network performance and/or certain programs to open very slowly, or not work at all. This is a very common error for beginners.

**Note:** Recent versions of the Arch Linux Installer automatically add your hostname to this file once you edit `/etc/rc.conf` with such information. If, for whatever reason, this is not the case, you may add it yourself with the given instructions.

If you use a static IP, add another line using the syntax: <static-IP> <hostname.domainname.org> <hostname> e.g.:

```
192.168.1.100 **yourhostname**.domain.org  **yourhostname**

```

**Tip:** For convenience, you may also use `/etc/hosts` aliases for hosts on your network, and/or on the Web, e.g.:

```
192.168.1.90 media
192.168.1.88 data

```

The above example would allow you access a media and data server on your network by name and without the need for typing out their respective IP addresses.

#### /etc/locale.gen

The `/usr/sbin/locale-gen` command reads from `/etc/locale.gen` to generate specific locales. They can then be used by **glibc** and any other locale-aware program or library for rendering text, correctly displaying regional monetary values, time and date formats, alphabetic idiosyncrasies, and other locale-specific standards.

By default `/etc/locale.gen` is an empty file with commented documentation. Once edited, the file remains untouched. `locale-gen` runs on every **glibc** upgrade, generating all the locales specified in `/etc/locale.gen`.

Choose the locale(s) you need by removing the # in front of the lines you want, e.g.:

```
en_US ISO-8859-1
en_US.UTF-8

```

The installer will now run the locale-gen script, which will generate the locales you specified. You may change your locale in the future by editing `/etc/locale.gen` and subsequently running `locale-gen` as root.

**Note:** If you fail to choose your locale, this will lead to a "The current locale is invalid..." error. This is perhaps the most common mistake by new Arch users.

#### Pacman Mirror

Choose a mirror repository for `pacman`. Remember that archlinux.org is throttled, limiting downloads to 50KB/s. Check [Mirrors](/index.php/Mirrors "Mirrors") for more details about selecting a pacman mirror. Note that the mirror chosen here will carry over into your installation.

#### Root password

Finally, set a root password and make sure that you remember it later. Return to the Main Menu and continue with **Installing Bootloader**.

#### Done

When you select "Done", the system will rebuild the images and put you back to the Main Menu. This may take some time.

### Install Bootloader

Because we have no secondary operating system in our example, we will need a bootloader. [GRUB](/index.php/GRUB "GRUB") (**GR**and **U**nified **B**ootloader) will be used in the following examples. Alternatively, you may choose [LILO](/index.php/LILO "LILO"), [Syslinux](/index.php/Syslinux "Syslinux") or [GRUB2](/index.php/GRUB2 "GRUB2"). Please see the related wiki and documentation pages if you choose to use a bootloader other than GRUB.

The provided **GRUB** configuration (`/boot/grub/menu.lst`) should be sufficient, but verify its contents to ensure accuracy (specifically, ensure that the root (/) partition is specified by UUID on line 3). You may want to alter the resolution of the console by adding a vga=<number> kernel argument corresponding to your desired virtual console resolution. (A table of resolutions and the corresponding numbers is printed in the `menu.lst`.)

**Explanation:**

title

A printed menu selection. "Arch Linux (Main)" will be printed on the screen as a menu selection.

root

**GRUB'**s root; the drive and partition where the kernel (/boot) resides, according to system BIOS. (More accurately, where GRUB's stage2 file resides). **NOT necessarily the root (/) file system**, as they can reside on separate partitions. GRUB's numbering scheme starts at 0, and uses an hd_x,x_ format regardless of IDE or SATA, and enclosed within parentheses. The example indicates that /boot is on the first partition of the first drive, according to the BIOS, so (hd0,0).

kernel

This line specifies:

*   The path and filename of the kernel _**relative to GRUB's root**_. In the example, /boot is merely a directory residing on the same partition as / and **vmlinuz-linux** is the kernel filename; `/boot/vmlinuz-linux`. If /boot were on a separate partition, the path and filename would be simply `/vmlinuz-linux`, being relative to **GRUB'**s root.
*   The `root=` argument to the kernel statement specifies the partition containing the root (/) directory in the booted system, (more accurately, the partition containing `/sbin/init`). An easy way to distinguish the 2 appearances of "root" in `/boot/grub/menu.lst` is to remember that the first root statement _informs GRUB where the kernel resides_, whereas the second `root=` kernel argument _tells the kernel where the root filesystem (/) resides_.
*   Kernel options: In our example, **ro** mounts the filesystem as read-only during startup, which is usually a safe default; you may wish to change this in case it causes problems booting. **quiet** sets the default kernel log level so that all messages during boot are suppressed except serious ones. Depending on hardware, **rootdelay=8** may need to be added to the kernel options in order to be able to boot from an external usb hard drive.

initrd

The path and filename of the initial RAM filesystem **relative to GRUB'**s root. Again, in the example, /boot is merely a directory residing on the same partition as / and **initramfs-linux.img** is the initrd filename; `/boot/initramfs-linux.img`. If /boot were on a separate partition, the path and filename would be simply **/initramfs-linux.img**, being relative to **GRUB'**s root.

Example:

```
title  Arch Linux (Main)
root   (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro quiet
initrd /boot/initramfs-linux.img

```

Example for /boot on a separate partition:

```
title  Arch Linux (Main)
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda3 ro quiet
initrd /initramfs-linux.img

```

Install the [GRUB](/index.php/GRUB "GRUB") bootloader to the **Master Boot Record** (/dev/sda in our example).

**Warning:** Make sure to install GRUB on **/dev/sdX** and **not /dev/sdX_#_**! This is a common mistake.

**Tip:** For more details, see the [GRUB](/index.php/GRUB "GRUB") wiki page.

### Reboot

That is it; You have configured and installed your Arch Linux base system. Exit the install, and reboot:

 `# reboot` 

**Tip:** Be sure to remove the installation media and perhaps change the boot preference in your BIOS; otherwise you may boot back into the installation!

## Nakon instalacije

**Čestitamo! Dobrodošli u svoj novi sustav Arch Linux!**

Ova sekcija će prolaziti kroz razne obavezne procedore nakon instalacije poput nadogradnje novog sustava i dodavanje regularnog korisnika ne-administratora.

### Nadogradnja

Your new Arch Linux base system is now a functional GNU/Linux environment ready for customization. From here, you may build this elegant set of tools into whatever you wish or require for your purposes.

Login with the root account. We will configure pacman and update the system as root.

**Note:** Virtual consoles 1-6 are available. You may switch between them with <ALT>+F1...F6

#### Configure the network (if necessary)

If you properly configured your system, you should have a working network. Try to `ping example.com` to verify:

 `$ ping -c 3 example.com ` 

```
PING example.com (192.0.43.10) 56(84) bytes of data.
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=1 ttl=248 time=25.6 ms
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=2 ttl=248 time=22.9 ms
64 bytes from 43-10.any.icann.org (192.0.43.10): icmp_req=3 ttl=248 time=23.6 ms

--- example.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 22.912/24.062/25.632/1.156 ms
```

If you have successfully established a network connection, continue with **[Update, Sync, and Upgrade the system with pacman](#Update.2C_Sync.2C_and_Upgrade_the_system_with_pacman)**.

If, after trying to ping www.google.com, an "unknown host" error is received, you may conclude that your network is not properly configured. You may choose to double-check the following files for integrity and proper settings:

`/etc/rc.conf` - Specifically, check your HOSTNAME and NETWORKING section for typos and errors.

`/etc/hosts` - Double-check for format, typos, and errors.

`/etc/resolv.conf` - If you are using a static IP. If you are using DHCP, this file will be dynamically created and destroyed by default.

**Tip:** Advanced instructions for configuring the network can be found in the [Network](/index.php/Network "Network") article.

##### Wired LAN

Check your Ethernet with

 `$ ip addr` 

All interfaces will be listed. You should see an entry for eth0, or perhaps eth1\. These examples will use eth0.

**Static IP**

If required, you can set a new static IP with:

 `# ip addr add <ip>/<netmask> dev <interface>` 

and the default gateway with

 `# ip route add default via <ip>` 

Verify that `/etc/resolv.conf` contains your DNS server and add it if it is missing. Check your network again with `ping -c 3 www.google.com`. If everything is working now, adjust `/etc/rc.conf` as described above for static IP.

**DHCP**

If you have a DHCP server/router in your network try:

 `# dhcpcd eth0` 

If this is working, adjust `/etc/rc.conf` as described above, for dynamic IP.

##### Wireless LAN

Please see [Wireless Quickstart For the Live Environment](#Setup_wireless_in_the_live_environment_.28optional.29) for details on connecting to a wireless network. Although you are no longer running off the installation media, the commands are the same as long as you installed all related wireless packages during package selection. Remember, your wireless device may need firmware in order to operate. For troubleshooting, check the detailed [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") page.

##### Proxy Server

If you are behind a proxy server, edit `/etc/wgetrc` and set http_proxy and ftp_proxy in it.

##### Analog Modem, ISDN, and DSL (PPPoE)

See [Internet Access](/index.php/Internet_Access "Internet Access") for detailed instructions.

#### Update, Sync, and Upgrade the system with [pacman](/index.php/Pacman "Pacman")

Now we will update the system using [pacman](/index.php/Pacman "Pacman"). [Pacman](/index.php/Pacman "Pacman") is the **pac**kage **man**ager of Arch Linux. It manages your entire package system and handles installation, removal, package downgrade (through cache), custom compiled package handling, automatic dependency resolution, remote and local searches and much more. Pacman will now be used to download software packages from remote repositories and install them onto your system.

**Note:** If you installed via a Netinstall, many, if not all, of your packages will already be up to date. However, it is still advisable to run through this update process.

##### /etc/pacman.conf

pacman will attempt to read `/etc/pacman.conf` each time it is invoked. This configuration file is divided into sections, or repositories. Each section defines a package [repository](/index.php/Official_repositories "Official repositories") that pacman can use when searching for packages. The exception to this is the `options` section, which defines global options.

**Note:** The defaults should work, so modifying at this point may be unnecessary, but verification is always recommended. Further info available in the [Mirrors](/index.php/Mirrors "Mirrors") article.

 `# nano /etc/pacman.conf` 

Repositories are described below; enable all desired repositories by removing the # in front of the 'Include =' and '[repository]' lines.

**Note:** When choosing repos, be sure to uncomment both the repository header lines in [brackets] as well as the 'Include =' lines. Failure to do so will result in the selected repository being omitted! This is a very common error.

##### Package Repositories

A [software repository](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository") is a storage location from which software packages may be retrieved and installed on a computer. Arch Linux [package maintainers](/index.php/Package_Maintainer "Package Maintainer") (developers and [Trusted Users](/index.php/Trusted_Users "Trusted Users")) maintain a number of official repositories containing software packages for essential and popular software, readily accessible via [pacman](/index.php/Pacman "Pacman"). This article outlines those officially-supported repositories. See [Official repositories](/index.php/Official_repositories "Official repositories") for more information including details about the purpose of each repository.

Most people will want to use [core], [extra] and [community]. If you want to run 32-bit applications on Arch x86_64, enable the [multilib] repository by adding the lines below to `/etc/pacman.conf`:

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

##### AUR

The **[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")** (AUR) also contains the **unsupported** branch, which cannot be accessed directly by pacman. **AUR** [unsupported] does not contain binary packages. Rather, it provides more than thirty-one thousand PKGBUILD scripts for building packages from source, that may be unavailable through the other repos. When an AUR unsupported package acquires enough popular votes, it may be moved to the AUR [community] binary repo, if a trusted user (TU) is willing to adopt and maintain it there.

*   TU maintained
*   All PKGBUILD bash build scripts
*   **Not** pacman accessible by default

**Note:** There are a number of pacman wrappers (**[AUR helpers](/index.php/AUR_helpers "AUR helpers")**) available to help you seamlessly access AUR.

#### /etc/pacman.d/mirrorlist

Defines pacman repository mirrors and priorities.

**Note:** If your installation medium is old, your mirrorlist might be outdated, which might lead to problems when updating archlinux with pacman (see here for the [bug report](https://bugs.archlinux.org/task/22510)). Therefore it is a good idea to get the latest version of the mirrorlist from [the pacman mirror list generator page](https://www.archlinux.org/mirrorlist/). Copy the freshly generated list to `/etc/pacman.d/mirrorlist` before you continue.

Open `/etc/pacman.d/mirrorlist` in an editor and uncomment (remove the '#' in front) a server close to you. Then issue a complete package refresh:

 `# pacman -Syy` 

Passing two `--refresh` or `-y` flags forces pacman to refresh all package lists even if they are considered to be up to date. Issuing `pacman -Syy` _whenever a mirror is changed_, is good practice and will avoid possible headaches.

#### rankmirrors

Alternatively, you can use `rankmirrors`. `rankmirrors` is a bash script which will attempt to detect uncommented mirrors specified in `/etc/pacman.d/mirrorlist` which are closest to the installation machine based on latency. Faster mirrors will dramatically improve pacman performance, and the overall Arch Linux experience. This script may be run periodically, especially if the chosen mirrors provide inconsistent throughput and/or updates. Note that `rankmirrors` does not test for throughput. Tools such as `wget` or `rsync` may be used to effectively test for mirror throughput after a new `/etc/pacman.d/mirrorlist` has been generated.

Issue the following command to completely refresh package database, upgrade and install `curl`:

 `# pacman -Syyu curl` 

*   _If you get an error at this step, use the command `nano /etc/pacman.d/mirrorlist` and uncomment a server that suits you._

`cd` to the `/etc/pacman.d/` directory:

 `# cd /etc/pacman.d` 

Backup the existing `/etc/pacman.d/mirrorlist`:

 `# cp mirrorlist mirrorlist.backup` 

Edit mirrorlist.backup and uncomment all mirrors on the same continent or within geographical proximity to test with rankmirrors.

 `# nano mirrorlist.backup` 

Run the script against the mirrorlist.backup with the -n switch and redirect output to a new /etc/pacman.d/mirrorlist file:

 `# rankmirrors -n 6 mirrorlist.backup > mirrorlist` 

**Note:** **-n 6**: will rank the 6 closest mirrors

Force pacman to refresh all package lists with the new mirrorlist in place:

 `# pacman -Syy` 

##### Mirrorcheck for up-to-date packages

Since `rankmirrors` does not take into account how up-to-date a mirror's package list is, it is important to note that one or more of the mirrors it selects as fastest may still be out-of-date. [ArchLinux MirrorStatus](https://www.archlinux.org/mirrors/status/) reports various aspects about the mirrors such as network problems with mirrors, data collection problems, the last time mirrors have been synced, etc. One may wish to manually inspect `/etc/pacman.d/mirrorlist`, ensuring that the file contains only up-to-date mirrors if having the latest package versions is a priority.

Alternatively, the [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) can automatically rank mirrors close to your location by how up-to-date they are.

**Tip:** For a script that automates the process of getting and installing a `mirrorlist` file from the Pacman Mirrorlist Generator, see [Mirrors](/index.php/Mirrors#Script_to_automate_use_of_Pacman_Mirrorlist_Generator "Mirrors").

#### Get familiar with pacman

pacman is the Arch user's best friend. It is highly recommended to study and learn how to use the pacman(8) tool. Try:

 `$ man pacman` 

For more information, have a look at the [pacman](/index.php/Pacman "Pacman") wiki entry at your own leisure, or check out the [pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") entry for a comparison to other popular package managers.

#### Update the System

You are now ready to upgrade your entire system. Before you do, read through the [news](https://www.archlinux.org/news/) (and optionally the [announce mailing list](https://archlinux.org/pipermail/arch-announce/)). Often the developers will provide important information about required configurations and modifications for known issues. Consulting these pages before any upgrade is good practice.

Sync, refresh, and upgrade your entire new system with:

 `# pacman -Syu` 

or:

 `# pacman --sync --refresh --sysupgrade` 

pacman will now download a fresh copy of the master package list from the server(s) defined in `/etc/pacman.conf` and perform all available upgrades. You may be prompted to upgrade pacman itself at this point. If so, say yes, and then reissue the `pacman -Syu` command when finished.

Reboot if a kernel upgrade has occurred.

**Note:** Occasionally, configuration changes may take place requiring user action during an update; read pacman's output for any pertinent information. See [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") for more details.

Pacman output is saved in `/var/log/pacman.log`.

See [Package Management FAQ](/index.php/FAQ#Package_Management "FAQ") for answers to frequently asked questions regarding updating and managing your packages.

##### Ignoring Packages

After executing the command `pacman -Syu`, the entire system will be updated. It is possible to prevent a package from being upgraded. A typical scenario would be a package for which an upgrade may prove problematic for the system. In this case, there are two options; indicate the package(s) to skip in the pacman command line using the --ignore switch (`pacman -S --help` for details) or permanently indicate the package(s) to skip in the `/etc/pacman.conf` file in the IgnorePkg array. For more information, please see the [pacman](/index.php/Pacman "Pacman") wiki entry.

Please note that the power user is expected to keep the system up to date with pacman -Syu, rather than selectively upgrading packages. You may diverge from this typical usage as you wish; just be warned that there is a greater chance that things will not work as intended and that it could break your system. The majority of complaints happen when selective upgrading, unusual compilation or improper software installation is performed. Use of **IgnorePkg** in `/etc/pacman.conf` is therefore discouraged, and should only be used sparingly, if you know what you are doing.

##### The Arch rolling release model

Keep in mind that Arch is a **rolling release** distribution. This means there is never a reason to reinstall or perform elaborate system rebuilds to upgrade to the newest version. Simply issuing `pacman -Syu` periodically keeps your entire system up-to-date and on the bleeding edge. At the end of this upgrade, your system is completely current. Remember to **reboot** if a kernel upgrade has occurred.

### Adding a User

**Note:** Before adding your users, consider hardening your system by switching from md5 password hashes to sha512 password hashes (see: [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes")).

Linux is a multi-user environment. You should not do your everyday work using the root account: it is more than poor practice, it is dangerous. Use root for administrative tasks only and instead add a normal user account using the `adduser` program:

 `# adduser` 

You will be asked to enter some information in an interactive way. In the following example we are creating the user _archie_:

```
Login name for new user []: **archie**

User ID ('UID') [ defaults to next available ]:

Initial group [ users ]:

Additional groups (comma separated) []: **audio,lp,optical,storage,video,wheel,games,power,scanner**

Home directory [ /home/archie ]:

Shell [ /bin/bash ]:

Expiry date (YYYY-MM-DD) []:

```

As showed in the example, you are advised to enter values only for the _Login name_ and the _Additional groups_, and leave empty all the other fields.

The list of _Additional groups_ in the example is a typical choice for a desktop system, hence it is recommended especially for beginners:

*   **audio** - for tasks involving sound card and related software
*   **lp** - for managing printing tasks
*   **optical** - for managing tasks pertaining to the optical drive(s)
*   **storage** - for managing storage devices
*   **video** - for video tasks and hardware acceleration
*   **wheel** - for using sudo
*   **games** - needed for write permission for games in the games group
*   **power** - used with power options (e.g. shutdown with power button)
*   **scanner** - for using a scanner

Now you will be presented with a preview of your new account, and the ability to cancel or continue operations: after pressing `ENTER` the account will be created, and you will be prompted to enter additional, optional informations for the new user (e.g. the full name). After that, you will be asked to enter the password for your account.

Your new non-root user has finally been created, complete with a home directory and a login password.

See [Users and groups](/index.php/Users_and_groups "Users and groups") for further information. If you want to change the name of your user or any existing user, consult the [Change username](/index.php/Change_username "Change username") page. You may also check the man pages for `usermod(8)` and `gpasswd(8)`.

#### Deleting the user account

In the event of error, or if you wish to delete this user account in favor of a different name or for any other reason, use `/usr/sbin/userdel`:

 `# userdel -r [username]` 

The `-r` option will remove the user's home directory and its content, along with the the user's mail spool.

## Extras

You should now have a completely functional Arch system which will act as a suitable base for you to build upon based on your needs. However, most people are interested in a desktop system, complete with sound and graphics. This part of the guide will provide a brief overview of the procedure to acquire these extras.

### Create DVD and CDROM symlinks

Many desktop applications will expect the presence of CDROM and DVD symlinks to the `/dev/sr0` device node. Four useful symlinks may be created as so:

 `# for i in cdrom cdrw dvd dvdrw; do ln -s /dev/sr0 /dev/$i; done` 

To make the symlinks persistently created after each boot, add the above command to `/etc/rc.local`.

Alternatively, you may wish to add the commands sequentially for readability:

```
#!/bin/bash
#
# /etc/rc.local: Local multi-user startup script.
#
# create optical drive symlinks
ln -s /dev/sr0 /dev/cdrom
ln -s /dev/sr0 /dev/cdrw
ln -s /dev/sr0 /dev/dvd
ln -s /dev/sr0 /dev/dvdrw

```

### Sudo

Install Sudo:

 `# pacman -S sudo` 

To add a user as a sudo user (a "sudoer"), the visudo command must be run as root.

By default, the visudo command uses the editor [vi](/index.php/Vi "Vi"). If you do not know how to use vi, you may set the EDITOR environment variable to the editor of your choice, such as in this example with the editor "nano":

```
# EDITOR=nano visudo

```

**Note:** Please note that you are setting the variable and starting visudo on the same line at the same time. This will not work properly as two separated commands.

If you are comfortable using vi, issue the visudo command without the EDITOR=nano variable:

 `# visudo` 

This will open the file `/etc/sudoers` in a special session of vi. visudo copies the file to be edited to a temporary file, edits it with an editor, (vi by default), and subsequently runs a sanity check. If it passes, the temporary file overwrites the original with the correct permissions.

**Warning:** Do not edit `/etc/sudoers` directly with an editor; errors in syntax can cause annoyances (like rendering the root account unusable). You **must** use the _visudo_ command to edit `/etc/sudoers`.

In the previous section we added your user to the "wheel" group. To give users in the wheel group full root privileges when they precede a command with "sudo", uncomment the following line:

```
%wheel	ALL=(ALL) ALL

```

Now you can give any user access to the sudo command by simply adding them to the wheel group.

For more information, such as sudoer <TAB> completion, see [Sudo](/index.php/Sudo "Sudo").

### Sound

If you want sound, proceed to [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") for instructions. Alternatively, proceed to the [next section](#Graphical_User_Interface) first, and set up sound later.

**Note:** ALSA usually works out-of-the-box, it just needs to be unmuted.

The [Advanced Linux Sound Architecture](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (ALSA) is included with the kernel and it is recommended to try it first. However, if it does not work or you are not satisfied with the quality, the [Open Sound System](https://en.wikipedia.org/wiki/Open_Sound_System "wikipedia:Open Sound System") is a viable alternative. OSSv4 has been released under a free license and is generally considered a significant improvement over the older OSSv3 which was replaced by ALSA. Instructions can be found in the [OSS article](/index.php/OSS "OSS").

If you have advanced audio requirements, take a look at [Sound](/index.php/Sound "Sound") for an overview of various articles.

### **G**raphical **U**ser **I**nterface

#### Install X

The [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (commonly **X11**, or **X**) is a networking and display protocol which provides windowing on bitmap displays. It provides the standard toolkit and protocol to build graphical user interfaces (GUIs).

**Note:** If you are installing Arch as a Virtualbox guest, you need a different way to complete X installation. See [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest"), then jump to the configuration part below.

Now we will install the base **[Xorg](/index.php/Xorg "Xorg")** packages using pacman.

Install the base packages:

 `# pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils` 

Install [mesa](https://en.wikipedia.org/wiki/Mesa_3D_(OpenGL) "wikipedia:Mesa 3D (OpenGL)") for 3D support:

 `# pacman -S mesa` 

The 3D utilities glxgears and [glxinfo](http://dri.freedesktop.org/wiki/glxinfo) are included in the **mesa-demos** package. Install if needed:

 `# pacman -S mesa-demos` 

#### Install video driver

Next, you should install a driver for your graphics card.

You will need knowledge of which video chipset your machine has. If you do not know, use the `/usr/sbin/lspci` program:

 `$ lspci` 

**Note:** The **vesa** driver is the most generic, and should work with almost any modern video chipset. If you cannot find a suitable driver for your video chipset, vesa _should_ work with any video card, but it offers only unaccelerated 2D performance.

For a complete list of all **open-source** video drivers, search the package database:

```
$ pacman -Ss xf86-video | less

```

**Note:** Proprietary drivers for NVIDIA and ATI are covered in the next sections. If you plan on doing heavy 3D processing such as gaming, consider using these.

Use pacman to install the appropriate video driver for your video card/onboard video. Example for the Savage driver:

 `# pacman -S xf86-video-savage` 

**Tip:** For some Intel graphics cards, configuration may be necessary to get proper 2D or 3D performance, see [Intel](/index.php/Intel "Intel") for more information.

##### NVIDIA Graphics Cards

NVIDIA users have three options for drivers (in addition to the vesa driver):

*   The open-source nouveau driver, which offers fast 2d acceleration and experimental 3d support which is good enough for basic compositing (note: does not fully support powersaving yet). [Feature Matrix.](http://nouveau.freedesktop.org/wiki/FeatureMatrix)
*   The open-source (but obfuscated) nv driver, which is very slow and only has 2d support.
*   The proprietary nvidia drivers, which offer good 3d performance and powersaving. Even if you plan on using the proprietary drivers, it is recommended to start with nouveau and then switch to the binary driver after you have X set up and working. Nouveau often works out-of-the-box, while nvidia will require configuration and likely some troubleshooting. See [NVIDIA](/index.php/NVIDIA "NVIDIA") for more information.

The open-source nouveau driver should be good enough for most users and is recommended:

 `# pacman -S xf86-video-nouveau` 

For experimental 3D support:

 `# pacman -S nouveau-dri` 

**Tip:** For advanced instructions, see [Nouveau](/index.php/Nouveau "Nouveau").

##### ATI Graphics Cards

ATI owners have two options for drivers (in addition to the vesa driver):

*   The open source **radeon** driver provided by the **xf86-video-ati** package. See the [radeon feature matrix](http://wiki.x.org/wiki/RadeonFeature) for details.
*   The proprietary **fglrx** driver provided by the [catalyst](https://aur.archlinux.org/packages.php?O=0&K=catalyst&do_Search=Go) package located in the [AUR](/index.php/AUR "AUR"). It supports only newer devices (HD2xxx and newer). It was once a package offered by Arch in the **extra** repository, but as of March 2009, official support has been dropped because of dissatisfaction with the quality and speed of development of the proprietary driver. See [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") for more information.

The open-source driver is the recommended choice. Install the **radeon** ATI Driver:

 `# pacman -S xf86-video-ati` 

**Tip:** For advanced instructions, see [ATI](/index.php/ATI "ATI").

#### Install input drivers

Udev should be capable of detecting your hardware without problems and evdev (**xf86-input-evdev**) is the modern, hotplugging input driver for almost all devices so in most cases, installing input drivers is not needed. At this point, evdev has already been installed as a dependency of Xorg.

If evdev does not support your device, install the needed driver from the xorg-input-drivers group.

For a complete list of available input drivers, invoke a pacman search:

```
# pacman -Ss xf86-input | less

```

**Note:** You only need xf86-input-keyboard or xf86-input-mouse if you plan on disabling hotplugging, otherwise, evdev will act as the input driver.

Laptop users (or users with a touchscreen) will also need the synaptics package to allow X to configure the touchpad/touchscreen:

 `# pacman -S xf86-input-synaptics` 

**Tip:** For instructions on fine tuning or troubleshooting touchpad settings, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") article.

#### Configure X (Optional)

**Warning:** Proprietary drivers usually require a reboot after installation along with configuration. See [NVIDIA](/index.php/NVIDIA "NVIDIA") or [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") for details.

X Server features auto-configuration and therefore can function without an `xorg.conf`. If you still wish to manually configure X Server, please see the [Xorg](/index.php/Xorg "Xorg") wiki page.

##### Non-US keyboard

If you do not use a standard US keyboard, you need to set the keyboard layout in `/etc/X11/xorg.conf.d/10-evdev.conf`:

```
Section "InputClass"
    Identifier "evdev keyboard catchall"
    MatchIsKeyboard "on"
    MatchDevicePath "/dev/input/event*"
    Driver "evdev"
    **Option "XkbLayout" "be"**
EndSection

```

If, for example, you wish to use a variant of the US keyboard, add the following into the same section from the previous example:

```
Option "XkbLayout" "us"
Option "XkbVariant" "dvorak"

```

**Note:** The **XkbLayout** key may differ from the keymap code you used with the km or loadkeys command. A list of many keyboard layouts and variants can be found in `/usr/share/X11/xkb/rules/base.lst` (see text after line beginning with `! layout`). For instance the layout: **gb** corresponds to "English (UK)".

#### Testing X

This section will explain how to start a very basic graphical environment in order to test **X**. This uses the simple default **X** window manager, twm.

Install the default test environment:

 `# pacman -S xorg-twm xorg-xclock xterm` 

The default X environment is rather bare. [This section below](#Choose_and_install_a_graphical_interface) will deal with installing a desktop environment or window manager of your choice to supplement X.

If you installed Xorg before creating your regular user, there will be an empty `.xinitrc` file in your $HOME that you need to either delete or edit in order to start a graphical environment. Simply deleting it will cause **X** to run with the default environment (twm, xclock, xterm).

 `$ rm ~/.xinitrc` 

##### Message bus

**Note:** [dbus](/index.php/Dbus "Dbus") is likely required for many of your applications to work properly, if you know you do not need it, skip this section.

Install [dbus](/index.php/Dbus "Dbus"):

 `# pacman -S dbus` 

Start the dbus daemon:

 `# rc.d start dbus` 

Add dbus to your DAEMONS array so it starts automatically on boot:

 `/etc/rc.conf`  `DAEMONS=(... **dbus** ...)` 

##### Start X

**Note:** The Ctrl-Alt-Backspace shortcut traditionally used to kill X has been deprecated and will not work to exit out of this test. You can enable Ctrl-Alt-Backspace by editing `xorg.conf`, as described [here](/index.php/Xorg#Ctrl-Alt-Backspace_doesn.27t_work "Xorg").

Finally, start Xorg:

 `$ startx` 

or:

 `$ xinit -- /usr/bin/X -nolisten tcp` 

A few movable windows should show up, and your mouse should work. Once you are satisfied that **X** installation was a success, you may exit out of **X** by issuing the `exit` command into the prompts until you return to the console.

If the screen goes black, you may still attempt to switch to a different virtual console (CTRL-Alt-F2, for example), and login blindly as root, followed by <Enter>, followed by root's password followed by <Enter>.

You can attempt to kill the **X** server with `/usr/bin/pkill` (note the capital letter **X**):

 `# pkill X` 

If **pkill** does not work, reboot blindly with:

 `# reboot` 

##### In case of errors

If a problem occurs, look for errors in `/var/log/Xorg.0.log`. Be on the lookout for any lines beginning with `(EE)` which represent errors, and also `(WW)` which are warnings that could indicate other issues.

 `$ grep EE /var/log/Xorg.0.log` 

Errors may also be searched for in the console output of the virtual console from which **X** was started.

See the [Xorg](/index.php/Xorg "Xorg") article for detailed instructions and troubleshooting.

##### Need Help?

If you are still having trouble after consulting the [Xorg](/index.php/Xorg "Xorg") article and need assistance via the Arch forums, be sure to install and use **wgetpaste**:

 `# pacman -S wgetpaste` 

Use **wgetpaste** and provide links for the following files when asking for help in your forum post:

*   ~/.xinitrc
*   /etc/X11/xorg.conf
*   /var/log/Xorg.0.log
*   /var/log/Xorg.0.log.old

Use it like so:

 `$ wgetpaste </path/to/file>` 

Post the corresponding links given within your forum post. Be sure to provide appropriate hardware and driver information as well.

**Note:** It is very important to provide detail when troubleshooting X. Please provide all pertinent information as detailed above when asking for assistance on the Arch forums.

#### Install Fonts

At this point, you may wish to save time by installing visually pleasing, true type fonts, before installing a desktop environment/window manager. DejaVu is a set of high quality, general-purpose fonts.

Install with:

 `# pacman -S ttf-dejavu` 

*   Refer to [Font configuration](/index.php/Font_configuration "Font configuration") for how to configure font rendering and [Fonts](/index.php/Fonts "Fonts") for font suggestions and installation instructions.
*   Steps to install Microsoft fonts are detailed in the [MS Fonts](/index.php/MS_Fonts "MS Fonts") article.

#### Choose and install a graphical interface

The X Window System provides the basic framework for building a graphical user interface (GUI).

**Note:** Choosing your DE or WM is a very subjective and personal decision. Choose the best environment for _your_ needs.

Window Manager (WM) 

Controls the placement and appearance of application windows in conjunction with the X Window System. **See [Window managers](/index.php/Window_manager#Window_managers "Window manager") for more information.**

Desktop Environment (DE)

Works atop and in conjunction with X, to provide a completely functional and dynamic GUI. A DE typically provides a window manager, icons, applets, windows, toolbars, folders, wallpapers, a suite of applications and abilities like drag and drop. **See [Desktop environments](/index.php/Desktop_environment#Desktop_environments "Desktop environment") for more information.**

**Note:** You can build your own DE by using a WM and the applications of your choice.

After installing a graphical interface, you may wish to continue with [General recommendations](/index.php/General_recommendations "General recommendations") for post-installation instructions.

#### Methods for starting your Graphical Environment

##### Manually

You might prefer to start X manually from your terminal rather than booting straight into the desktop. For DE-specific commands, please see the wiki page corrosponding to your DE for more information. For more generic **X** commands, please see the [section on the Xorg page](/index.php/Xorg#Methods_for_starting_your_Graphical_Environment "Xorg").

##### Automatically

You might prefer to have the desktop start automatically during boot instead of starting X manually. See [Display manager](/index.php/Display_manager "Display manager") for instructions on using a login manager or [Start X at Boot](/index.php/Start_X_at_Boot "Start X at Boot") for two lightweight methods that do not rely on a display manager.

## Bilješke

Za listu [često korištenih](/index.php?title=Common_Applications_(Hrvatski)&action=edit&redlink=1 "Common Applications (Hrvatski) (page does not exist)") i [nezahtjevnih](/index.php?title=Lightweight_Applications_(Hrvatski)&action=edit&redlink=1 "Lightweight Applications (Hrvatski) (page does not exist)") aplikacija, posjeti njihove stranice.

Vidi [opće savjete](/index.php?title=General_Recommendations_(Hrvatski)&action=edit&redlink=1 "General Recommendations (Hrvatski) (page does not exist)") za vodiče nakon instalacije poput postavljanja skaliranja frekvencije procesora ili boljeg prikaza fontova.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Hrvatski)&oldid=411523](https://wiki.archlinux.org/index.php?title=Beginners%27_guide_(Hrvatski)&oldid=411523)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [About Arch (Hrvatski)](/index.php/Category:About_Arch_(Hrvatski) "Category:About Arch (Hrvatski)")
*   [Getting and installing Arch (Hrvatski)](/index.php/Category:Getting_and_installing_Arch_(Hrvatski) "Category:Getting and installing Arch (Hrvatski)")