Članak će Vas voditi proces instalacije i podešavanja raznih komponenata **L**ightweight(lagano) **X**11 **D**esktop **E**nvironment(okruženje). LXDE je dizajniran da bude u mogućnosti da radi na računarima sa minimalnim hardverskim zahtevima, a zahteva samo nekoliko zavisnosti. LXDE dizajn filozofija je biti lagan i koristan.

## Contents

*   [1 Karakteristike](#Karakteristike)
*   [2 Komponente](#Komponente)
*   [3 Instalacija](#Instalacija)
*   [4 Startovanje desktopa](#Startovanje_desktopa)
*   [5 Kratki saveti i opravke za bagove](#Kratki_saveti_i_opravke_za_bagove)
    *   [5.1 Programi koji startuju automatski](#Programi_koji_startuju_automatski)
    *   [5.2 Digitalni aplet za sat](#Digitalni_aplet_za_sat)
    *   [5.3 Editovanje menija za aplikacije](#Editovanje_menija_za_aplikacije)
    *   [5.4 My Documents ime](#My_Documents_ime)
    *   [5.5 Podešavanja fontova](#Pode.C5.A1avanja_fontova)
    *   [5.6 Automatsko mountovanje (nasađivanje)](#Automatsko_mountovanje_.28nasa.C4.91ivanje.29)
        *   [5.6.1 NTFS sa Kineskim slovima](#NTFS_sa_Kineskim_slovima)
    *   [5.7 LXNM](#LXNM)
    *   [5.8 KDM i LXDE sesija](#KDM_i_LXDE_sesija)
    *   [5.9 lxpanel Dodavanje pokretača (aplikacija)](#lxpanel_Dodavanje_pokreta.C4.8Da_.28aplikacija.29)
    *   [5.10 lxpanel Dodavanje pokretača (lokacija)](#lxpanel_Dodavanje_pokreta.C4.8Da_.28lokacija.29)
    *   [5.11 Ikone/Kursor](#Ikone.2FKursor)
        *   [5.11.1 Kursor](#Kursor)
        *   [5.11.2 lxpanel Ikone](#lxpanel_Ikone)
        *   [5.11.3 My Documents Ikona](#My_Documents_Ikona)
    *   [5.12 Zamenite Window Menadžer](#Zamenite_Window_Menad.C5.BEer)
    *   [5.13 Gašenje i resetovanje iz LXDE-a](#Ga.C5.A1enje_i_resetovanje_iz_LXDE-a)
    *   [5.14 Problem pri nadogradnji na 0.4.1 verziju lxsessiona](#Problem_pri_nadogradnji_na_0.4.1_verziju_lxsessiona)
    *   [5.15 LXsession full](#LXsession_full)
    *   [5.16 Korišćenje KDEmod3 aplikacije sa LXDE](#Kori.C5.A1.C4.87enje_KDEmod3_aplikacije_sa_LXDE)
*   [6 Korisni LxDE linkovi](#Korisni_LxDE_linkovi)

## Karakteristike

Neke od LXDE karakteristika su:

*   **Laganost** - radi sa razumnom upotrebom operativne memorije. (Nakon što su [Xorg](/index.php/Xorg "Xorg") server i LXDE startovani, totalna iskorišćenost memorije je oko 45 megabajta na i686 mašinama.)
*   **Brz** - radi dobro čak i na starijim mašinama. (Hardverski zahtevi LXDE-a su slični kao za Windows 98.)
*   **Funkcionalni dizajn** - gtk2 korisnički interfejs i GNOME HIG standardi.
*   **Nezavisnost od desktopa** - komponente se mogu koristiti bez LXDE-a.
*   **U skladu je sa standardima** - prati specifikacije Freedesktop projekta.

## Komponente

Informacije o različitim komponentama:

*   **[PCManFM](/index.php/PCManFM "PCManFM")**: Fajl menadžer, desktop funkcionalnost, i pozadina na desktopu.
*   **[LXPanel](http://www.gnomefiles.org/app.php/LXPanel)**: Taskbar sa menadžerom aplikacija, meni za aplikacije, i veliki broj apleta.
*   **[LXSession](http://www.gnomefiles.org/app.php/LXSession)**: Saglasan sa standardima, X11 menadžer sesija sa ugasi/restartuj/suspenduj podrškom (zahteva [HAL](/index.php/HAL "HAL")).
*   **[LXAppearance](http://www.gnomefiles.org/app.php/LXAppearance)**: Editor za teme sposoban da menja GTK+ teme, teme za ikone, i fontove za GTK aplikacije.
*   **[Openbox](http://icculus.org/openbox/index.php/Main_Page)**: Lagan, saglasan sa standardima i visoko podesiv menadžer prozora (preporučiv menadžer prozora koji se ne razvija u okviru LXDE projekta)
*   **[Obconf](http://tr.openmonkey.com/pages/obconf/)** - Alat za podešavanje tema i stilova Openbox-a.
*   **[GPicView](http://lxde.sourceforge.net/gpicview/)**: Osnovni, lagani program za gledanje slika.
*   **[Leafpad](http://tarot.freeshell.org/leafpad/)**: Lagani i osnovni tekst editor (ne razvija se u okviru LXDE projekta).
*   **[XArchiver](http://xarchiver.xfce.org/)**: Lagani fajl arhiver (ne razvija se u okviru LXDE projekta).
*   **[LXNM](http://lxde.sourceforge.net/about.html)** Lagani menadžer za mrežu za bežične konekcije pod razvojem. Možete naći [lxnm](https://aur.archlinux.org/packages/lxnm/) u [AUR](/index.php/AUR "AUR").

## Instalacija

LXDE je modularan pa možete da birate pakete koji Vam trebaju. Neki paketi su eksperimentalni i moraćete da koristite [AUR](/index.php/AUR "AUR") repozitorijum da bi ih instalirali.

Minimalan broj obaveznih paketa koje morate da instalirate da bi ste pokrenuli LXDE su [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession), [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils), i prozor menadžer.

Instalirajte LXDE grupu sa:

```
# pacman -S lxde

```

Instalacija lxde grupe će instalirati sledeće pakete:

*   gpicview
*   lxappearance
*   lxde-common
*   lxde-icon-theme
*   lxlauncher
*   lxmenu-data
*   lxpanel
*   lxrandr
*   lxsession-lite
*   lxtask
*   lxterminal
*   menu-cache
*   openbox
*   pcmanfm

Takođe će biti neophodno da instalirate [Gamin](/index.php/Gamin "Gamin"). Gamin je je alakta za monitoring fajlova i direktorijuma dizajniran da bude podset FAM-a. Pokreće se na zahtev programa koji imaju podršku za njega, tako da mu nije neophodan daemon kao što to fam zahteva. Ako imate instaliran fam, uklonite ga iz DAEMON niza `/etc/rc.conf` i zaustavite daemon pre nego što instalirate gamin.

```
pacman -S gamin

```

Drugi lagani paketi koje ćete možda želeti da instalirate:

```
pacman -S leafpad xarchiver obconf epdfview

```

Za više informacija pogledajte na [Lightweight_Applications](/index.php/Lightweight_Applications "Lightweight Applications").

## Startovanje desktopa

Možete startovati LXDE na nekoliko različitih načina. Ako koristite displej menadžere poput [SLiM](/index.php/SLiM "SLiM"), [GDM](/index.php/GDM "GDM"), ili [KDM](/index.php/KDM "KDM"), otvorite sesija opciju i izaberite. Da bi ste bili u mogućnosti da uradite ovo iz konzole, nekoliko drugih opcija postoji.

Da bi ste koristili **startx** neophodno je da definišete LXDE u Vašem [`~/.xinitrc`](/index.php/Beginners%27_Guide_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)#Jednostavan_X_test "Beginners' Guide (Српски)") fajlu:

```
exec startlxde

```

Da bi ste startovali LXDE iz komandne linije bez `~/.xinitrc` (ako `~/.xinitrc` već postoji ovo neće raditi):

```
$ xinit /usr/bin/startlxde

```

Ako želite da pokrenete **startx** automatski prilikom startovanja sistema, bacite pogled na [starting X at login](/index.php/Start_X_at_login#Starting_X_as_preferred_user_without_logging_in "Start X at login") uputstvo.

## Kratki saveti i opravke za bagove

Saveti za rad sa LXDE programima i opravke za bagove.

### Programi koji startuju automatski

	.desktop fajlovi

Prvo možete da linkujete fajlove programa `.desktop` na `~/.config/autostart/`. Instalirani programi umeću svoje `.desktop` fajlove u `/usr/share/applications`. Naprimer:

```
$ ln -s /usr/share/applications/lxterminal.desktop ~/.config/autostart/

```

Pošto su `.desktop` fajlovi dodati, možete da manipulišete njima sa GKI (grafički korisnički interfejs) konfiguracionim alatom [lxsession-edit](https://aur.archlinux.org/packages/lxsession-edit/).

	autostart file

Drugi metod je upotreba `~/.config/lxsession/LXDE/autostart` fajla.

```
$ touch ~/.config/lxsession/LXDE/autostart

```

Dodajte program koji bi ste želeli da startuje u novu liniju sa *@* prefiksom (i bez *&* na kraju):

```
@lxterminal
@leafpad

```

	Globalno automatsko startovanje

Treći metod je upotreba globalnog fajla `/etc/xdg/lxsession/LXDE/autostart`. Ovaj fajl nije shell skripta, već svaka linija predstavlja različitu komandu koja treba da se izvrši. Ako linija počinje sa @, komanda koja sledi posle @ će biti automatski restartovana ako dođe do zablokiranja. Ako oba `~/.config/lxsession/LXDE/autostart` i `/etc/xdg/lxsession/LXDE/autostart` fajla su prisutna, svi unosi u oba fajla će biti izvršeni.

### Digitalni aplet za sat

Da dobijete standardno vreme (ne vojno vreme) upotrebite hh:mm i hh:mm:ss format (`man strftime` za više opcija):

```
%I:%M
%I:%M:%S

```

### Editovanje menija za aplikacije

Meni za aplikacije radi kroz rešavanje fajlova sa informacijama za startovanje programa u njima (imenovanih `.desktop` fajlovi) koji se nalaze u `/usr/share/applications`. Mnoga desktop okruženja pokreću programe koji zamenjuju ova podešavanja da bi dozvolili prilagođavanje menija sopstvenim potrebama. LXDE-u još predstoji da kreira aplikaciju za editovanje menija, ali Vi možete ručno da ga napravite ukoliko ste skloni tome.

Da bi ste dodali program u meni (ili da editujete meni stavku), napravite link ka `.desktop` fajlu u `~/.local/share/applications`.

Da uklonite stavke iz menija, moraćete da editujete `.desktop` fajlove i da opišete da program ne treba da bude prikazan. Prvo, kopirajte fajlove iz Vaše globalne liste programa u Vašu lokalnu korisničku meni lokaciju.

```
cp /usr/share/applications/example.desktop ~/.local/share/applications

```

Zatim dodajte u fajl `NoDisplay=true`. Da bi ste ubrzali proces na veći broj falova, možete upotrebiti petlju. Na primer:

```
cd /usr/share/applications
for i in program1.desktop program2.desktop ...; do cp /usr/share/applications/$i \
/home/user/.local/share/applications/; echo "NoDisplay=true" >> \
/home/user/.local/share/applications/$i; done
```

Ovo će raditi za sve aplikacije izuzev KDE aplikacija. Za ove je jedini način da ih uklonite iz menija da se prijavite na sam KDE i upotrebite njegov meni editor. Za svaku stavku koju ne želite da bude prikazana, označite 'Show only in KDE' opciju.

### My Documents ime

Fascikla na desktopu pod imenom 'My Documents' je tvrdo-kodirana u pcmanfm-u. U ovom momentu ne postoji mogućnost za promenu njenog imena.

### Podešavanja fontova

Većina korisnika LXDE-a obično pokušava da koristi GTK programe jer GTK se koristi kao pozadina za LXDE. Da podesite fontove, možete da koristite [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) i da podesite glavni font, ali za druge fontove ćete morati da upotrebite Gnome 'Font Preferences' kontrolni panel. Da ga instalirate:

```
pacman -S gnome-control-center

```

Nakon što ste podesili Vaša podešavanja, možete da uklonite programe jer će podešavanja biti zadržana.

### Automatsko mountovanje (nasađivanje)

Ako želite da se odstranjivi uređaji za skladištenje podataka automatski nasađuju sa [PCManFM](/index.php/PCManFM "PCManFM"), morate da instalirate [HAL](/index.php/HAL "HAL") i dodate Vašeg korisnika u hal grupu:

```
# gpasswd -a Vaše_korisničko_ime hal

```

Zatim je pmount neophodan za nasađivanje odstranjivih uređaja bez root pristupa sistemu:

```
pacman -S pmount

```

Sada se odjavite i ponovo prijavite na sistem da bi Vaš korisnik bio prepoznat kao deo hal grupe.

#### NTFS sa Kineskim slovima

Za prikazivanje Kineskih slova potrebno je uraditi sledeće

*   Uklonite "/sbin/mount.ntfs-3g" što je symlink.

```
rm /sbin/mount.ntfs-3g

```

*   Kreirajte nov "/sbin/mount.ntfs-3g" Sa novom bash skriptom koja sadrži:

```
#!/bin/bash
/bin/ntfs-3g $1 $2 -o locale=en_US.UTF-8

```

*   Stavite da bude executable:

```
chmod +x /sbin/mount.ntfs-3g 

```

*   Dodajte "NoUpgrade = sbin/mount.ntfs-3g" to pacman.conf under the "[options]"

### LXNM

LXNM je program koji je zasnovan na skriptama koji pokušava da upravlja mrežnim konekcijama.Nije potpun program kao [NetworkManager](/index.php/NetworkManager "NetworkManager"). Ako želite veću kontrolu tu je onda , [Wicd](/index.php/Wicd "Wicd") i Gnome verzija [NetworkManager](/index.php/NetworkManager "NetworkManager") koji radi korektno na LxDE okruženju.

```
Možete instalirat LXNM iz [community] riznice sa sledećom komandom: pacman -S lxnm

```

Glavnu skriptu je potrebno pokrenit kao root. Ako mislite da je koristite češće stavite je u `/etc/rc.conf`.

### KDM i LXDE sesija

Od KDE-a 4.3.3, KDM ne prepoznaje LXDE desktop sesiju. Da bi dodali LxDE u KDM potrebno je dodat sledeću komandu:

```
# cp /usr/share/xsessions/LXDE.desktop /usr/share/apps/kdm/sessions/

```

### lxpanel Dodavanje pokretača (aplikacija)

lxpanel dolazi sa pokretačima po podrazumevanim vrednostima, da bi dodali novi pokretač potrebno je sledeće:

1.  Make sure launch bar applet is enabled:
    *   1a. desni klik na panel
    *   1b. izaberite "add/remove panel items"
    *   1c. uverite se da "application launch bar" je izlistana (ako nije, izaberite "add" i dodajte je)
2.  Desni klik bilo gde na pokretačkoj traki
3.  Izaberite "application launch bar settings"
4.  Izaberite "add"
5.  Izaberite .desktop fajl koje želite da dodate (nalaze se u /usr/share/applications)

### lxpanel Dodavanje pokretača (lokacija)

Da dodate pokretač za posebnu lokaciju kao što je hard disk ili folder potrbno je napraviti .desktop fajl i snimiti ga u /usr/share/applications. Možete ga dodati na isti način kako ste dodavali i aplikacije.

Evo jedan primer .desktop fajla, izmenite "Exec" i "Icon" ako je potrebno:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Name=media
Exec=pcmanfm /mnt/xbox (basically you are telling pcmanfm to open a specific location - /mnt/xbox in this case)
Icon=xbmc.png (this should be the name of an icon in /usr/share/pixmaps)
Terminal=false
X-MultipleArgs=false
Type=Application
Categories=Application
StartupNotify=true

```

### Ikone/Kursor

Podešavanje ikona i kursora.

#### Kursor

Na LxDE-u je sada vrlo lako instalirat teme za kursor, sa novim lxapperencom koji ima integrisno podešavanja za menjanje tema za miša.

#### lxpanel Ikone

Podrazumevane ikone koji koristi lxpanel ,pohranjene su na `/usr/share/pixmaps` i bilo koje dodatne ikone koje želite da lxpanel koristi potrebno je da tamo snimite.

Možete promeniti podrazumevane ikone za aplikacije,tako što ćete slediti ove korake:

1.  Snimite nove ikone u /usr/share/pixmaps
2.  Koristite tekstualni editor da otvorite .desktop fajl od programa kojem oćete ikonu da promenite (.desktop se nalazi u /usr/share/applications)
3.  Promenite

```
Icon=/default/icon/.png 

```

U

```
Icon=/name/of/new/icon/added/to/pixmaps/.png

```

#### My Documents Ikona

Desktop ikona"My Documents" nemože se ukloniti. Ona je kompajlirana direktno u pcmanfm, fajl src/desktop/desktop-window.c. Ako se promeni tema ikona, i ako nepostoji My Documents ikona potrebno je napraviti ikonu, ili u protivnom je neće biti.

### Zamenite Window Menadžer

OpenBox, je podrazumevani window manager na LXDE-u,i on se može lako zameniti sa onim koji vama odgovara, kao naprime fvwm, icewm, dwm,awesome... itd..

U ovom fajlu LXDE drži postavke za svoj window manager:

	/etc/xdg/lxsession/LXDE/config

Kao podrazumevana vrednost postavljeno je sledeće

```
[Session]
window_manager=openbox-lxde

```

Zamenite openbox-lxde sa window manager koji vama odgovara.

Takođe može se i ovde pogledati:

	/etc/xdg/lxsession/LXDE/default

Ove podrazumevane vrednosti se čine zastarele, kao što je i naznačeno u ovim komentarima:

```
! This file is kept for backward compatibility.
! Only used by obsolete lxsession, not lxsession-lite.

```

Evo jedan primer kako bi trebao da izgleda /etc/xdg/lxsession/LXDE/default

```
smproxy
openbox
lxpanel

```

smproxy je program u okviru xorg-a. On obezbeđuje podršku za upravljanje programima koji nisu u X11 R6 i preporučuje se da se doda u podešavanjima

### Gašenje i resetovanje iz LXDE-a

Da bi bili u mogućnosti da pokrećete,resetujete računar iz lxde-a treba da imate pokrenut DBus i HAL. Zatim treba da imate vaš username u grupi power.

```
# gpasswd -a <USERNAME> power

```

Ako i dalje imate problem, dodajte između ovih linija <config></config> tags in /etc/PolicyKit/PolicyKit.conf sledeće linije:

```
<match action="org.freedesktop.hal.power-management.shutdown">
 <return result="yes"/>
</match>
<match action="org.freedesktop.hal.power-management.reboot">
 <return result="yes"/>
</match>
<match action="org.freedesktop.hal.power-management.suspend">
 <return result="yes"/>
</match>
<match action="org.freedesktop.hal.power-management.hibernate">
 <return result="yes"/>
</match>

```

Zatim resetujte HAL.

### Problem pri nadogradnji na 0.4.1 verziju lxsessiona

Kada pokrećete neki GTK2 program i dobijete:

```
 GTK+ icon them is not properly set

```

```
 Ovo obično znači da nemate pokrenut XSETTINGS manager. Desktop okruženja kao GNOME ili XFCE automatski izvršuju

```

njihove XSETTING menadžere kao gnome-settings-daemon ili xfce-mcs-manager.

Da bi vam radio lxde-settings-daemon potrebno je da prebacite sledeće fajlove u vaš home direktorijum :

```
 /usr/share/lxde/config
 ~/.config/lxde/config

```

I

```
 etc/xdg/lxsession/LXDE/desktop.conf
 ~/.config/lxsession/LXDE/desktop.conf

```

Takođe možete da koristite lxappearance iz community riznice da popravite ovo.

### LXsession full

Još postoje bagovi u punom lxsession managementu. Zato se preporučuje da se koristi ***lxsession-lite*** dok se problemi u lxsession reše.

### Korišćenje KDEmod3 aplikacije sa LXDE

Sa starijom verzijom KDEmod-a [-legacy] koji se instalira u /opt/kde/bin, aplikacije neće biti automatski prepoznante od strane LXDE. I da bi koristili njegove aplikacije potrebno je dodat sledeću komandu:

```
echo 'PATH=$PATH:/opt/kde/bin' >> /etc/rc.local

```

ili možete dodat sledeću skriptu u /etc/profile.d:

```
#!/bin/sh
PATH=$PATH:/opt/kde/bin

```

Snimite kao "kde3path.sh" i napravite da je executable:

```
chmod +x /etc/profile.d/kde3path.sh

```

## Korisni LxDE linkovi

*   [LXDE wiki entry related to Arch Linux](http://wiki.lxde.org/en/ArchLinux)
*   [LXDE Project](http://lxde.sourceforge.net)
*   [LXDE Forum](http://forum.lxde.org)
*   [The Latest LX... Packages](https://sourceforge.net/project/showfiles.php?group_id=180858)
*   [PCMan File Manager](https://sourceforge.net/project/showfiles.php?group_id=156956)