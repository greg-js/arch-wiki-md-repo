Del [FAQ](https://github.com/Bumblebee-Project/Bumblebee/wiki/FAQ) de Bumblebee:

*Bumblebee es una solución para aprovechar la tecnología Nvidia Optimus, presente en los ordenadores portátiles habilitados, disponible para los sistemas GNU/Linux. Esta tecnología combina el uso de dos tarjetas gráficas con dos perfiles diferentes de consumo de energía, que están conectadas de una manera estratificada compartiendo un solo framebuffer*.

## Contents

*   [1 Bumblebee: Tecnología Optimus para Linux](#Bumblebee:_Tecnolog.C3.ADa_Optimus_para_Linux)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Instalar Bumblebee con Intel/NVIDIA](#Instalar_Bumblebee_con_Intel.2FNVIDIA)
    *   [2.2 Instalar Bumblebee con Intel/Nouveau](#Instalar_Bumblebee_con_Intel.2FNouveau)
*   [3 Iniciar Bumblebee](#Iniciar_Bumblebee)
*   [4 Uso](#Uso)
*   [5 Configuración](#Configuraci.C3.B3n)
    *   [5.1 Optimizar la velocidad cuando se utiliza VirtualGL como puente](#Optimizar_la_velocidad_cuando_se_utiliza_VirtualGL_como_puente)
    *   [5.2 Administración de energía](#Administraci.C3.B3n_de_energ.C3.ADa)
        *   [5.2.1 Estado de energía predeterminado de la tarjeta NVIDIA](#Estado_de_energ.C3.ADa_predeterminado_de_la_tarjeta_NVIDIA)
        *   [5.2.2 Activar la tarjeta NVIDIA durante el apagado](#Activar_la_tarjeta_NVIDIA_durante_el_apagado)
    *   [5.3 Varios monitores](#Varios_monitores)
        *   [5.3.1 Salidas conectadas al chip de Intel](#Salidas_conectadas_al_chip_de_Intel)
        *   [5.3.2 Salidas conectadas al chip de NVIDIA](#Salidas_conectadas_al_chip_de_NVIDIA)
            *   [5.3.2.1 xf86-video-intel-virtual-crtc y hybrid-screenclone](#xf86-video-intel-virtual-crtc_y_hybrid-screenclone)
*   [6 Cambiar entre tarjeta dedicada e integrada como Windows](#Cambiar_entre_tarjeta_dedicada_e_integrada_como_Windows)
*   [7 CUDA sin Bumblebee](#CUDA_sin_Bumblebee)
*   [8 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [8.1 [VGL] ERROR: Could not open display :8](#.5BVGL.5D_ERROR:_Could_not_open_display_:8)
    *   [8.2 [ERROR]Cannot access secondary GPU](#.5BERROR.5DCannot_access_secondary_GPU)
        *   [8.2.1 Ningún dispositivo detectado](#Ning.C3.BAn_dispositivo_detectado)
        *   [8.2.2 NVIDIA(0): Failed to assign any connected display devices to X screen 0](#NVIDIA.280.29:_Failed_to_assign_any_connected_display_devices_to_X_screen_0)
    *   [8.3 ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored.](#ERROR:_ld.so:_object_.27libdlfaker.so.27_from_LD_PRELOAD_cannot_be_preloaded:_ignored.)
    *   [8.4 Fatal IO error 11 (Recurso temporalmente no disponible) en el servidor X](#Fatal_IO_error_11_.28Recurso_temporalmente_no_disponible.29_en_el_servidor_X)
    *   [8.5 Vídeo rasgado](#V.C3.ADdeo_rasgado)
    *   [8.6 Bumblebee no puede conectarse al socket](#Bumblebee_no_puede_conectarse_al_socket)
*   [9 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Bumblebee: Tecnología Optimus para Linux

La [Tecnología Optimus](http://www.nvidia.com/object/optimus_technology.html) es una implementación [*gráfica híbrida*](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics) sin un hardware multiplexor. La GPU integrada controla la pantalla, mientras que la GPU dedicada gestiona las prestaciones más exigente y envía el resultado a la GPU integrada para la visualización. Cuando el ordenador está funcionando con alimentación de la batería, la GPU dedicada se apaga para ahorrar energía y prolongar la autonomía de la batería.

Bumblebee es una implementación de software que se comprende de dos partes:

*   Procesa programas fuera de pantalla utilizando la tarjeta de vídeo dedicada y los visualiza en la pantalla con la tarjeta de vídeo integrada. Este puente es proporcionado por VirtualGL o primus (leer más adelante) y se conecta a un servidor X iniciado por la tarjeta de video dedicada.
*   Deshabilita la tarjeta de vídeo dedicada cuando no está en uso (véase el apartado [#Administración de energía](#Administraci.C3.B3n_de_energ.C3.ADa))

Se trata de imitar el comportamiento de la tecnología Optimus, utilizando la GPU dedicada para aprovechar sus prestaciones cuando sea necesario y apagarla cuando no esté en uso. Las versiones actuales solo soportan las prestaciones a petición, mientras que no está implementado aún el que un programa se inicie automáticamente con la tarjeta de video dedicada en función de la carga de trabajo.

**Advertencia:** Bumblebee está todavía en desarrollo, por lo que toda ayuda será bien recibida.

## Instalación

Antes de proceder a la instalación de Bunblebee compruebe su BIOS y active la opción *Optimus* (los ordenadores portátiles más antiguos la llaman *«shareable graphics»*), si es posible (no todas las BIOS proporcionan esta opción), e instale el [controlador intel](/index.php/Intel_(Espa%C3%B1ol) "Intel (Español)") para la tarjeta gráfica secundaria.

Varios paquetes están disponibles para una configuración completa:

*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) - el paquete principal que proporciona el demonio y programas clientes.
*   (opcional) [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) (o [bbswitch-dkms](https://www.archlinux.org/packages/?name=bbswitch-dkms)) - recomendado para ahorrar energía desactivando la tarjeta Nvidia.
*   (opcional) Si quiere algo más que un simple ahorro de energía, es decir procesar programas con la tarjeta Nvidia dedicada, también es necesario:
    *   Un controlador para la tarjeta de Nvidia. El controlador de código abierto `nouveau` o el controlador propietario `nvidia`. Véase la subsección correspondiente.
    *   Un puente para los procesos/pantalla. Dos paquetes están disponibles en la actualidad para ello, [primus](https://www.archlinux.org/packages/?name=primus) (o [primus-git](https://aur.archlinux.org/packages/primus-git/)) y [virtualgl](https://www.archlinux.org/packages/?name=virtualgl). Solo uno de ellos es necesario, pero la instalación de ambos no hace daño.

**Nota:** Si desea ejecutar una aplicación de 32 bits en un sistema de 64-bit debe instalar las bibliotecas apropiadas lib32-* del programa. Además de esto, también es necesario instalar [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) o [lib32-primus](https://www.archlinux.org/packages/?name=lib32-primus), dependiendo de su elección para el «render bridge» (*puentear prestaciones*). Basta con asegurarse de ejecutar `primusrun` en lugar de `optirun` si decide utilizar Primus render bridge.

### Instalar Bumblebee con Intel/NVIDIA

*   [Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [mesa](https://www.archlinux.org/packages/?name=mesa), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) y [nvidia](https://www.archlinux.org/packages/?name=nvidia).

Si desea ejecutar las aplicaciones de 32 bits (como los juegos con wine) en un sistema de 64 bits necesita también el paquete [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils).

**Advertencia:** No instale [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl). Bumblebee encontrará las bibliotecas lib32 de NVIDIA correctas sin aquel paquete.

### Instalar Bumblebee con Intel/Nouveau

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)"):

*   [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) - controlador experimental con aceleración 3D.
*   [nouveau-dri](https://www.archlinux.org/packages/?name=nouveau-dri) - controladores Mesa classic DRI + Gallium3D.
*   [mesa](https://www.archlinux.org/packages/?name=mesa) - bibliotecas gráficas Mesa 3-D.

## Iniciar Bumblebee

Para poder utilizar Bumblebee es necesario añadir el propio usuario (y otros eventuales usuarios) al grupo bumblebee:

```
# gpasswd -a $USER bumblebee

```

donde `$USER` es el nombre de inicio de sesión del usuario. A continuación, cierre la sesión para que surtan efectos los cambios de grupo.

**Sugerencia:** Para iniciar **bumblebee** automáticamente al arranque, active el servicio **bumblebeed** de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

Terminado, reinicie el sistema y utilice el programa `[optirun](#Uso)` para disfrutar de la tecnología NVIDIA Optimus para el *rendering*.

Si simplemente desea desactivar su tarjeta NVIDIA, esto debería ser todo lo que se necesita, además de tener instalado `bbswitch`. El demonio bumblebeed, de forma predeterminada, instruye a bbswitch para desactivar la tarjeta cuando se inicia. Consulte también la sección [administración de energíam](#Administraci.C3.B3n_de_energ.C3.ADa)ás abajo.

## Uso

El programa de línea de comandos `optirun` equipado con Bumblebee, es su mejor aliado para ejecutar aplicaciones corriendo en su tarjeta NVIDIA Optimus.

Compruebe si Bumblebee funciona con el sistema Optimus mediante la siquiente orden:

```
$ optirun glxgears -info

```

Si tiene éxito y el terminal donde se está ejecutando muestra algo acerca de su tarjeta NVIDIA significa que ¡Optimus está funcionando con Bumblebee!

Utilización general:

 `$ optirun [opciones] *aplicación* [parámetros-de-la-aplicación]` 

Algunos ejemplos:

Iniciar aplicaciones de Windows con Optimus:

```
$ optirun wine *aplicación de windows*.exe

```

Utilizar NVIDIA Settings con Optimus:

```
$ optirun nvidia-settings -c :8

```

Para obtener una lista de opciones para `optirun`, vea las páginas del manual.

Existe un programa nuevo llamado a convertirse en la opción predefinida debido a que aporta un mejor desempeño, llamado primus. En la actualidad es necesario ejecutar este programa por separado (no admite opciones a diferencia de `optirun`), pero en el futuro va a poder ser iniciado por optirun. Utilización:

```
$ primusrun glxgears

```

## Configuración

Puede configurar el comportamiento de Bumblebee para satisfacer sus necesidades. Afinar ajustes como la optimización de la velocidad, administración de energía y otros recursos se pueden configurar en `/etc/bumblebee/bumblebee.conf`

### Optimizar la velocidad cuando se utiliza VirtualGL como puente

Bumblebee gestiona la presentación de los fotogramas para la tarjeta NVIDIA Optimus en un servidor X con VirtualGL invisible y lo transporta de vuelta al servidor X visible.

Los Frames se comprimen antes de ser transportados - esto ahorra ancho de banda y se puede utilizar para la optimización de la velocidad de Bumblebee:

Para utilizar un método de compresión para una sola aplicación, la sintaxis del comando es:

```
$ optirun -c <método-de-comprensión> aplicación

```

El método de compresión afectará al rendimiento del uso de la CPU/GPU. Los métodos que comprimen (como `jpeg`) cargan la máximo la CPU y al mínimo posible la GPU; los métodos que no comprimen cargan más la GPU mientras la CPU tendrá la carga mínima posible.

Métodos comprimidos son: `jpeg`, `rgb`, `yuv`

Métodos sin comprimir son: `proxy`, `xv`

Para utilizar un estándar de compresión para todas las aplicaciones habrá que establecer el valor `VGLTransport` con el `<método-de-compresión>` preferido en `/etc/bumblebee/bumblebee.conf`

 `/etc/bumblebee/bumblebee.conf` 
```
[...]
[optirun]
VGLTransport=proxy
[...]

```

También se puede reproducir con el método VirtualGL que vuelve a leer los píxeles de la tarjeta gráfica. Ajustando la variable de entorno `VGL_READBACK` a `pbo` debe aumentar el rendimiento. Comparar estas dos:

```
# PBO debería ser más rápido.
VGL_READBACK=pbo optirun glxspheres
# El valor por defecto es sync.
VGL_READBACK=sync optirun glxspheres

```

**Nota:** El escalado de frecuencia de la CPU afectará directamente a las prestaciones del renderizado

### Administración de energía

El objetivo de gestionar la energía consiste en apagar la tarjeta NVIDIA cuando no se utiliza más por bumblebee. Si bbswitch está instalado, detectará automáticamente cuándo se inicia el demonio Bumblebee. No es necesario ninguna configuración adicional.

#### Estado de energía predeterminado de la tarjeta NVIDIA

El comportamiento predeterminado de bbswitch es dejar el estado de energía de la tarjeta sin cambios. `bumblebeed` deshabilita la tarjeta cuando se inicia, así que lo siguiente solo es necesario si se utiliza bbswitch sin bumblebeed.

Configure la opción de los módulos `load_state` y `unload_state` de acuerdo a sus necesidades (véase la [documentación de bbswitch](https://github.com/Bumblebee-Project/bbswitch)).

 `/etc/modprobe.d/bbswitch.conf` 
```
options bbswitch load_state=0 unload_state=1

```

#### Activar la tarjeta NVIDIA durante el apagado

La tarjeta NVIDIA no puede inicializarse correctamente durante la fase de arranque si la tarjeta se apaga cuando el sistema se cerró por última vez. Una solución es configurar la opción `TurnCardOffAtExit=false` en `/etc/bumblebee/bumblebee.conf`, sin embargo, ésto todavía permitirá a la tarjeta detenerse cada vez que lo haga el daemon de Bumblebee, aunque se haga manualmente. Para asegurarse de que la tarjeta NVIDIA esté siempre accecible, es decir, activa, durante el apagado, añada el siguiente servicio de[systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") (si está utilizando [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)):

 `/etc/systemd/system/nvidia-enable.service` 
```
[Unit]
Description=Enable NVIDIA card

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'echo ON > /proc/acpi/bbswitch'

[Install]
WantedBy=shutdown.target
```

A continuación, active el servicio ejecutando `systemctl enable nvidia-enable.service` en un terminal como root.

### Varios monitores

#### Salidas conectadas al chip de Intel

Si el puerto (DisplayPort/HDMI/VGA) está conectado al chip de Intel, es posible configurar varios monitores con xorg.conf. Puede ajustarse para utilizar la tarjeta Intel, pero con Bumblebee todavía será posible usar la tarjeta NVIDIA. Un ejemplo de configuración, a continuación, muestra dos pantallas idénticas con una resolución de 1080p y utilizando la salida HDMI.

 `/etc/X11/xorg.conf` 
```
Section "Screen"
    Identifier     "Screen0"
    Device         "intelgpu0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "intelgpu1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "intelgpu0"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier     "intelgpu1"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection
```

Necesitará probablemente cambiar el BusID tanto para el procesador Intel como para la tarjeta NVIDIA.

 `$ lspci | grep VGA` 
```
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)

```

En este ejemplo el BusID es 0:2:0

#### Salidas conectadas al chip de NVIDIA

En algunos notebooks, la salida de vídeo digital (HDMI o Displayport) está conectado con el chip de NVIDIA. Si desea utilizar todas las pantallas en tal sistema simultáneamente, tiene que ejecutar dos servidores X. El primer servidor va a utilizar el controlador de Intel para el panel del notebook y una pantalla conectada a VGA. La segunda se iniciará a través de optirun con la tarjeta de NVIDIA, y acciona la pantalla digital.

Actualmente existen varias instrucciones en la web sobre cómo se pueden hacer tales ajustes para que funcione. Una de esas instrucciones se pueden encontrar en la [página wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup) de bumblebee. A continuación se describe otro enfoque adecuado.

##### xf86-video-intel-virtual-crtc y hybrid-screenclone

Este método utiliza un controlador parcheado de Intel, que viene modificado para tener una pantalla VIRTUAL, y el programa hybrid-screenclone que viene usado para copiar la pantalla desde la pantalla virtual a un segundo servidor X que se ejecuta en la tarjeta NVIDIA utilizando Optirun. El mérito debemos atribuirlo a [Triple-head monitors on a Thinkpad T520](http://judsonsnotes.com/notes/index.php?option=com_content&view=article&id=673:triple-head-monitors-on-thinkpad-t520&catid=37:tech-notes&Itemid=59) que contiene una explicación detallada sobre cómo hacer esto en un sistema Ubuntu.

Para simplificar, DP se utiliza a continuación para referirse a la salida digital (DisplayPort). Las instrucciones deben ser las mismas si el portátil tiene un puerto HDMI en su lugar.

*   Configurar el sistema para utilizar exclusivamente la tarjeta NVIDIA, hacer prueba combinando DP/Monitor y generar xorg.nvidia.conf. No se requiere este paso, pero se recomienda si la Bios del sistema tiene una opción para cambiar los gráficos a modalidad «NVIDIA-only». Para ello, primero desinstale el paquete bumlbebee e instale solo el controlador de NVIDIA. A continuación, reinicie el sistema, entre en la BIOS y cambie los gráficos a «NVIDIA-only». Cuando vuelva a Arch, conecte el Monitor a la DP y utilice startx para comprobar que todo funciona correctamente. Utilice Xorg -configure para generar un archivo xorg.conf para la tarjeta NVIDIA. Este nos será muy útil más adelante.
*   Vuelva a instalar bumlbebee y bbswitch, reinicie y configure la gráfica del sistema a «Hybrid» en la BIOS.
*   Instale [xf86-video-intel-virtual-crtc](https://aur.archlinux.org/packages/xf86-video-intel-virtual-crtc/), y sustituya el paquete xf86-video-intel con aquel.
*   Descargue [hybrid-screenclone](https://github.com/liskin/hybrid-screenclone) y compílelo utilizando "make".
*   Cambie estos ajustes en el archivo bumblebee.conf:

 `/etc/bumblebee/bumblebee.conf` 
```
KeepUnusedXServer=true
Driver=nvidia
```

**Nota:** Lance el parámetro PMMethod ajustado para "bumblebee". Esto es contrario a las instrucciones relacionadas en el artículo anterior, pero en Arch es necesario lanzarlo para que el módulo bbswitch se cargue automáticamente con esta opción.

*   Copie el archivo xorg.conf generado en el Paso 1 al directorio `/etc/X11` (por ejemplo `/etc/X11/xorg.nvidia.conf`). En la sección [driver-nvidia] del archivo `bumblebee.conf`, cambie el parámetro `XorgConfFile` para que apunte al mismo.
*   Compruebe que la configuración del archivo `/etc/X11/xorg.nvidia.conf` funciona con `startx -- -config /etc/X11/xorg.nvidia.conf`
*   Para que su monitor DP aparezca con la resolución correcta en la pantalla VIRTUAL puede que tenga que editar la sección Monitor del archivo `/etc/xorg.nvidia.conf`. Dado que este es un trabajo extra, podría intentar continuar con el archivo generado automáticamente. Vuelva a este paso de las instrucciones si encuentra que la resolución de la pantalla VIRTUAL, como se muestra por xrandr, no es la correcta.
    *   Primero tiene que generar un Modeline. Puede utilizar la herramienta [amlc](http://amlc.berlios.de/), el cual generará un Modeline introduciendo algunos parámetros básicos.

	Ejemplo: Monitor de 24" de 1920x1080

	Iniciar la utilidad con `amlc -c`

```
Monitor Identifier: Samsung 2494
Aspect Ratio: 2
physical size[cm]: 60
Ideal refresh rate, in Hz: 60
min HSync, kHz: 40
max HSync, kHz: 90
min VSync, Hz: 50
max VSync, Hz: 70
max pixel Clock, MHz: 400
```

Esta es la sección Monitor que `amlc` genera para esta entrada:

```
Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494
```

Cambie su archivo `xorg.nvidia.conf` para incluir esta sección Monitor. También puede recortar su archivo de forma que solo contenga las secciones ServerLayout, Monitor, Device y Screen. He aquí un archivo de referencia:

 `/etc/X11/xorg.nvidia.conf` 
```
Section "ServerLayout"
        Identifier     "X.org Nvidia DP"
        Screen      0  "Screen0" 0 0
        InputDevice    "Mouse0" "CorePointer"
        InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

Section "Device"
        Identifier  "DiscreteNvidia"
        Driver      "nvidia"
        BusID       "PCI:1:0:0"
EndSection

Section "Screen"
        Identifier "Screen0"
        Device     "DiscreteNvidia"
        Monitor    "Samsung 2494"
        SubSection "Display"
                Viewport   0 0
                Depth     24
        EndSubSection
EndSection

```

*   Conecte los dos monitores externos e inicie X (con startx). Mire el archivo `/var/log/Xorg.0.log`. Compruebe que el monitor VGA se detecta con las modalidades correctas. También debería ver una salida VIRTUAL mostrada con una modalidad propia.
*   Ejecute `xrandr` y las tres pantallas deberían aparecer allí, junto con las modalidades soportadas.
*   Si el listado Modelines para la pantalla VIRTUAL no tiene la resolución nativa de los monitores, anote el nombre de la salida exacta. Para este ejemplo es `VIRTUAL1`. A continuación, echaremos un vistazo de nuevo al archivo Xorg.0.log. Debe verse el mensaje: "Output VIRTUAL1 has no monitor section" (*«La salida VIRTUAL1 no tiene la sección del monitor»*). Vamos a cambiar esto poniendo un archivo con la necesaria sección Monitor en `/etc/X11/xorg.conf.d`. Salimos y reiniciamos X seguidamente.

 `/etc/X11/xorg.conf.d/20-monitor_samsung.conf` 
```
Section "Monitor"
    Identifier     "VIRTUAL1"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

```

*   Cambie a la tarjeta NVIDIA ejecutando: `sudo tee /proc/acpi/bbswitch <<< ON`.
*   Comience otro servidor X para el monitor conectado a DisplayPort: `sudo optirun true`.
*   Compruebe el registro del segundo servidor X en `/var/log/Xorg.8.log`.
*   Ejecute xrandr para configurar la pantalla VIRTUAL con el tamaño y la ubicación correcta, por ejemplo: `xrandr --output VGA1 --auto --rotate normal --pos 0x0 --output VIRTUAL1 --mode 1920x1080 --right-of VGA1 --output LVDS1 --auto --rotate normal --right-of VIRTUAL1`.
*   Tome nota de la posición de la pantalla VIRTUAL en la lista de salidas como se muestra por xrandr. El conteo comienza por cero, es decir, si es la tercera pantalla la que se muestra, se especificaría `-x 2` como parámetro para `screenclone`.
*   Clonar el contenido de la pantalla VIRTUAL en el servidor X creado por bumblebee,que está conectado al monitor a través de DisplayPort y del chip de NVIDIA:

	`screenclone -d :8 -x 2`

Eso es todo, las tres pantallas deberían estar en funcionamiento ahora.

## Cambiar entre tarjeta dedicada e integrada como Windows

En Windows, la forma en que funciona Optimus con NVIDIA se basa en la existencia de una lista blanca de aplicaciones las cuales demandan Optimus, y se pueden agregar aplicaciones a dicha lista blanca, según se necesite. Al iniciar la aplicación, esto determina automáticamente qué tarjeta usar.

Para imitar este comportamiento en Linux, es posible utilizar [libgl-switcheroo-git](https://aur.archlinux.org/packages/libgl-switcheroo-git/). Después de instalarlo, puede agregar lo siguiente en el archivo .xprofile.

 `~/.xprofile` 
```
mkdir -p /tmp/libgl-switcheroo-$USER/fs
gtkglswitch &
libgl-switcheroo /tmp/libgl-switcheroo-$USER/fs &
```

Para permitir esto, debe agregar lo que sigue abajo para la shell que tiene la intención de lanzar las aplicaciones (o simplemente agréguelo al archivo .xprofile):

```
export LD_LIBRARY_PATH=/tmp/libgl-switcheroo-$USER/fs/\$LIB${LD_LIBRARY_PATH+:}$LD_LIBRARY_PATH

```

Una vez hecho esto, cualquier aplicación que se inicie desde esta shell abrirá una ventana GTK+ preguntando cuál es la tarjeta en la que desea ejecutarla (también se puede añadir una aplicación a la lista blanca en la configuración). La configuración se encuentra en `$XDG_CONFIG_HOME/libgl-switcheroo.conf`, normalmente `~/.config/libgl-switcheroo.conf`

## CUDA sin Bumblebee

Esto no está bien documentado, pero no es necesario que Bumblebee utilice CUDA y pueda funcionar incluso en máquinas donde optirun falla. Para una guía sobre cómo conseguir que funcione con el Lenovo IdeaPad Y580 (que utiliza la GeForce 660m), consulte: [Lenovo IdeaPad Y580#NVIDIA_Card](/index.php/Lenovo_IdeaPad_Y580#NVIDIA_Card "Lenovo IdeaPad Y580"). Estas instrucciones son muy probable que se adapten a otras máquinas.

## Solución de problemas

**Nota:** Por favor, informe de los errores con el *trazador GitHub* del [Proyecto-Bumblebee](https://github.com/Bumblebee-Project/Bumblebee), como se describe en su [wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Reporting-Issues).

### [VGL] ERROR: Could not open display :8

Hay un problema conocido con algunas aplicaciones que vienen lanzadas con wine que se bifurcan y matan el proceso padre sin hacer el seguimiento del problema (por ejemplo, la sesión libre del juego en línea "Runes of Magic")

Este es un problema conocido con VirtualGL. A partir de bumblebee 3.1, siempre y cuando lo tenga instalado, puede utilizar Primus como su render bridge:

```
$optirun -b primus wine <programa de windows>.exe

```

Si esto no funciona, una solución para este problema puede ser:

```
$ optirun bash
$ optirun wine <programa de windows>.exe

```

Si está utilizando el controlador de NVIDIA, una solución para este problema es editar `/etc/bumblebee/xorg.conf.nvidia` y cambiar la opción `ConnectedMonitor` en `CRT-0`.

### [ERROR]Cannot access secondary GPU

#### Ningún dispositivo detectado

En algunos casos, la ejecución de optirun devuelve el siguiente error:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) No devices detected.
[ERROR]Aborting because fallback start is disabled.

```

En este caso, será necesario mover el archivo `/etc/X11/xorg.conf.d/20-intel.conf` a otro lugar. Reinicie el demonio bumblebeed y el error no debería presentarse más.

Podría ser también necesario comentar la línea referente al driver en el archivo `/etc/X11/xorg.conf.d/10-monitor.conf`.

Si está utilizando el controlador nouveau, podría intentar cambiar al controlador de nVidia.

Puede que tenga que definir la tarjeta nvidia en algún lugar (por ejemplo, en el archivo `/etc/X11/xorg.conf.d`), y recuerde cambiar el BusID utilizando lspci.

```
Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection

```

#### NVIDIA(0): Failed to assign any connected display devices to X screen 0

Si la salida de la consola es:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) NVIDIA(0): Failed to assign any connected display devices to X screen 0
[ERROR]Aborting because fallback start is disabled.

```

Puede cambiar esta línea en `/etc/bumblebee/xorg.conf.nvidia`:

```
Option "ConnectedMonitor" "DFP"

```

a

```
Option "ConnectedMonitor" "CRT"

```

### ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored.

Probablemente quiera comenzar una aplicación de 32-bits con bumblebee en un sistema x64\. Instale [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) o el más rápido en rendimiento de Primus, [primus-git](https://aur.archlinux.org/packages/primus-git/), de [AUR](https://aur.archlinux.org/). Recuerde usar `primusrun` con Primus.

### Fatal IO error 11 (Recurso temporalmente no disponible) en el servidor X

Cambie `KeepUnusedXServer` en `/etc/bumblebee/bumblebee.conf` de `false` a `true`. Bumblebee no será capaz de reconocer los programas ejecutados en segundo plano.

### Vídeo rasgado

El problema del lagrimeo en el vídeo es poco común utilizando Bumblebee. Para solucionarlo, necesita habilitar vsync. Debe venir activado por defecto en la tarjeta Intel, pero verifíquelo a partir de los registros de Xorg. Para comprobar si está o no habilitado para nvidia, ejecute:

 `$ optirun nvidia-settings -c :8 ` 

Las entradas `X Server XVideo Settings -> Sync to VBlank` y `OpenGL Settings -> Sync to VBlank` deben estar también habilitadas. La tarjeta Intel tiene, en general, menos problemas de tearing, de modo que puede ser buena idea utilizarla para la reproducción de vídeo. En particular utilizando VA-API para la decodificación de vídeo (por ejemplo, `mplayer-vaapi` y con el parámetro `-vsync`).

Consulte el artículo [Intel](/index.php/Intel#Video_tearing "Intel") sobre cómo resolver el problema de tearing en la tarjeta Intel.

Si todavía no está resuelto, trate de desactivar la compositing de su entorno de escritorio. Como última solución, pruebe también deshabilitar el triple buffering.

### Bumblebee no puede conectarse al socket

Podemos obtener algo como esto:

 `$ optirun glxspheres` 
```
[ 1648.179533] [ERROR]You've no permission to communicate with the Bumblebee daemon. Try adding yourself to the 'bumblebee' group
[ 1648.179628] [ERROR]Could not connect to bumblebee daemon - is it running?

```

Si ya estamos en el grupo `bumblebee` (`$ groups | grep bumblebee`), puede intentar [eliminar el socket](https://bbs.archlinux.org/viewtopic.php?pid=1178729#p1178729) `/var/run/bumblebeed.socket`.

## Véase también

*   [Bumblebee Project repository](http://www.bumblebee-project.org)
*   [Bumblebee Project Wiki](http://wiki.bumblebee-project.org/)
*   [Bumblebee Project bbswitch repository](https://github.com/Bumblebee-Project/bbswitch)

Puede unirse al canal #bumblebee en freenode.net