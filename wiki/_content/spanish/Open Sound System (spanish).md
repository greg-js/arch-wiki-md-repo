El [Open Sound System](https://es.wikipedia.org/wiki/Open_Sound_System) (**OSS**) es una arquitectura de sonido alternativa para sistemas compatibles con UNIX y POSIX. OSS versión 3 era el sistema original de sonido para Linux y estaba incluido en el kernel hasta que fue reemplazado por [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture_(Espa%C3%B1ol) "Advanced Linux Sound Architecture (Español)") (**ALSA**) en 2002, año en que la versión 4 de OSS se convirtió en un producto propietario. Luego, OSSv4 volvió a ser software libre en 2007 cuando [4Front Technologies](http://www.opensound.com/) liberó el código bajo licencia GPL.

## Contents

*   [1 Comparaciones con ALSA](#Comparaciones_con_ALSA)
    *   [1.1 Ventajas de OSS (usuarios)](#Ventajas_de_OSS_.28usuarios.29)
    *   [1.2 Ventajas de OSS (desarrolladores)](#Ventajas_de_OSS_.28desarrolladores.29)
    *   [1.3 Ventajas de ALSA sobre OSS](#Ventajas_de_ALSA_sobre_OSS)
*   [2 Instalacion](#Instalacion)
*   [3 Comprobación](#Comprobaci.C3.B3n)
*   [4 Control del Volumen con el Mezclador](#Control_del_Volumen_con_el_Mezclador)
    *   [4.1 Definiciones de los Colores](#Definiciones_de_los_Colores)
    *   [4.2 Guardar los Niveles del Mezclador](#Guardar_los_Niveles_del_Mezclador)
    *   [4.3 Otros Mezcladores](#Otros_Mezcladores)
*   [5 Configurar aplicaciones para OSS](#Configurar_aplicaciones_para_OSS)
    *   [5.1 Aplicaciones que usan Gstreamer](#Aplicaciones_que_usan_Gstreamer)
    *   [5.2 Aplicaciones que usan OpenAL](#Aplicaciones_que_usan_OpenAL)
    *   [5.3 Audacity](#Audacity)
    *   [5.4 Gajim](#Gajim)
    *   [5.5 MOC](#MOC)
    *   [5.6 MPD](#MPD)
    *   [5.7 Mplayer](#Mplayer)
    *   [5.8 Skype](#Skype)
    *   [5.9 VLC media player](#VLC_media_player)
    *   [5.10 Wine](#Wine)
    *   [5.11 Otras aplicaciones](#Otras_aplicaciones)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Usar las teclas multimedia con OSS](#Usar_las_teclas_multimedia_con_OSS)
    *   [6.2 Modificar la frecuencia de muestreo](#Modificar_la_frecuencia_de_muestreo)
    *   [6.3 Un sencillo applet para la bandeja del sistema](#Un_sencillo_applet_para_la_bandeja_del_sistema)
    *   [6.4 Iniciar ossxmix en la bandeja del sistema al arrancar](#Iniciar_ossxmix_en_la_bandeja_del_sistema_al_arrancar)
        *   [6.4.1 KDE](#KDE)
        *   [6.4.2 Gnome](#Gnome)
    *   [6.5 Guardar la salida de audio de un programa](#Guardar_la_salida_de_audio_de_un_programa)
    *   [6.6 Suspensión e hibernación](#Suspensi.C3.B3n_e_hibernaci.C3.B3n)
    *   [6.7 Cambiar la salida de sonido predeterminada](#Cambiar_la_salida_de_sonido_predeterminada)
    *   [6.8 Creative Sound Blaster X-Fi Surround 5.1 USB SB1090](#Creative_Sound_Blaster_X-Fi_Surround_5.1_USB_SB1090)
    *   [6.9 Emular ALSA](#Emular_ALSA)
        *   [6.9.1 Instrucciones](#Instrucciones)
    *   [6.10 Configurar el controlador específico](#Configurar_el_controlador_espec.C3.ADfico)
*   [7 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [7.1 Solución de problemas con dispositivos HD Audio](#Soluci.C3.B3n_de_problemas_con_dispositivos_HD_Audio)
        *   [7.1.1 Conocer la causa del problema](#Conocer_la_causa_del_problema)
        *   [7.1.2 Cómo resolverlo](#C.C3.B3mo_resolverlo)
    *   [7.2 Sonido distorsionado con los MMS en Totem](#Sonido_distorsionado_con_los_MMS_en_Totem)
    *   [7.3 El Micrófono funciona a través de los altavoces](#El_Micr.C3.B3fono_funciona_a_trav.C3.A9s_de_los_altavoces)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Comparaciones con ALSA

A continuación se relacionan algunas ventajas y desventajas de OSS comparado con el uso de Advanced Linux Sound Architecture.

### Ventajas de OSS (usuarios)

*   Control sobre el nivel del volumen de cada aplicación.
*   Menor latencia debido a que todo se ejecuta dentro del kernel de Linux. El tiempo de respuesta inicial en las aplicaciones de audio, en la mayoría de los casos, es mejor.
*   OSS siempre dispone de mezcla de sonido, ALSA no.
*   La mezcla de sonido es de mayor calidad, debido a que OSS usa de forma más precisa las matemáticas en su mezcla de sonido.
*   Algunas tarjetas de sonido antiguas tienen mejor soporte.

### Ventajas de OSS (desarrolladores)

*   Suporte para el controlador en el espacio del usuario.
*   Accesibilidad. OSS también funciona con BSDs y Solaris.
*   El API es más limpio, más fácil de usar.

### Ventajas de ALSA sobre OSS

*   Mejor soporte para aparatos de audio USB.
*   Soporte para aparatos de audio Bluetooth.
*   Soporte para el software de modems [AC'97](https://en.wikipedia.org/wiki/AC%2797 "wikipedia:AC'97") y [HD Audio](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio").
*   Mejor soporte para aparatos MIDI.
*   Soporte para suspender.
*   Mejor soporte para detección de clavijas (*jack*).

**Nota:**

*   OSS tiene soporte de salida experimental para dispositivos de audio USB, pero no de entrada.
*   OSS soporta dispositivos MIDI con la ayuda de un sintetizador de software como [Timidity](/index.php/Timidity "Timidity") o [FluidSynth](/index.php/FluidSynth "FluidSynth").

## Instalacion

Instale [oss](https://aur.archlinux.org/packages/oss/) que está disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). También hay una versión de desarrollo de OSS disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") con el paquete [oss-git](https://aur.archlinux.org/packages/oss-git/).

Esto instalará OSS, ejecute el script de instalación de OSS (desactivando temporalmente los módulos de ALSA) e instale los módulos del kernel de OSS. Dado que ALSA está activado por defecto en los scripts de arranque, es necesario desactivarlo para que no entre en conflicto con OSS. Se puede hacer esto mediante la inclusión del módulo en blacklist:

 `/etc/modprobe.d/alsa_blacklist.conf`  `install soundcore /bin/false` 

Después del blacklisting del modulo, puede [activar](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)") el demonio **oss** para que se inicie al arranque.

Si su usuario no forma parte del grupo de *audio*, añádalo, y **reinicie sesión** para que los cambios tengan efecto:

```
# gpasswd -a $USER audio

```

En caso de que OSS no pueda detectar su tarjeta de sonido cuando reinicie, ejecute:

```
# ossdetect -v
# soundoff && soundon

```

## Comprobación

**Advertencia:** El nivel inicial del volumen predeterminado es muy alto. Por eso, no use auriculares y (si es posible) baje físicamente el nivel del altavoz antes de ejecutar la prueba.

**Comprobar OSS, ejecutando:**

```
$ osstest

```

Debería oir música durante la prueba. Si no hay sonido, trate de ajustar el nivel del volumen o consulte la sección de [solución de problemas](#Soluci.C3.B3n_de_problemas).

Para escuchar sonidos procedentes de más de una aplicación simultáneamente es necesario usar `vmix`, el software de mezcla de OSS.

**Comprobar que vmix está habilitado, ejecutando:**

```
$ ossmix -a | grep -i vmix

```

Debería ser posible ver una línea del tipo `vmix0-enable ON|OFF (currently ON)`. Si no ve ninguna línea que inicie con `vmix`, probablemente significa que `vmix` no se ha conectado con el dispositivo de audio. Para conectar `vmix`, ejecute la orden:

```
$ vmixctl attach device

```

donde *device* es la tarjeta de audio, por ejemplo, `/dev/oss/oss_envy240/pcm0`.

Para evitar tener que volver a ejecutar esta orden manualmente en el futuro, puede agregarla en `/usr/lib/oss/soundon.user`, como se sugiere en [este artículo](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output).

Si recibe el error **«Device or resource busy»** («Dispositivo o recurso ocupado»), debe agregar `vmix_no_autoattach=1` en `/usr/lib/oss/conf/osscore.conf` y, seguidamente, reiniciar.

**Ver qué dispositivos son reconocidos, ejecutando:**

```
$ ossinfo

```

Debería ver una lista de los dispositivos en *Device Objects* o *Audio Devices*. Si el dispositivo que desea utilizar no se encuentra en la parte superior de estas secciones, debe editar el archivo `/usr/lib/oss/etc/installed_drivers` y colocar el controlador para el dispositivo en la parte superior. Puede ser necesario hacer un:

```
$ soundoff && soundon

```

Si esto no funciona, comente todos los controladores, excepto los que figuran para el dispositivo propio.

## Control del Volumen con el Mezclador

Para controlar el nivel del volumen de los diferentes aparatos, se tienen que ajustar los niveles con los mixers. Hay dos mixers:

*   **ossmix**: un mixer en línea de comandos, similar al mixe de audio `mixerctl` de BSD.
*   **ossxmix**: un mixer gráfico basado en GTK+.

Los controles primarios de `ossxmix` tendrán el siguiente aspecto:

```
 / High Definition Audio ALC262 \    --------------------------------> 1
/________________________________\________________________________
|                                                                 \
| [x] vmix0-enable [vmix0-rate: 48.000kHz]      vmix0-channels    |--> 2
|                                               [ Stereo [v] ]    |
|                                                                 |
|  __codec1______________________________________________________ |
| |  _jack______________________________________________________ ||--> 3
| | |  _int-speaker_________________   _green_________________  |||
| | | |                             | |                       | |||
| | | |  _mode_____ | |             | |  _mode_____   | |     | |||
| | | | [ mix [v] ] o o [x] [ ]mute | | [ mix  [v] ]  o o [x] | |||
| | | |             | |             | |               | |     | |||
| | | |_____________________________| |_______________________| |||
| | |___________________________________________________________|||
| |______________________________________________________________||
| ___vmix0______________________________________________________  |
| |  __mocp___  O O   _firefox_  O O  __pcm7___  O O            | |--> 4
| | |         | O O  |         | x x |         | O O            | |
| | | | |     | x O  | | |     | x x | | |     | O O            | |
| | | o o [x] | x x  | o o [x] | x x | o o [x] | O O            | |
| | | | |     | x x  | | |     | x x | | |     | O O            | |
| | |_________| x x  |_________| x x |_________| O O            | |
| |_____________________________________________________________| |
|_________________________________________________________________|

```

1.  Una pestaña por cada tarjeta de sonido.
2.  La configuración especifica de `vmix` (mixer virtual) aparece abajo. Eso incluye frecuencia de muestreo (*«sampling rate»*) y prioridad del mexclador (*«mixer priority»*).
3.  Estas son las configuraciones (entrada y salida) de las tomas (*«jack»*) de la tarjeta de sonido. Cada controlador del mixer, que se muestra aquí, lo provee su propia tarjeta de sonido.
4.  Los controles del mezclador y los medidores del sonido de la aplicación `vmix`. Si la aplicación no produce ningún sonido será etiquetada como `pcm08, pcm09...`, y, en cuanto reproduzca algún sonido, aparecerá el nombre de la aplicación.

### Definiciones de los Colores

Para el audio de alta definición (HD), `ossxmix` mostrará la configuración de cada toma (*jack*) coloreada según los siguientes colores predefinidos:

| Color | Tipo | Conector |
| verde | canal frontal (salida estéreo) | 3.5mm TRS |
| negro | canal posterior (salida estéreo) | 3.5mm TRS |
| gris | canal lateral (salida estéreo) | 3.5mm TRS |
| amarillo | central y subwoofer (salida dual) | 3.5mm TRS |
| azul | línea de nivel (entrada estéreo) | 3.5mm TRS |
| rosa | micrófono (entrada mono) | 3.5mm TS |

### Guardar los Niveles del Mezclador

Los niveles del mezclador se guardan cuando se apaga el equipo. Si desea guardar el nivel de sonido de inmediato, ejecute, como root:

```
# savemixer

```

`savemixer` se puede utilizar para guardar los niveles del mixer en un archivo con el parámetro `-f` y restaurarlos con el parámetro `-L`.

### Otros Mezcladores

Otras mixer soportados por OSS:

*   **Gnome Volume Control** — para [GNOME](/index.php/GNOME "GNOME").

	[http://library.gnome.org/users/gnome-volume-control/stable/](http://library.gnome.org/users/gnome-volume-control/stable/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **Kmix** — para [KDE](/index.php/KDE "KDE").

	[http://www.kde.org/applications/multimedia/kmix/](http://www.kde.org/applications/multimedia/kmix/) || [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix)

*   **VolWheel** — para [LXDE](/index.php/LXDE "LXDE").

	[http://oliwer.net/b/volwheel.html](http://oliwer.net/b/volwheel.html) || [volwheel](https://www.archlinux.org/packages/?name=volwheel)

	Después de instalar VolWheel, tendrá que hacer lo que sigue para habilitar la compatibilidad con OSS:

*   Añada lo siguiente al archivo `autostart` de [LXDE](/index.php/LXDE "LXDE") :

```
 echo "volwheel" >> ~/.config/lxsession/LXDE/autostart

```

*   Pulse sobre el icono de la bandeja del sistema, eliga *Preferencias* y cambie:
    *   Driver: **OSS**.
    *   Default Channel: **vmix0-outvol** (averigue qué canal de salida va a utilizar desde `ossmix`).
    *   Default Mixer: **ossxmix**.
    *   En la pestaña MiniMixer (opcional), añada **vmix0-outvol** y opcionalmente otros.

## Configurar aplicaciones para OSS

### Aplicaciones que usan Gstreamer

Si tiene problemas con las aplicaciones que usan Gstreamer para audio, pruebe eliminando [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio), e instalando el paquete [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) que es requerido por `oss4sink` y `oss4src`.

Puede cambiar la configuración de GStreamer a fin de enviar el sonido a OSS, en lugar de a ALSA por defecto, con `gstreamer-properties` (parte del paquete [gnome-media](https://www.archlinux.org/packages/?name=gnome-media) ). Después de iniciar `gstreamer-properties`, se tienen que modificar las opciones de la siguiente manera:

*   en la sección *Default Output*: si OSS no está disponible como un plugin, cambie *Plugin* por **Custom** y *Pipeline* por **oss4sink**.
*   en la sección *Default Input*: si OSS no está disponible, cambie *Plugin* por **Custom** y *Pipeline* por **oss4src**.

**Nota:** También puede usar `osssrc` como una alternativa a `oss4src` si encuentra que reproduce un mejor sonido.

Para algunas aplicaciones (por ejemplo, Rhythmbox, Totem) las configuraciones ajustadas para `gstreamer-properties` no tienen ningún efecto, ya que se basan en `musicaudiosink` en lugar de `audiosink` (el cual es modificado por `gstreamer-properties`).

Una posible solución puede consistir en ajustar los valores para `audiosink` con `gstreamer-properties` y usar `gconf-editor` para copiar el valor de `/system/gstreamer/0.10/default/audiosink` a `musicaudiosink` (en el mismo lugar).

Si está utilizando Phonon con el backend GStreamer tendrá que establecer la variable del entorno correspondiente:

```
export PHONON_GST_AUDIOSINK=oss4sink

```

Agregue esta orden al archivo `~/.bashrc` para cargarlo al iniciar sesión.

### Aplicaciones que usan OpenAL

Por defecto OpenAL utiliza ALSA. Para cambiar esto, simplemente defina que va a usar OSS en `/etc/openal/alsound.conf`:

 `/etc/openal/alsound.conf` 
```
drivers=oss

```

### Audacity

Si [Audacity](http://audacity.sourceforge.net/) se inicia, pero se queja de que no puede abrir el dispositivo o simplemente no funciona nada, entonces puede que esté utilizando `vmix`, ya que Audacity espera hasta tener el acceso exclusivo al dispositivo de sonido. Para solucionar este problema, antes de iniciar audacity, ejecute:

```
$ ossmix vmix0-enable OFF

```

Puede restaurar `vmix`, después de terminar con audacity, ejecutando:

```
$ ossmix vmix0-enable ON

```

### Gajim

Por defecto, [Gajim](http://gajim.org/) usa `aplay -q` para reproducir sonido. Para OSS puede cambiarlo por el equivalente `ossplay -qq`, para lo cual vaya a *Editar > Preferencias > Avanzado*, y abra *Editar Configuración Avanzada* y modifique la variable `soundplayer` en consecuencia.

### MOC

Para utilizar [MOC](/index.php/Moc "Moc") con OSS v4.1 debe cambiar la sección `OSSMixerDevice` en `/dev/ossmix` del archivo de configuración (ubicado en `~/.moc`). Si tiene problemas con la interfaz pruebe cambiando `OSSMixerChannel` presionando `w` en `mocp` (para cambiar a mixer software).

### MPD

[MPD](/index.php/MPD "MPD") se configura a través de `/etc/mpd.conf` o `~/.mpdconf`. Compruebe ambos archivos, en busca de algo que se parezca a:

 `/etc/mpd.conf` 
```
...
audio_output {
    type    "alsa"
    name    "Some Device Name"
}
...
```

Si encuentra una configuración de ALSA no comentada (esto es, las líneas que comienzan sin almohadilla `#`) como la de arriba, comente todas las salidas, o bórrelas, y añada lo siguiente:

 `/etc/mpd.conf` 
```
...
audio_output {
    type    "oss"
    name    "Nombre del Dispositivo OSS"
}
...
```

No deberían ser necesarias configuraciones ulteriores para los demás usuarios. Sin embargo, si experimenta problemas (MPD no funciona correctamente después de que se haya reiniciado), o si prefiere tener un archivo de configuración específico (es decir, más configurado por el usuario, menos configurado automáticamente), la salida de audio para OSS puede ser específicamente configurada de la siguiente manera:

*   Primeramente ejecute:

```
$ ossinfo | grep /dev/dsp

```

*   Busque una línea similar a `/dev/dsp -> /dev/oss/<SOME_CARD_IDENTIFIER>/pcm0`. Tome nota de `<SOME_CARD_IDENTIFIER>` y añada las líneas resaltadas en negrita a `audio_output` de OSS en el archivo de configuración MPD:

 `/etc/mpd.conf` 
```
...
audio_output {
    type            "oss"
    name            "Nombre del Dispositivo OSS"
    **device          "/dev/oss/<SOME_CARD_IDENTIFIER>/pcm0"**
    **mixer_device    "/dev/oss/<SOME_CARD_IDENTIFIER>/mix0"**
}
...

```

Consulte también: [Music Player Daemon#Global configuration](/index.php/Music_Player_Daemon#Global_configuration "Music Player Daemon").

### Mplayer

Si está utilizando la interfaz gráfica de usuario (SMplayer, GNOME MPlayer, etc.), es necesario cambiar la configuración de la salida de OSS en los ajustes de audio. Si usa [MPlayer](/index.php/MPlayer "MPlayer"), desde la línea de comandos debe especificar la salida de sonido:

```
$ mplayer -ao oss /some/file/to/play.mkv

```

Si no quiere molestarse en escribirla una y otra vez, agregue `ao=oss` al propio archivo de configuración (`~/.mplayer/config`).

Consulte también: [MPlayer#Configuration](/index.php/MPlayer#Configuration "MPlayer").

### Skype

El paquete [skype](https://www.archlinux.org/packages/?name=skype) solo incluye soporte para ALSA, ya que el soporte para OSS fue eliminado en las versiones recientes. Para tener una versión OSS compatible con [Skype](/index.php/Skype "Skype"), instale el paquete [skype-oss](https://aur.archlinux.org/packages/skype-oss/) desde el repositorio Community.

O utilice [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) con module-oss: Modifique `/etc/pulse/default.pa`, comentando la línea que comienza con `load-module module-udev-detect` y añada `load-module module-oss device="/dev/dsp" sink_name=output source_name=input mmap==0`.

Véase también: [Skype#Skype-OSS Sound (Pre-2.0)](/index.php/Skype#Skype-OSS_Sound_.28Pre-2.0.29 "Skype").

### VLC media player

Puede seleccionar OSS como la salida por defecto en las configuraciones de audio.

### Wine

Para proporcionar soporte de OSS en [Wine](/index.php/Wine "Wine") inicie:

```
$ winecfg

```

y, en la pestaña `Audio`, seleccione `OSS Driver`.

Consulte también: [Wine#Sound](/index.php/Wine#Sound "Wine").

### Otras aplicaciones

*   Si no puede hacer funcionar una aplicación no listada aquí, pruebe buscando en la página [Configurar Aplicaciones para OSSv4](http://www.4front-tech.com/wiki/index.php/Configuring_Applications_for_OSSv4).
*   Busque los paquetes específicos para OSS usando `pacman -Ss -- -oss` o busque en [AUR](https://aur.archlinux.org/packages.php?K=-oss&start=0&PP=100).

## Consejos y trucos

### Usar las teclas multimedia con OSS

Una manera fácil de activar/desactivar el sonido y subir/bajar el volumen es usar el script [ossvol](https://aur.archlinux.org/packages/ossvol/) disponible en [AUR](/index.php/AUR "AUR"). Para más información sobre el script consulte [este artículo](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#ossvol) de la wiki de OSS.

Una vez instalado, escriba:

```
$ ossvol -t

```

para silenciarlo, o:

```
$ ossvol -h

```

para ver las órdenes disponibles.

**Nota:** Si `ossvol` da un error como **Bad mixer control name(987) 'vol'**, tiene que editar el script `/usr/bin/ossvol` y cambiar la variable `CHANNEL` al canal por defecto (normalmente `vmix0-outvol`).

Si desea utilizar las teclas multimedia con `ossvol`, consulte [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") y asegúrese de que están correctamente configuradas. Después puede utilizar, por ejemplo, [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") para asociarlo al script `ossvol`. Añada lo siguiente al archivo `~/.xbindkeysrc`:

 `~/.xbindkeysrc` 
```
# Toggle mute
"ossvol -t"
    m:0x0 + c:121
    XF86AudioMute

# Lower volume
"ossvol -d 2"
    m:0x0 + c:122
    XF86AudioLowerVolume

# Raise volume
"ossvol -i 2"
    m:0x0 + c:123
    XF86AudioRaiseVolume

```

y, opcionalmente, cambie las teclas multimedia con los atajos que prefiera.

### Modificar la frecuencia de muestreo

El cambio de la frecuencia de muestreo de salida no se hace evidente al principio. Las frecuencias de muestreo solo pueden ser modificadas por el superusuario y `vmix` no debe ser usado por ningún programa cuando se solicita un cambio. Antes de seguir alguno de estos pasos, asegúrese de utilizar un receptor/amplificador y altavoces de calidad y no simplemente lo altavoces del PC. Si está utilizando solamente los altavoces del ordenador, no se moleste en cambiar nada aquí, ya que no notará la diferencia.

Por defecto, la frecuencia de muestreo es 48000Hz. Hay varias condiciones en las que es posible que desee cambiar esta situación. Depende todo de la utilización que se haga. Es conveniente ajustar la frecuencia de muestreo correspondiente a la fuente utilizada más a menudo. Si el equipo tiene que cambiar la frecuencia de muestreo de una fuente para adaptarla a la del hardware, es probable, aunque no se garantiza, que va a tener una pérdida de calidad de audio. Esto es más notable en el downsampling (submuestreo) (es decir, 96000Hz → 48000Hz ). Hay un artículo sobre este tema en [«Stereophile»](http://www.stereophile.com/news/121707lucky/) que ha sido [discutido](http://lists.apple.com/archives/coreaudio-api/2008/Jan/msg00272.html) en la lista de correo «CoreAudio API» de Apple, por si desea obtener más información acerca de este tema.

Algunos ejemplos de frecuencias de muestreo:

	44100hz

	Frecuencia de muestreo estándar de [Red Book](https://en.wikipedia.org/wiki/Red_Book_(audio_CD_standard) para el CD de audio.

	88000hz

	Frecuencia de muestreo de [SACD](https://en.wikipedia.org/wiki/Super_Audio_CD "wikipedia:Super Audio CD") de alta definición. Es raro que su placa base soporte este tipo de frecuencia.

	96000hz

	Frecuencia de muestreo de la mayoría de las descargas de audio de alta definición. Si su placa base es una placa base [AC'97](https://en.wikipedia.org/wiki/AC%2797 "wikipedia:AC'97"), probablemente esta será su frecuencia más alta.

	192000hz

	Frecuencia de muestreo de BluRay, y de algunas (muy pocas) descargas de alta definición. Soporte para receptores de audio externo y limitado a los dispostivos de gama alta. No todas las placas base lo soportan. Un ejemplo de chipset de una placa base que podría soportarlo lo incluye [HD Audio](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio").

Para comprobar cuál es su frecuencia de muestreo actualmente configurada, ejecute

```
ossmix | grep rate

```

Probablemente verá una salida como esta `"vmix0-rate <decimal value> (currently 48000) (Read-only)"`

Si no ve `vmix0-rate` (o `vmix1-rate`, etc.), probablemente significa que `vmix` está desactivado. En ese caso, OSS usará la frecuencia requerida por el programa que utiliza el dispositivo, ignorando esta sección. Una excepción es la tarjeta Envy24 (y Envy24HT) que tiene un valor especial `envy24.rate`, lo que supone una función similar (consulte la página del manual de `oss_envy24`).

Pasos para efectuar el cambio:

1.  Primero, asegúrese de que su tarjeta es capaz de utilizar la nueva frecuencia. Ejecute `ossinfo -v2` y vea si la frecuencia deseada está presente en *Native sample rates*.
2.  Como root, ejecute `/usr/lib/oss/scripts/killprocs.sh`. Tenga en cuenta que esto cerrará cualquier programa que actualmente tenga un canal de sonido abierto.
3.  Después que todos los programas que estaba utilizando `vmix` finalicen, ejecute como root: `vmixctl rate /dev/dsp 96000`, sustituyendo la frecuencia presente por la frecuencia deseada (y `ossmix envy24.rate 96000` si fuera aplicable).
4.  Ejecute `ossmix | grep rate` y compruebe `vmix0-rate <decimal value> (currently 96000) (Read-only)` para ver si todo ha salido correctamente.
5.  **Haga que los cambios sean permanentes** añadiendo lo siguiente al archivo `soundon.user`:

 `/usr/lib/oss/soundon.user` 
```
#!/bin/sh

vmixctl rate /dev/dsp 96000
# ossmix envy24.rate 96000 # uncomment if you have an Envy24(HT) card

exit 0

```

y hágalo ejecutable:

```
# chmod +x /usr/lib/oss/soundon.user 

```

### Un sencillo applet para la bandeja del sistema

Para aquellos que quieran un applet ligero de OSS en la bandeja del sistema consulte [esto](http://pastebin.furver.se/0xflchkfz/).

Para instalarlo:

*   Descargue [el script](http://pastebin.furver.se/0xflchkfz/0xflchkfz.txt) con cualquier nombre que desee (por ejemplo `ossvolctl`)
*   Hágalo ejecutable:

```
$ chmod +x ossvolctl

```

*   Y copielo en `/usr/bin`:

```
# cp ossvolctl /usr/bin/ossvolctl

```

o:

```
# install -Dm755 ossvolctl /usr/bin/ossvolctl

```

### Iniciar ossxmix en la bandeja del sistema al arrancar

#### KDE

Cree un archivo para lanzar aplicaciones con el nombre `ossxmix.desktop` en el directorio local para lanzar aplicaciones (`~/.local/share/applications/` e introduzca:

 `~/.local/share/applications/ossxmix.desktop` 
```
[Desktop Entry]
Name=Open Sound System Mixer
GenericName=Audio Mixer
Exec=ossxmix -b
Icon=audio-card
Categories=Application;GTK;AudioVideo;Player;
Terminal=false
Type=Application
Encoding=UTF-8

```

Para que se inicie automáticamente con el sistema, añádalo a la lista autostart del sistema en *System Settings > System Administration > Startup and Shutdown > Autostart*.

#### Gnome

Como root, cree el archivo `/usr/local/bin/ossxmix_bg`, con el siguiente contenido:

 `/usr/local/bin/ossxmix_bg` 
```
#!/bin/sh

exec /usr/bin/ossxmix -b

```

Vaya a *System > Preferences > Aplicaciones Start Up* y:

*   Pinche en *Agregar*, escriba `OSSMIX` en el campo *Nombre* y la ruta `/usr/local/bin/ossxmix_bg` en el campo *Comando*; a continuación, pinche en el botón *Agregar*.

*   Reinicie la sesión para ver los cambios.

### Guardar la salida de audio de un programa

*   [Grabar la salida de sonido de un programa](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Recording_sound_output_of_a_program).

### Suspensión e hibernación

OSS no admite automáticamente la suspensión, lo que significa que es necesario detener manualmente OSS antes de suspender o hibernar y reiniciar después.

OSS proporciona `soundon` y `soundOff` para activar y desactivar OSS, aunque todos los procesos que estén utilizando el sonido deben cesar primero.

El script siguiente es un método bastante básico para cerrar automáticamente OSS antes de la suspensión y recargarlo después.

 `/etc/pm/sleep.d/50osssound` 
```
#!/bin/sh
. "${PM_FUNCTIONS}"

suspend_osssound()
{
    /usr/lib/oss/scripts/killprocs.sh
    /usr/sbin/soundoff
}

resume_osssound()
{
    /usr/sbin/soundon
}

case "$1" in
    hibernate|suspend)
        suspend_osssound
 	;;
    thaw|resume)
 	resume_osssound
 	;;
    *) exit $NA
 	;;
esac

```

Guarde el contenido del script (como root) en `/etc/pm/sleep.d/50ossound` y hágalo ejecutable:

```
chmod a+x /etc/pm/sleep.d/50ossound

```

**Advertencia:** Este script es bastante básico y terminará cualquier aplicación que esté usando directamente OSS, por lo tanto, guarde sus trabajos antes de suspender/hibernar.

Otra alternativa sería usar [s2ram](/index.php/Suspend_to_RAM "Suspend to RAM") para suspender. Basta con crear un script de suspensión a `/sbin/suspend` y hacerlo ejecutable

```
 #!/bin/sh

 ## Checking if you are a root or not
 if ! [ -w / ]; then
   echo >&2 "This script must be run as root"
   exit 1
 fi

 s2ram -f

 sleep 2

 /etc/rc.d/oss restart 2>/tmp/oss.txt || echo "OSS restart failed, check /tmp/oss.txt for information"

```

Con esto, todas las aplicaciones deben quedar funcionando bien.

**Nota:** Si utiliza el navegador Opera debe terminar `operapluginwrapper` antes de suspender. Para hacerlo añada `pid=$(pidof operapluginwrapper) && kill $pid` antes de `s2ram -f`.

### Cambiar la salida de sonido predeterminada

Cuando se ejecuta `osstest`, la primera prueba se supera por el primer canal, pero no por el canal de la derecha o por los canales estéreos, en los cuales el sonido sale distorsionado y/o silbante. Si sucede esto es que ha sido asignada la salida de audio equivocada.

```
*** Scanning sound adapter #-1 ***
/dev/oss/oss_hdaudio0/pcm0 (audio engine 0): HD Audio play front
- Performing audio playback test... 
<left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)>

```

La izquierda suena bien, el derecho y estéreo suenan distorsionados.

Deje que la prueba continúe hasta obtener una salida que funcione:

```
/dev/oss/oss_hdaudio0/spdout0 (audio engine 5): HD Audio play spdif-out 
- Performing audio playback test... 
<left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)> 

```

Si se supera la prueba en todos los canales, izquierdo, derecho y estéreo, proceda con el siguiente paso.

Para cambiar las órdenes de salida por defecto consulte [este artículo de la wiki de OSS](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output). Cambie la configuración por la que se ajuste a su caso, por ejemplo:

```
 # ln -sf /dev/oss/oss_hdaudio0/spdout0 /dev/dsp_multich

```

Para obtener un sonido envolvente (4.0-7.1) seleccione `dsp_multich`, con solo 2 canales, `dsp` debería funcionar. Consulte [esto](http://manuals.opensound.com/usersguide/dsp.html) para conocer todos los dispositivos disponibles.

### Creative Sound Blaster X-Fi Surround 5.1 USB SB1090

Esta información proviene del [4front-tech foro](http://www.4front-tech.com/forum/viewtopic.php?f=3&t=3423).

Es sorprendente saber que la tarjeta externa no funciona solo a causa de la ausencia del valor de retorno *true* en la función `write_control_value(...)` en `ossusb_audio.c`.

Para solucionar este problema, es necesario una recompilación de OSS, por ahora.

*   Obtenga la última versión de OSS desde los repositorios de Arch

```
[https://projects.archlinux.org/svntogit/community.git/tree/trunk?h=packages/oss](https://projects.archlinux.org/svntogit/community.git/tree/trunk?h=packages/oss)

```

*   Extráigalo.
*   Para ir a la carpeta de destino utilice la orden `cd`
*   Ejecute `makepkg --nobuild`
*   Vaya a la carpeta `src/kernel/drv/oss_usb/` con la orden `cd` y edite `ossusb_audio.c`: añada `return 1;`.
    *   Debería quedar así:

 `ossusb_audio.c` 
```
static int
write_control_value (ossusb_devc * devc, udi_endpoint_handle_t * endpoint,
                     int ctl, int l, unsigned int v)
{
     return 1;
...

```

*   Vaya a la carpeta `src/kernel/setup` con `cd` y edite `srcconf_linux.inc`, busque `-Werror` y elimínelo, de lo contrario OSS no se compilará.
*   Haga `makepkg --noextract`

Ahora hay que instalar el paquete con `pacman -U`. Remueva primero OSS si ya está instalado.

### Emular ALSA

Es posible configurar `alsa-lib` para utilizar OSS como su sistema de audio de salida. Esto funciona como una especie de emulación de ALSA.

Nótese, sin embargo, que este método puede introducir una latencia adicional en el sonido de salida, y que la emulación no es completa y no funciona con todas las aplicaciones. No funciona, por ejemplo, con los programas que tratan de detectar los dispositivos que usan ALSA.

Así que, como la mayoría de las aplicaciones son compatibles con OSS directamente, utilice este método solo como último recurso.

En el futuro, estarán disponibles métodos más completos para emular ALSA, como `libsalsa` y `cuckoo`.

#### Instrucciones

*   Instale el paquete `alsa-plugins`, disponible en los repositorios oficiales.:

*   Modifique el archivo `/etc/asound.conf` como sigue:

```
pcm.oss {
   type oss
    device /dev/dsp
}

pcm.!default {
    type oss
    device /dev/dsp
}

ctl.oss {
    type oss
    device /dev/mixer
}

ctl.!default {
    type oss
    device /dev/mixer
}

```

**Nota:** Si no desea utilizar más OSS, no se olvide de revertir los cambios realizados en `/etc/asound.conf`.

### Configurar el controlador específico

Si algo no funciona, existe la posibilidad de que se deba a algunos ajustes de OSS para el controlador específico o simplemente son inadecuados para el controlador.

Para solucionarlo:

*   Averigüe qué controlador se utiliza:

 `$ lspci -vnn | grep -i -A 15 audio` 
```
00:1e.2 Multimedia audio controller [0401]: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) AC'97 Audio Controller [8086:266e] (rev 03)
Subsystem: Hewlett-Packard Company NX6110/NC6120 [103c:099c]
Flags: bus master, medium devsel, latency 0, IRQ 21
I/O ports at 2100 [size=256]
I/O ports at 2200 [size=64]
Memory at d0581000 (32-bit, non-prefetchable) [size=512]
Memory at d0582000 (32-bit, non-prefetchable) [size=256]
Capabilities: <access denied>
Kernel driver in use: *oss_ich*
Kernel modules: snd-intel8x0

```

*   Localice el archivo de configuración del dispositivo en:

```
# cd /usr/lib/oss/conf/

```

*   Trate de cambiar los valores predeterminados. Hay solo unos pocos ajustes, y son fáciles de entender.

Por ejemplo, al configurar:

```
ich_jacksense = 1

```

en `oss_ich.conf`, enciende `jack-sense` (que es responsable de reconocer los auriculares conectados y silenciar el altavoz). Otros ajustes para`jack-sense` se encuentra en `hdaudio.conf` donde hay que cambiar la variable `hdaudio_jacksense`.

*   [Reinicie](/index.php/Daemon "Daemon") el demonio **oss** para que los cambios surtan efecto.

## Solución de problemas

### Solución de problemas con dispositivos HD Audio

#### Conocer la causa del problema

Si se dispone de un dispositivo de sonido HD Audio, es muy probable que tenga que ajustar algunos parámetros del mezclador antes de que el audio funcione correctamente.

Los dispositivos HD Audio son muy potentes en el sentido de que pueden contener una gran variedad de pequeños circuitos (llamados *widgets*) que pueden ser ajustado vía software en cualquier momento. Estos controles están disponibles en el mixer, y se pueden utilizar, por ejemplo, para activar una toma de auriculares reasignándolo como una toma de entrada de sonido en lugar de una toma de salida de sonido.

Sin embargo, esto es un problema secundario, el gran problemas está, sobre todo, en que el estándar HD Audio es más flexible de lo que, tal vez, debería ser, ya que los vendedores, a menudo, solo se preocupan de conseguir el correcto funcionamiento de sus *driver oficiales*.

Luego, cuando se utilizan dispositivos HD Audio, a menudo se encuentran controles del mezclador desorganizados que no funcionan en absoluto para ninguna de las configuraciones por defecto, siendo necesario probar todas las combinaciones posibles de los controles del mixer hasta alcanzar una configuración que funcione.

#### Cómo resolverlo

Abra `ossxmix` y trate de cambiar todos los controles del mezclador en el **área central** (*«middle area»*), que contiene los controles específicos de las tarjetas de sonido, tal como se explica en la sección anterior [Control de volumen](#Control_del_Volumen_con_el_Mezclador).

Probablemente esté interesado en configurar un programa para grabar/reproducir continuamente en segundo plano (por ejemplo, `ossrecord - | ossplay -` para grabar, o `osstest -lV` para reproducir), mientras se está cambiando la configuración del mezclador con `ossxmix` en primer plano.

*   Suba cada deslizador de los controles del volumen.
*   En cada cuadro de opción, trate de cambiar la opción seleccionada, probando todas las combinaciones posibles.
*   Si se obtiene ruido, trate de bajar y/o silenciar algunos controles del volumen, hasta encontrar la fuente del ruido.
*   Edite el archivo `/usr/lib/oss/conf/oss_hdaudio.conf`, quite los comentarios (`#`) y modifique `hdaudio_noskip=0` con un valor de **0 a 7**, lo cual le va a permitir disponer de más opciones relativas a las clavijas en `ossxmix`.

**Nota:** Si modifica los archivos, [reinicie](/index.php/Daemon "Daemon") el demonio **oss** para que los cambios surtan efecto.

### Sonido distorsionado con los MMS en Totem

Si los flujos tienen un sonido distorsionado o producen ruidos extraños en Totem, es posible probar reproducir con otro backend como [FFmpeg](/index.php/FFmpeg "FFmpeg"). Esto no va a solucionar el problema, que de alguna manera aparece en GStreamer durante la reproducción de secuencias de MMS, pero se le dará la opción de reproducir con buena calidad de sonido. Reproducir con MPlayer es simple:

```
# mplayer mmsh://yourstreamurl

```

### El Micrófono funciona a través de los altavoces

OSS, por defecto, reproduce el micrófono a través de los altavoces. Para deshabilitar esta función busque en `ossxmix` la sección *Misc*. Marque cada `input-mix-mute` para desactivarla.

## Véase también

*   [Web oficial](http://www.opensound.com/)
*   [Wiki de OSS](http://www.opensound.com/wiki)
*   [Foro de OSS](http://www.opensound.com/forum/index.php)
*   [Información sobre desarrollo](http://www.opensound.com/developer/index.html)
*   [Repositorio Git](http://sourceforge.net/p/opensound/git/)
*   [Lista de correo de opensound-devel](http://sourceforge.net/p/opensound/mailman/opensound-devel/)