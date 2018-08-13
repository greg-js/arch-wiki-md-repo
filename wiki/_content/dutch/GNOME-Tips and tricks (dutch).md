## Contents

*   [1 Tips voor de configuratie](#Tips_voor_de_configuratie)
    *   [1.1 Betere video prestatie](#Betere_video_prestatie)
    *   [1.2 Een sessie aan GDM toevoegen of wijzingen](#Een_sessie_aan_GDM_toevoegen_of_wijzingen)
*   [2 Overigetips](#Overigetips)
    *   [2.1 Schermbeveiliging](#Schermbeveiliging)
    *   [2.2 GNOME Files Tips](#GNOME_Files_Tips)
*   [3 Bruikbare toevoegingen](#Bruikbare_toevoegingen)
    *   [3.1 FAM](#FAM)
    *   [3.2 GNOME system monitor](#GNOME_system_monitor)
*   [4 Nog enkele nuttige pakketen](#Nog_enkele_nuttige_pakketen)
    *   [4.1 Gnome-terminal](#Gnome-terminal)
    *   [4.2 Gedit](#Gedit)
    *   [4.3 eog](#eog)
    *   [4.4 file-roller](#file-roller)
    *   [4.5 gcalctool](#gcalctool)
    *   [4.6 rhythmbox](#rhythmbox)
    *   [4.7 totem](#totem)
    *   [4.8 Gimp](#Gimp)
    *   [4.9 gftp](#gftp)
    *   [4.10 Abiword](#Abiword)
    *   [4.11 gnumeric](#gnumeric)
*   [5 Bekijk ook](#Bekijk_ook)

## Tips voor de configuratie

### Betere video prestatie

Dit is alleen computers die niet beschikken over een hele goede videokaart. Als je het venster waar je een film op kijkt verplaatst dan kan er een blauwe rand verschijnen. Dit probleem is optelossen, door te gaan naar multimediasysteem selecteren te gaan die vind u in het menu Werkplek-->> Voorkeuren.

Als het venster van multimediasysteem selecteren is verschenen, klik dan op video. Kies bij standaart uitvoer voor Xwindow system noXv.

Uw videoprestaties zouden nu beter moeten zijn.

### Een sessie aan GDM toevoegen of wijzingen

Het configuratiebestand van GDM is /opt/gnome/etc/gdm/gdm.conf Het bestand verwijst naar de map /etc/X11/sessions waar de desktop en vensterbeheerporgramma's worden aangegeven. Het staat opgeslagen in *.desktop bestanden.

**Het toevoegen van een nieuwe sessie** Maak gebruik van een bestaand .desktop om een nieuwe aan te maken.

```
cd /etc/X11/sessions
enlightenment.desktop voorbeeld.desktop 

```

Pas het bestand aan naar het vensterbeheer programma.

Ga vervolgens terug naar GDM en de nieuwe sessie zal er tussen staan.

## Overigetips

### Schermbeveiliging

1.  Het installeren van xscreenserver. Voer het volgende commando uit

in een terminal programma:

 ` pacman -S xscreensaver` 

1.  U opent xscreensaver door te klikken op schermbeveiliging. U vind schermbeveiliging in het menu werkplek,voorkeuren.
2.  Makkeer vervolgens welke filmpje(s) uit wilt gebruiken voor uw schermbeveiling
3.  Als u een tijdje de computer laat aanstaan zonder dat er wat gebeurd op scherm. Zal de schermbeveiling zich laden en moet u opnieuw inloggen om het te stoppen.

### GNOME Files Tips

**Sneller naar een andere map** Sneller naar een andere map. Door de toetsencombinatie: control + L Kunt u meteen aangeven naar welke map u wilt.

**Werkbalken activeren en deactiveren**

1.  Open het menu Toepassingen,Systeemgereedschap en kies voor Gconf-editor.
2.  Blader vervolgens naar apps,nautilus, preference. Klik op use_always_browser.

Kies voor waar als u de werkbalken wilt activeren klik op deactiveren als u de werkblaken wilt sluiten.

## Bruikbare toevoegingen

### FAM

FAM zorgt ervoor dat het menu direct wordt aangepast als u nieuwe toepassingen heeft geinstalleerd. Ook zorgt FAM ervoor dat GNOME Files direct herlaad als er een map wordt aangepast. Bekijk het Engelstalig artikel voor het installeren van FAM: [FAM Wiki](/index.php/FAM "FAM")

### GNOME system monitor

GNOME system monitor kunt u zien hoeveel processor snelheid en werkgeheugen een draaien programma gebruikt. GNOME system monitor is standaart niet geinstalleerd u kunt het installeren door het commando:

```
pacman -S  gnome-system-monitor

```

intevoeren in een terminal programma.

## Nog enkele nuttige pakketen

U kunt de onderstaande pakketen installeren met slechts een commando:

 ` packman -S gnome-extra` 

### Gnome-terminal

Het standaart terminal programma van GNOME. Opmerking: u kunt het standaart terminal programma wijzingen door te bladeren naar: Werkplek,Voorkeuren, Standaardtoepassingen

### Gedit

De teksteditor van GNOME. Het bied o.a tekskleuring van scripts.

### eog

Eye of GNOME hiermee kunt u foto's bekijken,de grote aanpassen en foto's roteren.

### file-roller

Het archief programma voor GNOME. Handig voor het uit- en inpakken van pakketen. Het verschillende bestandsformaten. Het is aanbevolen om unrar en unzip te installeren.

### gcalctool

Een rekenmachine.

### rhythmbox

Lijkt erg op itunes van Mac. Hiermee kunt u muziekafspelen en ordenen.

### totem

Een filmafspeler wat gebruikt maakt van gstreamer

### Gimp

Een fotobewerkingsprogramma. Sterk aanbevolen voor iedereen die werkt met plaatjes,animaties en foto's.

### gftp

Een klein Gtk+ ftp-programma.

### Abiword

Een tekstverwerker die o.a het Word document formaat ondersteunt.

### gnumeric

Een spreadsheet programma

## Bekijk ook

*   [GNOME](/index.php/GNOME "GNOME")
*   [GNOME (Nederlands)](/index.php/GNOME_(Nederlands) "GNOME (Nederlands)")
*   [Gnome Menu tweaking](/index.php/Gnome_Menu_tweaking "Gnome Menu tweaking")
*   [Gnome Custom Menu Icon](/index.php/Gnome_Custom_Menu_Icon "Gnome Custom Menu Icon")