Openbox je lagan i visokokonfigurabilan prozor menadžer sa širokom podrškom za standarde. Njegove mogućnosti su dobro dokumentovane na [oficijalnom web sajtu](http://openbox.org/). Ovaj članak će biti u vezi sa pokretanjem Openbox-a pod Arč Linuksom.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacija](#Instalacija)
*   [2 Samostalni menadžeri prozora](#Samostalni_menadžeri_prozora)
*   [3 Prozor menadžer za desktop okruženja](#Prozor_menadžer_za_desktop_okruženja)
    *   [3.1 GNOM](#GNOM)
        *   [3.1.1 GNOM 2.26](#GNOM_2.26)
        *   [3.1.2 GNOM 2.24](#GNOM_2.24)
        *   [3.1.3 GNOM 2.22 i prethodni](#GNOM_2.22_i_prethodni)
    *   [3.2 KDE](#KDE)
    *   [3.3 Xfce4](#Xfce4)
*   [4 Podešavanja](#Podešavanja)
    *   [4.1 Ručno podešavanje](#Ručno_podešavanje)
    *   [4.2 ObConf](#ObConf)
    *   [4.3 Podešavanje aplikacije](#Podešavanje_aplikacije)
*   [5 Meniji](#Meniji)
    *   [5.1 Ručno konfigurisanje](#Ručno_konfigurisanje)
    *   [5.2 MenuMaker](#MenuMaker)
    *   [5.3 Obmenu](#Obmenu)
        *   [5.3.1 Obm-xdg](#Obm-xdg)
    *   [5.4 Python bazirani xdg meni skripta](#Python_bazirani_xdg_meni_skripta)
    *   [5.5 OpenBox meni generator](#OpenBox_meni_generator)
    *   [5.6 Pipe meniji](#Pipe_meniji)
*   [6 Programi koji se pokreću prilikom startovanja](#Programi_koji_se_pokreću_prilikom_startovanja)
*   [7 Teme i izgled](#Teme_i_izgled)
    *   [7.1 Openbox teme](#Openbox_teme)
    *   [7.2 X11 izgled](#X11_izgled)
    *   [7.3 X11 miš kursori](#X11_miš_kursori)
    *   [7.4 GTK teme](#GTK_teme)
        *   [7.4.1 GTK2/GTK+](#GTK2/GTK+)
        *   [7.4.2 GTK1](#GTK1)
        *   [7.4.3 GTK fontovi](#GTK_fontovi)
        *   [7.4.4 GTK Ikone](#GTK_Ikone)
    *   [7.5 Desktop icons](#Desktop_icons)
    *   [7.6 Desktop pozadina (wallpaper)](#Desktop_pozadina_(wallpaper))
*   [8 Programi sa preporukom za korištenje](#Programi_sa_preporukom_za_korištenje)
    *   [8.1 Menadžeri za prijavu](#Menadžeri_za_prijavu)
    *   [8.2 Composite desktop](#Composite_desktop)
    *   [8.3 Panels, trays, and pagers](#Panels,_trays,_and_pagers)
        *   [8.3.1 Paneli](#Paneli)
        *   [8.3.2 Trays (sistem tray ikone)](#Trays_(sistem_tray_ikone))
        *   [8.3.3 Pagers](#Pagers)
    *   [8.4 Menadžeri fajlova](#Menadžeri_fajlova)
    *   [8.5 Starteri aplikacija](#Starteri_aplikacija)
        *   [8.5.1 dmenu](#dmenu)
        *   [8.5.2 Gmrun](#Gmrun)
        *   [8.5.3 Bashrun](#Bashrun)
        *   [8.5.4 Launchy](#Launchy)
        *   [8.5.5 LXPanel](#LXPanel)
        *   [8.5.6 gnome-panel](#gnome-panel)
    *   [8.6 Clipboard menadžer (menadžer ostave)](#Clipboard_menadžer_(menadžer_ostave))
    *   [8.7 Menadžeri za kontrolu zvuka](#Menadžeri_za_kontrolu_zvuka)
        *   [8.7.1 gvolwheel](#gvolwheel)
        *   [8.7.2 gvtray](#gvtray)
        *   [8.7.3 obmixer](#obmixer)
        *   [8.7.4 volti](#volti)
        *   [8.7.5 volumeicon](#volumeicon)
        *   [8.7.6 volwheel](#volwheel)
    *   [8.8 Menjači jezika na tastaturama](#Menjači_jezika_na_tastaturama)
        *   [8.8.1 fbxkb](#fbxkb)
        *   [8.8.2 xxkb](#xxkb)
        *   [8.8.3 axkb](#axkb)
        *   [8.8.4 xneur](#xneur)
*   [9 Saveti i trikovi](#Saveti_i_trikovi)
    *   [9.1 File associations](#File_associations)
    *   [9.2 Kopiranje i nalepljivanje](#Kopiranje_i_nalepljivanje)
    *   [9.3 Providnost](#Providnost)
    *   [9.4 Xprop values for applications](#Xprop_values_for_applications)
        *   [9.4.1 Xprop za Firefox](#Xprop_za_Firefox)
    *   [9.5 Linkovanje menia u komandu](#Linkovanje_menia_u_komandu)
    *   [9.6 Urxvt kao pozadina](#Urxvt_kao_pozadina)
    *   [9.7 Kontrola zvuka preko tastature](#Kontrola_zvuka_preko_tastature)
*   [10 Korisni Openbox linkovi](#Korisni_Openbox_linkovi)

## Instalacija

Openbox je dostupan iz standardnih repozitorijuma:

```
# pacman -S openbox

```

Kada je instaliran, pacman će Vas uputiti da kopirate default `menu.xml` i `rc.xml` konfiguracione fajlove u `~/.config/openbox`, na primer:

**Note:** Uradite ovo kao regularni korisnik, ne kao root.

```
$ mkdir -p ~/.config/openbox
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox
$ cp /etc/xdg/openbox/autostart.sh ~/.config/openbox

```

`rc.xml` je glavni konfiguracioni fajl za Openbox. Koristi se za upravljanje prečicama za tastaturu, temama, virtualnim desktopima i ostalim mogućnostima.

`menu.xml` kontroliše meni za aplikacije u Openbox-u koji se pojavljuje kada kliknete na Vaš desktop. Fabričke stavke su vrlo oskudne, ali veoma je lako modifikovati strukturu menija kako bi pasovao Vašim potrebama. Pogledajte meni sekciju ispod za više detalja, ili posetite [Openbox web sajt](http://icculus.org/openbox/).

`autostart.sh` Fabriči autostart fajl podešava veliki broj stvari za Vas. Možete upotrebiti ovu skriptu za pokretanje panela, da podesite desktop pozadinu, ili bilo šta drugo. Posetite [Openbox Wiki web sajt](http://openbox.org/wiki/Help:Autostart).

## Samostalni menadžeri prozora

Da pokrenete Openbox kao samostalan, jednostavno dodajte sledeće na dno `~/.xinitrc`:

```
exec openbox-session

```

Ako ste pre koristili drugi prozor menadžer, poput Xfwm-a, i Openbox neće da startuje nakon odjavljivanja iz X-a, pokušajte da pomerite autostart folder:

```
mv ~/.config/autostart ~/.config/autostart-bak

```

**Note:** [pyxdg](https://www.archlinux.org/packages/?name=pyxdg) je neophodan za Openbox xdg-autostart

## Prozor menadžer za desktop okruženja

### GNOM

#### GNOM 2.26

***Pratite sledeće uputstvo za GNOM 2.24\. Ako ne uspe probajte ovo:***

Ako, nakon što ste instalirali Openbox i probali da se ulogujete u 'Gnom/openbox' sesiju session, niste doživeli uspeh, možete uraditi sledeće kao jedan od načina za dostizanje situacije u kojoj će Vam Openbox raditi kao Vaš prozor menadžer svaki put kada se ulogujete u 'Gnom' sesiju iz Vašeg menadžera za prijavljivanje (xdm, gdm, kdm, entrance, slim, itd.)

1.  Prijavite se na Vašu Gnom sesiju (koja će i dalje koristiti metacity kao prozor menadžer) ako niste već.
2.  Instalirajte openbox ako niste to već uradili
3.  Istražite Vaše menije u *System → Preferences → Startup Applications* (verovatno pod imenom 'Session' za starije verzije Gnoma)
4.  Otvorite Startup Application, selektujte '+ Add' i dodajte tekst koji vidite u box-u ispod izuzimajući tekst ispod #.
5.  Sada pritisnite 'Add' dugme za taj prozor za unos podataka i uverite se da je boks za čekiranje ispod Vašeg novog unosa upaljen.
6.  Thus log out of your gnome session and log back in and you should be running openbox as your window manager.
7.  Uživajte!

```
Name:    Openbox Windox Manager          # Može biti promenjen
Command: openbox --replace               # Tekst ne bi trebalo uklanjati sa ove linije
Comment: Replaces metacity with openbox  # Može biti promenjeno

```

Ovo kreira unos u listi za startovanje koji se izvršava od strane Gnoma svaki put kada je gnome-session od određenog korisnika pokrenut.

#### GNOM 2.24

Prvo, kreirajte `/usr/share/applications/openbox.desktop` koji sadrži sledeće:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=OpenBox
Exec=openbox
NoDisplay=true
# ime učitavajućeg modula za kontrolni centar
X-GNOME-WMSettingsModule=openbox
# ime koje stavljamo na prozor za proveru specifikacije od prozor menadžera
X-GNOME-WMName=OpenBox

```

Zatim, u gconf-u, podesite `/desktop/gnome/session/required_components/windowmanager` u `openbox`:

```
$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox

```

Konačno, izaberite **GNOM** sesiju u GDM meniju za sesije.

#### GNOM 2.22 i prethodni

1.  Ako koristite GDM, izaberite "GNOME/Openbox" opciju za prijavljivanje
2.  Ako koristite `startx`, dodajte `exec openbox-gnome-session` u `~/.xinitrc`
3.  Iz terminala:

```
$ xinit /usr/bin/openbox-gnome-session

```

### KDE

1.  Ako koristite KDM, izaberite "KDE/Openbox" opciju za prijavljivanje
2.  Ako koristite startx, dodajte `exec openbox-kde-session` u `~/.xinitrc`
3.  Iz terminala:

```
$ xinit /usr/bin/openbox-kde-session

```

### Xfce4

Prijavite se u normalnu Xfce4 sesiju. Iz Vašeg terminala izbora uradite sledeće:

```
$ killall xfwm4 ; openbox & exit

```

Ovo će ubiti xfwm4, pokrenuti Openbox i zatvoriti terminal.

Odjavite se, ali uvereni da ste upalili "Save session for future logins" boks za čekiranje. Prilikom sledećeg prijavljivanja, Xfce4 će koristiti Openbox kao svoj prozor menadžer. Da bi ste bili u mogućnosti da izađete iz sesije koristeći xfce4-session, otvorite Vaš fajl `~/.config/openbox/menu.xml` (ako nije tu, kopirajte ga iz `/etc/xdg/openbox/menu.xml`).

Pronađite unos:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

i promenite ga u:

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

U suprotnom, koristeći "Exit" unos od root menija će uzrokovati da Openbox poništi svoje pokretanje, ostavljajući Vas bez prozor menadžera.

Ako imate problema prilikom prelaska između virtualnih desktop-a sa točkićem na mišu koji preskače preko virtualnih desktopa, otvorite Vaš `~/.config/openbox/rc.xml` fajl i pomerite bindove miša sa akcijama "DesktopPrevious" i "DesktopNext" sa konteksta "Desktop" na kontekst "Root" (možda ćete morati da definišete Root kontekst).

Ako želite da koristite Openbox root meni umesto Xfce-ov, možete da ugasite Xfcedesktop pokretanjem sledeće komande iz terminala:

```
$ xfdesktop --quit

```

Kako god, Xfcedesktop upravlja slikom u pozadini i desktop ikonama i zahteva korišćenje drugih alata, poput ROX-a, za ove funkcije.

(Kada poništavate Xfdesktop, gornji problem sa virtualnim radnim površinama više nije problem.)

## Podešavanja

Trenutno postoje dve opcije za podešavanje srži Openbox parametara; ručno uređivanje `rc.xml`, ili korišćenje ObConf alata.

### Ručno podešavanje

Da bi ste podesili Openbox ručno, jednostavno uredite `~/.config/openbox/rc.xml` sa Vašim omiljenim tekst editorom. Fajl za podešavanje pruža dosta komentara i [potpuna dokumentacija](http://openbox.org/wiki/Configuration) je dostupna na oficijalnom sajtu.

### ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) je grafički baziran, Openbox alat za podešavanje koji se može koristiti za podešavanje najvećeg dela opcija uključujući teme, virtualne radne površine, osobine prozora i margine radnih površina.

Da bi ste instalirali ObConf pokrenite:

```
# pacman -S obconf

```

**Note:** ObConf ne može biti korišćen za podešavanje prečica za tastaturu i nekih drugih naprednih mogućnosti. Za ove modifikacije morate urediti `rc.xml` ručno (pogledajte gore). Druga opcija je [ObKey](http://code.google.com/p/obkey/) aplikacija (dostupna u [AUR](/index.php/AUR "AUR")).

### Podešavanje aplikacije

Openbox karakteriše podešavanje po aplikaciji, dozvoljavajući Vam da definišete pravila za Vaše programe. Na primer, Vi možete:

*   učitati Vaš web pretraživač na odrešenoj radnoj površini
*   učitati Vaš terminal bez graničnika za prozor
*   učitati Vaš torent klijent pozicioniran na odrešenom mestu na ekranu

Ovi su definisani u `~/.config/openbox/rc.xml`. Kao što možete da očekujete, instrukcije su dobro dokumentovane u okviru samog fajla. Puni detalji takođe mogu biti nađeni ovde: [http://openbox.org/wiki/Help:Applications](http://openbox.org/wiki/Help:Applications)

## Meniji

"Fabrički" Openbox meni sadrži raznolike aplikacije kako bi Vam omogućile da startujete, ali Vi ćete verovatno želeti da prilagodite ove u nekom trenutku. Postoji veći broj načina da to uradite:

### Ručno konfigurisanje

Slično kao `rc.xml` fajl, možete urediti `~/.config/openbox/menu.xml` sa Vašim omiljenim tekst editorom. Mada su mnoga od ovih podešavanja samo-objašnjena, [potpuna dokumentacija](http://openbox.org/wiki/Help:Menus) je dostupna.

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) je moćna alatka koja kreira XML-bazirane menije za razne menadžere prozora, uključujući Openbox. MenuMaker će pretražiti Vaš računar za izvršne programe i kreirati XML meni zasnovan na rezultatima. Može biti konfigurisan da izostavi Legacy X, GNOM, KDE, ili Xfce aplikacije ako korisnik poželi.

MenuMaker je dostupan u community repozitorijumu:

```
# pacman -S menumaker

```

Kad je instaliran, možete da generišete kompletan meni izvršavanjem:

```
$ mmaker -v OpenBox3

```

Prema "fabričkim podešavanjima", MenuMaker neće prepisati već postojeći menu.xml. Da bi ste to uradili, pokrenite ga sa -f (force) argumentom:

```
$ mmaker -vf OpenBox3

```

Da vidite celu listu opcija, pokrenite `mmaker --help`.

Ovo će Vam dati prilično temeljan meni. Sada možete da izmenite menu.xml ručno, ili jednostavno ponovo generišite listu kad god instalirate nov softver.

### Obmenu

Obmenu je meni editor za Openbox baziran na grafičkom korisničkom interfejsu. Za one koji ne uživaju u editovanju XML izvornog koda, ovo je verovatno najbolja opcija za Vas.

Dostupan je u repozitorijumu community:

```
# pacman -S obmenu

```

Kada je instaliran, jednostavno pokrenite `obmenu` i dodajte ili uklonite željenu aplikaciju.

#### Obm-xdg

<tt>obm-xdg</tt> je alat koji se koristi u komandnoj liniji koji dolazi sa Obmenu-jem. Može da generiše kategorizovane podmenije instaliranih GTK/GNOM aplikacija.

Da koristite obm-xdg, dodajte sledeće linije u `~/.config/openbox/menu.xml`:

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

Zatim izvršite `openbox --reconfigure` da osvežite Openbox meni. Sada bi trebali da vidite podmeni sa oznakom **xdg** u Vašem meniju.

**Note:** If you do not have GNOME installed, then you need to install **gnome-menus** package for obm-xdg to work.

### Python bazirani xdg meni skripta

Ova skripta se može naći u Fedorinom Openbox paketu. Sve što ćete morati da uradite je da stavite skriptu negde i da dodate stavku u meniju.

Evo ga moj "nalepi": [http://pastebin.com/f2f827625](http://pastebin.com/f2f827625) I evo je glava: [http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup](http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup)

Skinite onu koja Vam se sviđa (možda ćete Više voleti glava verziju). Možete staviti fajl bilo gde. Ja sam koristio ~/Documents/build/xdg-menu (samo modifikujte meni unos kasnije u skladu sa Vašom adresom fajla).

Zatim otvorite Vaš menu.xml sa Vašim omiljenim tekst editorom i dodajte sledeće stavke tamo gde želite novi meni (naravno, možete da modifikujete obeležja kako god želite):

```
<menu id="apps-menu" label="xdgmenu" execute="python /home/shiki/Documents/build/xdg-menu"/>

```

Sačuvajte fajl i izvršite: `openbox --reconfigure`.

### OpenBox meni generator

OpenBox meni generator, dostupan u AUR-u kao [obmenugen-bin](https://aur.archlinux.org/packages.php?ID=27300) je meni generator za OpenBox koji koristi *.desktop fajlove. Obezbeđuje tekstualni fajl za filtriranje, koristeći osnovni regex koji utvrđuje koje su meni stavke skrivene. Da upotrebite, jednostavno pokrenite:

```
$ obmenugen

```

Zatim osvežite OpenBox sa:

```
$ openbox --reconfigure

```

### Pipe meniji

Openbox (i drugi prozor menadžeri poput WindowMaker-a i PekWM-a) Vam pružaju da napišete skripte koji dinamički grade menije u hodu. Neki primeri su sistem posmatrači, kontrole za medija plejere i vremenske prognoze. Mnogi primeri se mogu naći u openbox [sajtu](http://openbox.org/wiki/Openbox:Pipemenus).

Xyne je takođe kreirao fajl pretraživač i brisbin33 ima jedan za skeniranje / konektujući dva bežična "hot spot"-a (zahteva netcfg). Relevantni postovi na forumu za ove alate su [ovde](https://bbs.archlinux.org/viewtopic.php?id=77197&p=1) i [ovde](https://bbs.archlinux.org/viewtopic.php?id=78290)

## Programi koji se pokreću prilikom startovanja

Openbox karakteriše podrška za pokretanje programa prilikom startovanja. Ovo je obezbeđeno sa "openbox-session" komandom.

Postoje načini da omogućite automatsko startovanje:

1.  Ako koristite start/xinit da se ulogujete u X sesiju, izmenite `~/.xinitrc` i promenite liniju koja izvršava *openbox* da izvršava **openbox-session** umesto.
2.  Ako se prijavite sa GDM/KDM-om, selektujte *Openbox* sesiju i oni će automatski koristiti automatsko startovanje.

Programi koji se pokreću prilikom startovanja su upravljani u `~/.config/openbox/autostart.sh`. Potpune instrukcije i najbolje prakse vezane za ovo su dostupne na [Openbox web sajt za programe koji automatski startuju](http://openbox.org/wiki/Help:).

## Teme i izgled

Sa izuzetkom Openbox tema, ova sekcija je namenjena za korisnike koji su podesili Openbox za pokretanje na samostalnom desktopu bez pomoći GNOMA, KDEa ili Xfcea.

### Openbox teme

Openbox teme kontrolišu izgled okvira prozora, uključujući naslovnu liniju i dugmiće na naslovnoj liniji. Takođe određuju izgled menija za aplikacije i on-screen displeja (OSD).

Dodatne teme su dostupne iz standardnih repozitorijuma:

```
# pacman -S openbox-themes

```

Ovaj paket ni u kom slučaju nije konačan. Možete preuzeti više tema na web sajtovima poput:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

Preuzete teme bi trebale biti izdvojene u <tt>~/.themes</tt> i mogu biti instalirane ili selektovane sa ObConf alatom.

Kreiranje novih tema je prilično lako i opet [dokumentovane teme](http://openbox.org/wiki/Help:Dobro).

Za editor tema sa grafičkim korisničkim interfejsom, pogledajte na [ObTheme](http://xyne.archlinux.ca/info/obtheme).

### X11 izgled

Ako izvršavate Openbox kao samostalan, moraćete da podesite .Xdefaults fajl. Sačuvajte kopiju u ~/.Xdefaults i /home/root/.Xdefaults za prozore otvorene kao root.

Xdefaults je konfiguracioni tačkafajl na korisničkom nivou, tipično lociran u ~/.Xdefaults. Kad je prisutan, analiziran je od strane xrdb (Xorg baza za resurse) programa koji to radi automatski kada se Xorg startuje i može biti upotrebljen za podešavanje ili predupređivanje osobina za X i X aplikacije. Može uraditi mnogo operacija, uključujući:

```
- definisati boje u terminalu
- podešavati osobine terminala
- podešavati broj tačaka po inču, umekšavanje stepena, nagoveštavanje i ostala podešavanja za X font.
- izmena teme X kursora
- promena teme za xscreensaver
- izmena osobina kod X aplikacija na niskom nivou (xclock, xpdf, itd.) 

```

Xdefaults Arch WiKi [Xdefaults](/index.php/Xdefaults "Xdefaults")

### X11 miš kursori

Izdvojite željene Xcursor teme u <tt>/usr/share/icons</tt> (pristup ima ceo sistem) ili <tt>~/.icons</tt> (pristup na nivou korisnika). Takođe postoje ograničene količine tema dostupnih u community repozitorijumu koje mogu biti instalirane upotrebom pakmena.

Dodajte ovo u `~/.Xdefaults`:

```
Xcursor.theme:   [ime-teme-za-kursor]

```

gde `[ime-teme-za-kursor]` je ime direktorijuma od kursor teme. Na primer:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

Da promenite veličinu:

```
Xcursor.size: [veličina]

```

Ponekad je neophodno da simbolički linkujete direktorijum ikone na svaki korisnički direktorijum da bi ste omogućili prozor menadžeru da ih koristi:

```
$ mkdir ~/.icons
$ ln -s /usr/share/icons/[ime-teme-za-kursor] ~/.icons/default

```

Za više informacija pročitajte Arč Wiki [X11 Cursors](/index.php/X11_Cursors "X11 Cursors")

### GTK teme

#### GTK2/GTK+

Prvo, izdvojite željene teme u <tt>/usr/share/themes</tt> (pristup ima ceo sistem) ili <tt>~/.themes</tt> (pristup na nivou korisnika), zatim:

GTK+ teme mogu biti upravljane lako sa **[lxappearance](/index.php/LXDE "LXDE")**, **gtk-chtheme**, ili **switch2** alatima. Da instalirate, izvršite:

```
# pacman -S lxappearance

```

i/ili

```
# pacman -S gtk-chtheme

```

i/ili

```
# pacman -S gtk-theme-switch2

```

Sada možete jednostavno da pokrenete `lxappearance`, `gtk-chtheme` ili `switch2` da podesite željenu temu.

#### GTK1

Za GTK1 teme iz zaostavštine, instalirajte **gtk-theme-switch** paket:

```
# pacman -S gtk-theme-switch

```

Zatim pokrenite `switch` da izaberete željenu temu.

#### GTK fontovi

Da ručno promenite tip i veličinu Vaših fontova, dodajte sledeće u `~/.gtkrc.mine`:

```
style "user-font"
{
font_name = "[font-name] [size]"
}
widget_class "*" style "user-font"
gtk-font-name = "[font-name] [size]"

```

gde `[font-name] [veličina]` je poželjna veličina fonta i tačke. Na primer:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Oba `font_name` i `gtk-font-name` polja su neophodna za kompatibilnost u nazad.

Takođe možete da upotrebite **gtk-chtheme** ili **lxappearance** da podesite GTK font podešavanja. Molim Vas uputite se na gornju sekciju.

#### GTK Ikone

Prvo otpakujte željenu temu sa ikonicama u <tt>/usr/share/icons</tt> (dostupno za ceo sistem) ili <tt>~/.icons</tt> (dostupno samo određenom korisniku), zatim:

Dodati sledeće u `~/.gtkrc.mine`:

```
gtk-icon-theme-name = "[ime-teme-od-ikona]"

```

gde je `[ime-teme-od-ikona]` ime direktorijuma od teme za ikone. Naprimer:

```
gtk-icon-theme-name = "Tango"

```

Osigurajte da je `~/.gtkrc-2.0` konfigurisan u `~/.gtkrc.mine`:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

Možete da koristite i mnogo lakši način sa **lxappearance** da izaberete GTK temu za ikone. Takođe možete da koristite i [lxappearance2-git](https://aur.archlinux.org/packages.php?ID=39339) iz AUR-a da menjate Kursor miša, GTK Teme, Teme Ikone i Šemu boja. Takođe možete da instalirate i ovaj dodatak [lxappearance-obconf-git](https://aur.archlinux.org/packages/lxappearance-obconf-git/)sa njim možete da menjate dekoracione prozore u Openboxu iz lxappearance.

### Desktop icons

Openbox does not provide a means to display icons on the desktop. Xfdesktop, PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](http://idesk.sourceforge.net), or even Nautilus (and the gnome-settings-daemon) can provide this function.

ROX and PCmanFM have the additional advantage of being lightweight file managers.

### Desktop pozadina (wallpaper)

Openbox sam po sebi ne nudi način za menjanje wallpapera. Ovo je moguće uz aplikacije kao što su [Feh](/index.php/Feh "Feh") ili [Nitrogen](/index.php/Nitrogen "Nitrogen"). Druge opcije uključuju ImageMagick, hsetroot i xsetbg. Ili Pcmanfm i Xfdesktop mogu da urade.

Možete da onemogućite wallpaper učitavanje iz gnome-settings-daemon ovako:

```
$ gconftool-2 --set /apps/gnome_settings_daemon/plugins/background/active --type bool False

```

Takođe iz AUR-a možete da instalirate i [pybgsetter](https://aur.archlinux.org/packages/pybgsetter/) menadžer za menjanje wallpapera.

## Programi sa preporukom za korištenje

[Lista laganog softvera](/index.php/Lightweight_Applications "Lightweight Applications") na Arch wiki strani; većina programa se lepo uklapa u Openbox okruženje.

### Menadžeri za prijavu

[LXDM](http://wiki.lxde.org/en/LXDM) Veoma lagan menadžer za prijavu, koji poseduje grafičko biranje sesija i mogućnost resetovanja i gašenja računara, najbolje rešenje za lake sistemska okruženje a isto i za zahtevnija.

[SLiM](http://slim.berlios.de/) Pruža elegantno lagano rešenje za openbox. Pregledati [SLiM](/index.php/SLiM "SLiM") wiki stranicu za detaljnije uputstvo.

[Qingy](http://qingy.sourceforge.net/) je ultra lako podesivo grafički prijavnik. Podržava prijavu iz konzole i iz X sesije. on koristi [DirectFB](http://www.directfb.org), Pregledadit upustvo na Arch wiki stranici za [Qingy](/index.php/Qingy "Qingy") menadžer za prijavu.

### Composite desktop

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") is a lightweight composite manager capable of rendering drop shadows, fading and simple window transparency within Openbox and other window managers. (It's worth noting that xcompmgr is no longer developed, and so any issues are unlikely to be fixed) (Developed an issue with tint2 0.9, the systray icons have a tendency to corrupt)

### Panels, trays, and pagers

There are quite a lot of utilities available that provide a panel (taskbar), system tray, and pager to Openbox. The most common are:

#### Paneli

*   [PyPanel](/index.php/PyPanel "PyPanel")
*   [BMPanel](http://nsf.110mb.com/bmpanel/)
*   [tint2](/index.php/Tint2 "Tint2")
*   [LXPanel](http://www.gnomefiles.org/app.php/LXPanel)
*   [fbpanel](http://fbpanel.sourceforge.net)
*   [PerlPanel](http://freshmeat.net/projects/perlpanel/)
*   [fspanel](http://www.chatjunkies.org/fspanel/)
*   [Xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)
*   [GnomePanel](http://live.gnome.org/GnomePanel/)
*   [avant-window-navigator](https://launchpad.net/awn)
*   [cairo-dock](http://developer.berlios.de/projects/cairo-dock/)
*   [wbar](http://code.google.com/p/wbar/)
*   [screenlets](http://www.screenlets.org/)
*   [pancake](http://www.failedprojects.de/pancake/)

#### Trays (sistem tray ikone)

*   [Stalonetray](http://stalonetray.sourceforge.net/)
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

#### Pagers

*   [Visibility](http://projects.l3ib.org/trac/visibility)
*   [bbpager](http://bbtools.sourceforge.net/)
*   [netwmpager](https://aur.archlinux.org/packages.php?ID=17563)
*   [IPager](http://useperl.ru/ipager/index.en.html)
*   [neap](http://code.google.com/p/neap/)

Make your choice and add it to your startup file. If you wish to set the desktop layout without using a pager, you can use [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/), which is a packaged version of the setlayout tool from the Openbox wiki.

### Menadžeri fajlova

Postoji mnogo fajl menadžera, ali najpopularniji lagani fajl menadžeri su:

*   [Thunar](/index.php/Thunar "Thunar"). Thunar podržava auto-mount i još poseduje dodatne priključke.
*   [ROX](http://rox.sourceforge.net) (ROX ima mogućnost dodavanja desktop ikona)

```
# pacman -S rox

```

*   [PCManFM](http://pcmanfm.sourceforge.net) (pcmanfm takođe ima podršku za desktop ikone)

```
# pacman -S pcmanfm

```

Da pristupite NTFS particijama sa PCManFM, instalirajte ntfs-3g:

```
# pacman -S ntfs-3g

```

i dodajte svoj username u hal grupu:

```
# gpasswd -a username hal

```

Za još laganije fajl menadžere pogledajte [Gentoo](http://www.obsession.se/gentoo/) ili [emelFM2](http://emelfm2.net/), oba koriste sličan 'Midnight Commander' podeljeni panel preglednik.

Drugi: Xfe muCommander qtfm

Naravno mogu se instalirati i GNOME's Nautilus. Iako sporiji od gore navedenih ima svoje prednosti kao VFS podrška (kao daljinska SSH, FTP i Samba konekcije)

### Starteri aplikacija

#### dmenu

Set-up dmenu as described in the [dmenu](/index.php/Dmenu "Dmenu") wiki article. Then, add the following entry to the <keyboard> section `~/.config/openbox/rc.xml` to enable a shortcut to launch dmenu:

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### [Gmrun](/index.php/Gmrun "Gmrun")

[gmrun](http://sourceforge.net/projects/gmrun) je odličan starter koji se pokreće sa Alt+F2 kao kod KDE ili gnome okruženja:

```
# pacman -S gmrun

```

Za detalje pročitati wiki artikl [ovde](/index.php/Gmrun "Gmrun"). Dodati sledeđe u <keyboard> section `~/.config/openbox/rc.xml` da se omogući Alt+F2 funkcija:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

#### Bashrun

[bashrun](http://bashrun.sourceforge.net) provides a different, barebones approach to a run dialog, using a specialized bash session within a small xterm window. It is available in the community repository and can be launched through the Alt+F2 style approach mentioned previously. To make bashrun act more like a traditional run dialog, add the following entry to the <applications> section `~/.config/openbox/rc.xml`:

```
   <application name="bashrun">
     <desktop>all</desktop>
     <decor>no</decor>  # switch to yes if you prefer a bordered window
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

#### Launchy

[Launchy](http://www.launchy.net/) ima manje minimalistički pristup; on nudi skinove i ima opcije kao što je kalkulartor, proveravanje vremenske prognoze...

```
# pacman -S launchy

```

On se pokreće sa Ctrl+Space kombinacijom tastera.

#### LXPanel

LXPanel se može pokrenuti sa ovom komandom:

```
lxpanelctl run

```

#### gnome-panel

Gnome-panel starter se pokreće sa ovom komandom:

```
gnome-panel-control --run-dialog

```

### Clipboard menadžer (menadžer ostave)

Ako želite menadžer ostave sa copy/paste mogućnostima. **xfce4-clipman-plugin, parcellite,** ili **glipper-old** mogu se instalirati preko pacman-a. Svoj izbor stavite u autostart.sh da se podiže sa sistemom.

### Menadžeri za kontrolu zvuka

#### gvolwheel

lagani audio mixer koji vam dozvoljava da iz tray ikone menjate jačinu zvuka [[1]](https://aur.archlinux.org/packages.php?ID=25502)

#### gvtray

Još jedan audio menadžer koji dozvoljava iz tray ikone menjanje zvuka [[2]](https://aur.archlinux.org/packages.php?ID=6362)

#### obmixer

Obmixer je mixer pisan u C jeziku sa namernom da bude lagana alternativa gnome mixeru [[3]](https://aur.archlinux.org/packages.php?ID=31131)

#### volti

GTK+ aplikacija za kontrolu zvuka iz sistem tray ikone /notification area [[4]](https://aur.archlinux.org/packages.php?ID=33525)

#### volumeicon

Još jedan audio menadžer koji dozvoljava iz tray ikone menjanje zvuka[[5]](https://aur.archlinux.org/packages.php?ID=35793)

#### volwheel

Tray ikona za podešavanje zvuka, preko srednjeg dugmeta na mišu [volwheel](https://aur.archlinux.org/packages/volwheel/)

### Menjači jezika na tastaturama

#### fbxkb

Indikator za tastaturu i menjač jezika na tastaturi [[6]](https://aur.archlinux.org/packages.php?ID=3458)

#### xxkb

Indikator za tastaturu i menjač jezika na tastaturi [xxkb](https://www.archlinux.org/packages/?name=xxkb)

#### axkb

QT4 menjač jezika na tastaturi [[7]](https://aur.archlinux.org/packages.php?ID=25555)

#### xneur

X Neural Menjač je tekst analizator, detektuje jezik [[8]](https://aur.archlinux.org/packages.php?ID=9750)

## Saveti i trikovi

### File associations

Since Openbox and the applications you are going to use with it are not very well integrated you might run into the issue that your browser does not know which programm it is supposed to use for certain types of files. The package in the AUR [gnome-defaults-list](https://aur.archlinux.org/packages.php?ID=23170) contains a list of file-types and programms specific to the gnome desktop. It will be installed to

```
/etc/gnome/defaults.list

```

Open it with your text-editor and now you can search&replace everything with your appropriate programms. Like totem<=>vlc or eog<=>mirage. Save the file to:

```
~/.local/share/applications/defaults.list

```

Another way is to use the package *perl-file-mimeinfo* from the repositories, and invoke the mimeopen command like this:

```
mimeopen -d /path/to/file

```

You will then be asked what application to use when opening /path/to/file:

```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

Your answer will be set as the default handler for that type of file.

### Kopiranje i nalepljivanje

Iz terminala, Ctrl+Insert za kopiranje i Shift+Insert za nalepljivanje. Može se kopirat iz terminala i sa Ctrl+Shift+C, a zalepiti sa srednjim klikom miša.

### Providnost

Korišćenjem programa transset-df, isto je kao i sa [transset](/index.php?title=Transset&action=edit&redlink=1 "Transset (page does not exist)"), (dostupan preko: pacman -S transset-df) možete omogućiti providnost prozora . Na primer tako što ćete izmeniti sledeće `~/.config/openbox/rc.xml` možete da omogućite/onemogućite providnost sa srednjim klikom miša tako što skrolujete gori ili dole, preko title bara (nalazi se u <mouse> sekciji):

```
    <context name="Titlebar">
     <mousebind button="Left" action="Press">
       <action name="Focus"/>
       <action name="Raise"/>
     </mousebind>
     <mousebind button="Left" action="Drag">
       <action name="Move"/>
     </mousebind>
     <mousebind button="Left" action="DoubleClick">
       <action name="ToggleMaximizeFull"/>
     </mousebind>
     <mousebind button="Middle" action="Press">
     	<action name="Lower"/> 
       <action name="FocusToBottom"/>
       <action name="Unfocus"/>
     </mousebind>
     <mousebind button="Up" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --inc  </execute>
       </action>
     </mousebind>
     <mousebind button="Down" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --dec </execute>
       </action>
     </mousebind>
     <mousebind button="Right" action="Press">
       <action name="Focus"/>
       <action name="Raise"/>
       <action name="ShowMenu">
         <menu>client-menu</menu>
       </action>
     </mousebind>
   </context>

```

Ovo radi samo kada druge akcije nisu preduzete

### Xprop values for applications

If you use per-application settings frequently, you might find this bash alias handy:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

To use, run **`xp`** and click on the running program that you'd like to define with per-app settings. The result will display only the info that Openbox requires, namely the WM_WINDOW_ROLE and WM_CLASS (name and class) values:

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Xprop za Firefox

For whatever reason, Firefox and its open source equivalents will ignore application rules (e.g. <desktop>) unless `class="Firefox*"` is used, regardless of what xprop reports as the actual WM_CLASS values.

### Linkovanje menia u komandu

Neki ljudi žele da povežu Openbox glavni menu, ili bilo koje druge, sa komandom. Ovo je korisnoј pri kreiranje dugmeta za menu u panelu, naprimer. Iako Openbox ne podržava ovo,postoji vrlo jednostavna skripte xdotool, koja simulira ovo sa pritiskom dugmeta. Xdotool se nalazi [u AUR-u](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd). Za korišćenje dodajte sledeći kod u <keyboard> sekciju vašeg `rc.xml`:

```
    <keybind key="A-C-q">
      <action name="ShowMenu">
        <menu>root-menu</menu>
      </action>
    </keybind>

```

Restart/reconfigure Openbox. You can now magically summon your menu at your cursor position by running the following command:

```
# xdotool key ctrl+alt+q

```

Naravno vi možete da stavljate komande koje vama odgovaraju.

### Urxvt kao pozadina

Sa Openboxom, pokretanje terminala kao desktop pozadina je lako. Neće vam trebati **devilspie** ovde.

Prvo treba da omogućite providnost, otvorite vaš `.Xdefaults` fajl (ako ne postoji kreirajte ga u vašem home folderu).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #I don't use the whole screen, if you want a full screen term don't bother with this and see below.
URxvt*borderLess:true
URxvt*foreground:Black   #Font color. My wallpaper is White, you may wish to change this to White.

```

Zatim izmenite vaš `.config/openbox/rc.xml` fajl:

```
<application name="URxvt">
  <decor>no</decor>
  <focus>yes</focus>
  <position>
    <x>center</x>
    <y>20</y>
  </position>
  <layer>below</layer>
  <desktop>all</desktop>
  <maximized>true</maximized> #Only if you want a full size terminal.
</application>

```

The *magic* comes from the `<layer>below</layer>` line, which place the application under all others. Here Urxvt is displayed on all desktops, change it to your convenience.

Note: Instead of using <application name="URxvt">, you can use another name ("URxvt-bg" for example), and use the -name option when starting uxrvt. That way, only the urxvt terminals which you choose to name URxvt-bg would be captured and modified by the application rule in rc.xml. For example: urxvt -name URxvt-bg (case sensitive)

### Kontrola zvuka preko tastature

Ako koristite ALSU za zvuk, možete da koristite amixer za zvuk. Može se koristiti Openbox's keybindings da budu kao multimedijani tasteri. (Alternativno, možete naći multimedijano ime tastera i mapirati ga ako posedujete tastaturu sa multimedijanim tasterima.) Naprimer, u <keyboard> sekciji kod rc.xml:

```
   <keybind key="W-Up">
     <action name="Execute">
       <command>amixer set Master 5%+</command>
     </action>
   </keybind>

```

kombinacija Windows tastera + Up strelice će pojačati zvuk sa ALSA volume za 5%. Isto tako primer za smanjive:

```
   <keybind key="W-Down">
     <action name="Execute">
       <command>amixer set Master 5%-</command>
     </action>
   </keybind>

```

Još jedan primer kako možete da koristite XF86Audio keybindings:

```
   <keybind key="XF86AudioRaiseVolume">
     <action name="Execute">
       <command>amixer set Master 5%+ unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioLowerVolume">
     <action name="Execute">
       <command>amixer set Master 5%- unmute</command>
     </action>
   </keybind>
   <keybind key="XF86AudioMute">
     <action name="Execute">
       <command>amixer set Master toggle</command>
     </action>
   </keybind>

```

Gornji primer bi trebao da radi sa multimedijalnim tastaturama. Trebalo bi da pojača smanji i ugasi zvuk.

## Korisni Openbox linkovi

*   [Openbox Website](http://openbox.org/) – Openbox zvanični sajt
*   [Planet Openbox](http://planetob.openmonkey.com/) – Openbox portal za vesti
*   [Box-Look.org](http://www.box-look.org/) – A good resource for themes and related artwork
*   [Openbox Hacks and Configs Thread](https://bbs.archlinux.org/viewtopic.php?id=93126) @ Arch Linux Forum
*   [Openbox Screenshots Thread](https://bbs.archlinux.org/viewtopic.php?id=45692) @ Arch Linux Forum