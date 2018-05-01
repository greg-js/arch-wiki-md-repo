Conky es un monitor de sistema para los sistemas X Window. Está disponible para GNU/Linux y FreeBSD. Es un software libre liberado bajo los términos de la licencia GPL. Conky es capaz de monitorear distintas variables de sistema, incluyendo CPU, memoria, swap, espacio de disco, temperaturas, subidas, bajadas, mensajes de sistema, y mucho más. Es completamente configurable, la configuración puede ser un poco difícil de entender, pero es bastante posible realizarla. Conky es un *fork* de torsmo.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Consejos y trucos](#Consejos_y_trucos)
    *   [2.1 Habilitar transparecian real (KDE4)](#Habilitar_transparecian_real_.28KDE4.29)
    *   [2.2 Evitar el parpadeo](#Evitar_el_parpadeo)
    *   [2.3 Integrar con KDesktop](#Integrar_con_KDesktop)
    *   [2.4 Visualizar información de actualización de paquetes](#Visualizar_informaci.C3.B3n_de_actualizaci.C3.B3n_de_paquetes)
    *   [2.5 Mostrar Weather Forecast](#Mostrar_Weather_Forecast)
    *   [2.6 Mostrar RSS feeds](#Mostrar_RSS_feeds)
    *   [2.7 Mostrar ranking Distrowatch Arch Linux](#Mostrar_ranking_Distrowatch_Arch_Linux)
    *   [2.8 Mostrar estadísticas rTorrent](#Mostrar_estad.C3.ADsticas_rTorrent)
    *   [2.9 Mostrar numero de correos nuevos (GMail)](#Mostrar_numero_de_correos_nuevos_.28GMail.29)
    *   [2.10 Mostrar correos nuevos (IMAP + SSL)](#Mostrar_correos_nuevos_.28IMAP_.2B_SSL.29)
*   [3 Contribución de usuarios con ejemplos de configuración](#Contribuci.C3.B3n_de_usuarios_con_ejemplos_de_configuraci.C3.B3n)
    *   [3.1 Graysky](#Graysky)
*   [4 Un ejemplo de los anillos con soporte nVidia](#Un_ejemplo_de_los_anillos_con_soporte_nVidia)
*   [5 Una nota sobre fuentes simbólicas](#Una_nota_sobre_fuentes_simb.C3.B3licas)
*   [6 Enlaces externos](#Enlaces_externos)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [conky](https://www.archlinux.org/packages/?name=conky) de los repositorios oficiales. También hay varios paquetes disponibles en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") con opciones extras de compilación disponibles.

*   Instalar [conky-cli](https://aur.archlinux.org/packages/conky-cli/) para dependencias conky sans X11.
*   Instalar [conky-nvidia](https://aur.archlinux.org/packages/conky-nvidia/) para soporte nVidia.
*   Instalar [conky-lua](https://aur.archlinux.org/packages/conky-lua/) para soporte lua.
*   Instalar [conky-lua-nv](https://aur.archlinux.org/packages/conky-lua-nv/) para soporte de ambos (lua, nVidia).

Algunas variables incluidas en conky requieren paquetes adicionales para ser utilizados, por ejemple [Hddtemp](/index.php/Hddtemp "Hddtemp") para la temperatura del disco duro y [MPD](/index.php/Music_Player_Daemon_(Espa%C3%B1ol) "Music Player Daemon (Español)") para música.

## Consejos y trucos

### Habilitar transparecian real (KDE4)

Desde la versión 1.8.0, conky soporta transparencias reales. Para habilitarlo (y hacerlo trabajar correctamente con KDE4), hay que agregar las siguientes líneas a `~/.conkyrc`:

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type normal
own_window_class conky-semi
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

Esto reemplaza los métodos [feh](https://www.archlinux.org/packages/?name=feh) descritos a continuación.

### Evitar el parpadeo

Conky necesita soporte Doble de extensión de buffer (DBE) desde el servidor X para prevenir el parpadeo, porque no puede actualizar rápidamente la pantalla sin esto. Esto puede ser activado en `/etc/X11/xorg.conf` con `Load "dbe"` línea en `Section "Module"`. El archivo xorg.conf ha sido reemplazado (1.8.x actualización de patch) por `/etc/X11/xorg.conf.d`, que contiene una configuración particular de los archivos. *DBE* se carga automáticamente.

Para verificar:

```
# cat /var/log/Xorg.0.log | grep dbe

```

Salida (debería ser similar):

```
# [    86.101] (II) LoadModule: "dbe"
# [    86.101] (II) Loading /usr/lib/xorg/modules/extensions/libdbe.so
# [    86.111] (II) Module dbe: vendor="X.Org Foundation"

```

Para activar el buffer-doble verificar de tener en `~/.conkyrc`:

```
# Place below the other options, not below TEXT or XY
double_buffer yes

```

### Integrar con KDesktop

Conky con configuración de impresión de pantalla genera problemas con la visualización de iconos. Se deben seguir ciertos pasos.

*   Agregar estas líneas a `~/.conkyrc`:

```
own_window yes
own_window_type normal
own_window_transparent yes
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

*   Si esta configuración esta activada, comentarla o eliminar la línea:

```
minimum_size

```

*   Para iniciar automáticamente conky crear el siguiente enlace:

```
$ ln -s /usr/bin/conky ~/.kde/share/autostart/conkylink

```

Para usuarios KDE4

```
$ ln -s /usr/bin/conky ~/.kde4/Autostart/conkylink

```

*   Instalar feh:

```
# pacman -S feh

```

*   Hacer un script que permita la transparencia con el escritorio:

Para usuarios KDE3

```
$ nano -w ~/.kde/share/autostart/fehconky 

```

```
#!/bin/bash
feh --bg-scale `dcop kdesktop KBackgroundIface currentWallpaper 1`

```

Para usuarios KDE

```
$ nano -w ~/.kde4/Autostart/fehconky

```

```
#!/bin/bash
feh --bg-scale "`grep 'wallpaper=' ~/.kde4/share/config/plasma-desktop-appletsrc | tail --lines=1 | sed 's/wallpaper=//'`"

```

Utilizar `--bg-center` si se usa un fondo de pantalla centrado.

*   Hacerlo ejecutable:

```
$ chmod +x ~/.kde/share/autostart/fehconky

```

KDE4

```
$ chmod +x ~/.kde4/Autostart/fehconky

```

*   Opcionalmente, en vez de usar un script se puede agregar la siguiente línea correspondiente al final de `.conkyrc`:

```
$ nano ~/.conkyrc:

```

Para KDE3

```
${exec feh --bg-scale `dcop kdesktop KBackgroundIface currentWallpaper 1`}

```

Para KDE4

```
${exec feh --bg-scale "`grep 'wallpaper=' ~/.kde4/share/config/plasma-desktop-appletsrc | tail --lines=1 | sed 's/wallpaper=//'`"}

```

### Visualizar información de actualización de paquetes

*   [Paconky](https://bbs.archlinux.org/viewtopic.php?id=68104) - Muestra información de actualizaciones de paquetes en un formato usario-definido. La salida de este programa puede ser incluida en Conky con el comando ${execpi}.
*   [Scrolling Notifications](https://bbs.archlinux.org/viewtopic.php?id=53761) - Imprime notificaciones de actualizaciones de desplazamiento. Del autor de Paconky.
*   [Perl Script](https://bbs.archlinux.org/viewtopic.php?id=57291) - Línea de comandos anterior y simple del autor de Paconky. Imprime solo la cantidad de paquetes necesarios para actualizar.
*   [Python Script](https://bbs.archlinux.org/viewtopic.php?id=37284) - Programa de notificaciones de actualización bastante configurable en Python.
*   [Bash Script](https://bbs.archlinux.org/viewtopic.php?pid=483742#p483742) - Bash script para usuarios que han habilitado ShowSize.

### Mostrar Weather Forecast

Mirar [este enlace](https://bbs.archlinux.org/viewtopic.php?id=37381).

### Mostrar RSS feeds

Conky tiene la habilidad de mostrar RSS feeds nativamente sin la necesidad de un script ajeno para ejecutar una salida en conky. Por ejemplo, para mostrar los títulos de las diez actualizaciones más recientes de Planeta Arch y refrescar el feed cada minuto, se debe insertar dentro del archivo `.conkyrc`:

```
${rss [https://planet.archlinux.org/rss20.xml](https://planet.archlinux.org/rss20.xml) 1 item_titles 10 }

```

### Mostrar ranking Distrowatch Arch Linux

Mirar [este enlace](https://bbs.archlinux.org/viewtopic.php?id=88779).

### Mostrar estadísticas rTorrent

Mirar [este enlace](https://bbs.archlinux.org/viewtopic.php?id=67304).

### Mostrar numero de correos nuevos (GMail)

Crear un archivo con nombre `gmail.py` en la ubicación conveniente (este ejemplo usa `~/.scripts/`) con el siguiente código [Python](/index.php/Python "Python"):

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

Si la secuencia de comandos anterior no funciona para ti y tu cuenta de Google Apps, puedes modificar el script siquiente para que funcione con una cuenta de correo Google App, en código [Python](/index.php/Python "Python"):

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

Agregar la siguiente línea de comandos a tu `.conky` para verificar tu cuenta de correo Gmail por correo nuevo cada 5 minutos (300 segundos) y mostrar: *# new*

```
${execpi 300 python ~/.scripts/gmail.py}

```

Alternativamente se puede usar [stunnel](http://www.stunnel.org/).

```
pacman -S stunnel

```

La siguiente configuración está tomada desde las [Preguntas frecuentes de Conky](http://conky.sourceforge.net/faq.html).

Modificar /etc/stunnel/stunnel.conf:

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

E iniciar stunnel:

```
/etc/rc.d/stunnel start

```

Lo único que queda es el conkyrc:

```
imap localhost username * -i 120 -p 993
TEXT
Inbox: ${imap_unseen}/${imap_messages}

```

Aquí uso * como la contraseña de conky para preguntar al inicio, pero tú no *necesitas* hacerlo.

### Mostrar correos nuevos (IMAP + SSL)

Conky tiene soporte para cuentas IMAP, pero no soporta SSL. Esto se puede proveer utilizando la siguiente línea de comando tomada [este de esta publicación en un foro](http://www.unix.com/shell-programming-scripting/115322-perl-conky-gmail-imap-unread-message-count.html). Esto requiere los modulos Perl/CPAN Mail::IMAPClient e IO::Socket::SSL que están en los paquetes perl-mail-imapclient y perl-io-socket-ssl.

Crear un archivo llamado imap.pl en una ubicación para ser leída por conky. En este archivo agregar (con los cambios correspondientes):

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

Agregar a .conkyrc:

```
${execpi 300 ~/.conky/imap.pl} 

```

o donde se haya guardado el archivo.

Alternativamente, se puede usar stunnel como se muestra en: [Conky#How to display the number of new emails (Gmail) in Conky](/index.php/Conky#How_to_display_the_number_of_new_emails_.28Gmail.29_in_Conky "Conky").

## Contribución de usuarios con ejemplos de configuración

### Graysky

[Screen shot](http://img9.imageshack.us/img9/3153/imageffj.jpg)

[Aquí](https://github.com/graysky2/dotfiles/blob/master/.conkyrc) esto es - modificado para ajustarse a tu pantalla. Optimizado para un chip Quad Core con varios discos de almacenamiento (HDDs) (aunque uno de ellos no esta conectado para este screenshot) y una tarjeta de video nVidia. Se puede modificar fácilmente esto para un sistema dual-o-single core con cualquier numero de discos de almacenamiento (HHDs).

## Un ejemplo de los anillos con soporte nVidia

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

*   Y la línea de comandos lua.lua requerida:

```
 1 --[[
  2 Ring Meters by londonali1010 (2009)
  3  
  4 This script draws percentage meters as rings. It is fully customisable; all options are described in the script.
  5  
  6 IMPORTANT: if you are using the 'cpu' function, it will cause a segmentation fault if it tries to draw a ring straight away. 
The if statement on line 145 uses a delay to make sure that this doesn't happen. It calculates the length of the delay by the number 
of updates since Conky started. Generally, a value of 5s is long enough, so if you update Conky every 1s, use update_num > 5 in that 
if statement (the default). If you only update Conky every 2s, you should change it to update_num > 3; conversely if you update Conky 
every 0.5s, you should use update_num > 10\. ALSO, if you change your Conky, is it best to use "killall conky; conky" to update it, 
otherwise the update_num will not be reset and you will get an error.
  7  
  8 To call this script in Conky, use the following (assuming that you save this script to ~/scripts/rings.lua):
  9         lua_load ~/scripts/rings-v1.2.1.lua
 10         lua_draw_hook_pre ring_stats
 11  
 12 Changelog:
 13 + v1.2.1 -- Fixed minor bug that caused script to crash if conky_parse() returns a nil value (20.10.2009)
 14 + v1.2 -- Added option for the ending angle of the rings (07.10.2009)
 15 + v1.1 -- Added options for the starting angle of the rings, and added the "max" variable, to allow for variables that output a 
numerical value rather than a percentage (29.09.2009)
 16 + v1.0 -- Original release (28.09.2009)
 17 ]]
 18 
 19 settings_table = {
 20         {
 21                 -- Edit this table to customise your rings.
 22                 -- You can create more rings simply by adding more elements to settings_table.
 23                 -- "name" is the type of stat to display; you can choose from 'cpu', 'memperc', 'fs_used_perc', 'battery_used_perc'.
 24                 name='time',
 25                 -- "arg" is the argument to the stat type, e.g. if in Conky you would write ${cpu cpu0}, 'cpu0' would be the argument. 
If you would not use an argument in the Conky variable, use ''.
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
 37                 -- "x" and "y" are the x and y coordinates of the centre of the ring, relative to the top left corner of the Conky 
window.
 38                 x=191, y=145,
 39                 -- "radius" is the radius of the ring.
 40                 radius=32,
 41                 -- "thickness" is the thickness of the ring, centred around the radius.
 42                 thickness=4,
 43                 -- "start_angle" is the starting angle of the ring, in degrees, clockwise from top. Value can be either positive or 
negative.
 44                 start_angle=0,
 45                 -- "end_angle" is the ending angle of the ring, in degrees, clockwise from top. Value can be either positive or negative, 
but must be larger (e.g. more clockwise) than start_angle.
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
106                 arg='',
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
120                 arg='',
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
278                 local str=''
279                 local value=0
280 
281                 str=string.format('${%s %s}',pt['name'],pt['arg'])
282                 str=conky_parse(str)
283 
284                 value=tonumber(str)
285                 if value == nil then value = 0 end
286                 pct=value/pt['max']
287 
288                 draw_ring(cr,pct,pt)
289         end
290 
291         if conky_window==nil then return end
292         local cs=cairo_xlib_surface_create(conky_window.display,conky_window.drawable,conky_window.visual, conky_window.width,conky_window.height)
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

## Una nota sobre fuentes simbólicas

Muchos de los más decorados archivos *.conkyrc* usan las fuentes PizzaDude Bullets y Pie Charts para mapas. Están disponibles en el AUR como 'ttf-pizzadude-bullets' y 'ttf-piechartsformaps' respectivamente, o pueden ser hallados y descargados con una simple búsqueda he instalación manual usando las instrucciones en [Fonts](/index.php/Fonts "Fonts").

## Enlaces externos

*   [Configuraciones de Conkys en los foros de Arch](https://bbs.archlinux.org/viewtopic.php?id=39906)
*   [Página web oficial](http://conky.sourceforge.net/)
*   [Conky](http://freshmeat.net/projects/conky/) en [Freshmeat](https://en.wikipedia.org/wiki/Freshmeat "wikipedia:Freshmeat")
*   [Conky](http://sourceforge.net/projects/conky/) en [SourceForge](https://en.wikipedia.org/wiki/sourceforge.net "wikipedia:sourceforge.net")
*   [#conky](irc://chat.freenode.org/conky) Canal de chat IRC en [freenode](https://en.wikipedia.org/wiki/Freenode "wikipedia:Freenode")
*   [FAQ](http://novel.evilcoder.org/wiki/index.php/ConkyFAQ)