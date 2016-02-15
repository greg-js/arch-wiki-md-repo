## Contents

*   [1 Početak](#Po.C4.8Detak)
    *   [1.1 Kompletno uputstvo](#Kompletno_uputstvo)
    *   [1.2 Startovanje Fluxbox-a](#Startovanje_Fluxbox-a)
        *   [1.2.1 Metoda 1: KDM/GDM](#Metoda_1:_KDM.2FGDM)
        *   [1.2.2 Metod 2: ~/.xinitrc](#Metod_2:_.7E.2F.xinitrc)
*   [2 Podešavanje](#Pode.C5.A1avanje)
    *   [2.1 Upravljanje menijem](#Upravljanje_menijem)
        *   [2.1.1 Built-in metoda](#Built-in_metoda)
        *   [2.1.2 MenuMaker](#MenuMaker)
        *   [2.1.3 Arch Linux Xdg meni](#Arch_Linux_Xdg_meni)
        *   [2.1.4 Kreiranje prilagođenog menija sa fluxconf-om](#Kreiranje_prilago.C4.91enog_menija_sa_fluxconf-om)
        *   [2.1.5 Ručno kreirajte/editujte meni](#Ru.C4.8Dno_kreirajte.2Feditujte_meni)
    *   [2.2 Prečice](#Pre.C4.8Dice)
    *   [2.3 Radne površine](#Radne_povr.C5.A1ine)
    *   [2.4 Pozadina](#Pozadina)
        *   [2.4.1 Dodatne beleške za ljude koji vole da često menjaju pozadine](#Dodatne_bele.C5.A1ke_za_ljude_koji_vole_da_.C4.8Desto_menjaju_pozadine)
        *   [2.4.2 Feh](#Feh)
    *   [2.5 Teme](#Teme)
    *   [2.6 GTK2 Themes](#GTK2_Themes)
    *   [2.7 Automatsko startovanje aplikacija](#Automatsko_startovanje_aplikacija)
    *   [2.8 Život nakon xorg.conf-a](#.C5.BDivot_nakon_xorg.conf-a)
        *   [2.8.1 Podešavanje Vaše tastature na pravi način](#Pode.C5.A1avanje_Va.C5.A1e_tastature_na_pravi_na.C4.8Din)
        *   [2.8.2 Onemogući uštedu energije](#Onemogu.C4.87i_u.C5.A1tedu_energije)
*   [3 Dodatni izbori](#Dodatni_izbori)

# Početak

## Kompletno uputstvo

Hvala narada-i; on je autor ovog uputstva. Možete ga pronaći na: [[1]](https://bbs.archlinux.org/viewtopic.php?id=77729)

## Startovanje Fluxbox-a

### Metoda 1: KDM/GDM

Korisnici [KDM](/index.php/KDM "KDM") ili [GDM](/index.php/GDM "GDM") će naći novi fluxbox unos automatski dodat u njihov meni sesije.will find a new fluxbox entry added to their session menu automatically. Jednostavno izaberite fluxbox opciju kada se prijavljujete na sistem.

### Metod 2: ~/.xinitrc

Izmenite `~/.xinitrc` i dodajte sledeći kod:

```
exec fluxbox

```

ili ako bi ste želeli da koristite 'startfluxbox' fajl, dodajte ovu liniju umesto:

```
exec startfluxbox 

```

<tt>startfluxbox</tt> je metoda koja se preporučuje, jer ona će takođe izvršiti sve programe definisane u `~/.fluxbox/startup`.

Ako takođe koristite **polkit** i **D-Bus** (npr. za drajvere za automatsko nasađivanje), upotrebite ovaj kod umesto:

```
 exec startfluxbox

```

**Note:** Može biti samo jedna <tt>exec</tt> linija u Vašem `~/.xinitrc` fajlu.

Ako dođe do pada sistema prilikom startovanja, moguće je da je problem u lokalizaciji. Podešavanjem LC_ALL na početnu "C" lokalizaciju, možete izbeći ovaj problem. [1](https://bbs.archlinux.org/viewtopic.php?t=25797).

# Podešavanje

## Upravljanje menijem

### Built-in metoda

Built-in command:

```
$ fluxbox-generate_menu

```

Ova komanda će napraviti ~/.fluxbox/menu/ fajl baziran na Vašim instaliranim programima. Takođe postoji "helper / regenerate menu" u fluxbox meniju.

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) je moćna alatka za kreiranje XML-baziranih menija za razne menadžere prozora, uključujući i Fluxbox. MenuMaker će pretražiti Vaš kompjuter za izvršne programe i napraviti meni baziran na rezultatima. Može biti konfigurisan za izuzme Legacy X, GNOM, KDE, ili Xfce aplikacije ako tako želite.

MenuMaker je dostupan u [community] preko pakmena:

```
# pacman -S menumaker

```

Nakon što je instaliran, možete generisati kompletan meni izvršavanjem:

```
$ mmaker -v Fluxbox

```

Da vidite celu listu opticija, izvršite **mmaker --help**

### Arch Linux Xdg meni

Zahteva [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu)

```
$ xdg_menu --fullmenu --format fluxbox --root-menu /etc/xdg/menus/arch-applications.menu >~/.fluxbox/menu

```

**Savet:** zamenite početni xterm/urxvt:

```
$ sed -i 's/xterm/urxvt/g' ~/.fluxbox/menu

```

Više informacija:

```
$ xdg_menu --help

```

_Takođe pogledajte: [XdgMenu](/index.php/XdgMenu "XdgMenu")_

### Kreiranje prilagođenog menija sa fluxconf-om

Da startujete meni sekciju fluxconf-a izvršite:

```
$ fluxmenu

```

U prozoru ćete videti tri kolone: Type, Title, & Command/Comment.
Klikom na jedan od unosa će Vam dozvoliti da ga editujete.
Klikom na "Add sub" ćete dodati podmeni.
Klikom na "Add exec" ćete dodati komandu.

Kolona za tip ima nekoliko validnih opcija:

1.  begin, neophodna za startovanje meni fajla. Title opcija je meni zaglavlje.

2.  submenu, "folder" u okviru menija. Title je ime submenu-ja.

3.  exec, komandna linija. Title je ono što je prikazano i Command/Comment je komanda koja će biti izvršena.
4.  separator, razdvajač u meniju. Nema argumenata za njega.
5.  workspaces, lista radnih površina i koje aplikacije se izvršavaju na svakoj. Title je ono što će biti prikazano korisniku.
6.  stylesdir, direktorijum koji sadrži stilove. Title je staza ka direktorijumu. Preporučuje se da stavite ovo u svoj zasebni poddirektoirjum jer može postati prilično velik. Direktorijumi koji su pogodni: /usr/share/fluxbox/styles ~/.fluxbox/stylesRecommended that you put this into its own subdirectory as it can get quite large. directories to use: /usr/share/fluxbox/styles ~/.fluxbox/styles .
7.  config, meni sa mnogo opcija za konfigurisanje ponašanja fluxbox-a. Title je ime menija prikazanog korisniku.
8.  reconfig, ponovo učitava konfig fajl. Title je naslov prikazan korisniku.
9.  restart, restartuje fluxbox. Title je naslov prikazan korisniku.
10.  exit, izlazi iz fluxbox-a, iskočiće u upravljač desktop-a ili izaći iz X-a sve u zavisnosti od metode za startovanje koju ste upotrebili. Title je naslov prikazan korisniku.

Zapamtite da stisnete save pre zatvaranja

### Ručno kreirajte/editujte meni

Upotrebite komandu:

```
$ nano ~/.fluxbox/menu

```

Zatim napišite linije u ovom stilu:

```
[exec] (name) {command}

```

Ako želite da napravite podmeni napišite:

```
[submenu] (Name)
...
...
[end]

```

Kada ste završili sačuvajte i izađite. Nije neophodno da restartujete fluxbox.

## Prečice

Fluxbox pruža funkcionalnost osnovnih prečica. Fluxbox fajl sa prečicama se nalazi u:

```
~/.fluxbox/keys

```

Control je predstavljen sa "Control". Mod1 odgovara Alt-u i Mod4 odgovara Meta tasteru (nestandardan stater ali mnogi mapiraju meta na win taster).

Evo ga brzi način za kontrolisanje Vašeg Master glasnoće zvuka, upotrebom CTRL-ALT+ strelica na gore ili dole:

```
Control Mod1 Up :Exec amixer set Master,0 5%+  
Control Mod1 Down :Exec amixer set Master,0 5%-  

```

Ako ste instalirali fluxconf, možete upotrebiti njegov metod editovanja ovoga u GUI-ju sa sledećom komandom:

```
$ fluxkeys

```

Prvi tekstualni boks je za dugme, a drugi je za akciju. Izaberite execCommand da podesite komandu i stavite ime komande u 3\. tekst boks.

Više funkcija ovog tipa možete upotrebiti iz 2\. tekstualnog boksa (Padajući meni je dostupan)

## Radne površine

Fluxbox početna podešavanja imaju četiri radne površine. Ona su dostupna upotrebom Alt+F1-F4 skraćenica, ili strelica na liniji sa alatkama pored mesta gde piše **one**.

Desnim klikom na desktop i ulaskom u Workspaces meni (menumaker koristi: FluxBox>Workspaces, fluxconf korisnici: the workspaces title) će Vam omogućiti interakciju sa radnim površinama.

Meni radnih površina:

```
Icons - prikazuje umanjene aplikacije
--razdvajač--
Workspace names (početna: jedan,dva,tri,četiri) - Prikazuje sve aplikacije na tom desktopu
--razdvajač--
New Workspace - Dodaje radnu površinu
Editu Current workspace name - omogućava Vam da date naziv Vašoj radnoj površini onako kako želite. Prikazaće se na levoj strani linije sa alatkama. 
Remove Last - Uklanja poslednju radnu površinu u listi, izbacuje sve aplikacije koje se nalaze na toj površini na jednu pre nje.

```

## Pozadina

Podešavanje pozadine zahteva program koji to omogućava. Moraćete da instalirate jedan od ovih paketa:

*   eterm
*   feh (nedostaje mu meni transparentnost).

Postoje i drugi ali ovo su dva najpreporučljivija, da vidite ostale proverite fbsetbg dokumentaciju u "Sekciji za dodatne linkove" Da podesite pozadinu:

```
$ fbsetbg /path/to/background.image

```

Takođe možete dodati (ili izmeniti) sledeće linije u fajlu ~/.fluxbox/init u nešto poput ovog:

```
session.screen0.rootCommand:	fbsetbg /path/to/wallpaper

```

Ili jednostavno:

```
session.screen0.rootCommand:	fbsetbg -l

```

#### Dodatne beleške za ljude koji vole da često menjaju pozadine

Dodajte sledeći podmeni u fluxbox meni

```
[submenu] (Pozadine)
[wallpapers] (~/.fluxbox/pozadine)
[wallpapers] (/usr/share/fluxbox/pozadine)
[end]

```

Zatim stavite Vaše slike pozadina u ~/.fluxbox/pozadine ili neki drugi direktorijum koji sami odredite, oni će se zatim pojaviti na isti način kao i Vaši stilovi.

### Feh

Instalirajte feh sa:

```
# pacman -S feh

```

Možete dodati brzi podmeni u Vaš `~/.fluxbox/menu` fajl koji će Vam omogućiti da menjate pozadine u letu:

```
[submenu] (Wallpaper)
[wallpapers] (/staza/ka/Vašim/pozadinama) {feh --bg-scale}
[end]

```

Da bi ste bili sigurni da će fluxbox učitati feh pozadine prilikom sledećeg startovanja:

**1.** Napravite `.fehbg` izvršni fajl:

```
$ chmod 770 ~/.fehbg

```

**2.** Zatim dodajte (ili izmenite) sledeće linije u fajlu `~/.fluxbox/init`:

```
session.screen0.rootCommand:	~/.fehbg

```

**3.** ili dodajte (ili izmenite) sledeće linije u fajlu `~/.fluxbox/startup`:

```
~/.fehbg

```

## Teme

Da bi ste instalirali teme, odpakujte arhivu u direktorijum za stilove. Uobičajeni direktorijumi su:

*   globalni - /usr/share/fluxbox/styles
*   samo korisnik - ~/.fluxbox/styles

Linkovi ka nekim sajtovima sa temama su obezbeđeni ispod.

## GTK2 Themes

_Pogledajte: [GTK+](/index.php/GTK%2B "GTK+")_

## Automatsko startovanje aplikacija

xinitrc korisnici bi trebali da stave sav kod u `~/.xinitrc`. Međutim, fluxbox pruža funkcionalnost za automatsko startovanje programa sam za sebe.

`~/.fluxbox/startup` fajl je skripta za automatsko startovanje aplikacija kao i za startovanje samog fluxbox-a. # simbol označava komentar.

Primerak fajla:

```
fbsetbg -l # podešava poslednju pozadinu, vrlo korisno i preporučljivo.
# U donjim komandama znak (&) je neophodan za sve aplikacije koje se ne gase istog momenta. 
# neuspeh u njihovom obezbeđivanju će uzrokovati time da fluxbox ne startuje.
idesk & 
xterm &
# exec je za startovanje samog fluxboxa, ne stavljajte (&) nakon ovoga ili će fluxbox izaći istog momenta
exec /usr/bin/fluxbox
# ili ako želite da zadržite log, odkomentirajte komandu ispod i stavite pod komentare gornju komandu:
# exec /usr/bin/fluxbox -log ~/.fluxbox/log

```

## Život nakon xorg.conf-a

Xorg više ne zahteva xorg.conf fajl. Tradicionalno ovo je mesto gde bi ste menjali Vaša podešavanja za tastaturu i podešavanja za čuvanje energije. Srećom postoje elegantna rešenja bez upotrebe xorg.conf-a.

### Podešavanje Vaše tastature na pravi način

Dodajte sledeću liniju u `~/.fluxbox/startup`:

```
setxkbmap us & # za tastaturu SAD - Sjedinjene Američke Države
ili za srpsku latinicu dodajte:
setxkbmap rs latin &
za srpsku ćirilicu:
setxkbmap rs &

```

Umesto 'us', 'rs latin' ili 'rs' možete dodati kod za neki drugi jezik i ukloniti prethodnu opciju. Pogledajte man setxkbmap za više opcija.

Da napravite help funkciju u Vašem meniju, jednostavno dodajte `~/.fluxbox/menu`:

```
[submenu] (Tastatura)
      [exec] (srpski latinica) {setxkbmap rs latin}

```

[exec] (srpski ćirilica) {setxkbmap rs}

```
      [exec] (internacionalna) {setxkbmap us}
[end]

```

### Onemogući uštedu energije

Da li prepoznajete problem dok gledate film, a ekran postane crn? Čestitamo, Xorg je upravo primetio da ništa niste radili :). Ako Vam ne trebaju ovakva vežbanja sa pokretima, možete da onemogućite ovu opciju u potpunosti. Samo treba da zapamtite da ručno ugasite Vaš monitor ako ga ne koristite.

Dodajte sledeću liniju na početak `~/.fluxbox/startup`:

```
xset s off -dpms &

```

# Dodatni izbori

*   [Fluxbox Homepage](http://fluxbox.org/)
*   [Gentoo Wiki about Fluxbox](http://wiki.gentoo.org/wiki/Fluxbox)
*   [Themes for Fluxbox](http://box-look.org/)
*   [Fluxbox Wiki](http://fluxbox-wiki.org/)
*   [fbsetbg documentation](http://www.xs4all.nl/~hanb/software/fbsetbg/fbsetbg.html)
*   [Application recommendations](http://archux.com/page/application-recommendations)
*   [Fluxbox Style Guide](/index.php/Fluxbox_Style_Guide "Fluxbox Style Guide")