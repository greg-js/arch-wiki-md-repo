[rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) visoko prilagodljivi [terminal emulator](/index.php?title=Terminal_Emulator&action=edit&redlink=1 "Terminal Emulator (page does not exist)") nastao od [rxvt](https://en.wikipedia.org/wiki/Rxvt kako bi smanjio korišćenje sistemskih resursa. Razvijen od strane Marc Lehmann-a, neke od značajnijih odlika rxvt-unicode uključuju internacionalnu podršku jezika kroz [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"), mogućnost da prikaže različite tipove fonta i podrška za [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") ekstenzije.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacija](#Instalacija)
*   [2 Konfiguracija](#Konfiguracija)
    *   [2.1 Kreiranje ~/.Xresources](#Kreiranje_~/.Xresources)
    *   [2.2 Prava providnost](#Prava_providnost)
    *   [2.3 Traka za pomeranje](#Traka_za_pomeranje)
    *   [2.4 Metode Deklaracije Fontova](#Metode_Deklaracije_Fontova)
*   [3 Perl ekstenzije](#Perl_ekstenzije)
    *   [3.1 Klikabilni URLovi](#Klikabilni_URLovi)
    *   [3.2 Duplikatni URLovi (Bez Miša)](#Duplikatni_URLovi_(Bez_Miša))
    *   [3.3 Tabovi](#Tabovi)
*   [4 Poboljšanje performansi](#Poboljšanje_performansi)
*   [5 Cut i Paste](#Cut_i_Paste)
    *   [5.1 Klipbord Menadžment](#Klipbord_Menadžment)
    *   [5.2 Menadžment Automatskih Skripti](#Menadžment_Automatskih_Skripti)
*   [6 Poboljšano Kuake-oliko Ponašanje u Openboxu](#Poboljšano_Kuake-oliko_Ponašanje_u_Openboxu)
    *   [6.1 Scriptleti](#Scriptleti)
    *   [6.2 urxvtq sa tabovima](#urxvtq_sa_tabovima)
        *   [6.2.1 Kontrola tabova](#Kontrola_tabova)
    *   [6.3 Openbox konfiguracija](#Openbox_konfiguracija)
    *   [6.4 Dalja konfiguracija](#Dalja_konfiguracija)
    *   [6.5 Povezane skripte](#Povezane_skripte)
*   [7 Rešavanje problema](#Rešavanje_problema)
    *   [7.1 Providnost ne radi posle nadogradnje na V9.09](#Providnost_ne_radi_posle_nadogradnje_na_V9.09)
    *   [7.2 Daljinski Hostovi](#Daljinski_Hostovi)
    *   [7.3 Korišćenje rxvt-unicode kao gmrun terminal](#Korišćenje_rxvt-unicode_kao_gmrun_terminal)
*   [8 Eksterni resursi](#Eksterni_resursi)

## Instalacija

[rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) je dostupan u [extra] i uključuje podršku 256 boja:

```
# pacman -S rxvt-unicode

```

[rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched/) je dostupan u [AUR](/index.php/AUR "AUR") i uključuje popravku za kvar širine fonta i dodaje podršku za ignorisanje hintova za veličinu prozora (zaključavanje veličine prozora na n_columns * column_width, itd.) bez mrtvog prostora.

## Konfiguracija

Pogledajte [rxvt-unicode dokumentaciju](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) za kompletnu listu dostupnih podešavanja i vrednosti.

### Kreiranje ~/.Xresources

Izgled, osećaj i funkcija rxvt-unicode je kontrolisana preko argumenata komandne linije i/ili [X resources](https://en.wikipedia.org/wiki/X_resources "wikipedia:X resources"). X resources se može podesiti preko `~/.Xresources` i xrdb, pogledajte [wiki stranu](/index.php/Xresources "Xresources") za detalje.

**Note:** Argumenti u komandnoj liniji imaju prednost u odnosu na podešavanja resursa određenih u ovom fajlu.

### Prava providnost

Za korišćenje prave providnosti morate koristiti menadžer prozora koji podržava compositing ili poseban compositor.

Iz komandne linije:

```
$ urxvt -depth 32 -bg rgba:3f00/3f00/3f00/dddd

```

Koristeći konfiguracioni fajl:

 `~/.Xresources` 
```
URxvt.depth:      32
URxvt.background: rgba:3f00/3f00/3f00/dddd
!Ako ta boja ne radi kako valja, pokušajte:
!urxvt*background: rgba:1111/1111/1111/dddd

```

### Traka za pomeranje

Izgled trake za pomeranje može biti odabran kroz ovaj unos u `~/.Xresources`:

```
# scrollbar style - rxvt (default), plain, next, ili xterm
URxvt*scrollstyle:rxvt

```

Od kojih je "plain" najkompaktniji.

### Metode Deklaracije Fontova

```
URxvt.font:  9x15

```

je isto što i:

```
URxvt.font:  -misc-fixed-medium-r-normal--15-140-75-75-c-90-iso8859-1

```

i:

```
URxvt.font:  9x15bold

```

je isto što i:

```
URxvt.font:  -misc-fixed-bold-r-normal--15-140-75-75-c-90-iso8859-1

```

Kompletna lista skraćenica X core fontova se može naći u `/usr/share/fonts/misc/fonts.alias` (takođe postoje neki fonts.alias u nekim od drugih poddirektorijuma `/usr/share/fonts/`, ali kako su oni pakovani odvojeno od pravih fontova, mogu prikazati fontove koje uopšte nemate instalirane). Treba reći i da ovi kratki alijasi biraju ISO-8859-1 verziju fonta pre nego ISO-10646-1 (Unicode) verzije, i 75 DPI pre nego 100 DPI verzije, pa je verovatno bolje izbegavati ih i birati fontove po njihovom punom, dužem imenu.

*   Pasus iznad važi samo za bitmap fontove. Xft fontovi mogu biti određeni koristeći sledeći format:

```
Urxvt.font: xft:monaco:size=10

```

Ili

```
Urxvt.font: xft:monaco:bold:size=10

```

## Perl ekstenzije

### Klikabilni URLovi

Možete podesiti klikabilne URLove u terminalu koristeći matcher ekstenziju. Na primer, za otvaranje linkova u [Firefox](/index.php/Firefox "Firefox") dodajte sledeće u `.Xresources`:

```
URxvt.perl-ext-common:  default,matcher
URxvt.urlLauncher:      /usr/bin/firefox
URxvt.matcher.button:   1 

```

### Duplikatni URLovi (Bez Miša)

Kao dodatak, možete odibarati i otvarati URLove u vašem web pregledaču bez korišćenja miša.

Instalirajte [urxvt-url-select](https://www.archlinux.org/packages/?name=urxvt-url-select) paket iz [community] repoa i podesite vaš `.Xresources` prema potrebi. Primer je prikazan ispod:

```
URxvt.perl-ext:      default,url-select
URxvt.keysym.M-u:    perl:url-select:select_next
URxvt.urlLauncher:   firefox
URxvt.underlineURLs: true

```

**Note:** Ova ekstenzija menja Klikabilni URLovi ekstenziju pomenutu iznad pa `matcher` može biti uklonjen iz `URxvt.perl-ext` liste.

**Key commands:**

`Alt` + `U` Ulaz u odabirni modus. Poslednji URL na vašem ekranu će biti odabran. Možete ponoviti `Alt+u` da odaberete sledeći URL iznad.

`k` Odabir sledećeg URLa iznad

`j` Odabir sledećeg URLa ispod

`Return` Otvaranje odabranog URLa u pregledaču i izlaz iz odabirnog modusa

`o` Otvaranje odabranog URLa u pregledaču bez izlaska iz odabirnog modusa

`y` Kopiranje (dupliranje) odabranog URLa i izlaz iz odabirnog modusa

`Esc` Izlaz iz odabirnog modusa

### Tabovi

Za dodavanje tabova u urxvt, dodajte sledeće u vaš `~/.Xresources`:

```
URxvt.perl-ext-common:  default,tabbed

```

To control tabs use:

`Shift` + `↓` novi tab

`Shift` + `←` prelazak u tab levo

`Shift` + `→` prelazak u tab desno

`Ctrl` + `←` pomeranje taba u levo

`Ctrl` + `→` pomeranje taba u desno

`Ctrl` + `d`: zatvaranje taba

Možete promeniti boje tabova na sledeći način:

```
URxvt.tabbed.tabbar-fg: 2
URxvt.tabbed.tabbar-bg: 0
URxvt.tabbed.tab-fg:    3
URxvt.tabbed.tab-bg:    0

```

Boje moraju biti određene korišćenjem indeksa boja: 0 do 15 odgovaraju bojama iz rxvt uputstva, sekcija "Boja i Grafika".

```
BOJA I GRAFIKA

Ako je grafička podrška omogućena u vreme kompajliranja, može biti pokrenut sa ANSI escape sekvencama i može prikazati individualne piksele umesto tekstualnih karaktera. Treba paziti jer se grafička podrška i dalje smatra beta kodom.

Kao dodatak osnovnim foreground i background bojama, rxvt može prikazati do 16 boja (8 ANSI boja plus visoko-intenzivna bold/blink
verzije istih). Evo liste boja sa njihovim rgb.txt imenima.

color0 	(crna)   	 = Black
color1 	(crvena)         = Red3
color2 	(zelena) 	 = Green3
color3 	(žuta) 	         = Yellow3
color4 	(plava)	         = Blue3
color5 	(purpurna)  	 = Magenta3
color6 	(cyan) 	         = Cyan3
color7 	(bela) 	         = AntiqueWhite
color8 	(svetlo crna) 	 = Grey25
color9 	(svetlo crvena)	 = Red
color10 (svetlo zelena)	 = Green
color11 (svetlo žuta)    = Yellow
color12 (svetlo plava) 	 = Blue
color13 (svetlo purpurna)= Magenta
color14 (svetlo cyan) 	 = Cyan
color15 (svetlo bela) 	 = White
foreground 		 = Black
background 		 = White

Takođe je moguće odrediti vrednost boje od foreground, background, cursorColor, cursorColor2, colorBD, colorUL kao broj 0-15, kao korisna skraćenica koja se odnosi na ime boje od color0-color15.

Komanda -rv ("reverseVideo: True") simulira obrnuti video tako što uvek menja foreground sa background bojom. Ovo je u kontrastu sa xterm(1)
gde su boje obrnute samo ako inače nisu bile određene. Na primer,

rxvt -fg Black -bg White -rv
    bi prikazao belu na crnoj,dok na xterm(1) bi prikazalo crnu na beloj.
```

Za imenovane tabove, pogledajte [ovaj paket u AUR](https://aur.archlinux.org/packages.php?ID=38990), (Shift+Up: imenuje tab).

## Poboljšanje performansi

*   Izbegavajte korišćenja Xft fontova. Ako morate koristiti Xft fontove, dodajte `:antialias=false` uz zadatu vrednost.

*   Podignite rxvt-unicode sa isključenom podrškom za nepotrebne odlike, `--disable-xft` and `--disable-unicode3` na primer.

*   Limitirajte broj `saveLines` (option `-sl`) u scrollback baferu da smanjite potrošnju memorije.

*   Razmotrite pokretanje `urxvtd` kao daemon koji prima konekcije od `urxvtc` klijenata.

## Cut i Paste

Za korisnike kojima nije poznata [Xorg](/index.php/Xorg "Xorg") metoda transfera podataka, razmena informacija u i iz rxvt-unicode može postati teret. Dovoljno je reći da rxvt-unicode koristi cut bafere koji su inače učitavani u `PRIMARY` selekciju. Korisnicima se strogo preporučuje čitanje [Wikipedia:X Window selection](https://en.wikipedia.org/wiki/X_Window_selection "wikipedia:X Window selection") za dodatne informacije.

#### Klipbord Menadžment

*   [Parcellite](http://parcellite.sourceforge.net/) je GTK+ klipbord menadžer koji se može pokrenuti u pozadini kao daemon.

*   [autocutsel](http://www.nongnu.org/autocutsel/) obezbeđuje komandnu liniju i daemon interfejs za sinhronizaciju PRIMARY, `CLIPBOARD` i cut selekciju bafera.

*   [Glipper](http://glipper.sourceforge.net/) je [GNOME](/index.php/GNOME "GNOME") panel applet sa dostupnim starijim verzijama za korišćenje u drugim okruženjima osim GNOME.

*   [Clipman](http://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin) (xfce-clipman-plugin) je GUI klipbord menadžer plugin za [Xfce](/index.php/Xfce "Xfce") panel (xfpanel).

#### Menadžment Automatskih Skripti

Skottish[[5]](https://bbs.archlinux.org/viewtopic.php?pid=506845#p506845) je kreirao perl skriptu da automatski kopira bilo koju selekciju iz urxvt u X klipbord. Snimite sledeće kao `/usr/lib/urxvt/perl/clipboard`:

```
#! /usr/bin/perl

sub on_sel_grab {
    my $query=quotemeta $_[0]->selection;
    $query=~ s/
/\
/g;
    $query=~ s/\r/\\r/g;
    system( "echo -en " . $query . " | xsel -i -b -p" );
}

```

Xyne je napravio svoju varijantu Skottish-ove skripte (koja je takođe [dostupna u AUR](https://aur.archlinux.org/packages.php?ID=35526)):

```
#! /usr/bin/perl

sub on_sel_grab {
    my $query = $_[0]->selection;
    open (my $pipe,'|-','xsel -ibp') or die;
    print $pipe $query;
    close $pipe;
}

```

Za nju je takođe potreban `xsel` i mora biti omogućen u `*perl-ext-common` ili `*perl-ext` poljima u `.Xresources`. Na primer:

```
URxvt.perl-ext-common: default,clipboard

```

## Poboljšano Kuake-oliko Ponašanje u Openboxu

Ovo je najpre postovano na forumu od strane Xyne i oslanja se na `xdotool` koji je dostupan u community repou.

### Scriptleti

Snimite ovaj scriptlet iz `urxvtc` man strane negde u vašem sistemu kao `urxvtc` (Npr, u `~/.config/openbox`):

```
#!/bin/sh
urxvtc "$@"
if [ $? -eq 2 ]; then
   urxvtd -q -o -f
   urxvtc "$@"
fi

```

i snimite ovaj kao `urxvtq`:

```
#!/bin/bash

wid=$(xdotool search --classname urxvtq)
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 80x28
  wid=$(xdotool search --classname urxvtq | head -1)
  xdotool windowfocus $wid
  xdotool key Control_L+l
else
  if [ -z "$(xdotool search --onlyvisible --classname urxvtq 2>/dev/null)" ]; then
    xdotool windowmap $wid
    xdotool windowfocus $wid
  else
    xdotool windowunmap $wid
  fi
fi

```

Prethodna verzija xdotool je donela i kvar koji je isključivao prepoznavanje vidljivih prozora i tako naveo neke korisnike da koriste sledeći scriptlet umesto gore navedenog. Ovo više nije potrebno jer xdotool>=1.20100416.2809, ali je ostavljeno ovde kao napomena za ubuduće.

```
#!/bin/bash

wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 200x28
  wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
  xdotool windowfocus $wid
  xdotool key Control_L+l
else
  if [ -z "$(xprop -id $wid | grep 'window state: Normal' 2>/dev/null)" ]; then
    xdotool windowmap $wid
    xdotool windowfocus $wid
  else
    xdotool windowunmap $wid
  fi
fi

```

Ne zaboravite da promenite `/path/to/urxvtc` na pravu adresu do `urxvtc` scriptleta koji ste snimili iznad. Koristićemo `urxvtc` da pokrenemo i regularne instance `urxvt` kao i kuake-olike instance.

### urxvtq sa tabovima

Ako želite da imate tagove u vašem kuake-olikom `urxvtc` (ovde zvanim `urxvtq`) samo zamenite treći red u vašem `urxvtq`:

```
wid=$(xdotool search --name urxvtq)

```

sa:

```
wid=$(xdotool search --name urxvtq | grep -m 1 "" )

```

Da aktivirate podršku tabova, možete ili zameniti peti red u vašem `urxvtq`:

```
/path/to/urxvtc -name urxvtq -geometry 80x28

```

sa:

```
/path/to/urxvtc -name urxvtq -pe tabbed -geometry 80x28

```

ili zameniti sledeći red u vašem `.Xresources`:

```
URxvt.perl-ext-common: default,matcher

```

sa

```
URxvt.perl-ext-common: default,matcher,tabbed

```

#### Kontrola tabova

<SHIFT>-Levo: Pomeranje u tab levo od onoga u kom ste trenutno

<SHIFT>-Desno: Pomeranje u tab desno od onoga u kom ste trenutno

<SHIFT>-Dole: Kreiranje novog taba

Možete takođe koristiti vaš miš za kretanju izmedju tabova samo kliknite na onaj koji želite ili kreirati novi tab tako što ćete kliknuti na *[NEW].\\*

Za zatvaranje taba samo unesite 'exit' kao kad zatvarate terminal.

### Openbox konfiguracija

Dodajte sledeće redove u `<applications>` sekciju od `~/.config/openbox/rc.xml`:

```
<application name="urxvtq">
   <decor>no</decor>
   <position force="yes">
     <x>center</x>
     <y>0</y>
   </position>
   <desktop>all</desktop>
   <layer>above</layer>
   <skip_pager>yes</skip_pager>
   <skip_taskbar>yes</skip_taskbar>
   <maximized>Horizontal</maximized>
</application>
```

i dodajte ove redove u `<keyboard>` sekciju:

```
<keybind key="W-t">
  <action name="Execute">
    <command>/path/to/urxvtc</command>
  </action>
</keybind>
<keybind key="W-grave">
  <action name="Execute">
    <execute>/path/to/urxvtq</execute>
  </action>
</keybind>
```

I ovde morate promeniti `/path/to/*` redove tako da pokazuju na skriptu koju ste snimili iznad. Snimite fajl a onda rekonfigurišite Openbox. Sada bi trebalo da možete da pokrenete regularne instance urxvt sa Windows/Super key + "**t**", koristite kuake-oliku konzolu sa Windows/Super+grave (**`**).

### Dalja konfiguracija

Prednost ove konfiguracije nad urxvt kuake perl skriptom je ta što Openbox obezbeđuje više opcija za korišćenje prečica na tastaturi kao što su "modifier" tasteri. Kuake skripta oduzima ceo fizički taster nevezano za bilo kakvu modifier kombinaciju. Pregledajte [Openbox dokumentaciju tastera](http://icculus.org/openbox/index.php/Help:Bindings) za pun dijapazon mogućnosti.

[Openbox pojedinačna podešavanja](http://icculus.org/openbox/index.php/Help:Applications) se mogu koristiti za dalje konfigurisanje ponašanja kuake-olike konzole (Npr, pozicija ne ekranu, sloj, itd), možda ćete morati da promenite "geometry" parametar u `urxvtq` scriptletu da prilagodite visinu konzole.

### Povezane skripte

*   hbekel je postovao generalizovanu vertiju `urxvtq` [here](https://bbs.archlinux.org/viewtopic.php?pid=550380#p550380) koja se može koristiti za menjanje bilo koje aplikacije koristeći `xdotool`.

*   [http://www.jukie.net/~bart/blog/20070503013555](http://www.jukie.net/~bart/blog/20070503013555) - Skripta za otvaranje url-ova sa vašom tastaturom umesto mišem u okviru urxvt.

## Rešavanje problema

### Providnost ne radi posle nadogradnje na V9.09

rxvt-unicode developeri su uklonili kod za kompatibilnost za mnoge nestandardne programe za podešavanje pozadine(wallpaper) u ovoj verziji. Korišćenje nekompatibilnog programa za postavljanje pozadine će pokvariti podršku za providnost. Zato se preporučuju sledeći programi:

*   [feh](/index.php/Feh "Feh")
*   hsetroot
*   esetroot

Da bi prava providnost radila, morate komentovati urxvt*tintColor i urxvt*inheritPixmap.

### Daljinski Hostovi

Ako se logujete na daljinski host, možete se suočiti sa problemima kada pokrećete tekstualne programe u rxvt-unicode. Ovo se može rešiti kopirajući `/usr/share/terminfo/r/rxvt-unicode` iz vaše lokalne mašine na vaš host `~/.terminfo/r/rxvt-unicode`.

### Korišćenje rxvt-unicode kao gmrun terminal

Za razliku od nekih drugih terminala, urxvt očekuje argumente do -e da budu zadati odvojeno, a ne zajedno grupisane pod navodnicima. Ovo izaziva probleme sa gmrun, koji pretpostavlja suprotno. Ovo se može rešiti dodavanjem "eval" ispred gmrun-ove "Terminal" varijable u .gmrunrc:

```
Terminal = eval urxvt
TermExec = ${Terminal} -e
```

(gmrun koristi /bin/sh za izvršavanje komandi, pa se "eval ovde podrazumeva.) "eval" ima sporedni efekat "razbijanja" argumenta do -e na isti način kao što $@ radi u bash-u, čineći komandu shvatljivom za urxvt.

## Eksterni resursi

*   [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) - Zvanični sajt
*   [rxvt-unicode FAQ](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod) - Zvanični FAQ
*   [rxvt-unicode Reference](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) - Zvanična strana uputstva
*   [urxvtperl](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/src/urxvt.pm) - Zvanično uputstvo za perl ekstenzije
*   [urxvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/urxvt.1)