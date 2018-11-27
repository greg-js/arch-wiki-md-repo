## Contents

*   [1 Introductie](#Introductie)
    *   [1.1 Richtlijnen](#Richtlijnen)
*   [2 Partities](#Partities)
    *   [2.1 Standaard Mappen structuur](#Standaard_Mappen_structuur)
    *   [2.2 Partitie Layout](#Partitie_Layout)
        *   [2.2.1 Shadowhands's Layout](#Shadowhands's_Layout)
        *   [2.2.2 Romashka's Layout](#Romashka's_Layout)
*   [3 Apparaat namen](#Apparaat_namen)
    *   [3.1 Harde schijven](#Harde_schijven)
    *   [3.2 CD/DVD apparaten](#CD/DVD_apparaten)
    *   [3.3 USB schijven](#USB_schijven)

## Introductie

Deze pagina wordt gebruikt om een lijst te maken van technische linux termen en voorbeelden. Voeg dingen toe waar je dat nodig vindt. **Waarschuwing:** Alle informatie op deze pagina is Arch-specifiek. maar het is mogelijk dat het ook op andere distributies werkt.

### Richtlijnen

Volg a.u.b. de richtlijnen en lees [Help:Editing](/index.php/Help:Editing "Help:Editing") al voor het aanpassen van deze pagina.

## Partities

Deze sectie bevat voorbeelden en informatie over de verschillende types bestandssystemen en partitie-layouts

### Standaard Mappen structuur

De standaard mappen structuur van Arch Linux is als volgt:
(Items die **vet** zijn afgedrukt worden automatisch gemaakt.)

*   root partitie
    *   bin — *syteem utilities*
    *   boot — *kernel boot images en configuratie*
    *   **dev** — *apparaten*
    *   etc — *systeem configuratie bestanden*
        *   rc.d — *daemon start/stop scripts*
        *   conf.d — *daemon configuratie*
        *   profile.d — *globale shell configuratie*
    *   home — *persoonlijke informatie van gebruikers*
    *   lib
        *   firmware — *firmware voor kernel modules*
        *   modules — *kernel modules*
        *   security — *authencatie modules*
        *   tls — *glibc modules*
        *   udev — *udev scripts*
    *   mnt — *gemounte media*
    *   opt — *grote groepen applicaties*
    *   **proc** — *process informatie*
    *   root — *root's persoonlijke bestanden*
    *   sbin — *systeem utilities (alleen toegang voor root)*
    *   **sys** — *system informatie*
    *   **tmp** — *tijdelijke bestanden*
    *   usr
        *   bin — *uitvoerbare applicaties*
        *   include — *applicatie headers*
        *   lib — *applicatie bibliotheken*
        *   man — *man pages*
        *   sbin — *uitvoerbare applicaties (alleen toegang voor root)*
        *   src — *kernel broncode*
        *   share — *gedeelde bestanden voor applicaties*
    *   var
        *   abs — *Arch ABS bestanden*
        *   cache — *tijdelijke opslag (cache bestanden)*
            *   pacman — *pacman cache van pakketten en broncode-bestanden*
        *   lib — *informatiedatabase*
            *   pacman — *pacman repository databases*
        *   log — *log bestanden*
        *   spool — *inkomende mail*

### Partitie Layout

Er zijn verschillende manieren om de harde schijf te partitioneren. Dit zijn enkele voorbeelden van gebruikers. **Richtlijnen:**

```
*root_partition &mdash; **size** *(filesystem)*
**partition &mdash; **size** *(filesystem)*
***sub_partition &mdash; **size** *(filesystem)*
**partition &mdash; **size** *(filesystem)*

Verklaring en details (optioneel)

```

#### Shadowhands's Layout

*   root — **8G** *(ext3)*
    *   boot — **1G** *(ext3)*
    *   home — **30G** *(jfs)*
    *   var — **4G** *(reiserfs)*
    *   media — **140G** *(ext3)*

Alle ext3 partities gebruiken ook <tt>dir_index</tt> ([Details](https://bbs.archlinux.org/viewtopic.php?p=124880#124880)). Ik verkies ext3 over ext2 voor <tt>/boot <tt>omdat ext3 ook als ext2 gemount kan worden en het biedt betere opties voor data recovery. Ik gebruik reiserfs voor <tt>/var</tt> omdat reiserfs goed is met kleine bestanden (<16K), waaruit <tt>/var</tt> voor het meeste bestaat. Ik sla al mijn muziek, spellen, films etc. in <tt>/media</tt> op, omdat ik mijn home-map alleen gebruik voor persoonlijke bestanden.</tt></tt>

<tt><tt>

#### Romashka's Layout

*   root — **1G** *(ext3)*
    *   boot — **64M** *(ext3)*
    *   usr — **8G** *(ext3)*
    *   var — **4G** *(ext3)*
    *   home — **32G** *(ext3)*
    *   storage — **120G** *(xfs)*

## Apparaat namen

**Richtlijnen:**

```
Description
*type
#name 1
#name 2
*type
#name 1
#name 2
#name 3

```

### Harde schijven

In de volgende lijst staat X voor een schijf-letter of nummer (a-z of 0-99) en is Y een partitie-nummer (0-99). De eerste schijf in udev is **a**, in devfs en GRUB is het **0**.

*   udev naam

1.  /dev/hdXY (IDE)
2.  /dev/sdXY (SATA/SCSI)

*   devfs naam (niet meer gebruikt sinds Arch 0.7.1)

1.  /dev/discs/discX/partY

*   GRUB naam

1.  (hdX,Y)

### CD/DVD apparaten

In de volgende lijst is X de apparaat-letter (a-z)

*   udev IDE naam

```
1\. /dev/hdX

```

*   udev SCSI naam (SATA of SCSCI cdrom)

```
1\. /dev/sdX

```

### USB schijven

```
Nog te doen

```
</tt></tt>