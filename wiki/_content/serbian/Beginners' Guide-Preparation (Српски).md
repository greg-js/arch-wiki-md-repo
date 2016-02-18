**Tip:** Ovo je deo Uputstva za pocetnike koji se sastoji iz vise strana. **[Kliknite ovde](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)")** ako zelite da citate uputstvo u celosti.

## Contents

*   [1 Priprema](#Priprema)
    *   [1.1 Preuzimanje najskorijeg instalacionog medija](#Preuzimanje_najskorijeg_instalacionog_medija)
        *   [1.1.1 Provera integriteta preuzetog fajla](#Provera_integriteta_preuzetog_fajla)
        *   [1.1.2 CD instaler](#CD_instaler)
        *   [1.1.3 Flash memorijski uredjaj ili USB stik](#Flash_memorijski_uredjaj_ili_USB_stik)
            *   [1.1.3.1 *nix metod](#.2Anix_metod)
            *   [1.1.3.2 Microsoft Windows metod](#Microsoft_Windows_metod)
        *   [1.1.4 Instalacija preko mreze](#Instalacija_preko_mreze)
        *   [1.1.5 Instalacija na virtualnu masinu](#Instalacija_na_virtualnu_masinu)
    *   [1.2 Pokretanje Arch Linux instalera](#Pokretanje_Arch_Linux_instalera)
        *   [1.2.1 Pokretanje sa medija](#Pokretanje_sa_medija)
        *   [1.2.2 Startovanje OS-a](#Startovanje_OS-a)
            *   [1.2.2.1 Resavanje problema prilikom pokretanja sistema](#Resavanje_problema_prilikom_pokretanja_sistema)
        *   [1.2.3 Izmena rasporeda tastera](#Izmena_rasporeda_tastera)
        *   [1.2.4 Dokumentacija](#Dokumentacija)

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

**[Beginners' Guide (Српски)](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)")**

* * *

[Predgovor](/index.php/Beginners%27_Guide/Preface_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Preface (Српски)") >> **Priprema** >> [Instalacija](/index.php/Beginners%27_Guide/Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Installation (Српски)") >> [Nakon instalacije](/index.php/Beginners%27_Guide/Post-Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Post-Installation (Српски)") >> [Dodaci/Prilog](/index.php/Beginners%27_Guide/Extra_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Extra (Српски)")