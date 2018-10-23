**Estado de la traducción**
Este artículo es una traducción de [VLC media player](/index.php/VLC_media_player "VLC media player"), revisada por última vez el **2018-10-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=VLC_media_player&diff=0&oldid=550109) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Desde la [página de inicio](https://www.videolan.org/vlc/) del proyecto:

	VLC es un marco y reproductor multimedia multiplataforma gratuito y de código abierto que reproduce la mayoría de los archivos multimedia, así como DVD, CD de audio, VCD y varios protocolos de transmisión.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Idioma](#Idioma)
*   [3 Máscaras](#M.C3.A1scaras)
*   [4 Interfaz Web](#Interfaz_Web)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Twitch.tv transmitiendo a través de VLC](#Twitch.tv_transmitiendo_a_trav.C3.A9s_de_VLC)
    *   [5.2 Reproducción de contenido transmitido desde un servidor DLNA local](#Reproducci.C3.B3n_de_contenido_transmitido_desde_un_servidor_DLNA_local)
    *   [5.3 Control usando teclas de acceso rápido o cli](#Control_usando_teclas_de_acceso_r.C3.A1pido_o_cli)
    *   [5.4 Previniendo múltiples instancias](#Previniendo_m.C3.BAltiples_instancias)
    *   [5.5 Aceleración de vídeo por hardware](#Aceleraci.C3.B3n_de_v.C3.ADdeo_por_hardware)
    *   [5.6 Servicio de systemd](#Servicio_de_systemd)
    *   [5.7 Soporte de Chromecast](#Soporte_de_Chromecast)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Vídeo roto u otro problema después de la actualización](#V.C3.ADdeo_roto_u_otro_problema_despu.C3.A9s_de_la_actualizaci.C3.B3n)
    *   [6.2 Fallo de segmentación](#Fallo_de_segmentaci.C3.B3n)
    *   [6.3 Faltan iconos en los menús desplegables](#Faltan_iconos_en_los_men.C3.BAs_desplegables)
    *   [6.4 Error al abrir el backend VDPAU](#Error_al_abrir_el_backend_VDPAU)
    *   [6.5 No se reproducen a través de SFTP los nombres de los archivos multimedia que contienen espacios](#No_se_reproducen_a_trav.C3.A9s_de_SFTP_los_nombres_de_los_archivos_multimedia_que_contienen_espacios)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [vlc](https://www.archlinux.org/packages/?name=vlc).

Las variantes notables son:

*   [vlc-git](https://aur.archlinux.org/packages/vlc-git/) - Rama de desarrollo.
*   [vlc-nox](https://aur.archlinux.org/packages/vlc-nox/) - Sin soporte X.

## Idioma

VLC no ofrece una opción para cambiar el idioma en su menú *Preferencias*. Pero puedes usar el prefijo *LANGUAGE=*. Por ejemplo, modifique la línea `/usr/share/applications/vlc.desktop`:

```
Exec=/usr/bin/vlc %U

```

a:

```
Exec=LANGUAGE=fr /usr/bin/vlc %U

```

para cambiar la interfaz VLC al francés.

## Máscaras

VLC puede ser "desollado" para una apariencia diferente. Puede obtener máscaras en el sitio web [skins](https://www.videolan.org/vlc/skins.php).

Para instalar una máscara descárguela y muévala a:

```
~/.local/share/vlc/skins2

```

Abra VLC, haga clic en *Herramientas> Preferencias*. Cuando se abra la ventana de preferencias, debería estar en la pestaña "Interfaz"

Elija el botón de opción "Usar máscara personalizada" y seleccione la máscara descargada.

Reinicie VLC para que el cambio surta efecto.

## Interfaz Web

Ejecute VLC con el parámetro `--extraintf=http` para usar la interfaz de escritorio y web. El parámetro `--http-host` especifica la dirección a, que es `localhost` por defecto. Para establecer una contraseña, use `--http-password`, de lo contrario VLC no le permitirá iniciar sesión

```
# vlc --extraintf=http --http-host 0.0.0.0 --http-port 8080 --http-password 'sucontraseñaaquí'

```

O puede habilitar esta función en la interfaz de usuario si navega a "Ver> Agregar interfaz> Interfaz web".

El puerto por defecto de VLC es el 8080: [http://127.0.0.1:8080](http://127.0.0.1:8080)

Edite `/usr/share/vlc/lua/http/.hosts` para permitir conexiones remotas. Deberá reiniciar VLC para que los cambios surtan efecto.

## Consejos y trucos

### Twitch.tv transmitiendo a través de VLC

Vea [Streamlink#Twitch](/index.php/Streamlink#Twitch "Streamlink").

### Reproducción de contenido transmitido desde un servidor DLNA local

Si descubre que está intentando reproducir contenido uPNP/DLNA (yendo a "Ver> Lista de reproducción> Red local> Reproducir y conectar universal"), vlc no ve el servidor DLNA en la red local, luego asegúrese de que el firewall no está bloqueando el puerto 1900 UDP. Es esencial que este puerto esté abierto para reproducir contenido local de uPNP / DLNA.

### Control usando teclas de acceso rápido o cli

Instale [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat).

Obtenga el script en: [http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035](http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035)

Siga las instrucciones en el script para configurar un socket para VLC.

Ejecute el script desde la línea de comandos o registre el script con atajos de teclado a través de su escritorio.

Alternativamente, puede usar dbus-send [como se explica aquí](https://theelitist.github.io/control-vlc-media-player-through-d-bus) para interactuar con VLC:

```
$ dbus-send --print-reply --session --dest=org.mpris.MediaPlayer2.vlc /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause

```

### Previniendo múltiples instancias

La configuración predeterminada para VLC es abrir una nueva instancia del programa para cada archivo que se abre. Esto puede ser molesto si está utilizando VLC para algo como reproducir su colección de música. Puede deshabilitar esto en *Herramientas> Preferencias> Interfaz> Instancias> Permitir solo una instancia* . Opcionalmente, marque "Encolar archivos cuando se encuentre en modo de instancia", que mantiene la reproducción del archivo actual y agrega cualquier archivo recién abierto a la lista de reproducción actual.

### Aceleración de vídeo por hardware

Véase [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

VLC intenta automáticamente usar una API disponible, pero puede anularla yendo a "Herramientas> Preferencias> Entrada y códecs" y seleccionando la opción adecuada en "Decodificación acelerada por hardware", por ejemplo. `API de aceleración de vídeo (VA)` para VA-API o `Video Decode y API de presentación para Unix (VDPAU)` para VDPAU.

### Servicio de systemd

La interfaz web de VLC se puede iniciar desde systemd. Primero, necesita crear un usuario predeterminado:

```
# useradd -c "VLC daemon" -d / -G audio -M -p \! -r -s /usr/bin/nologin -U vlcd

```

Ahora cree el archivo de servicio systemd:

 `/etc/systemd/system/vlc.service` 
```
[Unit]
Description=VideoOnLAN Service
After=network.target

[Service]
Type=forking
User=vlcd
ExecStart=/usr/bin/vlc --daemon --syslog -I http --http-port 8090 --http-password *password* 
Restart=on-abort

[Install]
WantedBy=multi-user.target

```

[Inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") y [habilite](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `vlc.service`. Inicie sesión en http://*yourmachine*:8090/ sin nombre de usuario y con la contraseña que ingresa en el archivo de servicio.

### Soporte de Chromecast

A partir de la versión 3.0 (rama *Vetinari*), VLC puede transmitir a dispositivos Chromecast en la misma red inalámbrica.

Instale los paquetes:

*   [libmicrodns](https://www.archlinux.org/packages/?name=libmicrodns) - VLC puede encontrar el dispositivo Chromecast y aparece en el menú *Reproducción > Procesador*
*   [protobuf](https://www.archlinux.org/packages/?name=protobuf) - habilita la transmisión al dispositivo seleccionado en el menú *Reproducción > Renderizador*

## Solución de problemas

### Vídeo roto u otro problema después de la actualización

De vez en cuando, VLC tendrá algunos problemas con la configuración incluso en versiones menores. Antes de realizar informes de errores, elimine o cambie el nombre de su configuración ubicada en `~/.config/vlc` y confirme si el problema sigue ahí.

Si utiliza una variante ffmpeg de AUR, asegúrese de que también la haya actualizado. Pacman no lo actualizará cuando sea necesario y una falta de coincidencia interrumpirá VLC.

### Fallo de segmentación

Al iniciar VLC, puede obtener un fallo de seguridad y descartar factores generales como [microcódigo](/index.php/Microcode "Microcode"), una posible solución a esto es ejecutar lo siguiente:

```
# /usr/lib/vlc/vlc-cache-gen /usr/lib/vlc/plugins

```

Luego vuelva a instalar VLC.

Si eso no funciona, VLC tiene un problema de segfault con `plugins.dat` (vea [FS#57777](https://bugs.archlinux.org/task/57777)), simplemente elimine el archivo:

```
# rm /usr/lib/vlc/plugins/plugins.dat

```

### Faltan iconos en los menús desplegables

Esto puede suceder bajo XFCE, no habrá más íconos en los menús desplegables, como el ícono de la tarjeta PCI.

Ejecute estos comandos para reactivar estos iconos:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true
```

### Error al abrir el backend VDPAU

consulte [Hardware video acceleration#Failed to open VDPAU backend](/index.php/Hardware_video_acceleration#Failed_to_open_VDPAU_backend "Hardware video acceleration").

Como su sistema probablemente no admita VDPAU, debería decirle a VLC que use VA-API en su lugar, véase [#Aceleración de vídeo por hardware](#Aceleraci.C3.B3n_de_v.C3.ADdeo_por_hardware).

### No se reproducen a través de SFTP los nombres de los archivos multimedia que contienen espacios

Si VLC no reproduce ningún vídeo o archivo de audio a través de SFTP, asegúrese de tener instalado [sshfs](https://www.archlinux.org/packages/?name=sshfs).

Si se niega a reproducir cualquier archivo multimedia que contenga espacios a través de SFTP y siempre solicita autenticación, cambie la línea Exec en el archivo `vlc.desktop` a:

```
Exec=/usr/bin/vlc --started-from-file %F

```

Ver [[1]](https://bugs.launchpad.net/ubuntu/+source/vlc/+bug/239431/comments/11).

## Véase también

*   [Artículo Wikipedia](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")
*   [List of applications#Multimedia](/index.php/List_of_applications#Multimedia "List of applications")
*   [Página inicial VLC](https://www.videolan.org/vlc/)
*   [playerctl](https://github.com/acrisci/playerctl): Una utilidad de línea de comandos y una biblioteca para controlar reproductores multimedia
*   [Controlar VLC a través de un navegador](https://wiki.videolan.org/Control_VLC_via_a_browser)