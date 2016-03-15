Dit document legt uit hoe je ALSA aan de praat kan krijgen.

## Contents

*   [1 Installatie](#Installatie)
    *   [1.1 Kernel stuurprogramma's](#Kernel_stuurprogramma.27s)
    *   [1.2 Gebruikersapparatuur](#Gebruikersapparatuur)
*   [2 Configuratie](#Configuratie)
    *   [2.1 Configuren, volume instellen en testen](#Configuren.2C_volume_instellen_en_testen)
    *   [2.2 Permissies instellen](#Permissies_instellen)
    *   [2.3 Ervoor zorgen dat de volumeinstellingen hersteld worden bij het opstarten](#Ervoor_zorgen_dat_de_volumeinstellingen_hersteld_worden_bij_het_opstarten)

## Installatie

### Kernel stuurprogramma's

ALSA zit standaard in alle 2.6 kernels. Als je je eigen kernel wil compileren, moet je niet vergeten ALSA aan te zetten.

### Gebruikersapparatuur

*   Gebruik pacman om de volgende software te installeren.

```
# pacman -S alsa-lib alsa-utils alsa-oss

```

## Configuratie

### Configuren, volume instellen en testen

*   Draai alsaconf:

```
 # alsaconf

```

*   Stel het volume in met:

```
 # alsamixer

```

*   Probeer een bestand te spelen:

```
 # aplay /usr/share/sounds/alsa/Front_Center.wav

```

### Permissies instellen

Om ervoor te zorgen dat normale gebruikers ook de geluidskaart kunnen gebruiken, volg deze stappen:

*   Voeg de gebruiker toe aan de audiogroep:

```
 # gpasswd -a GEBRUIKERSNAAM audio

```

*   Log uit en weer in om ervoor te zorgen dat de audiogroep geladen is.

### Ervoor zorgen dat de volumeinstellingen hersteld worden bij het opstarten

*   Voer als root 'alsactl' uit om '/etc/asound.state' te creëren:

```
 # alsactl store

```

*   Bewerk '/etc/rc.conf' en voeg 'alsa' toe aan de lijst met daemons die starten bij het opstarten van de computer. Dit zorgt ervoor dat de volumeinstellingen worden opgeslagen als de computer wordt afgesloten en weer worden geladen als de computer opstart.