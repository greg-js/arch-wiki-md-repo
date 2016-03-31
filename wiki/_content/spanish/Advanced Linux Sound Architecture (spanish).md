La [Arquitectura Avanzada para el Sonido en Linux](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture") (conocido con el acrónimo **ALSA**) es un componente del kernel destinado a sustituir el original Open Sound System (Open OSSv3) para proporcionar controladores de dispositivos para las tarjetas de sonido. Además de los controladores de dispositivos de sonido, **ALSA** también pone a disposición una amplia biblioteca en el espacio de usuario para los desarrolladores de aplicaciones que quieran utilizar las funciones del controlador mediante un API de alto nivel con una interacción directa con los controladores del kernel.

**Nota:** Para un entorno de sonido alternativo, consulte la página [Open Sound System](/index.php/Open_Sound_System_(Espa%C3%B1ol) "Open Sound System (Español)")
.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Utilidades en el espacio de usuario](#Utilidades_en_el_espacio_de_usuario)
*   [2 Abrir los canales de audio](#Abrir_los_canales_de_audio)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Sin sonido en virtualbox](#Sin_sonido_en_virtualbox)
    *   [3.2 Establecer la tarjeta de sonido predeterminada](#Establecer_la_tarjeta_de_sonido_predeterminada)
        *   [3.2.1 Seleccionar el PCM por defecto a través de la variable de entorno](#Seleccionar_el_PCM_por_defecto_a_trav.C3.A9s_de_la_variable_de_entorno)
        *   [3.2.2 Método alternativo](#M.C3.A9todo_alternativo)
    *   [3.3 Asegurarse de que los módulos de sonido se cargan](#Asegurarse_de_que_los_m.C3.B3dulos_de_sonido_se_cargan)
    *   [3.4 Conseguir salida SPDIF](#Conseguir_salida_SPDIF)
    *   [3.5 Ecualizador System-Wide](#Ecualizador_System-Wide)
        *   [3.5.1 Usar AlsaEqual (proporciona la interfaz gráfica)](#Usar_AlsaEqual_.28proporciona_la_interfaz_gr.C3.A1fica.29)
            *   [3.5.1.1 Administrar los estados de AlsaEqual](#Administrar_los_estados_de_AlsaEqual)
        *   [3.5.2 Usar mbeq](#Usar_mbeq)
*   [4 Remuestreo de alta calidad](#Remuestreo_de_alta_calidad)
*   [5 Upmixing/Downmixing](#Upmixing.2FDownmixing)
    *   [5.1 Upmixing](#Upmixing)
    *   [5.2 Downmixing](#Downmixing)
*   [6 Mezclar](#Mezclar)
    *   [6.1 Mezclar con software (dmix)](#Mezclar_con_software_.28dmix.29)
    *   [6.2 Mezclar con Hardware](#Mezclar_con_Hardware)
        *   [6.2.1 Soporte](#Soporte)
        *   [6.2.2 Arreglos](#Arreglos)
*   [7 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [7.1 Sonido con saltos durante el uso de Dynamic Frequency Scaling](#Sonido_con_saltos_durante_el_uso_de_Dynamic_Frequency_Scaling)
    *   [7.2 Problemas con la disponibilidad del software de mezcla por solo un usuario a la vez](#Problemas_con_la_disponibilidad_del_software_de_mezcla_por_solo_un_usuario_a_la_vez)
    *   [7.3 Problemas de reproducción simultánea](#Problemas_de_reproducci.C3.B3n_simult.C3.A1nea)
    *   [7.4 Ausencia de sonido al azar en el inicio](#Ausencia_de_sonido_al_azar_en_el_inicio)
        *   [7.4.1 Timidity](#Timidity)
    *   [7.5 Problemas específicos de algunos programas](#Problemas_espec.C3.ADficos_de_algunos_programas)
    *   [7.6 Configurar los modelos](#Configurar_los_modelos)
    *   [7.7 Audio en conflicto con altavoz interno del PC](#Audio_en_conflicto_con_altavoz_interno_del_PC)
    *   [7.8 Sin entrada en el micrófono](#Sin_entrada_en_el_micr.C3.B3fono)
    *   [7.9 Configuración predeterminada de Micrófono/Dispositivo de captura](#Configuraci.C3.B3n_predeterminada_de_Micr.C3.B3fono.2FDispositivo_de_captura)
    *   [7.10 El micrófono interno no funciona](#El_micr.C3.B3fono_interno_no_funciona)
    *   [7.11 Sin sonido con tarjeta de sonido Intel integrada](#Sin_sonido_con_tarjeta_de_sonido_Intel_integrada)
    *   [7.12 Sin sonido en auriculares con tarjeta de sonido Intel integrada](#Sin_sonido_en_auriculares_con_tarjeta_de_sonido_Intel_integrada)
    *   [7.13 Sin sonido cuando se instala la tarjeta de vídeo con S/PDIF](#Sin_sonido_cuando_se_instala_la_tarjeta_de_v.C3.ADdeo_con_S.2FPDIF)
    *   [7.14 Calidad de audio deficiente](#Calidad_de_audio_deficiente)
    *   [7.15 Crepiteos al iniciar y detener la reproducción](#Crepiteos_al_iniciar_y_detener_la_reproducci.C3.B3n)
    *   [7.16 La salida S/PDIF no funciona](#La_salida_S.2FPDIF_no_funciona)
    *   [7.17 La salida HDMI no funciona](#La_salida_HDMI_no_funciona)
    *   [7.18 La salida multicanal PCM de HDMI no funciona (Intel)](#La_salida_multicanal_PCM_de_HDMI_no_funciona_.28Intel.29)
    *   [7.19 HP TX2500](#HP_TX2500)
    *   [7.20 Salto de sonido durante la reproducción MP3](#Salto_de_sonido_durante_la_reproducci.C3.B3n_MP3)
    *   [7.21 Auriculares USB y tarjetas de sonido externas USB](#Auriculares_USB_y_tarjetas_de_sonido_externas_USB)
        *   [7.21.1 Sonido crepitante con dispositivos USB](#Sonido_crepitante_con_dispositivos_USB)
        *   [7.21.2 Conexión hot-plugging de una tarjeta de sonido USB](#Conexi.C3.B3n_hot-plugging_de_una_tarjeta_de_sonido_USB)
    *   [7.22 Error 'Unkown hardware' después de una actualización del Kernel](#Error_.27Unkown_hardware.27_despu.C3.A9s_de_una_actualizaci.C3.B3n_del_Kernel)
    *   [7.23 HDA Analyzer](#HDA_Analyzer)
    *   [7.24 ALSA con SDL](#ALSA_con_SDL)
    *   [7.25 Alternativa al sonido bajo](#Alternativa_al_sonido_bajo)
    *   [7.26 Sonido abrupto después de reanudar la suspensión](#Sonido_abrupto_despu.C3.A9s_de_reanudar_la_suspensi.C3.B3n)
    *   [7.27 Silencio después de reiniciar](#Silencio_despu.C3.A9s_de_reiniciar)
*   [8 Configuraciones de ejemplo](#Configuraciones_de_ejemplo)
*   [9 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

ALSA está incluido en el kernel de Arch por defecto como un conjunto de módulos, por lo que no es necesaria su instalación explícitamente.

[udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") explorará automáticamente el hardware en el arranque, cargando el módulo del kernel correcto para la tarjeta de sonido encontrada. Por lo tanto, el sonido debería estar funcionando desde el inicio, pero, ha de tener en cuenta que su configuración viene, por defecto, con todos los canales de audio silenciados.

Los usuarios con un inicio de sesión local (en una terminal virtual o un gestor de pantalla) tienen habilitados los permisos para reproducir sonido y cambiar los niveles del mezclador. Para permitir esto en un inicio de sesión remoto, el usuario tiene que ser [añadido](/index.php/Users_and_groups#Group_management "Users and groups") al grupo de `audio`. La calidad de miembro del grupo de `audio` también permite el acceso directo a los dispositivos, lo que puede conducir a que se graben exclusivamente las salidas de las aplicaciones (rompiendo el software de mezcla) y frustrar el rápido intercambio entre usuarios, y multisede. Por lo tanto, la adición de un usuario al grupo de `audio` **no** es recomendable, a menos que se necesite específicamente [[1]](https://wiki.ubuntu.com/Audio/TheAudioGroup).

### Utilidades en el espacio de usuario

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories") que contienen la herrameinta `alsamixer` para el espacio de usuario, que permite la configuración de los dispositivos de sonido desde la consola o terminal. Instale también el paquete [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) si desea [remuestreo en alta calidad](#Remuestreo_de_alta_calidad), [upmixing/downmixing](#Upmixing.2FDownmixing) y otras características avanzadas.

Si desea que las aplicaciones de OSS funcionen mediante dmix (software de mezcla), instale también el paquete [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss). Cargue los [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") `snd_seq_oss`, `snd_pcm_oss` y `snd_mixer_oss` para activar los módulos de emulación de OSS.

## Abrir los canales de audio

La versión actual de ALSA se instala con todos los canales **silenciados por defecto**. Será necesario revertir manualmente el **enmudecimiento** de los canales.

Lo más cómodo es utilizar la interfaz gráfica `alsamixer` para hacer esto:

```
$ alsamixer

```

Como alternativa, puede usar `amixer` desde la línea de comandos:

```
$ amixer sset Master unmute

```

La etiqueta `MM`, por debajo de un canal, indica que el canal está silenciado, y `00` indica que está abierto.

El procedimiento a seguir es el siguiente:

Desplácese hasta los canales `Master` y `PCM` con las teclas `←` y `→`, y retire el silencio pulsando la tecla `m`. Utilice la tecla `↑` para aumentar el volumen y obtener un «dB gain» con valor `0`. El valor «gain» se puede encontrar en la parte superior izquierda junto al campo `Item:`. Los valores más altos de «gain» producirán sonido distorsionado.

Para obtener un verdadero sonido envolvente (surround) 5.1 o 7.1 es probable que tenga que activar otros canales como Front, Surround, Center, LFE (subwoofer) y Side (estos son los nombres de los canales para el módulo Intel HD Audio, y pueden variar según el hardware). Tenga en cuenta que esto no se logrará automáticamente con Upmix para las fuentes de sonido estéreo (como, por ejemplo, la música). Con el fin de lograrlo, consulte [Upmixing/Downmixing](#Upmixing.2FDownmixing).

Salga de alsamixer pulsando `Esc`.

**Nota:**

*   Algunas tarjetas necesitan tener el canal de salida digital silenciado/apagado para poder escuchar el sonido analógico. Para la LS Soundblaster Audigy es necesario silenciar el canal IEC958.
*   Algunas máquinas, (como la Thinkpad T61), tienen un canal speaker (altavoz) que debe ser activado y ajustado también.
*   Algunas máquinas (como Dell E6400) también pueden requerir que el silencio sea desactivado en los canales `Front` y `Headphone` y ajustados

Se puede ahora comprobar si el sonido funciona:

```
$ speaker-test -c 2

```

Modifique el valor -c para ajustar la configuración de los altavoces. Por ejemplo, use -c 8 para 7.1:

```
$ speaker-test -c 8

```

Si esto no funciona, vaya a [configuración](#Configuraci.C3.B3n) o consulte la sección sobre [solución de problemas](#Soluci.C3.B3n_de_problemas).

El paquete [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) incluye `alsa-restore.service` y `alsa-store.service`, que están preconfigurados para hacer funcionar el arranque y la parada, respectivamente.

## Configuración

### Sin sonido en virtualbox

Si tiene problemas con virtualbox, el siguiente comando puede ser de ayuda:

 `$ alsactl init` 
```

Found hardware: "ICH" "SigmaTel STAC9700,83,84" "AC97a:83847600" "0x8086" "0x0000"
Hardware is initialized using a generic method

```

Puede que tenga que activar la salida de ALSA en su software de audio también.

### Establecer la tarjeta de sonido predeterminada

Si sus tarjetas de sonido cambian de orden durante el arranque, puede especificar el orden de las mismas en el archivo `/etc/modprobe.d/modprobe.conf` (se sugiere el archivo `/etc/modprobe.d/alsa-base.conf`). Por ejemplo, si desea que el tarjeta de sonido «mia» se cargue primero, colóquele el valor #0:

 `/etc/modprobe.d/alsa-base.conf` 
```
options snd slots=snd_mia,snd_hda_intel
options snd_mia index=0
options snd_hda_intel index=1

```

Utilice `$ lsmod | grep snd` para obtener una lista de dispositivos. Esta configuración asume que tiene una tarjeta de sonido «mia» usando `snd_mia`, y una tarjeta «snd-hda-intel» (es decir, integrada) usando `snd_hda_intel`.

También puede proporcionar un índice de `-2` para indicarle a ALSA que nunca use una tarjeta como la primera. Distribuciones como Linux Mint y Ubuntu utilizan la siguiente configuración para evitar que USB y de otros tipos de controladores «extraños» obtengan el índice `0`:

 `/etc/modprobe.d/alsa-base.conf` 
```
options bt87x index=-2
options cx88_alsa index=-2
options saa7134-alsa index=-2
options snd-atiixp-modem index=-2
options snd-intel8x0m index=-2
options snd-via82xx-modem index=-2
options snd-usb-audio index=-2
options snd-usb-caiaq index=-2
options snd-usb-ua101 index=-2
options snd-usb-us122l index=-2
options snd-usb-usx2y index=-2
# Keep snd-pcsp from being loaded as first soundcard
options snd-pcsp index=-2
# Keep snd-usb-audio from beeing loaded as first soundcard
options snd-usb-audio index=-2

```

Estos cambios requieren un reinicio del sistema, para que surtan efectos.

#### Seleccionar el PCM por defecto a través de la variable de entorno

En el archivo de configuración, preferentemente el global, agregue:

```
 pcm.!default {
   type plug
   slave.pcm {
     @func getenv
     vars [ ALSAPCM ]
     default "hw:Audigy2"
   }
 }

```

Es necesario sustituir la línea «default» con el nombre de la tarjeta (en el ejemplo es `Audigy2`). Se pueden obtener los nombres con `aplay -l` o también puede utilizar los PCM como **surround51**. Pero si se necesita utilizar el micrófono es una buena idea seleccionar PCM full-duplex por defecto.

Ahora se pueden comenzar los programas seleccionando la tarjeta de sonido con solo cambiar la variable de entorno `ALSAPCM`. Funciona muy bien para todos los programas que no permiten seleccionar la tarjeta, para los demás asegúrese de que mantener la tarjeta predeterminada. Por ejemplo, asumiendo que escribió un PCM downmix llamado **mix51to20** se puede utilizar el mismo con `mplayer` usando la línea de órdenes `ALSAPCM=mix51to20 mplayer example_6_channel.wav`

#### Método alternativo

En primer lugar, tendrá que averiguar la identificación de la tarjeta y del dispositivo que desea establecer como predeterminados, ejecutando `aplay -l`:

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: CONEXANT Analog [CONEXANT Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: Conexant Digital [Conexant Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: JamLab [JamLab], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Audio [Altec Lansing XT1 - USB Audio], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

Por ejemplo, la última entrada de esta lista tiene el ID de la tarjeta 2 y el ID de dispositivo 0\. Para establecer esta tarjeta como la predeterminada, puede utilizar el archivo que afecta a todo el sistema `/etc/asound.conf` o el archivo específico del usuario `~/.asoundrc`. Puede que tenga que crear el archivo si no existe. A continuación, inserte las siguientes opciones con el id correspondiente del dispositivo y de la tarjeta.

```
pcm.!default {
	type hw
	card 2
}

ctl.!default {
	type hw           
	card 2
}

```

Las opciones 'pcm' afectan a la tarjeta y al dispositivo que se pueden utilizar para la reproducción de audio, mientras que la opción 'ctl' afecta a la tarjeta que es utilizada por la utilidades de control como alsamixer.

Los cambios entrarán en vigor tan pronto se (re)inicie una aplicación (mplayer, etc.). También puede probar con una orden como aplay:

```
aplay -D default <your_favourite_sound.wav>

```

Si recibe un error acerca de la configuración de asound, compruebe [upstream documentation](http://www.alsa-project.org/main/index.php/Asoundrc#The_default_plugin) para conocer posibles cambios en el formato del archivo de configuración.

### Asegurarse de que los módulos de sonido se cargan

Es de suponer que udev detectará automáticamente el sonido correctamente. Puede verificar que esto ha ocurrido así con la orden siguiente:

 `$ lsmod | grep '^snd' | column -t` 
```
snd_hda_codec_hdmi     22378   4
snd_hda_codec_realtek  294191  1
snd_hda_intel          21738   1
snd_hda_codec          73739   3  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel
snd_hwdep              6134    1  snd_hda_codec
snd_pcm                71032   3  snd_hda_codec_hdmi,snd_hda_intel,snd_hda_codec
snd_timer              18992   1  snd_pcm
snd                    55132   9  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel,snd_hda_codec,snd_hwdep,snd_pcm,snd_timer
snd_page_alloc         7017    2  snd_hda_intel,snd_pcm

```

Si el resultado es similar, los controladores de sonido han sido reconocidos automáticamente con éxito.

**Nota:** Desde `udev>=171`, los módulos de emulación de OSS (`snd_seq_oss, snd_pcm_oss, snd_mixer_oss`) no se cargan de forma predeterminada: [Cárguelos manualmente](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_m.C3.B3dulos "Kernel modules (Español)") si son necesarios.

También puede ser que desee comprobar el directorio `/dev/snd/` para verificar que los archivos de dispositivos son los correctos:

 `$ ls -l /dev/snd` 
```
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer

```

**Nota:** Si solicita ayuda en el IRC o los foros, por favor envíe la salida proporcionada por las órdenes anteriores.

Si tiene presente, por lo menos, los dispositivos **controlC0** y **pcmC0D0p** o similares, entonces los módulos de sonido han sido detectados y cargados correctamente.

Si este no es el caso, sus módulos de sonido no se han detectado correctamente. Para solucionar esto, pruebe intentando cargar los módulos manualmente:

*   Localice el módulo de la tarjeta de sonido: [ALSA Soundcard Matrix](http://www.alsa-project.org/main/index.php/Matrix:Main). El módulo contendrá el prefijo 'snd-' (por ejemplo: `snd-via82xx`).
*   [Cargue el módulo](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_m.C3.B3dulos "Kernel modules (Español)").
*   Verifique que los archivos del dispositivo en `/dev/snd` tienen una salida razonable (véase más arriba) y/o compruebelo con `alsamixer` o `amixer`.
*   Configure `snd-NAME-OF-MODULE` y `snd-pcm-oss` para [cargar al arranque](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_m.C3.B3dulos "Kernel modules (Español)").

### Conseguir salida SPDIF

(De los foros de Gentoo)

*   En el control del volumen de GNOME, en la pestaña Opciones, cambie IEC958 a PCM. Esta opción puede estar habilitada en las preferencias.
*   Si no tiene instalado el control del volumen de GNOME:
    *   Edite `/var/lib/alsa/asound.state`. En este archivo alsasound guarda la configuración de mixer.
    *   Encuentre una línea que dice: 'IEC958 Playback Switch'. Cerca de ella se encuentra una línea que dice `value:false`. Cambie el valor a `value:true`.
    *   Ahora busque esta línea: 'IEC958 Playback AC97-SPSA'. Cambie su valor a `0`.
    *   Reinicie ALSA.

Otra forma alternativa para activar la salida SPDIF automáticamente al iniciar sesión (probado en SoundBlaster Audigy):

*   Añada las siguientes líneas a `/etc/rc.local`:

```
 # Use COAX-digital output
 amixer set 'IEC958 Optical' 100 unmute
 amixer set 'Audigy Analog/Digital Output Jack' on

```

Se puede ver el nombre de la salida digital de la tarjeta con:

```
 $ amixer scontrols

```

### Ecualizador System-Wide

#### Usar AlsaEqual (proporciona la interfaz gráfica)

Instale [alsaequal](https://aur.archlinux.org/packages/alsaequal/) desde [AUR](/index.php/AUR "AUR").

**Nota:** Si tiene un sistema x86_64 y está utilizando 32bit-flashplugin, el sonido en flash no funcionará. Tendrá que, o bien desactivar alsaequal, o bien compilarlo para 32 bits.

Después de instalar el paquete, introduzca lo siguiente en el archivo de configuración de ALSA (`~/.asoundrc` o `/etc/asound.conf`):

```
ctl.equal {
 type equal;
}

pcm.plugequal {
  type equal;
  # Modifique la línea de abajo si
  # desea utilizar la tarjeta de sonido 0.
  #slave.pcm "plughw:0,0";
  #por defecto funcionará con más de una fuente simultáneamente:
  slave.pcm "plug:dmix";
}
#pcm.equal {
  # Si no desea que el ecualizador utilice la
  # tarjeta de sonido predeterminada comente la siguiente
  # línea y descomente la línea anterior. (Puede
  # elegirlo como dispositivo de salida al usar
  # otras aplicaciones específicas, por ejemplo, mpg123 -a equal 06.Back_In_Black.mp3)
pcm.!default {
  type plug;
  slave.pcm plugequal;
}

```

Y ya está listo para cambiar su ecualizador con la orden:

```
$ alsamixer -D equal

```

Tenga en cuenta que el archivo de configuración es diferente para cada usuario (mientras no se especifique otra cosa) que se guarda en `~/.alsaequal.bin`. Así que si desea utilizar AlsaEqual con [mpd](/index.php/Mpd "Mpd") u otro software que se ejecute bajo un usuario diferente, se puede configurar mediante la orden:

```
# su mpd -c 'alsamixer -D equal'

```

O, por ejemplo, se puede hacer un enlace simbólico a `.alsaequal.bin` en el directorio home de aquel usuario.

##### Administrar los estados de AlsaEqual

Instale [alsaequal-mgr](http://xyne.archlinux.ca/projects/alsaequal-mgr/) desde los [repositorios de Xyne](http://xyne.archlinux.ca/repos/) o desde [AUR](https://aur.archlinux.org/packages.php?ID=62420).

Configure el ecualizador como de costumbre con:

```
$ alsamixer -D equal

```

Cuando esté satisfecho con el estado, puede darle un nombre («foo» en este ejemplo) y guardarlo:

```
$ alsaequal-mgr save foo

```

El estado «foo», entonces se puede restaurar en un momento posterior con:

```
$ alsaequal-mgr load foo

```

De esta forma puede crear diferentes estados de ecualizador para juegos, películas, géneros musicales, aplicaciones de VoIP, etc. y volver a cargarlos cuando sea necesario.

Consulte la [página del proyecto](http://xyne.archlinux.ca/projects/alsaequal-mgr/) y los consejos de ayuda para más opciones.

#### Usar mbeq

**Nota:** Este método requiere el uso del plugin ladspa que podría suponer un consumo un poco alto de la CPU cuando se reproduce el sonido. Además, esto se hizo pensando en la utilización de sonido estereofónico (por ejemplo, optimizado para escuchar a través de auriculares).

Instale los paquetes [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins), [ladspa](https://www.archlinux.org/packages/?name=ladspa) y [swh-plugins](https://www.archlinux.org/packages/?name=swh-plugins) si aún no los tiene.

*   Si no ha creado el archivo `~/.asoundrc` o `/etc/asound.conf`, a continuación, cree cualquiera de ellos y añada lo siguiente:

 `/etc/asound.conf` 
```
pcm.eq {
  type ladspa

  # La salida del EQ puede ir directamente a un dispositivo de hardware
  # (si usted tiene un mezclador de hardware, por ejemplo SBLive/Audigy) o puede ir
  # para el mezclador de software que se muestra aquí.
  #slave.pcm "plughw:0,0"
  slave.pcm "plug:dmix"

  # A veces es posible que necesite especificar la ruta de los plugins,
  # especialmente si acaba de instalarlos. Una vez que haya iniciado sesión
  # salir/reiniciar no debería ser necesario, pero sí, si se producen errores
  # por no poder encontrar los plugins, intente eliminando el comentario de estos.
  #path "/usr/lib/ladspa"

  plugins [
    {
      label mbeq
      id 1197
      input {
        #este ajuste se puede hacer aquí, por ejemplo; edite a su gusto
        #bandas: 50Hz, 100Hz, 220Hz, 156hz, 311hz, 440hz, 622hz, 880hz, 1250hz, 1750Hz, 25000hz,
        #50000hz, 10000Hz, 20000Hz
        controls [ -5 -5 -5 -5 -5 -10 -20 -15 -10 -10 -10 -10 -10 -3 -2 ]
      }
    }
  ]
 }

 # Redirigir el dispositivo predeterminado para pasar por el EQ - es posible que desee hacer esto.
 # haga esto último, una vez que esté seguro de que todo está funcionando. De lo contrario todos
 # sus programas de audio se romperán/bloquearán si algo ha ido mal.

 pcm.!default {
  type plug
  slave.pcm "eq"
 }

 # Redirigir la emulación OSS a través del EQ también (con programas que corren a través de "AOSS")

 pcm.dsp0 {
  type plug
  slave.pcm "eq"
 }

```

*   Ahora todo debe ir bien (en su defecto, pregunte en el foro).

## Remuestreo de alta calidad

Cuando el software de mezcla está habilitado, ALSA se ve obligado a volver a muestrear (remuestrear) todo en la misma frecuencia (48000 por defecto cuando se admite). Dmix utiliza un algoritmo de remuestreo pobre que produce una pérdida notable de la calidad de sonido.

Instale [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) y [libsamplerate](https://www.archlinux.org/packages/?name=libsamplerate).

Cambie el convertidor de frecuencia por defecto a libsamplerate:

 `/etc/asound.conf`  `defaults.pcm.rate_converter "samplerate_best"` 

o

 `~/.asoundrc`  `defaults.pcm.rate_converter "samplerate_best"` 

**samplerate_best** ofrece mejor calidad de sonido, pero se necesita una CPU decente para poder usarlo, ya que requiere una gran cantidad de ciclos de CPU en tiempo real para el remuestreo. Existen otros algoritmos disponibles (**samplerate**, etc.), pero no proporcionan una gran mejora respecto al remuestreador por defecto.

**Advertencia:** En algunos sistemas, samplerate_best puede causar un problema por el que no se obtiene ningún sonido desde flashplayer.

## Upmixing/Downmixing

### Upmixing

A fin de que una fuente de audio estéreo, como música, pueda ser capaz de ocupar todas las salidas de un sistema de sonido 5.1 o 7.1, es necesario utilizar upmixing. En el pasado este proceso resultaba difícil y propenso a errores, pero a día de hoy existen plugins que hacen fácil esta tarea. Por lo tanto, instale [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

A continuación, añada lo siguiente al archivo de configuración de ALSA de su elección (ya sea `/etc/asound.conf` o `~/.asoundrc`):

```
pcm.upmix71 {
    type upmix
    slave.pcm "surround71"
    delay 15
    channels 8
}

```

Puede cambiar fácilmente este ejemplo de upmixing 7.1 a 5.1 o 4.0.

Esto agrega un nuevo pcm que se puede utilizar por upmixing. Si desea que todas las fuentes de audio pasen por este pcm, agréguelo como predeterminado debajo de la definición anterior, así:

```
pcm.!default "plug:upmix71"

```

El plugin permite automáticamente múltiples fuentes de sonido para trabajar a través de él sin problemas, de modo que este ajuste por defecto es, en realidad, una elección segura. Si esto no funciona, pruebe configurar su propio dmixer, para efectuar upmixing del canal PCM, así:

```
pcm.dmix6 {
    type asym
    playback.pcm {
        type dmix
        ipc_key 567829
        slave {
            pcm "hw:0,0"
            channels 6
        }
    }
}

```

y usar «dmix6» en lugar de «surround71». Si experimenta problemas de sonido, como saltos o distorsiones, puede aumentar el buffer_size (a 32768, por ejemplo) o utilizar un [remuestreador de alta calidad.](#Remuestreo_de_alta_calidad)

### Downmixing

Si se quiere efectuar downmixing (pasar las fuentes de downmix a estéreo), por ejemplo, desea escuchar una película con sonido 5.1 en un equipo de música con salida estéreo, es necesario utilizar el plugin `vdownmix`, incluido en el paquete [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins).

Una vez más, en el archivo de configuración, añada lo siguiente:

```
pcm.!surround51 {
    type vdownmix
    slave.pcm "default"
}
pcm.!surround40 {
    type vdownmix
    slave.pcm "default"
}

```

**Nota:** Esto podría no ser suficiente para hacer funcionar downmixing, véase [[2]](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=541786). So, you might also need to add `pcm.!default "plug:surround51"` o `pcm.!default "plug:surround40"`. Sólo se puede utilizar un plug `vdownmix`; si tiene canales 7.1, necesitará utilizar `surround71` en el lugar de la configuración anterior. Un buen ejemplo, que incluye una configuración que funciona tanto con`vdownmix` como con `dmix`, se puede encontrar [aquí](https://bbs.archlinux.org/viewtopic.php?id=167275).

## Mezclar

### Mezclar con software (dmix)

**Nota:** Para versiones 1.0.9rc2 y superiores de ALSA, no es necesario configurar dmix para las salidas de sonido analógicas. Dmix está habilitado, de forma predeterminada, para las tarjetas de sonido que no son compatibles con el hardware de mezcla.

Si eso no funciona automáticamente, sin embargo, es cuestión simplemente de crear un archivo `.asoundrc` (o modificar el existente) en el directorio personal, con el siguiente contenido:

```
pcm.dsp {
    type plug
    slave.pcm "dmix"
}

```

Esto debería habilitar dmix (software de mezcla) y permitir el acceso simultáneo de más de una aplicación para hacer uso de la tarjeta de sonido.

Para una salida de sonido digital como S/PDIF, el paquete ALSA todavía no habilita dmix por defecto. Así, la configuración dmix anteriormente citada se puede usar para habilitar dmix para dispositivos con salida S/PDIF.

Consulte el apartado sobre [solución de problemas](#Soluci.C3.B3n_de_problemas) para los problemas más comunes y sus soluciones.

### Mezclar con Hardware

#### Soporte

Si tiene un chipset de audio que soporte mezclar con hardware, entonces no se requiere configuración. Casi todos los chipsets de sonido incorporados no son compatibles con el hardware de mezcla y requieren que la mezcla se haga con software (véase más arriba). Muchas tarjetas de sonido no tienen soporte para la mezcla con hardware y las que tienen mejor soporte en Linux son las siguientes:

*   Creative SoundBlaster Live! (modelo 5.1)
*   Creative SoundBlaster Audigy (algunos modelos)
*   Creative SoundBlaster Audidy 2 (modelos ZS)
*   Creative SoundBlaster Audigy 4 (modelos Pro)

**Nota:**

*   Las variantes de la gama baja de las tarjetas anteriores (Audigy SE, Audigy 2 NX, SoundBlaster Live! de 24 bits y SoundBlaster Live! 7.1) **no** proporcionan soporte de hardware de mezcla, las cuales usan otros chips.
*   Una excepción es el chip integrado VIA8237 que soporta hardware de mezcla de 4-stream. Sin embargo, en algunas placas base solo 3 funcionan (el cuarto no produce ningún sonido), o se rompe recién se inicia. Incluso si funciona, la calidad no es buena en comparación con otras soluciones.

#### Arreglos

Si está usando Arch 64-bit y la tarjeta *Intel Corporation 82801I (ICH9 Family) HD Audio Controller (rev 02)*, se puede obtener sonido para que funcione con «Enemy Territory» haciendo lo siguiente:

```
echo "et.x86 0 0 direct" > /proc/asound/card0/pcm0p/oss
echo "et.x86 0 0 disable" > /proc/asound/card0/pcm0c/oss

```

## Solución de problemas

### Sonido con saltos durante el uso de Dynamic Frequency Scaling

Algunas combinaciones de determinados drivers ALSA y chipsets pueden causar **saltos** en el audio de todas las fuentes cuando se utiliza en combinación con un regulador de frecuencia de la CPU de escalamiento dinámico como `ondemand` o `conservative`. En la actualidad, la solución es volver al gobernador `performance`.

Consulte la [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") para obtener más información.

### Problemas con la disponibilidad del software de mezcla por solo un usuario a la vez

Puede suceder que solo un usuario puede utilizar el dmixer a la vez. Esto probablemente pueda andar bien para la mayoría de los usuarios cuando solo ellos utilizan su máquina, pero para los que corren [mpd](/index.php/Mpd "Mpd") en una máquina con usuarios distintos plantea un problema. Cuando mpd está corriendo, otro usuario normal no puede reproducir sonidos mediante dmixer. Aunque es posible solucionarlo corriendo mpd en la cuenta de inicio de sesión del usuario habilitado, otra solución es factible. Añada la línea `ipc_key_add_uid 0` al bloque `pcm.dmixer` para desactivar esta limitación. El siguiente es un fragmento del código de `asound.conf`, el resto es lo mismo que el anterior.

```
...
pcm.dmixer {
 type dmix
 ipc_key 1024
 ipc_key_add_uid 0
 ipc_perm 0660
slave {
...

```

### Problemas de reproducción simultánea

Si está teniendo problemas de reproducción simultánea, y si [PulseAudio](/index.php/PulseAudio "PulseAudio") se ha instalado (por ejemplo, utilizando [GNOME](/index.php/GNOME "GNOME")), su configuración por defecto está ajustada para «secuestrar» a favor de pulseadio la tarjeta de sonido. Algunos usuarios de ALSA no desean utilizar [PulseAudio](/index.php/PulseAudio "PulseAudio") y están bastante satisfechos con su actual configuración de ALSA. Una solución para resolver el problema es editar `/etc/asound.conf` y comentar las siguientes líneas:

```
# Use PulseAudio by default
#pcm.!default {
#  type pulse
#  fallback "sysdefault"
#  hint {
#    show on
#    description "Default ALSA Output (currently PulseAudio Sound Server)"
#  }
#}

```

Comentando lo siguiente también puede resulta útil:

```
#ctl.!default {
#  type pulse
#  fallback "sysdefault"
#}

```

Esta puede ser una solución mucho más simple que desinstalar por completo [PulseAudio](/index.php/PulseAudio "PulseAudio").

Efectivamente, este es un ejemplo de un archivo `/etc/asound.conf` funcionando correctamente:

```
pcm.dmixer {
        type dmix
        ipc_key 1024
        ipc_key_add_uid 0
        ipc_perm 0660
}
pcm.dsp {
        type plug
        slave.pcm "dmix"
}

```

**Nota:** Este archivo `/etc/asound.conf` fue creado y utilizado con éxito para una configuración global de [MPD](/index.php/MPD "MPD"). Consulte [esta sección](/index.php/ALSA/Troubleshooting#Problems_with_availability_to_only_one_user_at_a_time "ALSA/Troubleshooting") sobre múltiples usuarios

### Ausencia de sonido al azar en el inicio

Se puede probar rápidamente el sonido mediante la ejecución de `speaker-test`. Si no hay sonido, el mensaje de error podría ser algo como:

```
 ALSA lib pcm_dmix.c:1022:(snd_pcm_dmix_open) unable to open slave
 Playback open error: -16
 Device or resource busy

```

Si no tiene sonido aleatoriamente en el arranque, puede deberse a que el sistema tiene varias tarjetas de sonido, y su orden puede, a veces, cambiar al inicio. Si este es el caso, trate de [configurar la tarjeta de sonido predefinida](#Establecer_la_tarjeta_de_sonido_predeterminada)

Si utiliza mpd y los consejos de configuración anteriores no funcionan para usted, intente [leyendo esto](http://mpd.wikia.com/wiki/Configuration#ALSA_MPD_software_volume_control) en su lugar.

#### Timidity

[Timidity](/index.php/Timidity "Timidity") puede ser la causa de la falta de audio. Pruebe a ejecutar:

```
$ systemctl status timidity

```

Si esto falla, pruebe `# killall -9 timidity`. Si esto resuelve el problema, debe desactivar el demonio timidity para que no se inicie al arranque.

### Problemas específicos de algunos programas

Algunos programas definen por sí su propia configuración de audio, por ejemplo, XMMS o Mplayer, con lo cual tendría que configurar sus opciones específicas.

Para mplayer, abra `~/.mplayer/config` (o `/etc/mplayer/mplayer.conf` para el ajuste global) y añada la siguiente línea:

```
ao=alsa

```

Para XMMS/Beep Media Player, entre en sus opciones y asegúrese de que el controlador de sonido está ajustado a ALSA y no, a OSS.

Para hacer esto en XMMS:

*   Abra XMMS
    *   Opciones → Preferencias.
    *   Elija el plugin de salida de Alsa.

Para las aplicaciones que no proporcionan compatibilidad con ALSA, puede usar AOSS desde el paquete alsa-oss. Para utilizar aoss, se ejecuta el programa, anteponiendo el prefijo `aoss`, por ejemplo:

```
aoss realplay

```

pcm.!default{ ... } parece que no funciona más, pruebe en su lugar:

```
 pcm.default pcm.dmixer

```

### Configurar los modelos

Aunque Alsa detecta la tarjeta de sonido a través de la BIOS, a veces puede no ser capaz de reconocer el [tipo de modelo](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio-Models.txt). El chip de la tarjeta de sonido puede ser encontrado en `alsamixer` (por ejemplo ALC662) y el modelo se puede ajustar en `/etc/modprobe.d/modprobe.conf` o `/etc/modprobe .d/sound.conf`. Por ejemplo:

```
options snd-hda-intel model=MODEL

```

Hay otras opciones, según el modelo. Para la mayoría de los casos, Alsa lo hará de manera automática, por defecto. Si desea ver más opciones de configuración específica para su tarjeta de sonido, eche un vistazo a la [Lista de Tarjetas de sonido Alsa](http://bugtrack.alsa-project.org/main/index.php/Matrix:Main), localice su modelo, a continuación, pinche en Detalles, a continuación, busque la sección «Setting up modprobe ...». Introduzca esos valores en el archivo `/etc/modprobe.d/modprobe.conf`. Por ejemplo, para una tarjeta de audio Intel AC97:

```
# ALSA portion
alias char-major-116 snd
alias snd-card-0 snd-intel8x0
# module options should go here

# OSS/Free portion
alias char-major-14 soundcore
alias sound-slot-0 snd-card-0

# card #1
alias sound-service-0-0 snd-mixer-oss
alias sound-service-0-1 snd-seq-oss
alias sound-service-0-3 snd-pcm-oss
alias sound-service-0-8 snd-seq-oss
alias sound-service-0-12 snd-pcm-oss
```

### Audio en conflicto con altavoz interno del PC

Si está seguro de que nada está silenciado, que los controladores están instalados correctamente y que el volumen es el correcto, pero todavía no se oye nada, entonces trate de añadir la siguiente línea a `/etc/modprobe.d/modprobe.conf`:

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

La solución anterior se ha observado que funciona con `via82xx`

```
options snd-NAME-OF-MODULE ac97_quirk=1

```

La solución anterior se ha informado que funciona con `snd_intel8x0`

### Sin entrada en el micrófono

En alsamixer, asegúrese de que todos los niveles del volumen, en la sección grabación, están activados, y que la modalidad *CAPTURE* del micrófono está activa (por ejemplo, Mic, -micrófono interno-) y/o sobre *capture* (en alsamixer, seleccione estos elementos en el primer espacio). Pruebe poner Mic Boost en positivo y aumentar al máximo los niveles de Capture y Digital; esto no produce sonido o lo produce distorsionado, pero entonces podrá ajustar los niveles hacia abajo hasta oir *algo* cuando se graba.

En la medida que pulseaudio se muestra como «default» en alsamixer, puede ser necesario presionar F6 para seleccionar la propia tarjeta de sonido en primer lugar. También puede ser necesario activar y aumentar el volumen de Line-in (Línea de entrada) en la sección Playblack (reproducción).

Para probar el micrófono, ejecute estas órdenes (consulte la página del manual de arecord para más información):

```
 arecord -d 5 test-mic.wav
 aplay test-mic.wav

```

Si todo falla, es posible que desee descartar un fallo de hardware, probando el micrófono con un dispositivo diferente.

En algunos ordenadores, silenciar un micrófono (MM) significa simplemente que su entrada no va de inmediato a los altavoces. Todavía recibe la entrada.

Muchos portátiles Dell necesitan «-dmic», que se añade al nombre del modelo en `/etc/modprobe.d/modprobe.conf`:

```
 options snd-hda-intel model=dell-m6-dmic

```

Algunos programas intenta utilizar OSS como software de entrada principal. Si tiene inicialmente activados los [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") `snd_pcm_oss`, `snd_mixer_oss` o `snd_seq_oss` (no se cargan de forma predeterminada), pruebe entonces evitar cargarlos.

Consulte también:

*   [http://www.alsa-project.org/main/index.php/SoundcardTesting](http://www.alsa-project.org/main/index.php/SoundcardTesting)
*   [http://alsa.opensrc.org/Record_from_mic](http://alsa.opensrc.org/Record_from_mic)

### Configuración predeterminada de Micrófono/Dispositivo de captura

Algunas aplicaciones (Pidgin, Adobe Flash) no ofrecen una opción para cambiar el dispositivo de captura. Se convierte en un problema si el micrófono está en un dispositivo separado (por ejemplo, webcam USB o micrófono) de la tarjeta de sonido interna. Para cambiar solo el dispositivo de captura predeterminado, dejando el dispositivo de reproducción predeterminado como está, puede editar el archivo `~/.asoundrc` para incluir lo siguiente:

```
pcm.usb
{
    type hw
    card U0x46d0x81d
}

pcm.!default
{
    type asym
    playback.pcm
    {
        type plug
        slave.pcm "dmix"
    }
    capture.pcm
    {
        type plug
        slave.pcm "usb"
    }
}

```

Reemplace «U0x46d0x81d» con el nombre de la tarjeta del dispositivo de captura en ALSA. Es posible utilizar la orden `arecord -L` para listar todos los dispositivos de captura detectados por ALSA.

### El micrófono interno no funciona

En primer lugar, asegúrese, en almixer, de que todos los niveles del volumen, en la sección de grabación, están activados. Para obtener un nuevo ajuste del volumen, llamado Capture, que registre el micrófono interno, vuelva a añadir una nueva opción al archivo /etc/sound.conf y recargue el módulo snd-*. Por ejemplo, para snd-hda-intel, añada:

```
 options snd-hda-intel enable_msi=1

```

Recargando el módulo (como se indica abajo), activará el nuevo ajuste del volumen de grabación (Capture) y luego pruebe.

 `# rmmod snd-hda-intel && modprobe snd-hda-intel` 

### Sin sonido con tarjeta de sonido Intel integrada

Puede haber un problema con dos módulos cargados en conflicto, a saber `snd_intel8x0` y `snd_intel8x0m`. En este caso, introduzca en blacklist snd_intel8x0m:

 `/etc/modprobe.d/modprobe.conf`  `blacklist snd_intel8x0m` 

*Deshabilitar* el canal «External Amplifier» en `alsamixer` o `amixer` también puede ayudar. Consulte [la wiki de ALSA](http://alsa.opensrc.org/Intel8x0#Dell_Inspiron_8600_.28and_probably_others.29).

Activar el sonido en la configuración de «Mix» en el mezclador puede ayudar, también.

### Sin sonido en auriculares con tarjeta de sonido Intel integrada

Si tiene un portatil con **Intel Corporation 82801 I (ICH9 Family) HD Audio Controller**, puede que tenga que añadir esta línea a modprobe o sound.conf:

```
options snd-hda-intel model=$model

```

Donde $model es cualquiera de los siguientes modelos (por orden de posibilidad de funcionar, no por mérito):

*   dell-vostro
*   olpc-xo-1_5
*   laptop
*   dell-m6
*   laptop-hpsense

**Nota:** Puede que sea necesario poner esas «opciones» abajo (después de) los «alias».

Puede ver todos los modelos disponibles en la documentación del kernel. Por ejemplo [aquí](http://git.kernel.org/?p=linux/kernel/git/stable/linux-2.6.35.y.git;a=blob;f=Documentation/sound/alsa/HD-Audio-Models.txt;h=dc25bb84b83b49665a7ed850e7bf5423d50cd3ba;hb=HEAD), pero compruebe que se trata de la versión correcta de ese documento para su versión del kernel.

Una lista de modelos disponibles también está recogida [aquí](http://www.mjmwired.net/kernel/Documentation/sound/alsa/HD-Audio-Models.txt). Para conocer el nombre de su chip debe escribir la siguiente orden (con el asterisco `*` que permite adaptarse a las peculiaridades de sus archivos). Tenga en cuenta que algunos chips podrían haber cambiado de nombre y no corresponderse directamente a los que están disponibles en el archivo.

```
cat /proc/asound/card*/codec* | grep Codec

```

Tenga en cuenta, por último, que hay una alta probabilidad de que ninguno de los dispositivos de entrada (todos los micrófonos internos y externos) funcionen si decide hacer esto, por lo que o funcionarán los auriculares o el micrófono. Por favor, informe a ALSA si se ve afectado por este error.

Por otro lado, si tiene problemas con las señales acústicas (pcspkr):

```
options snd-hda-intel model=$model enable=1 index=0

```

### Sin sonido cuando se instala la tarjeta de vídeo con S/PDIF

Localice los módulos disponibles y su orden:

```
$ cat /proc/asound/modules
0 snd_hda_intel
1 snd_ca0106

```

Desactive el códec de audio de la tarjeta de vídeo en `/etc/modprobe.d/modprobe.conf`:

```
# /etc/modprobe.d/modprobe.conf
#
install snd_hda_intel /bin/false

```

Si ambos dispositivos utilizan el mismo módulo, entonces podría utilizar el parámetro *enable* del módulo snd-hda-intel, el cual es una matriz booleana que permite activar/desactivar la tarjeta de sonido deseada.

Por ejemplo:

```
options snd-hda-intel enable=1,0

```

Lo siguiente da la lista de las tarjetas:

```
cat /proc/asound/cards

```

### Calidad de audio deficiente

Si la calidad de sonido es pobre, intente ajustar el volumen de PCM (en alsamixer) a un nivel tal que gain sea 0.

Si se ha cargado el controlador snd-usb-audio, puede intentar habilitar `softvol` en el archivo **/etc/asound.conf**. He aquí un ejemplo de configuración para el primer dispositivo de audio:

```
 pcm.!default {
   type plug
   slave.pcm "softvol"
 }
 pcm.dmixer {
      type dmix
      ipc_key 1024
      slave {
          pcm "hw:0"
          period_time 0
          period_size 4096
          buffer_size 131072
          rate 50000
      }
      bindings {
          0 0
          1 1
      }
 }
 pcm.dsnooper {
      type dsnoop
      ipc_key 1024
      slave {
          pcm "hw:0"
          channels 2
          period_time 0
          period_size 4096
          buffer_size 131072
          rate 50000
      }
      bindings {
          0 0
          1 1
      }
 }
 pcm.softvol {
      type softvol
      slave { pcm "dmixer" }
      control {
          name "Master"
          card 0
      }
 }
 ctl.!default {
   type hw
   card 0
 }
 ctl.softvol {
   type hw
   card 0
 }
 ctl.dmixer {
   type hw
   card 0
 }

```

### Crepiteos al iniciar y detener la reproducción

Algunos módulos (como snd-ac97-codec y snd-hda-intel) pueden apagar la tarjeta de sonido cuando no está en uso. Esto puede provocar un ruido audible (como un crack/pop/crepiteos) al encender/apagar su tarjeta de sonido. A veces, puede ocurrir, incluso, cuando se mueve el control deslizante del volumen, o las ventanas se abren y cierran (KDE4). Si encuentra este sonido molesto, puede ejecutar `modinfo snd-MY-MODULE`, y buscar una opción que regule o desactive esta función.

Ejemplo: para desactivar el modo de ahorro de energía utilizando snd-hda-intel para evitar las distorsiones y resolver el problema de sonido de los altavoces, añada en `/etc/modprobe.d/modprobe.conf`

```
[options snd-hda-intel power_save=0]

```

o

```
[options snd-hda-intel power_save=0 power_save_controller=N]

```

También puede probar con `modprobe snd_hda_intel power_save=0` antes.

Puede que sea necesario también activar el canal 'Line' de alsa para que esto funcione. Cualquier valor puede servir (que no sea '0' o algo muy alto).

*Ejemplo:* en una tarjeta integrada VIA VT1708S (utilizando el módulo snd-hda-intel) estas distorsiones seguían presentes a pesar de haber ajustado el parámetro 'power_save' a 0\. Activando el canal 'Line' y estableciendo el valor '1' se resolvió el problema.

Fuente: [http://www.kernel.org/doc/Documentation/sound/alsa/powersave.txt](http://www.kernel.org/doc/Documentation/sound/alsa/powersave.txt)

Si utiliza un ordenador portátil, pm-utils cambiará `power_save` de nuevo a `1` cuando se utiliza la batería, incluso si se desactiva el ahorro de energía en `/etc/modprobe.d`. Para solucionar este problema, desactive esta opción para pm-utils mediante la desactivación del script que realiza el cambio:

```
# chmod -x /usr/lib/pm-utils/power.d/intel-audio-powersave

```

### La salida S/PDIF no funciona

Si la salida digital óptica/coaxial de la placa base/tarjeta de sonido no funciona o ha dejado de funcionar, y en alsamixer los correspondientes canales de sonido están activados, pruebe lo siguiente:

```
# iecset audio on

```

También puede poner esta orden en un servicio de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") activado, ya que a veces puede dejar de funcionar después de un reinicio.

### La salida HDMI no funciona

El procedimiento descrito a continuación se puede utilizar para una prueba de audio HDMI. Antes de continuar, asegúrese de que ha activado y quitado el silencio de la salida con `alsamixer`.

**Nota:** Si utiliza una tarjeta ATI y el kernel de linux >=3.0, tendrá desactivado, por defecto, un módulo del kernel necesario. Consulte [ATI#HDMI audio](/index.php/ATI#HDMI_audio "ATI").

Conecte el PC a la pantalla mediante un cable HDMI y active la pantalla con una herramienta como `xrandr` o `arandr`. Por ejemplo:

```
$ xrandr # list outputs
$ xrandr --output DVI-D_1 --mode 1024x768 --right-of PANEL # enable output

```

Utilice la orden `aplay -l` para descubrir el número de la tarjeta y del dispositivo. Por ejemplo:

 `$ aplay -l` 
```
 **** List of PLAYBACK Hardware Devices ****
 card 0: SB [HDA ATI SB], device 0: ALC892 Analog [ALC892 Analog]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 0: SB [HDA ATI SB], device 1: ALC892 Digital [ALC892 Digital]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 **card 1**: Generic [HD-Audio Generic], **device 3**: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0

```

Ahora que tenemos la información del dispositivo HDMI, haga una prueba. En el siguiente ejemplo, 1 es el número de tarjeta y 3 es el número de dispositivo.

```
$ aplay -D plughw:1,3 /usr/share/sounds/alsa/Front_Center.wav

```

Si «aplay» no emite ningún error, pero aún no hay ningún sonido, «reinicie» el receptor, monitor o televisor. Desde la interfaz HDMI revise rigurosamente la conexión, dado que podría haber informado anteriormente de que no había flujo de audio y haber deshabilitado así la decodificación de audio.En particular, si está usando un gestor de ventanas independiente (distinto al de Gnome o KDE), puede que tenga un poco de reproducción de sonido mientras enchufa el cable HDMI.

Si la prueba tiene éxito, cree o modifique el archivo `~/.asoundrc` para establecer HDMI como el dispositivo de audio predeterminado.

 `~/.asoundrc` 
```
pcm.!default {
  type hw
  card 1
  device 3
}

```

O si la configuración de arriba no funciona, pruebe esto:

 `~/.asoundrc` 
```
defaults.pcm.card 1
defaults.pcm.device 3
defaults.ctl.card 1

```

### La salida multicanal PCM de HDMI no funciona (Intel)

En Linux 3.1 la salida multicanal PCM a través de HDMI con una tarjeta Intel (Intel Eaglelake, IbexPeak/Ironlake,SandyBridge/CougarPoint y IvyBridge/PantherPoint) aún no está soportada. El apoyo está siendo desarrollado actualmente y se espera que esté disponible para Linux 3.2\. Para hacer que funcione en Linux 3.1 es necesario aplicar los siguientes parches:

*   [drm: support routines for HDMI/DP ELD](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=patch;h=76adaa34db407f174dd06370cb60f6029c33b465)
*   [drm/i915: pass ELD to HDMI/DP audio driver](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=patch;h=e0dac65ed45e72fe34cc7ccc76de0ba220bd38bb)

### HP TX2500

Agregue estas dos líneas en `/etc/modprobe.d/modprobe.conf`:

```
options snd-cmipci mpu_port=0x330 fm_port=0x388
options snd-hda-intel index=0 model=toshiba position_fix=1

```

```
options snd-hda-intel model=hp (funciona para tx2000cto)

```

### Salto de sonido durante la reproducción MP3

Si tiene saltos de sonido al reproducir archivos MP3 y tiene más de dos altavoces conectados al ordenador (es decir, dos o más sistema de altavoces), ejecute `alsamixer` y desactive los canales para los altavoces que **NO** tiene (es decir, deshabilite, por ejemplo, el canal del altavoz central si no se dispone de un altavoz central).

### Auriculares USB y tarjetas de sonido externas USB

Si está usando un auricular USB con ALSA puede probar a usar [asoundconf](https://aur.archlinux.org/packages/asoundconf/) (actualmente solo disponible en [AUR](/index.php/AUR "AUR")) para ajustar el auricular como salida de sonido principal. Antes de proseguir, asegúrese de tener el módulo usb audio habilitado (`modprobe snd-usb-audio`).

```
# asoundconf is-active
# asoundconf list
# asoundconf set-default-card <tarjeta-de-sonido elegida>

```

#### Sonido crepitante con dispositivos USB

Si usted experimenta crepiteos o crujidos en dispositivos USB, puede intentar ajustar el snd-usb-audio para una latencia mínima.

Agregue lo siguiente a su `/etc/modprobe.d/modprobe.conf`:

```
options snd-usb-audio nrpacks=1

```

Fuente: [http://alsa.opensrc.org/Usb-audio#Tuning_USB_devices_for_minimal_latencies](http://alsa.opensrc.org/Usb-audio#Tuning_USB_devices_for_minimal_latencies)

#### Conexión hot-plugging de una tarjeta de sonido USB

Con el fin de configurar automáticamente una tarjeta de sonido USB como dispositivo de salida principal, cuando la tarjeta está conectada, puede utilizar las siguientes reglas udev (por ejemplo, añadir las dos líneas siguientes a `/etc/udev/rules.d/00-local.rules` y reiniciar).

```
KERNEL=="pcmC[D0-9cp]*", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#pcmC}; K=$${K%%D*}; echo defaults.ctl.card $$K > /etc/asound.conf; echo defaults.pcm.card $$K >>/etc/asound.conf'"
KERNEL=="pcmC[D0-9cp]*", ACTION=="remove", PROGRAM="/bin/sh -c 'echo defaults.ctl.card 0 > /etc/asound.conf; echo defaults.pcm.card 0 >>/etc/asound.conf'"
```

### Error 'Unkown hardware' después de una actualización del Kernel

Los siguientes mensajes pueden aparecer durante la puesta en marcha de ALSA después de la actualización del kernel:

```
Unknown hardware "foo" "bar" ...
Hardware is initialized using a guess method
/usr/sbin/alsactl: set_control:nnnn:failed to obtain info for control #mm (No such file or directory)

```

o

```
Found hardware: "HDA-Intel" "VIA VT1705" "HDA:11064397,18490397,00100000" "0x1849" "0x0397"
Hardware is initialized using a generic method
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #1 (No such file or directory)
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #2 (No such file or directory)
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #25 (No such file or directory)
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #26 (No such file or directory)

```

Simplemente guarde las configuraciones del mixer de ALSA otra vez (como root):

```
# alsactl -f /var/lib/alsa/asound.state store

```

Puede ser necesario configurar de nuevo ALSA con `alsamixer`.

### HDA Analyzer

Si las asignaciones de los pin (conectores) de audio no se corresponden con ALSA, pero este funciona bien, puede probar con HDA Analyzer -una interfaz gráfica de usuario pyGTK2 para el control de audio HD, que se puede encontrar en la [wiki de ALSA](http://www.alsa-project.org/main/index.php/HDA_Analyzer)-. Trate de configurar la sección de Control Widget para gestionar los PIN, ajustando IN para micrófonos y AUT para auriculares. Puede ser buena idea hacer referencia a los valores por defecto (Config Defaults).

**Nota:**

*   El script se ejecuta de tal manera que es incompatible con python3 (que es el actualmente proporcionado por ArchLinux) pero, no obstante, trate de usarlo.Para solucionar este problema, abra «run.py», encuentre todas las entradas de «python» (2 entradas - una en la primera línea, y la segunda en la última línea) y reemplácelas todas por «python2».
*   El script requiere acceso de root, pero no funciona a través de su/sudo. Ejecútelo mediante `kdesu` o `gksu`.

### ALSA con SDL

Si no se obtiene ningún sonido a través de SDL, y ALSA no puede ser seleccionado desde la configuración de la aplicación, pruebe a establecer la variable de entorno SDL_AUDIODRIVER a «alsa».

 `# export SDL_AUDIODRIVER=alsa` 

### Alternativa al sonido bajo

Si se obtiene un sonido bajo, incluso después usar al máximo sus altavoces/auriculares, puede intentar solucionar el problema probando el plugin softvol. Agregue lo siguiente a `/etc/asound.conf`.

```
pcm.!default {
      type plug
      slave.pcm "softvol"
  }

pcm.softvol {
    type softvol
    slave {
        pcm "dmix"
    }
    control {
        name "Pre-Amp"
        card 0
    }
    min_dB -5.0
    max_dB 20.0
    resolution 6
}

```

**Nota:** Es probable que tenga que reiniciar el equipo, así como reiniciar el demonio si alsa no se ha cargado con la nueva configuración. Además, si la configuración no funciona, incluso después de reiniciar, intente cambiar `plug` con `hw` en la configuración antes expuesta

Después que los cambios se carguen correctamente, aparecerá una nueva sección `Pre-Amp` en alsamixer. Puede ajustar los niveles desde allí.

**Nota:**

*   Establecer un valor alto para `Pre-Amp` puede causar distorsión del sonido, por lo que ajustelo de acuerdo al nivel más adecuado.
*   Algunos códecs de audio pueden necesitar ajustes en el HDA Analyzer ([véase arriba](#HDA_Analyzer)) a fin de lograr un volumen adecuado y sin distorsión. Comprobar la opción HP con el control del widget en el interruptor del Playback (Node[0x14] PIN en el códec ALC892, por ejemplo) puede, a veces, mejorar la calidad del audio y del volumen significativamente.

### Sonido abrupto después de reanudar la suspensión

Se puede escuchar un sonido a modo de estallido después de reanudar el equipo desde la suspensión. Esto se puede solucionar editando `/etc/pm/sleep.d/90alsa` y eliminado la línea que dice `aplay -d 1 /dev/zero`

### Silencio después de reiniciar

Tras el arranque, el ajuste de sonido establecido con alsamixer no permanece. Talvez se pueda restablecerlo con la orden `sudo alsactl restore`. Compruebe el estado del indicador `Auto-Mute` en alsamixer: ajuste `Enabled` a `Disabled`.

## Configuraciones de ejemplo

Consulte [Advanced Linux Sound Architecture/Example Configurations](/index.php/Advanced_Linux_Sound_Architecture/Example_Configurations "Advanced Linux Sound Architecture/Example Configurations").

## Véase también

*   [Advanced ALSA module configuration](http://www.mjmwired.net/kernel/Documentation/sound/alsa/ALSA-Configuration.txt)
*   [Unofficial ALSA Wiki](http://alsa.opensrc.org/Main_Page)
*   [HOWTO: Compile driver from svn](https://bbs.archlinux.org/viewtopic.php?id=36815)