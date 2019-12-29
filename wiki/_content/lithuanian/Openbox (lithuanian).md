**Openbox** yra lengva ir giliai konfigūruojama langų tvarkyklė, kuri palaiko daug standartu. Jos savybės yra gerai aprašytos [tinklapyje](http://openbox.org/oficialiame). Šis straipsnis susies Openbox naudojimą Arch Linux sistemoje.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Įdiegimas](#Įdiegimas)
*   [2 Autonominė langų tvarkyklė](#Autonominė_langų_tvarkyklė)
*   [3 Langų tvarkyklė darbastalio aplinkoms](#Langų_tvarkyklė_darbastalio_aplinkoms)
    *   [3.1 GNOME](#GNOME)
        *   [3.1.1 GNOME 2.26](#GNOME_2.26)
        *   [3.1.2 GNOME 2.24](#GNOME_2.24)
        *   [3.1.3 GNOME 2.22 ir ankstesni](#GNOME_2.22_ir_ankstesni)
    *   [3.2 KDE](#KDE)
    *   [3.3 Xfce4](#Xfce4)
*   [4 Nustatymai](#Nustatymai)
    *   [4.1 Rankinis nustatymas](#Rankinis_nustatymas)
    *   [4.2 ObConf](#ObConf)
    *   [4.3 Programiniai nustatymai](#Programiniai_nustatymai)
*   [5 Menu](#Menu)
    *   [5.1 Rankinis konfigūravimas](#Rankinis_konfigūravimas)
    *   [5.2 MenuMaker](#MenuMaker)
    *   [5.3 Obmenu](#Obmenu)
        *   [5.3.1 Obm-xdg](#Obm-xdg)
    *   [5.4 Python paremti xdg menu skriptai](#Python_paremti_xdg_menu_skriptai)
    *   [5.5 Pipe menu](#Pipe_menu)
*   [6 Paleisties programos](#Paleisties_programos)
*   [7 Temos ir išvaizda](#Temos_ir_išvaizda)
    *   [7.1 Openbox temos](#Openbox_temos)
    *   [7.2 X11 išvaizda](#X11_išvaizda)
    *   [7.3 X11 pelės kursoriai](#X11_pelės_kursoriai)
    *   [7.4 GTK temos](#GTK_temos)
        *   [7.4.1 GTK2/GTK+](#GTK2/GTK+)
        *   [7.4.2 GTK1](#GTK1)
        *   [7.4.3 GTK šriftai](#GTK_šriftai)
        *   [7.4.4 GTK ikonos](#GTK_ikonos)
    *   [7.5 Darbalaukio ikonos](#Darbalaukio_ikonos)
    *   [7.6 Darbalaukio užsklanda](#Darbalaukio_užsklanda)
*   [8 Rekomenduojamos programos](#Rekomenduojamos_programos)
    *   [8.1 Prisijungimo programos](#Prisijungimo_programos)
    *   [8.2 Kompozitiniai darbastaliai](#Kompozitiniai_darbastaliai)
    *   [8.3 Panelės, dėklai ir puslapiatoriai](#Panelės,_dėklai_ir_puslapiatoriai)
        *   [8.3.1 Panelės](#Panelės)
        *   [8.3.2 Dėklai](#Dėklai)
        *   [8.3.3 Puslapiatoriai](#Puslapiatoriai)
    *   [8.4 Failų tvarkyklės](#Failų_tvarkyklės)
    *   [8.5 Programų leistuvai](#Programų_leistuvai)
        *   [8.5.1 dmenu](#dmenu)
        *   [8.5.2 Gmrun](#Gmrun)
        *   [8.5.3 Bashrun](#Bashrun)
        *   [8.5.4 Launchy](#Launchy)
        *   [8.5.5 LXPanel](#LXPanel)
        *   [8.5.6 gnome-panel](#gnome-panel)
    *   [8.6 Mainų tvarkyklės](#Mainų_tvarkyklės)
    *   [8.7 Garso tvarkyklės](#Garso_tvarkyklės)
        *   [8.7.1 gvolwheel](#gvolwheel)
        *   [8.7.2 gvtray](#gvtray)
        *   [8.7.3 obmixer](#obmixer)
        *   [8.7.4 volti](#volti)
        *   [8.7.5 volumeicon](#volumeicon)
        *   [8.7.6 volwheel](#volwheel)
    *   [8.8 Klaviatūros išdėstymo tvarkyklės](#Klaviatūros_išdėstymo_tvarkyklės)
        *   [8.8.1 fbxkb](#fbxkb)
        *   [8.8.2 xxkb](#xxkb)
        *   [8.8.3 axkb](#axkb)
        *   [8.8.4 xneur](#xneur)
*   [9 Patarimai ir triukai](#Patarimai_ir_triukai)
    *   [9.1 Failų asociacijos](#Failų_asociacijos)
    *   [9.2 Kopijavimas ir įklijavimas](#Kopijavimas_ir_įklijavimas)
    *   [9.3 Skaidrumas](#Skaidrumas)
    *   [9.4 Xprop programų reikšmės](#Xprop_programų_reikšmės)
        *   [9.4.1 Xprop ir Firefox](#Xprop_ir_Firefox)
    *   [9.5 Sujungiant menu ir komandą](#Sujungiant_menu_ir_komandą)
    *   [9.6 Urxvt darbastalio fone](#Urxvt_darbastalio_fone)
    *   [9.7 Garso reguliavimas su klaviatūra](#Garso_reguliavimas_su_klaviatūra)
*   [10 Resursai](#Resursai)

## Įdiegimas

Openbox yra pasiekiamas iš standartinės saugyklos:

```
# pacman -S openbox

```

Iškarto po diegimo pabaigos, pacman nurodys nukopijuoti numatytus `menu.xml` ir `rc.xml` konfigūracines bylas į `~/.config/openbox`, pavyzdžiui:

**Note:** Darykite tai kaip paprastas vartotojas, ne kaip root.

```
$ mkdir -p ~/.config/openbox
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox
$ cp /etc/xdg/openbox/autostart.sh ~/.config/openbox

```

`rc.xml` yra pagrindinis Openbox konfigūracinė byla. Ji naudojama tvarkant klaviatūros nuorodas, temas, virtualius darbastalius ir kitas savybes.

`menu.xml` valdo Openbox programų menu, kuris pasirodo, kai paspaudžiate ant savo darbastalio. Numatytos menu programos yra labai retos, bet menu struktūra yra labai lengvai keičiama, taikantis prie Jūsų poreikių. Jeigu norite sužinoti daugiau apie menu, peržiūrėkite menu skyrių žemiau arba aplankykite [Openbox tinklapį](http://openbox.org).

`autostart.sh` Numatytas paleidimo failas, kuris nustato kelis dalykus Jums. Jūs galite naudoti šį skriptą paleisti panelę, nustatyti darbastalio foną ar kitus dalykus. Daugiau dėtalių [Openbox Wiki](http://openbox.org/wiki/Help:Autostart).

## Autonominė langų tvarkyklė

Norint paleisti Openbox kaip pagrindinę langų tvarkyklę, tiesiog pridėkite sekančią eilutę į `~/.xinitrc` failo pabaigą:

```
exec openbox-session

```

Jeigu Jūs naudojote kitą langų tvarkyklę prieš tai, kaip Xfwm, Openbox nepasileis išregistruojant iš X, pabandykite perkelti autostart aplanką:

```
mv ~/.config/autostart ~/.config/autostart-bak

```

**Note:** [python2-xdg](https://www.archlinux.org/packages/?name=python2-xdg) yra reikalingas Openbox xdg-autostart programai

## Langų tvarkyklė darbastalio aplinkoms

### GNOME

#### GNOME 2.26

***Sekite kitą vadovą GNOME 2.24 versijai. Jeigu nepavyksta, pabandykite tai:***

Jeigu po openbox įdiegimo ir bandymo prisijungti prie 'Gnome/openbox' sesijos, sistema lūžta, tada Jūs galite pabandyti vieną iš tokių būdų, kurie padės Jums paleisti openbox kaip langų tvarkyklę kiekvieną kart, kai tik prisijungsite prie 'Gnome' sesijos iš Jūsų prisijungimo tvarkytojo (xdm, gdm, kdm, entrance, slim, kt.).

1.  Prisijunkite prie vien tik Gnome sesijos ( kuri naudos metacity kaip langų tvarkyklę ), jeigu iki šiol to dar nepadarėte.
2.  Įdiekite openbox, jeigu to dar nepadarėte.
3.  Ištirkite savo menu iki *System → Preferences → Startup Applications* (tikėtina, kad pavadinimas bus 'Session', jeigu naudojate senesnę Gnome versiją)
4.  Atidarykite Startup Application, paspauskite '+ Add' ir įveskite tekstą, kuris matosi tolesniame bloke, ignuorodami tekstą už # simbolio.
5.  Dabar paspauskite 'Add' mygtuką duomenų įvedimo langelyje ir įsitikinkite, kad yra žymė šalia Jūsų naujo įrašo yra pažymėta.
6.  Dabar išsiregistruokite iš gnome sesijos ir įsiregistruokite per naujo. Dabar Jūs jau turėtumėt matyti openbox kaip savo langų tvarkyklę.
7.  Mėgaukitės!

```
Name:    Openbox Windox Manager          # Gali būti pakeista
Command: openbox --replace               # Tekstas negali būti pašalintas iš šitos eilutės, bet gali būti pridėtas
Comment: Replaces metacity with openbox  # Gali būti pakeista

```

Tai sukuria įrašą paleidimo sąraše, kuriuo gnome-session naudojasi paleidžiant programas sesijos pradžioje.

#### GNOME 2.24

Pirmiausiai, sukurkite failą `/usr/share/applications/openbox.desktop` ir įveskite į jį:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=OpenBox
Exec=openbox
NoDisplay=true
# pakraunamo centrinio valdymo modulio vardas
X-GNOME-WMSettingsModule=openbox
# WM charakteristikų tikrinimo vardas
X-GNOME-WMName=OpenBox

```

Tuomet, gconf aplinkoje, nustatykite `/desktop/gnome/session/required_components/windowmanager` `openbox`:

```
$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox

```

Galiausiai, pasirinkite **GNOME** sesiją iš GDM sesijų menu.

#### GNOME 2.22 ir ankstesni

1.  Jeigu naudojate GDM, pasirinkite "GNOME/Openbox" prisijungimo kriterijų
2.  Jeigu naudojate `startx`, pridėkite `exec openbox-gnome-session` į `~/.xinitrc`
3.  Iš terminalo:

```
$ xinit /usr/bin/openbox-gnome-session

```

### KDE

1.  Jeigu naudojate KDM, pasirinkite "KDE/Openbox" prisijungimo kriterijų
2.  Jeigu naudojate `startx`, pridėkite `exec openbox-kde-session` į `~/.xinitrc`
3.  Iš terminalo:

```
$ xinit /usr/bin/openbox-kde-session

```

### Xfce4

Prisijunkite į standartinę Xfce4 sesiją. Pasirinktam terminale įveskite:

```
$ killall xfwm4 ; openbox & exit

```

Sekanti komanda nužudys xfwm4, paleis Openbox ir uždarys terminalą.

Atsijunkite ir įsitikinkite, kad pasirinkote "Save session for future logins" žymę. Sekančiam prisijungime, Xfce4 automatiškai naudos Openbox kaip langų tvarkyklę. Tam, kad būtų galimybė išeiti iš sesijos, pasinaudojant xfce4-session, atidarykite failą `~/.config/openbox/menu.xml` ( jeigu jo ten nėra, nukopijuokite iš `/etc/xdg/openbox/menu.xml`).

Suraskite sekančias eilutes:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

ir jas pakeiskite į:

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

Kitaip, naudojantis "Exit" įrašu pagrindiniame menu, Openbox nutrauks savo darbą ir paliks sistemą be langų tvarkyklės.

Jeigu turite problemų su virtualių darbastalių keitimu, pasinaudojant pelės ratuką, atsidarykite `~/.config/openbox/rc.xml` failą ir nustatykite pelės junginius su "DesktopPrevious" ir "DesktopNext" įvykiais iš "Desktop" konteksto į "Root" kontekstą (gali prireikti sukurti Root kontekstą).

Jeigu norite naudoti Openbox pagrindinį menu, vietoj Xfce pagrindinio menu, galite nutraukti xfdesktop pasinaudojant sekančia komanda:

```
$ xfdesktop --quit

```

Tačiau, xfdesktop tvarko darbastalio foną ir ikonas, tuomet jums reikia naudoti kitas programas, pavyzdžiui ROX, kurios grąžins prarastą funkcionalumą.

(Nutraukiant xfdesktop veiklą, ankščiau paminėta problema su virtualiais darbastaliais, pradingsta.)

## Nustatymai

Šiuo metu egzistuoja du pasirinkimai kaip galima konfigūruoti Openbox nustatymus. Rankiniu būdu redaguojant `rc.xml` arba naudoti ObConf programą.

### Rankinis nustatymas

Norint sukonfigūruoti Openbox rankiniu būdu, paprasčiausiai atidarykite `~/.config/openbox/rc.xml` su mėgstamiausiu redaktoriumi. Konfigūraciniam faile yra daug komentarų, kurie padės susigaudyti, o [pilna dokumentacija](http://openbox.org/wiki/Configuration) yra pasiekiama oficialiame tinklapyje.

### ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) yra grafine aplinka paremtas Openbox konfigūracinis įrankis, kuris gali būti naudojamas daugeliams nustatymų, kaip temos, virtualūs darbastaliai, langų nustatymai ir darbastalio dydžio marža.

Norint įdiegti ObConf, paleiskite:

```
# pacman -S obconf

```

**Note:** ObConf negali būti naudojama konfigūruojant klaviatūros nuorodas ar kitas pažangesnes opcijas. Šiems pakeitimams įgyvendinti, reikia redaguoti `rc.xml` failą rankiniu būdu (žiūrėti aukščiau). Kita galimybė yra naudoti [ObKey](http://code.google.com/p/obkey/) programą, kuri yra pasiekiama per [AUR](/index.php/AUR "AUR").

### Programiniai nustatymai

Openbox palaiko konfigūracija kiekvienai programai atskirai, leidžiant nustatyti taisykles kai kurioms programoms:

*   leisti naršykle tam tikram darbastalyje
*   leisti terminalą be lango apvedžiojimų
*   leisti torrent klientą tam tikroje lango vietoje

Viskas tai nusakoma `~/.config/openbox/rc.xml`. Kaip galima tikėtis, šios instrukcijos yra gerai dokumentuotos pačioje byloje. Pilną dokumentaciją galima rasti čia: [http://openbox.org/wiki/Help:Applications](http://openbox.org/wiki/Help:Applications)

## Menu

Numatytasis Openbox menu įtraukia į save skirtingas programas, bet garantuotai bus būtinybė kas keisti. Yra keli būdai tai padaryti:

### Rankinis konfigūravimas

Panašiai kaip ir su `rc.xml` byla, galima redaguoti `~/.config/openbox/menu.xml` bylą su mėgstamiausiu redaktoriumi. Netgi, jeigu ir kai kurie nustatymai yra gerai paaiškinti, yra pasiekiama [pilna dokumentacija](http://openbox.org/wiki/Help:Menus).

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) yra galingas įrankis, kuris sukuria XML paremtus menu skirtingoms langų tvarkyklėms, tame tarpe ir Openbox. MenuMaker suieškos kompiuteryje paleidžiamų programų ir, priklausomai nuo rezultato, sukurs XML paremtą menu. Jeigu vartotojas nori, jis gali būti sukonfigūruotas, kad būtų nepaisoma Legacy X, GNOME, KDE ar Xfce programų.

MenuMaker yra pasiekiamas bendruomenės repozite:

```
# pacman -S menumaker

```

Po įdiegimo, galima iškarto sugeneruoti menu:

```
$ mmaker -v OpenBox3

```

Pagal numatytas opcijas, MenuMaker neperrašys egzistuojančio menu.xml. Tam, kad jis jį perrašytų reikia pridėti -f (force) argumentą:

```
$ mmaker -vf OpenBox3

```

Norint pamatyti pilną argumentų sąrašą, paleiskit `mmaker --help`.

Tai suteiks gerą menu. Dabar yra galimybė redaguoti menu.xml rankiniu būdu arba regeneruoti sąrašą kiekvieną kart, kai tik yra įdiegiama nauja programa.

### Obmenu

Obmenu yra grafine aplinka paremtas Openbox menu redaktorius. Tiems, kurie nejaučia didelio malonumo redaguojant XML pradinį kodą, tai turbūt yra geriausias sprendimas.

Obmenu yra pasiekiamas bendruomenės repozite:

```
# pacman -S obmenu

```

Po įdiegimo, tiesiog paleiskite `obmenu` ir pridėkite ar ištrinkite programas.

#### Obm-xdg

<tt>obm-xdg</tt> yra komandine eilute paremtas įrankis, kuris ateina kartu su Obmenu. Jis gali sugeneruoti menu, suskirstytą į GTK/GNOME programų kategorijas.

Tam, kad pradėti naudoti obm-xdg, pridėkite sekančia eilutę į `~/.config/openbox/menu.xml`:

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

Tuomet paleiskite `openbox --reconfigure`, kad atnaujinti Openbox menu. Dabar menu lange turėtumėt pamatyti sub-menu pavadinimu **xdg**

**Note:** Jeigu neturite įdiegę GNOME, tuomet jums prireiks įdiegti **gnome-menus** paketą. Tik tuomet obm-xdg veiks.

### Python paremti xdg menu skriptai

Skriptą galima rasti Fedoros Openbox pakete. Tereikės tik kažkur padėti skriptą ir pridėti jį į menu.

Čia galima rasti autoriaus kodą: [http://pastebin.com/f2f827625](http://pastebin.com/f2f827625) Čia galima rasti projekto puslapį: [http://pkgs.fedoraproject.org/gitweb/?p=openbox.git;f=xdg-menu;hb=HEAD](http://pkgs.fedoraproject.org/gitweb/?p=openbox.git;f=xdg-menu;hb=HEAD)

Parsisiųskite tą skriptą, kuris Jums atrodo prieinamesnis ( rekomenduojama siųstis iš projekto puslapio ). Galite patalpinti failą bet kur, autorius naudoja ~/Documents/build/xdg-menu.

Tuomet atsidarykite menu.xml su mėgstamiausiu redaktoriumi ir pridėkite sekantį įrašą, kur norite, kad atsirastų naujas menu įrašas:

```
<menu id="apps-menu" label="xdgmenu" execute="python /home/shiki/Documents/build/xdg-menu"/>

```

Išsaugokite failą ir terminale paleiskite: `openbox --reconfigure`.

### Pipe menu

Openbox ( ir kiti langų tvarkytojai, kaip WindowMaker ar PekWM ) leidžia rašyti skriptus, kurie dinamiškai keičia menu. Jie gali būti taikomi sistemos stebėjimui, muzikos grotuvo kontrolei ar oro pranešimams. Daug pavyzdžių galima rasti openbox [tinklapyje](http://openbox.org/wiki/Openbox:Pipemenus).

Xyne taip pat sukūrė bylų peržiūros programą ir brisbin33 yra naudojamas bevielio tinklo prisijungimams ( tam reikalaujamas netcfg ). Atitinkami forumo pranešimus galima rasti [čia](https://bbs.archlinux.org/viewtopic.php?id=77197&p=1) arba [čia](https://bbs.archlinux.org/viewtopic.php?id=78290)

## Paleisties programos

Openbox siūlo paleisties programų palaikymą. Tai suteikiama pasitelkus "openbox-session" komanda.

Yra du būdai, kaip galima įgalinti paleisties programas:

1.  Jeigu naudojate startx/xinit jungiantis prie X sesijos, paredaguokite `~/.xinitrc` pakeisdami *openbox* į *openbox-session*.
2.  Jeigu naudojate GDM/KDM, tuomet pasirinkite *Openbox* sesiją. Tai automatiškai įgalins paleisties programas.

Paleisties programos yra tvarkomos `~/.config/openbox/autostart.sh` faile. Pilna instrukcija ir geriausius praktinius sprendimus galima rasti [Openbox tinklapyje](http://openbox.org/wiki/Help:Autostart).

## Temos ir išvaizda

Neįskaitant Openbox temų, sekantis skyrius yra orientuotas į vartotojus, kurie pasirinko Openbox kaip vienintelę darbastalio programą, be GNOME, KDE ir Xfce.

### Openbox temos

Openbox tema kontroliuoja lango ribų išvaizdą, įtraukiant lango pavadinimą ir lango mygtukus. Ji taip pat nustato programos menu išvaizdą ir ekrano vaizdą.

Papildomos temos yra pasiekiamos per standartinį repozitą:

```
# pacman -S openbox-themes

```

Paketas yra niekaip neapibūdinamas. Daugiau temų galite gauti:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

Parsiųstos temos turi būti išarchyvuotos į <tt>~/.themes</tt> arba gali būti įdiegtos su ObConf.

Naujų temų kūrimas yra paprastas. Dokumentaciją galite rasti [čia](http://openbox.org/wiki/Help:Themes).

Temas taip pat galite kurti per grafinę aplinką, naudodami [ObTheme](http://xyne.archlinux.ca/info/obtheme) įrankį.

### X11 išvaizda

Jeigu naudojate Openbox kaip pagrindinę savo darbastalio programą, reikės konfigūruoti .Xdefaults failą. Išsaugokite ~/.Xdefaults kopiją į /home/root/.Xdefaults. Tuomet ir `root` vartotojas turės tokį langų atvaizdavimą.

Xdefaults yra vartotojo lygmens konfigūruojamas taškinis failas, dažniausiai randamas kaip ~/.Xdefaults. Kuomet jis egzistuoja, Xorg krovimo metu, jis gali būti nagrinėjamas xorg programos automatiškai, ir gali nustatyti ar perrašyti X ir X programų opcijas. Jis gali atlikti daug operacijų, pavyzdžiui:

```
- nustatyti terminalo spalvas
- konfigūruoti terminalo opcijas
- nustatant DPI, antialiasing, hinting ir kitus X šrifto nustatymus
- keisti Xcursor temą
- nustatyti xscreensaver
- keisti žemo lygio X programų nustatymus ( xclock, xpdf, kt. )

```

Apie Xdefaults daugiau skaitykite [Xdefaults Arch WiKi](/index.php/Xdefaults "Xdefaults")

### X11 pelės kursoriai

Išarchyvuokite norimą Xcursor temą arba į <tt>/usr/share/icons</tt> ( tuomet kursioriaus tema bus pasiekiama globaliai ) arba į <tt>~/.icons</tt> ( tuomet kursoriaus tema bus pasiekiama tik vartotojo ). Yra labai ribotas kursoriaus temų skaičius, kuris pasiekiamas bendruomenės repozite.

Pridėkite `~/.Xdefaults`:

```
Xcursor.theme:   [kursoriaus-temos-vardas]

```

kur `[kursoriaus-temos-vardas]` yra kursoriaus temos direktorijos pavadinimas. Pavyzdžiui:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

Norint pakeisti dydį:

```
Xcursor.size: [dydis]

```

Kai kada yra reikalaujama sukurti sisteminę nuorodą kiekvieno vartotojo namų direktorijoje tam, kad langų tvarkyklė galėtų naudoti kursoriaus temą:

```
$ mkdir ~/.icons
$ ln -s /usr/share/icons/[name-of-cursor-theme] ~/.icons/default

```

Apie kursorių daugiau skaitykite [X11_Cursors Arch Wiki](/index.php/X11_Cursors "X11 Cursors")

### GTK temos

#### GTK2/GTK+

Pirmiausia, išarchyvuokite norimą temą į <tt>/usr/share/themes</tt> ( bus pasiekiama visa sistema ) arba <tt>~/.themes</tt> ( bus pasiekiama vartotojo ), tuomet:

Tvarkyti GTK+ temas galima labai lengva i su **[lxappearance](/index.php/LXDE "LXDE")**, **gtk-chtheme**, arba **switch2** programomis. Įdiegimui, paleiskite:

```
# pacman -S lxappearance

```

ir/arba

```
# pacman -S gtk-chtheme

```

ir/arba

```
# pacman -S gtk-theme-switch2

```

Dabar, kai tik norite pasikeisti temą, tiesiog paleiskite `lxappearance`, `gtk-chtheme` arba `switch2`.

#### GTK1

GTK1 temoms, įdiekite **gtk-theme-switch** paketą:

```
# pacman -S gtk-theme-switch

```

Tuomet paleiskite `switch` ir pasirinkite norimą temą.

#### GTK šriftai

Norint pakeisti šrifto dydį ir tipą rankiniu būdu, pridėkite sekančia eilutę į `~/.gtkrc.mine`:

```
style "user-font"
{
font_name = "[šrifto-pavadinimas] [dydis]"
}
widget_class "*" style "user-font"
gtk-font-name = "[šrifto-pavadinimas] [dydis]"

```

kur `[šrifto-pavadinimas] [dydis]` yra pasirinktas šrifto ir taško dydis. Pavyzdžiui:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Abu `font_name` ir `gtk-font-name` yra reikalingi atvirkštiniam palaikymui.

Norint nustatyti šriftą, taip pat galite naudoti **gtk-chtheme** ir **lxappearance**. Prašome vadovautis ankstesnėmis temomis.

#### GTK ikonos

Pirmiausiai, išarchyvuokite ikonų temą į <tt>/usr/share/icons</tt> ( globaliam pasiekimui ) arba į <tt>~/.icons</tt> ( lokaliam pasiekimui ), tuomet:

Pridėkite sekančia eilutę į `~/.gtkrc.mine` failą:

```
gtk-icon-theme-name = "[name-of-icon-theme]"

```

kur `[name-of-icon-theme]` yra ikonų temos direktoriją. Pavyzdžiui:

```
gtk-icon-theme-name = "Tango"

```

Įsitikinkite, jog `~/.gtkrc-2.0` yra sukonfigūruotas skaityti `~/.gtkrc.mine` failą:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

Norint pasirinkti GTK ikonų temas, taip pat galite naudoti **lxappearance**. Prašome vadovautis ankstesnėmis temomis.

### Darbalaukio ikonos

Openbox nesuteikia darbastalio ikonų. Xfdesktop, PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](http://idesk.sourceforge.net) ir netgi Nautilus ( su gnome-settings-daemon ) gali suteikti tokį funkcionalumą.

ROX ir PCmanFM turi papildomą privalumą, būdami lengvomis failų tvarkyklėmis.

### Darbalaukio užsklanda

Openbox nesuteikia jokio būdo keisti darbalaukio užsklandos. Tai gali labai lengvai kompensuoti tokios programos kaip [Feh](/index.php/Feh "Feh") arba [Nitrogen](/index.php/Nitrogen "Nitrogen"). Kiti būdai įtraukia ImageMagick, hsetroot ir xsetbg. Arba PCmanFM ir Xfdesktop gali tai atlikti.

Nutraukti darbalaukio užsklandos krovimą per gnome-settings-daemon galima taip:

```
$ gconftool-2 --set /apps/gnome_settings_daemon/plugins/background/active --type bool False

```

## Rekomenduojamos programos

Čia galima rasti [lengvų programų sąrašą](/index.php/Lightweight_Applications "Lightweight Applications"); daugelis jų puikiai veikia Openbox.

### Prisijungimo programos

[SLiM](http://slim.berlios.de/) suteikia lengvą ir elegantišką grafinio prisijungimo sprendimą, jeigu Openbox naudojama, kaip autonominė langų tvarkyklė. Daugiau informacijos galite rasti [SLiM](/index.php/SLiM "SLiM") wiki puslapyje.

[Qingy](http://qingy.sourceforge.net/) yra super lengva ir labai konfigūruojama grafinio prisijungimo programa. Jinai palaiko kartu ir konsolinį ir X langų sesijos prisijungimą. Jinai naudoja [DirectFB](http://www.directfb.org). Taip pat ji iškarto nepaleidžia X sesijos, jeigu nebuvo pasirinkta X langų sesija. Daugiau skaitykite [Qingy](/index.php/Qingy "Qingy") wiki puslapyje.

### Kompozitiniai darbastaliai

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") yra lengva kompozito tvarkyklė, sugebanti atvaizduoti šešėlius, blukimą ir paprastą langų skaidrumą kartu su Openbox ir kitom langų tvarkyklėmis.

(Verta pažymėti, jog xcompmgr vystymas yra sustojęs ir jokios problemos nėra taisomos) (Turint problemą su tint2 0.9, sistemos ikonos turi polinkį sulūžti)

### Panelės, dėklai ir puslapiatoriai

Yra labai daug programų, kurie suteikia panelės, dėklo ir puslapiatoriaus galimybę. Pagrindinės yra:

#### Panelės

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

#### Dėklai

*   [Stalonetray](http://stalonetray.sourceforge.net/)
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

#### Puslapiatoriai

*   [Visibility](http://projects.l3ib.org/trac/visibility)
*   [bbpager](http://bbtools.sourceforge.net/)
*   [netwmpager](https://aur.archlinux.org/packages.php?ID=17563)
*   [IPager](http://useperl.ru/ipager/index.en.html)
*   [neap](http://code.google.com/p/neap/)

Padarykite savo pasirinkimą ir pridėkite jį į savo paleidimo failą. Jeigu norite naudoti darbastalį be puslapiatoriaus, galite naudoti [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/), kuris yra setlayout įrankio paketinė versija iš Openbox wiki.

### Failų tvarkyklės

Pasirinkimų yra daug, bet populiariausios tarp lengvų failų tvarkyklių yra:

*   [Thunar](/index.php/Thunar "Thunar"). Thunar palaiko automatinį priregistravimą ( org.: auto-mount ) ir kitus įskiepius.
*   [ROX](http://rox.sourceforge.net) (ROX suteikia darbastalio ikonas)

```
# pacman -S rox

```

*   [PCManFM](http://pcmanfm.sourceforge.net) (pcmanfm taip pat suteikia darbastalio ikonas)

```
# pacman -S pcmanfm

```

Norint pasiekti NTFS diskus su PCmanFM, įdiekite ntfs-3g:

```
# pacman -S ntfs-3g

```

ir įsitikinkite, jog esate *hal* grupėje:

```
# gpasswd -a username hal

```

Norint daug lengvesnių alternatyvų, pasidomėkite [Gentoo](http://www.obsession.se/gentoo/) arba [emelFM2](http://emelfm2.net/), kurie naudoja 'Midnight Commander' stiliaus dviejų panelių išdėstymą.

**Note:** Atnaujinti temą, kai tik bus atnaujintas originalus wiki.

Kiti: Xfe muCommander

Žinoma, galite naudoti ir GNOME'o Nautilus. Nors šitas sprendimas yra žymiai lėtesnis, tačiau Nautilus turi VFS palaikymo privalumą ( pvz.: nuotolinus SSH, FTP ir Samba jungtys ).

### Programų leistuvai

#### dmenu

Nustatykite dmenu kaip aprašyta [dmenu](/index.php/Dmenu "Dmenu") wiki puslapyje. Tuomet, įgalinkite trumpinį, pridėdami sekantį įrašą į `~/.config/openbox/rc.xml` failo <keyboard> sekciją:

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### Gmrun

[Gmrun](http://sourceforge.net/projects/gmrun) suteikia nuostabų paleidimo langą, panašų į Alt+F2 ypatybę, kuri randama Gnome ir KDE aplinkose:

```
# pacman -S gmrun

```

Norint nustatyti Alt+F2 ypatybę, pridėkite sekantį įrašą į `~/.config/openbox/rc.xml` failo <keyboard> sekciją

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

Daugiau informacijos galite rasti [Gmrun](/index.php/Gmrun "Gmrun") wiki puslapyje.

#### Bashrun

[Bashrun](http://bashrun.sourceforge.net) suteikia kitokį, pliko kiauto priėjimo variantą prie paleidimo dialogo, naudojant specialią bash sesiją su mažu xterm langu. Jis yra pasiekiamas bendruomenės repozite ir gali būti paleistas Alt+F2 stiliumi, aptartu aukščiau. Norint *bashrun* naudoti kaip tradicišką paleidimo langą, pridėkite sekantį įtašą į `~/.config/openbox/rc.xml` failo <applications> sekciją:

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

[Launchy](http://www.launchy.net/) yra mažiau minimalistinis priėjimas; Jo išvaizda yra keičiama ir jis siūlo daugiau funkcionalumo, kaip kalkuliatorius, orų pranešimą, kt. Pradžioje kuriamas Windows, panašus į Gnome Do.

```
# pacman -S launchy

```

Jis paleidžiamas Ctrl+Space mygtukų kombinacija.

#### LXPanel

LXPanel paleidimo langas gali būti iškviestas su

```
lxpanelctl run

```

#### gnome-panel

Gnome-panel paleidimo langas gali būti iškviestas su

```
gnome-panel-control --run-dialog

```

### Mainų tvarkyklės

Pagerintam kopijavimui/įklijavimui, yra galimybė įdiegti iškarpų tvarkyklę. **xfce4-clipman-plugin**, **parcellite** arba **glipper-old** gali būti įdiegtos su pacman. Pridėkite savo pasirinkimą į autostart.sh. Paprastai, geriausiai terminale veikia Ctrl+Insert kopijavimui ir Shift+Insert įklijavimui. Taip pat kopijavimui galite naudoti Ctrl+Shift+C ir vidurinį pelės mygtuką įklijavimui.

### Garso tvarkyklės

#### gvolwheel

[Gvolweel](https://aur.archlinux.org/packages.php?ID=25502) yra lengvas garso reguliatorius, kuris leidžia kontroliuoti garso stiprumą per dėklo ikoną.

#### gvtray

[Gvtray](https://aur.archlinux.org/packages.php?ID=6362) yra pagrindinio kanalo reguliatorius sisteminiam dėkle.

#### obmixer

[Obmixer](https://aur.archlinux.org/packages.php?ID=31131) yra C programavimo kalba parašyta reguliatoriaus programėlė, kuri yra lengva gnome garso kontrolės alternatyva.

#### volti

[Volti](https://aur.archlinux.org/packages.php?ID=33525) yra GTK+ programa, kuri kontroliuoja garso lygi iš sisteminio dėklo.

#### volumeicon

[Volumeicon](https://aur.archlinux.org/packages.php?ID=35793) yra garso lygio reguliatorius tavo sisteminiam dėkle.

#### volwheel

[volwheel](https://aur.archlinux.org/packages/volwheel/) yra dėklo ikona, kurios srityje galima keisti garso lygi pelės ratuko pagalba.

### Klaviatūros išdėstymo tvarkyklės

#### fbxkb

[Fbxkb](https://aur.archlinux.org/packages.php?ID=3458) yra klaviatūros indikatorius ir perjungiklis.

#### xxkb

[xxkb](https://www.archlinux.org/packages/?name=xxkb) yra klaviatūros išdėstymo perjungiklis/indikatorius.

#### axkb

[Axkb](https://aur.archlinux.org/packages.php?ID=25555) yra QT4 klaviatūros iįdėstymo perjungiklis.

#### xneur

[X Neural Switcher](https://aur.archlinux.org/packages.php?ID=9750) yra teksto analizatorius, kuris atpažįsta kalba, pagal įvedimą ir pataiso įvesta kalba, jeigu tai yra būtina.

## Patarimai ir triukai

### Failų asociacijos

Kadangi Openbox ir programos, kurios bus naudojamos kartu su juo, nėra labai stipriai integruotos, naršyklė gali susidurti su problema, kad ji nežinos už kokį failų tipą kokia programa atsakinga. AUR saugykloje guli [gnome-defaults-list](https://aur.archlinux.org/packages.php?ID=23170) paketas, kuris turi savyje plėtinius, susietus su programomis gnome darbastaliui. Paketas bus įdiegtas į:

```
/etc/gnome/defaults.list

```

Atidarykite failą su teksto redaktoriumi ir dabar galite ieškoti ir keisti viską, su Jūsų programomis. Kaip totem<=>vlc ar eog<=>mirage. Išsaugokite failą į:

```
~/.local/share/applications/defaults.list

```

Kitas būdas yra naudoti *perl-file-mimeinfo* paketą iš repozito, ir pasiremti mimeopen komanda, pavyzdžiui:

```
mimeopen -d /path/to/file

```

Tuomet bus paprašyta pasakyti kokia programa turi būti susieta su /path/to/file, jos atidarymo metu:

```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

Atsakymas bus susietas kaip numatyta programa visiems tokio pat plėtinio failams.

### Kopijavimas ir įklijavimas

Iš terminalo gerai veikia Ctrl+Insert kopijavimui ir Shift+Insert įklijavimui. Taip pat galite kopijuoti iš terminalo Ctrl+Shift+C ir įklijuoti su viduriniu pelės mygtuko paspaudimu.

### Skaidrumas

Naudodami transset-df programą, kurios pavadinimas iš esmės yra [transset](/index.php?title=Transset&action=edit&redlink=1 "Transset (page does not exist)"), ( pasiekiama *pacman -S transset-df* komanda ) galite iškarto nustatyti langų skaidrumą. Pavyzdžiui redaguodami sekantį bloką `~/.config/openbox/rc.xml` faile, galite padaryti, kad kai pelės žymeklis yra ties lango pavadinimo sritimi, pelės ratuko sukimas įjungtu ar išjungtu skaidrumą:

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

Šiuo metu jis dirbs, kai nebus vykdomi kiti veiksmai.

### Xprop programų reikšmės

Jeigu naudojante kiekvienai programai išskirtinius nustatymus, sekantis bash trumpinys Jums tikriausiai labai padės:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

Norint jį panaudoti, paleiskite **`xp`** ir paspauskite ant norimo programos lango, kurio nustatymus norite pakeisti. Trumpinys parodys informaciją, kuri reikalinga Openbox - WM_WINDOW_ROLE ir WM_CLASS (pavadinimas ir klasė) reikšmes:

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Xprop ir Firefox

Kažkokios priežasties dėka, Firefox ir jo atviro kodo pasekėjai totaliai ignoruoja programų nustatymus ( pvz <desktop> ). Išeitis yra naudoti `class="Firefox*"`, nepriklausomai kokią WM_CLASS reikšmę praneša xprop.

### Sujungiant menu ir komandą

Kai kuriems turi iškilti būtinybė sujungti pagrindinį Openbox menu su kokia nors komanda. Tai yra naudinga, kai norima sukurti naują panelės mygtuką ar panašiai. Nors Openbox to ir nepalaiko, tačiau paprastas skriptas, xdotool, gali simuliuoti klaviatūros paspaudimą. Xdotool yra [pasiekiamas AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd). Norint jį panaudoti, paprasčiausiai pridėkite sekantį kodą į `rc.xml` failo <keyboard> sekciją:

```
    <keybind key="A-C-q">
      <action name="ShowMenu">
        <menu>root-menu</menu>
      </action>
    </keybind>

```

Perkraukite/perkonfigūruokite Openbox. Dabar pagrindinis Openbox menu gali atsirasti stebuklingai paleidus tokią komandą:

```
# xdotool key ctrl+alt+q

```

Žinoma, trumpinį galite pakeisti į bet kokį kitą.

### Urxvt darbastalio fone

Su Openbox, paleisti terminalą darbastalio fone yra lengva.

Pirmiausiai, reikia įjungti skaidrumą. Atsidarykite `.Xdefaults` failą ( jeigu tokio failo nėra, tuomet jį sukurkite ).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #I don't use the whole screen, if you want a full screen term don't bother with this and see below.
URxvt*borderLess:true
URxvt*foreground:Black   #Font color. My wallpaper is White, you may wish to change this to White.

```

Tuomet atsidarykite savo `.config/openbox/rc.xml` failą:

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

*Magija* ateina iš `<layer>below</layer>` eilutės, kuri patalpiną programą po visom kitom programom. Čia Urxvt yra rodomas visuose darbastaliuose. Pakeitimai, žinoma, yra galimi.

Pastaba: Vietoj to, kad naudoti <application name="URxvt">, galite naudoti kitą ( pavyzdžiui "URxvt-bg" ), ir naudoti -name pasirinkimą, kuomet paleidžiama urxvt. Tokiu būdu, tik tie terminalai, kuriuos pavadinsite *URxvt-bg* bus pagauti ir pakeisti, kaip tai aprašyta *rc.xml*. Pavyzdžiui:

```
 urxvt -name URxvt-bg

```

### Garso reguliavimas su klaviatūra

Jeigu garsui naudojate ALSA, galite naudoti įvairias garso reguliavimo programas. Tačiau yra galimybė nustatyti klaviatūros trumpinius, kaip garso reguliatorius. Pavyzdžiui, `.config/openbox/rc.xml` failo <keyboard> sekcijoje:

```
   <keybind key="W-Up">
     <action name="Execute">
       <command>amixer set Master 5%+</command>
     </action>
   </keybind>

```

Tai sujungia *Windows* ir *į viršų* mygtuką su garso padidėjimu 5%. Atitinkamai, garso lygio mažinimui:

```
   <keybind key="W-Down">
     <action name="Execute">
       <command>amixer set Master 5%-</command>
     </action>
   </keybind>

```

Taip pat galite naudoti XF86Audio klaviatūros trumpinius:

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

Aukščiau esantis pavyzdys turi veikti daugelioms daugia-funkcinėms klaviatūroms. Jis turi įgalinti pagrindinio kanalo garso didėjimą, mažėjimą ir išjungimą su daugia-funkciniais mygtukais. Verta paminėti:

*   "Išjungimo" mygtukas turi įjungti pagrindinį kanalą, jeigu jis jau yra išjungtas.
*   "Didėjimo" ir "Mažėjimo" mygtukai turi įjungti pagrindinį kanalą, jeigu jis yra išjungtas.

## Resursai

*   [Openbox Website](http://openbox.org/) – Oficialus tinklapis
*   [Planet Openbox](http://planetob.openmonkey.com/) – Openbox naujienų portalas
*   [Box-Look.org](http://www.box-look.org/) – Geras temų ir kitų dizainų elementų šaltinis
*   [Openbox Hacks and Configs Thread](https://bbs.archlinux.org/viewtopic.php?id=93126) @ Arch Linux Forume
*   [Openbox Screenshots Thread](https://bbs.archlinux.org/viewtopic.php?id=45692) @ Arch Linux Forume