(Traducción al español en curso)

**PulseAudio** es un servidor de sonido para sistemas POSIX y Win32 . Permite tener varios programas reproduciendo sonido en una maquina, entre otras características mas avanzadas.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Ejecución](#Ejecuci.C3.B3n)
*   [3 Configuración del motor](#Configuraci.C3.B3n_del_motor)
    *   [3.1 ALSA](#ALSA)
    *   [3.2 OSS](#OSS)
        *   [3.2.1 osspd](#osspd)
        *   [3.2.2 padsp wrapper](#padsp_wrapper)
    *   [3.3 GStreamer](#GStreamer)
    *   [3.4 OpenAL](#OpenAL)
    *   [3.5 libao](#libao)
    *   [3.6 PortAudio](#PortAudio)
    *   [3.7 ESD](#ESD)
*   [4 Entornos de escritorio](#Entornos_de_escritorio)
    *   [4.1 General X11](#General_X11)
        *   [4.1.1 X11 bell](#X11_bell)
    *   [4.2 GNOME](#GNOME)
    *   [4.3 KDE 3](#KDE_3)
    *   [4.4 KDE 4 y Qt 4](#KDE_4_y_Qt_4)
*   [5 Aplicaciones](#Aplicaciones)
    *   [5.1 Audacious](#Audacious)
    *   [5.2 mpd](#mpd)
    *   [5.3 MPlayer](#MPlayer)
    *   [5.4 Flashplugin (solo x86_64)](#Flashplugin_.28solo_x86_64.29)
    *   [5.5 Skype (x86_64 only)](#Skype_.28x86_64_only.29)
    *   [5.6 Control de Volumen](#Control_de_Volumen)
*   [6 Configuraciones alternativas](#Configuraciones_alternativas)
    *   [6.1 Systemas de sonido envolvente](#Systemas_de_sonido_envolvente)
    *   [6.2 Configuracion avanzada de ALSA](#Configuracion_avanzada_de_ALSA)
        *   [6.2.1 Monitor de fuentes ALSA](#Monitor_de_fuentes_ALSA)
    *   [6.3 PulseAudio over network](#PulseAudio_over_network)
        *   [6.3.1 TCP support (networked sound)](#TCP_support_.28networked_sound.29)
        *   [6.3.2 Zeroconf (Avahi) publishing](#Zeroconf_.28Avahi.29_publishing)
        *   [6.3.3 Switching the PulseAudio server used by local X clients](#Switching_the_PulseAudio_server_used_by_local_X_clients)
    *   [6.4 Pulseaudio through JACK](#Pulseaudio_through_JACK)
        *   [6.4.1 QjackCtl with Startup/Shutdown Scripts](#QjackCtl_with_Startup.2FShutdown_Scripts)
    *   [6.5 Pulseaudio a través OSS](#Pulseaudio_a_trav.C3.A9s_OSS)
    *   [6.6 Pulseaudio from within a chroot (ex. 32-bit chroot in 64-bit install)](#Pulseaudio_from_within_a_chroot_.28ex._32-bit_chroot_in_64-bit_install.29)
    *   [6.7 Simultaneous Digital and Analog Output](#Simultaneous_Digital_and_Analog_Output)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 No hay sonido después de instalar](#No_hay_sonido_despu.C3.A9s_de_instalar)
    *   [7.2 Contenido Flash](#Contenido_Flash)
        *   [7.2.1 Sin Tarjetas](#Sin_Tarjetas)
        *   [7.2.2 KDE4](#KDE4)
        *   [7.2.3 Dispositivo de audio silenciado](#Dispositivo_de_audio_silenciado)
    *   [7.3 Fallo al iniciar el Demonio](#Fallo_al_iniciar_el_Demonio)
    *   [7.4 padevchooser](#padevchooser)
    *   [7.5 Problemas técnicos y uso intensivo de la CPU desde 0.9.14](#Problemas_t.C3.A9cnicos_y_uso_intensivo_de_la_CPU_desde_0.9.14)
    *   [7.6 Sonido entrecortado](#Sonido_entrecortado)
    *   [7.7 Volume adjustment doesn't work properly](#Volume_adjustment_doesn.27t_work_properly)
    *   [7.8 Volume gets louder every time a new application is started](#Volume_gets_louder_every_time_a_new_application_is_started)
*   [8 External links](#External_links)

## Instalación

Todos los paquetes son del repositorio community, así que debes tenerlo habilitado. Luego, para instalar PulseAudio:

```
# pacman -S pulseaudio

```

Opcionalmente puedes instalar algunos entornos GTK para PulseAudio:

```
# pacman -S paprefs pavucontrol

```

## Ejecución

Si el demonio D-Bus no se está ejecutando, habrá que iniciarlo:

```
# /etc/rc.d/dbus start

```

PulseAudio puede ser iniciado con:

```
$ pulseaudio --start

```

O si usas X11:

```
$ start-pulseaudio-x11

```

Para kde:

```
$ start-pulseaudio-kde

```

PulseAudio puede ser detenido con:

```
$ pulseaudio --kill

```

Tener en cuenta que en el caso de ciertos entornos X11, PulseAudio sera iniciado en el login. Ver la sección en Entornos de Escritorio para detalles.

## Configuración del motor

### ALSA

Para las aplicaciones que no soportan PulseAudio y soportan ALSA es **recomendable** instalar el modulo PulseAudio para ALSA. Este modulo está disponible en el paquete pulseaudio-alsa.

```
# pacman -S pulseaudio-alsa

```

Este paquete contiene el `/etc/asound.conf` con la configuración necesaria para que ALSA utilizar utilice PulseAudio.

Para poder añadir sonido a programas de 32 bit sobre Arch x86_64 (como Wine), tendremos que instalar lib32-libpulse y lib32-alsa-plugins también.

```
# pacman -S lib32-libpulse lib32-alsa-plugins

```

Para prevenir que las aplicaciones utilicen la emulación OSS de ALSA en lugar de PulseAudio (impedirían que otras aplicaciones reprodujeran sonido), debemos remover el módulo `snd-pcm-oss` ejecutando:

```
# rnmod snd-pcm-oss

```

Para que no tengamos que realizar el paso anterior cada vez que reiniciemos, introduciremos el módulo en la lista negra, añadiendo `!snd-pcm-oss` a MODULES en `/etc/rc.conf`.

### OSS

Tenemos varias alternativas para hacer que reproduzcan con PulseAudio programas que sólo utilizan OSS:

#### osspd

Éste es el método más simple

Instala **ossp** e inicialízalo:

```
# pacman -S ossp
# /etc/rc.d/osspd start

```

Después, incluye osspd a DAEMONS en rc.conf.

#### padsp wrapper

Si tiene un programa que utiliza OSS puedes hacer que trabaje con PulseAudio ejecutándolo con padsp:

```
$ padsp OSSprogram

```

Ejemplos:

```
$ padsp aumix
$ padsp sox foo.wav -t ossdsp /dev/dsp

```

Si quiere, puede renombrar el OSSprogama por OSSprograma-real y crear un macro como éste:

 `/usr/bin/OSSProgram` 

```
#!/bin/sh
if test -x /usr/bin/padsp; then
    exec /usr/bin/padsp /usr/bin/OSSprogram-bin "$@"
else
    exec /usr/bin/OSSprogram "$@"
fi

```

### GStreamer

Para hacer que [GStreamer](/index.php/GStreamer "GStreamer") use PulseAudio, ejecute `gstreamer-properties` (parte del paquete _gnome-media_) y seleccione _PulseAudio Sound Server_, en el cuadro Entrada y Salida de Audio.

```
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/audiosink pulsesink
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/audiosrc pulsesrc

```

Algunas aplicaciones (como Rhythmbox) ignoran la propiedad _audiosink_, pero utilizan el valor de _musicaudiosink_, aunque no se puede configurar esto usando `gstreamer-properties`. Necesita establecerlo manualmente usando `gconf-editor` o `gconftool-2`:

```
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/musicaudiosink pulsesink

```

### OpenAL

OpenAl debería utilizar PulseAudio por defecto, pero puede ser explícitamente configurado editando `/etc/openal/alsoft.conf`  `drivers=pulse,alsa` 

### libao

Editar el fichero de configuración de libao:

 `/etc/libao.conf`  `default_driver=pulse` 

### PortAudio

El actual binario de PortAudio que se encuentra en el repositorio de community no soporta PulseAudio y no mapea dispositivos de audio. Puede solucionarlo compilando PortAudio desde ABS y aplicando [este parche](http://svn.mandriva.com/cgi-bin/viewvc.cgi/packages/cooker/portaudio/current/SOURCES/portaudio-19-alsa_pulse.patch?revision=313993) a los fuentes.

### ESD

PulseAudio es un reemplazo para el demonio enlightened sound (ESD). Si PulseAudio está en ejecución, los clientes ESD deberían tener disponible la salida sin modificar su configuración.

## Entornos de escritorio

### General X11

Se puede iniciar PulseAudio después de ejecutar X usando:

```
$ start-pulseaudio-x11

```

Esto iniciará PulseAudio y cargará los modulos X11.

Si usamos GNOME o KDE, PulseAudio será lanzado automáticamente en el login.

#### X11 bell

Para hacer que PulseAudio reproduzca un sonido cuando se produce un evento de campana de sistema en X11 (ejemplo: hacer que el terminal haga 'Ping!' en vez del 'Beep!'), añadimos al final de `/etc/pulse/default.pa`:

```
# Prevent pulseaudio --start from failing when following commands fail (eg. when X is not active)
.nofail
load-sample-lazy x11-bell /usr/share/sounds/freedesktop/stereo/dialog-error.oga
load-module module-x11-bell sample=x11-bell 
.fail

```

Puedes usar cualquier otro sonido. `dialog-error.oga` está en el paquete _sound-theme-freedesktop_.

### GNOME

La integración adecuada de PulseAudio con GNOME requiere algunos paquetes especiales:

*   libcanberra-pulse
*   gnome-media-pulse
*   gnome-settings-daemon-pulse

Son parte del grupo _pulseaudio-gnome_.

### KDE 3

Note que Pulseaudio _NO_ es un reemplazo para aRts. Si usas KDE 3, no es posible usar PulseAudio.

### KDE 4 y Qt 4

En principio, al iniciar la sesión, debería ser lanzado por defecto. Para más información, visitar [la wiki de PulseAudio en las páginas KDE](http://www.pulseaudio.org/wiki/KDE)

Adicionalmete, una alternativa en KDE a pavucontrol, es [veromix plasmoid](https://aur.archlinux.org/packages.php?ID=43848) disponible en el AUR.

## Aplicaciones

### Audacious

Audacious soporta PulseAudio de forma nativa. Para utilizarlo, debemos ir en Audacious a Preferencias->Audio->Salida->plugin para "PulseAudio".

### mpd

You will need to [configure](http://mpd.wikia.com/wiki/PulseAudio) mpd to use PulseAudio.

On a headless box, run PulseAudio as the _mpd_ user. On a desktop, running mpd as yourself and not using the _mpd_ user is preferred.

### MPlayer

MPlayer soporta la salida PulseAudio de forma nativa, con la opción "`-ao pulse`". También puede configurar la salida PulseAudio por defecto en `~/.mplayer/config` por usuario, o en `/etc/mplayer/mplayer.conf` para todo el sistema:

 `/etc/mplayer/mplayer.conf`  `ao=pulse` 

### Flashplugin (solo x86_64)

Si está usando flashplugin desde el repositorio multilib, necesitará instalar lib32-alsa-plugins y lib32-libcanberra-pulse para poder usar el mezclador de sonido, en otro caso, no podrá tener sonido simultáneo en una aplicación y flashplugin.

```
# pacman -S lib32-alsa-plugins lib32-libcanberra-pulse

```

### Skype (x86_64 only)

Tiene que instalar lib32-libpulse desde multilib, sino obtendrá el error "Problema con la reproducción de audio" cuando inicie una llamada.

### Control de Volumen

Adapte la variable 'device' a su sink-device listado en `pactl list` 

Puede cambiar el volumen usando este macro.

```
#!/bin/bash
device="alsa_output.pci-0000_00_14.2.analog-stereo"
case "$1" in
	"up")    # incrementar volumen en 1000
		pacmd dump | awk --non-decimal-data '$1~/set-sink-volume/{if ($2~/'${device}'/) {if ($3+1000 > 65535) {system ("pactl "$1" '${device}' "65535)} else {system ("pactl "$1" '${device}' "$3+1000)}}}'
		;;
	"down")  # decrementar volumen en 1000
		pacmd dump | awk --non-decimal-data '$1~/set-sink-volume/{if ($2~/'${device}'/) {if ($3-1000 < 0) {system ("pactl "$1" '${device}' "0)} else {system ("pactl "$1" '${device}' "$3-1000)}}}'
		;;
	"mute")  # encender mute
		pacmd dump|awk --non-decimal-data '$1~/set-sink-mute/{if ($2~/'${device}'/) {system ("pactl "$1" '${device}' "($3=="yes"?"no":"yes"))}}'
		;;
esac

```

## Configuraciones alternativas

### Systemas de sonido envolvente

Muchas personas poseen una placa compatible con sonido envolvente, pero tienen altavoces para solo dos canales, entonces PulseAudio no puede usar una configuración envolvente por defecto. Para habilitar todos los canales, edite `/etc/pulse/daemon.conf`: descomentando la linea default-sample-channels (i.e. remueva el punto y coma del principio de la linea) y configure el valor a **6** si tiene un sistema _5.1_, o **8** si tiene un sistema _7.1_ etc.

```
# Default
default-sample-channels=2
# Para 5.1
default-sample-channels=6
# Para 7.1
default-sample-channels=8

```

Luego de realizar la edición, sera necesario reiniciar el servidor de PulseAudio

### Configuracion avanzada de ALSA

Para que ALSA pueda usar PulseAudio se necesita una configuración especial`/etc/asound.conf` (system wide settings) (recomendado) o `~/.asoundrc` (configuración en una base por usuario):

 `/etc/asound.conf` 

```
pcm.pulse {
    type pulse
}
ctl.pulse {
    type pulse
}
pcm.!default {
    type pulse
}
ctl.!default {
    type pulse
}

```

Si omite los dos últimos grupos, PulseAudio no se utilizará de forma predeterminada. A continuación, tendrá que cambiar el dispositivo ALSA "pulse " en las aplicaciones que se utilizan para hacer que funcione.

#### Monitor de fuentes ALSA

To be able to record from a monitor source (a.k.a. "What-U-Hear", "Stereo Mix"), use `pactl list` to find out the name of the source in Pulseaudio (e.g. `alsa_output.pci-0000_00_1b.0.analog-stereo.monitor`). Then add lines like the following to `/etc/asound.conf` or `~/.asoundrc`:

```
pcm.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

ctl.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

```

Now you can select `pulse_monitor` as a recording source.

**Note:** You can also simply install the package 'pulseaudio-alsa'

### PulseAudio over network

One of PulseAudio's magnificent features is the possibility to stream audio from clients over TCP to the server running the PulseAudio daemon, allowing sound to be streamed through your LAN.

To accomplish this, one needs to enable module-native-protocol-tcp, and copy the pulse-cookie to the clients.

#### TCP support (networked sound)

To enable the TCP module, add this to (or uncomment, if already there) `/etc/pulse/default.pa`:

```
load-module module-native-protocol-tcp

```

To allow remote connections to the TCP module, you also have to remember to unblock the service in `/etc/hosts.allow` with the following line:

```
pulseaudio-native: ALL

```

Note: If you are having trouble connecting, use (on server)

```
pacmd>> list-modules

```

(you can even load modules from here!)

#### Zeroconf (Avahi) publishing

For the remote Pulseaudio server to appear in the PulseAudio Device Chooser (`padevchooser`), you will also need to add the `avahi-daemon` to the DAEMONS in rc.conf on both server and clients.

#### Switching the PulseAudio server used by local X clients

To switch between servers on the client from within X, the `pax11publish` command can be used. For example, to switch from the default server to the server at hostname foo:

```
$ pax11publish -e -S foo

```

Or to switch back to the default:

```
$ pax11publish -e -r

```

Note that for the switch to become apparent, the programs using Pulse must be restarted.

### Pulseaudio through JACK

The JACK-Audio-Connection-Kit is popular for audio work, and is widely supported by Linux audio applications. It fills a similar niche as Pulseaudio, but with more of an emphasis on professional audio work. In particular, audio applications such as Ardour and Audacity (recently) work well with Jack.

Pulseaudio provides module-jack-source and module-jack-sink which allow Pulseaudio to be run as a sound server above the JACK daemon. This allows the usage of per-volume adjustments and the like for the apps which need it, play-back apps for movies and audio, while allowing low-latency and inter-app connectivity for sound-processing apps which connect to JACK. However, this will prevent Pulseaudio from directly writing to the sound card buffers, which will increase overall CPU usage.

To just try PA on top of jack you can have PA load the necessary modules on start:

```
pulseaudio -L module-jack-sink -L module-jack-source

```

To use pulseaudio with JACK, JACK must be started up before Pulseaudio, using whichever method you prefer. Pulseaudio then needs to be started loading the 2 relevant modules. Edit `/etc/pulse/default.pa`, and change the following region:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink

### Automatically load driver modules depending on the hardware available
.ifexists module-udev-detect.so
load-module module-udev-detect
.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
load-module module-detect
.endif

```

to the following:

```
### Load audio drivers statically (it is probably better to not load
### these drivers manually, but instead use module-hal-detect --
### see below -- for doing this automatically)
#load-module module-alsa-sink
#load-module module-alsa-source device=hw:1,0
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink
load-module module-jack-source
load-module module-jack-sink

### Automatically load driver modules depending on the hardware available
#.ifexists module-udev-detect.so
#load-module module-udev-detect
#.else
### Alternatively use the static hardware detection module (for systems that
### lack udev support)
#load-module module-detect
#.endif

```

Basically, this prevents module-udev-detect from loading. module-udev-detect will always try to grab your sound-card (JACK has already done that, so this will cause an error). Also, the jack source and sink must be explicitly loaded.

#### QjackCtl with Startup/Shutdown Scripts

Using the settings listed above you can use QjackCtl to execute a script upon startup and shutdown to load/unload PulseAudio. Part of the reason you may wish to do this is that the above changes disable PulseAudio's automatic hardware detection modules. This particular setup is for using PulseAudio in an exclusive fashion with JACK, though the scripts could be modified to unload and load an alternate non-JACK setup, but killing and starting PulseAudio while programs might be using it would become problematic.

The following example could be used and modified as necessary as a startup script that daemonizes PulseAudio and loads the _padevchooser_ program (optional, needs to be built from AUR) called `jack_startup`:

```
#!/bin/bash
#Load PulseAudio and PulseAudio Device Chooser

pulseaudio -D
padevchooser&

```

as well as a shutdown script to kill PulseAudio and the Pulse Audio Device Chooser, as another example called `jack_shutdown` also in the home directory:

```
#!/bin/bash
#Kill PulseAudio and PulseAudio Device Chooser

pulseaudio --kill
killall padevchooser

```

Both scripts need to be made executable:

```
chmod +x jack_startup jack_shutdown

```

then with QjackCtl loaded, click on the _Setup_ button and then the _Options_ tab and tick both "Execute Script after Startup:" And "Execute Script on Shutdown:" and put either use the ... button or type the path to the scripts (assuming the scripts are in the home directory) `~/jack_startup` and `~/jack_shutdown` making sure to save the changes you have made.

### Pulseaudio a través OSS

Agregue lo siguiente a `/etc/pulse/default.pa`:

```
 load-module module-oss

```

Inicie normalmente PulseAudio. Debería tener las entradas y salidas de sus dispositivos OSS.

### Pulseaudio from within a chroot (ex. 32-bit chroot in 64-bit install)

Since a chroot sets up an alternative root for the running/jailing of applications, pulseaudio must be installed within the chroot itself (`pacman -S pulseaudio` within the chroot environment).

Pulseaudio, if not set up to connect to any specific server (this can be done in `/etc/pulse/client.conf`, through the PULSE_SERVER environment variable, or through publishing to the local X11 properties using module-x11-publish), will attempt to connect to the local pulse server, failing which it will spawn a new pulse server. Each pulse server has a unique ID based on the machine-id value in `/var/lib/dbus`. To allow for chrooted apps to access the pulse server, the following directories must be mounted within the chroot:-

```
/var/run
/var/lib/dbus
/tmp
~/.pulse

```

`/dev/shm` should also be mounted for efficiency and good performance. Note that mounting /home would normally also allow sharing of the `~/.pulse` folder.

For specific direction on accomplishing the appropriate mounts, please refer to the wiki on installing a bundled 32-bit system, especially the [additional section](https://wiki.archlinux.org/index.php?title=Arch64_Install_bundled_32bit_system#Additional_mount_option_to_allow_32-bit_apps_to_access_the_64-bit_Pulseaudio_server) specific to Pulseaudio.

### Simultaneous Digital and Analog Output

As an example situation: you want to listen to music at your desktop, using the regular 3.5mm analog outputs into your desktop PC speakers. You also want to feed the same music to your hi-fi system in another room via your sound card's digital output. You would think this would be a simple matter, but for many sound chipsets, it requires some editing to get it set up since the default Pulseaudio profiles allow you to use either analog or digital, but not both simultaneously.

The solution is as follows (with thanks for some useful pointers from: [http://superuser.com/questions/267442/how-to-get-simultaneous-sound-from-pulseadio-on-two-outputs-analog-and-digital](http://superuser.com/questions/267442/how-to-get-simultaneous-sound-from-pulseadio-on-two-outputs-analog-and-digital)). Amarok is used in this example.

*   Install "pavucontrol" (pacman -S pavucontrol). You _won't_ be needing the other useful pulse configuration utility "paprefs" for this task.
*   In a terminal, launch "pacmd" - a command line utility for loading pulse modules
*   Enter the following commands in pacmd in this order (where your numbers for "hw:0,0" are determined by entering "aplay -l" in terminal. One number is the hardware ID for the analog device, the other for the digital):

```
 load-module module-alsa-sink device="hw:0,0" sink_name=analog_output
 load-module module-alsa-sink device="hw:0,1" sink_name=digital_output
 load-module module-combine sink_name=analog_digital slaves=digital_output,analog_output

```

*   Open "pavucontrol" from a terminal
*   Under pavucontrol's "Playback Tab", for the running app Amarok, select "Simultaneous output to Internal Audio, Internal Audio" (you will need to have Amarok playing something to test this)
*   Under the "Configuration Tab" Select "Digital Stereo Duplex (IEC958)" for "Internal Audio" (your exact names may vary here, according to how ALSA has named your hardware). You should now be able to hear Amarok playing on both your analog and digital outputs!

The above solution only holds to long as you have pacmd running, and is specific for the running app (in the above example, Amarok).

To set the the sinks up every reboot and for all audio apps, add the above load-module commands to your **/etc/pulse/default.pa** file. You may need to add them at the start of the file, just above line "### Automatically restore the volume of streams and devices", or it may not work as expected.

Finally, use the Gnome 3 sound preferences to set your system's default "Output" to "Simultaneous output to Internal Audio, Internal Audio".

## Troubleshooting

### No hay sonido después de instalar

### Contenido Flash

Si después de instalar PulseAudio no tiene sonido desde un contenido flash, puede instalar [libflashsupport-pulse](https://aur.archlinux.org/packages/libflashsupport-pulse/) desde el AUR.

#### Sin Tarjetas

Si PulseAudio está iniciado, ejecute `pacmd list`. Si no devuelve ninguna tarjeta, aseguraté de que los dispositivos de ALSA no están en uso:

```
$ fuser -v /dev/snd/*
$ fuser -v /dev/dsp

```

Asegúrese de que ninguna aplicación que use pcm o dst está iniciada antes de inicializar PulseAudio.

#### KDE4

Puede ser que haya otro dispositivo de salida marcado como preferio en phonon. Asegúrese de que en cada catergoría tiene su dispositivo de salida en la parte superior.

**Note:** Pulseaudio doesn't work by default with the Gstreamer phonon-backend. It does, however, with the phonon-vlc backend (available in [extra]).

#### Dispositivo de audio silenciado

Si no hay salida de audio a través de cualquier medio durante el uso de ALSA como dispositivo por defecto, puede que tenga la tarjeta de sonido desactivada. Para activarla, tendrá que lanzar alsamixer y asegurarse de que cada columna, el valor 00, está de color verde. Si no es así, estará apagado el sonido, para activarlo pulse 'm.

```
$ alsamixer -c 0

```

### Fallo al iniciar el Demonio

Prueba a resetear PulseAudio. Hazlo así:

```
$ pulseaudio --kill
$ killall pulseaudio
$ killall -9 pulseaudio
$ rm -rf ~/.pulse*
$ rm -rf /tmp/pulse*

```

Después, inicia PulseAudio.

### padevchooser

Si no puede lanzar el PulseAudio Device Chooser, (re)inicie el Daemon Avahi así:

```
$ /etc/rc.d/avahi-daemon restart

```

### Problemas técnicos y uso intensivo de la CPU desde 0.9.14

El servidor de sonido PulseAudio ha sido reescrito para utilizar la programación de audio basado en temporizadores en lugar del enfoque tradicional por interrupciones. Eso puede provocar problemas con algunos drivers de ALSA. Para desactivarlo, reemplace la línea:

```
load-module module-udev-detect 

```

en `/etc/pulse/default.pa` por:

```
load-module module-udev-detect tsched=0

```

Then restart the PulseAudio server.

### Sonido entrecortado

El sonido entrecortado en pulseaudio puede venir por una configuración errónea de la frecuencia de muestreo en /etc/pulse/daemon.conf. Pruebe cambiando la línea:

```
; default-sample-rate = 44100

```

por

```
default-sample-rate = 48000

```

y reinicie el servidor pulseaudio.

### Volume adjustment doesn't work properly

You might wan't to check

```
/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common

```

If the volume does not appear to increment/decrement properly using `alsamixer` or `amixer`, it may be due to pulseaudio having a larger number of increments (65537 to be exact). Try using larger values when changing volume (e.g. `amixer set Master 655+`).

### Volume gets louder every time a new application is started

If you encounter this issue, you can fix it by uncommenting

```
flat-volumes = no

```

in

```
/etc/pulse/daemon.conf

```

## External links

*   [http://www.pulseaudio.org/wiki/PerfectSetup](http://www.pulseaudio.org/wiki/PerfectSetup) - A good guide to make your configuration perfect
*   [http://www.alsa-project.org/main/index.php/Asoundrc](http://www.alsa-project.org/main/index.php/Asoundrc) - Alsa wiki on .asoundrc
*   [http://www.pulseaudio.org/](http://www.pulseaudio.org/) - PulseAudio official site
*   [http://www.pulseaudio.org/wiki/FAQ](http://www.pulseaudio.org/wiki/FAQ) - PulseAudio FAQ