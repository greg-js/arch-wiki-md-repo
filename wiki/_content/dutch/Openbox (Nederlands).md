## Contents

*   [1 Introductie](#Introductie)
*   [2 Installatie](#Installatie)
*   [3 Beginnen](#Beginnen)
    *   [3.1 Openbox gebruiken](#Openbox_gebruiken)
    *   [3.2 Openbox gebruiken met GNOME](#Openbox_gebruiken_met_GNOME)
        *   [3.2.1 GNOME 2.24](#GNOME_2.24)
        *   [3.2.2 GNOME 2.22 en eerder](#GNOME_2.22_en_eerder)
    *   [3.3 Openbox gebruiken met KDE](#Openbox_gebruiken_met_KDE)
    *   [3.4 Openbox gebruiken met Xfce4](#Openbox_gebruiken_met_Xfce4)
*   [4 Configuratie](#Configuratie)
    *   [4.1 Voorkeuren](#Voorkeuren)
        *   [4.1.1 Voorkeuren handmatig instellen](#Voorkeuren_handmatig_instellen)
        *   [4.1.2 Voorkeuren instellen met ObConf](#Voorkeuren_instellen_met_ObConf)
    *   [4.2 Menu beheer](#Menu_beheer)
        *   [4.2.1 Handmatig](#Handmatig)
        *   [4.2.2 MenuMaker](#MenuMaker)
        *   [4.2.3 Obmenu](#Obmenu)
            *   [4.2.3.1 obm-xdg](#obm-xdg)
    *   [4.3 Programma's uitvoeren tijdens opstarten](#Programma.27s_uitvoeren_tijdens_opstarten)
    *   [4.4 Per-applicatie instellingen](#Per-applicatie_instellingen)
    *   [4.5 Thema's en uiterlijk](#Thema.27s_en_uiterlijk)
        *   [4.5.1 Openbox Thema's](#Openbox_Thema.27s)
        *   [4.5.2 Bureaublad achtergronden](#Bureaublad_achtergronden)
        *   [4.5.3 GTK Thema's](#GTK_Thema.27s)
            *   [4.5.3.1 GTK2/GTK+](#GTK2.2FGTK.2B)
            *   [4.5.3.2 GTK1](#GTK1)
        *   [4.5.4 GTK lettertypes](#GTK_lettertypes)
            *   [4.5.4.1 Handmatig het configuratiebestand wijzigen](#Handmatig_het_configuratiebestand_wijzigen)
            *   [4.5.4.2 Met behulp van grafische applicaties](#Met_behulp_van_grafische_applicaties)
        *   [4.5.5 GTK Iconen](#GTK_Iconen)
            *   [4.5.5.1 Handmatig het configuratiebestand wijzigen](#Handmatig_het_configuratiebestand_wijzigen_2)
            *   [4.5.5.2 Met behulp van grafische applicaties](#Met_behulp_van_grafische_applicaties_2)
        *   [4.5.6 Muispijl thema's](#Muispijl_thema.27s)
        *   [4.5.7 Bureaublad Iconen](#Bureaublad_Iconen)
*   [5 Tips en truuks](#Tips_en_truuks)
    *   [5.1 Weergave van lettertypen verbeteren](#Weergave_van_lettertypen_verbeteren)
    *   [5.2 Aanbevolen programma's](#Aanbevolen_programma.27s)
        *   [5.2.1 Login Managers](#Login_Managers)
        *   [5.2.2 Composite Desktop](#Composite_Desktop)
        *   [5.2.3 Applicatie starters](#Applicatie_starters)
            *   [5.2.3.1 dmenu](#dmenu)
            *   [5.2.3.2 Gmrun](#Gmrun)
            *   [5.2.3.3 Bashrun](#Bashrun)
            *   [5.2.3.4 Launchy](#Launchy)
            *   [5.2.3.5 LXPanel](#LXPanel)
        *   [5.2.4 File managers](#File_managers)
        *   [5.2.5 Clipbord beheerders en knippen/plakken](#Clipbord_beheerders_en_knippen.2Fplakken)
        *   [5.2.6 Panelen, Trays, and Pagers](#Panelen.2C_Trays.2C_and_Pagers)
    *   [5.3 xprop waarden voor per-applicatie instellingen snel tonen](#xprop_waarden_voor_per-applicatie_instellingen_snel_tonen)
    *   [5.4 Firefox/Gran Paradiso applicatieregels](#Firefox.2FGran_Paradiso_applicatieregels)
    *   [5.5 Een menu aan een commando koppelen](#Een_menu_aan_een_commando_koppelen)
    *   [5.6 Urxvt in de achtergrond](#Urxvt_in_de_achtergrond)
*   [6 Extra informatie](#Extra_informatie)

## Introductie

Openbox is een lichtgewicht, zeer configureerbare window manager, met uitgebreide ondersteuning voor diverse standaarden. Openbox' features zijn goed gedocumenteerd op de [officiële website](http://icculus.org/openbox/). Dit artikel gaat over het draaien van Openbox onder Arch Linux.

## Installatie

Openbox is beschikbaar van de standaard repository's:

```
# pacman -S openbox

```

Zodra Openbox is geinstalleerd, zal pacman je adviseren om de standaard <tt>menu.xml</tt> en <tt>rc.xml</tt> configuratiebestanden naar de map <tt>~/.config/openbox</tt> te kopieren. Doe dit met:

```
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox/rc.xml
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox/menu.xml

```

***Let op:**Doe dit als gewone gebruiker, niet als root*

<tt>rc.xml</tt> is het belangrijkste configuratiebestand voor Openbox. Het wordt gebruikt om keyboard snelkoppelingen te beheren en instellingen voor thema's, virtuele desktops en andere features te bewaren.

<tt>menu.xml</tt> beheert het applicatiemenu van Openbox, dat verschijnt als je met de rechtermuisknop op je bureaublad klikt. De standaard applicaties zijn behoorlijk schaars, maar het is erg makkelijk om de menu's in te richten zoals je ze zelf wilt hebben. Zie het menu-gedeelte beneden voor meer details, of bezoek de [Openbox website](http://icculus.org/openbox/).

## Beginnen

### Openbox gebruiken

Om Openbox alleenstaand te draaien, voeg je de volgende regel toe onderaan ~/.xinitrc:

```
exec openbox-session

```

### Openbox gebruiken met GNOME

#### GNOME 2.24

Maak eerst het bestand **/usr/share/applications/openbox.desktop** met de volgende inhoud:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=OpenBox
Exec=openbox
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=openbox
# name we put on the WM spec check window
X-GNOME-WMName=OpenBox

```

Zet vervolgens in gconf **/desktop/gnome/session/required_components/windowmanager** op **openbox**:

```
$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox

```

Kies uiteindelijk de **GNOME** sessie in het GDM sessiemenu.

#### GNOME 2.22 en eerder

1.  Als je GDM gebruikt, selecteer dan de "GNOME/Openbox" login optie
2.  Als je startx gebruikt, voeg dan **exec openbox-gnome-session** toe aan ~/.xinitrc
3.  Vanaf de shell:

```
xinit /usr/bin/openbox-gnome-session

```

### Openbox gebruiken met KDE

1.  Als je KDM gebruikt, selecteer dan de "KDE/Openbox" login optie
2.  Als je startx gebruikt, voeg dan **exec openbox-kde-session** toe aan ~/.xinitrc
3.  Vanaf de shell:

```
$ xinit /usr/bin/openbox-kde-session

```

### Openbox gebruiken met Xfce4

Log in in een normale Xfce4 sessie. Open vervolgens een terminal en doe:

```
$ killall xfwm4 ; openbox & exit

```

Dit zal xfwm4 stoppen (de window manager van Xfce), vervolgens de Openbox window manager starten en de terminal sluiten.

Log uit en verzeker jezelf ervan om de "Save session for future logins" checkbox aan te vinken.

Bij de volgende login zal Xfce4 openbox als window manager gebruiken.

Om de sessie te kunnen sluiten via xfce4-session, open je het bestand ~/.config/openbox/menu.xml Zoek naar de regel:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

En verander die naar:

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

Anders zorgt het gebruik van de "Exit" optie in het root-menu ervoor dat Openbox stopt, waardoor je zonder window manager komt te zitten.

Als je een probleem hebt met het schakelen tussen virtuele desktops met je muiswiel die virtuele desktops overslaat, open dan je ~/.config/openbox/rc.xml bestand en verplaats de muiskoppelingen met de acties "DesktopPrevious" en "DesktopNext" van de context "Desktop" naar de context "Root" (het kan zijn dat je de root-context eerst moet definieren).

Als je het Openbox root-menu wilt gebruiken in plaats van het root-menu van Xfce, kun je Xfdesktop stoppen door het volgende commando in een terminal uit te voeren:

```
$ xfdesktop --quit

```

Xfdesktop beheert normaal je actergrond en bureaubladiconen. Als je Xfdesktop hebt gestopt, zul je andere applicaties moeten gebruiken voor deze functionaliteit. Kijk hiervoor eens naar ROX, pcmanfm, feh en anderen.

**Let op:** Als je Xfdesktop stop, is het probleem met de virtuele desktops niet meer van toepassing.

## Configuratie

### Voorkeuren

Op dit moment zijn er twee mogelijkheden om de voorkeuren van Openbox te wijzigen: handmatig wijzigen van het **rc.xml** bestand of het programma ObConf gebruiken.

#### Voorkeuren handmatig instellen

Om Openbox handmatig te configureren, kun je eenvoudigweg het bestand **~/.config/openbox/rc.xml** aanpassen met je favoriete teksteditor. Het configuratiebestand biedt ruim voldoende commentaar bij de opties, en de [volledige documentatie](http://icculus.org/openbox/index.php/Help:Contents) is beschikbaar op de officiële website.

#### Voorkeuren instellen met ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) is een grafische tool om de voorkeuren van Openbox te wijzigen. Obconf kan de meeste voorkeuren wijzigen, waaronder thema's, virtuele desktops, window eigenschappen en desktop marges.

Om Obconf te installeren, voer je als gebruiker root het volgende commando uit:

```
# pacman -S obconf

```

***Let op:***ObConf kan niet worden gebruikt om keyboard snelkoppelingen en een aantal andere geadvanceerde features te wijzigen. Voor deze wijzigingen moet je **rc.xml** handmatig aanpassen (zie boven).

### Menu beheer

Het standaard menu van Openbox bevat koppelingen naar een aantal standaard applicaties, om je op weg te helpen, maar op een bepaald punt wil je de indelingen van de menu's waarschijnlijk wijzigen. Er zijn een aantal mogelijkheden om dit te doen:

#### Handmatig

Zoals ook bij het **rc.xml** bestand, kun je ook **~/.config/openbox/menu.xml** aanpassen met je favoriete teksteditor. Hoewel veel instellingen geen verdere uitleg nodig hebben, is er [volledige documentatie](http://icculus.org/openbox/index.php/Help:Menus) beschikbaar.

#### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) is een krachtige tool die XML-gebaseerde menu's maakt voor een divers aantal window managers, waaronder Openbox. MenuMaker zoekt je computer af naar programma's en maakt daar een XML-menu van. Het programma kan worden geconfigureerd om oude Legacy X applicaties, GNOME, KDE of Xfce applicaties niet mee te nemen in de menu's als de gebruiker dat wenst.

MenuMaker is te installeren vanuit [community]:

```
# pacman -S menumaker

```

Na installatie kun je een compleet menu genereren met:

```
$ mmaker -v OpenBox3

```

MenuMaker zal in de standaardinstelling geen bestaande menu.xml overschrijven. Om dat toch te doen, kun je de -f (force) parameter gebruiken:

```
$ mmaker -vf OpenBox3

```

Voor een volledige lijst van opties gebruik je **mmaker --help**.

Dit geeft je een behoorlijk compleet menu. Nu kun je handmatig het menu.xml bestand veranderen, of de lijst opnieuw genereren, als je nieuwe software hebt geinstalleerd.

#### Obmenu

Obmenu is een grafische menu editor voor Openbox. Voor degenen die liever niet met XML source code aan de slag willen, is Obmenu waarschijnlijk de beste optie.

Obmenu is beschikbaar vanuit [community]:

```
# pacman -S obmenu

```

Na installatie draai je **obmenu** en kun je de gewenste applicaties toevoegen of verwijderen.

##### obm-xdg

<tt>obm-xdg</tt> is een commandline tool die bij Obmenu hoort. obm-xdg kan een gecategoriseerde lijst van geinstalleerde GTK/GNOME applicaties maken.

Voeg de onderstaande regel aan **~/.config/openbox/menu.xml** toe, om obm-xdg te gebruiken:

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

Voer vervolgens **openbox --reconfigure** uit, om het Openbox menu te verversen. Je zou nu een sub-menu met de titel **xdg** moeten zien.

***LET OP:** Indien je GNOME niet geinstalleerd hebt, moet je **gnome-menus** installeren om obm-xdg te laten werken.*

### Programma's uitvoeren tijdens opstarten

Openbox heeft ondersteuning voor het uitvoeren van programma's tijdens het opstarten. Deze functionaliteit wordt voorzien door het "openbox-session" commando.

Er zijn twee manieren om autostart te activeren:

1.  Als je startx of xinit gebruikt om in te loggen op je X sessie, wijzig dan ~/.xinitrc en verander de regel die *openbox* uitvoert naar **openbox-session**.
2.  Indien je inlogt met GDM of KDM, selecteer dan *Openbox* uit het sessie-menu, en autostart wordt automatisch gebruikt.

Programma's die moeten worden opgestart worden beheerd in **~/.config/openbox/autostart.sh**. Instructies voor het automatisch opstarten zijn beschikbaar op de [Openbox website](http://icculus.org/openbox/index.php/Help:Autostart).

### Per-applicatie instellingen

Openbox ondersteunt per-applicatie instellingen, die je toestaan om regels te definieren voor je programma's. Je kunt bijvoorbeeld:

*   je webbrowser laden op een specifieke virtuele destkop
*   je terminal zonder window borders laten opstarten
*   je torrent client op een bepaalde positie op je scherm laten verschijnen

De regels hiervoor worden gedefinieerd in **~/.config/openbox/rc.xml**. Zoals je kon verwachten, zijn de instructies hiervoor uitstekend gedocumenteerd in het bestand zelf. Meer informatie kan hier worden gevonden: [http://icculus.org/openbox/index.php/Help:Applications](http://icculus.org/openbox/index.php/Help:Applications)

### Thema's en uiterlijk

Met uitzondering van het Openbox Thema's topic is de volgende sectie bedoeld voor gebruikers, die Openbox hebben geconfigureerd als alleenstaande desktop, zonder hulp van GNOME, KDE of Xfce.

#### Openbox Thema's

Openbox thema's bepalen het uiterlijk van de window randen, inclusief de titelbalk en de knoppen daarop. Ze bepalen ook het uiterlijk van het applicatie-menu en het on-screen display (OSD).

Extra thema's zijn beschikbaar van de standaard repository's:

```
# pacman -S openbox-themes

```

Dit pakket bevat lang niet alle beschikbare thema's. Je kunt meer thema's downloaden op websites als:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

Gedownloade thema's moeten worden uitgepakt in **~/.themes** en kunnen worden geinstallerd of geselecteerd met ObConf.

Het maken van nieuwe thema's is behoorlijk makkelijk en goed [gedocumenteerd](http://icculus.org/openbox/index.php/Help:Themes).

#### Bureaublad achtergronden

Openbox biedt zelf geen manier om de bureaubladachtergrond te wijzigen. Dit kan echter makkelijk worden gedaan met programma's als [Feh](/index.php/Feh "Feh") of [Nitrogen](/index.php/Nitrogen "Nitrogen"). Daarnaast zijn er nog andere programma's voor, waaronder ImageMagick, hsetroot (en xsetroot en esetroot), xsetbg, pcmanfm, gqview en meer.

#### GTK Thema's

###### GTK2/GTK+

GTK+ thema's kunnen makkelijk worden beheerd met *[lxappearance](/index.php/LXDE "LXDE")*, *gtk-chtheme* of *switch2*. Laatstgenoemden kunnen geinstalleerd worden met:

```
# pacman -S lxappearance

```

en/of

```
# pacman -S gtk-chtheme

```

en/of

```
# pacman -S gtk-theme-switch2

```

Nu kun je eenvoudigweg **lxappearance**, **gtk-chtheme** of **switch2** uitvoeren, om het gewenste thema in te stellen.

###### GTK1

Voor oude GTK1-thema's kun je het pakket **gtk-theme-switch** installeren:

```
# pacman -S gtk-theme-switch

```

Voer vervolgens **switch** uit, om het gewenste thema te selecteren.

#### GTK lettertypes

##### Handmatig het configuratiebestand wijzigen

Als je het lettertype of de lettergrootte wilt veranderen, kun je het volgende toevoegen aan **~/.gtkrc.mime**:

```
style "user-font"
{
font_name = "[font-name] [size]"
}
widget_class "*" style "user-font"
gtk-font-name = "[font-name] [size]"

```

waar [font-name] [size] het gewenste lettertype en lettergrootte (in punten) zijn. Bijvoorbeeld:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Zowel <tt>font_name</tt> en <tt>gtk-font-name</tt> velden zijn vereist voor compatibiliteitsredenen.

##### Met behulp van grafische applicaties

Je kunt **gtk-chtheme** of **lxappearance** gebruiken, om de lettertype instellingen te wijzigen, zie boven.

#### GTK Iconen

Pak eerst het gewenste icoonthema uit naar **/usr/share/icons** (systeem-breed) of **~/.icons** (voor je eigen gebruiker).

##### Handmatig het configuratiebestand wijzigen

Voeg het volgende toe aan ~/.gtkrc.mine:

```
gtk-icon-theme-name = "[name-of-icon-theme]"

```

waar [name-of-icon-theme] de naam van de directory van het icoonthema is. Bijvoorbeeld:

```
gtk-icon-theme-name = "Tango"

```

Verzeker jezelf ervan dat ~/.gtkrc-2.0 is geconfigureerd om ~/.gtkrc.mine te parsen:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

##### Met behulp van grafische applicaties

Je kunt **lxappearance** gebruiken om GTK icoonthema's te kiezen, zie boven.

#### Muispijl thema's

Pak het gewenste Xcursor thema uit naar **/usr/share/icons** (systeemwijd) of **~/.icons** (voor je eigen gebruiker).

Voeg het volgende toe aan ~/.Xdefaults:

```
Xcursor.theme:   [name-of-cursor-theme]

```

waar [name-of-cursor-theme] de naam van de map van het cursorthema is, bijvoorbeeld:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

Om de grootte te veranderen:

```
Xcursor.size: [size]

```

#### Bureaublad Iconen

Openbox biedt zelf geen mogelijkheden aan, om iconen op het bureaublad weer te geven. PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](http://idesk.sourceforge.net) of zelfs Nautilus en de gnome-settings-daemon bieden deze functionaliteit wel.

ROX en PCmanFM hebben daarnaast het voordeel dat het lichtgewichte bestandsbeheerders zijn.

## Tips en truuks

### Weergave van lettertypen verbeteren

Verbeter de weergave van lettertypes op LCD monitoren, door [door deze gids te volgen](/index.php/Fonts#Fonts_with_LCD_filter_enabled "Fonts").

Maak vervolgens ~/.fonts.conf en voeg het volgende toe:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
       <match target="font" >
              <edit mode="assign" name="rgba" >
                     <const>rgb</const>
              </edit>
       </match>
       <match target="font" >
              <edit mode="assign" name="hinting">
                     <bool>true</bool>
              </edit>
       </match>
       <match target="font" >
               <edit mode="assign" name="hintstyle">
               <const>hintfull</const>
               </edit>
       </match> 	
</fontconfig>

```

### Aanbevolen programma's

#### Login Managers

[SLiM](http://slim.berlios.de/) biedt een lichtgewichte elegante grafische loginmanager voor alleenstaande Openbox configuraties. Zie [SLiM](/index.php/SLiM "SLiM") voor meer informatie.

#### Composite Desktop

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") is een lichtgewichte composite manager, die in staat is om vallende schaduwen (drop shadows) te renderen, even als simpele transparante vensters binnen Openbox en andere window managers.

#### Applicatie starters

##### dmenu

Configureer dmenu, zoals beschreven in [dmenu](/index.php/Dmenu "Dmenu"). Voeg vervolgens de volgende regel toe aan het <keyboard>-gedeelte van '***~/.config/openbox/rc.xml** om een snelkoppeling te activeren voor dmenu:*

```
   <keybind key="W-p">
     <action name="Execute">
       <command>~/path/to/your/dmenu-script</command>
     </action>
   </keybind>

```

##### Gmrun

[gmrun](http://sourceforge.net/projects/gmrun) biedt een uitstekende Run dialog box, vergelijkbaar met de Alt+F2 functionaliteit zoals GNOME en KDE dat hebben:

```
pacman -S gmrun

```

Voeg de volgende regel toe aan de <keyboard>-sectie van **~/.config/openbox/rc.xml**, om Alt+F2 functionaliteit te activeren:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

##### Bashrun

[bashrun](http://bashrun.sourceforge.net) biedt een andere aanpak voor een Run dialoog, door een speciale bash-sessie binnen een smal xterm-venster te gebruiken. Bashrun is beschikbaar in de [community] repository en kan worden gestart middels de Alt+F2-methode, zoals bij Gmrun is beschreven. Om Bashrun zich als een wat traditionelere Run dialoog te laten gedragen, kun je de volgende regels toevoegen aan de <application>-sectie van **~/.config/openbox/rc.xml**:

```
   <application name="bashrun">
     <desktop>all</desktop>
     <decor>no</decor>  # switch to yes if you prefer a bordered window
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

##### Launchy

[Launchy](http://www.launchy.net/) is een wat minder minimalistische benadering; het is te skinnen en biedt meer functionaliteit, waaronder een rekenmachine, het weer controleren, etcetera.

```
pacman -S launchy

```

Launchy kan worden gestart middels Ctrl + Space.

##### LXPanel

[LXPanel](http://www.gnomefiles.org/app.php/LXPanel): Als LXPanel wordt gebruikt als taakbalk, dan kan het Run dialog programma van LXPanel worden gebruikt via "lxpanelctl run".

#### File managers

Er zijn veel mogelijkheden, maar de meest populaire lichtgewicht bestandsbeheerders zijn:

*   [Thunar](/index.php/Thunar "Thunar"). Thunar ondersteunt het automatisch mounten van externe media, alsook plugins:
*   [ROX](http://rox.sourceforge.net) (ROX biedt bureaubladiconen)

```
pacman -S rox

```

*   [PCMan](http://pcmanfm.sourceforge.net) (pcmanfm biedt ook bureaubladiconen)

```
pacman -S pcmanfm

```

Voor nog lichtere oplossingen kun je [Gentoo](http://www.obsession.se/gentoo/) of [emelFM](http://emelfm.sourceforge.net/) overwegen, welke beiden een bekende 'Midnight Commander' layout met twee panelen gebruiken. Beide filemanagers vereisen gtk1.2.x. Van ememfm is ook een GTK2-versie beschikbaar, genaamd emelfm2, welke in [extra] aanwezig is.

Natuurlijk kun je ook GNOME's Nautilus gebruiken. Hoewel langzamer als de bovenstaande oplossing, heeft het wel het voordeel dat het VFS ondersteund, waardoor je makkelijk verbinding met SSH, FTP en Samba shares kunt maken.

#### Clipbord beheerders en knippen/plakken

Je zou een Clipbord-beeerder kunnen installeren voor meer knippen/plakken mogelijkheden. **xfce4-clipman-plugin, parcellite,** of **glipper-old** kunnen worden geinstalleerd via pacman. Voeg het programma van je keuze toe aan autostart.sh. Vanaf de terminal werken Ctrl+Insert voor kopieren en Shift+Insert voor plakken vaak goed. Je kunt ook kopieren van de terminal met Ctrl+Shift+C en plakken met de middeste muisknop.

#### Panelen, Trays, and Pagers

Er zijn veel tools beschikbaar, die een paneel (taakbalk), system tray en pager voorzien voor Openbox. De meest bekende zijn:

**Panelen**

*   [PyPanel](/index.php/PyPanel "PyPanel")
*   [bmpanel](http://nsf.110mb.com/bmpanel/)
*   [Tint2](http://code.google.com/p/tint2/)
*   [LXPanel](http://sourceforge.net/projects/lxpanel)
*   [fbpanel](http://fbpanel.sourceforge.net)
*   [PerlPanel](http://perlpanel.org/)
*   [fspanel](http://www.chatjunkies.org/fspanel/)
*   [xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)
*   [gnome-panel](http://developer.gnome.org/arch/gnome/corecomponents/panel/)
*   [avant-window-navigator](http://code.google.com/p/avant-window-navigator/)
*   [cairo-dock](http://developer.berlios.de/projects/cairo-dock/)
*   [wbar](http://code.google.com/p/wbar/)

**Trays**

*   [Stalonetray](http://stalonetray.sourceforge.net/)
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

**Pagers**

*   [Visibility](http://projects.l3ib.org/trac/visibility)
*   [bbpager](http://bbtools.sourceforge.net/)
*   [netwmpager](https://aur.archlinux.org/packages.php?ID=970)
*   [IPager](http://useperl.ru/ipager/index.en.html)

Maak je keuze en voeg deze toe aan autostart.sh.

### xprop waarden voor per-applicatie instellingen snel tonen

Als je vaak gebruik maakt van per-applicatie instellingen, dan vind je deze bash alias mischien handig:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

Om het te gebruiken, voer je **xp** uit en klik je op het draaiende programma, waarvoor je per-applicatie instellingen wilt definieren. Het resultaat zal zijn dat alleen de informatie die Openbox nodig heeft, wordt weergegeven in een terminal venster, namelijk de WM_WINDOW_ROLE en WM_CLASS (naam en klasse) waarden:

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

### Firefox/Gran Paradiso applicatieregels

Om onduidelijke redenen negeren Firefox en zijn open source equivalenten de applicatieregels (waaronder <desktop), tenzij **`class="Firefox*"`** wordt gebruikt, ook al geeft xprop andere waarden aan voor WM_CLASS.

### Een menu aan een commando koppelen

Sommige mensen willen het Openbox hoofdmenu of een ander menu aan een commando koppelen. Dit is bijvoorbeeld handig om een menu-knop in een paneel te maken. Hoewel Openbox dit niet ondersteunt, is er een makkelijk script, xdotool, die een toetsaanraking kan simuleren door een commando uit te voeren. Xdotool is [beschikbaar in AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd). Voeg de volgende code toe aan het <keyboard>-gedeelte van je rc.xml:

```
    <keybind key="A-C-q">
      <action name="ShowMenu">
        <menu>root-menu</menu>
      </action>
    </keybind>

```

Herstart/herconfigureer Openbox. Je kunt nu je menu op de positie van je cursor oproepen, door het volgende commando uit te voeren:

```
# xdotool key ctrl+alt+q

```

Uiteraard kun je de snelkoppeling veranderen.

### Urxvt in de achtergrond

Met Openbox is het draaien van een terminal in de achtergrond makkelijk; je hebt geen **devilspie** nodig.

Allereerst moet je transparantie activeren. Open je **~.Xdefaults** bestand (of maak het indien het niet bestaat).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #I don't use the whole screen, if you want a full screen term don't bother with this and see below.
URxvt*borderLess:true
URxvt*foreground:Black   #Font color. My wallpaper is White, you may wish to change this to White.

```

Wijzig vervolgens je **.config/openbox/rc.xml** bestand:

```
<application name="urxvt">
  <decor>no</decor>
  <focus>yes</focus>
  <position>
    <x>center</x>
    <y>20</y>
  </position>
  <layer>below</layer>
  <desktop>all</desktop>
  <maximized>true</maximized> #Alleen als je een schermvullende terminal wilt
</application>

```

De *magie* komt van de **<layer>below</layer>** regel, welke de applicatie onder alle andere applicaties plaatst. Hier is Urxvt weergegeven op alle virtuele desktop, verander dit indien gewenst.

## Extra informatie

*   [Openbox Website](http://icculus.org/openbox/) - De officiële website
*   [Planet Openbox](http://planetob.openmonkey.com/) - Openbox nieuwsportaal
*   [Box-Look.org](http://www.box-look.org/) - Een goede bron voor thema's en gerelateerde kunst