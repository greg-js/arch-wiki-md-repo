## Contents

*   [1 Introduktion](#Introduktion)
*   [2 Strukturen](#Strukturen)
    *   [2.1 mythbackend](#mythbackend)
    *   [2.2 mythfrontend](#mythfrontend)
*   [3 Requirements](#Requirements)
*   [4 Igang med projektet](#Igang_med_projektet)
*   [5 Installing MythTV](#Installing_MythTV)
    *   [5.1 Backend setup](#Backend_setup)
*   [6 Frontend setup](#Frontend_setup)
    *   [6.1 Nvidia XvMC Setup](#Nvidia_XvMC_Setup)
*   [7 MythTV Plugins](#MythTV_Plugins)
    *   [7.1 MythWeb](#MythWeb)
    *   [7.2 Mythweather](#Mythweather)
*   [8 Miljø variabler](#Milj.C3.B8_variabler)
*   [9 Tricks til et stabilt MythTV System](#Tricks_til_et_stabilt_MythTV_System)
    *   [9.1 Brug GDM til automatisk login](#Brug_GDM_til_automatisk_login)
*   [10 References](#References)

## Introduktion

MythTV er en samlet applikation, designet til levere fantastiske multimedie oplevelser. Det leverer PVR-funktionen(Personal Video Recorder) til en linux baseret PC og supporterer også andre medietyper - såsom Xbox, IPhone og Windowsmobile. Kombineret med en stille Computer(Støjsvag) og et ordentligt TV - giver det et fantastisk alternativ til en hjemmebiograf.

## Strukturen

MythTV systemet er delt op i 2dele - 1 backend og frontend, hvor hver komponent har sine egne funktioner:

### mythbackend

*   Planlæg og optager TV, samt afspille LiveTV
*   Streame video data til frontends
*   Markerer reklamepause
*   Transcode videor fra det ene format til et andet

### mythfrontend

*   leverer en flot GUI
*   Afspiller optaget indhold
*   Leverer et interface til at planlægge optagelser

Frontend og Backend kan både være på seperate maskiner i et netværk, men der kan også være flere frontends på samme system. Arkitekturen tillader nemlig en central distribuering af medier der kan nå alle steder et netværk også kan. Det er et usædvanligt flexibelt system, som også muliggør meget små strømbesparende maskiner som de perfekte frontends.

## Requirements

MythTV er et meget skalerbart system som kan udvides på utallige måder. Med et standard TV og ren MPEG2 encoding og decoding og med hardware acceleration og et meget begrænset system kan faktisk agere både frontend og backend på system. Jamen hvor begrænset ??????? Nogle mennesker rapporterer omkring at have fået det til at fungere på systemer uden blæser såsom VIA fanless og et hauppauge PVR-kort.Imens er det ikke alle der anbefaler et så "let" system til dette - så kan det trodsalt lade sig gøre.

I den anden ende af skalaen High Defination TV med MPEG4 transcoding(HDTV) med reklamepause markering - kan kræve enorme hestekræfter.De fleste mennesker in HD-verdenen ville bruge highend Athlon XPs, mellem eller kvalitetsCPU, såsom Athlon64 og Pentium4 for deres backends.imens frontends kan klare sig med meget mindre hvis XvMC afspilningsacceleration er brugt på disse.

Alle systemer SKAL have et tunerkort. Hauppauge's PVR serie (PVR150, PVR250, PVR350 og PVR500) er meget populære, på grund af deres gode linuxsupportering af hardwaren og ikke mindst på deres lille CPU-forbrug. Andre kort - baseret på BT878chipset er også brugt i denne sammenhæng, men ligeså gode som Hauppauge's kort er det ikke pga et større CPU forbrug, eftersom disse korts output er rå frames og ikke en komprimeret streaming.

Der er mange forskellige opsætninger og meninger omkring dette - så derfor er denne wiki også lavet for at alle kan give et besyv med

## Igang med projektet

For at kunne installere MythTV på dit system, skal du have et kørende Linux installation. Da dette er Arch Linux Webside, denne artikel er skrevet efter denne distro, - nemlig et simpelt base system, uden nogle extra detaljer eller krav til installationen.

På selve Backend-maskinen, er det en god ide at have sat [LAMP](/index.php/LAMP "LAMP") op så man har en Apacheserver kørende med tilhørende PHP og MySQL, således at det er muligt at bruige en webbrowser til at planlægge optagelser. Det er dog ikke nødvendigt, men extremt brugbart i alle hensigter.

En fungerende [Xorg](/index.php/Xorg "Xorg") (grafisk) miljø er en nødvendighed .

## Installing MythTV

Der er en pakke med MythTV i *Extra* repoet.

*   Installer MythTV pakken:

```
  # pacman -S mythtv

```

*   Hvis du får en fejl med libXvMCW.so.1 shared library error, installer følgende pakke:

```
  # pacman -S libxvmc

```

Nu skulle du gerne have en fungerende MythTV installation. Det skal herefter defineres som frontend/Backend eller begge.

### Backend setup

Inden du konfigurerer din backend, vær sikker på du har et FUNGERENDE TV-kort installeret enten som USB,Firewire eller PCI. Desværre er denne del af installationen udenfor området som denne artikel dækker, men kig under de eneklte specielle install-guides omkring hvorsdan dit kort skal installeres. Det ville også være praktisk at have en Yahoo konto eller lign, for senere brug vedrørende XMLTV og grabning af programlister - mm du vil bruge den EIT der bliver sendt sammen med kanalerne.

*Installering af MySQL databasen:*

*   Installer og kør MySQL

```
  # pacman -S mysql
  # /etc/rc.d/mysqld start

```

*   Tilføj mysqld til "daemons" linen i /etc/rc.conf.

*   Importer database strukturen:

```
  # mysql -u root -p < /usr/share/mythtv/mc.sql

```

*Opsætning af master backend:*

*   Start X, hvis ikke du allerede har gjort dette:

```
  # startx

```

*   Åbn xterm eller en anden GUI terminal af eget valg:
*   Kør mythtv-setup programmet

```
  # mythtv-setup

```

*   **General menu**

Hvis dette er din masterbackend, put din IP adresse i første og fjerde felt, identificerer denne Computer som din masterbackend, og giver den sin IP-adresse på netværket.
På næste side, indtast stien til hvor du vil lægge dine optagelser og LiveTV. LVM eller RAID løsninger leverer nemt tilgængelig større skalerbare opbevaringspladser. Men igen, dette er udenfor denne artikel's område. Set din TV-buffer til en størrelse du kan håndtere og lad resten være som det er.
På næste side, indstil dit lokale sprog til dansk, og vær sikker på om det er kabeltv,satelit eller analog signal.
På de næste 2sider, efterlad alt som default, mm du er sikker på du vil ændre dette. På næste side, hvis du har en hurtig backend, som kan håndtere optagelser og mærkningsjob samtidigt, er det anbefalet at sætte CPU-forbruget til højt, sætte antallet af maximale job samtidigt til 2, og tjekke reklamemærkningsopsætningen.
på den sidste side, sæt automatisk reklamemærkning er anbefalesværdigt. Ignorer den sidste suide og afslut.

*   **Capture card menu**

Vælg dit TV-kort fra dropdown menuen, Hauppauge PVR brugere skal vælge MPEG2 encoder kortmuligheden.
Peg mythtv-setup hen til den rigtige sti - som regel /dev/v4l/video0

*   **Video sources menu**

Det er her det begynder at blive vigtigt at have diverse sources til TV-liste. Da vi i DK ikke bruger dataDirect skal man ikke tænke over dette. Man kan enten vælge at bruge EIT - eller xmlTV. XMLTV er forkaret under artikler til MythTV.

*   **Input connections menu**

Denne menu er ret sigende. Alt du behøver at gøre er - at vælge et input card og fortælle MythTV hvilkkenm inputkilde den er koblet til. De fleste brugere vil vælge deres tunere og lade alle andre input være. Satelitbrugere ville skulle vælge en videokilde og derefter indstille hvordan der skiftes kanaler mm på den næste side. Dette er dog igen udenfor denne artikels område.

*   **Channel editor menu**

Denne menu er muligt at ignorer

*   Forlad programmet (Esc)

*   kør mythfilldatabase

```
  # mythfilldatabase

```

Dette skulle meget gerne fylde din MySQL database med diverse informationer omkring den næste uges TV-programmer.

*   Tilføj mythbackend til /etc/rc.conf "daemons" linien. *Hvis du ikke kan starte mythbackend - tilføj HOME="/root" i toppen af /etc/rc.conf under variablerne.*

*   Genstart maskinen

```
  # reboot

```

Selvom det ikke er absolut nødvendigt at genstarte maskinen på dette punkt. Det er bare en god ide at tjekke om alting starter som det skal og systemet fungerer.

## Frontend setup

Sammenlignet med at sætte backend op og køre - er det at installere frontenden absolut nemmere. Bare sikre dig at du har et fungerende X-miljø, og log ind som almindelig bruger og kør mythfrontend fra kommandolinien. Det vil komme op med en menu hvor den spørger omkring IP-adressen på Backendserveren og lokalmaskinen. Udfyld disse informationer og din frointend skulle meget gerne fungere nu. på den anden side, frontend maskinen har flere valgmuligheder end en ny luksusbil. Alle disse indstillinger er i en artikel for sig selv.

Dog er det en god ide at tjekke indstillingerne for Alsa i general settings, for der er lige så mange løsninger som der er lydkort - så undersøg selv lidt nærmere omkring hvordan du får dit kort til at virke her.

### Nvidia XvMC Setup

Udfra vurderingen at du har installeret de propertiære Nvidia drivere fra pacman, er du nødt til at gøre følgende

 `echo "libXvMCNVIDIA_dynamic.so.1" > /etc/X11/XvMCConfig ` 

Dette vil tillade Mythfrontend til at bruge XvMC variablen til accelleration - genstart mythfrontend.

## MythTV Plugins

Der er utallige forskellige plugins, der er tilgængelige for MythTV, og de vil blive installeret hvis man ønsker dette? Jeg vil klart anbefale dette også for at få mere ud af dit eget mediecenter.

### MythWeb

[MythWeb](/index.php/MythWeb "MythWeb") er et Webinterface til MythTV. Instruktioner for installering af mythweb på Arch Linux, kan findes i [MythWeb](/index.php/MythWeb "MythWeb") artiklen.

### Mythweather

Fra 7-10-08 Mythweather er ødelagt i extra Extra

extra/mythweather 0.21-1 (mythtv-extras)

## Miljø variabler

Jeg har flere gange set en MythTV installation fejlæe pga følgende error: `Cannot locate your home directory. Please set the environment variable HOME or MYTHCONFDIR`

Så jeg har gjort følgende som root: `mkdir /home/mythtv ; cp /home/(myusername)/.lircrc /home/mythtv/ ; chown -R (myusername):users /home/mythtv`

Og putte følgende i /etc/rc.conf `MYTHCONFDIR=/home/mythtv`

## Tricks til et stabilt MythTV System

*   Kør ntpd eller openntpd på din backend for at sikre dig den rigtige tid hver gang.
*   [LIRC](/index.php/Lirc "Lirc") på din frontend tillader at du kan bruge en fjerntbetjening til dit MythTV system.
*   Brug gdm,kdm eller xdm for automatisk indlogning på systemet.og derefter brug .xinetrc til at starte mythfrontend hver gang.
*   Indstil "mythfilldatabase" til at køre automatisk på en af dine frontends for at sikre dig du har info fra kanalerne
*   Glem ikke at bruge verbose og logningsparametrene - så du kan se hvornår tingene fejler og ikke fungerer korrekt i myhtbackend
*   Kør IKKE din frontend som root! Opret en ny MythTV bruger.

### Brug GDM til automatisk login

[Display manager](/index.php/Display_manager "Display manager")

I din /etc/gdm/custom.conf tilføj følgende argumentunder [daemon] headings, add the following statements under the [daemon] heading:

```
AutomaticLoginEnable=true
AutomaticLogin=mythtv (assuming your frontend user is mythtv)
```

FYI - GDM vil IKKE logge root iond i grafisk miljø.

## References

*   [http://www.mythtv.org](http://www.mythtv.org)
*   [http://mythtv.info](http://mythtv.info)
*   [http://wilsonet.com/mythtv/fcmyth.php](http://wilsonet.com/mythtv/fcmyth.php)
*   [http://niels.dybdahl.dk/xmltvdk/index.php/Forside](http://niels.dybdahl.dk/xmltvdk/index.php/Forside)