**MPD** (music player daemon) je audio plejer koji ima server-klijent arhitekturu. MPD radi u pozadini kao daemon, upravlja muzickim listama i muzickom bazom, i koristi vrlo malo resursa. Da bi uspostavili interfejs sa njim, potreban vam je zaseban klijent. Vise informacija mozete naci na njihovom [web sajtu](http://www.musicpd.org/).

*Molim vas* pogledajte oficijalnu stranicu u instrukcija za podesavanje i resavanje eventualnih problema. Glavni programer je nazvao nasu MPD wiki stranicu *"punom ubica simptoma"*, iz cega se moze zakljuciti da oficijalne stranice sadrze bolje instrukcije.

## Contents

*   [1 Instaliranje MPD-a](#Instaliranje_MPD-a)
*   [2 Daemon podesavanje: Startovanje pri podizanju sistema](#Daemon_podesavanje:_Startovanje_pri_podizanju_sistema)
    *   [2.1 Podesavanje zvuka](#Podesavanje_zvuka)
    *   [2.2 Hronologija MPD-ovog ponasanja na tipicnoj radnoj stanici kad je startovan kao daemon](#Hronologija_MPD-ovog_ponasanja_na_tipicnoj_radnoj_stanici_kad_je_startovan_kao_daemon)
    *   [2.3 Cisti konfiguracioni fajl](#Cisti_konfiguracioni_fajl)
    *   [2.4 Izmenite mpd.conf](#Izmenite_mpd.conf)
    *   [2.5 Kreirajte fajlove](#Kreirajte_fajlove)
    *   [2.6 Napravite bazu](#Napravite_bazu)
*   [3 Alternativa za podesavanje: Startovanje kao obican korisnik](#Alternativa_za_podesavanje:_Startovanje_kao_obican_korisnik)
    *   [3.1 Brzo podesavanje](#Brzo_podesavanje)
    *   [3.2 Podesavanje vise mpd-ova](#Podesavanje_vise_mpd-ova)
*   [4 Klijenti](#Klijenti)
    *   [4.1 Konzola](#Konzola)
    *   [4.2 Graficki](#Graficki)
*   [5 Dodatne stvari](#Dodatne_stvari)
    *   [5.1 Last.fm skroblovanje](#Last.fm_skroblovanje)
        *   [5.1.1 mpdscribble](#mpdscribble)
        *   [5.1.2 Sonata i Ario](#Sonata_i_Ario)
        *   [5.1.3 lastfmsubmitd](#lastfmsubmitd)
    *   [5.2 Last.fm reprodukcija sa lastfmproxy](#Last.fm_reprodukcija_sa_lastfmproxy)
    *   [5.3 Nikad ne pustaj na startu](#Nikad_ne_pustaj_na_startu)
        *   [5.3.1 mpd-git metod](#mpd-gitAUR_metod)
        *   [5.3.2 1\. metod](#1._metod)
        *   [5.3.3 2\. metod](#2._metod)
        *   [5.3.4 3\. metod](#3._metod)
    *   [5.4 MPD i ALSA](#MPD_i_ALSA)
        *   [5.4.1 Opterecenost procesora (CPU) sa ALSA-om](#Opterecenost_procesora_.28CPU.29_sa_ALSA-om)
        *   [5.4.2 Primer konfiguracije: Izlaz sa 44.1 KHz na npr. 16 bit dubini, vise programa odjednom](#Primer_konfiguracije:_Izlaz_sa_44.1_KHz_na_npr._16_bit_dubini.2C_vise_programa_odjednom)
    *   [5.5 Upravljaj MPD-om sa lirc-om](#Upravljaj_MPD-om_sa_lirc-om)
    *   [5.6 Kontrola MPD-a sa bluetooth telefonom](#Kontrola_MPD-a_sa_bluetooth_telefonom)
    *   [5.7 MPD i PulseAudio](#MPD_i_PulseAudio)
    *   [5.8 Cue fajlovi](#Cue_fajlovi)
*   [6 Resavanje problema](#Resavanje_problema)
    *   [6.1 Bezuspesna autodetekcija](#Bezuspesna_autodetekcija)
    *   [6.2 Izvrsne dozvole](#Izvrsne_dozvole)
        *   [6.2.1 Alternativno resenje](#Alternativno_resenje)
        *   [6.2.2 Drugo alternativno resenje](#Drugo_alternativno_resenje)
    *   [6.3 Izbegavanje timeout-ova](#Izbegavanje_timeout-ova)
    *   [6.4 MPD koci na prvom pokretanju](#MPD_koci_na_prvom_pokretanju)
        *   [6.4.1 Easy Tag](#Easy_Tag)
        *   [6.4.2 KID3](#KID3)
    *   [6.5 Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution](#Cannot_connect_to_mpd:_host_.22localhost.22_not_found:_Temporary_failure_in_name_resolution)
    *   [6.6 Drugi problemi kada pokusavate da se konektujete na mpd sa klijentom](#Drugi_problemi_kada_pokusavate_da_se_konektujete_na_mpd_sa_klijentom)
        *   [6.6.1 Prvi nacin za popravku](#Prvi_nacin_za_popravku)
        *   [6.6.2 Drugi nacin za popravku](#Drugi_nacin_za_popravku)
        *   [6.6.3 Treci nacin za popravku](#Treci_nacin_za_popravku)
        *   [6.6.4 Cetvrti nacin za popravku](#Cetvrti_nacin_za_popravku)
    *   [6.7 Port 6600 already in use](#Port_6600_already_in_use)
    *   [6.8 Povezivanje na IPV6 pre IPV4](#Povezivanje_na_IPV6_pre_IPV4)
    *   [6.9 Pucketanje zvuka sa nekim audio fajlovima](#Pucketanje_zvuka_sa_nekim_audio_fajlovima)
    *   [6.10 daemon: cannot setgid for user "mpd": Operation not permitted](#daemon:_cannot_setgid_for_user_.22mpd.22:_Operation_not_permitted)
*   [7 Spoljni linkovi](#Spoljni_linkovi)

## Instaliranje MPD-a

Instalirajte sa [pacman](/index.php/Pacman "Pacman")-om:

```
# pacman -S mpd

```

## Daemon podesavanje: Startovanje pri podizanju sistema

Generalne informacije o MPD konfigurisanju se mogu naci na [http://mpd.wikia.com/wiki/Configuration](http://mpd.wikia.com/wiki/Configuration).

### Podesavanje zvuka

Da podesite audio izlaz tako da radi, uverite se da ste podesili zvucnu karticu i mikser na ispravan nacin. Pogledajte [ALSA](/index.php/ALSA "ALSA"), i [PulseAudio](/index.php/PulseAudio "PulseAudio") ako koristite Gnome 3\. Ne zaboravite da unmutirate neophodne kanale u alsamixer-u, podignite klizace i sacuvajte promene sa alsactl store. Pokrenite mpd sa `/usr/bin/mpd --stdout --no-daemon --verbose` ako zvuk i dalje ne radi.

Uverite se da vasa kartica moze da radi hardversko miksovanje (vecina moze, ukljucujuci i integrisani zvuk na matricnoj ploci). U protivnom to bi moglo da uzrokuje probleme sa pustanjem vise izvora zvuka u isto vreme. Naprimer, ovo moze da spreci Mplayer da pusta zvuk dok mpd daemon i dalje radi, vracajuci audio gresku koja kaze da je uredjaj zauzet.

### Hronologija MPD-ovog ponasanja na tipicnoj radnoj stanici kad je startovan kao daemon

1.  MPD je startovan prilikom startovanja sistema od strane `/etc/rc.conf`, tako sto je sadrzan u `DAEMONS` nizu. (Ili, ovo moze da se uradi i rucno tokom svake sesije pokretanjem `/etc/rc.d/mpd start` sa root privilegijama.
2.  Posto je MPD startovan kao root, prvo cita `/etc/mpd.conf` fajl.
3.  MPD cita varijable korisnika u `/etc/mpd.conf` fajlu i menja od root-a do ovog korisnika.
4.  MPD zatim cita sadrzaje `/etc/mpd.conf` fajla i podesava se u skladu sa njim.

Primetite da MPD menja korisnika koji ga izvrsava sa root-a na korisnika imenovanog u `/etc/mpd.conf` fajlu. Na ovaj nacin upotreba `~` u konfiguracionom fajlu pokazije ispravno na home direktorijum korisnika, a ne na root-ov direktorijum. Mozda je dobro da promenite sve upotrebe `~` na `/home/username` da bi ste izbeglu zbunjivanje kod ovog aspekta MPD-ovog ponasanja.

### Cisti konfiguracioni fajl

*   Kao root, proverite da li `/etc/mpd.conf` postoji i obrisite ga ako postoji. Ovo je bezbedno.

MPD dolazi sa primerom konfiguracionog fajla, dostupnog na `/usr/share/mpd/mpd.conf.example`. Ovaj fajl sadrzi izobilje informacija o MPD podesavanjima i ima podrazumevane mikser vrednosti koje mozete jednostavno da otkomentirate.

*   Kao root, kopirajte ovaj primer fajla u `/etc/mpd.conf`.

```
# cp /usr/share/mpd/mpd.conf.example /etc/mpd.conf

```

(`/usr/share/mpd/mpd.conf.example` je dobar za korisnicko podesavanje)

Jer je MPD podesen da radi kao daemon prilikom startovanja, nikad nemojte da stavljate ovaj fajl u korisnicki direktorijum kao sto to neki tutorijali predlazu, jer nece biti procitan. Stavise, ako ste prethodno napravili `.mpdconf` fajl u vasem home direktorijumu, uklonite ga (da podesite MPD da radi samo sa korisnickim privilegijama, molim vas obratite se sekciji [Alternativno_Podesavanje: Startovanje kao obican korisnik](/index.php/Music_Player_Daemon#Alternative_Setup:_Starting_as_a_User "Music Player Daemon")). Ovo je vazno za sprecavanje konfikata. Prisustvo konfiguracionog fajla u `/etc`, kao sto je ovde slucaj, je ono sto ce omoguciti MPD-u da radi kao daemon prilikom pokretanja sistema. U suprotnom, bila bi neophodna skripta za pokretanje MPD-a *nakon* sto se korisnik ulogovao (kao kdm ili `~/.fluxbox/startup`) ili bi zahtevao rucnu intervenciju svaki put. Za jednu kolekciju muzike, ovaj metod upotrebljen ovde je jednostavno bolji, cak i dok je kolecija deljena izmedju vise korisnika. Takodje, nemojte oklevati oko root privilegija: cak i dok MPD radi kao daemon, on nikad u potpunosti ne radi kao root jer on automatski odbacuje svoje root privilegije nakon izvrsenja.

### Izmenite `mpd.conf`

Difolt arch instalacija cuva podesavanje u /var i koristi "mpd" kao difolt korisnika, umesto da pravi zbrku u ~/. Izmenite `/etc/mpd.conf` da bude u skladu sa tim.

 `/etc/mpd.conf` 
```
music_directory       "/home/user/music"         # Your music dir.
playlist_directory    "/var/lib/mpd/playlists"
db_file               "/var/lib/mpd/mpd.db"
log_file              "/var/log/mpd/mpd.log"
pid_file              "/var/run/mpd/mpd.pid"
state_file            "/var/lib/mpd/mpdstate"
user                  "mpd"
# Binding to address and port causing problems in mpd-0.14.2 best to leave
# commented.
# bind_to_address       "127.0.0.1"
# port                  "6600"

```

*   Ako je vasa muzicka kolekcija sadrzana u vise direktorijuma, mozete da napravite simbolicke linkove pod /var/lib/mpd i podesite 'music_directory' na direktorijum koji sadrzi simbolicke linkove. Zapamtite da podesite dozvole u skladu sa direktorijumima sa kojima su povezani.

*   Da promenite jacinu zvuka sa MPD-a nezavisno od drugih programa, otkomentirajte ili dodajte prekidac u mpd.conf-u:

 `/etc/mpd.conf` 
```
mixer_type			"software"

```

*   Na kraju, ako koristite pulseaudio pod Gnomom 3, difolt podesavanja "alsa"-e za audio izlaz nece raditi. Napravite jos izmena u:

 `/etc/mpd.conf` 
```
audio_output {
        type                    "alsa"
        name                    "Sound Card"
}

```

to

 `/etc/mpd.conf` 
```
audio_output {
        type                    "pulseaudio"
        name                    "Sound Card"
}

```

### Kreirajte fajlove

*   Kao root, napravite direktorijume i fajlove koje ste zadali u `/etc/mpd.conf`.

```
# mkdir -p /var/lib/mpd/playlists /var/run/mpd
# touch /var/lib/mpd/{mpd.db,mpdstate} && touch /var/run/mpd/mpd.pid

```

*   Zatim morate da izmenite dozvole fajla tako da daemon moze da ih modifikuje.

```
# chown -R mpd /var/lib/mpd /var/run/mpd

```

### Napravite bazu

Pravljenje baze se sada ostvaruje preko azuriranja karakteristika klijenta, naprimer 'mpc update'. Prethodni metod, pravljenje MPD baze kao root korisnik (# mpd --create-db), je zastareo.

## Alternativa za podesavanje: Startovanje kao obican korisnik

MPD ne mora biti startovan sa root dozvolama. Jedini razlog zasto MPD mora da bude startovan kao root (tako sto bude pozvan iz `/etc/rc.conf`) je zbog toga sto difolt fajlovi i direktorijumi u difolt konfiguracionom fajlu pokazuju na direktorijume u vlasnistvu root-a (/var direktorijum). Manje uobicajen, ali mnogo bolji pristup je podesiti da MPD radi sa fajlovima i direktorijumima u vlasnistvu obicnog korisnika. Pokretanje MPD-a kao normalan korisnik ima nekoliko prednosti:

1.  Lako mozete imati jedan direktorijum ~/.mpd (ili bilo koji drugi direktorijum pod /home/username) za sve MPD konfiguracione fajlove
2.  Nema gresaka u dozvolama za citanje/pisanje
3.  Fleksibilnije poziva MPD koristeci `~/.xinitrc` umesto da ukljucuje 'mpd' u `/etc/rc.conf` nizu DAEMON-a.

Sledeci koraci pokazuju kako pokrenete MPD kao obican korisnik. **Note**: ovaj pristup nece raditi ako zelite da vise korisnika ima pristup MPD-u.

*   Kopirajte sadrzaj difolt MPD konfiguracionog fajla u `/usr/share/mpd/mpd.conf.example` u vas home direktorijum. Dobro mesto bi bilo `"/home/user/.mpd/mpd.conf"`.
*   Pratite 'stare instrukcije za podesavanje' odozgo, ignorisuci prvi deo o kopiranju konfig-a u `/etc/mpd.conf` i nemojte da podesavate varijablu za korisnika.
*   Napravite sve potrebne fajlove u `"/home/user/.mpd/"`:

```
"~/.mpd/playlists/"
"~/.mpd/db"
"~/.mpd/mpd.db"
"~/.mpd/mpd.log"
"~/.mpd/mpd.error"
"~/.mpd/mpd.pid"
"~/.mpd/mpdstate"

```

*   Podesite da MPD startuje prilikom butovanja sistema tako sto cete ga pozvati iz vaseg `~/.xinitrc`:

```
# this starts mpd as normal user
mpd ~/.mpd/mpd.conf

```

**Note:** that you don't have to put a "&" at the end of the line here, since MPD will automatically daemonize itself.

Na kraju, izbrisite unos 'mpd' iz vaseg DAEMONS niza u `/etc/rc.conf`, jer ga vise ne pokrecete kao root.

### Brzo podesavanje

Najbrzi nacin da podesite strukturu je da uradite sledece:

```
$ mkdir -p ~/.mpd/playlists && touch ~/.mpd/database && cp /usr/share/doc/mpd/mpdconf.example ~/.mpd/mpd.conf

```

Zatim izmenite mpd.conf prema zelji na slican nacin kao [Music Player Daemon#Edit_mpd.conf](/index.php/Music_Player_Daemon#Edit_mpd.conf "Music Player Daemon"). Vodite racuna da morate da otkomentirate db_file unos ako editujete mpd.conf.

Zatim, da ga pokrenete:

```
$ mpd ~/.mpd/mpd.conf

```

### Podesavanje vise mpd-ova

**Korisno ukoliko, naprimer, zelite da pokrenete icecast server.** Ako zelite da drugi MPD daemon (npr., sa icecast izlazom za deljenje muzike preko mreze) koristi istu muziku i muzicke liste kao i ovaj prethodni, jednostavno kopirajte gornji konfiguracioni fajl i napravite novi fajl (npr., `/home/username/.mpd/config-icecast`), i samo promenite log_file, error_file, pid_file i state_file parametre (npr., `mpd-icecast.log`, `mpd-icecast.error`, i tako dalje); upotreba istih staza za direktorijume za muziku i muzicke liste bi osiguralo da ce drugi mpd daemon koristiti istu muzicku kolekciju kao i prvi (npr., kreiranje i editovanje muzicke liste pod prvim daemonom bi uticalo i na drugi daemon, tako da ne morate da pravite iste liste iznova i iznova za drugi daemon). Zatim, pozovite drugi daemon na isti nacin iz vaseg `~/.xinitrc`. (Samo budite sigurni da imaju razlicit broj porta, tako da nisu u suprotnosti sa prvim MPD daemonom).

## Klijenti

Instalirajte klijent program za MPD. Popularne opcije su:

### Konzola

*   **mpc** – Klijent za komandnu liniju (verovatno cete ga zeleti bez obzira na sve)

```
# pacman -S mpc

```

*   [ncmpc](http://hem.bredband.net/kaw/ncmpc/) – NCurses klijent (ovaj je vrlo praktican za pokretanje iz konzole)

```
# pacman -S ncmpc

```

*   [ncmpcpp](http://unkart.ovh.org/ncmpcpp/) – Klon od ncmpc-a sa nekoliko novih karakteristika napisanih u C++

```
# pacman -S ncmpcpp

```

*   [pms](http://pms.sourceforge.net/) – NCurses klijent (visoko konfigurabilan i dostupan)

```
Install [pmus](https://aur.archlinux.org/packages/pmus/) from the [AUR](/index.php/AUR "AUR").

```

### Graficki

*   [ario](http://ario-player.sourceforge.net) – GTK+ klijent sa pretrazivacem biblioteka nalik na Rhythmbox

```
# pacman -S ario

```

*   [gmpc](http://gmpcwiki.sarine.nl/index.php?title=GMPC) – GNOME klijent

```
# pacman -S gmpc

```

*   [QMPDClient](http://bitcheese.net/wiki/QMPDClient) – Klijent napisan sa Qt 4.x.

```
# pacman -S qmpdclient

```

*   [sonata](http://sonata.berlios.de/) – Python GTK+ klijent

```
# pacman -S sonata

```

Pogledajte dugacku listu klijenata na [mpd wiki](http://mpd.wikia.com/wiki/Clients).

## Dodatne stvari

### Last.fm skroblovanje

Imate nekoliko alternativnih nacina da skroblujete vase pesme u [Last.fm](http://www.last.fm) upotrebom MPD-a.

#### mpdscribble

mpdscribble je jos jedan daemon, dostupan u "community" repozitorijumu (ako vise volite, "git" verzija je dostupna u [AUR](https://aur.archlinux.org/packages.php?ID=22274)). Ovo je verovatno najbolja alternativa, jer je polu-zvanicni MPD scrobler i koristi novu funkciju "mirovanja" u MPD-u za preciznije skroblovanje. Takodje, ne morate da imate root pristup da ka podesite, jer ne zahteva nikakve promene u `/etc`. Posetite [the official website](http://mpd.wikia.com/wiki/Client:Mpdscribble) za vise informacija.

Nakon sto ste instalirali mpdscribble, uradite sledece (ne kao root):

*   `$ mkdir ~/.mpdscribble`
*   Napravite fajl `~/.mpdscribble/mpdscribble.conf` i dodajte sledece:

```
 [mpdscribble] 
 host = <your mpd host> # optional, defaults to $MPD_HOST or localhost
 port = <your mpd port> # optional, defaults to $MPD_PORT or 6600
 log = /home/<YOUR_USERNAME>/.mpdscribble/mpdscribble.log
 verbose = 2
 sleep = 1
 musicdir = <your music directory>
 proxy = <your proxy> # optional, e. g. http://your.proxy:8080, defaults to none

 [last.fm]
 # last.fm section, comment if you don't use last.fm
 url = http://post.audioscrobbler.com/
 username = <your last.fm username>
 password = <your last.fm password> # md5sum also possible: echo -n 'PASSWORD' | md5sum | cut -f 1 -d " "
 journal = /home/<YOUR_USERNAME>/.mpdscribble/lastfm.journal

 [libre.fm]
 # libre.fm section, comment if you don't use libre.fm
 url = http://turtle.libre.fm/
 username = <your libre.fm username>
 password = <your libre.fm password> # md5sum also possible: echo -n 'PASSWORD' | md5sum | cut -f 1 -d " "
 journal = /home/<YOUR_USERNAME>/.mpdscribble/librefm.journal

```

*   Dodajte `mpdscribble` u vas `~/.xinitrc`:

```
pidof mpdscribble >& /dev/null
if [ $? -ne 0 ]; then
  mpdscribble &
fi

```

#### Sonata i Ario

Najlaksi nacin, ako vam ne smeta da imate stalno otvoren prozor programa, je da upotrebite Sonata-u ili Ario koji su graficki frontend-ovi za MPD. Oni imaju ugradjenu podrsku za Last.fm skroblovanje u njihovim podesavanjima. Mana toga je da Sonata ne kesira vase pesme ako iz nekog razloga nemate internet konekciju kada je pesma pustena.

#### lastfmsubmitd

lastfmsubmitd je daemon koji je dostupan u "community" repozitorijumu. Da ga instalirate, prvo editujte `/etc/lastfmsubmitd.conf` i dodajte oba `lastfmsubmitd` i `lastmp` u `DAEMONS` niz u `/etc/rc.conf`.

### Last.fm reprodukcija sa lastfmproxy

lastfmproxy je python skripta koja strimuje last.fm muzicki strim ka drugom medija plejeru. Da podesite, instalirajte [lastfmproxy](https://aur.archlinux.org/packages/lastfmproxy/) iz [AUR](/index.php/AUR "AUR")-a, a zatim editujte `/usr/share/lastfmproxy/config.py`. Ako planirate da strimujete samo ka MPD-u na istom hostu, samo editujte login informacije.

**Note:** Posto instarija u direktorijum koji je samo dostupan za citanje, ali zahteva pristup za citanje/pisanje za funkcije poput cuvanje prethodno slusanih stanica, bilo bi pametno kopirati `/usr/share/lastfmproxy` u vas home direktorijum.

Startujte lastfmproxy sa `lastfmproxy` i posetite [http://localhost:1881/](http://localhost:1881/) u vasem web pretrazivacu. Da dodate last.fm stanicu, pronadjite [http://localhost:1881/](http://localhost:1881/) praceno sa lastfm:// url. Primer: [http://localhost:1881/lastfm://globaltags/punk](http://localhost:1881/lastfm://globaltags/punk). Idite nazad na [http://localhost:1881/](http://localhost:1881/) i preuzmite m3u fajl selektovanjem *Start Listening* linka. Jednostavno ga dodajte u vasu muzicku biblioteku.

### Nikad ne pustaj na startu

Ova funkcija je skoro dodata u mpd git od strane Martin-a Kellerman-a, pogledajte *commit*-e b57330cf75bcb339e3f268f1019c63e40d305145 i 2fb40fe728ac07574808c40034fc0f3d2254d49d.

#### [mpd-git](https://aur.archlinux.org/packages/mpd-git/) metod

Ovo je najbolji metod koji je trenutno dostupan, ali je samo trenutno (April 2011) omogucen u git verziji. Instalirajte [mpd-git](https://aur.archlinux.org/packages/mpd-git/) iz [AUR](/index.php/AUR "AUR"), zatim dodajte `restore_paused "yes"` u vas `mpd.conf` fajl.

Ako imate problema sa konektovanjem na klijenta [mpd-git](https://aur.archlinux.org/packages/mpd-git/), pogledajte [Music Player Daemon#Other issues when attempting to connect to mpd with a client](/index.php/Music_Player_Daemon#Other_issues_when_attempting_to_connect_to_mpd_with_a_client "Music Player Daemon").

#### 1\. metod

Ako ne zelite da MPD uvek pusta prilikom startovanja sistema, ali ipak zelite da sacuvate druge informacije u vezi stanja daemona, dodajte sledece linije u vas `/etc/rc.d/mpd` fajl:

```
 *...*
 *stat_busy "Starting Music Player Daemon"*

```

```
   # always start in paused state
   awk '/^state_file[ \t]+"[^"]+"$/ {
       match($0, "\".+\"")
       sfile = substr($0, RSTART + 1, RLENGTH - 2)
   } /^user[ \t]+"[^"]+"$/ {
       match($0, "\".+\"")
       user = substr($0, RSTART + 1, RLENGTH - 2)
   } END {
       if (sfile == "")
               exit;
       if (user != "")
               sub(/^~/, "/home/" user, sfile)
       system("sed -i \x27s|^\\(state:[ \\t]\\{1,\\}\\)play$|\\1pause|\x27 \x27" sfile "\x27")
   }' /etc/mpd.conf

```

```
 */usr/bin/mpd /etc/mpd.conf &> /dev/null*
 *...*

```

Ovo ce izmeniti status plajera na "pauziran", ako je bio stopiran dok je pustao muziku. Zatim cete hteti da ovaj fajl bude sacuvan tako da MPD apdejtovi ne obrisu ovu izmenu. Dodajte (ili editujte) ovu liniju u vasem `/etc/pacman.conf`:

```
NoUpgrade = etc/rc.d/mpd

```

#### 2\. metod

Drugi, jednostavniji metod bio bi da dodate MPD u vas `[rc.conf](/index.php/Rc.conf "Rc.conf")` niz daemona i dodate `mpc stop` ili `mpc pause` u `/etc/rc.local.shutdown` i u `/etc/rc.local`. (Ne zaboravite da morate da imate mpc instaliran da koristite ovaj metod).

Dodavanje samo poretka u `/etc/rc.local` ne moze da garantuje da ce mpd pustati bilo sta, jer moze doci do kasnjenja pre nego sto je stop komanda izvrsena. S druge strane, ako samo dodate redosled u `/etc/rc.local.shutdown`, to ce osigurati da mpd nece uopste pustati pesme, sve dok ne ugasite vas sistem na ispravan nacin. Iako su tehnoloski visak, dodajuci ga u `/etc/rc.local` ce posluziti kao sigurnost za one koji u retkim prilikama ne ugase sistem na pravilan nacin (npr. nestanak struje).

#### 3\. metod

Generalna ideja izmedju ove metode je da pitate mpd da pauzira muziku gde se korisnik odjavljuje (logs out) tako da ce tokom sledeceg restarta mpd drzati kod tog "pauziranog " stanja. Slanje takve komande se moze postici upotrebom [mpc](https://www.archlinux.org/packages/?name=mpc), interfejsa za MPD koji se pokrece sa komandne linije:

```
pacman -S mpc

```

GDM korisnici mogu zatim da dodaju sledecu liniju u /etc/gdm/PostSession/Default (obavezno je dodajte pre "exit 0"):

```
/usr/bin/mpc pause

```

Ne-GDM korisnici mogu da koriste metodu od svog login menadzera da pokrenu liniju prilikom odjavljivanja (logout).

### MPD i ALSA

Ponekad, kada koristite drugi audio izlaz, npr.: neke web stranice sadrza Flash aplete, MPD ne moze da reprodukuje nista vise (dok ne restartujete). Greska izgleda otprilike ovako: (ako trazite fajl `/var/log/mpd/mpd.error`)

```
Error opening alsa device "hw:0,0": Device or resource busy

```

Resenje je sledece (dmix nas cuva opet). Dodajte ove linije u vas `/etc/mpd.conf`:

```
audio_output {
        type                    "alsa"
        name                    "Sound Card"
        options                 "dev=dmixer"
        device                  "plug:dmix"
}
```

A zatim restartujte sa `/etc/rc.d/mpd restart`.

Pretragom interneta nasao sam razlog zasto se to desava na Gentoo wikiju:

*   Zvucna karta ne podrzava hardver miksovanje (koristi **dmix** plugin)
*   Aplikacija ne radi sa ALSA-om sa njenim difolt podesavanjima

Za detaljan opis, preporucuje se da pogledate [ovaj](http://mpd.wikia.com/wiki/Alsa) link. Tu mozete naci primer asound.conf koji je radio za mene bez problema.

#### Opterecenost procesora (CPU) sa ALSA-om

Kada koristite MPD sa ALSA-om, moze doci do toga da MPD zauzima dosta procesora (CPU) (oko 20-30%). Uzrok tome je vecina kartica koje podrzavaju 48kHz, a vecina muzike je na 44kHz, pa zbog toga primorava MPD da je resampluje. Ova operacija zahteva dosta resursa procesora i rezultira njegovim opterecenjem.

Za vecinu korisnika problem se moze resiti tako sto cete reci MPD-u da ne koristi resamplovanje dodavanjem `auto_resample "no"` u audio_output-part od `/etc/mpd.conf`. Ovo ce, medjutim, blago umanjiti kvalitet zvuka.

Primer iz `mpd.conf`:

```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   auto_resample		"no"
}

```

Paljenje mmap-a moze ubrzati stvari, donekle:

```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   use_mmap		"yes"
}

```

Neki korisnici ce takodje zeleti da kazu dmix-u da koriste i 44kHz. Vise informacija oko podesavanja performansi vaseg MPD-a mozete naci na [MPD wiki](http://mpd.wikia.com/wiki/Tuning)

#### Primer konfiguracije: Izlaz sa 44.1 KHz na npr. 16 bit dubini, vise programa odjednom

*Zasto ovi formati?* Jer su oni standard CDA, jer ALSA sama po sebi dozvoljava da vise od jednog programa "koristi zvuk" samo sa dmix-om - ciji je algoritam za resamplovanje inferioran - i zato sto dmix po difoltu resampluje sve nize od 48 KHz (ili koji god visi format je pusten u tom momentu). Takodje, neki pojedinci dobijaju klikcuce zvukove ako bar `mpd.conf` nije izmenjen na ovaj nacin.

*Koji su nedostaci?* Ova podesavanja uzrokuju da *sve* (ako je neophodno) bude resamplovano na ovaj format, kao sto je materijal sa DVD-ja ili TV-a koji je uglavnom na 48 KHz. Ali ne postoji poznati nacin da ALSA dinamicki menja format, a posebno ako slusate mnogo vise CD-ova nego bilo sta drugo. 48 → 44.1 i nije preveliki gubitak.

Slece pretpostavlja da ne postoje vec druga podesavanja koja su u konfliktu, odnosno ga prepisuju. Ovo posebno vazi za potencijal trenutnog korisnika `~/.asoundrc` — koji MPD, kao svoj korisnik, ignorise, stoga sledece treba da ide u `/etc/asound.conf`:

 `/etc/asound.conf` 
```
defaults.pcm.dmix.rate 44100 # Force 44.1 KHz
defaults.pcm.dmix.format S16_LE # Force 16 bits

```
 `/etc/mpd.conf` 
```
audio_output {
        type                    "alsa" # Use the ALSA output plugin.
	name			"HDA Intel" # Can be called anything or nothing tmk, but must be present.
        options                 "dev=dmixer"
        device                  "plug:dmix" # Both lines cause MPD to output to dmix.
	format	        	"44100:16:2" # the actual format
	auto_resample		"no" # This bypasses ALSA's own algorithms, which generally are inferior. See below how to choose a different one.
	use_mmap		"yes" # Minor speed improvement, should work with all modern cards.
}

samplerate_converter		"0" # MPD's best, most CPU intensive algorithm. See 'man mpd.conf' for others — for anything other than the poorest "internal", libsamplerate must be installed.
```

**Note:** MPD daje mp3 formatu specijalni tretman prilikom dekodiranja: Kao rezultat uvek daje 24 bitni. (Konverzija kao primorana od strane *format* linije dolazi tek nakon toga.

Ako neko zeli da ostavi odluku vezanu za bit dubinu ALSA-i, odnosno MPD-u, otkomentirajte, odnosno izostavite *dmix.format* liniju i izmenite jednu za mpd sa *format* na "44100:*:2".

**Note:** *Pretapanje* izmedju fajlova dekodiranih na dve razlicite dubine bitova (naprimer, jedan mp3 i jedan 16 bitni flac) ne rade ukoliko konverzija nije aktivna.

### Upravljaj MPD-om sa lirc-om

Vec postoje neki klijenti dizajnirani za komunikaciju izmedju lircd-a i MPD-a, medjutim, sto se tice prakticne upotrebe, oni nisu vrlo korisni jer su im funkcije ogranicene.

Preporucuje se upotreba mpc-a sa irexec-om. mpc je plejer za komandnu liniju koji samo salje komande ka MPD-u i odmah izlazi, sto je savrseno za irexec, koji je inace izvrsilac komandi sadrzan u lirc-u. irexec izvrsava zadatu komandu po prispeloj informaciji sa udaljenog kontrolnog dugmeta.

Pre svega, podesite vase daljinske upravljace kao sto je navedeno u **[LIRC](/index.php/LIRC "LIRC")** clanku.

Editujte vas lirc konfiguracioni fajl za startovanje; difolt lokacija je `~/.lircrc`.

Popunite fajl sa sledecim obrascem:

```
begin
     prog = irexec
     button = <button_name>
     config = <command_to_run>
     repeat = <0 or 1>
end

```

Koristan primer:

```
## irexec
begin
     prog = irexec
     button = play_pause
     config = mpc toggle
     repeat = 0
end

begin
     prog = irexec
     button = stop
     config = mpc stop
     repeat = 0
end
begin
     prog = irexec
     button = previous
     config = mpc prev
     repeat = 0
end
begin
     prog = irexec
     button = next
     config = mpc next
     repeat = 0
end
begin
     prog = irexec
     button = volup
     config = mpc volume +2
     repeat = 1
end
begin
     prog = irexec
     button = voldown
     config = mpc volume -2
     repeat = 1
end
begin
     prog = irexec
     button = pbc
     config = mpc random
     repeat = 0
end
begin
     prog = irexec
     button = pdvd
     config = mpc update
     repeat = 0
end
begin
     prog = irexec
     button = right
     config = mpc seek +00:00:05
     repeat = 0
end
begin
     prog = irexec
     button = left
     config = mpc seek -00:00:05
     repeat = 0
end
begin
     prog = irexec
     button = up
     config = mpc seek +1%
     repeat = 0
end
begin
     prog = irexec
     button = down
     config = mpc seek -1%
     repeat = 0
end

```

Postoji vise funkcija za mpc, pokrenite [mpc(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mpc.1) za vise informacija.

### Kontrola MPD-a sa bluetooth telefonom

Mozete takodje da kontrolisete MPD (do odredjene mere) upotrebom telefona sa upaljenim bluetooth-om. Morate da uradite sledece:

*   instalirajte [remuco](http://remuco.sourceforge.net/index.php/Remuco) -- bezicni daljinski upravljac za nekoliko Linux medija plejera ([aur](https://aur.archlinux.org/packages.php?ID=25072))
*   prebacite remocu klijenta -- jar/jad fajlovi sa `/usr/share/remuco/client/` na vas telefon i instalirajte ga
*   pokrenite `remuco-mpd` (kao trenutni korisnik)
*   pokrenite remuco na vasem telefonu, definisite novu bluetooth remuco konekciju (uparite telefon i racunar ukoliko vec niste) i istrazite njegove mogucnosti

Vise informacija o remuco ukljucujuci i resavanje eventualnih problema mozete naci na njegovom [homepage-u](http://remuco.sourceforge.net/index.php/Remuco)

### MPD i PulseAudio

Editujte `/etc/mpd.conf`, i otkomentirajte audio_output deo za tip "pulse". Server i sink linije bi trebalo da budu komentovane osim ako znate sta radite.

Zatim, dodajte mpd korisnika (i vaseg ako to niste jos uradili) u neophodne pulse grupe. Pulse-access grupa bi trebalo da bude dovoljna, ali mozete da dodate i pulse-rt. Grupa "pulse" nije neophodna.

```
# gpasswd -a mpd pulse-access
# gpasswd -a mpd pulse-rt

```

Na kraju, mozda cete morati, a mozda i ne, da kopirate `~/.pulse-cookie` sa vaseg trenutnog (pulse radi) korisnickog direktorijuma u vas mpd korisnicki home direktorijum. To ce verovatno biti `/var/lib/mpd` ako ste pratili prvi deo ovog vikija. Ovo bi vreovatno samo dozvolilo vasem trenutnom korisniku da slusa na MPD-ovom pulse. Mozete razmotriti da pokrecete pulse za celokupni sistem (system-wide) ako je to nedovoljno.

### Cue fajlovi

Da podesite podrsku za cue fajlove koja ce zapravo raditi, moracete da zaobidjete nezgodni libcue bag. Libcue kopira neke fajlove direktno iz libcdio-a, stvarajuci konflikt sa njim. Koraci za obezbedjivanje ispravne cue podrske:

*   uklonite libcdio privremeno (pacman -Rdd libcdio)
*   instalirajte libcue (pacman -S libcue)
*   instalirajte mpd sa abs-om ili iz aur-a.
*   reinstalirajte libcdio (pacman -S libcdio)

U momentu pisanja, mpd ne analizira brojeve pesama iz cue listova. Postoji zakrpa dostupna na ([http://musicpd.org/mantis/view.php?id=3230](http://musicpd.org/mantis/view.php?id=3230)) Kada ova zakrpa bude spojena sa MPD-om, uklonicu ovu liniju :)

## Resavanje problema

### Bezuspesna autodetekcija

Tokom startovanja MPD-a, on pokusava da automatski detektuje vasa podesavanja i konfigurise izlaz i jacinu zvuka u skladu sa tim. Iako to uglavnom ide dobro, na nekim sistemima ce doziveti neuspeh. Moze pomoci da kazete MPD-u posebno sta da koristi za izlaz i mikser kontrole. Ako ste kopirali `/etc/mpd.conf` od `/etc/mpd.conf.example` kao sto je naznaceno gore, mozete jenostavno da otkomentirate:

Primer za alsa izlaz i alsa mikser:

```
audio_output {
	type			"alsa"
	name			"My ALSA Device"
	device			"hw:0,0"	# optional
	format			"44100:16:2"	# optional
	mixer_type		"hardware"
	mixer_device		"default"
	mixer_control		"PCM"
}

```

**Napomena:** u slucaju problema sa dozvolama kada koristite ESD sa MPD-om, izvrsite ovo kao root:

```
# chsh -s /bin/true mpd

```

### Izvrsne dozvole

**Warning:** Ovo nije dobra bezbednosna praksa i moze biti nepotrebna.

MPD zahteva +x dozvole na **SVIM** roditeljskim direktorijumima u vasoj muzickoj kolekciji (tj., ako je lociran van "mpd" home direktorijuma /var/lib/mpd). Po difoltu useradd podesava dozvole na home direktorijumu na 1700 drwx------. Tako da ako si kao i ja, moraces da promenis dozvole na /home/korisnik. Primer... moja muzicka kolekcija se nalazi u /home/korisnik/music.

```
# chmod a+x /home/$KORISNIK
# chmod -R a+X /home/$KORISNIK/music

```

#### Alternativno resenje

Alternativno resenje bi bilo da upotrebite vasu grupu da podelite odredjene fajlove, izmedju kojih i vasu muzicku biblioteku. Prvo uklonite sve dozvole za grupu, a zatim dodajte dozvole za grupu tako da mogu da citaju i izvrsavaju home i music.

```
# chmod -R g-rwx /home/$KORISNIK
# chmod g+rx /home/$KORISNIK
# chmod -R g+rX /home/$KORISNIK/music

```

#### Drugo alternativno resenje

Druga alternativa je da ponovo mountujete muzicki direktorijum pod direktorijumom gde mpd ima pristup. Ovo ne podrazumeva iste bezbednosne rizike kao sto su izmena dozvola na home direktorijumu korisnika.

```
# mkdir /var/lib/mpd/music
# echo "/home/$KORISNIK/music /var/lib/mpd/music none bind" >> /etc/fstab
# mount -a
# /etc/rc.d/mpd restart

```

I to bi trebalo da resi problem. Takodje pogledajte [tema na forumu.](https://bbs.archlinux.org/viewtopic.php?id=86449)

### Izbegavanje timeout-ova

Da se resite timeout-ova (tj., kada ste pauzirali muziku dugo vremena) u gpmc-u i drugim klijentima otkomentirajte i povecajte `connection_timeout` opciju u `mpd.conf`.

Ako su fajlovi i/ili naslovi prikazani u pogresnom sifrovanju, otkomentirajte i izmenite `filesystem_charset` i `id3v1_encoding` opcije. Imajte na umu da ne mozete da podesite sifrovanje za ID3 v2 tagove. Da resite ovo, mozete da upotrebite [spoljasnji citaci tag-ova](http://mpd.wikia.com/wiki/GenericDecoder#Generic_Tagreader).

Ako hocete da koristite drugi racunar da kontrolisete MPD preko mreze, `bind_to_address` opcija u `mpd.conf` ce morati da bude podesena na ili vasu IP adresu, ili `any` ako se vasa Ip adresa cesto menja. Zapamtite da dodate mpd u `/etc/hosts.allow` fajl da omogucite spoljasnji pristup.

**Streamovanje**
Sa zadnjom verzijom MPD-a (0.15), dolazi i sadrzani httpd za streamovanje.

Da aktivirate ovu funkciju, samo dodajte novi izlaz tipa httpd u `mpd.conf`:

```
audio_output {
          type   "httpd"
          name   "What you want"
          encoder "lame"     # vorbis or lame supported
          port    "8000"
          bitrate  "128"
          format   "44100:16:2"  # change 2 to 1 for mono
  }

```

Restartujte mpd daemon i, sa drugog kompjutera, jednsotavno ucitajte strim kao bilo koji url.

```
$ mplayer http://<server's IP>:8000

```

**Note:** Morate da otvorite port na vasem ruteru / firewall-u da bi strim bio poveziv sa drugog racunara.

Vecina plejera (odnosno vlc ili xmms2) bi trebalo da mogu da ucitaju strim preko "add url..." meni opcije.

Ovo je lep i cist nacin da zamenite trenutni icecast metod sa necim sto je prirodno podrzano u okviru MPD-a.

### MPD koci na prvom pokretanju

Ovo je cesta greska koja je uzrokovana korumpiranim mp3 tagovima. Evo ga eksperimentalni nacin za resavanje ovog problema. Zahtevi:

*   kid3
*   easytag

Ovaj metod je veoma dosadan, a posebno sa ogromnom bazom. Samo kao osnova je trajao 2.5 sati da popravi 160gb baze.

#### Easy Tag

Namena easytag-a je da on detektuje greske u tagovima, ali kao MPD on zastaje i umire. Trik je da vam easytag zapravo govori koji fajlovi uzrokuju probleme na statusnoj liniji. Pre startovanja easytag-a, uverite se da imate otvoren terminal spreman za ubijanje easytag-a kako bi izbegli kocenje. Kada ste spremni, na drvetu direktorijuma izaberite direktorijum gde se nalaze sve vase pesme. Po difoltu, easytag startuje pretragu svih poddirektorijuma za mp3 fajlove. Kada primetite da easytag stopira skeniranje za pesme, napravite notaciju za culprit i ubite easytag.

#### KID3

Ovde kid3 dolazi zgodno. Sa kid3 idite na korumpiranu pesmu i prepisite jedan od tagova, a zatim sacuvajte fajl. Ovo bi trebalo da primora kid3 da prepise ceo tag ponovo i tako popravi problem sa MPD-om i easytag kocenjem.

Ponovite ovu proceduru dok ne zavrsite muzicku biblioteku.

### Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution

Cannot connect to MPD (with ncmpcpp), ako ste diskonektovani sa mreze. Resenje je [iskljucite IPv6](/index.php/IPv6_-_Disabling_the_Module "IPv6 - Disabling the Module") ili dodajte liniju u /etc/hosts

```
::1 localhost.localdomain localhost

```

### Drugi problemi kada pokusavate da se konektujete na mpd sa klijentom

Pojedinci su prijavili da nisu mogli da pristupe MPD-u sa raznim klijentima, uz greske poput ovih:

```
$ ncmpcpp
Cannot connect to mpd: Connection closed by the server
$ sonata
2011-02-13 18:33:05  Connection lost while reading MPD hello
2011-02-13 18:33:05  Not connected
2011-02-13 18:33:05  Not connected

```

Molim vas da pogledate postove u vezi ncmpcpp na Arch forumima [OVDE](https://bbs.archlinux.org/viewtopic.php?id=109962) i [OVDE](https://bbs.archlinux.org/viewtopic.php?id=113493). Takodje pogledajte ARch bag izvestaj u vezi ovog problema [OVDE](https://bugs.archlinux.org/task/22071).

#### Prvi nacin za popravku

Prvi nacin bi bio da dodate sledece u /etc/hosts.allow.

 `/etc/hosts.allow`  `mod: ALL` 

#### Drugi nacin za popravku

Proverite `mpd.conf` za linije poput `mpd.error` i uklonite ih. MPD fajl za greske je zastareo i uklonjen je.

#### Treci nacin za popravku

**Note:** Nisam siguran da je ovo dobra ideja. Postoji upozorenje u vezi promene adrese koja binduje ka, u difolt mpd.conf. Ako ovo ne pomogne, mozete da stavite pod komentare izmene.

Ako to ne pomogne, dodajte sledece u `mpd.conf`:

```
 bind_to_address "127.0.0.1"
 port "6600"

```

Nakon toga, podesite vaseg klijenta da se poveze preko 127.0.0.1\. Naprimer, dodajte sledece u ncmpcpp konfig fajl:

```
 mpd_host "127.0.0.1"
 mpd_port "6600"

```

#### Cetvrti nacin za popravku

**Note:** Ovaj metod za popravku se odnosi samo na korisnike rucno kompajliranog MPD-a ili AUR paketa mpd-git

Konacno moguce resenje je jednostavno kompajliranje MPD-a bez libwrap podrske. Instalirajte mpd-git kao i obicno, ali editujte PKGBUILD i nadjite

 `--with-zeroconf=no` 

i zamenite ga sa

```
--with-zeroconf=no \
        --disable-libwrap
```

### Port 6600 already in use

MPD mora da se poveze na port 6600 i ne moze da startuje ako je taj port vec u upotrebi. Najcesci razlog za to je da je korisnik vec startovao MPD, a zatim jos jednom pokusao da ga startuje. U principu, ovde nista ne treba raditi.

Ako je port 6600 vezan iz nekog drugog razloga, mozete upotrebiti sledecu komandu da pronedjete proces koji ga zauzima:

```
# ss -tulpan | grep 6600

```

Ovo ce izlistati IP:Port i ime procesa koji drzi konekciju (root privilegije su neophodne da vidite sve procese).

```
Ako morate da restartujete MPD iz nekog razloga, upotrebite:

```

```
 $ mpd --kill
 $ mpd 

```

Brute-force pristup:

```
 $ killall mpd
 $ mpd 

```

**Note:** Ako obicno koristite MPD kao root, moracete da pokrenete gornje komande kao root.
U zadnjoj verziji MPD-a, --create-db je potpuno zastareo. Baza ce biti kreirana automatski prilikom prvog pokretanja i moze se nakon toga azurirati preko vaseg klijenta (npr., mpc update). Sada mozete da koristite inotify podrsku da automatski azurira muzicku bazu. Dodajte sledece u `mpd.conf`  `auto_update "yes"` da ga omogucite.

### Povezivanje na IPV6 pre IPV4

Ako pri pokretanju vidite ovu poruku:

```
listen: bind to '0.0.0.0:6600' failed: Address already in use (continuing anyway, because binding to '[::]:6600' succeeded)

```

MPD pokusava da se poveze na ipv6 interfejs pre povezivanja na ipv4\. Ako hocete da koristite vas ipv4 interfejs, hardkodirajte ga u mpd.conf na sledeci nacin:

```
bind_to_address "127.0.0.1"

```

Ili mozete da odredite nekoliko vezivanja, naprimer, da MPD slusa na localhost-u i na spoljasnjem IP-ju vase mrezne karte:

```
bind_to_address "127.0.0.1"
bind_to_address "192.168.1.13"

```

### Pucketanje zvuka sa nekim audio fajlovima

Ovo je obicno problem u brzini reprodukcije i moze se popraviti uklanjanjem komentara audio_output_format linije u:

 `/etc/mpd.conf`  `audio_output_format "44100:16:2"` 

Ovo je obicno razumna vrednost za vecinu mp3 fajlova.

### daemon: cannot setgid for user "mpd": Operation not permitted

Greska navodi da korisnik koji startuje proces (vi) nema dozvole da postane drugi korisnik (mpd).

Da resite problem, startujte mpd kao root.

```
su -c "/etc/rc.d/mpd start"

```

ili

```
sudo /etc/rc.d/mpd start

```

## Spoljni linkovi

*   [Oficijalni Web sajt](http://www.musicpd.org/)
*   [Oficijalni Wiki](http://mpd.wikia.com/wiki/Main_Page)
*   [Sortirana lista MPD klijenata](http://mpd.wikia.com/wiki/Clients)
*   [MPD forum](http://www.musicpd.org/forum/)