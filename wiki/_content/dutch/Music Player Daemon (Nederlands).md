Music Player Daemon is een geluidsspeler met een server-cliënt architectuur. MPD draait in de achtergrond als een daemon, beheert afspeellijsten en een muziekdatabank en gebruiks weinig rekenkracht. Om met MPD te communiceren is er een aparte cliënt nodig. Zit voor meer informatie de website, [http://www.musicpd.org/](http://www.musicpd.org/).

# MPD installatie

*   Gebruik pacman om MPD te installeren:

```
# pacman -S mpd

```

# MPD configuratie

*   Kopieer configuratiebestand:

```
 # cp /etc/mpd.conf.example /etc/mpd.conf

```

*   Bewerk configuratiebestand:

```
 # $EDITOR /etc/mpd.conf

```

*   Maak mappen aan:

```
 $ mkdir ~/.mpd
 $ mkdir ~/.mpd/playlists

```

*   Maak de databank aan (kan lang duren, afhankelijk van de grootte van de muziekcollectie):

```
 # /etc/rc.d/mpd create-db

```

*   Start MPD

```
 # /etc/rc.d/mpd start

```

*   Installeer een cliënt:

```
 # pacman -S ncmpc mpc gmpc glurp pygmy

```

**mpc** - Command Line Client (sowieso installeren)

**ncmpc** - NCurses Cliënt (handig in een terminalvenster of als X niet draait)

**pygmy** - Python GTK+ Cliënt (de "beste" in een grafische omgeving)

**gmpc** - Gnome Cliënt

**glurp** - GTK2 Cliënt

**pympd** is nog een andere cliënt, gemaakt door Matt "metzen" McDonald & Arch Linux gebruiker Natan "whatah" Zohar. Veel gebruikers verkiezen pympd. Hun website vind je hier: [http://pympd.sourceforge.net/](http://pympd.sourceforge.net/)

**sonata** - Populaire, lightweight GTK2 cliënt.

Er zijn nog veel meer clients, zie deze webpagina: [http://mpd.wikia.com/wiki/Clients](http://mpd.wikia.com/wiki/Clients)

## Externe links

*   [Wiki pagina van MPD (Engels)](http://mpd.wikia.com/wiki/Clients/)
*   [MPD Wiki (Engels)](http://mpd.wikicities.com/wiki/Main_Page)