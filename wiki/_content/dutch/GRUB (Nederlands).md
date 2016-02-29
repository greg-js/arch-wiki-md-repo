| **Summary**  |
| Beslaat diverse aspecten van Arch Linux's standaard bootloader, GRand Unified Bootloader (GRUB). |
| **Gerelateerde artikelen** |
| [GRUB2](/index.php/GRUB2 "GRUB2") |
| [grub-gfx](/index.php/Grub-gfx "Grub-gfx") |
| [LILO](/index.php/LILO "LILO") |
| [MBR](/index.php/MBR "MBR") |

[GNU GRUB (Legacy)](https://www.gnu.org/software/grub/grub-legacy.en.html) is een [multiboot](http://www.gnu.org/software/grub/manual/multiboot/) bootloader onderhouden door het [GNU Project](/index.php/GNU_Project "GNU Project"). Het is een afgeleide van the GRand Unified Bootloader, dewelke origineel ontworpen en geimplementeerd werd door Erich Stefan Boleyn.

Kort samengevat is de *bootloader* het eerste software programma dat wordt aangesproken wanneer de computer start. Het is verantwoordelijk voor het laden en transferen van de controle naar de linux kernel. De kernel op zijn beurt initialiseert de rest van het besturingssysteem.

**Note:** GRUB Legacy is al een tijdje afgeschaft en vervangen door [GRUB2](/index.php/GRUB2 "GRUB2") in vele Linux distributies. Voor het booten van meerdere distributies is het beter om GRUB2 te gebruiken. Gebruikers worden in het algemeen aangeraden om naar [GRUB2](/index.php/GRUB2 "GRUB2") of [Syslinux](/index.php/Syslinux "Syslinux") over te stappen.

**Note:** Het [grub](https://www.archlinux.org/packages/?name=grub) pakket ondersteund geen [GPT](/index.php/GPT "GPT") schijven, BTRFS bestandssysteem en [UEFI](/index.php/UEFI "UEFI") firmware.

## Contents

*   [1 GRUB installeren](#GRUB_installeren)
*   [2 Grub installeren or recoveren naar het Master Boot Record](#Grub_installeren_or_recoveren_naar_het_Master_Boot_Record)
*   [3 Boot loader configuratie](#Boot_loader_configuratie)
    *   [3.1 Dual booting](#Dual_booting)
        *   [3.1.1 Dual booting met Windows](#Dual_booting_met_Windows)
        *   [3.1.2 Dual booting met Windows op een andere hardeschijf](#Dual_booting_met_Windows_op_een_andere_hardeschijf)
        *   [3.1.3 Dual booten met andere Linux distributies](#Dual_booten_met_andere_Linux_distributies)
        *   [3.1.4 Dual booten met andere Linux distributies (Chainloading)](#Dual_booten_met_andere_Linux_distributies_.28Chainloading.29)
    *   [3.2 Tips en truuks](#Tips_en_truuks)
        *   [3.2.1 Herstarten met specifieke bootkeuze](#Herstarten_met_specifieke_bootkeuze)
*   [4 LiLO en GRUB interactie](#LiLO_en_GRUB_interactie)
*   [5 Framebuffer Resolutie](#Framebuffer_Resolutie)
    *   [5.1 Hoe de correcte code te vinden voor je gewenste resolutie](#Hoe_de_correcte_code_te_vinden_voor_je_gewenste_resolutie)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 GRUB error 15](#GRUB_error_15)
    *   [6.2 Reboot uitklapmenu in KDE heeft geen effect](#Reboot_uitklapmenu_in_KDE_heeft_geen_effect)
*   [7 Externe bronnen](#Externe_bronnen)

## GRUB installeren

Installeer Grub met:

```
pacman -S grub

```

Wijzig het bestand menu.lst naar gelang je wensen:

```
nano /boot/grub/menu.lst

```

*Opmerking: Gebruik hd[a-z] voor ide en sd[a-z] voor scsi en sata*

Hier is mijn menu.lst als voorbeeld:

```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/menu.lst

# DEVICE NAME CONVERSIONS 
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,1)
#  /dev/sda3       (hd0,2)
#

#  FRAMEBUFFER RESOLUTION SETTINGS
#     +-------------------------------------------------+
#          | 640x480    800x600    1024x768   1280x1024
#      ----+--------------------------------------------
#      256 | 0x301=769  0x303=771  0x305=773   0x307=775
#      32K | 0x310=784  0x313=787  0x316=790   0x319=793
#      64K | 0x311=785  0x314=788  0x317=791   0x31A=794
#      16M | 0x312=786  0x315=789  0x318=792   0x31B=795
#     +-------------------------------------------------+

# general configuration:
timeout   5
default   1
color light-blue/black light-cyan/blue

# boot sections follow
# each is implicitly numbered from 1 in the order of appearance below
#
# TIP: If you want a 1024x768 framebuffer, add "vga=773" to your kernel line.
#
#-*

# (0) Arch Linux
title  Arch Linux  [cpio]
root   (hd0,0)
kernel /boot/vmlinuz26 root=/dev/sda6 ro vga=773
initrd /boot/kernel26.img

title  Arch Linux  [thinkpad]
root   (hd0,0)
kernel /boot/vmlinuz26thinkpad root=/dev/sda6 ro video=vesafb:off acpi_sleep=s3_bios
resume=swap:/dev/sda5
initrd /boot/kernel26thinkpad.img

```

Kopier de aanhechtingspunten naar mtab:

```
grep -v rootfs /proc/mounts > /etc/mtab

```

## Grub installeren or recoveren naar het Master Boot Record

GRUB kan worden geinstalleerd vanaf een Live omgeving, of direct vanuit een draaiende Arch Linux installatie.

In beide gevallen start je het systeem op en voer je het **grub** commando uit als root:

```
# grub

```

Grub moet weten waar zijn bestanden zijn op het systeem, aangezien er meerdere instanties van kunnen bestaan. De grub bestanden verblijven in /boot, welke een aparte partitie kan zijn. Als je weet waar /boot is, specificeer dit dan met het **root** commando, zoals hieronder:

```
grub> root (hdx,x)

```

(onthoud dat /boot GRUB's root is)

Als je niet weet wat de locatie van /boot is, gebruik dan het **find** commando, om de GRUB bestanden te lokaliseren.

Het volgende voorbeeld is voor systemen *zonder* een aparte /boot partitie, waar /boot slechts een map is onder / :

```
grub> find /boot/grub/stage1

```

Het volgende voorbeeld is voor systemen *met* een aparte partitie voor /boot:

```
grub> find /grub/stage1

```

Grub zal het bestand vinden, en een uitvoer geven die de locatie toont van het stage1 bestand, hetwelke verblijft onder /boot. Bijvoorbeeld:

```
(hd1,0)

```

Gebruik het root commando (met de uitvoer van het find commando) om GRUB te vertellen welke partitie stage1 bevat (en dus /boot):

```
grub> root (hd1,0)

```

Uiteindelijk (her)installeer je GRUB naar het MBR van de hardeschijf. Het volgende voorbeeld installeert GRUB naar het MBR van de hardeschijf die /boot bevat:

```
grub> setup (hd1)

```

Gebruik het **quit** commando om GRUB te sluiten:

```
grub> quit

```

*   Alternatief, het installeren naar een partitie.

Je kunt GRUB natuurlijk overal installeren waar je wilt.

Bijvoorbeeld:

```
grub> setup (hd1,0) 

```

zal GRUB installeren op de eerste partitie van de tweede hardeschijf.

## Boot loader configuratie

De configuratie van GRUB geschied in dit bestand:

```
/boot/grub/menu.lst

```

*   *(hdn,m)* is de partitie m op hardeschijf n, nummers startend bij 0
*   *splashimage (hdn,m)/grub/Name.xpm.gz* is het splash-image bestand
*   *default n* is de standaard boot regel, die gekozen wordt na de time-out voor gebruikersinteractie
*   *timeout m* tijd m in seconden om te wachten voor gebruikersinteractie, voordat de standaard regel wordt opgestart
*   *password -md5 str* versleutelde opstartwachtwoord 'str'
*   *title str* titel 'str' voor een boot regel
*   *root (hdn,m)* basispartitie, waar de kernel is opgeslagen
*   *kernel /path ro root=/dev/device initrd /initrd.img* gebruik de root optie, als de kernel niet in / is geplaatst
*   *makeactive
    chainloader +1* activeert root en geeft de bootprocedure door aan de boatloader (bijvoorbeeld voor Windows)
*   *map (hd0) (hd1)
    map (hd1) (hd0)* verwisseld de primaire en secondaire disk voor een boot, nodig om Windows van een tweede schijf te booten
*   *root (hdn,m,z)
    kernel /boot/loader* boots de FreeBSD-partitie x
*   *default saved* onthoud elke boot-selectie en maak het de nieuwe standaard. Zet "savedefault" aan het eind van elke bootselectie, waarvoor je deze feature wilt gebruiken.

Voor degenen die van eye-candy houden, is er [Graphical GRUB](/index.php/Graphical_GRUB "Graphical GRUB").

### Dual booting

Dit zijn de twee meest gangbare manieren om het menu.lst bestand te configureren.

#### Dual booting met Windows

Voeg het volgende toe aan het eind van je /boot/grub/menu.lst. Dit neemt aan dat [s/h]da2 je Windows-partitie is.

```
# (2) Windows XP
title Windows XP
rootnoverify (hd0,1)
makeactive
chainloader +1

```

Merk op, dat hoewel het vaak wordt angenomen als waarheid, Windows 2000 en later niet op de eerste partitie hoeven te staan, om te worden opgestart. Als de Windows-partitie van nummer veranderd (bijvoorbeeld na het toevoegen van een partitie voor de Windows partitie), zul je het Windows-bestand boot.ini moeten wijzigen, om de veranderingen door te voeren (zie [dit artikel](http://vlaurie.com/computers2/Articles/bootini.htm) voor meer details.

#### Dual booting met Windows op een andere hardeschijf

Voeg dit toe aan het eind van je /boot/grub/menu.lst. Dit neemt aan dat [s/h]da2 je Windows-partitie is.

```
# (2) Windows XP
title Windows XP
map (hd0) (hd1)
map (hd1) (hd0)
rootnoverify (hd1,0)
makeactive
chainloader +1

```

De map functie houdt je Windows installatie voor de gek en laat het denken dat de tweede hardeschijf de eerste hardeschijf is.

#### Dual booten met andere Linux distributies

Dit wordt op exact dezelfde manier gedaan als Arch Linux wordt geladen. Hier nemen we aan dat de andere distributie zich op partitie [s/h]da3 bevind.

```
title Other Linux
root (hd0,2)
kernel /boot/vmlinuz (add other options here as required)
initrd /boot/initrd.img (if the other kernel uses/needs one)

```

#### Dual booten met andere Linux distributies (Chainloading)

Om een *onderhoud nachtmerrie* te voorkomen, zou je de GRUB bootloader mischien willen chainloaden naar een andere bootloader, die je zou kunnen hebben geinstalleerd in het bootrecord van een partitie [ (hd0,2) in ons voorbeeld] in plaats van het MBR. Op deze manier zullen de automatische procedures van de een of andere distributie het menu.lst bestand op [hd0,2] beheren (indien het GRUB is) voor zichzelf, en zul jij met alle benodigde opties booten in je eigen distributie.

In ons voorbeeld [[1]](http://home.tele2.fr/solsTiCe/img/dualbooting.png) is GRUB in het MBR en een andere bootloader (BL) (bijvoorbeeld GRUB of LiLo) is in het Boot Record van (hd0,2).

```
-------------------------------------------------
|   |           |           |    %   (hd0,2)     |
| M |           |           | B  %               |
| B |  (hd0,0)  |  (hd0,1)  | L  %  Other        |
| R |           |           |    %  Distro       |
|   |           |           |    %               |
-------------------------------------------------
  |                            ^
  |     chainloading           |
  -----------------------------

```

Dan gebruik je in menu.lst:

```
title Other Linux distro
root (hd0,2)
chainloader +1

```

Dit werkt uiteraard ook andersom, in andere woorden, als je Arch root in (hd0,2)/sda2 is en je kiest ervoor om Arch's GRUB daar te installeren, in plaats van in het MBR, omdat je daar al een andere distributie had geinstalleerd.

### Tips en truuks

#### Herstarten met specifieke bootkeuze

Als je je realiseert dat je moet overschakelen naar een ander niet-standaard besturingssysteem (Windows), dan is het herstarten en wachten voor het GRUB menu soms een langdurig proces. GRUB biedt een makkelijke manier aan, om de keuze van je besturingssysteem op te slaan bij het herstarten, zonder te hoeven wachten op het menu, door simpelweg een tijdelijke nieuwe standaard regel toe te wijzen, die wordt gereset naar de vorige standaardinstelling na gebruik.

Als voorbeeld nemen we een simpele menu.lst als deze:

```
# general configuration:
timeout   10
default 0
color light-blue/black light-cyan/blue

# (0) Arch
title  Arch Linux
root   (hd0,1)
kernel /boot/vmlinuz26 root=/dev/disk/by-uuid/a29113d7-2204-49e9-be69-d94699eba466 ro
initrd /boot/kernel26.img

# (1) Windows
title Microsoft Windows XP Pro
rootnoverify (hd0,0)
makeactive
chainloader +1

```

Arch is de standaard (0). We willen herstarten in Windows. Verander default naar saved ("default saved") - dit zal de huidige standaard bewaren in een 'default' bestand in de GRUB mapp, wanneer het 'savedefault' grub commando wordt gebruikt. Voeg nu de regel "savedefault 0" toe onderaan de Windows regel. Wanneer Windows wordt opgestart, zal het Arch resetten naar de standaard, waardoor het wijzigen van de standaardinstelling naar Windows tijdelijk wordt.

Het enige wat we nu nodig hebben, is een manier om de standaardinstelling makkelijk 'handmatig' te kunnen wijzigen. Dit kan worden bereikt met het commando 'grub-set-default [nummer van regel (startend bij 0)]. Dus, om te herstarten in Windows, voer je het volgende commando uit:

```
 sudo grub-set-default 1 && sudo shutdown -r now

```

Voor gebruiksgemak zou je de "[Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown") oplossing" kunnen implementeren (inclusief /sbin/grub-set-default onder de commando's die de gebruiker kan uitvoeren zonder een wachtwoord in te typen).

## LiLO en GRUB interactie

Als je ooit [LILO](/index.php/LILO "LILO") gebruikte, vergeet dan niet om het te verwijderen met:

```
pacman -R lilo

```

omdat sommige taken (bijvoorbeeld een kernel compilatie met `make all`) een lilo call zullen maken, waardoor lilo wordt geinstalleerd over GRUB. Let op dat dit LiLo niet zal verwijderen van het MBR. Het MBR wordt pas overschreven als je een andere bootloader installeert.

## Framebuffer Resolutie

Je kunt de resoluties gebruiken, die in het menu.lst bestand van [GRUB](/index.php/GRUB "GRUB") staan. Je zult echter liever je LCD wide-screen op zijn eigenlijke resolutie willen gebruiken. Hier is wat je kunt doen om dit te bereiken:

Op [wikipedia](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions#Linux_video_mode_numbers "wikipedia:VESA BIOS Extensions") staat een lijst van extended framebuffer resoluties (degenen die niet bij de VBE standaard horen). Maar, bijvoorbeeld, degene die ik wil gebruiken is 1440x900 de vga=867 optie werkt niet. Mischien omdat deze resoluties buiten de standaard vallen en de fabrikant van de grafische kaart een andere code gebruikt.

In plaats van het gebruiken van die tabel, suggereer ik deze methode:

### Hoe de correcte code te vinden voor je gewenste resolutie

1.  installeer het *lrmi* pakket van [community]
2.  draai *vbetest* als root in een **console** die al framebuffer draait. Het zal **niet** werken in een terminal in X
3.  noteer vervolgens het nummer in [ ] dat bij de gewenste resolutie hoort
4.  Typ 'q' om *vbetest* interactive prompt te sluiten. Als je de zojuist genoteerde resolutie wilt testen, kun je <tt>vbetest -m [nummer]</tt> uitvoeren, om de resolutie te testen. Je zult een gekleurd plaatje op je console zien, dat na een aantal seconden weer naar zwart terugkeert. Als de tekst op je console niet wordt teruggezet, zul je naar een andere console moeten overschakelen en weer terugschakelen.
5.  voeg 512 toe aan het vorige nummer en gebruik het totaal als de code in de <tt>vga=</tt> kernel optie in menu.lst.
6.  herstarten en voilà !

Bijvoorbeeld, wat ik kreeg met *vbetest* is:

```
[356] 1440x900 (256 color palette)
[357] 1440x900 (8:8:8)

```

dus hier is 357 het nummer dat ik wil. 357 + 512 = 869, dus ik zal **vga=869** gebruiken.

Nu heb je een console op de volledige resolutie van je scherm. De volgende stap is om een ander console lettertype te gebruiken op een juiste grootte. In mijn geval gebruik ik het *terminus* lettertype, genaamd ter-120b.

**Let op**:

*   (8:8:8) is for 24-bit color (of 32-bit ?)
*   (5:6:5) is for 16-bit color
*   (5:5:5) is for 15-bit color

## Troubleshooting

### GRUB error 15

Controleer dat de kernel regel `ro` bevat in menu.lst.

### Reboot uitklapmenu in KDE heeft geen effect

Als je een submenu geopend hebt in de lijst van besturingssystemen die je in GRUB hebt geconfigureert, en je kiest er 1 om in te herstarten, en je herstart toch in het standaard besturingssysteem, dan kun je controleren of je de volgende regel in je */boot/grub/menu.lst* hebt:

```
default   saved

```

## Externe bronnen

*   [GRUB Website](http://www.gnu.org/software/grub/)
*   [GRUB Grotto- een uitstekende GRUB hulpbron](http://www.troubleshooters.com/linux/grub/index.htm)