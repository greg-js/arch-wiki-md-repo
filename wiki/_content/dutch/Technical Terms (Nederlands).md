## Contents

*   [1 Introductie](#Introductie)
    *   [1.1 Richtlijnen](#Richtlijnen)
*   [2 Partities](#Partities)
    *   [2.1 Standaard Mappen structuur](#Standaard_Mappen_structuur)
    *   [2.2 Partitie Layout](#Partitie_Layout)
        *   [2.2.1 Shadowhands's Layout](#Shadowhands.27s_Layout)
        *   [2.2.2 Romashka's Layout](#Romashka.27s_Layout)
*   [3 Apparaat namen](#Apparaat_namen)
    *   [3.1 Harde schijven](#Harde_schijven)
    *   [3.2 CD/DVD apparaten](#CD.2FDVD_apparaten)
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
    *   bin — _syteem utilities_
    *   boot — _kernel boot images en configuratie_
    *   **dev** — _apparaten_
    *   etc — _systeem configuratie bestanden_
        *   rc.d — _daemon start/stop scripts_
        *   conf.d — _daemon configuratie_
        *   profile.d — _globale shell configuratie_
    *   home — _persoonlijke informatie van gebruikers_
    *   lib
        *   firmware — _firmware voor kernel modules_
        *   modules — _kernel modules_
        *   security — _authencatie modules_
        *   tls — _glibc modules_
        *   udev — _udev scripts_
    *   mnt — _gemounte media_
    *   opt — _grote groepen applicaties_
    *   **proc** — _process informatie_
    *   root — _root's persoonlijke bestanden_
    *   sbin — _systeem utilities (alleen toegang voor root)_
    *   **sys** — _system informatie_
    *   **tmp** — _tijdelijke bestanden_
    *   usr
        *   bin — _uitvoerbare applicaties_
        *   include — _applicatie headers_
        *   lib — _applicatie bibliotheken_
        *   man — _man pages_
        *   sbin — _uitvoerbare applicaties (alleen toegang voor root)_
        *   src — _kernel broncode_
        *   share — _gedeelde bestanden voor applicaties_
    *   var
        *   abs — _Arch ABS bestanden_
        *   cache — _tijdelijke opslag (cache bestanden)_
            *   pacman — _pacman cache van pakketten en broncode-bestanden_
        *   lib — _informatiedatabase_
            *   pacman — _pacman repository databases_
        *   log — _log bestanden_
        *   spool — _inkomende mail_

### Partitie Layout

Er zijn verschillende manieren om de harde schijf te partitioneren. Dit zijn enkele voorbeelden van gebruikers. **Richtlijnen:**

```
*root_partition &mdash; **size** _(filesystem)_
**partition &mdash; **size** _(filesystem)_
***sub_partition &mdash; **size** _(filesystem)_
**partition &mdash; **size** _(filesystem)_

Verklaring en details (optioneel)

```

#### Shadowhands's Layout

*   root — **8G** _(ext3)_
    *   boot — **1G** _(ext3)_
    *   home — **30G** _(jfs)_
    *   var — **4G** _(reiserfs)_
    *   media — **140G** _(ext3)_

Alle ext3 partities gebruiken ook <tt>dir_index</tt> ([Details](https://bbs.archlinux.org/viewtopic.php?p=124880#124880)). Ik verkies ext3 over ext2 voor <tt>/boot<tt> omdat ext3 ook als ext2 gemount kan worden en het biedt betere opties voor data recovery. Ik gebruik reiserfs voor <tt>/var</tt> omdat reiserfs goed is met kleine bestanden (<16K), waaruit <tt>/var</tt> voor het meeste bestaat. Ik sla al mijn muziek, spellen, films etc. in <tt>/media</tt> op, omdat ik mijn home-map alleen gebruik voor persoonlijke bestanden.

#### Romashka's Layout

*   root — **1G** _(ext3)_
    *   boot — **64M** _(ext3)_
    *   usr — **8G** _(ext3)_
    *   var — **4G** _(ext3)_
    *   home — **32G** _(ext3)_
    *   storage — **120G** _(xfs)_

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