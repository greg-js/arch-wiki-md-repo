**Note:** Ovo je deo visestranog clanka za Uputstvo za pocetnike.**[Kliknite ovde](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)")** ako biste pre zeleli da citate uputstvo u celosti.

## Contents

*   [1 Instalacija osnovnog sistema](#Instalacija_osnovnog_sistema)
    *   [1.1 Izaberite izvor za instalaciju](#Izaberite_izvor_za_instalaciju)
        *   [1.1.1 Podesavanje mreze (Netinstall)](#Podesavanje_mreze_.28Netinstall.29)
            *   [1.1.1.1 (A)DSL brzi start za zivo okruzenje](#.28A.29DSL_brzi_start_za_zivo_okruzenje)
            *   [1.1.1.2 Bezicni internet - brzi start za zivo okruzenje](#Bezicni_internet_-_brzi_start_za_zivo_okruzenje)
    *   [1.2 Podesavanje sata](#Podesavanje_sata)
    *   [1.3 Pripremite hard diskove](#Pripremite_hard_diskove)
        *   [1.3.1 Particionisanje hard diskova](#Particionisanje_hard_diskova)
            *   [1.3.1.1 Partition Info](#Partition_Info)
            *   [1.3.1.2 Swap particija](#Swap_particija)
            *   [1.3.1.3 Sema za particionisanje](#Sema_za_particionisanje)
            *   [1.3.1.4 Koliko velike particije treba da napravim?](#Koliko_velike_particije_treba_da_napravim.3F)
            *   [1.3.1.5 Kreiranje particija sa cfdisk](#Kreiranje_particija_sa_cfdisk)
        *   [1.3.2 Podesavanje tacaka za montiranje fajl sistema](#Podesavanje_tacaka_za_montiranje_fajl_sistema)
            *   [1.3.2.1 Fajl sistem tipovi](#Fajl_sistem_tipovi)
            *   [1.3.2.2 Napomena u vezi zurnalizovanja](#Napomena_u_vezi_zurnalizovanja)
    *   [1.4 Izaberite pakete](#Izaberite_pakete)
    *   [1.5 Instalacija paketa](#Instalacija_paketa)
    *   [1.6 Konfigurisanje sistema](#Konfigurisanje_sistema)
        *   [1.6.1 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [1.6.1.1 LOCALIZATION sekcija](#LOCALIZATION_sekcija)
            *   [1.6.1.2 HARDWARE sekcija](#HARDWARE_sekcija)
            *   [1.6.1.3 NETWORKING sekcija](#NETWORKING_sekcija)
            *   [1.6.1.4 DAEMONS sekcija](#DAEMONS_sekcija)
        *   [1.6.2 /etc/fstab](#.2Fetc.2Ffstab)
        *   [1.6.3 **/etc/mkinitcpio.conf**](#.2Fetc.2Fmkinitcpio.conf)
        *   [1.6.4 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [1.6.5 /etc/resolv.conf](#.2Fetc.2Fresolv.conf)
        *   [1.6.6 /etc/hosts](#.2Fetc.2Fhosts)
        *   [1.6.7 /etc/hosts.deny and /etc/hosts.allow](#.2Fetc.2Fhosts.deny_and_.2Fetc.2Fhosts.allow)
        *   [1.6.8 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [1.6.9 Pacman-Odraz](#Pacman-Odraz)
        *   [1.6.10 Root sifra](#Root_sifra)
        *   [1.6.11 Gotovo](#Gotovo)
    *   [1.7 Install and configure a bootloader](#Install_and_configure_a_bootloader)
        *   [1.7.1 For BIOS motherboards](#For_BIOS_motherboards)
            *   [1.7.1.1 Syslinux](#Syslinux)
            *   [1.7.1.2 GRUB](#GRUB)
        *   [1.7.2 For UEFI motherboards](#For_UEFI_motherboards)
            *   [1.7.2.1 Gummiboot](#Gummiboot)
            *   [1.7.2.2 GRUB](#GRUB_2)
    *   [1.8 Restartujte](#Restartujte)

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

**[Beginners' Guide (Српски)](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)") stranice:**

[Predgovor](/index.php/Beginners%27_Guide/Preface_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Preface (Српски)") >> **[Priprema za instalaciju](/index.php/Beginners%27_Guide/Preparation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Preparation (Српски)")** >> **Instalacija osnovnog sistema** >> [Nakon instalacije](/index.php/Beginners%27_Guide/Post-Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Post-Installation (Српски)") >> [Dalje citanje](/index.php/Beginners%27_Guide/Extra_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Extra (Српски)")