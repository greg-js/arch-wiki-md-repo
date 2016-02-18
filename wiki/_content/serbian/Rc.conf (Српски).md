`rc.conf` fajl (`/etc/rc.conf`) je vitalni konfiguracioni fajl u Arch Linux-u. Sadrži nekoliko često editovanih podešavanja poput vremenska zona(timezone); rasporeda tastature(keymap); kernel moduli, daemoni koji se učitavaju pri startovanju; itd.... u jednom zgodnom tekstualnom fajlu s ciljem ubrzanja procesa održavanja sistema.

## Contents

*   [1 Pregled](#Pregled)
*   [2 Lokalizacija](#Lokalizacija)
*   [3 Hardver](#Hardver)
*   [4 Umrežavanje](#Umre.C5.BEavanje)
*   [5 Daemoni](#Daemoni)

## Pregled

Ovako tipični `rc.conf` fajl izgleda nakon sveže instalacije ([izvorni kod](https://projects.archlinux.org/initscripts.git/tree/rc.conf)):

 `/etc/rc.conf` 
```
#
# /etc/rc.conf - Main Configuration for Arch Linux
#

# -----------------------------------------------------------------------
# LOCALIZATION
# -----------------------------------------------------------------------
#
# LOCALE: available languages can be listed with the 'locale -a' command
#   LANG in /etc/locale.conf takes precedence
# DAEMON_LOCALE: If set to 'yes', use $LOCALE as the locale during daemon
# startup and during the boot process. If set to 'no', the C locale is used.
# HARDWARECLOCK: set to "", "UTC" or "localtime", any other value will result
#   in the hardware clock being left untouched (useful for virtualization)
#   Note: Using "localtime" is discouraged, using "" makes hwclock fall back
#   to the value in /var/lib/hwclock/adjfile
# TIMEZONE: timezones are found in /usr/share/zoneinfo
#   Note: if unset, the value in /etc/localtime is used unchanged
# KEYMAP: keymaps are found in /usr/share/kbd/keymaps
# CONSOLEFONT: found in /usr/share/kbd/consolefonts (only needed for non-US)
# CONSOLEMAP: found in /usr/share/kbd/consoletrans
# USECOLOR: use ANSI color sequences in startup messages
#
LOCALE="en_US.UTF-8"
DAEMON_LOCALE="no"
HARDWARECLOCK="UTC"
TIMEZONE="Canada/Pacific"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

# -----------------------------------------------------------------------
# HARDWARE
# -----------------------------------------------------------------------
#
# MODULES: Modules to load at boot-up. Blacklisting is no longer supported.
#   Replace every !module by an entry as on the following line in a file in
#   /etc/modprobe.d:
#     blacklist module
#   See "man modprobe.conf" for details.
#
MODULES=()

# Udev settle timeout (default to 30)
UDEV_TIMEOUT=30

# Scan for FakeRAID (dmraid) Volumes at startup
USEDMRAID="no"

# Scan for BTRFS volumes at startup
USEBTRFS="no"

# Scan for LVM volume groups at startup, required if you use LVM
USELVM="no"

# -----------------------------------------------------------------------
# NETWORKING
# -----------------------------------------------------------------------
#
# HOSTNAME: Hostname of machine. Should also be put in /etc/hosts
#
HOSTNAME="myhost"

# Use 'ip addr' or 'ls /sys/class/net/' to see all available interfaces.
#
# Wired network setup
#   - interface: name of device (required)
#   - address: IP address (leave blank for DHCP)
#   - netmask: subnet mask (ignored for DHCP) (optional, defaults to 255.255.255.0)
#   - broadcast: broadcast address (ignored for DHCP) (optional)
#   - gateway: default route (ignored for DHCP)
# 
# Static IP example
# interface=eth0
# address=192.168.0.2
# netmask=255.255.255.0
# broadcast=192.168.0.255
# gateway=192.168.0.1
#
# DHCP example
# interface=eth0
# address=
# netmask=
# gateway=

interface=
address=
netmask=
broadcast=
gateway=

# Setting this to "yes" will skip network shutdown.
# This is required if your root device is on NFS.
NETWORK_PERSIST="no"

# Enable these netcfg profiles at boot-up. These are useful if you happen to
# need more advanced network features than the simple network service
# supports, such as multiple network configurations (ie, laptop users)
#   - set to 'menu' to present a menu during boot-up (dialog package required)
#   - prefix an entry with a ! to disable it
#
# Network profiles are found in /etc/network.d
#
# This requires the netcfg package
#
#NETWORKS=(main)

# -----------------------------------------------------------------------
# DAEMONS
# -----------------------------------------------------------------------
#
# Daemons to start at boot-up (in this order)
#   - prefix a daemon with a ! to disable it
#   - prefix a daemon with a @ to start it up in the background
#
# If you are sure nothing else touches your hardware clock (such as ntpd or
# a dual-boot), you might want to enable 'hwclock'. Note that this will only
# make a difference if the hwclock program has been calibrated correctly.
#
# If you use a network filesystem you should enable 'netfs'.
#
DAEMONS=(syslog-ng network crond)

```

## Lokalizacija

*   `[LOCALE](/index.php/LOCALE "LOCALE")`: Za podešavanje jezika na sistemu koji će se koristiti sa svim 18n-prijateljskim aplikacijama i pomoćnim programima. Možete preuzeti listu dostupnih lokaliteta izvršavanjem `locale -a` sa komandne linije. Difolt podešavanje je odgovarajuće za US English korisnike.
*   `HARDWARECLOCK`: Određuje da li hardverski sat, koji je sinhronizovan prilikom butovanja i gašenja računara, skladišti `UTC` vreme, ili `localtime`. `UTC` ima smisla jer u velikoj meri pojednostavljuje promenu vremenskih zona i pomeranje vremena. `localtime` je neophodan ako upražnjavate dualno butovanje sa nekim operativnim sistemom koji skladišti samo `localtime` u hardverski sat, poput Windows-a.

**Note:** GNU/Linux će se promeniti u-i-iz DST-a kad je `HARDWARECLOCK` podešavanje je podešeno na `UTC`, bez obzira na to da li je GNU/Linux pokrenut u vreme kada je DST ušao ili izašao. Kada je `HARDWARECLOCK` podešavanje podešeno na `localtime`, GNU/Linux neće podešavati vreme i radiće pod pretpostavkom da je vaš sistem dualni but sistem u tom trenutku i da drugi operativni sistem sam brine o DST prekidaču. Ako to nije slučaj, DST izmena se mora obaviti ručno.

*   `TIMEZONE`: Definise vašu vremensku zonu. Specifies your time zone. Moguće vremenske zone su relativna staza do zoneinfo fajla počev od direktorijuma `/usr/share/zoneinfo`. Naprimer, vremenska zona za Srbiju bi bila `Europe/Belgrade`, sto se odnosi na fajl `/usr/share/zoneinfo/Europe/Belgrade`.
*   `[KEYMAP](/index.php/KEYMAP "KEYMAP")`: Raspore tastera na tastaturi koji zelite da koristite. Ako zivite u SAD, verovatno koristite qwerty, koja se odnosi na nas (po difoltu). Dostupne tastature su u `/usr/share/kbd/keymaps`. Imajte na umu da ovo podešavanje vazi samo za TTYs, a ne bilo koje grafickie menadzere za prozore ili X!
*   `[CONSOLEFONT](/index.php/Fonts#Console_fonts "Fonts")`: Definise konzolni font koji se učitava sa `setfont` programom prilikom butovanja (ter-v14b naprimer). Fontovi koji su na raspolaganju se mogu naći u `/usr/share/kbd/consolefonts`. Za više informacija pogledajte: [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts")
*   `[CONSOLEMAP](/index.php/Fonts#Console_fonts "Fonts")`: Definise konzolnu mapu koja se učitava sa `setfont` programom prilikom butovanja (8859-1_to_uni naprimer). Dostupne mape se mogu naći u `/usr/share/kbd/consoletrans`. Najbolje je da podesite mapu na onu koja je odgovarajuća za vaš lokalni standard (8859-1 for Latin1, naprimer) ako koristite utf8 lokalni standard utf8 lokalni standard gore naveden i koristite programe koji generisu 8-bitni izlaz. Ako koristite X11 za svakodnevni rad, imajte na umu da ovo utiče samo na izlaz konzolnih aplikacija.
*   `USECOLOR`: Omogućite (ili onemogućite) obojene statusne poruke tokom butovanja.

## Hardver

*   `MOD_AUTOLOAD`: Ako je podešeno na "yes", Arch ce skenirati vaš hardver prilikom butovanja i pokušati da automatski učita odgovarajuće module za vaš sistem. To se radi sa [udev](/index.php/Udev "Udev").

**Tip:** Modul auto-loading se može onemogućiti da ubrza proces butovanja, ali korisnici moraju obezbediti da su svi neophodni moduli izlistani u `MODULES` nizu. [hwdetect](/index.php/Hwdetect "Hwdetect") pomocni program se može upotrebiti za detektovanje neophodnih modula; [lshwd](https://aur.archlinux.org/packages/lshwd/) je alternativni pomocni program dostupan u [AUR](/index.php/AUR "AUR").

*   `MODULES`: U ovom nizu možete da izlistate imena modula koje zelite da učitate tokom butovanja bez potrebe da ih vezujete za hardverski uređaj kao u `modprobe.conf`. Jednostavno dodajte ime modula ovde, razdvajajući unose sa prostorom, i stavite sve opcije u `modprobe.conf` ako je neophodno. Uzvicnik kao prefiks modula (!) će staviti na crnu listu taj modul prilikom butovanja (neće se učitati).

**Tip:** Korist od zadavanja mrežnih modula ovde je da Ethernet kartice pokrivene od strane izlistanih modula će uvek biti detektovane onim redosledom kojim su moduli izlistani. Ovo sprečava eventualno zbunjivanje interfejsa gde je vaš Ethernet hardver dodeljen nasumicno izabranim interfejsima nakon svakog buta. Jos bolji način da obavite ovo je da upotrebite obelezja statickog interfejsa podešavanjem [udev](/index.php/Udev "Udev")- na odgovarajući način.

*   `USELVM`: Skeniranje za [LVM](/index.php/LVM "LVM") obim grupe prilikom pokretanja sistema, neophodno ako koristite LVM. Podešavanje na "YES" izvršava vgchange tokom sysinit-a.

## Umrežavanje

*   `[HOSTNAME](/index.php/HOSTNAME "HOSTNAME")`: Podesite ovo na hostname od mašine, bez dela za domen. Ovo je u potpunosti vaš izbor, dokle god se držite slova, brojeva i nekoliko uobičajenih specijalnih karaktera poput crtice. Nemojte biti preterano kreativni ovde, i ako ste u nedoumici, koristite difolt.
*   `INTERFACES`: Ovde definisete podešavanja za vaše mrežne interfejse. Difolt linije i sadržani komentari objašnjavaju proces podešavanja dosta dobro. Ako ne koristite DHCP da podesite uređaj, imajte na umu da vrednost promenljive (cije ime mora biti jednako imenu uređaja koji bi trebalo da bude konfigurisano) je jednako liniji koja će biti dodata u `ifconfig` komandu ako ćete konfigurisati uređaj ručno u komandnoj liniji.
*   `ROUTES`: Ovde možete da definisete sopstvene statičke mrežne rute sa proizvoljnim imenima. Pogledajte primer za difolt gateway da bi dobili ideju o čemu se radi. U suštini citirani deo je identičan onom onom sto bi ste dodali za ručno određenu rutu sa add komandom, tako da je čitanje man route preporučljivo ako ne znate da pišete ovde, ili jednostavno ostavite ovo nepromenjeno.
*   `NETWORKS`: Ovo omogućava odgovarajuće [mrežne profile](/index.php/Network_profiles "Network profiles") prilikom butovanja. Mrežni profili omogućavaju zgodan način upravljanja više mrežnih podešavanja i namenjeni su da zamene standardne `INTERFEJSE`/ podešavanje `RUTA` sto se i dalje preporučuje za sisteme sa samo jednim mrežnim podešavanjem. Ako će se vaš računar povezivati na razne mreže u raznim vremenima (npr. laptop) onda možete da podesite profile u `/etc/network.d` direktorijumu. Postoje šablon fajlovi sadržani u `/etc/network.d/examples` koji se mogu upotrebiti za pravljenje novih profila.

## Daemoni

*   `[DAEMONS](/index.php/DAEMONS "DAEMONS")`: Ovaj niz jednostavno izlistava imena onih skripti koje su sadržane u `/etc/rc.d/` koje bi trebalo da startuju tokom procesa butovanja. Unosi u ovu listu se razdvajaju praznim prostorom. Ako ime skripte ima prefiks uzvicnik (!), neće se izvršiti. Ako skripta ima prefiks "at" simbol (@), onda će biti izvršena u pozadini, tj. startna sekvenca neće čekati za uspešan završetak pre nego sto nastavi dalje. Obično nije potrebno da menjate difolt podešavanja da bi ste dobili sistem koji radi, ali biće neophodno da editujete ovaj niz kad god instalirate novi sistemski servis poput `sshd`, i zelite da ga startujete automatski prilikom butovanja. Ovo je u suštini Arch-ov način rukovanja onim stvarima koje drugi obrađuju sa raznim simboličkim linkovima u jednom `init.d` direktorijumu. Za više informacija pogledajte: [Pisanje rc.d_skripti](/index.php/Writing_rc.d_scripts "Writing rc.d scripts")

**Note:** Redosled kojim su daemoni izlistani je bitan jer će se učitavati tim redosledom.