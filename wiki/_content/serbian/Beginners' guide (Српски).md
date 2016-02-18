**Tip:** Ovo uputstvo je dostupno i u više zasebnih strana (modula), pre nego jedna velika kopija. Ako bi ste pre pratili uputstvo na taj način, molim vas počnite **[ovde](/index.php/Beginners%27_Guide/Preface_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Preface (Српски)")**.

| **Summary**  |
| Pruza vrlo detaljano i precizno uputstvo za instalaciju, konfigurisanje i upotrebu potpuno opremljenog Arch Linux sistema. |
| **Srodno** |
| [Official Arch Linux Install Guide (Српски)](/index.php/Official_Arch_Linux_Install_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Official Arch Linux Install Guide (Српски)") |
| [General Recommendations](/index.php/General_Recommendations "General Recommendations") |

## Contents

*   [1 Predgovor](#Predgovor)
    *   [1.1 Uvod](#Uvod)
    *   [1.2 Licenca](#Licenca)
    *   [1.3 Arch nacin](#Arch_nacin)
    *   [1.4 O ovom uputstvu](#O_ovom_uputstvu)
*   [2 Priprema](#Priprema)
    *   [2.1 Preuzimanje najskorijeg instalacionog medija](#Preuzimanje_najskorijeg_instalacionog_medija)
        *   [2.1.1 Provera integriteta preuzetog fajla](#Provera_integriteta_preuzetog_fajla)
        *   [2.1.2 CD instaler](#CD_instaler)
        *   [2.1.3 Flash memorijski uredjaj ili USB stik](#Flash_memorijski_uredjaj_ili_USB_stik)
            *   [2.1.3.1 *nix metod](#.2Anix_metod)
            *   [2.1.3.2 Microsoft Windows metod](#Microsoft_Windows_metod)
        *   [2.1.4 Instalacija preko mreze](#Instalacija_preko_mreze)
        *   [2.1.5 Instalacija na virtualnu masinu](#Instalacija_na_virtualnu_masinu)
    *   [2.2 Pokretanje Arch Linux instalera](#Pokretanje_Arch_Linux_instalera)
        *   [2.2.1 Pokretanje sa medija](#Pokretanje_sa_medija)
        *   [2.2.2 Startovanje OS-a](#Startovanje_OS-a)
            *   [2.2.2.1 Resavanje problema prilikom pokretanja sistema](#Resavanje_problema_prilikom_pokretanja_sistema)
        *   [2.2.3 Izmena rasporeda tastera](#Izmena_rasporeda_tastera)
        *   [2.2.4 Dokumentacija](#Dokumentacija)
*   [3 Instalacija osnovnog sistema](#Instalacija_osnovnog_sistema)
    *   [3.1 Izaberite izvor za instalaciju](#Izaberite_izvor_za_instalaciju)
        *   [3.1.1 Podesavanje mreze (Netinstall)](#Podesavanje_mreze_.28Netinstall.29)
            *   [3.1.1.1 (A)DSL brzi start za zivo okruzenje](#.28A.29DSL_brzi_start_za_zivo_okruzenje)
            *   [3.1.1.2 Bezicni internet - brzi start za zivo okruzenje](#Bezicni_internet_-_brzi_start_za_zivo_okruzenje)
    *   [3.2 Podesavanje sata](#Podesavanje_sata)
    *   [3.3 Pripremite hard diskove](#Pripremite_hard_diskove)
        *   [3.3.1 Particionisanje hard diskova](#Particionisanje_hard_diskova)
            *   [3.3.1.1 Partition Info](#Partition_Info)
            *   [3.3.1.2 Swap particija](#Swap_particija)
            *   [3.3.1.3 Sema za particionisanje](#Sema_za_particionisanje)
            *   [3.3.1.4 Koliko velike particije treba da napravim?](#Koliko_velike_particije_treba_da_napravim.3F)
            *   [3.3.1.5 Kreiranje particija sa cfdisk](#Kreiranje_particija_sa_cfdisk)
        *   [3.3.2 Podesavanje tacaka za montiranje fajl sistema](#Podesavanje_tacaka_za_montiranje_fajl_sistema)
            *   [3.3.2.1 Fajl sistem tipovi](#Fajl_sistem_tipovi)
            *   [3.3.2.2 Napomena u vezi zurnalizovanja](#Napomena_u_vezi_zurnalizovanja)
    *   [3.4 Izaberite pakete](#Izaberite_pakete)
    *   [3.5 Instalacija paketa](#Instalacija_paketa)
    *   [3.6 Konfigurisanje sistema](#Konfigurisanje_sistema)
        *   [3.6.1 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [3.6.1.1 LOCALIZATION sekcija](#LOCALIZATION_sekcija)
            *   [3.6.1.2 HARDWARE sekcija](#HARDWARE_sekcija)
            *   [3.6.1.3 NETWORKING sekcija](#NETWORKING_sekcija)
            *   [3.6.1.4 DAEMONS sekcija](#DAEMONS_sekcija)
        *   [3.6.2 /etc/fstab](#.2Fetc.2Ffstab)
        *   [3.6.3 **/etc/mkinitcpio.conf**](#.2Fetc.2Fmkinitcpio.conf)
        *   [3.6.4 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [3.6.5 /etc/resolv.conf](#.2Fetc.2Fresolv.conf)
        *   [3.6.6 /etc/hosts](#.2Fetc.2Fhosts)
        *   [3.6.7 /etc/hosts.deny and /etc/hosts.allow](#.2Fetc.2Fhosts.deny_and_.2Fetc.2Fhosts.allow)
        *   [3.6.8 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [3.6.9 Pacman-Odraz](#Pacman-Odraz)
        *   [3.6.10 Root sifra](#Root_sifra)
        *   [3.6.11 Gotovo](#Gotovo)
    *   [3.7 Install and configure a bootloader](#Install_and_configure_a_bootloader)
        *   [3.7.1 For BIOS motherboards](#For_BIOS_motherboards)
            *   [3.7.1.1 Syslinux](#Syslinux)
            *   [3.7.1.2 GRUB](#GRUB)
        *   [3.7.2 For UEFI motherboards](#For_UEFI_motherboards)
            *   [3.7.2.1 Gummiboot](#Gummiboot)
            *   [3.7.2.2 GRUB](#GRUB_2)
    *   [3.8 Restartujte](#Restartujte)
*   [4 Nakon instalacije](#Nakon_instalacije)
    *   [4.1 Osvezavanje](#Osvezavanje)
        *   [4.1.1 Podesavanje mreze (ako je neophodno)](#Podesavanje_mreze_.28ako_je_neophodno.29)
            *   [4.1.1.1 Zicni LAN (Lokalna mreza)](#Zicni_LAN_.28Lokalna_mreza.29)
            *   [4.1.1.2 Bezicni LAN (Lokalna mreza)](#Bezicni_LAN_.28Lokalna_mreza.29)
            *   [4.1.1.3 Proksi server](#Proksi_server)
            *   [4.1.1.4 Analogni modem, ISDN i DSL (PPPoE)](#Analogni_modem.2C_ISDN_i_DSL_.28PPPoE.29)
        *   [4.1.2 Osvezavanje, sinhronizacija i nadogradnja sistema sa pacman-om](#Osvezavanje.2C_sinhronizacija_i_nadogradnja_sistema_sa_pacman-om)
            *   [4.1.2.1 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
            *   [4.1.2.2 Repozitorijumi za pakete](#Repozitorijumi_za_pakete)
            *   [4.1.2.3 AUR](#AUR)
        *   [4.1.3 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
            *   [4.1.3.1 rankmirrors](#rankmirrors)
            *   [4.1.3.2 Provera odraza za aktuelne pakete](#Provera_odraza_za_aktuelne_pakete)
        *   [4.1.4 Bolje se upoznajte se pacman-om](#Bolje_se_upoznajte_se_pacman-om)
        *   [4.1.5 Osvezavanje sistema](#Osvezavanje_sistema)
            *   [4.1.5.1 Ignorisanje paketa](#Ignorisanje_paketa)
            *   [4.1.5.2 The Arch rolling release model (Arch-ov model novih verzija u letu)](#The_Arch_rolling_release_model_.28Arch-ov_model_novih_verzija_u_letu.29)
    *   [4.2 Dodavanje korisnika](#Dodavanje_korisnika)
        *   [4.2.1 Instalacija i podesavanje Sudo-a (Opciono)](#Instalacija_i_podesavanje_Sudo-a_.28Opciono.29)
*   [5 Dodatci](#Dodatci)
    *   [5.1 Zvuk](#Zvuk)
    *   [5.2 **G**raphical **U**ser **I**nterface (graficki korisnicki interfejs)](#Graphical_User_Interface_.28graficki_korisnicki_interfejs.29)
        *   [5.2.1 Instalacija X-a](#Instalacija_X-a)
        *   [5.2.2 Instalirajte video drajver](#Instalirajte_video_drajver)
            *   [5.2.2.1 NVIDIA Graficke karte](#NVIDIA_Graficke_karte)
            *   [5.2.2.2 ATI graficke kartice](#ATI_graficke_kartice)
        *   [5.2.3 Instalirajte drajvere za unos](#Instalirajte_drajvere_za_unos)
        *   [5.2.4 Podesavanje X-a(Opciono)](#Podesavanje_X-a.28Opciono.29)
            *   [5.2.4.1 Ne-US tastatura](#Ne-US_tastatura)
        *   [5.2.5 Testiranje X-a](#Testiranje_X-a)
            *   [5.2.5.1 Magistrala za poruke](#Magistrala_za_poruke)
            *   [5.2.5.2 Startujte X](#Startujte_X)
            *   [5.2.5.3 U slucaju gresaka](#U_slucaju_gresaka)
            *   [5.2.5.4 Treba vam pomoc?](#Treba_vam_pomoc.3F)
        *   [5.2.6 Instalijate fontove](#Instalijate_fontove)
        *   [5.2.7 Izaberite i instalirajte graficki interfejs.](#Izaberite_i_instalirajte_graficki_interfejs.)
        *   [5.2.8 Metode za startovanje vaseg grafickog okruzenja](#Metode_za_startovanje_vaseg_grafickog_okruzenja)
            *   [5.2.8.1 Rucno](#Rucno)
            *   [5.2.8.2 Automatski](#Automatski)
*   [6 Dodatak](#Dodatak)

## Predgovor

### Uvod

Dobrodosli. Ovaj dokument ce vas voditi kroz proces instaliranja [Arch Linux](/index.php/Arch_Linux "Arch Linux")-a: jednostavne, lake [GNU](/index.php/GNU_Project "GNU Project")/Linux distribucije namenjene kompetentnim korisnicima. Ovo uputstvo je namenjeno novim Arch korisnicima, ali tezi ka tome da bude jaka referenca i izvor informacija za sve.

Preporucujemo vam da predjete [Cesto postavljana pitanja](/index.php?title=FAQ_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "FAQ (Српски) (page does not exist)") pre instalacije.

**Prednosti Arch Linux distribucije:**

*   [Jednostavan](/index.php/The_Arch_Way_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "The Arch Way (Српски)") dizajn i filozofija
*   [Svi paketi](https://www.archlinux.org/packages/?q=) su kompajlirani za [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) i [x86_64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") arhitekture
*   [Rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release") model, koji omogucava da samo jednom instalirate sistem, a zatim ga azurirate u kontinuitetu i na taj nacin uvek imate najskorije stabilne verzije instaliranog softvera
*   [BSD stil](/index.php?title=Arch_Boot_Process_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Arch Boot Process (Српски) (page does not exist)") init skripti koji zastupa jedan centralizovani fajl za podesavanja
*   [mkinitcpio (Српски)](/index.php?title=Mkinitcpio_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Mkinitcpio (Српски) (page does not exist)") je jednostavan i dinamicki [initramfs](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd") kreator
*   [Pacman (Српски)](/index.php/Pacman_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Pacman (Српски)") [paket menadzer](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") je lagan i brz, sa vrlo malim memorijskim otiskom
*   [Arch Build System (Српски)](/index.php?title=Arch_Build_System_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Arch Build System (Српски) (page does not exist)"): Sistem za izgradnju paketa po ugledu na portove koji pruza jednostavan radni okvir za pravljenje Arch paketa iz izvornog koda.
*   [Arch User Repository (Српски)](/index.php/Arch_User_Repository_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Arch User Repository (Српски)"): pruza vise hiljada korisnickih skripti za izgradnju i mogucnost da podelite vase

### Licenca

Arch Linux, pacman, dokumentacija i skripte su Copyright © 2002-2007 by Judd Vinet, Copyright © 2007-2011 by Aaron Griffin i licencirani pod [GNU General Public License Version 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### Arch nacin

***Dizajn principi iza Arch-a imaju za cilj da ga ucine [jednostavnim](/index.php/The_Arch_Way_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "The Arch Way (Српски)").***

'Jednostavan', u ovom kontekstu, bi znacilo 'bez bespotrebnih dodataka, modifikacija ili komplikacija'. Ukratko; elegantan, minimalisticki pristup.

**Kada razmatrate jednostavnost, imajte sledece na umu:**

*   *" 'Jednostavno' je definisano sa tehnicke tacke gledista, a ne sa tacke gledista upotrebljivosti. Bolje je biti tehnicki elegantan sa visom krivom ucenja, nego biti lak za koriscenje i tehnicki [inferioran]." -Aaron Griffin*
*   *Entia non sunt multiplicanda praeter necessitatem* ili "Entitete ne bi trebalo umnozavati bespotrebno." -Occam's razor. Termin *razor* se odnosi na cin uklanjanja (brijanja) bespotrebnih komplikacija da se dodje do najjednostavnijeg objasnjenja, metode ili teorije.
*   *"Izuzetni deo [moje metode] lezi u jednostavnosti.. Visina kultivacije uvek tezi ka jednostavnosti."* - Bruce Lee

### O ovom uputstvu

Odrzavan od strane zajednice, [Arch wiki](/index.php/Main_Page_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Main Page (Српски)") je odlican izvor za resavanje problema. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanali ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) i ([irc://irc.freenode.net/#archlinux-rs](irc://irc.freenode.net/#archlinux-rs)), i [forumi](https://bbs.archlinux.org/) su takodje na raspolaganju ukoliko ne mozete da pronadjete odgovor. Posetite i `man` stranice za komande sa kojima niste upoznati; to mozete uciniti sa `man "komandom`*.*

**Note:** Pazljivo pracenje ovog uputstva je od kljucnog znacaja kako bi ste uspesno instalirali i podesili Arch Linux sistem, pa vas "molimo" da ga detaljno procitate. Jako je preporucljivo da procitate svaku sekciju u celosti <u>pre</u> obavljanja posla koji sekcija opisuje.

Uputstvo je podeljeno u 5 glavnih delova:

*   [Deo I: Priprema](#Preparation)
*   [Deo II: Instalacija](#Installation)
*   [Deo III: Nakon instalacije](#Post-Installation)
*   [Part IV: Dodaci](#Extra)
*   [Deo V: Prilog](#Appendix)

## Priprema

**Note:** Ukoliko zelite da instalirate na drugu particiju iz vec postojece distribucije ili LiveCD-a, molim vas pogledajte [ovaj wiki clanak](/index.php/Install_from_Existing_Linux "Install from Existing Linux") za neophodne korake. Ovo moze biti korisno, pogotovo ako planirate da instalirate Arch na udaljeni nacin preko [VNC](/index.php/VNC "VNC")-a ili [SSH](/index.php/SSH "SSH")-a. Uputstvo koje sledi pretpostavlja instalaciju na konvencionalan nacin.

### Preuzimanje najskorijeg instalacionog medija

[Ovde](https://archlinux.org/download/) mozete preuzeti Arch-ov oficijalni instalacioni medij. Najskorija verzija je 2011.08.19 i ovo uputstvo se odnosi na nju.

*   I **Core** i **Netinstall** slike pruzaju samo neophodne pakete za kreiranje **osnovnog Arch Linux sistema**. *Imajte na umu da Osnovni sistem ne sadrzi GUI. Primarno se sastoji od GNU toolchain-a (kompajlera, asemblera, linkera, biblioteka, shell-a i pomocnih alata), Linux kernel-a, pacman-a (Arch-ov paket menadzer) i nekoliko dodatnih biblioteka i modula.*
*   **Core** slike omogucavaju instalaciju sa CD-a i Interneta.
*   **Netinstall** slike su manje i ne sadrze pakete; ceo sistem se preuzima pre interneta.
*   [Arch64 FAQ](/index.php/Arch64_FAQ "Arch64 FAQ") vam moze pomoci u izboru izmedju 32-bitne i 64-bitne verzije. **Dual Architecture** slika ima pakete za obe arhitekture i sa njom mozete da instalirate Arch na 32-bitne i 64-bitne kompjutere.
*   Preuzmite i checksum txt fajlove zajedno sa izabranim ISO fajlom.

Dostupne su i beta slike koje se [ovde](https://releng.archlinux.org/isos/) mogu preuzeti. **Ovo nisu oficijalna izdanja i nisu oficijalno podrzana.** Treba ih koristiti samo ako oficijalne instalacione slike ne rade na vasem hardveru i verujete da ce novije slike imati odgovarajuce drajvere.

#### Provera integriteta preuzetog fajla

`cd` do direktorijuma gde se nalaze preuzeti fajlovi, a zatim `sha1sum`:

 `$ sha1sum --check ime_checksum_fajla.txt` 

Trebalo bi da dobijete "OK". (Ignorisite ostale linije). U suprotnom preuzmite ponovo sve fajlove.

md5sum provera radi na isti nacin.

#### CD instaler

Narezite fajl .iso slike na CD ili DVD medij sa CD/DVD rezacem i softverom, a zatim nastavite sa [Podizanje Arch Linux instalera](#Boot_Arch_Linux_installer).

**Note:** Kvalitet optickih uredjaja i CD medija varira u velikoj meri. Preporucuje se rezanje na manjim brzinama kako bi dobili pouzdane rezultate; Neki korisnici preporucuju brzine ***kao sto su 4x ili 2x.*** Ako imate problema sa CD-om, pokusajte da narezete na najmanjoj mogucoj brzini.

#### Flash memorijski uredjaj ili USB stik

Vidite [Instalacija sa USB flash diska](/index.php/Install_from_a_USB_flash_drive "Install from a USB flash drive") za detaljnija uputstva.

Ovaj metod radi za bilo koju vrstu flash medija sa koje vas BIOS moze da pokrene sistem, bilo da je to citac kartica ili USB port.

Znajte da ce svi podaci na prenosivom mediju biti nepovratno unisteni!

##### *nix metod

**Warning:** Budite pazljivi po pitanju toga gde saljete ISO sliku, jer `dd` ce poslusno pisati na bilo koju metu na koju ga usmerite, cak i ako je to vas hard disk (a to moze uzrokovati gubitak podataka i/ili korumpirani fajl sistem).

Ubacite prazan ili potrosivi flash uredjaj, odredite mu adresu, a zatim napisite .iso na uredjaj sa `dd` programom:

 `# dd if=archlinux-2011.08.19-''{core|netinstall}''-''{i686|x86_64|dual}''.iso of=/dev/sd''x''` 

gde je `if=` staza do .iso fajla, a `of=` je flash uredjaj. Upotrebite `/dev/sd**x**`, a ne `/dev/sd**x1**`. Trebace vam flash uredjaj koji je dovoljno velik da smesti sliku.

Da potvrdite da je slika uspesno zapisana na flash uredjaj, zabelezite broj zapisa (blokova) koji su zapisani u i iscitani iz (read in, written out), a zatim izvrsite sledecu proveru:

 `# dd if=/dev/sd''x'' count=''broj_zapisa'' status=noxfer | md5sum` 

Povratni md5sum bi trebalo da se poklopi sa [md5sum-om preuzete archlinux slike (2011.08.19)](https://www.archlinux.org/iso/2011.08.19/md5sums.txt); oba bi trebalo da se poklope sa md5sum-om slike kao sto je izlistano u md5sums fajlu na distribucionom sajtu za slike. Tipican slucaj ce izgledati ovako:

Zapis .iso fajla na disk

 `# dd if=archlinux-2011.08.19-core-i686.iso of=/dev/sdc` 
```
 744973+0 records in
 744973+0 records out
 381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s

```

Provera integriteta:

 `# dd if=/dev/sdc count=744973 status=noxfer | md5sum` 
```
 4850d533ddd343b80507543536258229  -
 744973+0 records in
 744973+0 records out
```

Nastavite sa [Podizanje Arch Linux instalera](#Boot_Arch_Linux_installer)

##### Microsoft Windows metod

[Ovde](https://launchpad.net/win32-image-writer/+download) preuzmite program za rezanje slika. Prikljucite flash medij. Startujte program za rezanje slika i izaberite sliku (ovaj program prihvata samo *.img fajlove, pa cete morati da stavite "*.iso" u dijalogu za otvaranje fajla da bi izabrali Arch snimak). Izaberite slovo diska koje se odnosi na flash uredjaj. Kliknite "Write".

Postoje i drugi nacini za [pisanje butabilnih ISO slika na USB uredjaje](/index.php/Install_from_a_USB_flash_drive#On_Windows "Install from a USB flash drive"). Ako imate problem da se USB uredjaj iskljucuje, probajte drugi USB port i/ili kabl.

Nastavite sa [Podizanje Arch Linux instalera](#Boot_Arch_Linux_installer).

#### Instalacija preko mreze

Umesto nasnimavanja boot medija na disk ili USB uredjaja, postoji mogucnost podizanja .iso slike preko mreze. Ovo funkcionise ako vec imate podeseni server. Vidite [ovaj clanak](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") za vise informacija, a zatim nastavite sa [Podizanje Arch Linux instalera](#Boot_Arch_Linux_installer).

#### Instalacija na virtualnu masinu

Instalacija na [virtualnu masinu](https://en.wikipedia.org/wiki/Virtual_machine "wikipedia:Virtual machine") je odlican nacin za upoznavanje sa Arch Linux-om i njegovom instalacionom procedurom bez napustanja vaseg sadasnjeg operativnog sistema i reparticionisanja hard diska. Ova opcija pruza i mogucnost otvaranja Uputstva za pocetnike u internet pretrazivacu tokom instalacije. Pojedini korisnici koriste nezavisni Arch Linux sistem na virtualnoj masini za svrhu testiranja.

Primeri softvera za virtualizaciju su [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

Tacna procedura pripreme virtualne masine zavisi od softvera, ali generalno se sastoji od sledecih koraka:

1.  Pravljenje virtualnog diska koji ce hostovati operativni sistem.
2.  Ispravno podesavanje parametara virtualne masine.
3.  Pokretanje preuzete .iso slike sa virtualne CD jedinice.
4.  Nastavite sa [Pokretanje Arch Linux instalera](#Boot_Arch_Linux_installer).

Sledeci clanci mogu biti od pomoci:

*   [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")

### Pokretanje Arch Linux instalera

**Tip:** Neophodna memorija za osnovnu instalaciju je 64MB RAM-a.

**Tip:** Tokom procesa se moze upaliti automatski zatamnjivac ekrana. Pritisnite Alt da ponovo upalite ekran.

#### Pokretanje sa medija

Ubacite CD ili flash medij koji ste pripremili i pokrenite sistem sa njega. Prethodno promenite u BIOS-u redosled uredjaja sa kog se pokrece sistem. Da uradite to, pritisnite `Delete`, `F1`, `F2`, `F11` ili `F12`) tokom POST (Power On Self-Test) faze.

**Glavni meni:** Trebalo bi da vidite glavni meni. Izaberite jednu od ponudjenih opcija upotrebom strelica na tastaturi i pritiskom na `Enter`. Meniji blago variraju medju ISO slikama.

#### Startovanje OS-a

Izaberite "Boot Arch Linux" iz glavnog menija i pritisnite `Enter` da bi zapoceli instalaciju. Sistem ce ucitati i prikazati komandnu liniju. Bicete automatski ulogovani kao root.

**Note:** Korisnicima koji zele da instaliraju Arch Linux na udaljeni nacin preko [SSH](/index.php/SSH "SSH") konekcije se preporucuje da naprave nekoliko podesavanja u ovom momentu kako bi omogucili SSH konekcije direktno u live CD okruzenje. Za vise informacija pogledajte [Instalacija iz SSH-a](/index.php/Install_from_SSH "Install from SSH").

##### Resavanje problema prilikom pokretanja sistema

Ako koristite Intel video chipset i ekran je crn tokom pokretanja sistema, problem je najverovatnije vezan za podesavanje kernel mode-a. Moguce resenje je restartovanje i pritisak na `Tab` na GRUB meniju da udjete u kernel opcije. Na kraju kernel linije dodajte sledece:

```
i915.modeset=0

```

Mozete dodati i:

```
video=SVIDEO-1:d

```

koji (ako radi) nece iskljuciti kernel mode podesavanja.

Vidite [Intel](/index.php/Intel "Intel") clanak za vise informacija.

Ako ekran *nije* crn i proces pokretanja se zaglavljuje prilikom ucitavanja kernela, pritisnite `Tab` da izmenite kernel liniju i dodate sledece:

```
acpi=off

```

Kada ste zavrsili sa izmenama, pritisnite `Enter` da pokrenete sistem za napravljenim izmenama.

#### Izmena rasporeda tastera

Ako imate ne-US raspored tastera, mozete na interaktivan nacin da izaberete raspored tastera/konzolni font sa komandom:

 `# km` 

ili upotrebite loadkeys komandu:

 `# loadkeys *layout*` 

gde je *layout* raspored vase tastature, kao sto su `fr` ili `be-latin1`

#### Dokumentacija

Oficijalno uputstvo za instalaciju (koji je zaseban dokument) je dostupno na live sistemu. Da mu pristupite, predjite na tty2 (virtualnu konzolu #2) sa `Alt+F2` i ulogujte se kao root. Ovde mozete da upotrebite `less` da izlistate dokument:

 `# less /usr/share/aif/docs/official_installation_guide_en` 

Vratite se na tty1 sa `Alt+F1` da ispratite ostatak instalacionog procesa. Mozete u bilo kom momentu da se vratite na tty2 ako vam ponovo zatrebaju informacije iz zvanicnog uputstva (Official Guide), kako budete napredovali kroz proces instalacije.

**Tip:** Imajte na umu da zvanicno uputstvo pokriva samo instalaciju i podesavanje osnovnog sistema. Preporucljivo je da se, nakon njegove instalacije, okrenete informacijama na wiki-ju u vezi post-instalacionih detalja i drugih pitanja.

## Instalacija osnovnog sistema

Kao root korisnik, pokrenite instalacionu skriptu sa tty1:

```
# /arch/setup

```

Trebalo bi da vidite Arch Linux frejmvork ekran.

### Izaberite izvor za instalaciju

Nakon ekrana za dobrodoslicu, bicete upozoreni za instalacioni izvor. Izaberite odgovarajuci izvor za instaler koji koristite. Ako koristite odraz za instalaciju preko interneta, relativna brzina i svezina paketa u repozitorijumima moze biti proverena [here](https://www.archlinux.de/?page=MirrorStatus).

*   Ako izaberete CORE instaler i zelite da koristite pakete sa CD-a, izaberite CD-ROM kao izvor
*   Alternativno, ako koristite net-instalacioni medij, izaberite NET i pogledajte sekciju ispod ([Podesavanje mreze](#Configure_Network_.28Netinstall.29)).

#### Podesavanje mreze (Netinstall)

Bicete obavesteni da ucitate ethernet drajvere rucno, ako zelite. Udev je prilocno efikasan kada je ucitavanje neophodnih modula u pitanju, tako da mozete da pretpostavite da je to vec uradio. Na sledecem ekranu, izaberite "Setup Network". Mozete potvrditi ovo pritiskom na <Alt>+F3 i pokretanjem ifconfig-a. Nakon toga se vratite na tty1 pritiskom na <Alt>+F1.

Dostupni interfejsi ce se pojaviti. Ako su jedan interfejs i HWaddr (**H**ard**W**are **addr**ess) izlistani, onda je vas modul vec ucitan. Ako vas interfejs nije izlistan, mozete da uradite probe iz instalera ili da to rucno uradite iz druge virtualne konzole. Izaberite vas interfejs da bi nastavili.

Instaler ce vas zatim upitati da li zelite da koristite DHCP. Ako izaberete Yes, to ce pokrenuti **dhcpcd** da pronadje dostupni gateway i da izda zahtev za IP adresom; Izborom No opcije cete biti upitani za vasu staticku IP adresu, netmask, broadcast, gateway DNS IP, HTTP proxy i FTP proxy. Nakon toga bicete vraceni na *Net instalacioni meni*

Izaberite *Choose Mirror* i selektujte FTP/HTTP odraz. Kada zavrsite, vratite se na glavni meni.

**Note:** archlinux.org je usporen na 50KB/s

##### (A)DSL brzi start za zivo okruzenje

(Ako imate modem ili ruter u bridge modu za konektovanje na vaseg ISP-a)

Predjite na drugu virtualnu konzolu (<Alt> + F2), ulogujte se kao root i pokrenite

```
# pppoe-setup

```

Ako je sve dobro konfigurisano na kraju, mozete da se povezete sa ISP-om sa

```
# pppoe-start

```

Vratite se na prvu virtualnu konzolu sa <ALT>+F1\. Nastavite sa [Podesavanje sata](#Set_Clock)

##### Bezicni internet - brzi start za zivo okruzenje

(Ako imate pristup bezicnom internetu tokom instalacionog procesa)

Drajveri za bezicni internet i pomocni programi su vam dostupni u zivom okruzenju instalacionog medija. Dobro poznavanje vaseg hardvera za bezicni internet ce biti od kljucnog znacaja za uspecno konfigurisanje. Imajte na umu da ce sledeca procedura za brzi start, "obavljena u ovom momentu u instalaciji", inicijalizovati vas hardver za bezicni internet za upotrebu "u zivom okruzenju instalacionog medija". Ovi koraci (ili neki drugi oblik upravljanja vajrles-om) moraju biti ponovljeni iz instaliranog sistema nakon njegovog startovanja.

Takodje znajte da su ovi koraci opcioni ukoliko vajrles konekcija nije neophodna u ovom momentu u okviru instalacije; vajrles funkcionalnost moze biti uspostavljena kasnije bez problema.

**Note:** Sledeci primeri koriste wlan0 za interfejs i 'linksys' za ESSID. Zapamtite da promenite ove u skladu sa vasom situacijom.

Osnovna procedura je:

*   Predjite na slobodnu virtualnu konzolu , npr.: <ALT>+F3
*   Ulogujte se kao root
*   (Opciono) identifikujte bezicni interfejs:

```
# lspci | grep -i net

```

*   Proverite da je udev ucitao drajver i da je drajver kreirao upotrebljiv vajrles kernel interfejs sa `/usr/sbin/iwconfig`:

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

`wlan0` je dostupni interfejs za vajrles (bezicni internet) u ovom primeru.

**Note:** Ako ne vidite izlaz slican ovom, onda vas vajrles drajver nije ucitan. U tom slucaju morate da ucitate drajver sami. Pogledajte [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") za vise detaljnih informacija.

*   Podignite (startujte) interfejs sa `/sbin/ifconfig <interface> up`.

```
# ifconfig wlan0 up

```

Mali procenat vajrles cipova zahteva i firmver, kao dodatak odgovarajucem drajveru. Ako vajrles cipovi zahtevaju firmver, verovatno cete dobiti ovu gresku prilikom podizanja interfejsa:

 `# ifconfig wlan0 up`  `SIOCSIFFLAGS: No such file or directory` 

Ako niste sigurni, pokrenite `/usr/bin/dmesg` da upitate kernel log da li su vajrles cipovi izdali zahtev za firmver. Primer izlaza za jedan Intel skup cipova koji su zatrazili firmver od kernela prilikom startovanja sistema:

 `$ dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Ako ne postoji izlaz, moze se zakljuciti da vajrles cipset ne zahteva firmver.

**Note:** **Firmver paketi za vajrles cipove (za kartice koje ih zahtevaju) su unapred instalirani pod /lib/firmware u zivom okruzenju (na CD/USB stiku) *ali moraju biti eksplicitno instalirani na vas sistem da pruze funkcionalnost vajrlesa nakon sto restartujete u sistem!* Selekcija i instalacija paketa je pokrivena kasnije u ovom uputstvu. Obezbedite instalaciju vajrles modula i firmvera tokom koraka selekcije paketa! Pogledajte [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") ako niste sigurni oko zahteva odgovarajuceg firmvera za vas specificni skup cipova. Ovo je vrlo cesta greska.**

*   Ako je ESSID zaboravljen ili je nepoznat, upotrebite `/sbin/iwlist <interface> scan` da skenirate mreze u okruzenju.

```
# iwlist wlan0 scan

```

*   Ako mreza ima WPA enkripciju:

Upotreba WPA enkripcije zahteva da kljuc bude enkriptovan i skladisten u fajlu, zajedno sa ESSID-om, da bi mogao kasnije da se upotrebi za konekciju preko `wpa_supplicant`. Usled toga, nekoliko dodatnih koraka je neophodno:

Za svrhu pojednostavljenja i rezervne kopije, preimenujte pocetni wpa_supplicant.conf fajl:

```
# mv /etc/wpa_supplicant.conf /etc/wpa_supplicant.conf.original

```

Upotrebom `wpa_passphrase`, omogucite vasoj vajrles mrezi i WPA kljucu da bude enkriptovan i zapisan u /etc/wpa_supplicant.conf

Sledeci primer enkriptuje kljuc 'my_secret_passkey' od 'linksys' vajrles mreze, generise novi konfiguracioni fajl (<file>/etc/wpa_supplicant.conf</file>), i and zatim preusmerava enkriptovani kljuc, zapisujuci ga u fajl:

```
# wpa_passphrase linksys "my_secret_passkey" > /etc/wpa_supplicant.conf

```

Proverite [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") za vise informacija i resavanje eventualnih problema.

**Note:** /etc/wpa_supplicant.conf se nalazi u obicnom tekst formatu. Ovo nije rizicno u instalacionom okruzenju, ali nakon restarta u vas novi sistem i rekonfigurisanja WPA, ne zaboravite da promenite dozvole na /etc/wpa_supplicant.conf (e.g. `chmod 0600 /etc/wpa_supplicant.conf` da ga ucinite citljivim samo za root korisnika).

*   Povezite vas vajrles uredjaj sa pristupnom tackom koju zelite da koristite. U zavisnosti od enkripcije (none, WEP, ili WPA), procedura moze da varira. Morate da znate ime izabrane vajrles mreze (ESSID).

| Enkripcija | Komanda |
| Bez enkripcije | `iwconfig wlan0 essid "linksys"` |
| WEP w/ Hex kljuc | `iwconfig wlan0 essid "linksys" key "0241baf34c"` |
| WEP w/ ASCII lozinka | `iwconfig wlan0 essid "linksys" key "s:pass1"` |
| WPA | `wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf` |

**Note:** Proces konektovanja na mrezu moze biti automatizovan kasnije upotrebom Arch mreznog daemon-a, [netcfg](/index.php/Netcfg "Netcfg"), [wicd](/index.php/Wicd "Wicd"), ili drugog mreznog menadzera prema vasem izboru.

*   Nakon primene odgovarajuce metode udruzenja, navedene gore, sacekajte nekoliko trenutaka i proverite da ste uspesno udruzeni sa pristupnom tackom nakon sto nastavite. Npr.:

```
# iwconfig wlan0

```

Izlaz bi trebao da nagovesti da je vajrles mreza udruzena sa interfejsom.

*   Zahtevajte IP adresu sa `/sbin/dhcpcd <interface>` . npr.:

```
# dhcpcd wlan0

```

*   Na kraju, uverite se da mozete da rutirate upotrebom `/bin/ping`:

```
# ping -c 3 www.google.com

```

Trebalo bi da imate mreznu konekciju koja radi. Za resavanje eventualnih problema, proverite detaljniju [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") stranicu.

Vratite se na tty1 sa <ALT>+F1\. Nastavite sa [Podesavanje sata](#Set_Clock)

### Podesavanje sata

*   UTC - Izaberite UTC ako koristite samo `UNIX`-olike operativne sisteme.

*   localtime - izaberite local ako pokrecete i Microsoft Windows OS uporedo.

### Pripremite hard diskove

**Warning:** Particionisanje hard diskova moze unistiti podatke. Upozoravamo vas da napravite kopiju vasih vaznih podataka pre nego sto nastavite.

**Note:** Particionisanje moze biti obavljeno pre pokretanja Arch instalacije, ako zelite, upotrebom [GParted](http://gparted.sourceforge.net/download.php) ili drugih dostupnih alata. Ako je instalacioni disk vec particionisan prema neophodnim specifikacijama, nastavite sa [Podesavanje tacaka za montiranje fajl sistema](#Set_Filesystem_Mountpoints)

Proverite trenutni raspored na disku i identitete pokretanjem `/sbin/fdisk` sa `-l` (malo L) prekidacem.

Otvorite drugu virtualnu konzolu (<ALT>+F3) i unesite:

```
# fdisk -l

```

Zabelezite disk/particiju koju cete upotrebiti za Arch instalaciju.

Predjite nazad na instalacionu skriptu sa <ALT>+F1

Izaberite prvu opciju na meniju "Prepare Hard Drive".

*   Opcija1: Auto-Prepare (Brise ceo hard disk i podesava particije)

Auto-Prepare deli disk na sledecu konfiguraciju:

*   ext2 /boot paricija, pocetna velicina 32MB. *Bicete upitani da modifikujete velicinu prema vasim potrebama.*
*   swap paricija, pocetna velicina 256MB. *Bicete upitani da modifikujete velicinu prema vasim potrebama.*
*   Odvojena / i /home particija, (velicina isto mogu biti zadate). Dostupni fajl sistemi su ext2, ext3, ext4, reiserfs, xfs and jfs, ali zapamtite da *oba / i /home ce deliti isti fajl sistem tip* ako izaberete Auto Prepare opciju.

Znajte da ce Be Auto-prepare kompletno obrisate izabrani hard disk. Procitajte <font color="red">upozorenje</font> prikazano od strane instalera veoma pazljivo i uverite se da je ispravan uredjaj selektovan za particionisanje.

*   Opcija 2: Rucno particionisanje hard diskova (sa cfdisk)- preporucljivo.

Ova opcija ce vam dozvoliti najrobustnije particionisanje hard diskova prema vasim potrebama.

*   Opcija 3: Rucno konfigurisanje blok uredjaja, fajl sistema i tacaka za montiranje

Ako je ovo selektovano, sistem ce listati fajl sisteme i tacke za montiranje koje je pronasao i pitati vas ako zelite da ih upotrebite. Ako izaberete "Yes", bice vam dat izbor da selektujete zeljenu metodu identifikacije, prema dev, label ili uuid.

*   Opcija 4: Vracanje zadnjih fajl sistem izmena

*U ovom momentu, napredniji GNU/Linux korisnici koji su upoznati i opusteni kada je rucno particionisanje u pitanju, mogu preskociti dole na **[Selektovanje paketa](#Select_Packages)** ispod.*

**Note:** Ako instalirate na USB fles, pogledajte "[Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")".

#### Particionisanje hard diskova

##### Partition Info

Particionisanje hard diskova definise odredjene oblasti (particije) u okviru diska, od kojih ce se svaka pojavljivati i ponasati se kao zaseban disk i na kojima se mogu kreirati razliciti fajl sistemi (formatiranje).

*   Postoji 3 vrste disk particionisanja:

1.  Primary (primarna)
2.  Extended (prosirena)
3.  Logical (logicka)

**Primary** particije mogu biti butabilne, i ogranicene su na 4 particije po disku ili raid-u. Ako sema za particionisanje zahteva vise od 4 particije, jedna "extended" particija koja ce sadrzati "logical" particije ce biti neophodna.

Prosirene (extended) particije nisu upotrebljive same po sebi; one su zapravo "kontejner" za logicke particije. Ako je neophodno, hard disk ce sadrzati samo jednu prosirenu (extended) particiju; koja ce zatim biti podeljenja na logicke particije.

Kada particionisete disk, mozete da posmatrate ovu semu za brojanje tako sto cete napraviti primarne particije sda1 do sda3 praceno sa kreiranjem jedne extended (prosirene) particije, sda4, a zatim da kreirate logicke particije u okviru prosirene (extended) particije; sda5, sda6, i tako dalje.

##### Swap particija

Swap particija je mesto na hard disku gde obitava ram memorija, pruzajuci kernelu da na lak nacin koristi hard disk za one podatke za koje nema mesta u fizickoj RAM memoriji.

Istorijski, generalno pravilo za velicinu swap particije je bilo 2x iznos fizickog RAM-a. Tokom vremena, kako su racunari dobijali sve vece kapacitete memorije, ovo pravilo je postalo zastarelo. Generalno, na masinama sa vise od 512MB RAM-a, pravilo 2x je obicno sasvim dovoljno. Ako instalaciona masina pruza veci iznos rama (vise od 1024 MB), vrlo lako mozete kompletno da zaboravite na swap particiju, jer je opcija za kreiranje [swap fajl](/index.php/HOW_TO:_Create_swap_file "HOW TO: Create swap file") uvek dostupna kasnije. 1 GB swap particija ce biti upotrebljena u ovom slucaju.

**Note:** Ako koristite suspend-to-disk, (hibernacija) swap particija bar **jednaka** u velicini sa ukupnim iznosom fizikog RAM-a je neophonda. Neki Arch korisnici su cak preporucili pravljenje vecih swap particija od fizickog RAM-a za nekih 10-15%, da bi obezbedili prostor za eventualne lose sektore.

##### Sema za particionisanje

Sema za particionisanje diska je zasebna za svaku osobu. Izbor svakog korisnika ce biti jedisntven u skladu sa njihovim licnim navikama i potrebama u koriscenju racunara. Ako zelite da imate dupli boot izmedju Arch Linux-a i Windows operativnog sistema molim vas pogledajte [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot").

Fajl sistem kandidati za zasebne particije obuhvataju:

**/** (root) *Root fajl sistem je primarni fajl sistem iz kog se svi ostali fajl sistemi granaju; vrh hijerarhije. Svi fajlovi i direktorijumi se pojavljuju pod "/", cak i ako su skladisteni na drugim fizickim uredjajima. Sadrzaji root fajl sistema moraju biti adekvatni za startovanje, povratak, oporavak i/ili popravku sistema. Tako da odgovarajuci direktorijumi pod / nisu sami za sebe kandidati za zasebne particije. (Pogledajte upozorenje ispod)."*

**/boot** *Ovaj direktorijum sadrzi kernel i ramdisk odraze i konfiguracioni fajl za bootloader, i bootloader faze. /boot takodje skladisti podatke koji se koriste pre nego sto kernel pocne sa izvrsavanjem programa za korisnicki prostor. Ovo moze da sadrzi cuvanje master boot sektora i sektor map fajlova. /boot je od vitalnog znacaja za startovanje, ali je jedinstven po tome sto moze biti skladisten na svojoj zasebnoj particiji (ukoliko je neophodno)."*

**/home** *Pruza poddirektorijume, svaki imenovan za korisnika sistema, za skladistenje raznih licnih podataka kao i konfiguracionih fajlova za aplikacije na nivou korisnika.*

**/usr** *Dok je root primarni fajl sistem, /usr je sekundarna hijerarhija za sve podatke sistem korisnika, ukljucujuci vecinu visekorisnickih pomocnih programa i aplikacija. /usr je upotrebljiv od strane vise korisnika i dozvoljeno je samo njegovo citanje. To znaci da ce /usr biti deljiv izmedju nekoliko razlicitih hostova i u njega ne sme biti pisano, osim u slucaju osvezavanja/nadogradnje sistema. Svaka informacija koja je specificna za hosta ili varira po pitanju vremena je skladistena na nekom drugom mestu."*

**/tmp** *direktorijum za programe koji zahtevaju privremene fajlove poput '.lck' fajlova, koji se mogu koristiti za sprecavanje vise instanci njihovog odgovarajuceg programa sve dok posao nije zavrsen, u kom momentu ce '.lck' fajl biti uklonjen. Programi ne smeju pretpostaviti da su bilo koji fajlovi ili direktorijumi u /tmp sacuvani izmedju pokretanja programa i fajlovi i direktorijumi locirani pod /tmp ce tipicno biti obrisati svaki put kad se sistem restartuje.*

**/var** *sadrzi varijabilne podatke; spool direktorijume i fajlove, administrativne i login podatke, kes od pakmena, ABS drvo, itd. /var postoji da bi omogucio montiranje /usr kao samo-citljivog. Sve sto kroz istoriju ide u /usr, a zapisano je tokom operacija sistema (u odnosu na instalaciju i odrzavanje softvera) mora obitavati pod /var.*

**Warning:** Pored /boot, direktorijumi od vitalnog znacaja za startovanje su: '***/bin', '/etc', '/lib', and '/sbin'. Tako da, oni ne smeju obitavati na odvojenim particijama od /.***

***Postoji nekoliko prednosti za koriscenje diskretnih fajl sistema, pre nego ih kombinovati sve na jednu particiju***:

*   Bezbednost: Svaki fajlsistem moze biti podesen u /etc/fstab kao 'nosuid', 'nodev', 'noexec', 'readonly', itd.
*   Stabilnost: Korisnik, ili program koji ne funkcionise mogu kompletno da popune fajl sistem sa smecem ako ne imaju dozvole za pisanje da to ucine. Kriticni programi, koji obitavaju na razlicitim fajl sistemima ne trpe ovaj uticaj.
*   Brzina: Fajl sistem na koji se pise cesto moze postati fragmentovan. (Efikasan metod izbegavanja fragmentacije je da obezbedite da fajl sistemi nikad ne dodju u opasnost od potpunog popunjavanja.) Zasebni fajl sistemi ne trpe ovaj uticaj, i svaki moze biti defragmentovan odvojeno za sebe.
*   Integritet: Ako jedan fajl sistem postane korumpiran, odvojeni fajl sistemi nemaju taj problem.
*   Prilagodljivost: Deljenje podataka preko nekoliko sistema postaje celishodno kada su nezavisni fajl sistemi u upotrebi. Zasebni fajl sistem tipovi mogu isto biti izabrani bazirano na prirodi podataka i upotrebi.

U ovom primeru, mi cemo koristiti odvojene particije za /, /var, /home, i swap particije.

**Note:** /var sadrzi mnogo malih fajlova. Ovo treba uzeti u obzir kada birate fajl sistem tip za njega, (ako kreirate njegovu zasebnu particiju).

##### Koliko velike particije treba da napravim?

Ovo pitanje se najbolje odgovara bazirano na individualnim potrebama. Mozda cete zeleti da prosto kreirate **jednu particiju za root i jednu particiju za swap ili samo jednu root particiju bez swap-a** ili pogledajte sledece primere i razmotrite smernice da obezbedite referentni okvir:

*   Root fajl sistem (/) u primeru ce stadrzati /usr direktorijum, koji ce postati srednje velik, u zavisnosti od toga koliko softvera je instalirano. 15-20 GB bi trebalo da bude dovoljno za vecinu korisnika.

*   /var fajl sistem ce sadrzati, pored ostalih podataka, [ABS](/index.php/ABS "ABS") drvo i pacman kes. Cuvanje kesiranih paketa je korisno i pruza mogucnost prilagodljivosti; pruza mogucnost da unazadite pakete ako je neophodno. /var tezi da raste u velicini; pacman kes moze narasti velik tokom dugog vremenskog perioda, ali moze biti bezbedno ociscen ukoliko je neophodno. Ako koristite SSD, mozete da locirate vas /var na hard disku i da drzite / i /home particije na vasem SSD-u da bi ste izbegli besportrebno citanje/pisanje na SSD. 8-12 gigabajta na desktop sistemu bi trebalo da bude dovoljno za /var, u zavisnosti od toga koliko softvera nameravate da instalirate. Serveri teze da imaju relativno vece /var fajl sisteme.

*   The /home fajl sistem je tipicno gde se nalaze korisnicki podaci, download-i, i multimedija. Na desktop sistemu, /home je tipicno najveci fajl sistem na hard disku. Zapamtite da ako izaberete da reinstalirate Arch, svi podaci na vasoj /home particiji ce biti netaknuti (sve dok imate zasebnu /home particiju).

*   Dodatnih 25% prostora dodatih na svaki fajl sistem ce pruziti prostor za nepredvidjene slucajeve, prosirenje, i moze posluziti kao preventiva za fragmentaciju.

***Iz gornjih uputstava, primer sistema ce sadrzati ~15GB root (/) particiju, ~10GB /var, 1GB swap i /home koji sadrzi ostatak prostora.***

##### Kreiranje particija sa cfdisk

Startujte sa kreiranjem primarne particije koja ce sadrzati **root**, (/) fajlsistem.

Izaberite **N**ew -> Primary i unesite zeljenu velicinu za root (/). Stavite particiju na pocetak diska.

Takodje izaberite **T**ype obelezavanjem na '83 Linux'. Kreirana / particija ce se pojaviti kao sda1 u nasem primeru.

Sada kreirajte primarnu particiju za /var, obelezavanjem **T**ype 83 Linux. Kreirana /var particija ce se pojaviti kao sda2.

Sledece, kreirajte particiju za swap. Izaberite odgovarajucu velicinu i zadajte **T**ype kao 82 (Linux swap / Solaris). Kreirana particija ce se pojaviti kao sda3.

Na kraju, kreirajte particiju za vas /home direktorijum. Izaberite drugu primarnu particiju i podesite zeljenu velicinu.

Takodje, izaberite **T**ype kao 83 Linux. Kreirana /home particija ce se pojaviti kao sda4.

Primer:

```
Name    Flags     Part Type    FS Type           [Label]         Size (MB)
-------------------------------------------------------------------------
sda1               Primary     Linux                             15440 #root
sda2               Primary     Linux                             10256 #/var
sda3               Primary     Linux swap / Solaris              1024  #swap
sda4               Primary     Linux                             140480 #/home

```

Izaberite **W**rite i napisite '**yes'**. Budite na oprezu da ova operacija moze da unisti podatke na vasem disku. Izaberite **Q**uit da napustite particioner. Izaberite Done da napustite meni i nastavite sa "Podesavanje tacaka za montiranje fajl sistema".

**Note:** Od zadnjeg razvoja Linux kernela koji sadrzi libata i PATA module, svi IDE, SATA i SCSI diskovi su usvojili sd*x* sistem imenovanja. Ovo je savrseno normalno i ne treba da bude briga.

#### Podesavanje tacaka za montiranje fajl sistema

Zadajte svaku particiju i odgovarajucu tacku za montiranje prema vasim potrebama. (Setite se da se particije zavrsavaju sa brojem. Tako da , **sda** nije sama po sebi particija, vec oznacava ceo disk).

##### Fajl sistem tipovi

Opet, fajl sistem tip je vrlo subjektivna stvar koja se zasniva na licnom izboru. Svaka ima svoje prednosti, nedostatke i jedinstvene atribute. Kratak pregled podrzanih fajl sistema:

1\. [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") *Second Extended Filesystem*- Stari, pouzdani GNU/Linux fajl sistem. Vrlo stabilan, ali *bez podrzke za zurnalizovanja*. Moze biti nepogodna za root (/) i /home, zbog vrlo dugackog fsck-a (dugacke provere fajl sistema). ext2 fajl sistem moze lako biti konvertovan u ext3.

2\. [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") *Third Extended Filesystem*- U sustini ext2 sistem, ali sa podrskom za zurnalizovanje. ext3 je kompatibilan u nazad sa ext2\. Ektremno stabilan, zreo i najvise koriscen i podrzan GNU/Linux fajl sistem.

3\. [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") *Fourth Extended Filesystem*- Kompatibilan u nazad sa ext2 i ext3\. Predstavlja podrsku za diskove velicine preko 1 exabajta i fajlove sa velicinom do 16 terabajta. Uvecava 32,000 velicinu poddirektorijuma u ext3 na 64,000\. Pruza mogucnost onlajn defragmentacije.

4\. [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") (V3)- Hans Reiser-ov fajl sistem visokih performansi sa zurnalizovanjem. Koristi vrlo interestantan metod protoka podataka baziranog na nekonvencionalnom i kreativnom algoritmu. ReiserFS se reklamira kao vrlo brz, pogotovo kada radi sa mnogo malih fajlova. ReiserFS se brzo formatira, ali je spor prilikom montiranja. Prilicno sazreo i stabilan. ReiserFS (V3) nije u procesu razvoja u ovom momentu. Generalno se smartra kao dobar izbor za /var.

5\. [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) - IBM's **J**ournaled **F**ile**S**ystem- Prvi fajl sistem koji je pruzio zurnalizovanje. JFS je imao mnogo godina upotrebe u IBM AIX® OS-u pre nego sto je ubacen u GNU/Linux. JFS trenutno koristi najmanje procesorskih resursa od svih GNU/Linux fajl sistema. Veoma brz prilikom formatiranja, montiranja i fsck-a (provere fajl sistema) i generalno veoma dobre performanse, pogotovo u odnosu sa dedlajnom I/O zakazivacem. (Pogledajte [JFS](/index.php/JFS "JFS").) Nije tako siroko podrzan kao ext ili ReiserFS, ali veoma zreo i stabilan.

6\. [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") - Jos jedan rani fajl sistem sa zurnalizovanjem originalno razvijen od strane Silicon Graphics-a za IRIX operativni sistem i ubacen u GNU/Linux. XFS pruza veoma brz protok za velike fajlove i velike fajl sisteme. Veoma brz prilikom formatiranja i montiranja. Generalno obelezen kao spor sa mnogo malih fajlova, u poredjenju sa ostalim fajl sistemima. XFS je veoma zreo i pruza onlajn mogucnost defragmentovanja.

7\. [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") - Takodje poznat kao "Bolji FS" je novi fajl sistem sa znatnim, novim i mocnim karakteristikama. Slican Sun/Oracle-ovom odlicnom [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS")-u. Ovi sadrze snepsotove, pravljenje odraza sa vise diskova (prakticno softverski raid bez mdadm-a), checksum-e, inkementalni bekap i kompresiju u letu (koja moze da pruzi znacajno povecanje performansi kao i stednju prostora), i jos toga. Jos uvek se smatra "nestabilnim" od Januara 2011, ali je zdruzen u glavni kernel pod eksperimentalnim statusom. Btrfs izgleda kao buducnost linux fajl sistema i sada se pruza kao root fajl sistem izbor u Ubuntu 10.10, OpenSUSE 11.3 i drugim velikim distribucijama.

*   JFS i XFS fajl sistemi ne mogu biti *smanjeni* sa disk alatima (poput gparted-a ili parted magic-a)

##### Napomena u vezi zurnalizovanja

Svi gornji fajl sistemi, osim ext2, koriste [zurnalizovanje](http://en.wikipedia.org/wiki/Journaling_file_system). Fajl sistemi sa zurnalizovanjem su otporni na greske. Oni koriste zurnalizovanje da loguju promene pre nego sto su pocinjene nad fajl sistemom da bi izbegli korupciju meta podataka u slucaju pada sistema. Imajte na umu da nisu sve tehnike zurnalizovanja iste; samo ext3 i ext4 pruzaju *data-mod zurnalizovanje*, (ali ne kao pocetno podesavanje), koji zurnalizuje *oba*, podatke *i* meta podatke (ali sa znacajnim penalom u brzini). Ostali samo pruzaju *ordered-mod zurnalizovanje*, koji zurnalizuje samo meta podatke. Dok ce svi vratiti vas fajl sistem u ispravno stanje nakon oporavka od pada, *data-mod zurnalizovanje* pruza najvecu zastitu protiv korupcije fajl sistema i gubitka podataka, ali moze patiti od pada performansi jer su svi posaci pisu dva puta (prvo u dnevnik, a zatim na disk). U zavisnosti od toga koliko su vam bitni vasi podaci, mozete razmotriti odgovarajuci fajl sistem za vas.

***Nastavak dalje ...***

Izaberite i napravite fajl sistem (foramtirajte particiju) za / tako sto cete selektovati **yes**. Bicete upozoreni da dodate dodatne particije. U nasem primeru, sda2 i sda4 ostaju. Za sda2, izaberite fajl sistem tip i montirajte ga je kao /var. Konacno, izaberite fajl sistem tip za sda4 montirajte je kao /home.

**Note:** Ako niste napravili i ne treba vam odvojena /boot particija, mozete bezbedno da izignorisete upozorenje da ona ne postoji.
Vratite se na glavni meni.

### Izaberite pakete

Svi paketi tokom instalacije su iz [core] repozitorijuma (udaljena baza paketa na internetu iz koje skidate pakete - programe za Arch). Oni su dalje podeljeni na **Base**, i **Base-devel**. Informacije paketa i kratki opisi su dostupni [ovde](https://www.archlinux.org/packages/?repo=Core&arch=i686&limit=all&sort=pkgname).

Prvo, izaberite paket kategoriju:

**Note:** Radi ubrzanja procesa, svi paketi u **base** su izabrani u skladu sa difoltom (pocetnim podesavanjem). Upotrebite spejs da selektujete i deselektujete pakete.

	Base 

	Paketi iz [core] repozitorijuma pruzaju minimalno osnovno okruzenje. Uvek selektujte uklonite samo one pakete koji nece biti korisceni.

	Base-devel 

	Dodatni alati iz [core] poput `make`, i `automake`. Vecina pocetnika bi trebalo da ih instalira jer ce vecini trebati kasnije.

Nakon selektovanja kategorije bice vam prikazana cela lista paketa sa prilikom da detaljno podesite vase selekcije. Koristite spejs za selektovanje i deselektovanje.

**Note:** Ako je vajrles konekcija neophodna, zapamtite da izaberete i instalirate **wireless_tools** pakete. Neki vajrles interfejsi zahtevaju i [**ndiswrapper**](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration") i/ili odredjeni [**firmver**](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration"). Ako planirate da koristite WPA enkripciju, trebace vam [**wpa_supplicant**](/index.php/WPA_supplicant "WPA supplicant"). [Vajrles podesavanje](/index.php/Wireless_Setup "Wireless Setup") stranica ce vam pomoci da izaberete odgovarajuce pakete za vas vajrles uredjaj. Isto razmotrite instalaciju [**netcfg-a**](/index.php/Netcfg "Netcfg"), koji ce vam pomoci da podesite mreznu konekciju i profile nakon sto restartujete u vas novi sistem.

Nakon izbora potrebnih paketa, napustite ekran za selekciju i nastavite na sledeci korak, **Install packages**.

### Instalacija paketa

*Install Packages* ce instalirati izabrane pakete na vas novi sistem. Ako ste izabrali a CD/USB kao izvor, verzije paketa sa CD/USB-a ce biti instalirani. Ako ste se opredelili za Net-instalaciju (Netinstall), svezi paketi ce biti preuzeti sa interneta i instalirani.

**Note:** U nekim instalerima, bicete upitani ako zelite da zadrzite pakete u pacman kesu. Ako izaberete 'yes', imacete fleksibilnost da [unazadite](/index.php/Downgrade_packages "Downgrade packages") na prethodne paket verzije u buducnosti, pa je ovo preporucljivo (uvek mozete da ispraznite kes u buducnosti).

Nakon sto su paketi preuzeti, instaler ce proveriti njihov integritet. Zatim ce napraviti kernel od preuzetih paketa.

### Konfigurisanje sistema

**Tip:** Blisko pracenje i razumevanje ovih koraka je od vitalnog znacaja da obezbedite ispravno konfigurisani sistem.

U ovoj fazi instalacije, podesicete primarne konfiguracione fajlove vaseg Arch Linux osnovnog sistema. Prethodne verzije instalera su sadrzale [hwdetect](/index.php/Hwdetect "Hwdetect") da prikupe informacije o vasoj konfiguraciji. Ovo je unazadjeno i zamenjeno sa **[udev-om](/index.php/Udev "Udev")**, koji bi trebalo da uspe da ucita vecinu modula automatski prilikom startovanja.

Sada cete biti upitani koji tekst editor zelite da koristite; izaberite [nano](/index.php/Nano "Nano"), [joe](http://joe-editor.sourceforge.net/) ili [[Vim|vi]. `nano` se generalno smatra kao najlaksi od ova tri. Molim vas pogledajte wiki stranice, za odredjeni editor koji zelite da koristite, za instrukcije kako da ga koristite. Pojavice vam se meni zajedno sa glavnim konfiguracionim fajlovima za vas sistem.

**Note:** Vrlo je vazno u ovom momentu da editujete, ili bar potvrdite tako sto cete otvoriti svaki konfiguracioni fajl. Instalaciona skripta se oslanja na vas unos da kreirate ove fajlove u vasoj instalaciji. Cesta greska je preskakanje ovih kriticnih koraka podesavanja.

**Moze li instaler da obavi ovo vise automatski?**

Skrivanje procesa sistem konfigurisanja je u direktnoj suprotnosti sa ***[The Arch Way (Arch-ovim nacinom)](/index.php?title=The_Arch_Way_(Arch-ovim_nacinom)&action=edit&redlink=1 "The Arch Way (Arch-ovim nacinom) (page does not exist)")***. Dok je tacno da zadnje verzije alata za isprobavanje kernela i hardvera pruzaju odlicnu podrsku za hardver i automatsku konfiguraciju, Arch predstavlja korisniku sve relevantne konfiguracione fajlove tokom instalacije u svrhu *transparentnosti i kontrole sistemskih resursa*. U momentu kada zavrsite sa menjanjem ovih fajlova prema vasim potrebama, naucicete jednostavan metod rucnog konfigurisanja Arch Linux-a i postacete srodniji i upoznatiji sa osnovnom strukturom. Na taj nacin cete biti bolje pripremljeni da odrzavate vasu novu instalaciju na produktivan nacin.

#### /etc/rc.conf

Arch Linux koristi fajl `/etc/rc.conf` kao glavnu lokaciju za sistemsko podesavanje. On sadrzi sirok spektar konfiguracionih informacija koji se uglavnom koriste prilikom startovanja sistema. Kao sto njegovo ime samo govori, takodje sadrzi podesavanja za pokretanje /etc/rc* fajlova i, naravno, potice *od* tih fajlova.

* * *

##### LOCALIZATION sekcija

Primer za LOKALIZACIJU:

```
LOCALE="en_US.utf8"
HARDWARECLOCK="localtime"
USEDIRECTISA="no"
TIMEZONE="US/Eastern"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

```

	LOCALE 

	Ova stavka podesava vasu sistemsku lokalizaciju koja ce biti u upotrebi od strane svih 18n-svesnih aplikacija i pomocnih programa. Mozete dobiti listu svih dostupnih lokalizacija pokretanjem `locale -a` komande iz komandne linije. Pocetno podesavanje je obicno dobro za US English korisnike. Ali ako imate probleme sa nekim karakterima koji nece da se stampaju kako treba ili su zamenjeni sa kvadratima, verovatno cete zeleti da se vratite i zamenite "en_US.utf8" sa "en_US".

	HARDWARECLOCK 

	Odredjuje da li hardverski sat, koji se sinhronizuje prilikom startovanja i gasenja, skladisti **UTC** vreme, ili **localtime**. UTC ima smisla jer u velikom meri pojednostavljuje promenu vremenskih zona i pomeranje vremena. localtime je neophodan ako koristite dualno startovanje sa operativnim sistemom poput Windows-a koji skladisti samo localtime u hardverski sat.

	USEDIRECTISA 

	Koristi direktan I/O zahtev umesto `/dev/rtc` za hwclock

	TIMEZONE 

	Zadajte vasu vremensku zonu. (Sve dostupne zone su pod `/usr/share/zoneinfo/`).

	KEYMAP 

	Dostupni rasporedi tastatura su u `/usr/share/kbd/keymaps`. Molim vas da imate na umu da je ovo podesavanje validno samo za vase TTY-ove, a ne odnosi se na graficke prozor menadzere ili **X**.

	CONSOLEFONT 

	Dostupni konzolni fontovi se nalaze pod `/usr/share/kbd/consolefonts/` ako morate da ih promenite. Po pocetnim podesavanjima je (blank) i to je bezbedno podesavanje.

	CONSOLEMAP 

	Definise konzolnu mapu koju ce ucitati sa setfont programom prilikom startovanja. Raspolozive se nalaze u `/usr/share/kbd/consoletrans`, ako je vam treba. Po pocetnim podesavanjima je (blank) i to je bezbedno podesavanje.

	USECOLOR 

	Izaberite "yes" ako imate monitor u boji i zelite da imate boje u vasim konzolama.

* * *

##### HARDWARE sekcija

***Primer za HARDVER:***

```
# Scan hardware and load required modules at boot
MOD_AUTOLOAD="yes"
# Module Blacklist - Deprecated
MOD_BLACKLIST=()
#
MODULES=(!net-pf-10 !pcspkr loop)

```

	MOD_AUTOLOAD 

	Ako podesite ovo na "yes" **udev** ce automatski biti upotrebljen za isprobavanje hardvera i ucitavanje odgovarajucih modula tokom butovanja (startovanja), (zgodno sa pocetnim modularnim kernelom). Ako podesite ovo na "no" u tom slucaju ce korisnik morati da zada informacije rucno ili da kompajlira prilagodjenu verziju kernela i modula, itd..

	MOD_BLACKLIST 

	Ovo je zastarelo u korist dodavanja nezeljenih modula direktno u **MODULES=** liniju ispod.

	MODULES 

	Zadajte dodatne MODULE ako znate da vazan modul nedostaje. Ako vas sistem ima flopi uredjaje, dodajte "floppy". Ako cete koristiti loopback fajl sisteme, dodajte "loop". Isto, zadajte module sa crne liste tako sto cete im dodati prefiks (!). Udev ce biti primoran da NE ucita module sa crne liste. U primeru, IPv6 modul kao i dosadni pcspeaker su stavljeni na crnu listu.

* * *

##### NETWORKING sekcija

	HOSTNAME 

	Podesite vas HOSTNAME prema vasoj potrebi. Ovo je ime vaseg kompjutera. Sta god da stavite ovde, isto to stavite i u `/etc/hosts`

	eth0 

	'Ethernet, card 0'. *ako* koristite **staticki IP**, podesite interfejs IP adrese, netmask i broadcast adrese. Podesite eth0="dhcp" ako zelite da koristite **DHCP** za dinamicku/automatsku konfiguraciju.

	INTERFACES 

	Zadajte sve interfejse ovde. Vise interfejsa bi trebalo da bude razdvojeno sa spejsom kao u: (eth0 wlan0)

	gateway 

	Ako koristite **staticki IP**, podesite gateway adresu. Ako koristite **DHCP**, mozete obicno da igrnorisete ovu varijablu, iako su neki korisnici prijavili da je potrebu da ona bude definisana.

	ROUTES 

	Ako koristite staticki **IP**, uklonite **!** ispred 'gateway'. Ako koristite **DHCP**, mozete obicno da ostavite ovu varijablu pod komentarom sa bengom ispred (!), ali opet, neki korisnici zahtevaju gateway i ROUTES definisane. Ako iskusite probleme sa mrezom sa pacman-om, na primer, mozda cete hteti da se vratite na ove varijable.

**Example w/ Dynamic IP (*DHCP*):**

```
HOSTNAME="arch"
#eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
eth0="dhcp"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(!gateway)

```

**Example w/ Static IP:**

```
HOSTNAME="arch"
eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(gateway)

```

Kada koristite staticki IP, izmenite `/etc/resolv.conf` da zadate DNS servere prema izboru. Molim vas pogledajte [sekciju ispod](#.2Fetc.2Fresolv.conf) u vezi sa ovim fajlom.

**Note:** Zapamtite, konektovanje na vajrles mrezu automatski zahteva nekoliko dodatnih koraka i moze zahtevati od vas da podesite mreznog menadzera poput [netcfg](/index.php/Netcfg "Netcfg") ili [wicd](/index.php/Wicd "Wicd"). Molim vas pogledajte [Vajrles podesavanje](/index.php/Wireless_network_configuration#Part_II:_Wireless_management "Wireless network configuration") stranicu za vise informacija

**Tip:** Ako koristite nestandardnu MTU velicinu (jumbo frejmove) i ako ih hardver instalacione masine podrzava, pogledajte [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames") wiki clanak za dalje konfigurisanje.

##### DAEMONS sekcija

Ovaj niz jednostavno lista imena onih skripti koje se nalaze u /etc/rc.d/ koje se startuju tokom procesa butovanja, i onim redosledom kojim startuju. Asinhrono inicijalizovanje u pozadini je takodje podrzano i korisno za ubrzanje butovanja.

```
DAEMONS=(network @syslog-ng netfs @crond)

```

*   Ako ime skripte ima prefiks (!), onda ona nece biti izvrsena.
*   Ako skripta ima prefiks "et" simbol (@), ona ce biti izvrsena u pozadini; startna sekvenca nece cekati za uspesan zavrsetak svakog daemon-a pre nego sto predje na sledeci. (Korisno za ubrzavanje procesa startovanja sistema). Nemojte stavljati u pozadinu daemon-e koji su potrebni drugim daemon-ima. Na primer "mpd" zavisi od "network"-a, tako da stavljanje u pozadinu network-a moze uzrokovati da mpd ne radi.
*   Editujte ovaj niz kad god su novi sistemski servisi instalirani, ako zelite da ih startujete automatski tokom startovanja sistema.

**Note:** Ovaj 'BSD-style' init, je *The Arch way (Arch-ov nacin)* obavljanja onih stvari koje druge distribucije obavljaju sa razlicitim simbilicnim linkovima ka jednom /etc/init.d direktorijumu.

**O DAEMON-ima**

[daemons](/index.php/Daemons "Daemons") linija ne mora da se menja u ovom trenutku, ali korisno je da objasnimo sta su zapravo daemoni, jer ce se oni pominjati kasnije u ovom uputstvu.

*daemon* je program koji radi u pozadini, cekajuci dogadjaje da iskrsnu i pruza servise. Dobar primer je web server koji ceka zahtev da izda stranicu (e.g.:httpd) ili SSH server koji ceka korisnika da se uloguje (e.g.:sshd). Dok su ovi potpuno opremljene aplikacije, postoje i daemoni ciji posao nije tako vidljiv. Primeri su daemoni koji pisu poruke u log fajlove (e.g. syslog, metalog), i daemoni koji pruzaju graficko logovanje (e.g.: gdm, kdm). Svi ovi programi se mogu dodati u daemon liniju kako bi se startovali kada sistem startuje. Korisni daemoni ce biti predstavljeni tokom ovog uputstva.

Istorijski, termin *daemon* je izmisljen od strane programera MIT-ovog projekta MAC. Oni su uzeli ime od *Maxwell-ovog demon-a*, jednog imaginarnog stvorenja iz poznatog eksperimenta misli koji je stalno radio u pozadini, sortirajuci molekule. *nix sistemi su nasledili ovu terminologiju i napravili inverzni akronim (backronym) **d**isk **a**nd **e**xecution **mon**itor.

**Tip:** Svi Arch daemoni obitavaju pod /etc/rc.d/

#### /etc/fstab

**fstab** (za **f**ile **s**ystems **tab**le) je deo sistem konfiguracije koji izlistava diskove koji su na raspolaganju i disk particije i pokazuje kako oni mogu biti inicijalizovani ili, u suprotnom, integrisani u sveukupni fajl sistem sistema. **/etc/fstab** fajl je nacesce koriscen od strane **mount** komande. Mount komanda uzima fajl sistem na uredjaju i dodaje ga u glavnu sistem hijerarhiju koju vidite kada koristite vas sistem. **mount -a** se zove iz /etc/rc.sysinit, na oko 3/4 ukupnog puta kroz proces startovanja (but proces), i cita /etc/fstab da odredi koje opcije bi trebale da se koriste kada montira odredjeni uredjaj. Ako je **noauto** dodat za fajl sistem u /etc/fstab, **mount -a** ga nece montirati prilikom prilikom but-a.

*Jedan primer `/etc/fstab`-a*

```
# <file system>        <dir>        <type>        <options>                 <dump>    <pass>
none                   /dev/pts     devpts        defaults                       0         0
none                   /dev/shm     tmpfs         defaults                       0         0
/dev/sda1                   /          jfs        defaults,noatime               0         1
/dev/sda2                   /var     reiserfs     defaults,noatime,notail        0         2
/dev/sda3                    swap     swap        defaults                       0         0
/dev/sda4                   /home      jfs        defaults,noatime               0         2

```

**Note:** 'noatime' opcija onemogucava pisanje-citanje-pristup vremena za meta podatke fajlova i moze se bezbedno dodati za / i /home u zavisnosti od zadatog fajl sistem tipa za uvecanje brzine, performansi, i efikasnosti u koriscenju energije (see [here](http://kerneltrap.org/node/14148) za vise informacija). 'notail' onemogucava ReiserFS tailpacking mogucnost, za povecanje performansi po ceni malo manje efikasnosti upotrebe diska.

	<file system> 

	opisuje blok uredjaj ili udaljeni fajl sistem koji se montira. Za regularno montiranje, ovo polje ce sadrzati link ka nodi blok uredjaja (kao sto je kreirano od strane mknod-a koji se poziva od strane udev-a prilikom butovanja) za uredjaj koji se montira; na primer, '/dev/cdrom' ili '/dev/sda1'.
**Note:** Ako vas sistem ima vise od jednog hard diska, instaler ce podesiti tako da koristi UUID pre nego sd*x* semu imenovanja, za konzistentno mapiranje uredjaja. **[Koriscenje UUID-a](/index.php/Persistent_block_device_naming "Persistent block device naming") ima nekoliko prednosti i moze biti upotrebljeno da se izbegnu problemi ako ce se hard diskovi dodavati na sistem u buducnosti.** Prema aktivnom razvoju u kernelu i udev-u, redosled prema kome se drajveri za kontrolere za skladistenje ucitavaju mogu menjati slucajnim redosledom, rezultirajuci sistemom koji nije u mogucnosti da startuje/kernel panika. Skoro svaka matricna ploca ima nekoliko kontrolera (integrisani SATA, integrisani IDE), i prema gore pomenutim informacijama o razvoju, /dev/sda moze postati /dev/sdb na sledecem restartu. (Pogledajte [ovaj wiki clanak](/index.php/Persistent_block_device_naming "Persistent block device naming") za vise informacija o trajnom imenovanju blok uredjaja.)

	<dir> 

	opisuje tacku za montiranje za fajl sistem. Za swap particiju ovo polje treba zadati kao 'swap'; (Swap particije nisu zapravo montirane.)

	<type> 

	opisuje tip fajl sistema. Linux kernel podrzava mnoge fajl sistem tipove. (Za fajl sisteme trenutno podrzane od strane kernela, pogledajte /proc/filesystems). Jedan unos 'swap' oznacava fajl ili particiju koja se korsti za svapovanje. Unos 'ignore' uzrokuje da linija bude ignorisana. Ovo je korisno da pokazete disk particije koje trenutno nisu u upotrebi.

	<options> 

	opisuje opcije za montiranje koje se odnose na fajl sistem. Formatiran je kao lista opcija koje su razdvojene zrezima bez praznih prostora. Sadrzi najmanje tip montiranja plus bilo koju dodatnu opciju koja odgovara fajl sistem tipu. Za dokumentaciju dostupnih opcija za ne-nfs fajl sisteme, pogledajte mount(8).

	<dump> 

	koristi se od strane dump(8)-a komande koja odredjuje koji fajl sistemi ce biti bekapovani. Ako peto polje ne postoji, nula vrednost se vraca i dump ce pretpostaviti da fajl sistem ne treba da bude bekapovan. *Imajte na umu da dump nije instaliran po difoltu.*

	<pass> 

	koristi se od strane fsck(8) programa za odredjivanje redosleda po kom su provere fajl sistema obavljene prilikom butovanja sistema. Root fajl sistem treba da bude zadat sa <pass> od 1, i ostali fajl sistemi bi trebali da imaju <pass> od 2 ili 0\. Fajl sistemi u okviru diska ce biti proveravani redom, ali fajl sistemi na razlicitim diskovima ce biti proveravani u isto vreme da bi se iskoristio paralelizam dostupan na hardveru. Ako sesto polje nije prisutno ili je nula, vrednost nula se vraca i fsck ce pretpostaviti da fajl sistem ne mora da bude proveren.

Prosirene informacije su dostupne na [Fstab](/index.php/Fstab "Fstab") wiki clanku.

#### **[/etc/mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio").conf**

*Vecina korisnika nece imati potrebu da modifikuje ovaj fajl u ovom momentu, ali molim vas procitajte sledece informacije koje objasnjavaju njegovu upotrebu.*

Ovaj fajl omogucava dalje fino podesavanje pocetnog ram fajl sistema, ili initramfs-a, (takodje istorijski nazivan kao inicijalni ram disk ili "initrd") za vas sistem. Initramfs je gzip-ovan odraz koji se iscitava od strane kernela prilikom butovanja. Svrha initramfs-a je da butstrapuje sistem do tacke gde on moze da pristupi root fajl sistemu. Ovo znaci da on mora da ucita module koji su neophodni za uredjaje poput IDE, SCSI, ili SATA uredjaja (ili USB/FW, ako butujete sa USB/FW uredjaja). Kad je initramfs ucitao odgovarajuce module, ili manuelno preko udev-a, on prepusta kontrolu kernelu i vas but se nastavlja. Iz ovog razloga, initramfs mora da sadrzi samo module neophodne za pristup root fajl sistemu. On ne zahteva sve module koje ce te ikada zeleti da koristite. Vecina uobicajenih kernel modula ce biti ucitani kasnije od strane udev-a, tokom init procesa.

`mkinitcpio` je sledeca generacija **initramfs kreacije**. Ima mnoge prednosti u odnosu na stari `mkinitrd` i `mkinitramfs` skripte.

*   Koristi **glibc** i **busybox** da pruzi malu i laganu bazu za rani korisnicki prostor.
*   Moze da koristi "*udev'* za hardversku automatsku detekciju prilikom izvrsavanja i tako spreci ucitavanje mnogobrojnih bespotrebnih module.
*   Njegova hook-bazirana init skripta je lako prosoriva sa dodatnim kukama, koje se lako mogu dodati u pacman paketima bez potrebe za modifikovanjem samog mkinitcpio-a.
*   Vec podrzava **lvm2**, **dm-crypt** za oba, legacy i luks uredjaje, **raid**, **swsusp** i **suspend2** nastavak i butovanje sa **usb uredjaja za masovno skladistenje**.
*   Mnoge mogucnosti mogu biti konfigurisane iz kernel komandne linije bez potrebe za reizgradnjom odraza.
*   **mkinitcpio** skripta omogucava da sadrzimo odraz u kernelu i tako pruza mogucnost da imamo samo-sadrzajni kernel odraz.
*   Njegova fleksibilnost omogucava rekompajliranje kernela bespotrebno u mnogim slucajevima.

Ako koristite RAID ili LVM na root fajl sistemu, odgovarajuce KUKE (HOOKS) moraju biti podesene. Pogledajte wiki stranice za [RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") i [/etc/mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio") za vise informacija. Ako koristite ne-US tastaturu, dodajte "`keymap`" hook da ucitate vas lokalni raspored tastature tokom butovanja. Dodajte "`usbinput`" hook ako koristite USB tastaturu. Ne zaboravite da dodate "`usb`" hook kada instalirate arch na externi hard disk, Comfact Flash, ili SD karticu, koji se konektuju preko usb-a, e.g.:

```
HOOKS="base udev autodetect block filesystems keymap usbinput"

```

(U suprotnom, ako but ne uspe iz nekog razloga, bicete upitani da unesete root sifru za odrzavanje sistema ali necete biti u mogucnosti da to ucinite.)

Ako vam treba podrska za butovanje sa USB uredjaja, FireWire uredjaja, PCMCIA uredjaja, NFS akcija, softverskih RAID nizova, LVM2 uredjaja, enkriptovanih uredjaja, ili DSDT podrska, podesite HOOKS u skladu s tim.

#### /etc/modprobe.d/modprobe.conf

Ovaj fajl moze da se koristi za podesavanje specijalnih konfiguracionih opcija za kernel module. Nije neophodno da podesite ovaj fajl u nasem primeru.

#### /etc/resolv.conf

**Note:** Ako koristite DHCP, mozete bezbedno da ignorisete ovaj fajl, jer prema pocetnim podesavanjima, on ce biti dinamicki kreiran i unistavan od strane dhcpcd daemon-a. Mozete promeniti ovo pocetno ponasanje ako zelite. Pogledajte [Mreza](/index.php/Network#For_DHCP_IP "Network") i [Resolv.conf](/index.php/Resolv.conf "Resolv.conf") stranice za vise informacija.

*resolver* je skup rutina u C biblioteci koji pruza pristup Internet Domen Ime Sistemu (DNS). Jedna od glavnih funkcija DNS-a je da prevede domen imena u IP adrese, da bi ucinio Web prijateljskijim mestom. Resolver konfiguracioni fajl, ili /etc/resolv.conf, sadrzi informacije koje se citaju od strane resolver-a rutina prvog puta kada su pokrenute od strane procesa.

Ako koristite staticki IP, podesite vase DNS servere u /etc/resolv.conf (nameserver <ip-address>). Mozete ih imati koliko god zelite. Jedan primer sa upotrebom OpenDNS-a:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

Ako koristite ruter, verovatno cete zeleti da zadate vase DNS servere u samom ruteru i prosto uperite ka njemu iz vaseg `/etc/resolv.conf`-a, upotrebom IP adrese vaseg rutera (koji je isto vas gateway iz `/etc/rc.conf`). Primer:

```
nameserver 192.168.1.1

```

Ako koristite **DHCP**, mozete da zadate vase DNS servere u ruteru, ili da dozvolite automatsku dodelu od vaseg ISP-a, ako vas ISP ima tu mogucnost.

#### /etc/hosts

Ovaj fajl asocira IP adrese sa imenima hostova i alias-ovima, jedna linija po IP adresi. Za svakog hosta jedna linija bi trebalo da postoji sa sledecim informacijama:

```
<IP-address> <hostname> [aliases...]

```

Dodajte vas *hostname*, tako da se poklapa sa onim zadatim u /etc/rc.conf, tako da izgleda ovako:

```
127.0.0.1   localhost.localdomain   localhost ***vasehostime***

```

**Warning:** *Ovaj format, **ukljucujuci 'localhost' i vase host ime**, su neophodni za kompatibilnost programa! Tako da ako ste imenovali vas kompjuter "arch", onda ta linija iznad treba da izgleda ovako:*
```
127.0.0.1   localhost.localdomain   localhost arch

```
Greske u ovom delu mogu da uzrokuju lose performanse mreze i/ili da odredjeni programi budu mnogo spori prilikom startovanja, ili da ne rade uopste. Ovo je vrlo cesta greska kod pocetnika.

**Note:** Skorije verzije Arch Linux instalera utomatski dodaju vas hostname u ovaj fajl cim editujete `/etc/rc.conf` sa tim informacijama. Ako, iz nekog razloga, ovo nije slucaj, mozete ga dodati sami u skladu sa datim informacijama.

Ako koristite staticki IP dodajte drugu liniju upotrebom sintakse: <static-IP> <hostname.domainname.org> <hostname> npr.:

```
192.168.1.100 ***vasehostime***.domain.org  ***vasehostime***

```

**Tip:** Za prakticnost, mozete isto upotrebiti /etc/hosts alijase za hostove na vasoj mrezi, i/ili na Web-u, npr.:
```
64.233.169.103   www.google.com   g
192.168.1.90   media
192.168.1.88   data

```
Gornji primer bi vam pruzio mogucnost da pristupite guglu jednostavnim ukucavanjem slova 'g' u vas browser i da pristupite serverima za mediju i podatke na vasoj mrezi prema imenu i bez potrebe za ukucavanjem njihovih odgovarajucih IP adresa.

#### /etc/hosts.deny and /etc/hosts.allow

Izmenite ova podesavanja u skladu sa vasim potrebama ako planirate da koristite {[SSH|ssh]] daemon. Pocetno podesavanje ce odbiti sve dolazece konekcije, ne samo ssh konekcije. Editujte vas "*/etc/hosts.allow '* fajl i dodajte odgovarajuce parametre:

*   Da dozvolite svima da se konektuju na vas

```
sshd: ALL

```

*   Da se ogranicite na odredjenu ip adresu

```
sshd: 192.168.0.1

```

*   Ogranicite ga na vasu loalnu LAN mrezu (range 192.168.0.0 do 192.168.0.255)

```
sshd: 192.168.0.

```

*   Ogranicite ga na IP opset

```
sshd: 10.0.0.0/255.255.255.0

```

Ako ne planirate da koristite {[SSH|ssh]] daemon, ostavite ovaj fajl na pocetnim podesavanjima, (prazan).

#### /etc/locale.gen

`/usr/sbin/locale-gen` komanda cita iz **/etc/locale.gen** da generise odredjene lokale. Oni zatim mogu da se koriste od strane **glibc** i bilo kojih drugih lokal-svesnih programa ili biblioteka za renderovanje teksta, ispravno predstavljanje regionalnih monetarnih vrednosti, formata za vreme i datum, alfabet znakova i drugih lokal-specificnih standarda.

Po pocetnim podesavanjima (difoltu) `/etc/locale.gen` je prazan fajl sa dokumentacijom pod komentarima. Jednom editovan, fajl ostaje nedotaknut. `locale-gen` radi na svakoj **glibc** nadogradnji, generisuci sve lokale zadate u `/etc/locale.gen`.

Izaberite lokale koji vam trebaju (uklonite # ispred linija koje zelite), npr.:Choose the locale(s) you need (remove the # in front of the lines you want), e.g.:

```
en_US ISO-8859-1
en_US.UTF-8

```

Instaler ce sada pokrenuti locale-gen skriptu koja ce generisati lokale koje ste specificirali (zadali). Mozete da promenite vase lokale u buducnosti editovanjem /etc/locale.gen i zatim pokretanjem 'locale-gen'-a kao root korisnik.

**Note:** Ako ne uspete da izaberete vas lokal, ovo ce voditi u "The current locale is invalid..." gresku. Ovo je verovatno najcesca greska medju novim Arch korisnicima.

#### Pacman-Odraz

Izaberite odraz repozitorijum za **`pacman`**. Zapamtite da je archlinux.org usporen i da ogranicava download na 50KB/s.

#### Root sifra

Konacno, podesite root sifru i uverite se da ste je zapamtili za kasnije. Vratite se na glavni meni i nastavite sa instalacijom bootloader-a.

#### Gotovo

Kada izaberete "Done", sistem ce ponovo napraviti odraze i vratiti vas nazad na glavni meni. Ovo moze da potraje neko vreme.

### Install and configure a bootloader

#### For BIOS motherboards

For BIOS systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [Syslinux](/index.php/Syslinux "Syslinux") is (currently) limited to loading only files from the partition where it was installed. Its configuration file is considered to be easier to understand. An example configuration can be found in the [syslinux](/index.php/Syslinux#Examples "Syslinux") article.
*   [GRUB](/index.php/GRUB "GRUB") is more feature-rich and supports more complex scenarios. Its configuration file(s) is more similar to 'sh' scripting language, which may be difficult for beginners to manually write. It is recommended that they automatically generate one.

##### Syslinux

If you opted for a GUID partition table (GPT) for your hard drive earlier, you need to install the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package now for the installation of *syslinux* to work:

```
# pacman -S gptfdisk

```

Install the [syslinux](https://www.archlinux.org/packages/?name=syslinux) package and then use the `syslinux-install_update` script to automatically *install* the bootloader (`-i`), mark the partition *active* by setting the boot flag (`-a`), and install the *MBR* boot code (`-m`):

```
# pacman -S syslinux
# syslinux-install_update -iam

```

After installing Syslinux, configure `syslinux.cfg` to point to the right root partition. This step is vital. If it points to the wrong partition, Arch Linux will not boot. Change `/dev/sda3` to reflect your root partition (if you partitioned your drive as in [the example](#Prepare_the_storage_drive), your root partition is `/dev/sda1`).

 `# nano /boot/syslinux/syslinux.cfg` 
```
...
LABEL arch
        ...
        APPEND root=**/dev/sda3** rw
        ...
```

If adding [UUID](/index.php/UUID "UUID") rather than partition number the syntax is `APPEND root=UUID=*partition_uuid* rw`.

Do the same for the fallback entry.

For more information on configuring and using Syslinux, see [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) package and then run `grub-install` to install the bootloader:

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

**Note:**

*   Change `/dev/sda` to reflect the drive you installed Arch on. Do not append a partition number (do not use `sda*X*`).
*   For GPT-partitioned drives on BIOS motherboards, you also need a "BIOS Boot Partition". See [GPT-specific instructions](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") in the GRUB page.
*   A sample `/boot/grub/grub.cfg` gets installed as part of the [grub](https://www.archlinux.org/packages/?name=grub) package, and subsequent `grub-*` commands may not over-write it. Ensure that your intended changes are in `grub.cfg`, rather than in `grub.cfg.new` or some such file.

While using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`) before running the next command.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** It is possible that multiple redundant menu entries will be generated. See [GRUB#Redundant_menu_entries](/index.php/GRUB#Redundant_menu_entries "GRUB").

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

#### For UEFI motherboards

For UEFI systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [gummiboot](/index.php/Gummiboot "Gummiboot") is a minimal UEFI Boot Manager which provides a menu for [EFISTUB](/index.php/EFISTUB "EFISTUB") kernels and other UEFI applications.
*   [GRUB](/index.php/GRUB "GRUB") is a more complete bootloader, useful if you run into problems with Gummiboot.

No matter which one you choose, first install the [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) package, so you can manipulate your EFI System Partition after installation:

```
# pacman -S dosfstools

```

**Note:** For UEFI boot, the drive needs to be GPT-partitioned and an [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (512 MiB or larger, gdisk type `EF00`, formatted with FAT32) must be present. In the following examples, this partition is assumed to be mounted at `/boot`. If you have followed this guide from the beginning, you have already done all of these.

##### Gummiboot

Install the [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) package and run `gummiboot install` to install the bootloader to the EFI System Partition:

```
# pacman -S gummiboot
# gummiboot install

```

**Warning:** Gummiboot and the Linux Kernel will not automatically update if your EFI System Partition is not mounted at `/boot`.

You will need to manually create a configuration file to add an entry for Arch Linux to the gummiboot manager. Create `/boot/loader/entries/arch.conf` and add the following contents, replacing `/dev/sdaX` with your **root** partition, usually `/dev/sda2`:

 `# nano /boot/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

For more information on configuring and using gummiboot, see [gummiboot](/index.php/Gummiboot "Gummiboot").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) and [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) packages and run `grub-install` to install the bootloader:

```
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

Next, while using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) before running the next command. However *os-prober* is not known to properly detect UEFI OSes.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

### Restartujte

To je to; Konfigurisali ste i instalirali vas Arch Linux sistem. Izadjite iz instalacije i restartujte:

```
# reboot

```

**Tip:** Uklonite instalacioni medij i, ako je neophodno, promenite but podesavanja u vasem BIOS-u; u suprotnom moze da se desi da butujete nazad u instalaciju!

## Nakon instalacije

**Cestitamo i dobrodosli u vas novi Arch Linux sistem!**

Ova sekcije ce pokriti razne, morate-uraditi, procedure nakon instalacije poput osvezavanja vaseg novog sistema i dodavanje regularnog, ne-root korisnika.

### Osvezavanje

Vas novi Arch Linux osnovni sistem je sada funkcionalano GNU/Linux okruzenje spremno za prilagodjavanje. Odavde, mozete graditi ovaj elegantni skup alata u sta god pozelite ili zahtevate za vase namene.

Prijavite se sa root nalogom. Konfigurisacemo pacman i osvezicemo sistem kao root.

**Note:** Virtualne konzole 1-6 su dostupne. Mozete prelaziti izmedju njih sa <ALT>+F1...F6

#### Podesavanje mreze (ako je neophodno)

Ako ste dobro konfigurisali vas sistem, trebalo bi da imate mrezu koja radi. Probajte `ping www.google.com` da potvrdite:

 `$ ping -c 3 www.google.com ` 
```
PING www.l.google.com (74.125.229.51) 56(84) bytes of data.
64 bytes from 74.125.229.51: icmp_seq=1 ttl=51 time=26.8 ms
64 bytes from 74.125.229.51: icmp_seq=2 ttl=51 time=27.4 ms
64 bytes from 74.125.229.51: icmp_seq=3 ttl=51 time=26.8 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 26.847/27.053/27.436/0.330 ms
```

Ako ste uspesno uspostavili mreznu konekciju, nastavite sa **[Osvezavanje, sinhronizovanje i nadgradnja sistema sa pacman-om](#Update.2C_Sync.2C_and_Upgrade_the_system_with_pacman)**.

Ako, nakon sto ste probali da pingujete www.google.com, dobijete "unknown host" gresku, mozete da zakljucite da vasa mreza nije ispravno konfigurisana. Mozete da proverite jos jednom sledece fajlove za integritet i ispravna podesavanja:

`/etc/rc.conf` - Posebno, proverite vas HOSTNAME i NETWORKING sekciju za eventualne greske u kucanju i greske generalno.

`/etc/hosts` - Duplo proverite za format, greske u kucanju i greske.

`/etc/resolv.conf` - Ako koristite staticku IP adresu. Ako koristite DHCP, ovaj fajl ce biti dinamicki kreiran i unisten prema pocetnim podesavanjima (default).

**Tip:** Napredne instrukcije za konfigurisanje mreze se mogu naci u [Network](/index.php/Network "Network") clanku.

##### Zicni LAN (Lokalna mreza)

Proverite vas Ethernet sa

```
# ip a

```

Svi interfejsi ce biti izlistani. Trebalo bi da vidite jedan unos za eth0, ili moguce eth1\. Ovi primeri ce koristiti eth0.

**Staticki IP**

Ako je neophodno, mozete da podesite novu staticku IP adresu sa:

```
# ip address add <ip adresa>/<mask-length> dev eth0

```

i default gejtvej sa

```
# ip route add default via <ip adresa gejtveja>

```

Proverite da `/etc/resolv.conf` sadrzi vas DNS server i dodajte ga ako nedostaje. Proverite vasu mrezu opet sa `ping -c 3 www.google.com`. Ako sada sve radi, podesite `/etc/rc.conf` kao sto je opisano gore za staticki IP.

**DHCP**

Ako imate DHCP server/ruter u vasoj mrezi probajte:

```
# dhcpcd eth0

```

Ako radi, podesite `/etc/rc.conf` kao sto je opisano gore, za dinamicki IP.

##### Bezicni LAN (Lokalna mreza)

Molim vas pogledajte [Bezicni brzi start za zivo okruzenje](#Wireless_Quickstart_For_the_Live_Environment) za detalje u vezi konektovanja na bezicnu mrezu. Iako vise ne radite sa intalacionog medija, komande su iste sve dok imate instalirane sve neophodne pakete za bezicni (vajrles) internet (instalirano u sekciji "Izaberite pakete"). Upamtite, vas bezicni uredjaj mozda zahteva firmver da bi mogao da radi. Za resavanje eventualnih problema, posetite za vise detalja [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") stranicu.

##### Proksi server

Ako ste iza proksi servera, editujte `/etc/wgetrc` i podesite http_proxy i ftp_proxy u njemu.

##### Analogni modem, ISDN i DSL (PPPoE)

Pogledajte [Internet Access](/index.php/Internet_Access "Internet Access") za detaljne instrukcije.

#### Osvezavanje, sinhronizacija i nadogradnja sistema sa [pacman](/index.php/Pacman "Pacman")-om

Sada cemo osveziti sistem koristeci [pacman](/index.php/Pacman "Pacman"). [Pacman](/index.php/Pacman "Pacman") je **pac**kage **man**ager (paket menadzer) za Arch Linux. On upravlja celim vasim paket sistemom i obavlja instalaciju, uklanjanje, unazadjivanje paketa (preko kesa), kompajliranje specijalno prilagodjenih paketa, automatsko resavanje zavisnosti, udaljene i lokalne pretrage i jos mnogo toga. Pacman ce sada biti upotrebljen za preuzimanje sofverskih paketa sa udaljenog repozitorijuma i njihovu instalaciju na vas sistem.

**Note:** Ako ste instalirali preko Net-instalera, mnogi, ako ne svi, od vasih paketa su vec aktuelni. Medjutim, preporucljivo je da prodjete kroz ovaj proces ozvezavanja.

##### /etc/pacman.conf

pacman ce pokusati da cita `/etc/pacman.conf` svaki put kad je pokrenut. Ovaj konfiguracioni fajl je podeljen u delove, ili repozitorijume. Svaka sekcija definise pakete [repository](/index.php/Official_repositories "Official repositories") koje pacman moze da koristi kada vrsi pretragu za paketima. Izuzetak za ovo su `options` sekcija, koja definise globalne opcije.

**Note:** Vec postojeca podesavanja bi trebala da rade, pa modifikovanje u ovom trenutku moze biti suvisno. Medjutim, provera je uvek preporucljiva. Dalje informacije su dostupne u [Mirrors](/index.php/Mirrors "Mirrors") clanku.

```
# nano /etc/pacman.conf

```

Repozitorijumi su opisani ispod; omogucite sve raspolozive repozitorijume tako sto cete ukloniti # ispred 'Include =' i '[repository]' linija.

**Note:** Kada birate repozitorijume, obavezno dekomentirajte naslove repozitorijuma u [zagradama] kao i 'Include =' linije. Ukoliko to ne ucinite, kao rezultat cete dobiti repozitorijum koji ce biti preskocen! Ovo je vrlo cesta greska koja se desava.

##### Repozitorijumi za pakete

[repozitorijum za softver](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository") je lokacija za skladistenje iz koje softverski paketi mogu biti preuzeti i instalirani na racunar. Arch Linux [odrzavaoci paketa](/index.php/Package_Maintainer "Package Maintainer") (programeri i [Trusted Users](/index.php/Trusted_Users "Trusted Users")) odrzavaju veliki broj oficijalnih repozitorijuma koji sadrze softverske pakete za vitalnim i popularnim softverom, spremni za pristup preko [pacman](/index.php/Pacman "Pacman")-a. Ovaj clanak istice te zvanicno-podrzane repozitorijume. Pogledajte [Official repositories](/index.php/Official_repositories "Official repositories") Za vise informacija ukljucujuci detalje o svrsi svakog repozitorijuma.

Vecina ljudi ce zeleti da koristi [core], [extra] i [community]. Ako zelite da koristite 32-bitne aplikacije na Arch x86_64, ukljucite [multilib] repozitorijum tako sto cete dodati linije ispod u /etc/pacman.conf:

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

##### AUR

**[AUR](/index.php/AUR "AUR")** takodje sadrzi **nepodrzanu** granu, kojoj se ne moze pristupiti direktno sa pacman-om. **AUR** [nepodrzan] ne sadrzi binarne pakete. On pre pruza vise od sesnaest hiljada PKGBUILD skripti za izgradnju paketa iz izvornog koda koji su mozda nedostupni preko drugih repozitorijuma. Kada jedan AUR nepodrzani paket stekne dovoljno glasova za popularnost, moze biti prebacen u AUR [community] binarni repozitorijum, ako je korisnik koji ga odrzava voljan da ga usvoji i odrzava tamo.

*   Odrzava se od strane korisnika kojima se veruje -eng. TU (Trusted User)
*   Svi PKGBUILD-ovi su bash skripte za izgradnju paketa
*   **Nije** dostupan sa pacman-om po difoltu

* pacman omotaci (***[AUR helpers](/index.php/AUR_helpers "AUR helpers")***) vam mogu pomoci da bez poteskoca pristupite AUR-u.

#### /etc/pacman.d/mirrorlist

Definise pacman repozitorijum odraze i prioritete.

Otvorite `/etc/pacman.d/mirrorlist` u nekom tekst editoru i uklonite komentare (uklonite '#' ispred) za server koji se nalazi blizu vas. Zatim izdajte komandu za kompletno osvezenje paketa:

```
# pacman -Syy

```

Dodavanje dva --refresh ili -y zastava primorava pacman-a da osvezi sve liste paketa cak i ako se smatra da su vec aktuelni. Izdavanje -Syy *kad god se promeni odraz*, je dobra praksa i tako cete izbeci moguce glavobolje.

##### `rankmirrors`

Alternativno, mozete da koristite `rankmirrors`. `rankmirrors` je bash skripta koja ce pokusati da detektuje nekomentirane odraze naznacene u `/etc/pacman.d/mirrorlist` koji su najblize do instalacione masine bazirano na latenciji. Brzi odrazi ce u velikoj meri da unaprede performanse pacman-a i opsti Arch Linux dozivljaj. Ova skripta moze da se pokrene periodicno, pogotovo ako izabrani odrazi pruzaju nekonzistentan protok i/ili osvezenja. Imajte na umu da `rankmirrors` ne testira za protok. Alati poput `wget` ili `rsync` mogu biti upotrebljeni za efikasno testiranje protoka odraza nakon sto je novi `/etc/pacman.d/mirrorlist` generisan.

Izdajte sledecu komandu da kompletno osvezite bazu paketa, nadogradite i instalirate `curl`:

```
# pacman -Syyu curl

```

*   *Ako dobijete gresku u ovom koraku, upotrebite komandu "nano /etc/pacman.d/mirrorlist" i uklonite komentar za server koji vam odgovara.*

`cd` u `/etc/pacman.d/` direktorijumu:

```
# cd /etc/pacman.d

```

Bekapujte postojeci `/etc/pacman.d/mirrorlist`:

```
# cp mirrorlist mirrorlist.backup

```

Editujte mirrorlist.backup i dekomentirajte sve odraze na istom kontinentu ili u geografskoj blizini da testirate sa rankmirrors.

```
# nano mirrorlist.backup

```

Pokrenite skriptu na mirrorlist.backup sa -n prekidacem i preusmerite izlaz u novi /etc/pacman.d/mirrorlist fajl:

```
# rankmirrors -n 6 mirrorlist.backup > mirrorlist

```

**-n 6**: rank the 6 closest mirrors

Primorajte pacman da osvezi sve liste paketa sa novom listom odraza na mestu:

```
# pacman -Syy

```

##### Provera odraza za aktuelne pakete

Jer `rankmirrors` ne uzima u obzir koliko je paket lista sa odraza aktuelna, vazno je da napomenemo da jedan ili vise odraza koje selektuje kao najbrze mogu ipak biti neaktuelni. [ArchLinux provera odraza](https://www.archlinux.de/?page=MirrorStatus;orderby=lastsync;sort=1) prijavljuje razne aspekte o odrazima poput mreznih problema sa odrazima, problema sa prikupljanjem podataka, zadnje vreme kada je odraz bio sinhronizovan, itd. Mozda cete pozeleti da rucno ispitate `/etc/pacman.d/mirrorlist`, da bi seuverili da fajl sadrzi samo aktuelne odraze ako je posedovanje najskorijih paket verzija prioritet.

Alternativno, [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) moze automatski da rankira odraze koji su blizu vase lokacije prema tome koliko su aktuelni.

#### Bolje se upoznajte se pacman-om

pacman je najbolji prijatelj Arch korisnika. Vrlo je preporucljivo da studirate i naucite kako da koristite pacman(8) alatku. Probajte:

```
$ man pacman

```

Za vise informacija, bacite pogled na [pacman](/index.php/Pacman "Pacman") wiki clanak u vase slobodno vreme, ili pogledajte [pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") unos za poredjenje sa drugim popularnim paket menadzerima.

#### Osvezavanje sistema

Sada ste spremni da nadogradite ceo vas sistem. Pre nego sto to ucinite, procitajte [vesti](https://www.archlinux.org/news/) (i opciono [mejling lista za objave](https://archlinux.org/pipermail/arch-announce/)). Obicno ce programeri obezbediti vazne informacije o neophodnim podesavanjima i modifikacijama za poznate probleme. Konsultovanje ovih stranica pre nadogradnje je dobra praksa.

Sinhronizujte, osvezite i nadogradite vas ceo sistem sa:

```
# pacman -Syu

```

ili:

```
# pacman --sync --refresh --sysupgrade

```

pacman ce sada preuzeti svezu kopiju glavne paket liste sa servera definisanog u `/etc/pacman.conf` i izvrsiti sve dostupne nadogradnje. Mozda cete biti upitani da nadogradite i sam pacman u ovom momentu. Ako je to slucaj, recite "yes", a zatim ponovo izdajte `pacman -Syu` komandu kada zavrsi.

Restartujte ukoliko je izvrsena nadogradnja kernela.

**Note:** Obicno, konfiguracione promene mogu zahtevati delovanje korisnika tokom nadogradnje; procitajte pacman-ove izlaze za relevantne informacije.

Pacman-ov izlaz se cuva u `/var/log/pacman.log`.

Pogledajte [Upravljanje paketima FAQ](/index.php/Package_Management_FAQs "Package Management FAQs") za odgovore za cesto postavljana pitanja koja se odnose na osvezenje i upravljanje vasim paketima.

##### Ignorisanje paketa

Nakon izvrsene komande `pacman -Syu`, ceo sistem ce biti nadogradjen. Moguce je da sprecite pakete da budu nadogradjeni. Tipicni scenario bi bio paket cija nadogradnja moze biti problematicna za sistem. U tom slucaju postoje dve opcije; odredite pakete koje zelite da preskocite u pacman komandnoj liniji tako sto cete upotrebiti --ignore prekidac (`pacman -S --help` za detalje) ili trajno odredite da se paket preskace u /etc/pacman.conf fajlu u IgnorePkg nizu. Za vise informacija, molim vas pogledajte [pacman](/index.php/Pacman "Pacman") wiki unos.

Molm vas da imate na umu da se od naprednog korisnika ocekuje da drzi sistem aktuelnim sa pacman -Syu, pre nego da selektivno nadogradjuje pakete. Mozete da odstupate od ovog tipicnog nacina upotrebe ukoliko zelite; samo budite upozoreni da postore vece sanse da stvari nece raditi ocekivano i da mogu slomiti vas sistem. Vecina zalbi se desava kada se vrsi selektivna nadogradnja, neobicno kompajliranje ili ako je izvrseno nepravilno instaliranje softvera. Upotreba **IgnorePkg** u /etc/pacman.conf je zbog toga nepreporucljiva i treba je koristiti samo sporadicno, ako znate sta radite.

##### The Arch rolling release model (Arch-ov model novih verzija u letu)

Imajte na umu da je Arch **rolling release** distribucija. To znaci da nikad ne postoji razlog da ponovo instalirate ili vrsite detaljnu reizgradnju sistema da bi ste nadogradili na najskoriju verziju. Jednostavnim izdavanjem `pacman -Syu` preiodicno odrzavate vas sistem aktuelnim i na krvavoj ostrici (bleeding edge). Na kraju ove nadogradnje, vas sistem je kompletno osvezen i nov. Zapamtite da **restartujete** ako je doslo do nadogradnje kernela.

### Dodavanje korisnika

**Note:** Pre dodavanja vasih korisnika, razmotrite ojacavanje vaseg sistema prelaskom sa md5 hesa za sifre na sha512 hesa za sifre. Pogledajte [SHA_sifra_hes](/index.php/SHA_password_hashes "SHA password hashes") wiki clanak za vise informacija.

Linux je visekorisnicko okruzenje. Ne bi trebali da radite svakidasnje poslove upotrebom root naloga. To je vise nego siromasna praksa; to je opasno. Root je za administrativne poslove. Umesto toga, dodajte normalnog, ne-root, korisnika upotrebom `/usr/sbin/useradd` programa.

```
# useradd -m -g [startne-grupe] -G [dodatne-grupe] -s [login_shell] [korisnicko-ime]

```

*   **-m** Pravi home direktorijum za korisnika kao /home/**korisnicko-ime**. U okviru svojih home direktorijuma, korisnici mogu da pisu fajlove, brisu ih, instaliraju programe, itd. Home direktorijumi korisnika ce sadrzati njihove podatke i licne konfiguracione fajlove, takozvane 'tacka fajlove' (njihovo ime kao prefiks ima tacku), koji su 'skriveni'. (Da vidite tacka-fajlove, ukljucite odgovarajucu opciju u vasem fajl menadzeru ili pokrenite ls komandu sa -a prekidacem.) Ako postoji konflikt izmedju *korisnickih* (pod /home/korisnicko-ime) i *globalnih* konfiguracionih fajlova, (obicno pod /etc/) podesavanja u *korisnickom* fajlu ce imati prednost. Tacka-fajlovi koji ce najverovatnije biti menjani od strane korisnika su .xinitrc i .bashrc fajlovi. To su konfiguracioni fajlovi za xinit i Bash. Oni omogucavaju korisniku mogucnost da promeni prozor menadzer koji ce biti startovan prilikom prijavljivanja i takodje aliase, komande zadate od strane korisnika i prostorne varijable. Kada je korisnik napravljen, njihovi tacka-fajlovi ce biti preuzeti iz /etc/skel direktorijuma gde obitavaju uzorci sistemskih fajlova.
*   **-g** Ime grupe ili broj korisnikove inicijalne grupe za prijavljivanje. Ime grupe mora da postoji. Ako je obezbedjen broj grupe, on mora da se odnosi na vec postojecu grupu. Ako nije zadat, ponasanje komande useradd ce zavisiti od USERGROUPS_ENAB varijable koja se nalazi u /etc/login.defs.
*   **-G** Lista dopunskih grupa kojih je korisnik isto clan. *Svaka grupa je odvojena od sledece zarezom, bez praznih prostora*. Prema pocetnim podesavanjima (default) korisnik pripada samo inicijalnoj grupi.
*   **-s** Staza i ime fajla korisnikove osnovnoe skoljke (shell) za logovanje. Arch Linux init skripte koriste Bash. Nakon pokretanja sistema (butovanja), osnovna skoljka za prijavljivanje je specificna za svakog korisnika pojedinacno. (Obezbedite paket za izabranu skoljku ukoliko koristite nesto drugo, a ne Bash).

Korisne grupe za vaseg ne-root korisnika su:

*   **audio** - za poslove koji ukljucuju zvucnu karticu i programe koji se odnose na nju
*   **floppy** - za pristup flopiju ukoliko postoji
*   **lp** - za upravljanje poslovima stampanja
*   **optical** - za upravljanje poslovima sa optickim citacima
*   **storage** - za upravljanje uredjajima za skladistenje podataka
*   **video** - za video poslove i hardversku akceleraciju
*   **wheel** - za upotrebu sudo-a
*   **games** - neophodno za dozvolu za pisanje za igrice u games grupi
*   **power** - za upravljanje napajanjem (npr.: gasenje racunara sa dugmetom za napajanje)
*   **scanner** - za upotrebu skenera

Tipicni desktop sistem primer, uz dodatog korisnika pod imenom "archie" sa bash-om kao skoljkom za prijavljivanje:

```
# useradd -m -g users -G audio,lp,optical,storage,video,wheel,games,power,scanner -s /bin/bash archie

```

Sledece, dodajte sifru za vaseg novog korisnika sa komandom `/usr/bin/passwd`.

Primer za naseg korisnika, 'archie':

```
# passwd archie

```

(Bicete upitani da obezbedite novu sifru.)

Vas novi ne-root korisnik je sada napravljen zajedno sa kuca (home) direktorijumom i sifrom za prijavljivanje.

**Brisanje korisnickog naloga:**

U slucaju greske, ili ako zelite da obrisete nalog korisnika u korist drugog imena ili iz nekog drugog razloga, upotrebite `/usr/sbin/userdel`:

```
# userdel -r [username]

```

*   **-r** Fajlovi u korisnickom kuca (home) direktorijumu ce biti uklonjeni zajedno sa kuca direktorijumom i korisnikovim mejl spool-om.

Ako zelite da promenite ime vaseg korisnika ili bilo kog postojeceg korisnika, pogledajte [Promena korisnickog imena](/index.php/Change_username "Change username") stranicu Arch wiki-ja i/ili [Grupe](/index.php/Groups "Groups") i [Upravljanje korisnikom](/index.php/User_Management "User Management") clanke za dalje informacije. Takodje mozete da proverite man stranice za `usermod(8)` i `gpasswd(8)`.

#### Instalacija i podesavanje Sudo-a (Opciono)

Instalirajte Sudo:

```
# pacman -S sudo

```

Da dodate korisnika kao sudo korisnika (a "sudoer"), visudo komanda mora biti pokrenuta kao root.

Po difoltu, visudo komanda koristi editor [vi](/index.php/Vi "Vi"). Ako ne znate kako da koristite vi, mozete da podesite EDITOR prostornu varijablu na editor prema vasem izboru, kao u ovom primeru sa editorom "nano":

```
# EDITOR=nano visudo

```

**Note:** Imajte na umu da podesavate varijablu i startujete visudo na istoj liniji u isto vreme. Ovo nece raditi ispravno kao dve zasebne komande.

Ako znate da koristite vi, upotrebite komandu visudo bez EDITOR=nano varijable:

```
# visudo

```

Ovo ce otvoriti fajl /etc/sudoers u specijalnoj sesiji vi-ja. Visudo kopira fajl da bi bio editovan u privremenom fajlu, edituje ga sa nekim editorom, (vi po difoltu), i zatim izvrsava proveru ispravnosti. Ako prodje proveru, privremeni fajl prepisuje original uz odgovarajuce dozvole.

**Warning:** Nemojte da editujete /etc/sudoers direktno sa editorom; Greske u sintaksi mogu uzrokovati probleme (poput toga da root korisnik postane neupotrebljiv. Morate da koristite *visudo* komandu da editujete /etc/sudoers.

U prethodnoj sekciji mi smo dodali vaseg korisnika u "wheel" grupu. Da damo korisnicima u wheel grupi pune root privilegije kada u svojim komandama imaju "sudo" kao prefix, uklonicemo sledecu liniju:

```
%wheel	ALL=(ALL) ALL

```

Sada mozete da date bilo kom korisniku pristup sudo komandi tako sto cete ih dodati u wheel grupu.

Za vise informacija, poput <TAB> kompletiranja, pogledajte [Sudo](/index.php/Sudo "Sudo").

## Dodatci

Sada bi trebalo da imate potpuno funkcionalan Arch sistem koji ce se ponasati kao pogodna baza na kojoj mozete da gradite dalje prema vasim potrebama. Kako kod, ljudi su vecinom zainteresovani za desktop sistem, zajedno sa zvukom i grafikom. Ovaj deo uputstva ce vam dati brzi start i za te dodatne stvari.

### Zvuk

Ako zelite zvuk, nastavite na [Napredna Linux zvuk arhitektura](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") za instrukcije. Alternativno, nastavite na sledecu sekciju (instaliranje GUI-ja) prvo, i podesite zvuk kasnije (obicno radi direktno iz kutije, pa cete samo morati da ga ukljucite (unmute)).

[Napredna Linux zvuk arhitektura](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (ALSA) je sadrzana u okviru kernela i preporucljivo je da prvo nju probate. Medjutim, ako ne radi ili niste zadovoljni kvalitetom, [Otvoreni sistem za zvuk](https://en.wikipedia.org/wiki/Open_Sound_System "wikipedia:Open Sound System") je dostupan kao alternativa. OSSv4 je objavljen pod besplatnom licencom i generalno se smatra za znacajno unapredjenje u odnosu na stariji OSS koji je zamenjen sa ALSA. Instrukcije se mogu naci u [OSS clanku](/index.php/OSS "OSS").

Ako imate napredne zahteve sto se tice zvuka, pogledajte [Zvuk](/index.php/Sound "Sound") za pregled razlicitih clanaka.

### **G**raphical **U**ser **I**nterface (graficki korisnicki interfejs)

#### Instalacija X-a

**X** prozor sistem verzija 11 (obicno se naziva **X11**, ili jednostavno **X**) je mrezni i displej protokol koji pruza mogucnost koriscenja prozora na bitmap ekranima. Laickim jezikom, pruza standardni skup alata i protokola za izgradnju grafickog korisnickog interfejsa (GUI-ja).

**Warning:** Ako instalirate Arch u Virtualbox-u, treba vam drugaciji nacin da zavrsite X instalaciju. Pogledajte [Pokretanje Arch Linux-a kao gost korisnik](/index.php/VirtualBox#Running_Arch_Linux_as_a_guest "VirtualBox"), preskocite A,B,C korake ispod.

Sada cemo instalirati osnovne **[Xorg](/index.php/Xorg "Xorg")** pakete pomocu pacman-a. Ovo je prvi korak u izgradnji GUI-ja.

Instalirajte osnovne pakete:

```
# pacman -S xorg

```

Instalirajte mesa za 3D podrsku:

```
# pacman -S mesa

```

3D pomocni programi glxgears i glxinfo su sadrzani u okviru **mesa-demos** paketa. Instalirajte ako je neophodno:

```
# pacman -S mesa-demos

```

#### Instalirajte video drajver

Sledece, trebali bi da instalirate drajver za vasu graficku karticu.

Trebace vam znanje vezano za skup video cipova koje vasa masina ima. Ako ne znate, upotrebite `/usr/sbin/lspci` program:

```
$ lspci

```

**Note:** **vesa** drajver je genericki i trebalo bi da radi sa skoro svakim modernim skupom video cipova. Ako ne mozete da nadjete odgovarajuci drajver za vas skup video cipova, vesa *bi* trebalo da radi sa bilo kojom karticom, ali pruza samo 2D.

Za kompletnu listu svih **open-source** video drajvera, pretrazite bazu paketa:

```
$ pacman -Ss xf86-video | less

```

**Note:** Vlasnicki drajveri za NVIDIA i ATI su pokriveni u sledecoj sekciji. Ako planirate da koristite 3D procesiranje poput igranja igrica, razmotrite upotrebu ovih.

Upotrebite pacman da instalirate vlasnicke video drajvere za vasu video karticu/integrisanu karticu. Primer za Savage drajver:

```
# pacman -S xf86-video-savage

```

**Tip:** Za neke Intel graficke kartice, moze biti neophodno dodatno podesavanje da bi ste dobili ispravne 2D ili 3D performanse. Pogledajte [Intel](/index.php/Intel "Intel") za vise informacija.

##### NVIDIA Graficke karte

NVIDIA korisnici imaju tri opcijeza drajvere (kao dodatak vesa drajveru):

*   Open sors nouveau drajver koji pruza brzu 2d akceleraciju i eksperimentalnu 3d podrsku koja je dovoljno dobra za osnovnu kompozitnost (napomena: ne podrzava u potpunosti stednju energije). [Feature Matrix.](http://nouveau.freedesktop.org/wiki/FeatureMatrix)
*   Open sors (ali bagovit) nv drajver, koji je veoma spor i ima samo 2d podrsku.
*   Vlasnicki nvidia drajveri, koji pruzaju dobre 3d performanse i stednju energije. Cak i ako planirate da koristite vlasnicke drajvere, preporucuje se da startujete sa nouveau i zatim predjete na binarni drajver, jer nouveau ce skoro uvek raditi direktno iz kutije, dok nvidia zahteva konfigurisanje i vrlo verovatno resavanje nekih problema. Pogledajte [NVIDIA](/index.php/NVIDIA "NVIDIA") za vise informacija.

Open sors nouveau drajver bi trebalo da bude dovoljan za vecinu korisnika i preporucuje se:

```
# pacman -S xf86-video-nouveau

```

Ili, za 3D podrsku (visoko eksperimentalan):

```
# pacman -S nouveau-dri

```

Napravite fajl `/etc/X11/xorg.conf.d/20-nouveau.conf`, i ubacite sledeci sadrzaj:

```
Section "Device"
    Identifier "n"
    Driver "nouveau"
EndSection

```

Ovo je neophodno da osigura ucitavanje nouveau drajvera. Xorg nije jos dovoljno pametan da to sam uradi.

**Tip:** Za napredne instrukcije, pogledajte [Nouveau](/index.php/Nouveau "Nouveau").

##### ATI graficke kartice

Vlasnici ATI-ja imaju dve glavne opcije za drajvere (uz dodatak vesa drajveru):

*   open sors **radeon** drajver sadrzan u **xf86-video-ati** paketu. Pogledajte [radeon feature matrix](http://wiki.x.org/wiki/RadeonFeature) za detalje.
*   Vlasnicki **fglrx** drajver obezbedjen u [catalyst](https://aur.archlinux.org/packages.php?O=0&K=catalyst&do_Search=Go) paketu koji se nalazi u [AUR](/index.php/AUR "AUR"). On podrzava samo novije uredjaje (HD2xxx i novije). U proslosti se taj paket nalazio u Arch `extra` repozitorijumu, ali od marta 2009, oficijalna podrska je izbacena zbog nezadovljstva sa kvalitetom i brzinom razvoja vlasnickih drajvera. Pogledajte [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") za vise informacija.

Open sors drajver se preporucuje kao izbor. Instalirajte **radeon** ATI drajver:

```
# pacman -S xf86-video-ati

```

**Tip:** Za napredne instrukcije pogledajte [ATI](/index.php/ATI "ATI").

#### Instalirajte drajvere za unos

Udev bi trebalo da bude u mogucnosti da detektuje vas hardver bez problema i evdev (xf86-input-evdev) je moderan, ulazni drajver sa hotplug mogucnostima za gotovo sve uredjaje u vecini slucajeva i instaliranje ulaznih drajvera u tom slucaju nije neophodno. U ovom momentu evdev he vec instaliran kao zavisnost Xorg-a.

Ako evdev ne podrzava vas uredjaj, instalirajte neophodni drajver iz xorg-input-drivers grupe.

Za kompletnu listu dostupnih ulaznih drajvera upotrebite pacman pretragu:

```
# pacman -Ss xf86-input | less

```

**Note:** Potrebni su vam samo xf86-input-keyboard ili xf86-input-mouse ako planirate da onemogucite hotplug. U suprotnom, evdev ce se ponasati kao input drajver.

Laptop korisnicima (ili korisnici sa ekranom na dodir) ce isto trebati synaptics paket da bi dozvolili X-u da konfigurise dodirnu tablu/ekran na dodir:

```
# pacman -S xf86-input-synaptics

```

**Tip:** Za instrukcije za fino podesavanje ili resavanje problema sa podesavanjima za dodirnu tablu, pogledajte [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") clanak.

#### Podesavanje X-a(Opciono)

**Warning:** Vlasnicki drajveri obicno zahtevaju restart nakon instalacije i konfigurisanja. Pogledajte [NVIDIA](/index.php/NVIDIA "NVIDIA") ili [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") za detalje.

X server ima mogucnost za automatsko konfigurisanje i zbog toga moze da funkcionise bez xorg.conf fajla. Ako ipak zelite da konfigurisete X server, molim vas pogledajte [Xorg](/index.php/Xorg "Xorg") wiki stranicu.

##### Ne-US tastatura

Ako ne koristite standardnu US tastaturu morate da podesite raspored tastature u `/etc/X11/xorg.conf.d/10-evdev.conf`:

```
Section "InputClass"
    Identifier "evdev keyboard catchall"
    MatchIsKeyboard "on"
    MatchDevicePath "/dev/input/event*"
    Driver "evdev"
    **Option "XkbLayout" "rs"**
    **Option "XkbLayout" "rs latin"**
EndSection

```

**Note:** **XkbLayout** taster se moze razlikovati od keymap koda koji ste koristili sa km ili loadkeys komandom. Na primer, uk raspored tastature odgovara tasteru: **gb**.

#### Testiranje X-a

Ova sekcija ce objasniti kako da startujete osnovno graficko okruzenje koje je sastavni deo xorg grupe, kako bi ga istestirali. On koristi jednostavan X prozor menadzer, twm.

Pocetno X okruzenje je sasvim prosto. [Ova sekcija ispod](#Choose_and_install_a_graphical_interface) ce obraditi instalaciju desktop okruzenja ili prozor menadzera prema vasem izboru i ono ce zameniti X.

Ako ste instalirali Xorg pre nego sto ste napravili vaseg regularnog korisnika, postojace prazan .xinitrc fajl u vasem $HOME koji cete morati ili da obrisete ili da editujete da bi ste uspesno startovali X. Ako ne uradite to X ce pokazati prazan ekran a `Xorg.0.log` ce izgledati kao da nema greske. Jednostavnim brisanjem cete ga pokrenuti sa pocetnim X okruzenjem.

```
$ rm ~/.xinitrc

```

##### Magistrala za poruke

**Note:** `dbus` je verovatno potrebna za mnoge od vasih aplikacija da bi radile ispravno. Ako vam to nije neophodno, preskocite ovu sekciju.

Instalirajte dbus:

```
# pacman -S dbus

```

Da startujete automatski prilikom butovanja, trebali bi da dodate `dbus` u vas DAEMONS niz u `/etc/rc.conf`:

```
DAEMONS=(syslog-ng **dbus** network crond)

```

Ako zelite da startujete dbus bez restartovanja, izvrsite

```
# /etc/rc.d/dbus start

```

##### Startujte X

**Note:** Ctrl-Alt-Backspace precica tradicionalno je koriscena za ubijanje X-a, ali ona je zastarela i nece raditi za izlazak iz ovog testa. Mozete je ukljuciti editovanjem xorg.conf-a, kao sto je opisano [ovde](/index.php/Xorg#Ctrl-Alt-Backspace_doesn.27t_work "Xorg").

Konacno, startujte Xorg:

```
$ startx

```

ili

```
$ xinit -- /usr/bin/X -nolisten tcp

```

Nekoliko prozora ,koje je moguce pomerati, bi trebalo da se pojave i vas mis bi trebao da radi. Kada budete zadovoljni da je **X** instalacija bila supeh, mozete izaci iz X-a izdavanjem `exit` komande u promtu i tako se vratite u konzolu.

Ako ekran postane crn, mozete da pokusate da se prebacite u drugu virtualnu konzolu (CTRL-Alt-F2, na primer), i da se ulogujete na slepo kao root, praceno sa <Enter>, praceno sa root sifrom, praceno sa <Enter>.

Mozete da probate da roknete X (haha) server sa `/usr/bin/pkill` (primetite veliko slovo **X**):

```
# pkill X

```

Ako pkill ne obavi posao, restartujte na slepo sa:

```
# reboot

```

##### U slucaju gresaka

Ako dodje do problema, pogledajte za greske u `/var/log/Xorg.0.log`. Trazite linije koje pocinju sa `(EE)` koje predstavljaju greske, i takodje `(WW)` koji su upozorenja koja ukazuju na druge probleme.

```
$ grep EE /var/log/Xorg.0.log

```

Greske se isto mogu pretraziti i u konzolnom izlazu iz virtualne konzole iz koje je **X** startovan.

Pogledajte [Xorg](/index.php/Xorg "Xorg") clanak za detaljne instrukcije i resavanje problema.

##### Treba vam pomoc?

Ako i dalje imate problema nakon konsultovanja [Xorg](/index.php/Xorg "Xorg") clanka i treba vam pomoc na Arch forumima, obavezno instalirajte wgetpaste:

```
# pacman -S wgetpaste

```

Koristite wgetpaste i obezbedite linkove za sledece fajlove kada trazite pomoc u vasem forum postu:

*   ~/.xinitrc
*   /etc/X11/xorg.conf
*   /var/log/Xorg.0.log
*   /var/log/Xorg.0.log.old

Upotrebite wgetpaste na sledeci nacin:

```
$ wgetpaste </path/to/file>

```

Post-ujte odgovarajuce linkove u vasem forum postu. Proverite, takodje, da ste dali ispravne hardverske informacije i informacije o drajverima.

**Warning:** Vrlo je vazno da date detalje kada resavate probleme za X. Molim vas obezbedite sve neophodne informacije, kao sto je naznaceno gore, kada trazite za pomoc na Arch forumima.

#### Instalijate fontove

U ovom trenutku, mozemo da sacuvamo malo vremena tako sto cemo instalirati vizuelno prijate, true type fontove, pre nego sto instaliramo desktop okruzenje/prozor menadzer. DajaVu je skup visoko kvalitetnih fontova za generalnu namenu..

Instalirajte sa:

```
# pacman -S ttf-dejavu

```

Pogledajte [Podesavanje fontova](/index.php/Font_configuration "Font configuration") da saznate kako da podesite renderovanje fontova i [Fontovi](/index.php/Fonts "Fonts") za sugestije o fontovima i intrukcije za instaliranje.

#### Izaberite i instalirajte graficki interfejs.

X prozor sistem pruza osnovni frejmvork za izgradnju grafickog korisnickog interfejsa (GUI-a).

**Note:** Nasuprot velikom proju drugih distribucija, Arch nece odluciti umesto vas koje graficko okruzenje cete koristiti. Izbor vaseg grafickog okruzenja ili prozor menadzera je vrlo subjektivan i licni izbor. Vredi probati veliki broj okruzenja izlistanih ovde pre nego sto napravite vas izbor jer pacman moze kompletno da ukloni sve sto vi instalirate.

	Prozor menadzer (WM) 

	kontrolise raspored i izgled prozora aplikacija u saradnji sa X prozor sistemom. **See [Prozor menadzeri](/index.php/Window_manager#Window_managers "Window manager") za vise informacija.**

	Desktop okruzenje (DE)

	Radi povrh i u saradnji sa X-om da obezbedi kompletno funkcionalan i dinamicki GUI. DE tipicno obezbedjuje prozor menadzer, ikone, aplete, prozore, toolbar-ove, foldere, pozadine (wallpaper-e), skup aplikacija i mogucnosti poput prevuci i ispusti (drag and drop). Kada razmisljate o licnom desktopu, obicno je DE ono sto zelite. **See [Desktop okruzenja](/index.php/Desktop_environment#Desktop_environments "Desktop environment") za vise informacija.**

Mozete izgraditi vas licni DE koriscenjem WM-a i aplikacija prema vasem izboru.

Nakon sto ste instalirali graficki interfejs, verovatno cete zeleti da nastavite sa [Generalnim preporukama](/index.php/General_recommendations "General recommendations") za instrukcije nakon instalacije.

#### Metode za startovanje vaseg grafickog okruzenja

##### Rucno

Mozda cete vise voleti da startujete X rucno iz vaseg terminala pre nego da startujete pravo u desktop. Za DE-specificne komande, molim vas pogledajte wiki stranicu vezanu za vas DE (desktop okruzenje) za vise informacija. Za vise generickih **X** komandi, molim vas pogledajte [sekciju za Xorg](/index.php/Xorg#Methods_for_starting_your_Graphical_Environment "Xorg").

##### Automatski

Mozda cete zeleti da imate desktop koji startuje automatski tokom butovanja umesto da startujete X rucno. Pogledajte [Display manager](/index.php/Display_manager "Display manager") za instrukcije za upotrebu menadzera za prijavljivanje ili [Startovanje X-a prilikom butovanja](/index.php/Start_X_at_Boot "Start X at Boot") za dve lagane metode koje se ne oslanjaju na displej menadzer-a.

## Dodatak

Za listu [Uobicajenih aplikacija](/index.php/Common_Applications "Common Applications") i [Laganih aplikacija](/index.php/Lightweight_Applications "Lightweight Applications"), posetite njihove zasebne clanke.

Pogledajte [Generalne preporuke](/index.php/General_recommendations "General recommendations") za uputstva nakon instalacije poput podesavanja skaliranja frekvencije procesora (CPU) ili font renderovanja.