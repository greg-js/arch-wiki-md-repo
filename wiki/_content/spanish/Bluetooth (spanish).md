[Bluetooth](http://www.bluetooth.org/) es un protocolo estándar para comunicación inalámbrica de corta distancia en teléfonos móviles, computadores portátiles y otros equipos electrónicos. En Linux la implementación mas conocida del protocolo Bluetooth es [BlueZ](http://www.bluez.org/).

## Contents

*   [1 Instalación](#Instalación)
    *   [1.1 Interfaces](#Interfaces)
        *   [1.1.1 Consola](#Consola)
        *   [1.1.2 Gráfica](#Gráfica)
            *   [1.1.2.1 GNOME Bluetooth](#GNOME_Bluetooth)
            *   [1.1.2.2 Bluedevil](#Bluedevil)
            *   [1.1.2.3 Blueberry](#Blueberry)
            *   [1.1.2.4 Blueman](#Blueman)
            *   [1.1.2.5 ObexFS](#ObexFS)
                *   [1.1.2.5.1 Transferencias con ObexFTP](#Transferencias_con_ObexFTP)
                *   [1.1.2.5.2 Obex Object Push](#Obex_Object_Push)
*   [2 Asociación](#Asociación)
*   [3 Configuración](#Configuración)
    *   [3.1 Inicio automático después de reiniciar](#Inicio_automático_después_de_reiniciar)
*   [4 Audio](#Audio)
    *   [4.1 Usar parlantes como audífonos de Bluetooth](#Usar_parlantes_como_audífonos_de_Bluetooth)

## Instalación

1.  [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquetes [bluez](https://www.archlinux.org/packages/?name=bluez), el cual contiene el protocolo de Bluetooth.
2.  [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquetes [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), el cual provee la utilidad `bluetoothctl`. Alternativamente puede instalar [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/) el cual contiene las herramientas obsoletas de BlueZ.
3.  El controlador genérico de Bluetooth es el modulo del kernel `btusb`. [Verifique](/index.php/Kernel_modules_(Espa%C3%B1ol)#Obtener_informaci.C3.B3n "Kernel modules (Español)") si el modulo ha sido cargado en su sistema. En caso de que no lo sea [cargue el modulo](/index.php/Kernel_modules_(Espa%C3%B1ol)#Manejar_m.C3.B3dulos_manualmente "Kernel modules (Español)") de manera manual.
4.  [Active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") / [active inicio automático](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") de la unidad de systemd `bluetooth.service`.

**Nota:**

*   Por defecto el demonio de bluetooth solo ofrecerá dispositivos a usuarios que son miembros del grupo `lp`. Asegúrese de agregar su usuario a este grupo si desea conectarse. Es posible cambiar el grupo que se requiere en el archivo `/etc/dbus-1/system.d/bluetooth.conf`.
*   Algunos adaptadores de bluetooth están combinados con una tarjeta de Wi-Fi (v.g. [Intel Centrino](http://www.intel.com/content/www/us/en/wireless-products/centrino-advanced-n-6235.html)). Estos requieren que la tarjeta Wi-Fi sea activada (normalmente hay alguna combinación de teclas en el teclado) para que el adaptador de bluetooth le sea visible al kernel.
*   Algunos adaptadores de bluetooth (v.g. Broadcom) entran en conflicto con con el adaptador de red, así que es necesario que el dispositivo de blueetooth se conecte antes del inicio del servicio de red.
*   Algunas herramientas como `hcitool` o `hciconfig` han sido abandonadas por los desarrolladores originales, y no son incluidas en el paquete [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils). Ya que estas herramientas no van a ser mantenidas, se recomienda que los scripts sean actualizados evitando su uso. Si de todas maneras se desea usarlas, instale el paquete [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/). Vea el reporte [FS#53110](https://bugs.archlinux.org/task/53110) y [the Bluez mailing list](https://www.spinics.net/lists/linux-bluetooth/msg69239.html) para mas información.

### Interfaces

#### Consola

*   **bluetoothctl** — Asociar un dispositivo desde la terminal es una de las opciones mas simples y robustas para establecer una conexion.

	[http://www.bluez.org/](http://www.bluez.org/) || [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)

**Sugerencia:** Para automatizar bluetoothctl en un script use `echo -e "<command1>
<command2>
" | bluetoothctl`

#### Gráfica

##### GNOME Bluetooth

[GNOME Bluetooth](https://wiki.gnome.org/Projects/GnomeBluetooth) es la herramienta de bluetooth de [GNOME (Español)](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"). El paquete [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) provee el motor del programa, [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) provee una miniaplicación para monitorear el estatus, y [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) provee el GUI para la configuración y se puede ver en el panel principal de configuración o desde la terminal con el comando `gnome-control-center bluetooth`. Es posible lanzar el comando `bluetooth-sendto` directamente para enviar archivos a un dispositivo remoto.

Para recibir archivos, abra el panel de configuración de Bluetooth; solo se puede recibir mientras que el panel de Bluetooth este abierto.

**Sugerencia:** Para agregar una entrada de *Enviar a* en el menu de Thunar, vea las instrucciones [aquí](http://docs.xfce.org/xfce/thunar/send-to). (El comando que necesita ser configurado es `bluetooth-sendto %F`).

##### Bluedevil

[Bluedevil](https://projects.kde.org/projects/kde/workspace/bluedevil) la herramienta de Bluetooth de [KDE (Español)](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)"). [Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete [bluedevil](https://www.archlinux.org/packages/?name=bluedevil) (KDE Plasma 5).

Si no hay un icono visible en Dolphin y en la bandeja de herramientas, se puede activar en las opciones de bandeja de herramientas o agregue un widget. Es posible configurar Bluedevil y detectar dispositivos Bluetooth haciendo clic en el icono. Una interfaz también esta disponible en el panel de configuración de KDE.

##### Blueberry

*Blueberry* es una alternativa a la interfaz de Bluetooth de GNOME. Se puede instalar con el paquete [blueberry](https://www.archlinux.org/packages/?name=blueberry). Provee una herramienta de configuración (*blueberry*), y una mini aplicación en la bandeja de herramientas (*blueberry-tray*).

**Nota:** *Blueberry* no soporta recibir archivos a traves de Obex Push, vea *Blueman* debajo si desea recibir archivos.

##### Blueman

[Blueman](http://blueman-project.org) es un gestor completo de Bluetooth. Provee una interfaz grafica de configuración `blueman-manager` y una mini aplicación `blueman-applet` para la bandeja de herramientas. Vea [Blueman](/index.php/Blueman "Blueman") para mas detalles.

##### ObexFS

Otra opción, en lugar de usar los paquetes de KDE o GNOME, es ObexFS. Este permite montar teléfonos móviles que son tratados como cualquier otro sistema de ficheros.

**Nota:** Para usar ObexFS se necesita un dispositivo que provee servicio de ObexFTP.

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") [obexfs](https://aur.archlinux.org/packages/obexfs/) y monte teléfonos soportados ejecutando:

```
$ obexfs -b *MAC_dispositivo* /puntodemontaje

```

Una vez finalizado, desmonte el dispositivo con el comando:

```
$ fusermount -u /puntodemontaje

```

Para mas información en las opciones de montaje vea [http://dev.zuckschwerdt.org/openobex/wiki/ObexFs](http://dev.zuckschwerdt.org/openobex/wiki/ObexFs)

**Nota:** Asegúrese que el dispositivo de Bluetooth que esta montando **no** esta en modo *solo-lectura*. Esto se puede modificar el la configuración del móvil. Si el dispositivo se monta en modo *solo-lectura* se pueden encontrar errores con permisos al intentar transferir archivos al dispositivo.

###### Transferencias con ObexFTP

Si su dispositivo es compatible con el servicio de ObexFTP pero no desea montar el dispositivo, se pueden transferir o recibir archivos usando el comando `obexftp`.

Para enviar un archivo a un dispositivo ejecute:

```
$ obexftp -b *MAC_dispositivo* -p /ruta/al/archivo

```

Para extraer un archivo de un dispositivo ejecute:

```
$ obexftp -b *MAC_dispositivo* -g nombredearchivo

```

**Nota:** Asegúrese que el archivo que esta extrayendo esta en la *carpeta de intercambio* del dispositivo. Si el archivo esta en una sub carpeta de la carpeta de intercambio, modifique la ruta de acceso en el comando.

###### Obex Object Push

Para dispositivos que no son compatibles con el servicio de ObexFTP, verifique si Obex Object Push es compatible.

```
# sdptool browse *XX:XX:XX:XX:XX:XX*

```

Lea la respuesta y busque *Obex Object Push*. Recuerde el canal para este servicio. Si es compatible, se puede usar [ussp-push](https://aur.archlinux.org/packages/ussp-push/) para enviar archivos a ese dispositivo:

```
# ussp-push *XX:XX:XX:XX:XX:XX*@*Canal* *Archivo* *nombre_en_el_destino*

```

## Asociación

**Nota:** Antes de usar un dispositivo de bluetooth, asegurese que no esta bloqueado por [rfkill](/index.php/Wireless_network_configuration_(Espa%C3%B1ol)#Rfkill "Wireless network configuration (Español)").

Asociar un dispositivo desde una terminal es una de las opciones mas simples y confiables. El procedimiento exacto depende de los dispositivos específicos y su funcionalidad. La siguiente guía es un bosquejo general de la asociación de un dispositivo usando `/usr/bin/bluetoothctl`:

Comience con el comando `bluetoothctl` en una terminal. Teclee `help` para una lista de comandos disponibles.

*   Posiblemente seleccione un controlador tecleando `select *dirección MAC*`.
*   Encienda la energía del controlador tecleando `power on`. Por defecto esta apagado y se apagara de nuevo en cada reinicio, vea [Encendido automatico despues de reiniciar](#Inicio_automático_después_de_reiniciar).
*   Teclee `devices` para obtener la dirección MAC del dispositivo con el que se quiere asociar.
*   Entre en el modo de descubrimiento de dispositivos tecleando `scan on`, si el dispositivo requerido aun no esta en la lista.
*   Encienda el agente con `agent on`, o seleccione el agente: al presionar tabulador dos veces después de `agent` se vera una lista de agentes disponibles.
*   Teclee `pair *dirección MAC*` para ejecutar la asociación (completado con tabulador también funciona).
*   Si se usa un dispositivo sin PIN, es necesariamente agregar el dispositivo a la lista de dispositivos confiables antes de conectarse. Teclee `trust *dirección MAC*` para hacerlo.
*   Finalmente, use el comando `connect *dirección MAC*` para establecer una conexión.

Una sesión de ejemplo puede verse de la siguiente manera:

```
# bluetoothctl 
[NEW] Controller 00:10:20:30:40:50 pi [default]
[bluetooth]# agent on 
Agent registered
[bluetooth]# default-agent 
Default agent request successful
[bluetooth]# power on
Changing power on succeeded
[CHG] Controller 00:10:20:30:40:50 Powered: yes
[bluetooth]# scan on
Discovery started
[CHG] Controller 00:10:20:30:40:50 Discovering: yes
[NEW] Device 00:12:34:56:78:90 myLino
[CHG] Device 00:12:34:56:78:90 LegacyPairing: yes
[bluetooth]# pair 00:12:34:56:78:90
Attempting to pair with 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
[CHG] Device 00:12:34:56:78:90 Connected: no
[CHG] Device 00:12:34:56:78:90 Connected: yes
Request PIN code
[agent] Enter PIN code: 1234
[CHG] Device 00:12:34:56:78:90 Paired: yes
Pairing successful
[CHG] Device 00:12:34:56:78:90 Connected: no
[bluetooth]# connect 00:12:34:56:78:90
Attempting to connect to 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
Connection successful

```

## Configuración

### Inicio automático después de reiniciar

Por defecto, los adaptadores de bluetooth no se inician después de reiniciar el computador. El metodo antiguo usando `hciconfig hci0 up` es obsoleto, vea [release note](http://www.bluez.org/release-of-bluez-5-35/). Ahora solo es necesario agregar la linea `AutoEnable=true` en el archivo `/etc/bluetooth/main.conf` al final de la seccion de `[Policy]`:

 `/etc/bluetooth/main.conf` 
```
[Policy]
AutoEnable=true
```

## Audio

Para poder usar equipo de audio como parlantes o audífonos con Bluetooth, es necesario [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete adicional [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth).

Vea la pagina [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset") (ingles) para mas información acerca de audio con Bluetooth en audífonos.

### Usar parlantes como audífonos de Bluetooth

Para habilitar que el sistema sea detectado como un A2DP sink (v.g. al reproducir música desde un móvil por los parlantes del computador), agregue lo siguiente al archivo `/etc/bluetooth/audio.conf` (cree el archivo si es necesario):

```
[General]
Enable=Source

```

Mas información en:

*   [https://gist.github.com/joergschiller/1673341](https://gist.github.com/joergschiller/1673341)
*   [http://www.lightofdawn.org/blog/?viewDetailed=00031](http://www.lightofdawn.org/blog/?viewDetailed=00031)