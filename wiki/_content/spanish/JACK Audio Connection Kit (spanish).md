Related articles

*   [Sound system](/index.php/Sound_system "Sound system")
*   [Professional audio](/index.php/Professional_audio "Professional audio")

De [JACK Audio Connection Kit](https://en.wikipedia.org/wiki/JACK_Audio_Connection_Kit "wikipedia:JACK Audio Connection Kit"):

	JACK Audio Connection Kit (o JACK; un acrónimo recursivo) es un demonio de servidores de sonido profesional que proporciona conexiones de baja latencia en tiempo real para audio y datos MIDI entre aplicaciones que implementan su API.

## Contents

*   [1 Instalacción](#Instalacci.C3.B3n)
    *   [1.1 JACK2](#JACK2)
        *   [1.1.1 JACK2 D-Bus](#JACK2_D-Bus)
    *   [1.2 JACK](#JACK)
    *   [1.3 GUI](#GUI)
*   [2 Configuración básica](#Configuraci.C3.B3n_b.C3.A1sica)
    *   [2.1 Descripción general](#Descripci.C3.B3n_general)
    *   [2.2 Una configuración de ejemplo basada en shell](#Una_configuraci.C3.B3n_de_ejemplo_basada_en_shell)
        *   [2.2.1 Detalles de la configuración de ejemplo basada en shell](#Detalles_de_la_configuraci.C3.B3n_de_ejemplo_basada_en_shell)
    *   [2.3 Una configuración de ejemplo basada en GUI](#Una_configuraci.C3.B3n_de_ejemplo_basada_en_GUI)
    *   [2.4 Jugando bien con ALSA](#Jugando_bien_con_ALSA)
    *   [2.5 GStreamer](#GStreamer)
    *   [2.6 PulseAudio](#PulseAudio)
    *   [2.7 Firewire](#Firewire)
*   [3 MIDI](#MIDI)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 Mensaje de "No se puede bloquear el área de memoria (No se puede asignar memoria)" en el inicio](#Mensaje_de_.22No_se_puede_bloquear_el_.C3.A1rea_de_memoria_.28No_se_puede_asignar_memoria.29.22_en_el_inicio)
    *   [4.2 Jack2-dbus y qjackctl errores](#Jack2-dbus_y_qjackctl_errores)
    *   [4.3 Error "ALSA: no se puede establecer el número de canales en 1 para la captura" en los registros](#Error_.22ALSA:_no_se_puede_establecer_el_n.C3.BAmero_de_canales_en_1_para_la_captura.22_en_los_registros)
    *   [4.4 Crackling y chasquidos en audio](#Crackling_y_chasquidos_en_audio)
    *   [4.5 Problemas con aplicaciones específicas.](#Problemas_con_aplicaciones_espec.C3.ADficas.)
        *   [4.5.1 VLC - no hay audio después de iniciar JACK](#VLC_-_no_hay_audio_despu.C3.A9s_de_iniciar_JACK)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalacción

Para que JACK funcione correctamente, su usuario debe ser [agregado](/index.php/Users_and_groups#Group_management "Users and groups") al grupo `realtime` para acceder a *ulimits* más altos definidos en `/etc/security/limits.d/99-realtime-privileges.conf` (proporcionado por el paquete [realtime-privileges](https://www.archlinux.org/packages/?name=realtime-privileges) package), que es necesario para el procesamiento de audio en tiempo real.

**Note:** Debe agregar manualmente su usuario al grupo `realtime` incluso si está usando logind, ya que logind solo maneja el acceso al hardware directo.

Hay dos implementaciones de JACK, consulte [esta comparación](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2) para ver la diferencia entre las dos. En resumen, Jack 1 y Jack 2 son implementaciones equivalentes del mismo protocolo. Los programas compilados contra Jack 1 funcionarán con Jack 2 sin recompilar (y viceversa).

### JACK2

**JACK2** Es una implementación de C++ con soporte SMP. [instálalo](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [jack2](https://www.archlinux.org/packages/?name=jack2) Si está en una instalación de 64 bits y necesita ejecutar aplicaciones de 32 bits que requieren JACK, también instale el paquete [lib32-jack2](https://www.archlinux.org/packages/?name=lib32-jack2) desde el repositorio [multilib](/index.php/Official_repositories_(Espa%C3%B1ol)#multilib "Official repositories (Español)").

#### JACK2 D-Bus

JACK2 con [D-Bus](/index.php/D-Bus "D-Bus") se puede instalar a través de [jack2-dbus](https://www.archlinux.org/packages/?name=jack2-dbus). Es igual que el paquete [jack2](https://www.archlinux.org/packages/?name=jack2) pero no proporciona el servidor "jackd" heredado.

Está controlado por la utilidad `jack_control`. La utilidad jack_control requiere que también instales el paquete [python2-dbus](https://www.archlinux.org/packages/?name=python2-dbus).

```
Los comandos importantes se enumeran a continuación:
jack_control start  -  inicia el servidor jack
jack_control stop  - detiene el servidor jack
jack_control ds alsa  -  Selecciona alsa como el conductor (backend)
jack_control eps realtime True  -  establecer los parámetros del motor, como en tiempo real
jack_control dps period 256  -  establecer el período de parámetros del controlador a 256

```

### JACK

utiliza una API de C y admite más de una tarjeta de sonido en Linux (más MIDI). [instálalo](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [jack](https://www.archlinux.org/packages/?name=jack). Si está en una instalación de 64 bits y necesita ejecutar aplicaciones de 32 bits que requieren JACK, también instale el paquete [lib32-jack](https://www.archlinux.org/packages/?name=lib32-jack) desde el repositorio [multilib](/index.php/Official_repositories_(Espa%C3%B1ol)#multilib "Official repositories (Español)").

### GUI

*   **Cadence** — Conjunto de herramientas útiles para la producción de audio. Realiza comprobaciones del sistema, administra JACK, llama a otras herramientas y realiza ajustes en el sistema.

	[https://kxstudio.linuxaudio.org/Applications:Cadence](https://kxstudio.linuxaudio.org/Applications:Cadence) || [cadence](https://www.archlinux.org/packages/?name=cadence)

*   **Patchage** — Bahía de parches modulares para sistemas de audio y MIDI basados en JACK y ALSA.

	[https://drobilla.net/software/patchage](https://drobilla.net/software/patchage) || [patchage](https://www.archlinux.org/packages/?name=patchage)

*   **PatchMatrix** — Parche de JACK en estilo de matriz de flujo.

	[https://git.open-music-kontrollers.ch/lad/patchmatrix/about/](https://git.open-music-kontrollers.ch/lad/patchmatrix/about/) || [patchmatrix](https://www.archlinux.org/packages/?name=patchmatrix)

*   **[QjackCtl](https://en.wikipedia.org/wiki/Qjackctl "wikipedia:Qjackctl")** — Aplicación Qt simple para controlar el demonio del servidor de sonido JACK.

	[https://qjackctl.sourceforge.io/](https://qjackctl.sourceforge.io/) || [qjackctl](https://www.archlinux.org/packages/?name=qjackctl)

## Configuración básica

### Descripción general

La configuración correcta para sus necesidades de hardware y aplicaciones depende de varios factores. Su tarjeta de sonido y la CPU afectarán en gran medida la baja latencia que puede alcanzar al usar JACK.

La línea principal del kernel de Linux ahora admite la programación en tiempo real, por lo que ya no es necesario usar un kernel parcheado. Sin embargo, [linux-rt](https://aur.archlinux.org/packages/linux-rt/) en el AUR es un kernel parcheado que tiene algunos parches adicionales que pueden ayudar a obtener latencias más bajas.

### Una configuración de ejemplo basada en shell

La edición D-Bus de JACK2 puede hacer que el arranque sea mucho más fácil. Anteriormente, se usaba QjackCtl para iniciarlo, o se usaba un demonio o algún otro método. Pero utilizando [jack2-dbus](https://www.archlinux.org/packages/?name=jack2-dbus), JACK2 se puede iniciar y configurar fácilmente a través de un script de shell.

Cree un script de shell que se pueda ejecutar al iniciar sesión en X:

 `start_jack.sh` 
```
#!/bin/bash

jack_control start
jack_control ds alsa
jack_control dps device hw:HD2
jack_control dps rate 48000
jack_control dps nperiods 2
jack_control dps period 64
sleep 10
a2jmidid -e &
sleep 10
qjackctl &

```

Lo anterior iniciará una instancia de JACK de trabajo que otros programas pueden utilizar. Los detalles de cada línea siguen. Cuando descubra su propia mejor configuración, es útil hacer pruebas y errores utilizando la GUI de QjackCtl con una versión de D-Bus JACK2.

#### Detalles de la configuración de ejemplo basada en shell

```
jack_control start

```

Inicia JACK si aún no está iniciado.

```
jack_control ds alsa

```

Establece JACK para usar el conjunto de controladores ALSA.

```
jack_control dps device hw:HD2

```

Configura a JACK para usar una tarjeta de sonido compatible con ALSA llamada HD2\. Uno puede encontrar los nombres con `cat /proc/asound/cards`. La mayoría de los tutoriales y configuraciones predeterminadas de ALSA utilizan números de tarjeta, pero esto puede resultar confuso cuando se utilizan dispositivos MIDI externos; Los nombres lo hacen más fácil.

```
jack_control dps rate 48000

```

Establece JACK para utilizar muestreo de 48000 khz. Sucede que funciona muy bien con esta tarjeta. Algunas tarjetas sólo se hacen 44100, muchos van a subir mucho más. Cuanto más alto vaya, más baja será su latencia, pero mejor deberán ser su tarjeta y su CPU, y el software también tiene que admitir esto.

```
jack_control dps nperiods 2

```

Establece JACK para usar 2 periodos. 2 es adecuado para la placa base, PCI, PCI-X, etc .; 3 para USB.

```
jack_control dps period 64

```

Establece JACK para usar 64 periodos por cuadro. Inferior es menos latencia, pero la configuración en este script proporciona 2.67 ms de latencia, que es bastante baja sin poner demasiado énfasis en el hardware en particular para el que se creó este ejemplo. Si un sistema de sonido USB estuviera en uso, podría ser bueno probar 32\. Cualquier cosa menor a 3-4 ms debería estar bien para síntesis en tiempo real y/o efectos, 5 ms es lo más pequeño que un ser humano puede detectar. QjackCtl te dirá cómo estás; sin carga, lo que significa que no hay clientes conectados, deseará un máximo de 3-5% de uso de CPU, y si no puede obtener eso sin xruns (los números rojos que significan que el sistema no puede cumplir con las demandas), Tienes que mejorar tu hardware.

```
sleep 10

```

Espera a que lo anterior se asiente.

```
a2jmidid -e &

```

Inicie el puente MIDI de ALSA a JACK. Bueno para mezclar en aplicaciones que toman entrada MIDI a través de ALSA pero no JACK.

```
sleep 10

```

Espera a que lo anterior se asiente.

```
qjackctl &

```

Cargar QjackCtl. La configuración de la GUI le dice que se ejecute en la bandeja del sistema. Recogerá la sesión JACK iniciada por D-Bus muy bien, y muy bien también. Mantiene el patchbay, las conexiones entre estas aplicaciones y cualquier otra aplicación habilitada para JACK para iniciarse manualmente. El patchbay se configura mediante la GUI manual, pero las conexiones preconfiguradas en el patchbay son creadas automáticamente por QjackCtl cuando se inician las aplicaciones.

### Una configuración de ejemplo basada en GUI

Esta configuración de ejemplo utiliza una configuración y administración más centrada en la GUI de JACK

*   Instale [jack2-dbus](https://www.archlinux.org/packages/?name=jack2-dbus).
*   Instale [qjackctl](https://www.archlinux.org/packages/?name=qjackctl), e informe a su sistema de escritorio/ventana GUI para que se ejecute al inicio.
*   Asegúrese de que se diga a QjackCtl que:
    *   usar la interfaz D-Bus,
    *   ejecutar en el arranque,
    *   guardar su configuración en la ubicación predeterminada,
    *   iniciar el servidor de audio JACK en el inicio de la aplicación,
    *   habilitar el icono de la bandeja del sistema, y
    *   inicio minimizado a la bandeja del sistema.
*   Reiniciar.
*   Después de iniciar sesión, verá QjackCtl en la bandeja del sistema. Haz clic izquierdo en él.
*   Ajustar la configuración en la interfaz gráfica de QjackCtl para reducir la latencia. La configuración de Tamaño de marco, Búfer de marco y Velocidad de bits afectan la latencia. Los tamaños de fotogramas más grandes reducen la latencia, los fotogramas inferiores reducen la latencia y los valores de bitrate más altos reducen la latencia, pero todos aumentan la carga en la tarjeta de sonido y en la CPU. Una latencia de aproximadamente ~ 5 ms es deseable para el monitoreo directo de instrumentos o micrófonos, ya que la latencia comienza a ser perceptible en latencias más altas.

### Jugando bien con ALSA

Para permitir que los programas Alsa se reproduzcan mientras se está ejecutando el conector, debe instalar el complemento del conector para alsa con [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

Y habilítelo editando (o creando) /etc/asound.conf (configuración de todo el sistema) para tener estas líneas:

```
# convertir alsa API sobre jack API
# usarlo con
#% aplay foo.wav

# usa esto como predeterminado
pcm.!default {
    type plug
    slave { pcm "jack" }
}

ctl.mixer0 {
    type hw
    card 1
}

# pcm tipo jack
pcm.jack {
    type jack
    playback_ports {
        0 system:playback_1
        1 system:playback_2
    }
    capture_ports {
        0 system:capture_1
        1 system:capture_2
    }
}
```

No necesitas reiniciar tu computadora ni nada. Solo edita los archivos de configuración alsa, inicia el jack, y listo...

Recuerde iniciarlo como **usuario**. Si lo inicia con `jackd` -d alsa como usuario X, no funcionará para el usuario Y. Otro enfoque, utilizando el dispositivo de bucle de retorno ALSA (más complejo pero probablemente más robusto), se describe en [este artículo](http://alsa.opensrc.org/Jack_and_Loopback_device_as_Alsa-to-Jack_bridge).

### GStreamer

GStreamer requiere que el paquete [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) funcione con JACK, que contiene el complemento jackaudiosink que agrega compatibilidad con la reproducción de JACK.

Más información (desactualizada): [http://jackaudio.org/faq/gstreamer_via_jack.html](http://jackaudio.org/faq/gstreamer_via_jack.html)

### PulseAudio

Si necesita mantener [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) instalado (en caso de que lo requieran otros paquetes, como [gnome-settings-daemon](https://www.archlinux.org/packages/?name=gnome-settings-daemon)), es posible que desee evitar que se genere automáticamente con X y tomando el relevo de JACK.

Edite `/etc/pulse/client.conf`, elimine el comentario "autospawn" y configúrelo en "no":

```
;autospawn = yes
autospawn = no

```

*Si desea que ambos se reproduzcan, consulte: [PulseAudio/Examples#PulseAudio a través de JACK](/index.php/PulseAudio/Examples#PulseAudio_a_trav.C3.A9s_de_JACK "PulseAudio/Examples")*

### Firewire

Para evitar que ALSA pierda el tiempo con sus dispositivos firewire, debe incluir en la lista negra todos los módulos de kernel relacionados con firewire. Esto también evita que PulseAudio use Firewire. Crea el siguiente archivo:

 `/etc/modprobe.d/alsa-no-jack.conf` 
```
blacklist snd-fireworks
blacklist snd-bebob
blacklist snd-oxfw
blacklist snd-dice
blacklist snd-firewire-digi00x
blacklist snd-firewire-tascam
blacklist snd-firewire-lib
blacklist snd-firewire-transceiver
blacklist snd-fireface
blacklist snd-firewire-motu

```

*La lista de módulos es la más reciente disponible en el momento de escribir en [Alsa Firewire mejorar repositorio](https://github.com/takaswie/snd-firewire-mejorar).*

Ahora puede descargar sus módulos Firewire cargados o reiniciar.

## MIDI

JACK puede manejar una tarjeta de sonido muy bien y un número arbitrario de dispositivos MIDI (conectados, por ejemplo, a través de USB). Si inicia JACK y desea usar un teclado MIDI o un sintetizador o algún otro dispositivo MIDI puro, debe iniciar JACK con una tarjeta de sonido adecuada (una que realmente emita o ingrese sonido PCM). Tan pronto como lo hayas hecho, puedes conectar el dispositivo MIDI. P.ej. con QjackCtl ([qjackctl](https://www.archlinux.org/packages/?name=qjackctl)), haga clic en el botón de conexión y encontrará su dispositivo en la lista de JACK-MIDI o ALSA-MIDI, dependiendo del controlador. Para JACK-MIDI, puede configurar el **Controlador MIDI** en **seq** o **raw** en Configuración> Configuración de QjackCtl *. Esto debería hacer que su dispositivo MIDI aparezca en la pestaña* MIDI *. También puede cambiar el nombre del cliente (de un genérico "midi_capture_1" a algo más descriptivo), si habilita "Configuración> Pantalla> Habilitar alias de puerto/cliente" y luego "Permitir la edición de alias de cliente/puerto (renombrar)* .

Para ALSA-MIDI, asegúrese de activar *'Habilitar el soporte del secuenciador ALSA'* en QjackCtl *Configuración> Miscelánea* . Esto agregará la pestaña *ALSA* en la ventana *Conectar* de QjackCtl donde se mostrará su controlador MIDI.

**Nota:** [jack2](https://www.archlinux.org/packages/?name=jack2) no viene con soporte de puente para aplicaciones heredadas de ALSA MIDI solamente. Por lo tanto, se requiere [a2jmidid](https://www.archlinux.org/packages/?name=a2jmidid) [hasta que el flujo ascendente alcance paridad de características en esto](https://github.com/jackaudio/jack2/issues/362).

Para conectar ALSA-MIDI a JACK-MIDI, puede considerar el uso de a2jmidid ([a2jmidid](https://www.archlinux.org/packages/?name=a2jmidid)). El siguiente comando exportará todos los puertos ALSA MIDI disponibles a los puertos JACK MIDI:

```
$ a2jmidid -e

```

Serán visibles en QjackCtl en la pestaña *MIDI* etiquetada como cliente "a2j". Puede automatizar el inicio de a2jmidid agregando a QjackCtl *Configuración> Opciones> Ejecutar secuencia de comandos después del inicio* : `/usr/bin/a2jmidid -e &`

**Nota:** Al conectar controladores de teclado MIDI en QjackCtl, asegúrese de *Expandir todo* primero y conecte los *Puertos de salida* deseados (debajo de *Clientes legibles* ) a los *Puertos de entrada* (debajo de los *clientes escribibles* ). Como acceso directo, si selecciona un cliente de escritura en lugar de puertos individuales como su destino, debería conectar todos los puertos de salida que se muestran actualmente debajo.

*   **Q:** ¿Cuál es la diferencia entre JACK-MIDI y ALSA-MIDI?
*   **A:** El primero ha mejorado la sincronización y muestra la alineación precisa de eventos MIDI. Extiende o incluso puede reemplazar a este último, pero en este punto ambos coexisten.

Para instalar algunos teclados MIDI M-Audio, necesitará el paquete de firmware [midisport-firmware](https://aur.archlinux.org/packages/midisport-firmware/) en [AUR](/index.php/AUR "AUR"). Además, el módulo snd_usb_audio debe estar disponible. Para obtener más información sobre dispositivos USB MIDI específicos, consulte [http://alsa.opensrc.org/USBMidiDevices](http://alsa.opensrc.org/USBMidiDevices).

## Solución de problemas

### Mensaje de "No se puede bloquear el área de memoria (No se puede asignar memoria)" en el inicio

Consulte [Realtime process management#Configuring PAM](/index.php/Realtime_process_management#Configuring_PAM "Realtime process management") y asegurarse de que el usuario está en el [grupo](/index.php/Grupo "Grupo") `realtime`.

### Jack2-dbus y qjackctl errores

¿Aún tiene el error "No se puede asignar memoria" y/o "No se puede conectar con el socket del servidor = No hay tal archivo o directorio" al presionar el botón de inicio de qjackctl (suponiendo que tiene el paquete jack2-dbus instalado)?

Borre `~/.jackdrc`, `~/.config/jack/conf.xml`, `~/.config/rncbc.org/QjackCtl.conf`. Mate *jackdbus* y reiniciar desde cero :) (Gracias a nedko)

Tambien intenta correr

```
$ fuser /dev/snd/*

```

y verifique los PID resultantes con

```
$ ps ax | grep [PID here]

```

Esperemos que esto muestre los programas conflictivos.

### Error "ALSA: no se puede establecer el número de canales en 1 para la captura" en los registros

Cambie los canales de entrada y salida de ALSA de 1 a 2.

### Crackling y chasquidos en audio

Su CPU o tarjeta de sonido es demasiado débil para manejar su configuración para JACK. Baje la tasa de bits, baje el tamaño del cuadro y aumente el período del cuadro en pequeños incrementos hasta que cese el crujido.

### Problemas con aplicaciones específicas.

#### VLC - no hay audio después de iniciar JACK

Ejecuta VLC y cambia las siguientes opciones de menú:

*   Herramientas> Preferencias
*   Mostrar ajustes: Todos
*   Audio> Módulos de salida> Módulo de salida de audio: salida de audio JACK
*   Audio> Módulos de salida> JACK: conectarse automáticamente a clientes grabables (habilitar)

## Véase también

*   [Diferencias entre JACK 1 y JACK2](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2)
*   [Preguntas frecuentes de JACK](http://jackaudio.org/faq/)