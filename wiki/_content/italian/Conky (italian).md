Conky è un monitor di sistema per X. È disponibile per sistemi Gnu/Linux e FreeBSD. ed è un software libero rilasciato con licenza GPL. Conky è in grado di monitorare molte variabili di sistena come CPU, memoria, swap, spazio su disco, temperatura, processi in top, upload, download, messaggi di sistema, e molto altro (tramite script aggiuntivi per es.). É estramamente configurabile, comunque, la configurazione può essere un pò difficile da capire.Conky è un fork di torsmo.

## Contents

*   [1 Installazione & Configurazione](#Installazione_.26_Configurazione)
*   [2 Pacchetti AUR](#Pacchetti_AUR)
*   [3 Suggerimenti](#Suggerimenti)
    *   [3.1 Abilitare la transparenza vera (KDE4)](#Abilitare_la_transparenza_vera_.28KDE4.29)
    *   [3.2 Prevenire lo sfarfallio](#Prevenire_lo_sfarfallio)
    *   [3.3 Non minimizzare quando si abilita Mostra Desktop (Compiz)](#Non_minimizzare_quando_si_abilita_Mostra_Desktop_.28Compiz.29)
    *   [3.4 Integrazione con KDesktop](#Integrazione_con_KDesktop)
    *   [3.5 Visualizzare informazioni di aggiornamento del pacchetto](#Visualizzare_informazioni_di_aggiornamento_del_pacchetto)
    *   [3.6 Visualizzazione previsioni meteo](#Visualizzazione_previsioni_meteo)
    *   [3.7 Visualizzazione feed RSS](#Visualizzazione_feed_RSS)
    *   [3.8 Visualizzazione ranking Arch Linux su Distrowatch](#Visualizzazione_ranking_Arch_Linux_su_Distrowatch)
    *   [3.9 Visualizzazione rTorrent](#Visualizzazione_rTorrent)
    *   [3.10 Visualizzazione numero di nuove email (GMail)](#Visualizzazione_numero_di_nuove_email_.28GMail.29)
    *   [3.11 Visualizzazione nuove email (IMAP + SSL)](#Visualizzazione_nuove_email_.28IMAP_.2B_SSL.29)
*   [4 Contributo-Utenti Configurazioni d'esempio](#Contributo-Utenti_Configurazioni_d.27esempio)
    *   [4.1 Graysky](#Graysky)
*   [5 Un semplice script ad anelli con supporto nvidia:](#Un_semplice_script_ad_anelli_con_supporto_nvidia:)
*   [6 Una nota inerente i caratteri simbolici](#Una_nota_inerente_i_caratteri_simbolici)
*   [7 Universal method to enable true transparency](#Universal_method_to_enable_true_transparency)
*   [8 Collegamenti esterni](#Collegamenti_esterni)

## Installazione & Configurazione

*   Conky è fornito dal repo extra di pacman

```
# pacman -S conky

```

*   Editare il file di configurazione usandone uno di esempio reperibile su [homeproject-screenshot](http://conky.sourceforge.net/screenshots.html)

```
$ nano ~/.conkyrc

```

*   In alternativa, è possibile utilizzare la configurazione di default presente in `/etc/conky/conky.conf`:

```
$ cp /etc/conky/conky.conf ~/.conkyrc

```

## Pacchetti AUR

Oltre al pacchetto conky presente nei repository, in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") sono disponibili vari pacchetti con abilitate diverse opzioni extra di compilazione:

*   Installare [conky-cli](https://aur.archlinux.org/packages/conky-cli/) per le dipendenze della famiglia di caratteri sans di X11
*   Installare [conky-nvidia](https://aur.archlinux.org/packages/conky-nvidia/) per abilitare il supporto nvidia.
*   Installare [conky-lua](https://aur.archlinux.org/packages/conky-lua/) per abilitare il supporto lua.
*   Installare [conky-lua-nv](https://aur.archlinux.org/packages/conky-lua-nv/) per abilitare il supporto nvidia e lua.

## Suggerimenti

### Abilitare la transparenza vera (KDE4)

Dalla versione 1.8.0 conky suppporta la transparenza vera. Per abilitarla (e farla funzionare bene con KDE4), aggiungere le seguenti righe a `~/.conkyrc`:

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type normal
own_window_class conky-semi
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

Si rimpiazzerà così il metodo feh descritto in seguito.

### Prevenire lo sfarfallio

Conky necessita del supporto Double Buffer Extension (DBE) del server X per prevenire lo sfarfallio, perchè non può aggiornarsi abbastanza velocemente senza di esso. Può essere abilitato tramite `/etc/X11/xorg.conf` dalla riga `Load "dbe"` in `Section "Module"`. Il file xorg.conf è stato sostituito (patch 1.8.x) da `/etc/X11/xorg.conf.d` che contiene file di configurazioni particolari. *DBE* è caricato automaticamente.

Per verificarlo:

```
# grep dbe /var/log/Xorg.0.log

```

L'output (si dovrebbe ottenere qualcosa di simile):

```
# [    86.101] (II) LoadModule: "dbe"
# [    86.101] (II) Loading /usr/lib/xorg/modules/extensions/libdbe.so
# [    86.111] (II) Module dbe: vendor="X.Org Foundation"

```

Per abilitare il double-buffer assicurarsi di avere in `~/.conkyrc`:

```
# Place below the other options, not below TEXT or XY
double_buffer yes

```

### Non minimizzare quando si abilita Mostra Desktop (Compiz)

Se premendo "Mostra Desktop" oppure la scorciatoia da tastiera conky viene minimizzato insieme a tutte le altre finestre, aprire il gestore delle impostazioni di compiz, andare su Opzioni Generali e deselezionare l'opzione "Hide Skip Taskbar Windows".

### Integrazione con KDesktop

Conky con la configurazione screenshot di default causa problemi con la visualizzazione delle icone sul desktop. Per evitarlo basta seguire questi semplici passi:

*   Aggiungere queste righe a `~/.conkyrc`:

```
own_window yes
own_window_type normal
own_window_transparent yes
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

*   Controllare di non avere questa impostazione cancellando la linea o commentandola

```
minimum_size

```

*   Creare questo link simbolico per avere conky al login

```
$ ln -s /usr/bin/conky ~/.kde/share/autostart/conkylink

```

Per KDE4

```
$ ln -s /usr/bin/conky ~/.kde4/Autostart/conkylink

```

*   Installare feh

```
# pacman -S feh

```

*   Creare uno script per abilitare la trasparenza al desktop

Per KDE3

```
$ nano -w ~/.kde/share/autostart/fehconky 

```

```
#!/bin/bash
feh --bg-scale `dcop kdesktop KBackgroundIface currentWallpaper 1`

```

Per KDE4

```
$ nano -w ~/.kde4/Autostart/fehconky

```

```
#!/bin/bash
feh --bg-scale "`grep 'wallpaper=' ~/.kde4/share/config/plasma-desktop-appletsrc | tail --lines=1 | sed 's/wallpaper=//'`"

```

utilizzare `--bg-center` se si utilizza un wallpaper centrato.

*   Renderlo eseguibile

```
$ chmod +x ~/.kde/share/autostart/fehconky

```

KDE4

```
$ chmod +x ~/.kde4/Autostart/fehconky

```

*   In alternativa, anzichè utilizzare uno script, è possibile aggiungere la linea corrispondente alla fine di `.conkyrc`

```
$ nano ~/.conkyrc

```

Per KDE3

```
${exec feh --bg-scale `dcop kdesktop KBackgroundIface currentWallpaper 1`}

```

Per KDE4

```
${exec feh --bg-scale "`grep 'wallpaper=' ~/.kde4/share/config/plasma-desktop-appletsrc | tail --lines=1 | sed 's/wallpaper=//'`"}

```

### Visualizzare informazioni di aggiornamento del pacchetto

*   [Paconky](https://bbs.archlinux.org/viewtopic.php?id=68104) - Visualizza informazioni inerenti l'aggiornamento di un pacchetto in un formato definito dall'utente. L'output di questo comando può essere incluso in Conky con il comando ${execpi}.
*   [Scrolling Notifications](https://bbs.archlinux.org/viewtopic.php?id=53761) - Visualizza le notifiche degli aggiornamenti e supporta lo scroll. Dall'autore di Paconky.
*   [Perl Script](https://bbs.archlinux.org/viewtopic.php?id=57291) - Semplice script dell'autore di Paconky. Visualizza solamente il numero dei pacchetti da aggiornare.
*   [Python Script](https://bbs.archlinux.org/viewtopic.php?id=37284) - Notificatore di aggiornamenti scritto in Python ed abbastanza configurabile.
*   [Bash Script](https://bbs.archlinux.org/viewtopic.php?pid=483742#p483742) - Script in Bash per utenti che hanno abilitato ShowSize.

### Visualizzazione previsioni meteo

Vedere [questa discussione](https://bbs.archlinux.org/viewtopic.php?id=37381).

### Visualizzazione feed RSS

Conky ha la possibilità di visualizzare i feed RSS in modo nativo, senza bisogno di eseguire uno script esterno. Ad esempio, per visualizzare i titoli degli ultimi dieci aggiornamenti del Planet di Arch Linux ed aggiornare il feed ogni minuto aggiungere nel proprio `.conkyrc` quanto segue:

```
${rss [https://planet.archlinux.org/rss20.xml](https://planet.archlinux.org/rss20.xml) 1 item_titles 10 }

```

### Visualizzazione ranking Arch Linux su Distrowatch

Vedere [questa discussione](https://bbs.archlinux.org/viewtopic.php?id=88779).

### Visualizzazione rTorrent

Vedere [questa discussione](https://bbs.archlinux.org/viewtopic.php?id=67304).

### Visualizzazione numero di nuove email (GMail)

Creare, in una directory a piacere (nell'esempio si userà `~/.scripts/`), un file chiamato `gmail.py` contenente il seguente codice Python:

```
import os

#Enter your username and password below within double quotes
# eg. username="username" and password="password"
username="****"
password="****"
com="wget -q -O - https://"+username+":"+password+"@mail.google.com/mail/feed/atom --no-check-certificate"

temp=os.popen(com)
msg=temp.read()
index=msg.find("<fullcount>")
index2=msg.find("</fullcount>")
fc=int(msg[index+11:index2])

if fc==0:
   print "0 new"
else:
   print str(fc)+" new"

```

Lo script su riportato non funziona con l'account Google Apps. Occorre quindi modificare il codice [Python](/index.php/Python "Python") come segue:

```
import os

#Enter your domain, username and password below within double quotes
# eg. domain="yourdomain.com", username="username" and password="password"
domain="yourdomain.com"
username="username"
password="password"
com="wget -q -O - [https://mail.google.com/a/](https://mail.google.com/a/)"+domain+"/feed/atom --http-user="+username+"@"+domain+" --http-password="+password+" --no-check-certificate"

temp=os.popen(com)
msg=temp.read()
index=msg.find("<fullcount>")
index2=msg.find("</fullcount>")
fc=int(msg[index+11:index2])

if fc==0:
   print "0 new"
else:
   print str(fc)+" new"

```

Con versioni inferiori di Python3, gli scripts precedenti riporteranno un errore relativo al print. Per risolvere, apportare questa modifica:

```
if fc==0:
   print ("0 new")
else:
   print (str(fc)+" new")

```

Per controllare l'arrivo di nuove mail ogni cinque minuti (300 secondi), aggiungere al proprio `.conkyrc` la seguente stringa: *# new*

```
${execpi 300 python ~/.scripts/gmail.py}

```

In alternativa, è possibile utilizzare [stunnel](http://www.stunnel.org/).

```
pacman -S stunnel

```

La seguente configurazione è presa dalle [FAQ di conky](http://conky.sourceforge.net/faq.html)

Modificare /etc/stunnel/stunnel.conf:

```
# Service-level configuration for TLS server
[imap]
client = yes
accept  = 143
connect = imap.gmail.com:143
protocol = imap
sslVersion = TLSv1
# Service-level configuration for SSL server
[imaps]
client = yes
accept  = 993
connect = imap.gmail.com:993

```

...ed avviare stunnel:

```
rc.d start stunnel

```

Ora non resta che conkyrc:

```
imap localhost username * -i 120 -p 993
TEXT
Inbox: ${imap_unseen}/${imap_messages}

```

In questo caso si è assunto * come password per l'avvio di conky, ma non è necessario *averne* una.

### Visualizzazione nuove email (IMAP + SSL)

Conky include il supporto per gli accounts IMAP, ma non supporta SSL. Si può ovviare utilizzando lo script presente in [questo post](http://www.unix.com/shell-programming-scripting/115322-perl-conky-gmail-imap-unread-message-count.html). Affinchè tutto funzioni, sono richiesti Perl/CPAN Modules Mail::IMAPClient e IO::Socket::SSL, presenti nei pacchetti perl-mail-imapclient e perl-io-socket-ssl

Creare un file chiamato imap.pl. Aggiungere al suo interno (apportando le opportune modifiche):

```
#!/usr/bin/perl

# gimap.pl by gxmsgx
# description: get the count of unread messages on imap

use strict;
use Mail::IMAPClient;
use IO::Socket::SSL;

my $username = 'example.username'; 
my $password = 'password123'; 

my $socket = IO::Socket::SSL->new(
  PeerAddr => 'imap.server',
  PeerPort => 993
 )
 or die "socket(): $@";

my $client = Mail::IMAPClient->new(
  Socket   => $socket,
  User     => $username,
  Password => $password,
 )
 or die "new(): $@";

if ($client->IsAuthenticated()) {
   my $msgct;

   $client->select("INBOX");
   $msgct = $client->unseen_count||'0';
   print "$msgct
";
}

$client->logout();

```

Aggiungere al file .conkyrc:

```
${execpi 300 ~/.conky/imap.pl} 

```

o la directory contenente il file.

In alternativa, è possibile utilizzare stunnel, come indicato sopra: [#Visualizzazione numero di nuove email (GMail)](#Visualizzazione_numero_di_nuove_email_.28GMail.29)

## Contributo-Utenti Configurazioni d'esempio

### Graysky

[Screen shot](http://img9.imageshack.us/img9/3153/imageffj.jpg)

[Disponibile qui](https://github.com/graysky2/configs/raw/master/dotfiles/.conkyrc) - modificarlo per adattarlo al proprio sistema. Ottimizzato per chip quad core w/ e numerosi hdds (anche se uno di essi non è collegato nello screenshot) ed una scheda grafica nvidia. E' possibile modificare facilmente a dual o single core con uno o un qualunque altro numero di hdds.

## Un semplice script ad anelli con supporto nvidia:

```
1 # -- Conky settings -- #
 2 background no
 3 update_interval 1
 4 
 5 cpu_avg_samples 2
 6 net_avg_samples 2
 7 
 8 override_utf8_locale yes
 9 
10 double_buffer yes
11 no_buffers yes
12 
13 text_buffer_size 2048
14 imlib_cache_size 0
15 
16 # -- Window specifications -- #
17 
18 own_window yes
19 own_window_type normal
20 own_window_transparent yes
21 own_window_hints undecorate,sticky,skip_taskbar,skip_pager,below
22 
23 border_inner_margin 0
24 border_outer_margin 0
25 
26 minimum_size 320 800
27 maximum_width 320
28 
29 alignment bottom_right
30 gap_x 0
31 gap_y 0
32 
33 # -- Graphics settings -- #
34 draw_shades no
35 draw_outline no
36 draw_borders no
37 draw_graph_borders yes
38 
39 # -- Text settings -- #
40 use_xft yes
41 xftfont MaiandraGD:size=24
42 xftalpha 0.4
43 
44 uppercase no
45 
46 default_color 888888
47 
48 # -- Lua Load -- #
49 lua_load ~/conky/lua/lua.lua
50 lua_draw_hook_pre ring_stats
51 
52 TEXT
53 ${alignr}${voffset 53}${goto 90}${font MaiandraGD:size=11}${time %A, %d %B %Y}
54 
55 
56 ${voffset 5}${goto 164}${font MaiandraGD:size=16}${time %H:%M}
57 
58 
59 
60 ${voffset -40}${goto 100}${font MaiandraGD:size=9}Kernel:${offset 70}Uptime:
61 ${goto 90}${font MaiandraGD:size=9}$kernel${offset 40}$uptime
62 ${voffset 57}${goto 117}${font snap:size=8}${cpu cpu0}%
63 ${goto 117}${cpu cpu1}%
64 ${goto 117}CPU
65 ${voffset 19}${goto 145}${memperc}%
66 ${goto 145}$swapperc%
67 ${goto 145}MEM
68 ${voffset 25}${goto 170}${nvidia gpufreq}
69 ${goto 170}${nvidia memfreq}
70 ${goto 170}GPU
71 ${voffset 27}${goto 198}${totaldown ppp0}
72 ${goto 198}${totalup ppp0}
73 ${goto 205}NET
74 ${voffset 21}
75 ${goto 222}${fs_used /home}
76 ${goto 230}DISK

```

*   Ed il relativo script lua.lua:

```
1 --[[
  2 Ring Meters by londonali1010 (2009)
  3  
  4 This script draws percentage meters as rings. It is fully customisable; all options are described in the script.
  5  
  6 IMPORTANT: if you are using the 'cpu' function, it will cause a segmentation fault if it tries to draw a ring straight away. The if s    tatement on line 145 uses a delay to make sure that this does not happen. It calculates the length of the delay by the number of updat    es since Conky started. Generally, a value of 5s is long enough, so if you update Conky every 1s, use update_num > 5 in that if state    ment (the default). If you only update Conky every 2s, you should change it to update_num > 3; conversely if you update Conky every 0    .5s, you should use update_num > 10\. ALSO, if you change your Conky, is it best to use "killall conky; conky" to update it, otherwise     the update_num will not be reset and you will get an error.
  7  
  8 To call this script in Conky, use the following (assuming that you save this script to ~/scripts/rings.lua):
  9         lua_load ~/scripts/rings-v1.2.1.lua
 10         lua_draw_hook_pre ring_stats
 11  
 12 Changelog:
 13 + v1.2.1 -- Fixed minor bug that caused script to crash if conky_parse() returns a nil value (20.10.2009)
 14 + v1.2 -- Added option for the ending angle of the rings (07.10.2009)
 15 + v1.1 -- Added options for the starting angle of the rings, and added the "max" variable, to allow for variables that output a numer    ical value rather than a percentage (29.09.2009)
 16 + v1.0 -- Original release (28.09.2009)
 17 ]]
 18 
 19 settings_table = {
 20         {
 21                 -- Edit this table to customise your rings.
 22                 -- You can create more rings simply by adding more elements to settings_table.
 23                 -- "name" is the type of stat to display; you can choose from 'cpu', 'memperc', 'fs_used_perc', 'battery_used_perc'.
 24                 name='time',
 25                 -- "arg" is the argument to the stat type, e.g. if in Conky you would write ${cpu cpu0}, 'cpu0' would be the argument    . If you would not use an argument in the Conky variable, use *.*
 26                 arg='%I.%M',
 27                 -- "max" is the maximum value of the ring. If the Conky variable outputs a percentage, use 100.
 28                 max=12,
 29                 -- "bg_colour" is the colour of the base ring.
 30                 bg_colour=0x888888,
 31                 -- "bg_alpha" is the alpha value of the base ring.
 32                 bg_alpha=0.3,
 33                 -- "fg_colour" is the colour of the indicator part of the ring.
 34                 fg_colour=0x888888,
 35                 -- "fg_alpha" is the alpha value of the indicator part of the ring.
 36                 fg_alpha=0.5,
 37                 -- "x" and "y" are the x and y coordinates of the centre of the ring, relative to the top left corner of the Conky wi    ndow.
 38                 x=191, y=145,
 39                 -- "radius" is the radius of the ring.
 40                 radius=32,
 41                 -- "thickness" is the thickness of the ring, centred around the radius.
 42                 thickness=4,
 43                 -- "start_angle" is the starting angle of the ring, in degrees, clockwise from top. Value can be either positive or n    egative.
 44                 start_angle=0,
 45                 -- "end_angle" is the ending angle of the ring, in degrees, clockwise from top. Value can be either positive or negat    ive, but must be larger (e.g. more clockwise) than start_angle.
 46                 end_angle=360
 47         },
 48         {
 49                 name='time',
 50                 arg='%M.%S',
 51                 max=60,
 52                 bg_colour=0x888888,
 53                 bg_alpha=0.3,
 54                 fg_colour=0x888888,
 55                 fg_alpha=0.5,
 56                 x=191, y=145,
 57                 radius=37,
 58                 thickness=4,
 59                 start_angle=0,
 60                 end_angle=360
 61         },
 62         {
 63                 name='time',
 64                 arg='%S',
 65                 max=60,
 66                 bg_colour=0x888888,
 67                 bg_alpha=0.3,
 68                 fg_colour=0x888888,
 69                 fg_alpha=0.5,
 70                 x=191, y=145,
 71                 radius=42,
 72                 thickness=4,
 73                 start_angle=0,
 74                 end_angle=360
 75         },
 76         {
 77                 name='cpu',
 78                 arg='cpu0',
 79                 max=100,
 80                 bg_colour=0x888888,
 81                 bg_alpha=0.3,
 82                 fg_colour=0x888888,
 83                 fg_alpha=0.5,
 84                 x=140, y=300,
 85                 radius=26,
 86                 thickness=5,
 87                 start_angle=-90,
 88                 end_angle=180
 89         },
 90         {
 91                 name='cpu',
 92                 arg='cpu1',
 93                 max=100,
 94                 bg_colour=0x888888,
 95                 bg_alpha=0.3,
 96                 fg_colour=0x888888,
 97                 fg_alpha=0.5,
 98                 x=140, y=300,
 99                 radius=20,
100                 thickness=5,
101                 start_angle=-90,
102                 end_angle=180
103         },
104         {
105                 name='memperc',
106                 arg=*,*
107                 max=100,
108                 bg_colour=0x888888,
109                 bg_alpha=0.3,
110                 fg_colour=0x888888,
111                 fg_alpha=0.5,
112                 x=170, y=350,
113                 radius=26,
114                 thickness=5,
115                 start_angle=-90,
116                 end_angle=180
117         },
118         {
119                 name='swapperc',
120                 arg=*,*
121                 max=100,
122                 bg_colour=0x888888,
123                 bg_alpha=0.3,
124                 fg_colour=0x888888,
125                 fg_alpha=0.5,
126                 x=170, y=350,
127                 radius=20,
128                 thickness=5,
129                 start_angle=-90,
130                 end_angle=180
131         },
132         {
133                 name='time',
134                 arg='%d',
135                 max=31,
136                 bg_colour=0x888888,
137                 bg_alpha=0.3,
138                 fg_colour=0x888888,
139                 fg_alpha=0.5,
140                 x=191, y=145,
141                 radius=50,
142                 thickness=5,
143                 start_angle=-140,
144                 end_angle=-30
145         },
146         {
147                 name='time',
148                 arg='%m',
149                 max=12,
150                 bg_colour=0x888888,
151                 bg_alpha=0.3,
152                 fg_colour=0x888888,
153                 fg_alpha=0.5,
154                 x=191, y=145,
155                 radius=50,
156                 thickness=5,
157                 start_angle=30,
158                 end_angle=140
159         },
160 --      {
161 --              name='fs_used_perc',
162 --              arg='/',
163 --              max=100,
164 --              bg_colour=0x888888,
165 --              bg_alpha=0.3,
166 --              fg_colour=0x888888,
167 --              fg_alpha=0.5,
168 --              x=260, y=503,
169 --              radius=26,
170 --              thickness=5,
171 --              start_angle=-90,
172 --              end_angle=180
173 --      },
174         {
175                 name='fs_used_perc',
176                 arg='/home',
177                 max=100,
178                 bg_colour=0x888888,
179                 bg_alpha=0.3,
180                 fg_colour=0x888888,
181                 fg_alpha=0.5,
182                 x=260, y=503,
183                 radius=20,
184                 thickness=5,
185                 start_angle=-90,
186                 end_angle=180
187         },
188         {
189                 name='totalup',
190                 arg='ppp0',
191                 max=2,
192                 bg_colour=0x888888,
193                 bg_alpha=0.3,
194                 fg_colour=0x888888,
195                 fg_alpha=0.5,
196                 x=230, y=452,
197                 radius=20,
198                 thickness=5,
199                 start_angle=-90,
200                 end_angle=180
201         },
202         {
203                 name='totaldown',
204                 arg='ppp0',
205                 max=2,
206                 bg_colour=0x888888,
207                 bg_alpha=0.3,
208                 fg_colour=0x888888,
209                 fg_alpha=0.5,
210                 x=230, y=452,
211                 radius=26,
212                 thickness=5,
213                 start_angle=-90,
214                 end_angle=180
215         },
216         {
217                 name='nvidia',
218                 arg='gpufreq',
219                 max=475,
220                 bg_colour=0x888888,
221                 bg_alpha=0.3,
222                 fg_colour=0x888888,
223                 fg_alpha=0.5,
224                 x=200, y=401,
225                 radius=26,
226                 thickness=5,
227                 start_angle=-90,
228                 end_angle=180
229         },
230 {
231                 name='nvidia',
232                 arg='memfreq',
233                 max=700,
234                 bg_colour=0x888888,
235                 bg_alpha=0.3,
236                 fg_colour=0x888888,
237                 fg_alpha=0.5,
238                 x=200, y=401,
239                 radius=20,
240                 thickness=5,
241                 start_angle=-90,
242                 end_angle=180
243         },
244 }
245 
246 require 'cairo'
247 
248 function rgb_to_r_g_b(colour,alpha)
249         return ((colour / 0x10000) % 0x100) / 255., ((colour / 0x100) % 0x100) / 255., (colour % 0x100) / 255., alpha
250 end
251 
252 function draw_ring(cr,t,pt)
253         local w,h=conky_window.width,conky_window.height
254 
255         local xc,yc,ring_r,ring_w,sa,ea=pt['x'],pt['y'],pt['radius'],pt['thickness'],pt['start_angle'],pt['end_angle']
256         local bgc, bga, fgc, fga=pt['bg_colour'], pt['bg_alpha'], pt['fg_colour'], pt['fg_alpha']
257 
258         local angle_0=sa*(2*math.pi/360)-math.pi/2
259         local angle_f=ea*(2*math.pi/360)-math.pi/2
260         local t_arc=t*(angle_f-angle_0)
261 
262         -- Draw background ring
263 
264         cairo_arc(cr,xc,yc,ring_r,angle_0,angle_f)
265         cairo_set_source_rgba(cr,rgb_to_r_g_b(bgc,bga))
266         cairo_set_line_width(cr,ring_w)
267         cairo_stroke(cr)
268 
269         -- Draw indicator ring
270 
271         cairo_arc(cr,xc,yc,ring_r,angle_0,angle_0+t_arc)
272         cairo_set_source_rgba(cr,rgb_to_r_g_b(fgc,fga))
273         cairo_stroke(cr)
274 end
275 
276 function conky_ring_stats()
277         local function setup_rings(cr,pt)
278                 local str=
279                 local value=0
280 
281                 str=string.format('${%s %s}',pt['name'],pt['arg'])
282                 str=conky_parse(str)
283 
284                 value=tonumber(str)
285                 if value == nil then value = 0 end
286                 pct=value/pt['max']
287 
288                 draw_ring(cr,pct,p<nowiki>Insert non-formatted text here'''Bold text'''</nowiki>t)
289         end
290 
291         if conky_window==nil then return end
292         local cs=cairo_xlib_surface_create(conky_window.display,conky_window.drawable,conky_window.visual, conky_window.width,conky_w    indow.height)
293 
294         local cr=cairo_create(cs)
295 
296         local updates=conky_parse('${updates}')
297         update_num=tonumber(updates)
298 
299         if update_num>5 then
300                 for i in pairs(settings_table) do
301                         setup_rings(cr,settings_table[i])
302                 end
303         end
304 end
~
```

## Una nota inerente i caratteri simbolici

La maggior parte delle decorazioni presenti nei .conkyrc's utilizzano i caratteri PizzaDude Bullets e Pie Charts for Maps. Essi sono disponibili in AUR, rispettivamente, come 'ttf-pizzadude-bullets' e 'ttf-piechartsformaps', oopure possono essere trovati e scaricati con una rapida ricerca e installati manualmente seguendo le istruzioni presenti in [Fonts](/index.php/Fonts_(Italiano) "Fonts (Italiano)").

## Universal method to enable true transparency

La trasparenza è ostica da impostare in Conky, ma c'è un metodo universale per applicare la vera trasparenza con qualsiasi ambiente desktop e gestore di finestre, ossia utilizzando xcompmgr e transset-df. Installare xcompmgr da [extra] e transset-df da [community] con `pacman -Sy xcompmgr transset-df`. Questi pacchetti richiedono le stesse dipendenze, perciò questo è il metodo più leggero per abilitare l'effetto ed è anche, per coloro che utilizzano un gestore di finestre standalone, il più gestibile.

NOTA: Questo potrebbe andare in conflitto con un altro compositing manager già in uso.

Controllare la documentazione di xcompmgr per ottenere informazioni inerenti le opzioni di composite da abilitare. Quanto segue è un comando standard usato comunemente.

```
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &

```

Assicurarsi che Conky sia avviato con `conky &`. Utilizzare transset-df per abilitare la trasparenza sulla finestra di Conky. Impostare '.5' ad ogni valore del range 0 - 1.

```
transset-df .5 -n Conky

```

Ciò dovrebbe attivare la trasparenza in Conky. Se si ottiene un errore del genere,

 `$ transset-df .5 -n Conky`  `No Window matching Conky exists!` 

Verificare che conky sia in esecuzione, utilizzare xprop e cliccare sulla finestra di conky per trovare il nome che si vuole processare con `transset-df`.

 `$ xprop | grep WM_NAME`  `WM_NAME(STRING) = "Conky (ArchitectLinux)"` 

In questo caso, "Conky" è impostato correttamente, ma ciò potrebbe non funzionare su ogni sistema, quindi assicurarsi di utilizzare il valore restituito dal proprio aoutput. Se ~/.conkyrc ha `own_window_type panel` allora l'invocazione di xprop potrebbe mostrare un output. Provare ad utilizzare una delle seguenti opzioni. `own_window_type {dock,normal,override,desktop`}

Aggiungere quanto segue al file ~/.xinitrc pre rendere conky trasparente quando si esegue `startx`.

```
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &
conky -d; sleep 1 && transset-df .5 -n Conky

```

## Collegamenti esterni

*   [Configurazioni di conky sul forum di Arch](https://bbs.archlinux.org/viewtopic.php?id=39906)
*   [Sito ufficiale](http://conky.sourceforge.net/)
*   [Conky](http://freshmeat.net/projects/conky/) su [Freshmeat](https://en.wikipedia.org/wiki/Freshmeat "wikipedia:Freshmeat")
*   [Conky](http://sourceforge.net/projects/conky/) su [SourceForge](https://en.wikipedia.org/wiki/sourceforge.net "wikipedia:sourceforge.net")
*   [#conky](irc://chat.freenode.org/conky) Canale IRC su [freenode](https://en.wikipedia.org/wiki/Freenode "wikipedia:Freenode")
*   [FAQ](http://novel.evilcoder.org/wiki/index.php?title=ConkyFAQ&oldid=12463)