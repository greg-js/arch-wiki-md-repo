## Contents

*   [1 Introduktion](#Introduktion)
*   [2 Installation af Xorg](#Installation_af_Xorg)
*   [3 Konfigurere xorg](#Konfigurere_xorg)
    *   [3.1 hwd](#hwd)
    *   [3.2 xorgconfig](#xorgconfig)
    *   [3.3 Xorg -configure](#Xorg_-configure)
    *   [3.4 nvidia-xconfig](#nvidia-xconfig)
*   [4 Redigere xorg.conf](#Redigere_xorg.conf)
    *   [4.1 Skærmindstillinger](#Skærmindstillinger)
        *   [4.1.1 Horizontal Sync (Horisontal synkronisering)](#Horizontal_Sync_(Horisontal_synkronisering))
        *   [4.1.2 Refresh Rate (Genopfriskningsrate)](#Refresh_Rate_(Genopfriskningsrate))
        *   [4.1.3 Colour Depth (Farvedybe)](#Colour_Depth_(Farvedybe))
        *   [4.1.4 Resolution (Opløsning)](#Resolution_(Opløsning))
    *   [4.2 Tastaturindstillinger](#Tastaturindstillinger)
        *   [4.2.1 Tastatur-layout](#Tastatur-layout)
        *   [4.2.2 Tastatur-model](#Tastatur-model)
    *   [4.3 Skærmstørrelse/DPI](#Skærmstørrelse/DPI)
    *   [4.4 Proprietære drivere](#Proprietære_drivere)
    *   [4.5 Fonte](#Fonte)
    *   [4.6 Eksempler på Xorg.conf-file](#Eksempler_på_Xorg.conf-file)
*   [5 Køre Xorg](#Køre_Xorg)
*   [6 Finpudse opstarten af X (/usr/bin/startx)](#Finpudse_opstarten_af_X_(/usr/bin/startx))
*   [7 Ændringer med modulær Xorg](#Ændringer_med_modulær_Xorg)
    *   [7.1 Mest almindelige pakker](#Mest_almindelige_pakker)
    *   [7.2 OpenGL 3D-acceleration](#OpenGL_3D-acceleration)
    *   [7.3 Glxgears og Glxinfo](#Glxgears_og_Glxinfo)
    *   [7.4 Ændrede søgestier (og konfiguration)](#Ændrede_søgestier_(og_konfiguration))
*   [8 Fejlfinding](#Fejlfinding)
    *   [8.1 Tastaturproblemer](#Tastaturproblemer)
    *   [8.2 Et hurtigt fiks for konflikten Bitstream-Vera](#Et_hurtigt_fiks_for_konflikten_Bitstream-Vera)
    *   [8.3 Et hurtigt fiks af filkonflikter i /usr/include](#Et_hurtigt_fiks_af_filkonflikter_i_/usr/include)
    *   [8.4 Musehjul fungerer ikke](#Musehjul_fungerer_ikke)
    *   [8.5 Ekstra museknap virker ikke](#Ekstra_museknap_virker_ikke)
    *   [8.6 Tastaturproblemer](#Tastaturproblemer_2)
        *   [8.6.1 AltGR fungerer ikke ordentligt](#AltGR_fungerer_ikke_ordentligt)
        *   [8.6.2 Kan ikke sætte 'qwerty'-layout op med kommandoen 'setxkbmap'](#Kan_ikke_sætte_'qwerty'-layout_op_med_kommandoen_'setxkbmap')
        *   [8.6.3 Opsætning af fransk-canadisk layout (gammel 'ca_enhanced)](#Opsætning_af_fransk-canadisk_layout_(gammel_'ca_enhanced))
    *   [8.7 Manglende biblioteker](#Manglende_biblioteker)
    *   [8.8 Bygning af nogle pakker fejler, og der klages over manglende X11-inkluderinger](#Bygning_af_nogle_pakker_fejler,_og_der_klages_over_manglende_X11-inkluderinger)
    *   [8.9 Ikke i stamd til at indlæse fonten '(null)'](#Ikke_i_stamd_til_at_indlæse_fonten_'(null)')
    *   [8.10 KDE opgavelinje/skrivebordsikoner ødelagt](#KDE_opgavelinje/skrivebordsikoner_ødelagt)
    *   [8.11 Opdatering fra 'testing'-version til 'extra'- (manglende filer)](#Opdatering_fra_'testing'-version_til_'extra'-_(manglende_filer))
    *   [8.12 Problemer med MIME-typer i forskellige skrivebordsmiljøer](#Problemer_med_MIME-typer_i_forskellige_skrivebordsmiljøer)
    *   [8.13 DRI virker ikke længere med Matrox-kort](#DRI_virker_ikke_længere_med_Matrox-kort)
    *   [8.14 Kan ikke starte nogen klient under 'Xephyr'](#Kan_ikke_starte_nogen_klient_under_'Xephyr')
*   [9 Links](#Links)

## Introduktion

**Xorg** er den offentlige 'open-source'-implementation af X11 X Window systemet. (Se [X.org Wikipedia Article](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server") eller [X.org](http://wiki.x.org/wiki/) for detaljer). I grunden er det sådan, at hvis du vil have en grafisk brugerflade til Arch Linux, så har du brug for Xorg.

## Installation af Xorg

Før du starter, skal du gøre flg:

1.  Sikre dig at [pacman](/index.php/Pacman "Pacman") er konfigureret og genopfrisket/synkroniseret.
2.  Hvis du kører en anden X-server, skal du stoppe den nu. `ctrl+alt+backspace`
3.  Lav nogle notater omkring tredjeparts-drivere (f.eks. nVidia eller ATI drivers).

Lad os så installere Xorg:

```
# pacman -S xorg

```

De fleste vil have muse- og tastatur-input understøttet.

```
# pacman -S xf86-input-mouse xf86-input-keyboard

```

Vi har også brug for en video-driver. Denne kommando viser en liste over alle tilgængelige video-drivere:

```
# pacman -Ss xf86-video

```

Se efter den rette driver til dit kort. Er du usikker, så installér 'vesa', men husk på dit valg, når du senere skal konfigurere 'xorg'.

```
# pacman -S xf86-video-vesa

```

Du skal også have 'startx' og 'xinit', medmindre du vil anvende en display manager såsom 'xdm', 'slim', 'kdm' or 'gdm', eller hvis du er vant til at starte X manuelt.

```
# pacman -S xorg-xinit

```

De lidt mere dovne kan kopiere denne kommando:

```
# pacman -S xorg-server xf86-input-mouse xf86-input-keyboard xf86-video-vesa xorg-xinit

```

(der var en 'xorg'-pakke, der gjorde dette, men vedligeholderen har fjernet den. Se [https://bbs.archlinux.org/viewtopic.php?id=37062](https://bbs.archlinux.org/viewtopic.php?id=37062) )

Når 'xorg' er installeret, er det tid til at lave `xorg.conf`

## Konfigurere xorg

Før du kan køre 'xorg', skal du have det konfigureret, så det kender til dit grafikkort, din skærm, din mus og dit tastatur. Der er flere måder, hvormed du kan gøre dette automatisk:

### hwd

Den måske letteste måde at få 'xorg' hurtigt op at køre, er at bruge <tt>hwd</tt>, der er et værktøj skrevet af Arch Linux fællesskabet. I grunden er det et værktøj til hardware-undersøgelse, der har flere muligheder, hvor en af dem er at sætte din X-server op. Heldigvis er dder mere strømlinet end `xorgconf` og kræver slet ingen input.

Først installeres pakken <tt>hwd</tt>:

```
# pacman -S hwd

```

Nu kører du simpelthen flg. kommando som 'root' for at generere en standard `xorg.conf`-fil:

```
# hwd -xa

```

Dette overskriver enhver eksisterende /etc/X11/xorg.conf-fil med et praktisk standardsæt, baseret på det hardware, som <tt>hwd</tt> fandt.

Alternativt, kan du generere en prøveudgave af 'xorg'-konfigurationen (/etc/X11/xorg.conf.hwd) uden at overskrive dine eksisterende indstillinger. For at gøre dette, kør <tt>hwd</tt> med flaget **-x** i stedet:

```
# hwd -x

```

For at bruge denne prøvekonfiguration, skal du manuelt omdøbe den:

```
# mv /etc/X11/xorg.conf.hwd /etc/X11/xorg.conf

```

*Tilføjelse*: Erfaringsvis opretter 'hwd' filen XF86Config-4, og Xorg bruger denne automatisk, hvis filen xorg.conf ikke eksisterer.

### xorgconfig

Start <tt>xorgconfig</tt> med:

```
# xorgconfig

```

Dette genererer en ny <tt>xorg.conf</tt>.

Besvar spørgsmålene og programmet laver filen for dig. Dette program er ikke særlig godt, men det er en begyndelse, og du kan tilføje mere specifikke ting manuelt bagefter.

### Xorg -configure

Du kan også benytte

```
# Xorg -configure

```

eller

```
# X -configure

```

### nvidia-xconfig

nVidia-brugere kan også benytte

```
# nvidia-xconfig

```

når de har de officielle nVidia-drivere [installerede](/index.php/NVIDIA "NVIDIA").

Kommentér linjen

```
Load       "type1"

```

i modulsektionen, da de seneste versioner af xorg-server ikke inkluderer font-modulet 'type1' (fuldstændigt erstattet af 'freetype').

## Redigere xorg.conf

Du vil måske redigere konfigurationen, efter den er genereret. For at åbne den i din favorit-editor - f.eks. 'vim' - skriver du (som 'root'):

```
# vim /etc/X11/xorg.conf

```

Skal du have understøttelse for musehjulet, se [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working") (Engelsk.

### Skærmindstillinger

Afhængigt af dit hardware, kan Xorg fejle, når det undersøger din skærms kapaciteter, eller du vil ganske enkelt anvende en lavere opløsning, der er lavere end kapaciteten af din skærm. Du bør referere til manualen for din skærm, for at finde de rigtige værdier for følgende indstillinger, før du sætter dem op.
Følgende indstillinger angives i sectionen 'Monitor':

#### Horizontal Sync (Horisontal synkronisering)

```
HorizSync 28-64

```

#### Refresh Rate (Genopfriskningsrate)

```
VertRefresh 60

```

Følgende angives i sektionen 'Screen':

#### Colour Depth (Farvedybe)

```
Depth 24

```

#### Resolution (Opløsning)

```
Modes "1280x1024" "1024x768" "800x600"

```

### Tastaturindstillinger

Xorg fejler måske, når det undersøger dit tastatur. Dete kan give problemer med, at dit tastatur-layout eller -model ikke bliver sat korrekt.
For at se en komplet liste over tastatur-layouts, -modeller, -varianter og -valgmuligheder, kan du åbne:

```
/usr/share/X11/xkb/rules/xorg.lst

```

#### Tastatur-layout

Benyt XkbLayout-valgmuligheden til at ændre tastatur-layout i sektionen 'InputDevice' > 'keyboard'.
For eksempel hvis du har et alm. dansk tastatur:

```
Option "XkbLayout" "da"

```

#### Tastatur-model

Benyt valgmuligheden XkbModel til at ændre tastaturmodel i sektionen 'InputDevice' > 'keyboard'.
For eksempel hvis du har et 'Microsoft trådløs multimedie tastatur:

```
Option "XkbModel" "microsoftmult"

```

### Skærmstørrelse/DPI

DPI = Dots Per Inch = pixel/tomme. For at få den rette font-størrelse skal skærmstørrelsen sættes op til den ønskede 'DPI'.
Sæt din skærms størrelse i mm. op i sektionen `"Monitor"`:

```
Section "Monitor"
   ...
 DisplaySize 336 252 # 96 DPI @ 1280x960
   ...
EndSection

```

Formelen til at beregne værdierne i 'DisplaySize' Bredde (i tommer) x 25.4 / DPI og Højde (i tommer) x 25.4 / DPI.
Hvis du kører Xorg med en opløsning på 1024x768 og ønsker en DPI på 96, anvend 1024 x 25.4 / 96 og 768 x 25.4 / 96\. Rund tallene ned.

```
# calc: (x|y)pixels * 25.4 / dpi
# DisplaySize 168 126 # 96 DPI @ 640x480
# DisplaySize 210 157 # 96 DPI @ 800x600
# DisplaySize 269 201 # 96 DPI @ 1024x768
# DisplaySize 302 227 # 96 DPI @ 1152x864
# DisplaySize 336 252 # 96 DPI @ 1280x960
# DisplaySize 336 269 # 96 DPI @ 1280x1024 (non 4:3 aspect)
# DisplaySize 370 277 # 96 DPI @ 1400x1050
# DisplaySize 420 315 # 96 DPI @ 1600x1200
# DisplaySize 506 315 # 96 DPI @ 1920x1200

```

For nVidia-drivere skal du sikkert deaktivere automatisk undersøgelse af DPI far at sætte det manuelt. Der er også en lettere måde at sætte DPI på disse kort. Den ene eller begge af de følgende linjer kan sættes i enhedssektionen for dit nVidia-kort.

```
  Option   "UseEdidDpi" "false"
  Option   "DPI" "96 x 96"

```

Resultater kan tjekkes med følgende kommando, der skulle returnere 96x96 DPI, hvis du har sat værdien 'DPI @ 96'.

```
$ xdpyinfo | grep -B1 dot

```

### Proprietære drivere

Hvis du vil bruge tredjeparts grafiske drivere, skal du først tjekke, at X-serveren kører godt. Xorg burde køre gnidningsløst uden officielle drivere, som typisk kun er nødvendige for avancerede funktioner som 3D-acceleret ydelse til spil, opsætning af to skærme og 'TV-out'. Der henvises til [nVidia-wiki (engelsk)](/index.php/NVIDIA "NVIDIA") og [Ati-wiki (Engelsk)](/index.php/ATI "ATI") for hjælp til installation af disse drivere.

### Fonte

Her er der nogle tips for indstilling af fonte: [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration").

### Eksempler på Xorg.conf-file

Enhver, der har en fungerende Xorg.conf-fil kan linke til den her, så andre kan have glæde af den.
Vær venlig IKKE at sætte hele filen ind, men upload den et andet sted og link til den her. Tak!

*   Shadowhand (nv and nvidia drivers): [http://people.os-zen.net/shadowhand/configs/xorg.conf](http://people.os-zen.net/shadowhand/configs/xorg.conf)
*   Cerebral (fglrx and radeon drivers): [http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf](http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf)
*   raskolnikov (via unichrome and synaptics drivers): [http://athanatos.free.fr/Arch/xorg.conf](http://athanatos.free.fr/Arch/xorg.conf)
*   Leigh (Three independent screens - Three nvidia cards): [http://files.myopera.com/allisonleigh/linuxbackup/xorg.conf](http://files.myopera.com/allisonleigh/linuxbackup/xorg.conf)

## Køre Xorg

Dette gøres ganske enkelt med kommandoen:

```
$ startx

```

X-miljøet som standard er noget bart, og du vil sikkert installere noget vindueshåndtering eller et skrivebordsmiljø til at suplementere X.

For at teste konfigurationsfilen, som du oprettede:

```
$ X -config *<din konfigurationsfil>*

```

Hvis der opstår et problem, kan du se loggen <tt>/var/log/Xorg.0.log</tt>. Kig efter linjer, der begynder med *(EE)*, der repræsenterer fejl, og også *(WW)* som er advarsler, der kan indikere andre problemer.

**Note:** For at benytte 'startx' skal du have en [~/.xinitrc](/index.php/Xinitrc "Xinitrc")-fil, så X ved, hvad den skal køre, når den starter.

Du kan ydermere installere 'twm' og 'xterm' med 'pacman', som vil amvendes som 'sikkerhednet', hvis ~/.xinitrc ikke eksisterer (som fastsat i /etc/X11/xinit/xinitrc).

## Finpudse opstarten af X (/usr/bin/startx)

For at se en omtale af valgmuligheder for X

```
$ man Xserver

```

Følgende valgmuligheder skal tilføjes til variablen 'defaultserverargs' i filen /usr/bin/startx.

Forhindre at X lytter på 'TCP':

```
-nolisten tcp

```

Blive fri for det gråtvævede mønster, når X starter, og lade X sætte et sort 'root'-vindue:

```
-br

```

Aktivere udsættelse af glyf-indlæsning for 16 bit fonte:

```
-deferglyphs 16

```

Bemærk: Hvis du starter X med 'KDM', eksekveres startx-script tilsyneladende ikke. Disse valgmuligheder skal vedhæftes variablen "ServerCmd" i filen /opt/kde/share/config/kdm/kdmrc.

## Ændringer med modulær Xorg

### Mest almindelige pakker

Husk at installere drivere for mus, tastatur og grafikkort. For mus og tastatur bør **xf86-input-keyboard** og **xf86-input-mouse** installeres. Andre **xf86-input-***pakker er tilgængelige for forskellige input-enheder.

For videokort, find ud af hvilken driver der kræves, og installér den rigtige **xf86-video-***pakke. ATI- og Nvidia-brugere vil måske installere de ufrie drivere for deres [nVidia-](/index.php/NVIDIA "NVIDIA") og [ATI-hardware](/index.php/ATI "ATI").

For at installere alle drivere på én gang er **xorg-input-drivers** og **xorg-video-drivers** tilgængelige.

### OpenGL 3D-acceleration

X.Org 7.0 på Arch Linux benytter et modulært design til 'mesa', OpenGL's gengivelsessystem. Flere implementationer er tilgængelige:

*   libgl-dri: Open-source DRI OpenGL implementation. Falder tilbage til software-gengivelse, når ingen DRI-driver er installeret.
*   andre der tilbyder libGL (ati, nvidia)

Når Pacman installerer et program, som behøver 'mesa', installerer det en af disse pakker. For at være sikker på hvilket bibliotek, der er det rigtige til din opsætning, installerer du biblioteket inden du installerer Xorg. Du kan også installere den rigtige pakke bagefter, selvom det somme tider kan give nogle afhængighedsfejl, hvilke kan ignoreres med flaget '-d'.

### Glxgears og Glxinfo

Disse er inkluderet i mesa-pakken.

### Ændrede søgestier (og konfiguration)

**Se her for ekstra information om opgradering af Xorg:** [https://www.archlinux.org/blog/2006/01/02/how-to-upgrade-xorg/](https://www.archlinux.org/blog/2006/01/02/how-to-upgrade-xorg/)

Modulær X.Org 7 installerer alt i `/usr`, hvor ældre versioner installerede i `/usr/X11R6`. Adskillige konfigurationsfiler kræver opdatering:

*   */etc/X11/xorg.conf*
    *   Font-søgestier er nu i /usr/share/fonts
    *   RGB-databasen er i /usr/share/X11/rgb
    *   modulsøgestien er /usr/lib/xorg/modules

Bemærk også, at nogle konfigurationsværktøjer for X måske ikke virker længere. Den nemmeste måde at konfigurere Xorg er ved at installere den rigtige driver-pakke og køre kommandoen *Xorg -configure*, hvilket giver `/root/xorg.conf.new`, som kun kræver ændringer i opløsninger, musekonfiguration og tastatur-layout.

Nogle pakker har fastkodede henvisninger til `/usr/X11R6`. Disse pakker har brug for at blive rettet. I mellemtiden, se hvilke pakker, der installerer filer i `/usr/X11R6`. Afinstallér disse og lav et symbolsk link fra `/usr` til `/usr/X11R6` og geninstallér de berørte pakker. En anden mulighed er at flytte indholdet af `/usr/X11R6` til `/usr` og lave det symbolske link.

Du kan også blot tilføje et andet modul med `ModulePath "/usr/X11R6/lib/modules"`.
Dette virker f.eks for for Nvidia 76.76.

## Fejlfinding

### Tastaturproblemer

Autogenererede xorg.conf-filer kan skabe problemer. Hvis du ikke kan gå til 'tty1' ved at holde CTRL+ALT og trykke F1, eller du ikke kan skrive €, $ eller £, tjek de følgende indgange i din /etc/X11/xorg.conf:

```
Option "XkbLayout"  "da"         #"da" er ikke et rigtigt layout. Se en liste over layouts i /usr/share/X11/xkb/symbols/.
Option "XkbRules"   "xfree86"    #dette burde være "xorg"
Option "XkbVariant" "nodeadkeys" #Denne linje er også kendt for at skabe de beskrevne problemer - prøv at udkommentere den.

```

For at skifte mellem layouts med Alt+Shift:

```
Option "XkbOptions" "grp:alt_shift_toggle,grp_led:scroll"

```

### Et hurtigt fiks for konflikten Bitstream-Vera

Hvis du får en fejlmeldingen *ttf-bitstream-vera conflicts with xorg*:

1.  Forlad pacman-sessionen ved at svare nej.
2.  Kør `pacman -Rd xorg`
3.  Kør `pacman -Syu`
4.  Kør `pacman -S xorg`
5.  Opdatér dine søgestier i /etc/X11/xorg.conf

### Et hurtigt fiks af filkonflikter i /usr/include

Hvis du ser meldinger om konflikter i /usr/include/X11 og /usr/include/GL:

1.  Kør `rm /usr/include/{GL,X11}`
2.  Kør `pacman -Su`

De symbolsk linkede mapper der fjernes med denne operation erstattes af rigtige mapper i den nye Xorg-pakke, som får disse filkonflikter til at vise sig.

### Musehjul fungerer ikke

Protokollen "Auto" ser ikke længere ud til at fungere ordentlig i Xorg 7\. I sektionen 'InputDevice' for din mus ændres flg:

```
Option         "Protocol" "auto"

```

til

```
Option         "Protocol" "IMPS/2"

```

eller

```
Option         "Protocol" "ExplorerPS/2"

```

### Ekstra museknap virker ikke

Brugere af USB-mus bør læse [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working") (Engelsk).

Intellimouse (ExplorerPS/2) -brugere finder måske, at deres rulle og sideknapper ikke opfører sig som de plejer. Tidligere xorg.conf behøvede:

```
Option      "Buttons" "7"
Option      "ZAxisMapping" "6 7"

```

for at få sideknapperne til at virke skulle brugere også køre 'xmodmap' med en kommando i stil med:

```
xmodmap -e "pointer = 1 2 3 6 7 4 5"

```

'xmodmap' kræves ikke mere. I stedet lav din xorg.conf i stil med dette:

```
Option      "Buttons" "5"
Option      "ZAxisMapping" "4 5"
Option      "ButtonMapping" "1 2 3 6 7"

```

og sideknapperne på en 7-knappers Intellimouse vil arbejde som vanligt uden at køre 'xmodmap'.

### Tastaturproblemer

Nogle tastatur-layouts er ændrede. Jeg undrede mig over flg:

*   Jeg kunne ikke skifte til konsol med Ctrl+Alt+Fx
*   Jeg kunne ikke benytte layout

Problemet var at layoutet *dk_qwerty* ikke længere eksisterer. Jeg skulle skifte

```
Option         "XkbLayout" "dk_qwerty"

```

ud med

```
Option         "XkbLayout" "dk"
Option         "XkbVariant" ",qwerty"

```

En anden ting at kigge efter, hvis dit tastatur ikke fungerer ordentligt, er valgmuligheden 'XkbRules'.
Du skal ændre

```
Option         "XkbRules" "xfree86"

```

til

```
Option         "XkbRules" "xorg"

```

#### AltGR fungerer ikke ordentligt

Hvis - efter en opdatering - tasten 'AltGr' ikke fungerer som ventet, prøv at tilføje dette til sektionen 'keyboard':

```
Option      "XkbOptions" "compose:ralt"

```

Dette er ikke den rigtige måde at aktivere tasten 'AltGr' på et tysk tastatur (f.eks. for tegnene '|' og '@' på tysk tastaturer). For at få det til at fungere igen skal du blot vælge et gyldigt tastatur som f.eks (eksemplet er for et tysk tastatur):

```
Option      "XkbLayout" "de"
Option      "XkbVariant" "nodeadkeys"

```

Løsningen ovenfor virker ikke for et italiensk tastatur. For at aktivere tasten 'AltGr' på et italiensk tastatur skal du sikre dig, at du har de følgende linjer sat rigtigt op:

```
 Driver          "kbd"
 Option          "XkbRules"      "xorg"
 Option          "XkbVariant"    ""

```

#### Kan ikke sætte 'qwerty'-layout op med kommandoen 'setxkbmap'

Efter opdateringen er der ingen 'qwerty'-layout som f.eks. 'dk_qwerty', Hvis du vil skifte dit nuværende layout ud med et 'qwerty' tastatur-layout, kan du benytte denne kommando:

```
$ setxkbmap NAVN_PÅ_LAYOUT qwerty

```

For 'dk_qwerty' skal du benytte:

```
$ setxkbmap dk qwerty

```

Jeg fik fejlmeddelelsen "Error loading new keyboard description", da jeg prøvede kommandoen erter opdateringen.
So give the permissions to that directory. Genstart X-serveren og du har dine 'deadkeys' tilbage!
Tror du det ikke? Prøv f.eks. koden 'it layout'.

```
$ setxkbmap -layout it

```

#### Opsætning af fransk-canadisk layout (gammel 'ca_enhanced)

Med Xorg7 eksisterer"ca_enhanced" ikke længere. Du skal lave et lille trik, for at få dette layout:
Skift det gamle:

```
       Option          "XkbLayout"     "ca_enhanced"

```

ud til:

```
       Option          "XkbLayout"     "ca"
       Option          "XkbVariant"    "fr"

```

Det skulle blive magen til det andet layout. Der henvises til
[http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml](http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml)

### Manglende biblioteker

*   **Hjælp! Jeg får en fejlmeddelelse, når jeg kører mit favoritprogram, der siger at "libX-et-eller-andet" ikke findes**

I de fleste tilfælde, behøver du blot at tage navnet på biblioteket (f.eks. libXau.so.1), konvertere det til små bogstaver, fjerne filendelsen og installere det med 'Pacman':

```
# pacman -S libxau

```

Dette vil installere det manglende bibliotek, og alt er godt igen!

### Bygning af nogle pakker fejler, og der klages over manglende X11-inkluderinger

Bare geninstallér pakkerne 'xproto' og 'libx11', selvom de allerede er installerede.

### Ikke i stamd til at indlæse fonten '(null)'

*   **Nogle programmer virker ikke, og siger at de ikke er i stand til at indlæse fonten `(null)'.**

Disse pakker vil gerne have nogle ekstra fonte. Nogle programmer virker kun med bitmap-fonte. Der er to større pakker med bitmap-fonte tilgængelige - 'xorg-fonts-75dpi' og 'xorg-fonts-100dpi'. Du behøver ikke begge - en skulle være tilstrækkelig. For at finde ud af, hvilken er den bedste i dit tilfælde, prøv dette:

```
$ xdpyinfo | grep resolution

```

Og hent den, der er nærmest dit behov (75 eller 100 i stedet for 'XX')

```
# pacman -S xorg-fonts-XXdpi

```

### KDE opgavelinje/skrivebordsikoner ødelagt

*   **KDE opgavelinje virker ikke, og skrivebordsikoner forsvinder**

Installér pakkerne 'libxcomposite' og 'libxss'. Så virker det.

```
# pacman -S libxcomposite libxss

```

### Opdatering fra 'testing'-version til 'extra'- (manglende filer)

Hvis du har opdateret fra 'Xorg 7' i 'testing' til 'Xorg 7' i 'current', og du finder, at mange filer tilsyneladende mangler (inklusiv startx, /usr/share/X11/rgb.txt og andre), har du sikkert mistet mange filer, fordi pakken 'xorg-clients' er delt op fra en enkelt pakke til mange mindre underpakker.
Du er nødt til at geninstallere alle de pakker, som er afhængigheder af 'xorg-clients':

```
# pacman -S xorg-apps xorg-font-utils xorg-res-utils xorg-server-utils \
          xorg-twm xorg-utils xorg-xauth xorg-xdm xorg-xfs xorg-xfwp \
          xorg-xinit xorg-xkb-utils xorg-xsm

```

Det skulle løse problemet.

### Problemer med MIME-typer i forskellige skrivebordsmiljøer

Hvis du har bemærket, at der mangler ikoner, og du ikke kan åbne filer med museklik i skrivebordsmiljøer, skal du tilføje følgende linjer til /etc/profile eller dit foretrukne 'init-script' og genstarte.

```
XDG_DATA_DIRS=$XDG_DATA_DIRS:/usr/share
export XDG_DATA_DIRS

```

### DRI virker ikke længere med Matrox-kort

Hvis du anvender et Matrox-kort, og DRI ikke virker efter en opgradering til 'Xorg 7', prøv at tilføje linjen

```
Option "OldDmaInit" "On"

```

til 'Device'-sektionen, der henviser til videokortet i 'xorg.conf'.

### Kan ikke starte nogen klient under 'Xephyr'

Klientforbindelserne afvises af X-serverens sikkerhedsmekanisme, du kan finde en komplet forklaring og en løsning på
[http://wiki.debian.org/XStrikeForce/FAQ#howtoxnest](http://wiki.debian.org/XStrikeForce/FAQ#howtoxnest)

## Links

Se også:

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")
*   [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration")
*   Proprietary Video Drivers
    *   [ATI](/index.php/ATI "ATI")
    *   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
    *   [KDE](/index.php/KDE "KDE")
    *   [GNOME](/index.php/GNOME "GNOME")
    *   [Xfce](/index.php/Xfce "Xfce")
    *   [Enlightenment](/index.php/Enlightenment "Enlightenment")
    *   [Fluxbox](/index.php/Fluxbox "Fluxbox")

Eksterne links:

*   [X.org Wikipedia Article](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server")
*   [http://wiki.x.org/wiki/](http://wiki.x.org/wiki/)