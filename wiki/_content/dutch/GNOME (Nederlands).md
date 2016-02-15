## Contents

*   [1 Wat is GNOME?](#Wat_is_GNOME.3F)
*   [2 Hoe installeer ik GNOME?](#Hoe_installeer_ik_GNOME.3F)
*   [3 Hoe start ik GNOME?](#Hoe_start_ik_GNOME.3F)
*   [4 Wat moet ik doen als GNOME niet goed opstart?](#Wat_moet_ik_doen_als_GNOME_niet_goed_opstart.3F)
*   [5 GDM Gnome Display Manager](#GDM_Gnome_Display_Manager)
*   [6 Meer over dit onderwerp:](#Meer_over_dit_onderwerp:)
*   [7 Handige websites over GNOME](#Handige_websites_over_GNOME)

## Wat is GNOME?

GNOME staat voor GNU Network Object Model Environment. Het is een eenvoudige grafische werkomgeving.

## Hoe installeer ik GNOME?

Door het volgende commando intevoeren in een terminal programma of het console:

```
pacman -S gnome

```

Ook is het sterk aanbevolen GNOME extra te installeren dit doet u met het volgende commando:

```
pacman -S gnome-extra

```

Nu moet je nog rc.conf aanpassen om de juiste diensten optestarten. Open het bestand /etc/rc.conf in uw favoriete texteditor. Zoek naar de regel met de opstartdiensten. Die zijn aangeven met **DAEMONS=(** Voeg de volgende diensten toe: "portmap", "fam" , "dbus" en "hal". Sla vervolgens het bestand op.

## Hoe start ik GNOME?

Zorg ervoor dat de regel: exec --exit-with-session /opt/gnome/bin/gnome-session in het bestand: $HOME/.xinitrc staat.

U kunt nu GNOME opstarten met het commando:

```
startx

```

## Wat moet ik doen als GNOME niet goed opstart?

Verwijder het GNOME session bestand met het commando: rm ~/.gnome2/session

## GDM Gnome Display Manager

Wilt u een grafisch inlogvenster, dan raad ik u GDM aan. U kunt het installeren met het commando:

```
pacman -S gdm

```

Heeft u programma's in uw ~.xinitrc die ook bij het opstarten van GDM moeten worden geladen zoals bijvoorbeeld xsetroot en xsetroot. Dat kunt u het vastleggen in het bestand: $HOME/.xprofile

Voorbeeld:

```
#!/bin/sh

#
# ~/.xprofile
#
# Wordt geladen tijdens het opstarten van GDM 
#

xmodmap -e "pointer = 1 2 3 6 7 4 5"  #set mouse buttons up correctly
xsetroot -solid black                 # Het instellen van een zwarte achtergrond

```

## Meer over dit onderwerp:

*   [GNOME Tips](/index.php/GNOME_Tips "GNOME Tips")
*   [Improve GTK Application Looks(EN)](/index.php/Improve_GTK_Application_Looks "Improve GTK Application Looks")

## Handige websites over GNOME

*   [GNOME-nl](http://nl.gnome.org/)
*   [De officële GNOME website (EN)](http://www.gnome.org/)
*   [De officële GNOME documentatie (EN)](http://www.gnome.org/learn/)
*   [GnomeHelp.org](http://gnomehelp.org/)
*   Opmaak
    *   [Gnome Art](http://art.gnome.org/)
    *   [Gnome Look](http://www.gnome-look.org/)
*   GTK/Gnome programma's:
    *   [Gnome Files](http://www.gnomefiles.org/)
    *   [Gnome Project Listing](http://www.gnome.org/projects/)