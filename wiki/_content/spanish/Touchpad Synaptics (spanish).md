Este artículo detalla el proceso de instalación y configuración de ***Synaptics input driver*** para los touchpads Synaptics (y ALPS) que se encuentra en la mayoría de portátiles.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Opciones de uso más frecuentes](#Opciones_de_uso_m.C3.A1s_frecuentes)
    *   [2.2 Otras opciones](#Otras_opciones)
    *   [2.3 GNOME/Cinnamon](#GNOME.2FCinnamon)
    *   [2.4 MATE](#MATE)
    *   [2.5 Configuración sobre la marcha](#Configuraci.C3.B3n_sobre_la_marcha)
        *   [2.5.1 Herramientas de consola](#Herramientas_de_consola)
        *   [2.5.2 Herramientas gráficas](#Herramientas_gr.C3.A1ficas)
*   [3 Configuración avanzada](#Configuraci.C3.B3n_avanzada)
    *   [3.1 Usar xinput para determinar las capacidades del panel táctil](#Usar_xinput_para_determinar_las_capacidades_del_panel_t.C3.A1ctil)
    *   [3.2 Synclient](#Synclient)
    *   [3.3 evtest](#evtest)
    *   [3.4 Desplazamiento circular](#Desplazamiento_circular)
    *   [3.5 Desplazamiento natural](#Desplazamiento_natural)
    *   [3.6 Software para intercambiar](#Software_para_intercambiar)
    *   [3.7 Desactivar el panel táctil al escribir](#Desactivar_el_panel_t.C3.A1ctil_al_escribir)
        *   [3.7.1 Usar la detección automática de la palma](#Usar_la_detecci.C3.B3n_autom.C3.A1tica_de_la_palma)
        *   [3.7.2 Usar .xinitrc](#Usar_.xinitrc)
        *   [3.7.3 Usar un gestor de inicio](#Usar_un_gestor_de_inicio)
    *   [3.8 Desactivar el panel táctil cuando se detecta un ratón externo](#Desactivar_el_panel_t.C3.A1ctil_cuando_se_detecta_un_rat.C3.B3n_externo)
*   [4 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [4.1 xorg.conf.d/50-synaptics.conf no parece aplicarse en GNOME y MATE](#xorg.conf.d.2F50-synaptics.conf_no_parece_aplicarse_en_GNOME_y_MATE)
    *   [4.2 Paneles táctiles ALPS](#Paneles_t.C3.A1ctiles_ALPS)
    *   [4.3 El panel táctil no funciona, Xorg.0.log muestra «Query no Synaptics: 6003C8»](#El_panel_t.C3.A1ctil_no_funciona.2C_Xorg.0.log_muestra_.C2.ABQuery_no_Synaptics:_6003C8.C2.BB)
    *   [4.4 Panel táctil detectado como ratón «PS/2 Generic» o «Logitech PS/2»](#Panel_t.C3.A1ctil_detectado_como_rat.C3.B3n_.C2.ABPS.2F2_Generic.C2.BB_o_.C2.ABLogitech_PS.2F2.C2.BB)
    *   [4.5 Habilidades especiales de synaptics que no funcionan (multitoque, desplazamiento, etc.)](#Habilidades_especiales_de_synaptics_que_no_funcionan_.28multitoque.2C_desplazamiento.2C_etc..29)
    *   [4.6 El cursor salta](#El_cursor_salta)
    *   [4.7 El dispositivo touchpad no se encuentra en /dev/input/*](#El_dispositivo_touchpad_no_se_encuentra_en_.2Fdev.2Finput.2F.2A)
    *   [4.8 Firefox y eventos especiales para el panel táctil](#Firefox_y_eventos_especiales_para_el_panel_t.C3.A1ctil)
    *   [4.9 Opera: problemas de desplazamiento horizontal](#Opera:_problemas_de_desplazamiento_horizontal)
    *   [4.10 Desplazamiento y acciones múltiples con Synaptics en portátiles LG](#Desplazamiento_y_acciones_m.C3.BAltiples_con_Synaptics_en_port.C3.A1tiles_LG)
    *   [4.11 Otros problemas con ratones externos](#Otros_problemas_con_ratones_externos)
    *   [4.12 Problemas de sincronización del panel táctil](#Problemas_de_sincronizaci.C3.B3n_del_panel_t.C3.A1ctil)
    *   [4.13 Retardo entre la presión al pulsar y el clic efectivo](#Retardo_entre_la_presi.C3.B3n_al_pulsar_y_el_clic_efectivo)
    *   [4.14 Xorg.log.0 muestra que el touchpad synaptics SynPS/2 no puede asociarse a los eventos del dispositivo, errno=16](#Xorg.log.0_muestra_que_el_touchpad_synaptics_SynPS.2F2_no_puede_asociarse_a_los_eventos_del_dispositivo.2C_errno.3D16)
    *   [4.15 Synaptics pierde la detección del multitoque después de reiniciar desde Windows](#Synaptics_pierde_la_detecci.C3.B3n_del_multitoque_despu.C3.A9s_de_reiniciar_desde_Windows)
    *   [4.16 Panel táctil sin botones (o ClickPads)](#Panel_t.C3.A1ctil_sin_botones_.28o_ClickPads.29)
    *   [4.17 Panel táctil detectado como ratón (paneles táctiles elantech)](#Panel_t.C3.A1ctil_detectado_como_rat.C3.B3n_.28paneles_t.C3.A1ctiles_elantech.29)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

El controlador Synaptics puede ser [instalado](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") con el paquete [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics), disponible en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)")

## Configuración

El método principal de configuración del touchpad (en adelante, *«panel táctil»*), es a través de un archivo de configuración del servidor [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"). Después de la instalación de `xf86-input-synaptics`, se crea un archivo de configuración predefinido en `/etc/X11/xorg.conf.d/50-synaptics.conf`.

Se puede editar este archivo para configurar las diversas opciones disponibles del controlador. Para obtener una lista completa de todas las opciones disponibles, los usuarios deben consultar las páginas del manual de synaptics:

 `$ man synaptics` 

### Opciones de uso más frecuentes

El controlador Synaptic permite ser modificado con un amplio número de opciones. Tenga en cuenta que todas estas opciones simplemente se añaden en el archivo de configuración principal `/etc/X11/xorg.conf.d/50-synaptics.conf`, como se muestra en el siguiente ejemplo de archivo de configuración, en el que se han activado los desplazamientos verticales, horizontales y circulares:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
 Section "InputClass"
       Identifier "touchpad"
       Driver "synaptics"
       MatchIsTouchpad "on"
              Option "TapButton1"            "1"
              Option "TapButton2"            "2"
              Option "TapButton3"            "3"
              Option "VertEdgeScroll"        "on"
              Option "VertTwoFingerScroll"   "on"
              Option "HorizEdgeScroll"       "on"
              Option "HorizTwoFingerScroll"  "on"
              Option "CircularScrolling"     "on"
              Option "CircScrollTrigger"     "2"
              Option "EmulateTwoFingerMinZ"  "40"
              Option "EmulateTwoFingerMinW"  "8"
              Option "CoastingSpeed"         "0"
              ...
 EndSection

```

	**TapButton1**

	(entero) determina qué botón del ratón es informado, excluyendo el área de la esquina del panel táctil, al tocar con un dedo.

	**TapButton2**

	(entero) determina qué botón del ratón es informado, excluyendo el área de la esquina del panel táctil, al tocar con dos dedos.

	**TapButton3**

	(entero) determina qué botón del ratón es informado, excluyendo el área de la esquina del panel táctil, al tocar con tres dedos.

	**RBCornerButton**

	(entero) determina qué botón del ratón se informa en el ángulo inferior derecho del panel táctil, al tocar con un dedo (utilice el parámetro `Option "RBCornerButton" "3"`. para lograr un comportamiento al estilo Ubuntu del botón derecho del ratón en la esquina inferior derecha del panel táctil).

	**RTCornerButton**

	(entero) igual que el anterior, pero para la esquina superior derecha, un toque del dedo.

	**VertEdgeScroll**

	(booleano) permite el desplazamiento vertical mientras se arrastra el dedo a través del borde derecho del panel táctil.

	**HorizEdgeScroll**

	(booleano) permite el desplazamiento horizontal mientras se arrastra el dedo a través del borde inferior del panel táctil.

	**VertTwoFingerScroll**

	(booleano) permite el desplazamiento vertical con dos dedos.

	**HorizTwoFingerScroll**

	(booleano) permite el desplazamiento horizontal con dos dedos.

	**EmulateTwoFingerMinZ/W**

	(entero) juegue con este valor para establecer la precisión del desplazamiento con dos dedos.

He aquí [un ejemplo](/index.php?title=Touchpad_Synaptics/10-synaptics.conf_example&action=edit&redlink=1 "Touchpad Synaptics/10-synaptics.conf example (page does not exist)") con una breve descripción de todas las opciones. Como de costumbre, los ajustes pueden variar según el ordenador. Se le recomienda que descubra sus propias opciones con [synclient](/index.php/Touchpad_Synaptics#Fine-tuning_with_synclient "Touchpad Synaptics").

**Nota:**

*   Si resulta que su mano roza con frecuencia su panel táctil, causando la activación de la opción TapButton2 (que copiará más de la cuenta desde el portapapeles), y no le importa perder la funcionalidad del toque de dos dedos, ajuste `TapButton2` a 0.
*   Las versiones recientes incluyen una función de «inercia», activada por defecto, que puede tener el efecto no deseado de seguir casi cualquier desplazamiento hasta el toque o el clic siguiente, incluso si ya no están tocando el panel táctil. Esto significa que para desplazarse un poco, debe iniciar el desplazamiento tocando (utilizando el borde, o una opción multitoque) y luego, casi de inmediato, volver a tocar el panel táctil, de lo contrario el desplazamiento continuará sin detenerse. Si desea evitar este efecto, establezca el valor `0` a la opción `CoastingSpeed`.

### Otras opciones

	**VertScrollDelta** y **HorizScrollDelta**

	(entero) configura la velocidad de desplazamiento, pero de un modo contra-intuitivo, dado que valores más altos producen una mayor precisión pero un desplazamiento más lento. Valores negativos hacen el desplazamiento más natural como en OS X.

	**SHMConfig**

	(booleano) alterna el encendido/apagado de la memoria compartida para su depuración en tiempo de ejecución. Esta opción no tiene un efecto adicional en la configuración del tiempo de ejecución y solo es útil para la depuración de eventos del hardware.

### GNOME/Cinnamon

Los usuarios de [GNOME](/index.php/GNOME "GNOME") pueden tener que modificar su configuración, ya que, por defecto, está desactivado tocar para hacer clic, el desplazamiento horizontal y no permite deshabilitar el panel táctil mientras se escribe.

Para cambiar esta configuración en **Gnome 2**:

1.  Ejecute `gconf-editor`
2.  Edite las claves en el directorio `/desktop/gnome/peripherals/touchpad/` .

Para cambiar esta configuración en **Gnome 3**:

1.  Abra *Configuración del sistema*.
2.  Seleccione *Ratón y «touchpad»*.
3.  Cambie la configuración del *Touchpad*.

Para cambiar esta configuración en **Cinnamon**:

1.  Abra *Configuración del sistema*.
2.  Seleccione *Ratón y «touchpad»*.
3.  Cambie la configuración del *Touchpad*.

El demonio de configuración de gnome puede sobreescribir la configuración existente (por ejemplo, las que figuran en `xorg.conf.d`) para las cuales no existe un equivalente en cualquiera de las utilidades gráficas de configuración. Es posible hacer que gnome no modifique la configuración del ratón en absoluto, haciendo lo siguiente:

1.  Ejecute `dconf-editor`
2.  Edite `/org/gnome/settings-daemon/plugins/mouse/` (o `/org/cinnamon/settings-daemon/plugins/mouse/` para cinnamon)

1.  Desmarque el valor **activo**.

Ahora se respetará la configuración existente para synaptics.

**Recordatorio**: Ya que, al ejecutar dconf-editor o gconf-editor, Gnome funciona con relación a ese usuario, esto debe hacerse en la sesión del usuario en curso. Repita este procedimiento para cada usuario que tenga para su equipo.

### MATE

Al igual que con [GNOME](/index.php/GNOME "GNOME"), es posible configurar el proyecto MATE para manejar el panel táctil:

1.  Ejecute `mateconf-editor`
2.  Edite las claves en la carpeta `desktop/mate/peripherals/touchpad/`.

Para evitar que el demonio de configuración de Mate redefina los valores existente, haga lo siguiente:

1.  Ejecute `mateconf-editor`
2.  Edite `/apps/mate_settings_daemon/plugins/mouse/`
3.  Desmarque el valor **active**.

### Configuración sobre la marcha

Junto al método tradicional de configuración, el controlador Synaptics también soporta la configuración al vuelo. Esto significa que los usuarios pueden configurar ciertas opciones a través de una aplicación de software, la cual aplica estas opciones inmediatamente sin necesidad de reiniciar X. Esto es útil para probar las opciones de configuración antes de incluirlos en el archivo de configuración.

**Advertencia:** La configuración al vuelo (*«on-the-fly»*) no es permanente y no se mantendrá después de un reinicio del sistema, ni después de suspender/reanudar o reiniciar udev. Esto solo se debe utilizar para funciones de prueba, afinamiento o configuración del script.

#### Herramientas de consola

*   **[Synclient](/index.php/Touchpad_Synaptics#Synclient "Touchpad Synaptics") (Recomendado)** — utilidad de línea de órdenes para configurar y buscar ajustes del controlador Synaptics en un sistema *live*, la herramienta es desarrollada por los mantenedores del controlador Synaptics y se proporciona con el controlador synaptics.

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)

*   **[xinput](/index.php/Touchpad_Synaptics#xinput "Touchpad Synaptics")** — una pequeña herramienta polivalente con interfaz de línea de órdenes (CLI) para configurar dispositivos.

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput)

#### Herramientas gráficas

**Advertencia:** Algunas de las herramientas que figuran a continuación todavía requieren el obsoleto modo `SHMConfig`, y no va a funcionar bien con el controlador xf86-input-synaptics. Por favor, elimine las herramientas obsoletas de la lista.

*   **GPointing Device Settings** — proporciona una configuración gráfica sobre la marcha para varios dispositivos punteadores conectados al sistema, incluyendo el panel táctil synaptics. Esta aplicación sustituye a GSynaptics, como la herramienta principal para la configuración gráfica del panel táctil a través del controlador synaptics

	[http://live.gnome.org/GPointingDeviceSettings](http://live.gnome.org/GPointingDeviceSettings) || [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings)

**Nota:** Para que GPointingDeviceSettings trabaje junto con los paneles táctiles Synaptics, debe tener instalados los paquetes [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) y [libsynaptics](https://www.archlinux.org/packages/?name=libsynaptics)

*   **Synaptiks** — herramienta de configuración y gestión de panel táctil para [KDE](/index.php/KDE "KDE"). Se proporciona un módulo de configuración del sistema para establecer las funciones básicas y avanzadas del panel táctil. Además viene con una pequeña aplicación en la bandeja del sistema que puede apagar el panel táctil automáticamente, en el momento en que un ratón externo se active o al teclear.

	[http://synaptiks.lunaryorn.de](http://synaptiks.lunaryorn.de) || [synaptiks](https://aur.archlinux.org/packages/synaptiks/)

## Configuración avanzada

### Usar xinput para determinar las capacidades del panel táctil

Dependiendo del modelo, el panel táctil Synaptics puede o no tener las siguientes características. Hay que determinar qué capacidades del hardware son compatibles con `xinput`.

*   Botones físicos izquierdo, central o derecho
*   Detección de dos dedos
*   Detección de tres dedos
*   Resolución configurable

En primer lugar, busque el nombre del panel táctil:

 `$ xinput -list` 

Ahora puede usar `xinput` para encontrar las capacidades del panel táctil:

```
$ xinput list-props "SynPS/2 Synaptics TouchPad" | grep Capabilities

      Synaptics Capabillities (309):  1, 0, 1, 0, 0, 1, 1

```

De izquierda a derecha, esto muestra:

*   (1) el dispositivo tiene un botón izquierdo físico
*   (0) el dispositivo no tiene un botón central físico
*   (1) el dispositivo tiene un botón físico derecho
*   (0) el dispositivo no es compatible con la detección de dos dedos (*two-finger*)
*   (0) el dispositivo no es compatible con la detección de tres dedos (*three-finger*)
*   (1) el dispositivo puede configurar la resolución vertical
*   (1) el dispositivo puede configurar la resolución horizontal

Use `xinput list-props "SynPS/2 Synaptics TouchPad"` para listar todas las propiedades del dispositivo.

### Synclient

Synclient puede configurar todas las opciones disponibles, como se documenta en `$ man synaptics`. Una lista completa de los ajustes actuales puede obtenerse con:

 `$ synclient -l` 

Cada opción de configuración enumerada se puede controlar a través de synclient, por ejemplo:

```
 $ synclient PalmDetect=1 (para habilitar la detección de la palma)
 $ synclient TapButton1=1 (para controlar los eventos de pulsación)
 $ synclient TouchpadOff=1 (para deshabilitar el panel táctil)

```

Después de haber probado con éxito las opciones a través de synclient, puede hacer que estos cambios sean permanentes, agregándolos a `/etc/X11/xorg.conf.d/50-synaptics.conf`.

### evtest

La herramienta [evtest](/index.php/Evdev "Evdev") permite mostrar la presión y la colocación del dedo en el panel táctil en tiempo real, lo que permite un mayor refinamiento de la configuración predeterminada de Synaptics.Puede iniciar el monitor evtest con la siguiente orden:

 `$ evtest /dev/input/eventX` 

Donde 'X' indica el ID del touchpad. Se puede encontrar buscando en la salida de `$ cat /proc/bus/input/devices`.

evtest necesita acceso exclusivo al dispositivo, lo que significa que no se puede ejecutar junto con una instancia del servidor X. Puede matar el servidor X o ejecutar evtest en un terminal virtual diferente (por ejemplo, pulsando Ctrl+Alt+2).

### Desplazamiento circular

El desplazamiento circular es una característica que Synaptics ofrece y que recuerda mucho el comportamiento de los iPod. En lugar de (o junto con) desplazamiento horizontal o vertical, puede desplazarse circularmente. Algunos usuarios encuentran esto más rápido y más preciso. Para habilitar el desplazamiento circular, agregue las siguientes opciones en la sección device del archivo del panel táctil en `/etc/X11/xorg.conf.d/50-synaptics.conf`:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
 Section "InputClass"
         ...
         Option      "CircularScrolling"          "on"
         Option      "CircScrollTrigger"          "0"
         ...
 EndSection

```

La opción **CircScrollTrigger** puede tener uno de los siguientes valores, a fin de determinar de qué borde debe comenzar el desplazamiento circular:

```
0 Todos los bordes
1 Borde superior
2 Esquina superior derecha
3 Borde derecho
4 Esquina inferior derecha
5 Borde inferior
6 Esquina inferior izquierda
7 Borde izquierdo
8 Esquina superior izquierda

```

Puede ser útil especificar un valor diferente de cero si desea utilizar el desplazamiento circular junto con el desplazamiento horizontal y/o vertical. Si lo hace, el tipo de desplazamiento será determinado del lado del cual se parte.

Para desplazarse rápidamente, dibuje pequeños círculos en el centro de su panel táctil. Para desplazarse lentamente y con precisión, trace círculos grandes.

### Desplazamiento natural

Es posible activar el desplazamiento natural a través de Synaptics. Solo tenemos que utilizar valores negativos para `VertScrollDelta` y `HorizScrollDelta` como sigue:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
 Section "InputClass"
         ...
         Option      "VertScrollDelta"          "-111"
         Option      "HorizScrollDelta"         "-111"
         ...
 EndSection

```

### Software para intercambiar

Puede que le resulte útil disponer de un software que le permita alternar la activación o desactivación del panel táctil, sobre todo si este es muy sensible y si escribe con mucha frecuencia. Véase también cómo [desactivar el panel táctil al detectar el ratón externo](#Desactivar_el_panel_t.C3.A1ctil_cuando_se_detecta_un_mouse_externo), dado que esta última puede ser una mejor solución, en cualquier caso es una cuestión de elección. La ventaja aquí es que se tiene el control, mientras que la otra solución utiliza un demonio para determinar cuándo apagar el panel táctil.

Si va a probar este método, debe instalar [xbindkeys](/index.php/Xbindkeys "Xbindkeys"), en el caso de no disponer aún de un software que gestione la combinación de teclas.

A continuación, guarde este script en algo como `/sbin/trackpad-toggle.sh`:

 `/sbin/trackpad-toggle.sh` 
```
 #!/bin/bash

 synclient TouchpadOff=$(synclient -l | grep -c 'TouchpadOff.*=.*0')

```

Y por último, añada una combinación de teclas para usar el script. Lo mejor es iniciarlo con xbindkeys así, (en el archivo `~/.xbindkeysrc`):

 `~/.xbindkeysrc` 
```
 "/sbin/trackpad-toggle.sh"
     m:0x5 + c:65
     Control+Shift + space

```

Ahora, (re)inicie `xbindkeys` y al teclear `Ctrl`+`Shift`+`Espacio` ¡alternará su panel táctil entre activo/inactivo!

Por supuesto, se podría utilizar cualquier otro software de combinación de teclas, como los proporcionados por Xfce4 y GNOME.

### Desactivar el panel táctil al escribir

#### Usar la detección automática de la palma

Ante todo, debe probar si funciona correctamente para su trackpad y si la configuración es correcta:

```
$ synclient PalmDetect=1

```

A continuación, compruebe la escritura. Puede ajustar la detección de:

```
$ synclient PalmMinWidth=

```

que es el ancho del área que su mano toca, y

```
$ synclient PalmMinZ=

```

que es la distancia Z mínima en la que se realiza la detección.

Una vez que haya encontrado la configuración correcta, guárdela en `/etc/X11/xorg.conf.d/50-synaptics.conf` así:

```
#synclient PalmDetect=1
Option "PalmDetect" "1"
#synclient PalmMinWidth=10
Option "PalmMinWidth" "10"
#synclient PalmMinZ=200
Option "PalmMinZ" "200"
```

#### Usar .xinitrc

Para que el panel táctil se desactive automáticamente cuando se comienza a escribir, añada la línea de abajo a su archivo `~/.xinitrc` antes de ejecutar el gestor de ventanas (en el caso de que no use un administrador de inicio de sesión):

 `$ syndaemon -t -k -i 2 -d &` 

	**-i 2**

	establece el tiempo de inactividad a 2 segundos. El tiempo de inactividad especifica cuántos segundos debe esperar después de la última pulsación de tecla antes de habilitar el panel táctil de nuevo.

	**-t**

	dice al demonio que no desactive el movimiento del ratón mientras se escribe, sino solo deshabilitar el toque y el desplazamiento.

	**k**

	dice al demonio que ignore las teclas modificadoras cuando se monitorea la actividad del teclado (permite, por ejemplo, Ctrl + clic izquierdo).

	**d**

	comienza como un demonio, en segundo plano.

Hay más detalles están disponibles en las páginas del manual:

 `$ man syndaemon` 

Si está utilizando un gestor de inicio de sesión, tendrá que especificar esta orden donde su entorno de escritorio le permite hacerlo.

#### Usar un gestor de inicio

La opción «-d» es necesaria para iniciar syndaemon como un proceso en segundo plano para obtener instrucciones del Login.

**Para GNOME: (GDM)**

Para activar syndaemon es necesario utilizar el programa de preferencias para el inicio de las aplicaciones de Gnome . Inicie sesión para Gnome y vaya a **Sistema> Preferencias> Aplicaciones de Inicio**. En la pestaña Programas de inicio, haga clic en el botón **Añadir**. Denomine como quiera al programa de inicio e introduzca cualquier comentario que desee (o deje este campo en blanco). En el campo para «comando» añada:

```
En Gnome 3 ejecute *gnome-session-properties* (en un terminal, como usuario root) para acceder a las aplicaciones de inicio.

```
 `$ syndaemon -t -k -i 2 -d &` 

Cuando haya terminado, pulse el botón **Añadir** para **agregar el programa al iniciar**. Asegúrese de que la casilla de verificación, situada junto al programa de arranque, ha sido creada, en la lista de nuevos programas de inicio. Cierre la ventana de las **Preferencias de Aplicaciones de Inicio** y listo.

**Para KDE: (KDM)**

Vaya a **Ajustes del sistema> Inicio y apagado> Autoiniciar**, luego pulse en **Agregar programa**, y escriba:

 ` syndaemon -t -k -i 2 -d &` 

A continuación, seleccione **Ejecutar en terminal**.

### Desactivar el panel táctil cuando se detecta un ratón externo

Con la ayuda de [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)"), es posible deshabilitar automáticamente el panel táctil, para el caso de que un ratón externo se conecte. Para ello, agregue las siguientes reglas udev al archivo siguiente:

 `/etc/udev/rules.d/01-touchpad.rules` 
```
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="add", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/*username*/.Xauthority", RUN+="/usr/bin/synclient TouchpadOff=1"
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="remove", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/*username*/.Xauthority", RUN+="/usr/bin/synclient TouchpadOff=0"
```

GDM conserva los archivos Xauthority en `/var/run/gdm` en un directorio con nombre aleatorio. De modo que las reglas udev se mostrarán de esta forma:

 `/etc/udev/rules.d/01-touchpad.rules` 
```
SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ACTION=="add", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=1"
SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ACTION=="remove", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=0"
```

Sin embargo, las reglas udev pueden entrar en conflicto con [syndaemon](#Usar_.xinitrc). Para desactivar el panel táctil y, al mismo tiempo, terminar syndaemon, puede usar una regla como esta:

 `/etc/udev/rules.d/01-touchpad.rules`  `SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ACTION=="add", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="$result/database", RUN+="/bin/sh -c '/usr/bin/synclient TouchpadOff=1 ; sleep 1; /bin/killall syndaemon; '"` 

Si *syndaemon* se inicia automáticamente con la omisión del ratón, entonces se puede combinar esto con la anterior regla de desactivación. Si se necesita para iniciar el propio *syndaemon*, entonces altere adecuadamente la orden con las opciones de *syndaemon* preferidas.

## Solución de problemas

### xorg.conf.d/50-synaptics.conf no parece aplicarse en GNOME y MATE

[GNOME](/index.php/GNOME "GNOME") y [MATE](/index.php/MATE "MATE"), de forma predeterminada, sobrescribe varias opciones para su panel táctil. Esto incluye características configurables para los que no hay ajustes gráficos en el panel de control del sistema de GNOME. Ello puede causar que lo que aparece en `/etc/X11/xorg.conf.d/50-synaptics.conf` no se aplique. Por favor, remítase a la sección de GNOME de este artículo para evitar este comportamiento.

*   [Touchpad_Synaptics_(Español)#GNOME](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol)#GNOME "Touchpad Synaptics (Español)")

### Paneles táctiles ALPS

Para los panéles táctiles ALPS, si la configuración anterior no proporciona los resultados deseados, pruebe la siguiente configuración, en su lugar:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
  Section "ServerLayout"
   ...
   InputDevice    "USB Mouse" "CorePointer"
   InputDevice    "Touchpad"  "SendCoreEvents"
 EndSection

   Section "InputDevice"
       Identifier  "Touchpad"
   Driver  "synaptics"
   Option  "Device"                 "/dev/input/mouse0"
   Option  "Protocol"               "auto-dev"
   Option  "LeftEdge"               "130"
   Option  "RightEdge"              "840"
   Option  "TopEdge"                "130"
   Option  "BottomEdge"             "640"
   Option  "FingerLow"              "7"
   Option  "FingerHigh"             "8"
   Option  "MaxTapTime"             "180"
   Option  "MaxTapMove"             "110"
   Option  "EmulateMidButtonTime"   "75"
   Option  "VertScrollDelta"        "20"
   Option  "HorizScrollDelta"       "20"
   Option  "MinSpeed"               "0.25"
   Option  "MaxSpeed"               "0.50"
   Option  "AccelFactor"            "0.010"
   Option  "EdgeMotionMinSpeed"     "200"
   Option  "EdgeMotionMaxSpeed"     "200"
   Option  "UpDownScrolling"        "1"
   Option  "CircularScrolling"      "1"
   Option  "CircScrollDelta"        "0.1"
   Option  "CircScrollTrigger"      "2"
   Option  "SHMConfig"              "on"
   Option  "Emulate3Buttons"        "on"
 EndSection

```

### El panel táctil no funciona, Xorg.0.log muestra «Query no Synaptics: 6003C8»

Debido a la forma en que synaptic está configurado actualmente, se cargan dos instancias del módulo synaptics. Podemos reconocer esta situación, abriendo el archivo de registro de xorg (`/var/log/Xorg.0.log`) y observando esto:

 `/var/log/Xorg.0.log` 
```
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "evdev touchpad catchall"
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "touchpad catchall"

```

Observe cómo dos instancias del módulo, con nombres diferentes, se cargan. En algunos casos, esto hace que el panel táctil resulte inutilizable.

Podemos evitar esta doble carga añadiendo `MatchDevicePath "/dev/input/event *"` al archivo `/etc/X11/xorg.conf.d/50-synaptics.conf`:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
 Section "InputClass"
       Identifier      "touchpad catchall"
       Driver          "synaptics"
       MatchIsTouchpad "on"
       MatchDevicePath "/dev/input/event*"
             Option "TapButton1" "1"
             Option "TapButton2" "2"
             Option "TapButton3" "3"
 EndSection

```

Reinicie X y compruebe los registros de xorg de nuevo, el error debe desaparecer y el panel táctil debe funcionar correctamente.

Informe de error relacionado con: [FS#20830](https://bugs.archlinux.org/task/20830)

Temas relacionados con el foro:

*   [https://bbs.archlinux.org/viewtopic.php?id=104769](https://bbs.archlinux.org/viewtopic.php?id=104769)
*   [https://bbs.archlinux.org/viewtopic.php?pid=825690](https://bbs.archlinux.org/viewtopic.php?pid=825690)

### Panel táctil detectado como ratón «PS/2 Generic» o «Logitech PS/2»

Esto es causado por un [error del kernel](https://bugzilla.kernel.org/show_bug.cgi?id=27442) corregido a partir de la versión 3.3 del kernel. El panel táctil detectado erróneamente no se podía configurar por el controlador de entrada Synaptic (*«Synaptic input driver»*). Para solucionar este problema, basta con instalar el paquete [psmouse-elantech](https://aur.archlinux.org/packages/psmouse-elantech/) de [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

Entre los portátiles afectados están los siguientes modelos:

*   Acer Aspire 7750G
*   Dell Latitude e6520 (ALPS touchpad), Inspiron N5110 (ALPS GlidePoint)
*   Samsung NC110/NF210/QX310/QX410/QX510/SF310/SF410/SF510/RF410/RF510/RF710/RV515

Puede comprobar si el panel táctil se detecta correctamente ejecutando:

 `$ xinput list` 

Más información sobre el tema en [este hilo](https://bbs.archlinux.org/viewtopic.php?id=117109).

### Habilidades especiales de synaptics que no funcionan (multitoque, desplazamiento, etc.)

En algunos casos el panel táctil Synaptics solo funciona parcialmente. Características tales como desplazarse con dos dedos o el clic central con dos dedos no funcionan correctamente, incluso si dichas opciones están habilitadas en su configuración. Esto está probablemente relacionado con [el panel táctil no funciona](#El_panel_t.C3.A1ctil_no_funciona.2C_Xorg.0.log_muestra_.C2.ABQuery_no_Synaptics:_6003C8.C2.BB) antes mencionado. Se resuelve de la misma manera, evitando la doble carga del módulo.

Si impidiendo que el módulo se cargue dos veces no se soluciona el problema, pruebe comentando la opción "MatchIsTouchpad" (que ahora se incluye por defecto en la configuración de synaptics).

Si al cliquear, tanto con 2 dedos como con 3 dedos, se interpreta como un clic del botón secundario, sin que sea posible un clic medio, independientemente de la configuración, el culpable sea, probablemente, este error: [https://bugs.freedesktop.org/show_bug.cgi?id=55365](https://bugs.freedesktop.org/show_bug.cgi?id=55365)

### El cursor salta

Algunos usuarios tienen un cursor que, inexplicablemente, *salta* por toda la pantalla. En este momento no hay un parche para este problema, pero los desarrolladores son conscientes del problema y están trabajando en ello.

Otra posibilidad para explicar este comportamiento es que se están experimentando *pérdidas de IRQ* relacionadas con el controlador i8042 (este dispositivo maneja el teclado y el panel táctil de muchos ordenadores portátiles), así que tiene dos posibilidades aquí:

1.  rmmod && insmod para el módulo psmouse.
2.  agregar i8042.nomux=1 a la línea de arranque y reiniciar el equipo.

### El dispositivo touchpad no se encuentra en `/dev/input/*`

Si este problema se presenta, puede utilizar la orden que sigue para mostrar información acerca de los dispositivos de entrada:

 `$ cat /proc/bus/input/devices` 

Se busca un dispositivo de entrada que tenga el nombre "SynPS/2 Synaptics TouchPad". La sección «Handlers» de la salida muestra qué dispositivo es necesario especificar.

**Ejemplo de salida:**

 `$ cat /proc/bus/input/devices` 
```
 I: Bus=0011 Vendor=0002 Product=0007 Version=0000
 N: Name="SynPS/2 Synaptics TouchPad"
 P: Phys=isa0060/serio4/input0
 S: Sysfs=/class/input/input1
 H: Handlers=mouse0 event1
 B: EV=b
 B: KEY=6420 0 7000f 0

```

En este caso, los `Handlers` son `mouse0` y `event1`, por lo que utilizaríamos `/dev/input/**mouse0**`.

### Firefox y eventos especiales para el panel táctil

Por defecto, Firefox está configurado para realizar eventos especiales al tocar o desplazarse por ciertas zonas del panel táctil. Puede modificar la configuración de las acciones escribiendo **about: config** en la barra de direcciones de Firefox. Para modificar estas opciones, haga doble clic en la línea en cuestión, cambiando el valor «true» a «false» y viceversa.

Para evitar que Firefox efectúe el desplazamiento (hacia atrás/adelante) a través del historial del navegador, en lugar de desplazarse por la página, modifique estos ajustes como se muestran:

```
mousewheel.horizscroll.withnokey.action = 1
mousewheel.horizscroll.withnokey.sysnumlines = true

```

Para evitar que Firefox efectúe el redireccionamiento a direcciones URL formado a partir de su contenido del portapapeles al tocar la esquina superior derecha del panel táctil (o el botón central del ratón), ajuste la siguiente opción a «false»:

```
middlemouse.contentLoadURL = false

```

### Opera: problemas de desplazamiento horizontal

Igual que el anterior. Para solucionarlo, vaya a Herramientas -> Preferencias -> Avanzado -> Accesos directos. Seleccione la configuración del ratón «Opera estándar» y pulse en «Editar». En la sección «Aplicación»:

*   asigne la tecla "Button 6" al comando "Scroll left"
*   asigne la tecla "Button 7" al comando "Scroll right"

### Desplazamiento y acciones múltiples con Synaptics en portátiles LG

Estos problemas parecen estar ocurriendo en varios modelos de portátiles LG. Los síntomas incluyen: al pulsar el botón del ratón 1, Synaptics lo interpreta como un ScrollUP y un clic normal del boton 1; lo mismo ocurre con el botón 2.

El problema de desplazamiento se puede resolver insertando en `xorg.conf`:

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option "UpDownScrolling" "0"` 
**Nota:** Avertirá que esto hará que Synaptics interprete una pulsación como tres. Hay un parche escrito por Oskar Sandberg [[1]](http://www.math.chalmers.se/~ossa/linux/lg_tx_express.html) que elimina estos clics.

Al parecer, cuando se trata de compilar esta solución a la última versión de Synaptics, esta falla. La solución es usar el repositorio GIT para Synaptics[[2]](http://web.telia.com/~u89404340/touchpad/synaptics/.git).

También hay un archivo de compilación del paquete en AUR para automatizar este: [xf86-input-synaptics-lg](https://aur.archlinux.org/packages/xf86-input-synaptics-lg/).

Para construir el paquete, después de descargar el tarball y haberlo desempaquetado, ejecute:

```
$ cd synaptics-git
$ makepkg

```

### Otros problemas con ratones externos

En primer lugar, asegúrese de que la sección que describe al mouse externo contiene esta línea (o que la línea tiene este aspecto):

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option     "Device" "/dev/input/mice"` 

Si la línea "Device" es diferente, cámbiela por la anterior y pruebe reiniciando X. Si esto no soluciona el problema, defina su **touchpad** como CorePointer en el "Server Layout":

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "Touchpad" "CorePointer"` 

y defina su dispositivo externo como "SendCoreEvents":

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "USB Mouse" "SendCoreEvents"` 

por último, añada esta línea a la sección de su device externo:

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option      "SendCoreEvents"    "true"` 

Si todo lo anterior no funciona en su caso, por favor revise la sección de errores relativa a un posible bug, o busque a través de los foros para ver si alguien ha encontrado una solución mejor.

### Problemas de sincronización del panel táctil

A veces, el cursor se congela durante unos segundos o empieza a actuar por su cuenta sin ninguna razón aparente. Este comportamiento viene registrado en `/var/log/messages.log`

 `/var/log/messages.log`  `psmouse.c: TouchPad at isa0060/serio1/input0 lost synchronization, throwing 3 bytes away` 

Este problema no tiene una solución única, pero hay varias posibilidades.

*   Si utiliza escalado de frecuencia de la CPU, evite el uso del gobernador "ondemand" y utilice "performance" cuando sea posible, ya que el panel táctil puede perder la sincronización en los momentos de cambios de frecuencia de la CPU.
*   Evite el uso de un monitor de batería ACPI.
*   Intente cargar psmouse con la opción "proto=imps". Para hacer esto, añada esta línea al archivo `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf`  `options psmouse proto=imps` 

*   Pruebe con otro entorno de escritorio. Algunos usuarios informan que este problema solo se produce cuando se utiliza XFCE o GNOME, por cualquier extraña razón.

### Retardo entre la presión al pulsar y el clic efectivo

Si se experimenta un retraso entre el golpecito en el panel táctil y el clic real que se registra en el monitor, necesita habilitar FastTaps:

Para ello, se debe añadir **Option "FastTaps" "1"** a `/etc/X11/xorg.conf.d/50-synaptics.conf` de modo que quede como sigue:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
 Section "InputClass"
      Identifier "Synaptics Touchpad"
      Driver     "synaptics"
      ...
      Option     "FastTaps" "1"
      ...
 EndSection

```

### Xorg.log.0 muestra que el touchpad synaptics SynPS/2 no puede asociarse a los eventos del dispositivo, errno=16

Si está utilizando Xorg 7.4, puede recibir una advertencia como esta de `/var/log/Xorg.0.log`, ello es debido al hecho de que el controlador registra el evento del dispositivo para un uso exclusivo cuando se utiliza el protocolo de eventos de Linux 2.6\. Cuando falla, X responde con este mensaje de error.

Registrar el evento del dispositivo significa que ningún programa, ni por parte de los usuarios ni por parte del kernel, pueden ver los acontecimientos del panel táctil. Esto es deseable si el archivo de configuración de X incluye `/dev/input/mice` como un dispositivo de entrada, pero no es deseable si se quiere controlar el dispositivo desde el espacio de usuario.

Si desea controlar, añadir o modificar la variable Option "GrabEventDevice" en la sección touchpad en `/etc/X11/xorg.conf.d/50-synaptics.conf`, añada:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
...
Option "GrabEventDevice" "*boolean*"
...
```

} Esta opción entrará en vigor cuando X se reinicie, aunque también se puede cambiar mediante el uso de synclient. Al cambiar este parámetro con el programa synclient, el cambio no tendrá efecto hasta que el controlador Synaptics se desactive y vuelva a activarse. Esto se puede lograr pasando a una consola de texto y luego volver de nuevo a X.

### Synaptics pierde la detección del multitoque después de reiniciar desde Windows

Muchos controladores contienen un firmware que se carga en la memoria flash cuando se inicia el equipo. Este firmware no necesariamente se borra durante el proceso de apagado, y no siempre es compatible con los controladores de Linux. La única manera de borrar la memoria flash consiste en apagar completamente, en lugar de utilizar el reinicio. En general, se considera la mejor práctica no utilizar nunca el reinicio al cambiar entre sistemas operativos.

### Panel táctil sin botones (o ClickPads)

Algunos ordenadores portátiles tienen un tipo especial de panel táctil que tiene los botones del ratón como parte de la placa de seguimiento, en vez de ser botones externos. Por ejemplo, HP series 4500 ProBooks, ThinkPad X220 y la serie X1 de ThinkPad tienen este tipo de panel táctil. Por defecto, el área del botón se detecta como una pulsación a la izquierda, con el resultado de que el segundo botón es de hecho inutilizable y que el arrastre no va a funcionar. Anteriormente, el soporte para tales dispositivos se logró mediante el uso de parches de terceros, pero desde la versión 1.6.0 el controlador Synaptics tiene soporte multitouch nativo (usando la biblioteca *mtdev*). Tenga en cuenta que aunque el controlador registra varios toques, no hace un seguimiento de los dedos individuales (a partir de la versión 1.7.1), lo que da como resultado un comportamiento confuso al utilizar los botones físicos de un Clickpad para arrastrar y soltar, y otros gestos. Puede mirar el controlador [xf86-input-mtrack](https://aur.archlinux.org/packages/xf86-input-mtrack/) para un mejor soporte multitoque.

Para habilitar otras pulsaciones modifique la sección touchpad en `/etc/X11/xorg.conf.d/50-synaptics.conf` (o mejor, de su archivo de configuración personalizada de synaptics, el cual debe ir precedido de un número superior a 10):

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
...
Option "ClickPad"             "true"
Option "EmulateMidButtonTime" "0"
Option "SoftButtonAreas"      "50% 0 82% 0 0 0 0 0"
...

```

Estas tres opciones son la clave, la primera activa el soporte multitouch, la segunda deshabilitará la emulación de la pulsación central (no soportado para ClickPads), y la tercera se definirán las áreas de pulsación.

El formato para la opción SoftButtonAreas es (de `man 4 synaptics`):

 `RightButtonAreaLeft RightButtonAreaRight RightButtonAreaTop RightButtonAreaBottom  MiddleButtonAreaLeft MiddleButtonAreaRight MiddleButtonAreaTop MiddleButtonAreaBottom` 

El ejemplo anterior se encuentra comúnmente en la documentación o en paquetes synaptics, y lo traduce ajustando la pulsación derecha al 18% de la parte inferior del panel táctil. **No hay una pulsación central** definida. Si desea definir un botón central recuerde una pieza clave de la información del manual: **el ángulo ajustado a 0 se extiende hasta el infinito en esa dirección.**

En el ejemplo siguiente la pulsación relativa al botón derecho ocupará el 40% de la parte más a la derecha del panel táctil. Entonces procedemos a configurar el botón central para ocupar el 20% del panel táctil en un área pequeña en el centro.

```
   ...
   Option     "SoftButtonAreas"  "60% 0 82% 0 40% 59% 82% 0"
   ...

```

Se puede utilizar `synclient` para comprobar las nuevas áreas del panel táctil:

```
   $ synclient -l | grep -i ButtonArea
      RightButtonAreaLeft     = 3914
      RightButtonAreaRight    = 0
      RightButtonAreaTop      = 3918
      RightButtonAreaBottom   = 0
      MiddleButtonAreaLeft    = 3100
      MiddleButtonAreaRight   = 3873
      MiddleButtonAreaTop     = 3918
      MiddleButtonAreaBottom  = 0

```

Si los botones no funcionan, las zonas de pulsación del panel no se han cambiando, asegúrese de que no tiene un archivo de configuración synaptics distribuido de algún paquete que está anulando los ajustes personalizados (es decir, algunos paquetes de AUR distribuyen configuraciones prefijadas con números muy altos).

Estos ajustes no se pueden modificar sobre la marcha con `synclient`, sin embargo, funciona con `xinput`:

```
xinput set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Soft Button Areas" 4000 0 4063 0 3000 4000 4063 0

```

No se pueden utilizar porcentajes con esta orden, así que busque en `/var/log/Xorg.0.log` para averiguar los rangos de los ejes x e y del panel táctil.

### Panel táctil detectado como ratón (paneles táctiles elantech)

Este problema puede acaecer en algunos portátiles con panel táctil elantech, por ejemplo ASUS x53s. En esta situación es necesario el paquete [psmouse-elantech](https://aur.archlinux.org/packages/psmouse-elantech/) de [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

## Véase también

*   [Synaptics touchpad driver](http://cgit.freedesktop.org/xorg/driver/xf86-input-synaptics/)