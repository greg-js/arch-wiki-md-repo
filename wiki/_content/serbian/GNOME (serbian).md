Od [GNOME: Desktop projekat slobodnog softvera](http://www.gnome.org/about/):

	*GNOME je projekat koji pruza dve stvari: GNOME desktop okruzenje, jedan intuitivan i atraktivan desktop za korisnike, i GNOME razvojnu platformu, prosiriv frejmvork za izgradnju aplikacija koje se integrisu u ostatak desktopa.*

	*GNOME je **slobodan**, **koristan**, **dostupan**, **internacionalan**, **pogodan za razvoj aplikacija**, **organizovan**, **podrzan**, i **zajednica**.*

Ovaj clanak pokriva GNOME desktop okruzenje.

## Contents

*   [1 Instalacija](#Instalacija)
    *   [1.1 Baza](#Baza)
    *   [1.2 Dodaci](#Dodaci)
*   [2 Daemoni i moduli koji su neophodni za GNOM](#Daemoni_i_moduli_koji_su_neophodni_za_GNOM)
*   [3 Pokretanje GNOM-a](#Pokretanje_GNOM-a)
*   [4 Dodela privilegija pod GNOM-om](#Dodela_privilegija_pod_GNOM-om)
    *   [4.1 Gasenje/restartovanje privilegija](#Gasenje.2Frestartovanje_privilegija)
    *   [4.2 Privilegije za skaliranje procesora](#Privilegije_za_skaliranje_procesora)
*   [5 GDM (GNOM menadzer ekrana)](#GDM_.28GNOM_menadzer_ekrana.29)
    *   [5.1 Podesavanje](#Podesavanje)
    *   [5.2 Automatsko prijavljivanje](#Automatsko_prijavljivanje)
    *   [5.3 Prijavljivanje bez sifre (predpredjivanje upozorenja za lozinku u GDM-u):](#Prijavljivanje_bez_sifre_.28predpredjivanje_upozorenja_za_lozinku_u_GDM-u.29:)
    *   [5.4 Vise](#Vise)
    *   [5.5 GDM legat](#GDM_legat)
*   [6 Ulepsavanje](#Ulepsavanje)
*   [7 Mintmeni (Napredni [Alternativni] GNOME meni)](#Mintmeni_.28Napredni_.5BAlternativni.5D_GNOME_meni.29)
*   [8 XDG korisnicki direktorijumi](#XDG_korisnicki_direktorijumi)
*   [9 Resavanje problema](#Resavanje_problema)
    *   [9.1 Generalno resenje](#Generalno_resenje)
    *   [9.2 Ukoliko vam sistem pada i GNOM vise ne startuje.](#Ukoliko_vam_sistem_pada_i_GNOM_vise_ne_startuje.)
    *   [9.3 GNOM lagovi](#GNOM_lagovi)
    *   [9.4 Ekran postaje crn dok se GNOM ucitava](#Ekran_postaje_crn_dok_se_GNOM_ucitava)
    *   [9.5 Imena fajlova sa losim karakterima na FAT particijama](#Imena_fajlova_sa_losim_karakterima_na_FAT_particijama)
    *   [9.6 gnome-terminal ne podrzava UTF-8 karaktere za mene](#gnome-terminal_ne_podrzava_UTF-8_karaktere_za_mene)
*   [10 Spoljasnji linkovi](#Spoljasnji_linkovi)

## Instalacija

### Baza

Instalirajte **xorg** dependency

```
# pacman -S xorg

```

Install the "base" GNOME desktop

```
# pacman -S gnome

```

Ovo je meta paket; koji je **grupa** paketa. Bice vam data opcija da instalirate sve ili neke od paketa iz ove grupe. Svi paketi mogu bezbedno da se instaliraju i to se preporucuje, medjutim postoji lista nekih paketa koji mozda nisu potrebni.

*   [epiphany](/index.php/Epiphany "Epiphany") je web pretrazivac koji dolazi uz GNOME. Ako planirate da koristite neki drugi pretrazivac, npr. [Firefox](/index.php/Firefox "Firefox"), onda ovaj paket nije potreban. Preporucuje se da bar probate Epiphany jer je to odlican pretrazivac koji je, nazalost, u senci Firefox-a.

*   [gnome-backgrounds](https://www.archlinux.org/packages/?name=gnome-backgrounds) je kolekcija desktop pozadina (wallpaper-i) koje je GNOME zajednica izabrala za vas da koristite. Ako vec znate sta cete koristiti za vasu pozadinu, npr. sliku vase drage osobe, onda ovaj paket nije potreban.

*   [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) je GUI terminal; ako vise volite neku drugu terminal aplikaciju poput [xterm](/index.php/Xterm "Xterm")-a ili aterm-a onda ovaj paket nije neophodan.

*   [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver) je kolekcija skrin sejvera za GNOME desktop. Ako necete koristiti skrin sejver ili cete koristiti GNOME menadzer za stednju energije da ugasite monitor kada nije u upotrebi onda ovaj paket nije potreban.

*   [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) je kolekcija desktop tema. Ako cete koristiti neku specificnu temu koju cete preuzeti odvojeno, onda ovaj paket nije potreban.

*   **gnome2-user-docs** i **yelp** su dokumenti za pomoc i citac dokumenata sa pomoc za GNOME desktop. Ako ste tip osobe koja ne cita dokumentaciju ili vise volite da koristite velike help dokumente poznate kao Google, onda nema potrebe da instalirate ove pakete. Ovo nije preporucljivo. (Ironicno, ako ste tip osobe koja ne cita dokumentaciju onda postoje sanse da necete ni ovo procitati.)

### Dodaci

Instalirajte ostatak GNOME Desktopa (vrlo preporucljivo, pogledajte [GNOME saveti](/index.php/GNOME_tips "GNOME tips")) sa:

```
# pacman -S gnome-extra

```

Kao i pre, ovo je meta paket, i preporucuje se da instalirate sve pakete iz ove grupe, ali postoji i lista nekih koji nisu neophodni. Ako jednostavno zelite da instalirate gnome-extra bez instaliranja Mono aplikacija poput Tomboy-ja, posetite [Mono](/index.php/Mono "Mono") stranicu za detalje kako da ga zablokirate.

*   **alacarte** je editor za gnome-menu; ako planirate da koristite meni, preporucuje se da koristite ovaj paket, iako to moze da se uradi rucno.

*   **bug-buddy** prijavljivanje bagova; ako ne zelite da prijavljujete bagove onda ovaj paket nije neophodan.

*   [cheese](https://www.archlinux.org/packages/?name=cheese) koristi vasu web kameru za preuzimanje slika i video snimaka; ako nemate web kameru onda ovaj paket nije neophodan.

*   [dasher](https://www.archlinux.org/packages/?name=dasher) je aplikacija za unos teksta koja koristi kursor umesto tastature. Ako vi i svi ostali koji ce koristiti taj desktop mogu da koriste tastaturu onda ovaj paket nije neophodan.

*   **deskbar-applet** je sve-u-jednom traka za pretrazivanje za GNOME desktop. Ako vam ne treba desktop pretrazivanje onda ovaj paket nije neophodan.

*   [ekiga](https://www.archlinux.org/packages/?name=ekiga) je VoIP (glas preko IP-a)/Video konferencijska aplikacija. Ako nemate potrebe za VoIP-om ili koristite neku drugu aplikaciju poput Skajpa, onda ovaj paket nije potreban.

*   [empathy](https://www.archlinux.org/packages/?name=empathy) je sve-u-jednom klijent za razmenu instant poruka. Ovo zamenjuje Pidgin kao startni program za cetovanje. Obavezno instalirajte odgovarajuce telepathy provajdere. Pogledajte optdepends za `pacman -Si empathy` za listu svih provajdera.

*   [eog](https://www.archlinux.org/packages/?name=eog) otvara skoro sve tipove slika; mozete da izaberete neku drugu aplikaciju za ovu svrhu.

*   [evince](https://www.archlinux.org/packages/?name=evince) je jednostavni pregledac za dokumenta (npr. pdf). Ako planirate da koristite neki drugi pregledac, npr. Adobe Reader, onda ovaj paket nije potreban.

*   **[evolution](/index.php/Evolution "Evolution")** je program za upravljanje licnim informacijama (e-mail, kalendar, kontakti, itd...) za GNOME. Ako planirate da koristite neku drugu aplikaciju za ovu svrhu, npr. Thunderbird, ili neku web aplikaciju poput Google ili Yahoo naloga onda ovaj paket nije potreban.

*   **evolution-exchange** je plugin za Evolution koji dozvoljava Evolution-u da se konektuje na Exchange. Ako ne koristite Exchange ili Evolution onda nemate potrebe za ovim paketom.

*   **evolution-webcal** je web kalendar plugin za Evolution. Ako ne koristite Evoluton onda nemate potrebe za ovim paketom.

*   **fast-user-switch-applet** je aplet koji omogucava prelazak sa korisnika na korisnika bez potrebe za odjavljivanjem (log out), tj. omogucava brzo smenjivanje korisnika. Ako postoji samo jedan korisnik na vasem racunaru ili ako volite da koristite ekran za prijavljivanje korisnika onda nema potrebe za ovim paketom.

*   [file-roller](https://www.archlinux.org/packages/?name=file-roller) je GUI menadzer za arhive koji radi kao winzip/winrar. Ako vise volite da odpakujete arhive preko komandne linije, ovaj paket nije neophodan.

*   [gcalctool](https://www.archlinux.org/packages/?name=gcalctool) , je pocetna kalkulator aplikacija sa razlicitim izgledima.

*   **gconf-editor** , editor za sva GNOM podesavanja.

*   **[gdm](/index.php/GDM "GDM")** olaksava startovanje GNOMA pri startovanju racunara. Ako vise volite da vam racunar startuje u tradicionalnu komandnu liniju i zelite da startujete GNOM samo kad vam zatreba, onda vam ovaj paket nije potreban.

*   [gedit](https://www.archlinux.org/packages/?name=gedit) je GUI baziran tekst editor. Ako planirate da koristite naki drugi tekst editor - kao sto je posvecenost vecine ljudi njihovim tekst editorima zapravo preraslo u religiju - onda nemate protrebe da instalirate ovaj paket. Gedit je vrlo dobar editor koji pruza korisne funkcije dok u isto vreme zadrzava stvari jednostavnim i pogotovo je dobar za pocetnike u programiranju koji ne zele da se muce sa vim-om, emacs-om ili kdevelop (note: ovo su sve odlicni programi koje vredi nauciti kasnije). Ima dosta korisnih pluginova kao sto je dodavanje/skidanje komentara na kodu, biranje boja i sadrzi takodje i terminal u sebi za brzo testiranje koda. Da bi ste koristili neki od ovih pluginova morate da instalirate zasebno gedit-plugins paket.

*   **gnome-audio** je kolekcija zvukova za dogadjaje u GNOME. Ako imate vase licne zvukove, ne zelite zvukove ili nemate zvuk uopste, onda ovaj paket nije potreban.

*   **gnome-games** i **gnome-games-extra-data** je kolekcija jednostavnih desktop igara; npr. Nibbles, Sudoku, itd. Ako mislite da su decije igre gubljenje vremena, prostora na hard disku i internet protoka onda ovaj paket nije za vas.

*   **gnome-mag** je lupa za ekran za ljude sa poremecenim vidom.

*   [gnome-nettool](https://www.archlinux.org/packages/?name=gnome-nettool) i **gnome-netstatus** su kolekcije GUI baziranih mreznih alata. Ako obavljate sve poslove vezane za mrezu preko komandne linije onda vam ne treba ovaj paket.

*   [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager) prati stanje baterije i drugih alata za pracenje stanja energije. Namenjeno je prvenstveno za laptop korisnike.

*   [gnome-system-monitor](https://www.archlinux.org/packages/?name=gnome-system-monitor) , je aplikacija koja prikazuje informacije o hardveru racunara i upotrebi sistemskih resursa.

*   [gnome-utils](https://www.archlinux.org/packages/?name=gnome-utils) je kolekcija programa za GNOME, ukljucujuci fajl loger, prikazivac logova, alatka za pretragu, recnik, podrska za flopi disk jedinicu i program za pravljenje slika od ekrana. Ovaj paket je preporucljiv za svakog korisnika.

*   **gucharmap** za gledanje Unicode karaktera.

*   **gok** je GNOME tastatura na ekranu. Ako korisnici vaseg racunara planiraju da koriste standardnu tastaturu za sve potrebe onda vam ne treba ovaj paket.

*   **hamster-applet** je aplet za pracenje vremena za GNOM panel. Mozete da posetite [website](http://projecthamster.wordpress.com/) za vise informacija.

*   **libgail-gnome** je GNOME implementaciona biblioteka za pristupacnost koja se koristi od strane citaca ekrana Orca.

*   [mousetweaks](https://www.archlinux.org/packages/?name=mousetweaks) je softver za pristupacnost za korisnike koji su ograniceni u koriscenju misa (npr. mogu da koriste samo jedno dugme).

*   [orca](https://www.archlinux.org/packages/?name=orca) je citac ekrana za GNOME desktop za korisnike sa ostecenim vidom.

*   [seahorse](https://www.archlinux.org/packages/?name=seahorse) i **seahorse-plugins** su paketi za enkriptovanje/deenkriptovanje informacija.

*   [sound-juicer](https://www.archlinux.org/packages/?name=sound-juicer) je program za ripovanje CD-ova za GNOME.

*   [tomboy](https://www.archlinux.org/packages/?name=tomboy) je jednostavna aplikacija za pravljenje beleski za vas desktop.

*   [totem](https://www.archlinux.org/packages/?name=totem) je oficijalni program za pustanje video fajlova (filmova) za GNOME desktop.

*   [vinagre](https://www.archlinux.org/packages/?name=vinagre) je VNC klijent za GNOME desktop.

*   [vino](https://www.archlinux.org/packages/?name=vino) je server za udeljani desktop za GNOME. Mozete da ga koristite da delite vas GNOME desktop sesiju sa drugim korisnicima.

*   **zenity** je alatka za prikazivanje GTK dijaloskih boksova u komandnoj liniji i skriptama za komandnu liniju.

Mozda ste primetili GNOME admin alate (*Sistem → Administracija*) koji nisu sadrzani u ekstra paketima. Trebace vam `gnome-system-tools` paket koji se instalira na sledeci nacin:

```
# pacman -S gnome-system-tools

```

Kao sto je vec receno gore, ovi i druge korisne informacije mozete naci na [Gnom saveti](/index.php/GNOME_tips "GNOME tips") wiki stranici.

**Note:** Upotreba `gnome-system-tools` na starijim GNOME verzijama ce najverovatnije zahtevati da ubacite vaseg korisnika u grupu `stb-admin`, u suprotnom mozete da dobijete poruku *"Podesavanje ne moze biti ucitano. Nije vam dozvoljen pristup sistemskim podesavanjima."*. Ovo nebi trebalo da je neophodno od verzije 2.28 `gnome-system-tools` jer ta verzija ne zahteva `stb-admin` grupu; ustvari, poboljsanje sa prethodne verzije ce ukloniti ovu grupu.

Da bi obicni korisnici koristili sistemske alate, neophodan je `gksu` paket:

```
# pacman -S gksu

```

Za podesavanje gksu koristite [Sudo](/index.php/Sudo "Sudo") pre nego [Su](/index.php/Su "Su"), i ovu komandu:

```
# gconftool-2 -s /apps/gksu/sudo-mode -t bool true

```

Proverite da li ste vec ispravno podesili [Sudo](/index.php/Sudo "Sudo").

Instalirajte [gamin](https://www.archlinux.org/packages/?name=gamin) ako zelite da izmene na fajlovima budu odmah detektovane.

Postoji mogucnost da vec imate instaliran FAM koji je zapostavljen. Ako ga imate instaliranog, uklonite ga kad budete upozoreni prilikom instaliranja gamin-a.

## Daemoni i moduli koji su neophodni za GNOM

GNOME desktop zahteva jedan daemon, [D-Bus](/index.php/D-Bus "D-Bus"), da bi radio kako treba.

Da startujete D-Bus daemon:

```
# /etc/rc.d/dbus start

```

Ili dodajte ove daemone u **DAEMONS** niz u `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` da bi startovali prilikom butovanja:

```
#
# /etc/rc.conf - Main Configuration for Arch Linux
#
.
.
# -----------------------------------------------------------------------
# DAEMONS
# -----------------------------------------------------------------------
#
# Daemons to start at boot-up (in this order)
#   - prefix a daemon with a ! to disable it
#   - prefix a daemon with a @ to start it up in the background
#
.
.
DAEMONS=(syslog-ng **dbus** network crond)

```

**GVFS** daje mogucnost nasadjivanja virtualnih fajl sistema (npr. fajl sistemi preko FTP-a ili SMB-a) za upotrebu od strane drugih aplikacija ukljucujuci GNOME fajl mendzer Nautilus. Ovo se radi upotrebom **FUSE**-a: virtualni fajl sistem sloj kernel modula za korisnicki prostor.

Za ucitavanje FUSE kernel modula:

```
# modprobe fuse

```

Ili dodajte modul u **MODULES** niz `/etc/rc.conf` da se ucitaju prilikom butovanja, npr.:

```
#
# /etc/rc.conf - Main Configuration for Arch Linux
#
.
.
# -----------------------------------------------------------------------
# HARDWARE
# -----------------------------------------------------------------------
#
# MOD_AUTOLOAD: Allow autoloading of modules at boot and when needed
# MOD_BLACKLIST: Prevent udev from loading these modules
# MODULES: Modules to load at boot-up. Prefix with a ! to blacklist.
#
# NOTE: Use of 'MOD_BLACKLIST' is deprecated. Please use ! in the MODULES array.
#
MOD_AUTOLOAD="yes"
#MOD_BLACKLIST=() #deprecated
MODULES=(**fuse** usblp)
.
.

```

**Note:** FUSE is a kernel module, not a daemon.

## Pokretanje GNOM-a

Dodajte sledecu liniju u vas `~/.xinitrc` fajl i uverite se da je to zadnja linija i jedina koja pocinje sa *exec* (pogledajte [xinitrc](/index.php/Xinitrc "Xinitrc")):

```
exec gnome-session

```

Sada ce GNOM startovati kada unesete sledecu komandu:

```
$ startx

```

## Dodela privilegija pod GNOM-om

### Gasenje/restartovanje privilegija

Ako je jedan korisnik ulogovan u GNOM i drugi korisnik se loguje (zamenjeni korisnici), drugi korisnik ne moze da ugasi ili restartuje racunar. Sledeci prozor izlazi, "Politika sistema sprecava sprecava zaustavljanje sistema kada su drugi korisnici prijavljeni. Korisnik ce biti upitan za super lozinku.

Diskusija: [https://bbs.archlinux.org/viewtopic.php?pid=641993](https://bbs.archlinux.org/viewtopic.php?pid=641993)

Popravka ovog je sledeca:

```
# nano /var/lib/polkit-1/localauthority/50-local.d/shutdown.pkla
[system shutdown privs]
Identity=unix-group:users
Action=org.freedesktop.consolekit.system.stop-multiple-users
ResultAny=no
ResultInactive=no
ResultActive=yes

```

```
# nano /var/lib/polkit-1/localauthority/50-local.d/restart.pkla
[system restart privs]
Identity=unix-group:users
Action=org.freedesktop.consolekit.system.restart-multiple-users
ResultAny=no
ResultInactive=no
ResultActive=yes

```

Konacno, restartujte hal i bilo koji korisnik u 'users' grupi ce imati mogucnost da ugasi ili restartuje sistem bez root lozinke i bez obzira da li su drugi prijavljeni na racunar ili ne.

Za vise detalja pogledajte man stranicu za pklocalauthority.

### Privilegije za skaliranje procesora

Pogledajte [cpufrequtils clanak](/index.php/Cpufreq#Privilege_Granting_Under_Gnome "Cpufreq").

## GDM (GNOM menadzer ekrana)

Ako zelite graficko prijavljivanje na sistem, trebace vam [GDM](http://www.gnome.org/projects/gdm/) (koji je takodje deo gnome-extra). Da to ucinite, ukucajte sledecu komandu u komandnoj liniji:

```
# pacman -S gdm

```

Da ucinite graficko prijavljivanje osnovnim metodom za prijavljivanje na sistem, editujte vas `/etc/inittab` fajl(preporucljivo). Alternativno mozete da dodate gdm u vasu listu daemona u `/etc/rc.conf`. Ove procedure su detaljno objasnjene na [Display manager](/index.php/Display_manager "Display manager") strani.

Ako ste naviknuti da koristite `~/.xinitrc` fajl za prosledjivanje argumenata za X server kada se startuje, poput **xmodmap** ili **xsetroot**, mozete da dodate iste komande u [xprofile](/index.php/Xprofile "Xprofile"). Primer:

 `~/.xprofile` 
```
#!/bin/sh

#
# ~/.xprofile
#
# Izvrsava se od strane gdm-a pri prijavljivanju
#

xmodmap -e "pointer=1 2 3 6 7 4 5" #ispravno podesava dugmice na misu
xsetroot -solid black                #podesava pozadinu na crnu boju

```

### Podesavanje

Ne mozete vise da koristite gdmsetup komandu da podesite GDM, i to od verzije 2.28\. Komanda je uklonjena i GDM je standardizovan i integrisan u ostatak Gnoma.

Mozete da instalirate gdm2setup iz AUR-a da podesite GDM ili da upotrebite sledece instrukcije.

**Note:** Iako sledece komande koriste sudo, ustvari vam treba da ih izvrsite kao root! ("su -" radi)

Podesavanje X server dozvolama za pristup

```
xhost +SI:localuser:gdm

```

Da podesite GDM teme upotrebite ovu komandu:

```
sudo -u gdm gnome-appearance-properties

```

Za vise opcija podesavanja, upotrebite ovu komandu:

```
sudo -u gdm gconf-editor

```

I izmenite sledece hijerarhije:

```
/apps/gdm/simple-greeter
/desktop/gnome/interface
/desktop/gnome/background

```

Ako ove komande budu bezuspesne sa greskom poput "Cannot open display" mozete da podignete dva prozora kada GDM startuje dodavanjem u GDM autostart. Da uradite ovo prvo napravite unos (kao root):

```
cp -t /usr/share/gdm/autostart/LoginWindow/ /usr/share/applications/gnome-appearance-properties.desktop /usr/share/applications/gconf-editor.desktop

```

Zatim se izlogujte iz vaseg korisnika nazad u GDM. Nakon sto se prozor za prijavljivanje pojavi, dva prozora bi takodje trebala da se pojave. Podesite GDM kako zelite, a zatim zatvorite prozore i ponovo se prijavite. Kada budete gotovi i zelite da se prozor vise ne otvara sa GDM-om, pokrenite ovo (kao root):

```
rm /usr/share/gdm/autostart/LoginWindow/gnome-appearance-properties.desktop /usr/share/gdm/autostart/LoginWindow/gconf-editor.desktop

```

**Note:** Upotrebom prijavljivanje/podesavanje metode mozete da vidite izmene dok ih pravite.

Za vise informacija i napredna podesavanja procitajte [ovo](http://library.gnome.org/admin/gdm/2.28/configuration.html.en).

### Automatsko prijavljivanje

Da omogucite automatsko prijavljivanje sa GDM-om, dodajte sledece u `/etc/gdm/custom.conf` (zamenite korisnika sa korisnickim imenom koje zelite da se automatski prijavljuje):

 `/etc/gdm/custom.conf` 
```
# Omogucite automatsko prijavljivanje za korisnika
[daemon]
AutomaticLogin=username
AutomaticLoginEnable=True

```

ili za automatsko prijavljivanje sa kasnjenjem:

 `/etc/gdm/custom.conf` 
```
[daemon]
# for login with delay
TimedLoginEnable=true
TimedLogin=username
TimedLoginDelay=1

```

### Prijavljivanje bez sifre (predpredjivanje upozorenja za lozinku u GDM-u):

Ako zelite da omogucite prijavljivanje bez lozinke na GNOME, onda jednostavno dodajte sledecu liniju u `/etc/pam.d/gdm`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

**Uverite se** da ova linije ide pravo ispod prve linije koja sadrzi "pam_unix.so" u sebi.

Zatim, dodajte grupu **nopasswdlogin** na vas sistem. To mozete da uradite graficki u System > Administration > Users and Groups. Pogledajte [Users and groups](/index.php/Users_and_groups "Users and groups") za opise grupa i komande za upravljanje grupama.

Sada, kada ste u System > Administration > Users and Groups (komanda: users-admin) i podesite vaseg korisnika za "Password: not asked at login" (cekiranjem "Don't ask for password on login" opcije), vas korisnik ce biti automatski dodat u "nopasswdlogin" grupu i tada cete moci jednostavnim klikom na vase korisnicko ime da se prijavite na sistem, tj. bez neophodne lozinke!

**Warning:** <u>NEMOJTE</u> OVO DA RADITE ZA ***ROOT*** NALOG!

### Vise

Napomenimo da sa verzijom 1.6.1 xorg-server, `Ctrl+Alt+Backspace` NECE vise restartovati gdm. Za uputstvo za ponovno osposobljavanje ove opcije, pogledajte [Xorg#Ctrl-Alt-Backspace doesn't work](/index.php/Xorg#Ctrl-Alt-Backspace_doesn.27t_work "Xorg").

Za vise informacija o grafickim prijavljivanjima (DM-ovi), pogledajte [ovau odlicnu stranu](http://endor.clublinux.org/RHCE-21.html).

### GDM legat

Ako zelite da se vratite na stari GDM, koji takodje ima alatku za podesavanje opcija, kompajlirajte i instalirajte [gdm-old](https://aur.archlinux.org/packages/gdm-old/) sa AUR-a.

## Ulepsavanje

Prema pocetnim podesavanjima, GNOME ne dolazi sa velikim brojem tema i ikona. Mozda cete zeleti da instalirate neke atraktivnije teme za GNOM:

Lep gtk endzin za teme (koji sadrzi i teme) je murrine endzin. Instalirajte sa:

```
# pacman -S gtk-engine-murrine

```

Ako zelite jos tema, mozete da ih preuzmete sa [murrine-themes-collection](https://aur.archlinux.org/packages/murrine-themes-collection/) sa AUR-a.

Kada ih instalirate, izaberite ih sa System -> Preferences -> Appearance -> Theme tab.

Arc Linuks repozitorijumi takodje imaju dodatnih tema i endzina. Instalirajte sledece da biste sami videli:

```
# pacman -S gtk-engines gtk-aurora-engine gtk-rezlooks-engine

```

Mozete naci jos mnogo tema, ikona i pozadina na [GNOME-Look](http://www.gnome-look.org).

Ali kako da namestim one zaista kul desktop efekte koje sam gledao na youtube-u? Pogledajte [Compiz](/index.php/Compiz "Compiz"). :)

## Mintmeni (Napredni [Alternativni] GNOME meni)

Instalirajte paket iz AUR-a [mintmenu](https://aur.archlinux.org/packages/mintmenu/) upotrebom [AUR](/index.php/AUR "AUR") po vasem izboru. Ime paketa:

```
mintmenu

```

Mintmenu koristi gconf da skladisti svoja podesavanja, ukljucujuci meni ikonu za prikaz. Ako je vasa trenutna vrednost `/usr/lib/linuxmint/mintMenu/mintMenu.png`, ovo moze biti zbog prethodne verzije tog paketa koji je uskladistio vrednost u `/apps/mintMenu/applet_icon`. Na svezoj instalaciji `/apps/mintMenu/applet_icon` vrednost je prema pocetnim podesavanjima `/usr/share/archlinux/icons/archlinux-icon-tango-16.svg`. Vrednost moze da se promeni sa gconf-editor, gconftool-2 ili iz Preferences (Right click on menu -> Preferences -> "Main Button" -> "Button icon:".

## XDG korisnicki direktorijumi

Mnoge Linuks distribucije poput Ubuntu ili Linux Mint dolaze prekonfigurisane sa vasim pocetnim korisnickim direktorijumima kao sto su downloads direktorijum, direktorijum za muziku, za dokumenta itd... To takodje dodeljuje tim specijalnim direktorijumima ikone. Da podesite XDG korisnicke direktorijume, izvrsite ovu komandu:

```
# pacman -S xdg-user-dirs

```

Startna podesavanja korisnickog direktorijuma su skladistena u `/etc/xdg/user-dirs.defaults`. Mozete da ih editujete i izmenite startna podesavanja za one direktorijume za koje zelite da imate posebne ikone:

**Tip:** Ne morate da editujete ovaj fajl ako samo zelite da podesite XDG korisnicke direktorijume za jednog korisnika ili ukoliko su vam startna podesavanja prihvatljiva.

```
# nano /etc/xdg/user-dirs.defaults

```

Izvrsite ovo kao normalan korisnik da podesite vase direktorijume:

```
$ xdg-user-dirs-update

```

Ova komanda pravi direktorijume i podesava ih tako da GNOM zna da gde odrejeni fajlovi treba da idu po difoltu. Direktorijumi takodje imaju specijalne ikone u zavisnosti od toga sta konfiguracioni fajl govori GNOM-u o pojedinim direktorijumima.

Da kasnije editujete korisnicki konfiguracioni fajl, znajte da se nalazi u `~/.config/user-dirs.dirs`. Mozete da ga editujete izvrsavanjem sledece komande ili upotrebom vaseg omiljenog tekst editora:

```
$ nano ~/.config/user-dirs.dirs

```

## Resavanje problema

### Generalno resenje

Probajte sa svezim podesavanjima tako sto cete ukloniti stara podesavanja:

```
$ for d in .gnome* .gconf*; do mv "$d" "$d.old"; done

```

### Ukoliko vam sistem pada i GNOM vise ne startuje.

Moguce resenje je da obnovite direktorijum za "sesiju" u `~/.gnome2`.

```
$ mv ~/.gnome2/session ~/.gnome2/session.old

```

### GNOM lagovi

Pogledajte [FAQ stranicu](/index.php/FAQ#Q.29_Why_is_Arch_so_slow.3F_Programs_open_slowly_or_do_not_run_at_all.21 "FAQ") za moguca resenja.

Ako je gnom logovanje sporo, mozete da probate da onemogucite flopi jedinice u biosu. Ovo ce spreciti "flopi" modul da se ucitava i moze da smanji vreme logovanja.

### Ekran postaje crn dok se GNOM ucitava

Ako je ekran crn prilikom ucitavanja GNOM-a, mozete pokusati sledece.

Otvorite terminal i izvrsite:

```
$ gconf-editor

```

Nadjite:

```
/ → apps → gnome-power-manager → backlight

```

i promenite vrednost

```
brightness_ac

```

od 100 na 0 kliktanjem na njega. Nakon restartovanja sistema problem bi trebalo da nestane.

**Tip:** Ako se problem ponovo vrati, promenite vrednosti za osvetljenje nazad na 100, sto bi moglo da resi problem.

### Imena fajlova sa losim karakterima na FAT particijama

Podesavanjem ove opcije u gnome-mount, vas Linuks sismtemi ce citati i pisati fajlove sa istim karakterima kao Windows sistemi (vrlo korisno za USB uredjaje):

```
gconftool-2 -s /system/storage/default_options/vfat/mount_options --list-type=string -t list [shortname=lower,uid=,utf8]

```

Vec postoji [bag izvestaj za to](https://bugzilla.gnome.org/show_bug.cgi?id=487547).

### gnome-terminal ne podrzava UTF-8 karaktere za mene

Dodajte ove dve linije u `/etc/environment` fajl:

```
LANG="en_US.UTF-8"
LC_ALL="en_US.UTF-8"

```

Restartujte vas sistem i gnome-terminal ce raditi ispravno.

## Spoljasnji linkovi

*   [Oficijalni web sajt](http://www.gnome.org/)
*   [Oficijalna dokumentacija](http://www.gnome.org/learn/)
*   Teme, ikone i pozadine:
    *   [Gnom umetnost](http://art.gnome.org/)
    *   [Gnom izgled](http://www.gnome-look.org/)
*   GTK/GNOM programi:
    *   [Gnom fajlovi](http://www.gnomefiles.org/)
    *   [Lista Gnom projekata](http://www.gnome.org/projects/)