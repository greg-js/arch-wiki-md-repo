**Tip:** Ovo je dio višestraničnog članka vodiča za početnike. **[Klikni ovdje](/index.php/Beginners%27_Guide_(Hrvatski) "Beginners' Guide (Hrvatski)")** ukoliko želiš čitati članak u cijelosti.

## Contents

*   [1 Instalacija](#Instalacija)
    *   [1.1 Odaberi instalacijski izvor](#Odaberi_instalacijski_izvor)
        *   [1.1.1 Konfiguriraj mrežu (mrežna instalacija)](#Konfiguriraj_mre.C5.BEu_.28mre.C5.BEna_instalacija.29)
            *   [1.1.1.1 Postavi ADSL most u interaktivnom okruženju (neobavezno)](#Postavi_ADSL_most_u_interaktivnom_okru.C5.BEenju_.28neobavezno.29)
            *   [1.1.1.2 Postavi bežičnu mrežu unutar interaktivnog okruženja (neobavezno)](#Postavi_be.C5.BEi.C4.8Dnu_mre.C5.BEu_unutar_interaktivnog_okru.C5.BEenja_.28neobavezno.29)
    *   [1.2 Postavi hardversko vrijeme](#Postavi_hardversko_vrijeme)
        *   [1.2.1 Dual boot](#Dual_boot)
    *   [1.3 Pripremi tvrdi disk](#Pripremi_tvrdi_disk)
        *   [1.3.1 Particioniranje tvrdih diskova (opće informacije)](#Particioniranje_tvrdih_diskova_.28op.C4.87e_informacije.29)
            *   [1.3.1.1 Tip particije](#Tip_particije)
            *   [1.3.1.2 Swap particija](#Swap_particija)
            *   [1.3.1.3 Particijski raspored](#Particijski_raspored)
            *   [1.3.1.4 Koliko velike moraju biti moje particije?](#Koliko_velike_moraju_biti_moje_particije.3F)
        *   [1.3.2 Ručno particioniranje tvrdog diska (pomoću cfdisk)](#Ru.C4.8Dno_particioniranje_tvrdog_diska_.28pomo.C4.87u_cfdisk.29)
        *   [1.3.3 Creating filesystems (general information)](#Creating_filesystems_.28general_information.29)
            *   [1.3.3.1 Filesystem types](#Filesystem_types)
            *   [1.3.3.2 A note on journaling](#A_note_on_journaling)
        *   [1.3.4 Manually configure block devices, filesystems and mountpoints](#Manually_configure_block_devices.2C_filesystems_and_mountpoints)
    *   [1.4 Select Packages](#Select_Packages)
    *   [1.5 Install Packages](#Install_Packages)
    *   [1.6 Configure the System](#Configure_the_System)
        *   [1.6.1 Can the installer handle this more automatically?](#Can_the_installer_handle_this_more_automatically.3F)
        *   [1.6.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [1.6.2.1 LOCALIZATION section](#LOCALIZATION_section)
            *   [1.6.2.2 HARDWARE section](#HARDWARE_section)
            *   [1.6.2.3 NETWORKING section](#NETWORKING_section)
            *   [1.6.2.4 DAEMONS section](#DAEMONS_section)
                *   [1.6.2.4.1 General information](#General_information)
        *   [1.6.3 /etc/fstab](#.2Fetc.2Ffstab)
        *   [1.6.4 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
        *   [1.6.5 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [1.6.6 /etc/resolv.conf](#.2Fetc.2Fresolv.conf)
        *   [1.6.7 /etc/hosts](#.2Fetc.2Fhosts)
        *   [1.6.8 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [1.6.9 Pacman Mirror](#Pacman_Mirror)
        *   [1.6.10 Root password](#Root_password)
        *   [1.6.11 Done](#Done)
    *   [1.7 Install Bootloader](#Install_Bootloader)
    *   [1.8 Reboot](#Reboot)

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

Na idućem ekranu odaberi postavljanje mrežnih opcija *Setup Network*. Bit će prikazana dostupna sučelja. Ukoliko je navedeno sučelje i HWaddr (**H**ard**W**are **addr**ess), tada je tvoj modul već učitan. Ukoliko sučelje nije navedeno, možeš ga pokrenuti unutar instalacije ili ručno putem druge virtualne konzole. Odaberi svoje sučelje za nastavak.

Instalacija će te zatim upitati želiš li koristiti DHCP. Odabiranjem "Yes" će se pokrenuti **dhcpcd** da otkrije dostupan gateway i zatraži IP-adresu; odabiranjem "No" ćeš morati ručno upisati mrežne postavke poput IP-adrese, maske i DNS-servera. Nakon toga se vraćaš u instalacijski meni mrežne instalacije *Net Installation Menu*.

Odaberi *Choose Mirror* te odaberi FTP ili HTTP zrcalni repozitorij. Zatim se vrati na glavni meni.

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

Driveri i uslužni programi za bežičnu mrežu su sada dostupni unutar interaktivnog okruženja instalacijskog medija. Dobro poznavanje bežičnog hardvera će biti ključno za uspješnu konfiguraciju. Primijeti da će iduća brzinska procedura, pokrenuta *na ovoj točci instalacije*, inicijalizirati tvoj bežični hardver samo tako da bude mogao biti korišten *tijekom instalacijskog procesa*. Čitavu ćeš proceduru (ili neku sličnu njoj) morati ponoviti jednom kada zaista instaliraš i pokreneš lokalni sustav.

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

| Enkripcija | Naredba |
| Bez enkripcije | `iwconfig wlan0 essid "linksys"` |
| WEP s hex ključem | `iwconfig wlan0 essid "linksys" key "0241baf34c"` |
| WEP s ASCII lozinkom | `iwconfig wlan0 essid "linksys" key "s:pass1"` |
| WPA | `wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf` |

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

**Warning:** Ako koristiš *localtime*, postoji šansa pojavljivanja nekih poznatih i nepopravljivih bugova.

**Note:** Bilo koja druga vrijednost rezultirat će u ostavljanju hardverskog sata onakvim kakav jest (što je korisno za virtualizaciju).

#### Dual boot

Ako dual-bootaš Windowse na svom računalu, imaš dvije opcije:

*   Postavi Arch Linux na *localtime*, a zatim kasnije (u [konfiguraciji sustava](#Konfiguriraj_sustav)) izbaci `hwclock` iz `DAEMONS` liste u `/etc/rc.conf` (Windowsi će se pobrinuti o izmjenama hardverskog sata). Ne preporuča se.
*   Postavi Arch Linux na UTC i natjeraj Windowse da isto koriste UTC (potreban je brza izmjena registryja, pogledaj [ovu stranicu](https://help.ubuntu.com/community/UbuntuTime#Make%20Windows%20use%20UTC) za upute). Također, ne dozvoli Windowsima da sinkroniziraju svoje vrijeme s Internetom, jer će to ponovno promijeniti hardverski sat u *localtime* mod. Ako želiš takvu funkcionalnost (sinkronizaciju s NTP-serverima), možeš koristiti **openntpd** na svom Arch-sustavu. Preporučeno.

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

*Na ovoj točci, napredniji korisnici GNU/Linuxa koji su upoznati s ručnim particioniranjem mogu preskočiti niže na [odabir paketa](#Odaberi_pakete).*

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

**/** (root) *Korijenska particija je primarna particija koja sadrži sve ostale; vrh hijerarhije. Svi direktoriji i datoteke se nalaze unutar korijenskog direktorija "/", čak ako se nalaze na drugačijim fizičkim uređajima. Sadržaj korijenske particije mora biti dovoljan da bi se sustav bootao, obnovio i/ili popravio. Neki direktoriji pod / su sami kandidati za posebne particije. (Pogledaj upozorenje niže.)*

**/boot** *Ovaj direktorij sadrži kernel, ramdisk slike, bootloader konfiguracijsku datoteku i bootloader razine. /boot sadrži i podatke koji se koriste prije nego kernel krene pokretati korisničke programe. To može uključivati sačuvane master boot sektore i datoteke rasporeda sektora.*

**Warning:** Osim /boot, direktoriji važni za bootanje su: '***/bin', '/etc', '/lib', i '/sbin'. Zato se ne smiju nalaziti na particijama na kojima se ne nalazi /.***

**/home** *Sadrži poddirektorije, svaki imenovan po jednom korisniku, za pohranu raznih osobnih podataka kao i konfiguracijskih datoteka specifičnih za svakog korisnika.*

**/usr** *Dok je root primarna particija, /usr je sekundarna hijerarhija za podatke svih korisnika sustava, što uključuje većinu višekorisničkih aplikacija. /usr sadrži dijeljene podatke koji se mogu samo čitati i ne smiju prebrisivati (osim u slučaju nadogradnje sustava).*

**Warning:** Zasebna /usr particija će uzrokovati neke probleme s udevom i pokvarit će [systemd](/index.php?title=Systemd_(Hrvatski)&action=edit&redlink=1 "Systemd (Hrvatski) (page does not exist)"). [izvor](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken)

**/tmp** *direktorij za programe koji zahtijevaju privremene datoteke poput '.lck' datoteke, koje se mogu koristiti da bi spriječile postojanje više instanci istog programa sve dok neki zadatak ne bude gotov, nakon čega se '.lck' datoteka briše. Programi ne smiju pretpostavljati da se sadržaj direktorija /tmp očuva između pokretanja tih programa; sadržaj tog direktorija se obično obriše prilikom svakog bootanja sustava.*

**/var** *sadrži podatke koji variraju: administratorske zapise, pacmanov cache i slično. Sve što se inače zapisivalo u /usr tijekom rada sustava danas se zapisuje unutar /var.*

***Postoji nekoliko prednosti ukoliko se koristi više particija umjesto jedne jedine:***:

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

*Ako pratiš gornja pravila, jedan tipični sustav će imati korijensku particiju / veličine 15 GB, /var particiju veličine 10 GB, swap particiju veličine 1 GB i /home particiju veličine preostalog dijela diska.*

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

**Note:** Since the latest developments of the Linux kernel which include the libata and PATA modules, all IDE, SATA and SCSI drives have adopted the sd*x* naming scheme. This is perfectly normal and should not be a concern.

#### Creating filesystems (general information)

##### Filesystem types

Again, a filesystem type is a very subjective matter which comes down to personal preference. Each has its own advantages, disadvantages, and unique idiosyncrasies. Here is a very brief overview of supported filesystems:

1.  [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") *Second Extended Filesystem*- Old, mature GNU/Linux filesystem. Very stable, but *without journaling support* or barriers, which can result in data loss in a power loss or system crash. May be inconvenient for root (/) and /home, due to very long fsck's. *An ext2 filesystem can easily be converted to ext3.*
2.  [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") *Third Extended Filesystem*- Essentially the ext2 system, but with journaling support and write barriers. ext3 is backward compatible with ext2\. Extremely stable and mature.
3.  [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") *Fourth Extended Filesystem*- Backward compatible with ext2 and ext3\. Introduces support for volumes with sizes up to 1 exabyte and files with sizes up to 16 terabytes. Increases the 32,000 subdirectory limit in ext3 to 64,000\. Offers online defragmentation ability.
4.  [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") (V3)- Hans Reiser's high-performance journaling FS uses a very interesting method of data throughput based on an unconventional and creative algorithm. ReiserFS is touted as very fast, especially when dealing with many small files. ReiserFS is fast at formatting, yet comparatively slow at mounting. Quite mature and stable. ReiserFS (V3) is not actively developed at this time. Generally regarded as a good choice for /var.
5.  [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) - IBM's **J**ournaled **F**ile**S**ystem- The first filesystem to offer journaling. JFS had many years of use in the IBM AIX® OS before being ported to GNU/Linux. JFS currently uses the least CPU resources of any GNU/Linux filesystem. Very fast at formatting, mounting and fsck's, and very good all-around performance, especially in conjunction with the deadline I/O scheduler. (See [JFS](/index.php/JFS "JFS").) Not as widely supported as ext or ReiserFS, but very mature and stable.
6.  [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") - Another early journaling filesystem originally developed by Silicon Graphics for the IRIX OS and ported to GNU/Linux. XFS offers very fast throughput on large files and large filesystems. Very fast at formatting and mounting. Generally benchmarked as slower with many small files, in comparison to other filesystems. XFS is very mature and offers online defragmentation ability.
7.  [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") - Also known as "Better FS" is a new filesystem with substantial new and powerful features similar to Sun/Oracle's excellent [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS"). These include snapshots, multi-disk striping and mirroring (basically software raid without mdadm), checksums, incremental backup, and on-the-fly compression (which can give a significant performance boost as well as save space), and more. It is still considered "unstable" as of January 2011, but has been merged into the mainline kernel under experimental status. Btrfs looks to be the future of linux filesystems, and is now offered as a root filesystem choice in all major distribution installers.

**Warning:** Btrfs has no fsck utility yet, so if any corruption occurs you cannot repair the filesystem.

*   JFS and XFS filesystems cannot be *shrunk* by disk utilities (such as *gparted* or *parted magic*)

##### A note on journaling

All above filesystems, except ext2, utilize [journaling](http://en.wikipedia.org/wiki/Journaling_file_system). Journaling file systems are fault-resilient file systems that use a journal to log changes before they are committed to the file system to avoid metadata corruption in the event of a crash. Note that not all journaling techniques are alike; specifically, only ext3 and ext4 offer *data-mode journaling*, (though, not by default), which journals *both* data *and* meta-data (but with a significant speed penalty). The others only offer *ordered-mode journaling*, which journals meta-data only. While all will return your filesystem to a valid state after recovering from a crash, *data-mode journaling* offers the greatest protection against file system corruption and data loss but can suffer from performance degradation, as all data is written twice (first to the journal, then to the disk). Depending upon how important your data is, this may be a consideration in choosing your filesystem type.

#### Manually configure block devices, filesystems and mountpoints

Specify each partition and corresponding mountpoint to your requirements. Recall that partitions end in a number. Therefore, **sda** is not itself a partition, but rather, signifies an entire drive.

Choose and create the filesystem (format the partition) for / by selecting **yes**. You will now be prompted to add any additional partitions. In our example, sda2 and sda4 remain. For sda2, choose a filesystem type and mount it as /var. Finally, choose the filesystem type for sda4, and mount it as /home.

**Note:** If you have not created and do not need a separate /boot partition, you may safely ignore the warning that it does not exist.

Return to the Main Menu.

### Select Packages

All packages during installation are from the [core] repository. They are further divided into **base**, and **base-devel**. Package information and brief descriptions are available [here](https://www.archlinux.org/packages/?repo=Core&arch=i686&limit=all&sort=pkgname).

First, select the package category:

**Note:** For expedience, all packages in **base** are selected by default. Use the space-bar to select and de-select packages.

*   base: Packages from the [core] repo to provide the minimal base environment. Always select this and do not remove any packages from it, as all packages in Arch Linux assume that *base* is always installed.
*   base-devel: Extra tools from [core] such as `make`, and `automake`. Most beginners should choose to install it, as many will probably need it later.

After category selection, you will be presented with the full lists of packages, allowing you to fine-tune your selections. Use the space bar to select and unselect.

**Note:** If connection to a wireless network is required, remember to select and install the **wireless_tools** package. Some wireless interfaces also need [**ndiswrapper**](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration") and/or a specific [**firmware**](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration"). If you plan to use WPA encryption, you will need [**wpa_supplicant**](/index.php/WPA_supplicant "WPA supplicant"). The [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") page will help you choose the correct packages for your wireless device. Also strongly consider installing **[netcfg](/index.php/Netcfg "Netcfg")**, which will help you set up your network connection and profiles after you reboot into your new system.

After selecting the needed packages, leave the selection screen and continue to the next step, **Install Packages**.

### Install Packages

*Install Packages* will install the selected packages to your new system. If you selected a CD-ROM/USB as the source, package versions from the CD-ROM/USB will be installed. If you opted for a netinstall, fresh packages will be downloaded from the Internet and installed.

**Note:** In some installers, you will be asked if you wish to keep the packages in the pacman cache. If you choose "yes", you will have the flexibility to [downgrade](/index.php/Downgrade "Downgrade") packages to previous versions in the future, so this is recommended (you can always clear the cache in the future).

### Configure the System

**Tip:** Closely following and understanding these steps is of key importance to ensure a properly configured system.

At this stage of the installation, you will configure the primary configuration files of your Arch Linux base system.

Now you will be asked which text editor you want to use; choose [nano](/index.php/Nano "Nano"), [joe](http://joe-editor.sourceforge.net/) or [vi](/index.php/Vim "Vim"). `nano` is generally considered the easiest of the three. Please see the related wiki pages of the editor you wish to use for instructions on how to use them. You will be presented with a menu including the main configuration files for your system.

**Note:** It is very important at this point to edit, or at least verify by opening, every configuration file. The installer script relies on your input to create these files on your installation. A common error is to skip over these critical steps of configuration.

#### Can the installer handle this more automatically?

Hiding the process of system configuration is in direct opposition to **[The Arch Way](/index.php/The_Arch_Way "The Arch Way")**. While it is true that recent versions of the kernel and hardware probing tools offer excellent hardware support and auto-configuration, Arch presents the user all pertinent configuration files during installation for the purposes of *transparency and system resource control*. By the time you have finished modifying these files to your specifications, you will have learned the simple method of manual Arch Linux system configuration and become more familiar with the base structure, leaving you better prepared to use and maintain your new installation productively.

#### /etc/rc.conf

Arch Linux uses the file `/etc/rc.conf` as the principal location for system configuration. This one file contains a wide range of configuration information, principally used at system startup. As its name directly implies, it also contains settings for and invokes the `/etc/rc*` files, and is, of course, sourced *by* these files.

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

	Optional, defaults to *255.255.255.0*. If you want to use a custom netmask, specify it here. **Leave this blank for DHCP.**

	broadcast

	Optional. If you want to use a custom broadcast address, specify it here. **Leave this blank for DHCP.**

	gateway

	If you set a static IP in "address", enter the IP address of the default gateway (eg. your modem/router) here. **Leave this blank for DHCP.**

	NETWORK_PERSIST 

	Setting this to "yes" will skip network shutdown. This is required if your root device is on NFS.

	NETWORKS

	This is an optional setting to be enabled only if using the [netcfg](/index.php/Netcfg "Netcfg") package with optional *dialog* package. Enable these netcfg profiles at boot-up. These are useful if you happen to need more advanced network features than the simple network service supports, such as multiple network configurations (ie, laptop users).

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

A [daemon](https://en.wikipedia.org/wiki/Daemon_(computing) is a program that runs in the background, waiting for events to occur and offering services. A good example is a web server that waits for a request to deliver a page (e.g.: httpd) or an SSH server waiting for a user login (e.g.: sshd). While these are full-featured applications, there are also daemons whose work is not that visible. Examples are a daemon which writes messages into a log file (e.g. syslog, metalog), and a daemon which provides a graphical login (e.g.: gdm, kdm). All these programs can be added to the daemons line and will be started when the system boots. Useful daemons will be presented during this guide.

**Tip:** All Arch daemon scripts reside under /etc/rc.d/

#### /etc/fstab

The [fstab](https://en.wikipedia.org/wiki/fstab "wikipedia:fstab") (for **f**ile **s**ystems **tab**le) is part of the system configuration listing all available disks and disk partitions, and indicating how they are to be initialized or otherwise integrated into the overall system's filesystem. The `/etc/fstab` file is most commonly used by the **mount** command. The mount command takes a filesystem on a device, and adds it to the main system hierarchy that you see when you use your system. **mount -a** is called from `/etc/rc.sysinit`, about 3/4 of the way through the boot process, and reads `/etc/fstab` to determine which options should be used when mounting the specified devices therein. If **noauto** is appended to a filesystem in `/etc/fstab`, **mount -a** will not mount it at boot.

*An example of `/etc/fstab`*

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
**Note:** If your system has more than one hard drive, the installer will default to using UUID rather than the sd*x* naming scheme, for consistent device mapping. **[Utilizing UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") has several advantages and may also be preferred to avoid issues if hard disks are added to the system in the future.** Due to active developments in the kernel and also udev, the ordering in which drivers for storage controllers are loaded may change randomly, yielding an unbootable system/kernel panic. Nearly every motherboard has several controllers (onboard SATA, onboard IDE), and due to the aforementioned development updates, `/dev/sda` may become `/dev/sdb` on the next reboot. For more information, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

	<dir>

	Describes the mount point for the filesystem. For swap partitions, this field should be specified as 'none'; (Swap partitions are not actually mounted.)

	<type>

	Describes the type of the filesystem. The Linux kernel supports many filesystem types. (For the filesystems currently supported by the running kernel, see `/proc/filesystems`). An entry 'swap' denotes a file or partition to be used for swapping. An entry 'ignore' causes the line to be ignored. This is useful to show disk partitions which are currently unused.

	<options>

	Describes the mount options associated with the filesystem. It is formatted as a comma-separated list of options with no intervening spaces. It contains at least the type of mount plus any additional options appropriate to the filesystem type. For documentation on the available options for non-nfs file systems, see mount(8).

	<dump>

	Used by the dump(8) command to determine which filesystems are to be dumped. dump is a backup utility. If the fifth field is not present, a value of zero is returned and dump will assume that the filesystem does not need to be backed up. *Note that dump is not installed by default.*

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

The *resolver* is a set of routines in the C library that provide access to the Internet Domain Name System (DNS). One of the main functions of DNS is to translate domain names into IP addresses, to make the Web a friendlier place. The resolver configuration file, or `/etc/resolv.conf`, contains information that is read by the resolver routines the first time they are invoked by a process.

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

Add your *hostname*, coinciding with the one specified in `/etc/rc.conf`, as an alias, so that it looks like this:

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

	**GRUB'**s root; the drive and partition where the kernel (/boot) resides, according to system BIOS. (More accurately, where GRUB's stage2 file resides). **NOT necessarily the root (/) file system**, as they can reside on separate partitions. GRUB's numbering scheme starts at 0, and uses an hd*x,x* format regardless of IDE or SATA, and enclosed within parentheses. The example indicates that /boot is on the first partition of the first drive, according to the BIOS, so (hd0,0).

	kernel

	This line specifies:

*   The path and filename of the kernel ***relative to GRUB's root***. In the example, /boot is merely a directory residing on the same partition as / and **vmlinuz-linux** is the kernel filename; `/boot/vmlinuz-linux`. If /boot were on a separate partition, the path and filename would be simply `/vmlinuz-linux`, being relative to **GRUB'**s root.
*   The `root=` argument to the kernel statement specifies the partition containing the root (/) directory in the booted system, (more accurately, the partition containing `/sbin/init`). An easy way to distinguish the 2 appearances of "root" in `/boot/grub/menu.lst` is to remember that the first root statement *informs GRUB where the kernel resides*, whereas the second `root=` kernel argument *tells the kernel where the root filesystem (/) resides*.
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

**Warning:** Make sure to install GRUB on **/dev/sdX** and **not /dev/sdX*#***! This is a common mistake.

**Tip:** For more details, see the [GRUB](/index.php/GRUB "GRUB") wiki page.

### Reboot

That is it; You have configured and installed your Arch Linux base system. Exit the install, and reboot:

 `# reboot` 
**Tip:** Be sure to remove the installation media and perhaps change the boot preference in your BIOS; otherwise you may boot back into the installation!

**[Vodič za početnike](/index.php/Beginners%27_Guide_(Hrvatski) "Beginners' Guide (Hrvatski)")**

* * *

[Predgovor](/index.php/Beginners%27_Guide/Preface_(Hrvatski) "Beginners' Guide/Preface (Hrvatski)") >> [Priprema](/index.php/Beginners%27_Guide/Preparation_(Hrvatski) "Beginners' Guide/Preparation (Hrvatski)") >> **Instalacija** >> [Nakon instalacije](/index.php/Beginners%27_Guide/Post-Installation_(Hrvatski) "Beginners' Guide/Post-Installation (Hrvatski)") >> [Bilješke](/index.php/Beginners%27_Guide/Extra_(Hrvatski) "Beginners' Guide/Extra (Hrvatski)")