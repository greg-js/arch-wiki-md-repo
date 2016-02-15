**Note:** Ovo je deo visestranog clanka za Uputstvo za pocetnike.**[Kliknite ovde](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)")** ako biste pre zeleli da citate uputstvo u celosti.

## Contents

*   [1 Nakon instalacije](#Nakon_instalacije)
    *   [1.1 Osvezavanje](#Osvezavanje)
        *   [1.1.1 Podesavanje mreze (ako je neophodno)](#Podesavanje_mreze_.28ako_je_neophodno.29)
            *   [1.1.1.1 Zicni LAN (Lokalna mreza)](#Zicni_LAN_.28Lokalna_mreza.29)
            *   [1.1.1.2 Bezicni LAN (Lokalna mreza)](#Bezicni_LAN_.28Lokalna_mreza.29)
            *   [1.1.1.3 Proksi server](#Proksi_server)
            *   [1.1.1.4 Analogni modem, ISDN i DSL (PPPoE)](#Analogni_modem.2C_ISDN_i_DSL_.28PPPoE.29)
        *   [1.1.2 Osvezavanje, sinhronizacija i nadogradnja sistema sa pacman-om](#Osvezavanje.2C_sinhronizacija_i_nadogradnja_sistema_sa_pacman-om)
            *   [1.1.2.1 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
            *   [1.1.2.2 Repozitorijumi za pakete](#Repozitorijumi_za_pakete)
            *   [1.1.2.3 AUR](#AUR)
        *   [1.1.3 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
            *   [1.1.3.1 rankmirrors](#rankmirrors)
            *   [1.1.3.2 Provera odraza za aktuelne pakete](#Provera_odraza_za_aktuelne_pakete)
        *   [1.1.4 Bolje se upoznajte se pacman-om](#Bolje_se_upoznajte_se_pacman-om)
        *   [1.1.5 Osvezavanje sistema](#Osvezavanje_sistema)
            *   [1.1.5.1 Ignorisanje paketa](#Ignorisanje_paketa)
            *   [1.1.5.2 The Arch rolling release model (Arch-ov model novih verzija u letu)](#The_Arch_rolling_release_model_.28Arch-ov_model_novih_verzija_u_letu.29)
    *   [1.2 Dodavanje korisnika](#Dodavanje_korisnika)
        *   [1.2.1 Instalacija i podesavanje Sudo-a (Opciono)](#Instalacija_i_podesavanje_Sudo-a_.28Opciono.29)
*   [2 Dodatci](#Dodatci)
    *   [2.1 Zvuk](#Zvuk)
    *   [2.2 **G**raphical **U**ser **I**nterface (graficki korisnicki interfejs)](#Graphical_User_Interface_.28graficki_korisnicki_interfejs.29)
        *   [2.2.1 Instalacija X-a](#Instalacija_X-a)
        *   [2.2.2 Instalirajte video drajver](#Instalirajte_video_drajver)
            *   [2.2.2.1 NVIDIA Graficke karte](#NVIDIA_Graficke_karte)
            *   [2.2.2.2 ATI graficke kartice](#ATI_graficke_kartice)
        *   [2.2.3 Instalirajte drajvere za unos](#Instalirajte_drajvere_za_unos)
        *   [2.2.4 Podesavanje X-a(Opciono)](#Podesavanje_X-a.28Opciono.29)
            *   [2.2.4.1 Ne-US tastatura](#Ne-US_tastatura)
        *   [2.2.5 Testiranje X-a](#Testiranje_X-a)
            *   [2.2.5.1 Magistrala za poruke](#Magistrala_za_poruke)
            *   [2.2.5.2 Startujte X](#Startujte_X)
            *   [2.2.5.3 U slucaju gresaka](#U_slucaju_gresaka)
            *   [2.2.5.4 Treba vam pomoc?](#Treba_vam_pomoc.3F)
        *   [2.2.6 Instalijate fontove](#Instalijate_fontove)
        *   [2.2.7 Izaberite i instalirajte graficki interfejs.](#Izaberite_i_instalirajte_graficki_interfejs.)
        *   [2.2.8 Metode za startovanje vaseg grafickog okruzenja](#Metode_za_startovanje_vaseg_grafickog_okruzenja)
            *   [2.2.8.1 Rucno](#Rucno)
            *   [2.2.8.2 Automatski](#Automatski)

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

Molim vas pogledajte [Bezicni brzi start za zivo okruzenje](/index.php/Beginners%27_Guide/Installation#Wireless_Quickstart_For_the_Live_Environment "Beginners' Guide/Installation") za detalje u vezi konektovanja na bezicnu mrezu. Iako vise ne radite sa intalacionog medija, komande su iste sve dok imate instalirane sve neophodne pakete za bezicni (vajrles) internet (instalirano u sekciji "Izaberite pakete"). Upamtite, vas bezicni uredjaj mozda zahteva firmver da bi mogao da radi. Za resavanje eventualnih problema, posetite za vise detalja [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") stranicu.

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

* pacman omotaci (_**[AUR helpers](/index.php/AUR_helpers "AUR helpers")**_) vam mogu pomoci da bez poteskoca pristupite AUR-u.

#### /etc/pacman.d/mirrorlist

Definise pacman repozitorijum odraze i prioritete.

Otvorite `/etc/pacman.d/mirrorlist` u nekom tekst editoru i uklonite komentare (uklonite '#' ispred) za server koji se nalazi blizu vas. Zatim izdajte komandu za kompletno osvezenje paketa:

```
# pacman -Syy

```

Dodavanje dva --refresh ili -y zastava primorava pacman-a da osvezi sve liste paketa cak i ako se smatra da su vec aktuelni. Izdavanje -Syy _kad god se promeni odraz_, je dobra praksa i tako cete izbeci moguce glavobolje.

##### `rankmirrors`

Alternativno, mozete da koristite `rankmirrors`. `rankmirrors` je bash skripta koja ce pokusati da detektuje nekomentirane odraze naznacene u `/etc/pacman.d/mirrorlist` koji su najblize do instalacione masine bazirano na latenciji. Brzi odrazi ce u velikoj meri da unaprede performanse pacman-a i opsti Arch Linux dozivljaj. Ova skripta moze da se pokrene periodicno, pogotovo ako izabrani odrazi pruzaju nekonzistentan protok i/ili osvezenja. Imajte na umu da `rankmirrors` ne testira za protok. Alati poput `wget` ili `rsync` mogu biti upotrebljeni za efikasno testiranje protoka odraza nakon sto je novi `/etc/pacman.d/mirrorlist` generisan.

Izdajte sledecu komandu da kompletno osvezite bazu paketa, nadogradite i instalirate `curl`:

```
# pacman -Syyu curl

```

*   _Ako dobijete gresku u ovom koraku, upotrebite komandu "nano /etc/pacman.d/mirrorlist" i uklonite komentar za server koji vam odgovara._

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

*   **-m** Pravi home direktorijum za korisnika kao /home/**korisnicko-ime**. U okviru svojih home direktorijuma, korisnici mogu da pisu fajlove, brisu ih, instaliraju programe, itd. Home direktorijumi korisnika ce sadrzati njihove podatke i licne konfiguracione fajlove, takozvane 'tacka fajlove' (njihovo ime kao prefiks ima tacku), koji su 'skriveni'. (Da vidite tacka-fajlove, ukljucite odgovarajucu opciju u vasem fajl menadzeru ili pokrenite ls komandu sa -a prekidacem.) Ako postoji konflikt izmedju _korisnickih_ (pod /home/korisnicko-ime) i _globalnih_ konfiguracionih fajlova, (obicno pod /etc/) podesavanja u _korisnickom_ fajlu ce imati prednost. Tacka-fajlovi koji ce najverovatnije biti menjani od strane korisnika su .xinitrc i .bashrc fajlovi. To su konfiguracioni fajlovi za xinit i Bash. Oni omogucavaju korisniku mogucnost da promeni prozor menadzer koji ce biti startovan prilikom prijavljivanja i takodje aliase, komande zadate od strane korisnika i prostorne varijable. Kada je korisnik napravljen, njihovi tacka-fajlovi ce biti preuzeti iz /etc/skel direktorijuma gde obitavaju uzorci sistemskih fajlova.
*   **-g** Ime grupe ili broj korisnikove inicijalne grupe za prijavljivanje. Ime grupe mora da postoji. Ako je obezbedjen broj grupe, on mora da se odnosi na vec postojecu grupu. Ako nije zadat, ponasanje komande useradd ce zavisiti od USERGROUPS_ENAB varijable koja se nalazi u /etc/login.defs.
*   **-G** Lista dopunskih grupa kojih je korisnik isto clan. _Svaka grupa je odvojena od sledece zarezom, bez praznih prostora_. Prema pocetnim podesavanjima (default) korisnik pripada samo inicijalnoj grupi.
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

**Warning:** Nemojte da editujete /etc/sudoers direktno sa editorom; Greske u sintaksi mogu uzrokovati probleme (poput toga da root korisnik postane neupotrebljiv. Morate da koristite _visudo_ komandu da editujete /etc/sudoers.

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

**Note:** **vesa** drajver je genericki i trebalo bi da radi sa skoro svakim modernim skupom video cipova. Ako ne mozete da nadjete odgovarajuci drajver za vas skup video cipova, vesa _bi_ trebalo da radi sa bilo kojom karticom, ali pruza samo 2D.

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

**[Beginners' Guide (Српски)](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide (Српски)") stranice:**

[Predgovor](/index.php/Beginners%27_Guide/Preface_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Preface (Српски)") >> **[Priprema za instalaciju](/index.php/Beginners%27_Guide/Preparation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Preparation (Српски)")** >> [Instalacija osnovnog sistema](/index.php/Beginners%27_Guide/Installation_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Installation (Српски)") >> **Nakon instalacije** >> [Dalje citanje](/index.php/Beginners%27_Guide/Extra_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Beginners' Guide/Extra (Српски)")