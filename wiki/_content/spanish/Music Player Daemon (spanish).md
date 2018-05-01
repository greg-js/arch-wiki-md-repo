Artículos relacionados

*   [MPD/Tips and Tricks](/index.php/MPD/Tips_and_Tricks "MPD/Tips and Tricks")
*   [MPD/Troubleshooting](/index.php/MPD/Troubleshooting "MPD/Troubleshooting")

**MPD** (Music Player Daemon) es un reproductor de audio que maneja una arquitectura servidor-cliente. MPD se ejecuta en el fondo como un daemon, gestiona listas de reproducción y una base de datos, y hace uso de muy pocos recursos. Para hacer uso de una interfaz gráfica, es necesario un cliente adicional. Más información puede obtenerse en su [página web](http://www.musicpd.org/).

## Contents

*   [1 Procedimiento de Instalación del Daemon](#Procedimiento_de_Instalaci.C3.B3n_del_Daemon)
*   [2 Instrucciones de Configuración](#Instrucciones_de_Configuraci.C3.B3n)
    *   [2.1 Linea de Tiempo del Comportamiento Habitual de MPD](#Linea_de_Tiempo_del_Comportamiento_Habitual_de_MPD)
    *   [2.2 Correcta Configuración de Sonido](#Correcta_Configuraci.C3.B3n_de_Sonido)
    *   [2.3 Configuracion General](#Configuracion_General)
    *   [2.4 Configuración Por Usuario](#Configuraci.C3.B3n_Por_Usuario)
    *   [2.5 Configuración Multi-MPD](#Configuraci.C3.B3n_Multi-MPD)
*   [3 Instalando Clientes para MPD](#Instalando_Clientes_para_MPD)
*   [4 Extra stuff](#Extra_stuff)
    *   [4.1 Envío de Canciones a Last.fm](#Env.C3.ADo_de_Canciones_a_Last.fm)
        *   [4.1.1 Mpdscribble](#Mpdscribble)
        *   [4.1.2 Sonata](#Sonata)
        *   [4.1.3 Lastfmsubmitd](#Lastfmsubmitd)
        *   [4.1.4 Reproducción Desde Last.fm](#Reproducci.C3.B3n_Desde_Last.fm)
            *   [4.1.4.1 Reproducción Nativa](#Reproducci.C3.B3n_Nativa)
            *   [4.1.4.2 Reproducir Desde Last.fm con Lastfmproxy](#Reproducir_Desde_Last.fm_con_Lastfmproxy)
    *   [4.2 Never play on start](#Never_play_on_start)
        *   [4.2.1 Installing mpd from the AUR](#Installing_mpd_from_the_AUR)
        *   [4.2.2 Method 1](#Method_1)
            *   [4.2.2.1 Method 1.1](#Method_1.1)
            *   [4.2.2.2 Method 1.2](#Method_1.2)
        *   [4.2.3 Method 2](#Method_2)
        *   [4.2.4 Method 3](#Method_3)
    *   [4.3 MPD y Alsa](#MPD_y_Alsa)
        *   [4.3.1 Alto uso de CPU con Alsa](#Alto_uso_de_CPU_con_Alsa)
        *   [4.3.2 Ejemplo de Configuración: Salida con 44.1 KHz a una profundidad de 16 bit, con múltiples programas](#Ejemplo_de_Configuraci.C3.B3n:_Salida_con_44.1_KHz_a_una_profundidad_de_16_bit.2C_con_m.C3.BAltiples_programas)
    *   [4.4 MPD y PulseAudio](#MPD_y_PulseAudio)
    *   [4.5 Control de MPD con lirc](#Control_de_MPD_con_lirc)
    *   [4.6 Control de MPD por medio del teléfono con Bluetooth](#Control_de_MPD_por_medio_del_tel.C3.A9fono_con_Bluetooth)
    *   [4.7 Archivos Cue](#Archivos_Cue)
    *   [4.8 HTTP Streaming](#HTTP_Streaming)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Falla en Auto-detección](#Falla_en_Auto-detecci.C3.B3n)
    *   [5.2 Avoiding timeouts](#Avoiding_timeouts)
    *   [5.3 mpd se cuelga en el primer inicio](#mpd_se_cuelga_en_el_primer_inicio)
        *   [5.3.1 Easy Tag](#Easy_Tag)
        *   [5.3.2 KID3](#KID3)
    *   [5.4 Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution](#Cannot_connect_to_mpd:_host_.22localhost.22_not_found:_Temporary_failure_in_name_resolution)
    *   [5.5 Other issues when attempting to connect to mpd with a client](#Other_issues_when_attempting_to_connect_to_mpd_with_a_client)
        *   [5.5.1 First fix](#First_fix)
        *   [5.5.2 Second fix](#Second_fix)
    *   [5.6 Port 6600 already in use](#Port_6600_already_in_use)
    *   [5.7 Binding to IPV6 before IPV4](#Binding_to_IPV6_before_IPV4)
    *   [5.8 Crackling sound with some audio files](#Crackling_sound_with_some_audio_files)
    *   [5.9 daemon: cannot setgid for user "mpd": Operation not permitted](#daemon:_cannot_setgid_for_user_.22mpd.22:_Operation_not_permitted)
*   [6 External links](#External_links)

## Procedimiento de Instalación del Daemon

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [mpd](https://www.archlinux.org/packages/?name=mpd), o la versión en desarrollo [mpd-git](https://aur.archlinux.org/packages/mpd-git/).

## Instrucciones de Configuración

Para más información de la configuración de MPD, por favor visite [http://mpd.wikia.com/wiki/Configuration](http://mpd.wikia.com/wiki/Configuration)

### Linea de Tiempo del Comportamiento Habitual de MPD

*   MPD es iniciado al cargar el sistema operativo por medio de `/etc/rc.conf`, incluyéndole en el apartado DAEMONS. (O, esto puede ser hecho manualmente ejecutando `/etc/rc.d/mpd start` con privilegios de root).
*   Al ser iniciado MPD como root, leerá el archivo `/etc/mpd.conf`.
*   MPD lee la variable usuario en el archivo `/etc/mpd.conf`, y cambia de root a este usuario.
*   MPD continúa leyendo el contenido del archivo `/etc/mpd.conf` y se configura de acuerdo a este.

Recuerde que MPD cambia el usuario de root a aquel mencionado en el archivo `/etc/mpd.conf`. Siendo asi, el uso de "~" en el archivo de configuracion hace referencia al directorio home del usuario, y no al directorio de root. Podria ser de utilidad cambiar todos los "~" a "/home/username" para prevenir cualquier confusion sobre este aspecto del comportamineto de MPD. Si no se espeifica un usuario, cuando este se ejecute lo hara como el usuario actual.

### Correcta Configuración de Sonido

Para que la salido de audio funcione, asegúrese de haber configurado la tarjeta de sonido y el mixer correctamente. Vea [ALSA](/index.php/ALSA "ALSA"). No olvide activar los canales requeridos en alsamixer, incrementar el volumen y guardar los cambios con alsactl store. Vea `~/.mpd/error` si aún no funciona.

Asegúrese que su tarjeta pueda hacer mezclas por hardware (la mayoría de ellas pueden, incluidas aquellas integradas de la board), si no, esto podría traer problemas con múltiples reproducciones de sonido. Por ejemplo, Mplayer no podría reproducir sonido mientras el daemon se esté ejecutando, mostrando un mensaje de error indicando que el dispositivo se encuentra ocupado.

### Configuracion General

*   Como root, verifique si `/etc/mpd.conf` existe y elimine el archivo en caso de que exista. Esto es hecho por seguridad.

MPD viene con un archivo de configuración de ejemplo, disponible en `/usr/share/doc/mpd/mpdconf.example`. Este archivo contiene abundante información acerca de la configuración de MPD, y contiene valores predeterminados para el mixer, que simplemente pueden ser descomentados.

*   Como root, copie este archivo de ejemplo a `/etc/mpd.conf`.

```
# cp /usr/share/doc/mpd/mpdconf.example /etc/mpd.conf

```

Para editar el archivo, como root:

```
# SUEDITOR /etc/mpd.conf

```

Edite `/etc/mpd.conf` para que se vea de la siguiente manera.

```
music_directory       "/home/usuario/música"         # Su directorio de música.
playlist_directory    "/var/lib/mpd/playlists"
db_file               "/var/lib/mpd/db"
log_file              "/var/log/mpd/mpd.log"
error_file            "/var/log/mpd/mpd.error"
pid_file              "/var/run/mpd/mpd.pid"
state_file            "/var/lib/mpd/mpdstate"
# Ediciones a la dirección y el puerto causan problemas en mpd-0.14.2 es preferible dejarlos
# comentados.
# bind_to_address       "127.0.0.1"
# port                  "6600"

```

Las direcciones de los archivos son los que por defecto se crean al istalar MPD, pero se pueden crear en otro lugar, por ejemplo si se desea tener todos los archivos bajo una misma carpeta.

*   Ahora como root, cree los archivos especificados en {Filename|/etc/mpd.conf}}, si los directorios no existen también deben ser creados.

```
# touch /var/lib/mpd/db
# touch /var/lib/mpd/mpdstate
# touch /var/run/mpd/mpd.pid
# touch /var/log/mpd/mpd.log
# touch /var/log/mpd/mpd.error

```

*   Si su colección musical está contenida en múltiples directorios, puede crear enlaces simbólicos en /var/lib/mpd y luego dirigir la variable 'music_dir' en mpd.conf a el directorio que contiene los enlaces.
*   Crear la base de datos ahora es realizado por medio de la opción "update" del cliente, por ejemplo, si ejecuta ncmpcpp, por medio de la tecla 'U'.
    *   El método anterior, crear la base de datos de MPD como root (# mpd --create-db), es obsoleto.

### Configuración Por Usuario

MPD no necesita ser iniciado con permisos de root. La única razón por la cual MPD necesita ser iniciado como root (siendo llamado por medio de `/etc/rc.conf`) es porque los archivos y directorios mencionados por defecto en el archivo de configuración son propiedad de root (el directorio /var). Una menos común, pero quizás mas sensible configuración, consiste en hacer que MPD trabaje con archivos y directorios que sean propiedad de un usuario normal. Ejecutar MPD como un usuario normal tiene varias ventajas:

1.  Puede manejar un solo directorio ~/.mpd (o cualquier otro directorio bajo /home/usuario) para todos los archivos de configuración de MPD
2.  No hay errores de lectura/escritura
3.  llamado más flexible a MPD haciendo uso de `~/.xinitrc` en vez de incluir MPD en la sección de DAEMONS en `/etc/rc.conf`.

Los siguientes pasos indican como iniciar MPD como un usuario normal. Debe realizar todos los pasos como usuario.
**Note:** Este método no funcionará si múltiples usuarios desean acceder a MPD.

*   Copie el contenido del archivo de configuración por defecto de MPD, ubicado en `/usr/share/doc/mpd/mpdconf.example` a su directorio home.

```
cp /usr/share/doc/mpd/mpdconf.example ~/.mpdconf

```

*   Siga los pasos de la configuración anterior, ignorando la primer parte, que hace referencia a copiar el archivo de configuración a `/etc/mpd.conf`.
*   Cree todos los archivos necesarios en `"/home/user/.mpd/"`:

```
"~/.mpd/playlists"
"~/.mpd/db"
"~/.mpd/mpd.log"
"~/.mpd/mpd.error"
"~/.mpd/mpd.pid"
"~/.mpd/mpdstate"

```

**Note:** No se olvide de especificar el nombre de usuario y grupo

*   Haga que MPD inicie al arranque de sesión (esto depende de su entorno de escritorio para su correcta configuracion).

**Note:** no tiene que poner un "&" al final de la linea, dado que MPD automáticamente se daemonizará.

Finalmente, elimine MPD de la sección de DAEMONS en `/etc/rc.conf`, ya que no será ejecutado como root nunca más.

### Configuración Multi-MPD

**Útil si desea ejecutar un servidor icecast, por ejemplo.** Si desea un segundo daemon MPD (ej., con una salida icecast para compartir su música a través de una red) que haga uso de la música y listas de reproducción del primero, simplemente copie el archivo de configuración anterior y cree uno nuevo (ej., `/home/username/.mpd/config-icecast`), y solo cambie los parámetros de log_file, error_file, pid_file, y state_file (ej., `mpd-icecast.log`, `mpd-icecast.error`, y demás); hacer uso de los mismos directorios de música y listas de reproducción asegurará que este segundo daemon MPD hará uso de la misma colección musical del primero (ej., crear y editar una lista de reproducción bajo el primer daemon afectará también al segundo daemon, de modo que no sea necesario crear la misma lista de nuevo para el segundo daemon). Finalmente, ejecute este segundo daemon por medio de su archivo `~/.xinitrc`. (Asegúrese de utilizar un numero de puerto diferente, para evitar conflictos con su primer daemon MPD).

## Instalando Clientes para MPD

Los mas populares son:

*   **mpc** – Cliente para línea de comandos. Lo mas común es instalar este en paralelo a otro cliente más avanzado.
*   **ncmpc** – Cliente que emplea la librería ncurses. Muy útil para usar en consola. [Pagina oficial de ncmpc](http://hem.bredband.net/kaw/ncmpc/)
*   **ncmpcpp** – Clon de ncmpc con algunas nuevas opciones escrito en C++. [Sitio oficial de ncmpcpp](http://unkart.ovh.org/ncmpcpp/)
*   **pms** – Otro cliente que utiliza ncurses. Altamente configurable y accesible. [Pagina Sourceforge de pms](http://pms.sourceforge.net/)
*   **ario** – Cliente GTK+ con un manejo de librerías similar a la de Rythmbox. [Sitio oficial de Ario](http://ario-player.sourceforge.net)
*   **sonata** – Cliente Python GTK+. [Sitio oficial de Sonata](http://sonata.berlios.de/)
*   **gmpc** – Cliente GNOME. [Sitio oficial de gmpc](http://gmpcwiki.sarine.nl/index.php?title=GMPC)
*   **QMPDClient** – Cliente escrito en Qt 4\. [Sitio oficial de QMPDClient](http://bitcheese.net/wiki/QMPDClient)

Instálelos usando:

```
# pacman -S mpc
# pacman -S ncmpc
# pacman -S ncmpcpp
# pacman -S pms
# pacman -S ario
# pacman -S sonata
# pacman -S gmpc
# pacman -S qmpdclient

```

## Extra stuff

### Envío de Canciones a Last.fm

Para enviar los títulos de las canciones hacia [Last.fm](http://www.last.fm) con MPD existen varias alternativas.

#### Mpdscribble

mpdscribble es otro demonio, pero sólo está disponible en [AUR](https://aur.archlinux.org/packages.php?ID=22274). Suele ser la mejor alterativa, ya que sería el scrobbler semi-oficial de MPD y, además, usa el nuevo "idle" en MPD para mejorar el scrobbling. No es necesario el acceso root para su configuración, porque no necesita realizar ningún cambio dentro del directorio <tt>/etc</tt>. Para más información, se puede visitar [sitio oficial de Mpdscribble](http://mpd.wikia.com/wiki/Client:El).

Para instalar mpdscribble, solo instálelo desde AUR y luego, sin ser root, haga:

*   `$ mkdir ~/.mpdscribble`
*   Cree el archivo `~/.mpdscribble/mpdscribble.conf` y añada lo siguiente:

```
username = <su nombre de usuario de last.fm>
password = <Número de verificación md5 de su password de last.fm> # Se genera ejecutándo "echo -n password | md5sum"
host = <su mpd host> # por defecto $MPD_HOST o localhost
port = <su mpd port> # por defecto $MPD_PORT o 6600
log = ~/.mpdscribble/mpdscribble.log
journal = ~/.mpdscribble/mpdscribble.cache
verbose = 2
sleep = 1
musicdir = <su directorio de música>

```

*   Añada `mpdscribble` a su `~/.xinitrc`.

#### Sonata

La forma más sencilla, pero implica usar una interfaz gráfica, es usar Sonata. Este programa es un frontend gráfico para MPD, que incluye de serie el soporte para scrobbling hacia Last.fm dentro de sus opciones. El punto negativo, es que como Sonata no realiza cache de los temas reproducidos, se necesita tener una conección activa durante la reproducción para que el scrobble se realice.

#### Lastfmsubmitd

lastfmsubmitd es un demonio disponible dentro del repositorio "community". Para instalarlo, primero edite `/etc/lastfmsubmitd.conf` y luego añada `lastfmsubmitd` y `lastmp` a la sección `DAEMONS` dentro de su `/etc/rc.conf`.

#### Reproducción Desde Last.fm

##### Reproducción Nativa

Desde la versión 0.16 MPD tiene un método para [reproducir desde last.fm](http://mpd.wikia.com/wiki/Last.fm_Radio).

 `/etc/mpd.conf` 
```
playlist_plugin {
       name            "lastfm"
       user            "my_username"
       password        "my_password"
}
```

Por Ejemplo:

 `$ mpc load "lastfm://artist/Beatles"` 

##### Reproducir Desde Last.fm con Lastfmproxy

Lastfmproxy es un script escrito en python que permite reproducir música desde last.fm hacia cualquier otro reproductor. Para instalarlo [lastfmproxy](https://aur.archlinux.org/packages/lastfmproxy/) desde [AUR](/index.php/AUR "AUR") debe editar `/usr/share/lastfmproxy/config.py`.

**Note:** El scrip se intslala en un directorio de solo lectura, pero este requiere lectura/escritura, puede mover `/usr/share/lastfmproxy` a su directorio Home.

Para iniciar `lastfmproxy` debe ir a `[http://localhost:1881/](http://localhost:1881/)` en su navegador. Para gregar una estacion a last.fm navegue desde `[http://localhost:1881/](http://localhost:1881/)` seguido por lastfm:// (por ejemplo: `[http://localhost:1881/lastfm://globaltags/punk](http://localhost:1881/lastfm://globaltags/punk)`). Vuelva a `[http://localhost:1881/](http://localhost:1881/)` y descargue el archivo m3u seleccionando el enlace de *Start Listening*. Sólo tiene que añadirlo a su biblioteca de música.

### Never play on start

This feature has recently been added to mpd git by Martin Kellerman, see commits `b57330cf75bcb339e3f268f1019c63e40d305145` and `2fb40fe728ac07574808c40034fc0f3d2254d49d`. As of September 2011, this feature has not yet arrived in a mpd version in the official repositories. If support for this feature is still required, have a look at the following proposals.

#### Installing mpd from the AUR

This is the best method currently available, but is only currently (as of April 2011) enabled in the git version. Install [mpd-git](https://aur.archlinux.org/packages/mpd-git/) from the [AUR](/index.php/AUR "AUR") and add `restore_paused "yes"` to your `mpd.conf` file.

If you have issues with connecting your client to [mpd-git](https://aur.archlinux.org/packages/mpd-git/), see [Music Player Daemon#Other issues when attempting to connect to mpd with a client](/index.php/Music_Player_Daemon#Other_issues_when_attempting_to_connect_to_mpd_with_a_client "Music Player Daemon").

#### Method 1

If you do not want MPD to always play on your system start, but yet you want to preserve the other state information, add the following lines to your `/etc/rc.d/mpd` file:

##### Method 1.1

Simpler, working method (disables playing on startup of mpd daemon):

```
 start)

```

...

```
     mpc -q pause #add this line only
     add_daemon mpd
     stat_done

```

##### Method 1.2

This method was described here before Method 1.1 and is much more complicated:

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

This will change the player status to "paused", if it was stopped while playing. Next, you want this file to be preserved, so MPD updates won't erase this edit. Add (or edit) this line to your `/etc/pacman.conf`:

```
NoUpgrade = etc/rc.d/mpd

```

#### Method 2

Another simpler method, would be to add mpd to your `[rc.conf](/index.php/Rc.conf "Rc.conf")` daemons array and add `mpc stop` or `mpc pause` to `/etc/rc.local.shutdown` and to `/etc/rc.local`. (Remember you must have mpc installed to use this method).

Adding only the order in `/etc/rc.local` cannot assure that mpd will play absolutely nothing, since there may be a delay before the stop command is executed. On the other hand, if you only add the order to `/etc/rc.local.shutdown`, that will assure that mpd won't play at all, as long as you properly shutdown your system. Even though they are redundant, adding it to `/etc/rc.local` would serve as a safety for those, presumably, rare occasions when you do not shutdown the system properly.

#### Method 3

The general idea is to ask mdp to pause music when the user logs out, so that mdp will stick to the "pause" state after a reboot. Sending such command can be achieved using [mpc](https://www.archlinux.org/packages/?name=mpc), the command line interface to MPD.

GDM users can then add `/usr/bin/mpc pause` to `/etc/gdm/PostSession/Default` (be sure to add it before `exit 0`):

Non-GDM users can use their own login manager's method to launch the line at logout.

### MPD y Alsa

A veces, con el uso de otros programas de audio, por ejemplo: páginas web que contienen applets de Flash, MPD se vuelve incapaz de reproducir (hasta que se reinicie). El error aparece en los log's de MPD de esta forma:

```
Error opening alsa device "hw:0,0": Device or resource busy

```

Las razones de esto pueden ser:

*   La placa no soporta la mezcla de audio por hardware (use el plug-in **dmix** )
*   La configuración predeterminada de ALSA no es adecuada.

Para mas detalles puede ir a [este](http://mpd.wikia.com/wiki/Alsa) link.

El problema se puede resolver editando:

 `mpd.conf` 
```
audio_output {
        type                    "alsa"
        name                    "Sound Card"
        options                 "dev=dmixer"
        device                  "plug:dmix"
```

Para que los cambios tengan efecto debe reiniciar MPD.

#### Alto uso de CPU con Alsa

Cuando se utiliza MPD con ALSA, los usuarios pueden experimentar un elevado consumo de CPU (alrededor de 20-30%). Esto es causado por la mayoría de las placas de audio que soportan 48kHz y la mayoria de los temas son en 44kHz, lo que obliga a MPD para volver a muestrear (resample). Esta operación requiere de muchos ciclos de CPU.

En la mayoría de las veces se soluciona indicándole a MPD que no realice resample. Agregue la linea `auto_resample "no"` en audio_output. Con esto disminuye la calidad de sonido.

 `mpd.conf` 
```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   auto_resample	"no"
}
```

Puede que no allá un cambio significativo pero agregando `use_map "yes"` disminuye aun mas el uso de CPU:

 `mpd.conf` 
```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   use_mmap		"yes"
}
```

En [Tuning MPD](http://mpd.wikia.com/wiki/Tuning) puede encontrar mas información.

#### Ejemplo de Configuración: Salida con 44.1 KHz a una profundidad de 16 bit, con múltiples programas

Este formato es un estándar CDA. ALSA permite la reproducción de mas de un programa con dmix — cuyo algoritmo de resample es inferior — ademas dmix, por defecto, realiza resamples todo aquello por debajo de 48 KHz. Ademas se pueden escuchar chasquidos sino se aplica esta configuración.

Esta configuración hace que todo (si es necesario) se vuelva a muestrear (resample) a este formato, como los DVD de video o la televisión, que generalmente es de 48 KHz. Pero no hay forma conocida de que ALSA cambie de forma dinámica de formato, y en particular, si usted escucha CD mucho más que cualquier otra cosa, 48 → 44,1 no es muy grande la pérdida.

Se supone que no hay otras configuraciones por resmple, ya que puede entrar en conflicto. Esto se aplica a nivel de usuario en `~/.asoundrc` pero MPD ignora este archivo por lo que tiene que especificar estas configuraciones en `/etc/asound.conf`:

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

**Note:** MPD porvee un tratamiento especial para la decodificacion de archivos mp3: Siempre es reproducida en 24 bit. (La conversión forzada de este formato se realiza después de esto)

Si quiere que la profundida de bits sea decidido por ALSA, quite o comente la linea *dmix.format* y cambiar la linea *format* to "44100:*:2".

**Note:** La 'transición' entre los archivos codificados en dos diferentes profundidades de bit (por ejemplo, un mp3 y un flac de 16 bits) no funciona a menos que la conversión está activo.

### MPD y PulseAudio

Editar `/etc/mpd.conf`f, y descomentar la sección audio_output para el tipo de `pulse`.

A continuación, agregue el usuario a los grupos de `pulse` necesarios. El grupo de `pulse-access` de acceso debería ser suficiente, pero es posible que desee agregar `pulse-rt` también. El grupo de `pulse` no parece ser necesario.

```
 # gpasswd -a mpd pulse-access
 # gpasswd -a mpd pulse-rt

```

### Control de MPD con lirc

Ya hay algunos clientes diseñado para las comunicaciones entre lircd y MPD, sin embargo, en cuanto a la utilidad práctica, no son muy útiles ya que sus funciones son limitadas.

Se recomienda el uso de MPC con irexec. MPC es un reproductor de línea de comandos que sólo le envía la orden a MPD y se cierra inmediatamente, lo cual es perfecto para irexec, el ejecutor de comandos incluidas en lirc. Lo que hace irexec es ejecutar un comando especificado una vez recibió una señal de algun control remoto.

Si asi lo desea, lea primero el articulo [LIRC](/index.php/LIRC "LIRC").

Edite el archivo de configuración, por defecto se encuentra en `~/.lircrc`.

Agregue las lineas:

 `~/.lircrc` 
```
begin
     prog = irexec
     button = <button_name>
     config = <command_to_run>
     repeat = <0 or 1>
end
```

Un ejemplo útil:

 `~/.lircrc` 
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

Para mas información de mpc ejecute [mpc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mpc.1).

### Control de MPD por medio del teléfono con Bluetooth

También puede controlar MPD (hasta cierto punto) con un teléfono con Bluetooth. Tiene que hacer lo siguiente:

*   instalar remuco - un control remoto inalámbrico para varios reproductores multimedia de Linux ([aur](https://aur.archlinux.org/packages.php?ID=25072))
*   transferir del cliente de remuco los archivos jar/jad de `/usr/share/remuco/client/` a tu teléfono e instalarlo
*   ejecutar remuco-mpd (como el usuario actual)
*   ejecutar remuco en su teléfono, definir una nueva conexión Bluetooth con remuco y explorar sus capacidades

Más información acerca de remuco (incluyendo solución a problemas) que se encuentran en su [página](http://remuco.sourceforge.net/index.php/Remuco).

### Archivos Cue

Para usar estos archivos, debe evitar un error de libcue. Libcue copia archivos desde libcdio, por lo que puede trare conflictos, para solucionarlo:

```
* Quitar libcdio temporalmente (pacman -Rdd libcdio)
* Instalar libcue (pacman -S libcue)
* Instalar MPD desde ABS o AUR.
* Reinstalar libcdio (pacman -S libcdio)

```

En el momento de escribir este articulo no analiza tracknumbers de los archivos cue. Hay un [parche](http://musicpd.org/mantis/view.php?id=3230) disponible.

### HTTP Streaming

Since version 0.15 there is a built-in HTTP streaming daemon/server that comes with MPD. To activate this server simply set it as output device in mpd.conf:

```
audio_output {    
	type		"httpd"    
	name		"My HTTP Stream"    
	encoder		"vorbis"		# optional, vorbis or lame    
	port		"8000"    
#	quality		"5.0"			# do not define if bitrate is defined    
	bitrate		"128"			# do not define if quality is defined    
	format		"44100:16:1"    
}

```

Then to listen to this stream simply open the URL of your mpd server (along with the specified port) in your favorite music player. Note: You may have to specify the file format of the stream using an appropriate file extension in the URL. For example, using Winamp 5.5, You would use [http://192.168.1.2:8000/mpd.ogg](http://192.168.1.2:8000/mpd.ogg) rather than [http://192.168.1.2:8000/](http://192.168.1.2:8000/).

To use mpd to connect to the stream from another computer.

```
mpc add [http://192.168.1.2:8000](http://192.168.1.2:8000)

```

## Troubleshooting

### Falla en Auto-detección

Durante el inicio de mpd, el intentará detectar automaticamente y configurar su salida de audio y control de volumen. Aunque en la mayoria de los casos esto suele funcionar, en otros sistemas puede fallar. Podria ser de ayuda para mpd especificar que utilizar como salida y mixer de sonido. Si su archivo `/etc/mpd.conf` es una copia de `/etc/mpd.conf.example` como se menciono anteriormente, simplemente descomente estas lineas:

Ejemplo de una salida tipo ALSA:

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

**Note:** in case of permission problems when using ESD with MPD run this as root:

```
# chsh -s /bin/true mpd

```

### Avoiding timeouts

To get rid of timeouts (i.e. when you paused music for long time) in gpmc and other clients uncomment and increase `connection_timeout` option in `mpd.conf`.

If files and/or titles are shown in wrong encoding, uncomment and change `filesystem_charset` and `id3v1_encoding` options. Note that you cannot set encoding for ID3 v2 tags. To workaround this you may use [external tag readers](http://mpd.wikia.com/wiki/GenericDecoder#Generic_Tagreader).

If you want to use another computer to control MPD over a network, the `bind_to_address` option in `mpd.conf` will need to be set to either your IP address, or `any` if your IP address changes frequently.

**Streaming**
With the latest version of MPD (0.15), built-in httpd streaming is now available.

To activate this feature, you'll just need to add a new output of type httpd in `mpd.conf`:

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

Restart the mpd daemon and, from another computer, simply load the stream as any other url.

```
$ mplayer http://<server's IP>:8000

```

**Note:** You must open the port on your router / firewall for the stream to be connectible to from another computer.

Most players (i.e. vlc or xmms2) should also be able to load the stream via their "add url..." menu option.

This is a nice clean way to replace your current icecast setup with something natively supported within MPD.

### mpd se cuelga en el primer inicio

Este es un error común causado por etiquetas mp3 dañadas. Esta es una manera experimental para resolver este problema. Requirements:

*   kid3
*   easytag

Este método es tedioso, especialmente con bases de datos enormes. Para que entiendan, tomó 2.5 horas arreglar una una base de datos de 16Gb.

#### Easy Tag

Easytag aparece aquí porque detecta los errores en las etiquetas mp3, pero igual que mpd, se cuelga y muere. El truco es que easytag te dice cual es el archivo problemático en su barra de estado. Antes de empezar, asegúrate de empezar easytag en una terminal para estar listo para cerrarlo por si se cuelga. Cuando estes listo, en la vista ramificada selecciona el directorio donde tienes tu música. Como opción predeterminada, easytag busca en todos los subdirectorios en busca de archivos mp3\. Cuando easytag se detenga, anota al culpable y mata easytag.

#### KID3

Aquí es donde usamos kid3\. Con kid3, busca la canción dañada y reescribe una de sus etiquetas, guarda el archivo y ya. Esto forzará a kid3 a reescribir todas las etiquetas y arreglara el problema con mpd.

Repite hasta que tu biblioteca musical este limpia. .

### Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution

Cannot connect to MPD (with ncmpcpp), if you are disconnected from network. Solution is [disable IPv6](/index.php/IPv6_-_Disabling_the_Module "IPv6 - Disabling the Module") or add line to /etc/hosts

```
::1 localhost.localdomain localhost

```

### Other issues when attempting to connect to mpd with a client

Some have reported being unable to access mpd with various clients, for example seeing errors like these:

```
$ ncmpcpp
Cannot connect to mpd: Connection closed by the server
$ sonata
2011-02-13 18:33:05  Connection lost while reading MPD hello
2011-02-13 18:33:05  Not connected
2011-02-13 18:33:05  Not connected

```

Please see posts on ncmpcpp on the Arch Forums [HERE](https://bbs.archlinux.org/viewtopic.php?id=109962) and [HERE](https://bbs.archlinux.org/viewtopic.php?id=113493). Also see the Arch bug report on this issue [HERE](https://bugs.archlinux.org/task/22071).

#### First fix

Check `mpd.conf` for a line like `mpd.error` and remove it. The mpd error file is deprecated and has been removed.

#### Second fix

**Note:** I'm not so sure this is a good idea. There is a warning about changing the address to bind to in the default mpd.conf. If this does not help, you might want to comment out the changes.

If that doesn't help, add the following to `mpd.conf`:

```
 bind_to_address "127.0.0.1"
 port "6600"

```

Afterwards, instruct your client to connect via 127.0.0.1\. For example, add the following to the ncmpcpp config file:

```
 mpd_host "127.0.0.1"
 mpd_port "6600"

```

### Port 6600 already in use

MPD needs to bind to port 6600 and cannot start if it's already in use. The most common reason for this is that the user has started MPD once and then subsequently tried to start mpd again. In general, nothing should be done here.

If port 6600 is tied up for some other reason, one can use the following command to find the offending process:

```
# ss -tulpan | grep 6600

```

This will list IP:Port and the process name holding the connection (root privileges are required to see all processes).

```
If you need to restart mpd for whatever reason, use:

```

```
 $ mpd --kill
 $ mpd 

```

A more brute-force approach:

```
 $ killall mpd
 $ mpd 

```

**Note:** If you typically run MPD as root, you will need to run the above commands as root.
In the latest version of MPD, --create-db is completely deprecated. The database will be created automagically on first run and can subsequently be updated via your client (i.e. mpc update). You can now use inotify support to automatically update your music database. Add the following to `mpd.conf`  `auto_update "yes"` to enable it.

### Binding to IPV6 before IPV4

If on startup, you see this message:

```
listen: bind to '0.0.0.0:6600' failed: Address already in use (continuing anyway, because binding to '[::]:6600' succeeded)

```

MPD is attempting to bind to the ipv6 interface before binding to ipv4\. If you want to use your ipv4 interface, hardcode it in mpd.conf, like so:

```
bind_to_address "127.0.0.1"

```

Or, you could specify several binds, for example, to have MPD listen on localhost and the external IP of your network card:

```
bind_to_address "127.0.0.1"
bind_to_address "192.168.1.13"

```

### Crackling sound with some audio files

This is usually a playback speed problem and can be fixed by uncommenting the audio_output_format line in:

 `/etc/mpd.conf`  `  audio_output_format "44100:16:2"` 

This is usually a sane value for most mp3 files.

### daemon: cannot setgid for user "mpd": Operation not permitted

The error is stating that the user starting the process (you) does not have permissions to become another user (mpd) which the configuration has told that process to run as.

To solve the issue, simply start mpd as root.

 `$ su -c "rc.d start mpd"` 

or

 `# rc.d start mpd` 

## External links

*   [Official Web Site and wiki](http://mpd.wikia.com/wiki/Music_Player_Daemon_Wiki)
*   [Sorted List of MPD Clients](http://mpd.wikia.com/wiki/Clients)
*   [MPD forum](http://www.musicpd.org/forum/)