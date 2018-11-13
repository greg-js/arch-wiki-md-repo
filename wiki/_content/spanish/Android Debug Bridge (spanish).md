El [puente de depurado de Android](https://developer.android.com/studio/command-line/adb) (**ADB**, siglas en ingles) es una herramienta de terminal que se usa para instalar, desinstalar, depurar aplicaciones, transferir archivos y acceso al dispositivo.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Uso](#Uso)
    *   [2.1 Conectar dispositivo](#Conectar_dispositivo)
    *   [2.2 Descubrimiento de dispositivos](#Descubrimiento_de_dispositivos)
    *   [2.3 Agregar reglas de udev](#Agregar_reglas_de_udev)
    *   [2.4 Configuración del puente](#Configuración_del_puente)
    *   [2.5 Descubrimiento de dispositivo](#Descubrimiento_de_dispositivo)
    *   [2.6 Transferencia de archivos](#Transferencia_de_archivos)
*   [3 Herramientas basadas en el puente](#Herramientas_basadas_en_el_puente)

## Instalación

ADB hace parte de los [paquetes SDK](/index.php/Android_(Espa%C3%B1ol)#Instalación_del_SDK "Android (Español)") de Android y del paquete [android-tools](https://www.archlinux.org/packages/?name=android-tools).

## Uso

Esta sección se refiere a lo que generalmente se conoce como **ADB (Android Debug Bridge)**, si existe alguna referencia a *ADB* es simplemente la versión en ingles.

### Conectar dispositivo

**Sugerencia:**

*   En algunos dispositivos, puede ser necesario activar la opción de transferencia de datos (MTP), antes que el puente de depurado funcione. Otros dispositivos requieren el modo PTP para que funcione.
*   Las reglas de udev para muchos dispositivos vienen configuradas con el paquete [libmtp](https://www.archlinux.org/packages/?name=libmtp), así que si lo tiene instalado los siguientes pasos puede que no sean necesarios.
*   Asegúrese que su cable de USB funciona para recargar batería y para transferencia de datos. Bastantes cables de USB que vienen con el dispositivo no tienen el pin para transferencia de datos.

Para conectar a un dispositivo o teléfono mediante el puente de depurado es necesario:

1.  Instalar el paquete [android-tools](https://www.archlinux.org/packages/?name=android-tools). Adicionalmente, es recomendable instalar el paquete [android-udev](https://www.archlinux.org/packages/?name=android-udev) si desea conectar el dispositivo con la entrada apropiada en `/dev/`.
2.  conecte el dispositivo de Android con el cable USB al computador.
3.  Habilite depurado por USB en el dispositivo:
    *   Android Jelly Bean (4.2) y nuevos: en *Configuración > Acerca del dispositivo* clic *Numero de compilación* 7 veces hasta que vea una notificación que se ha vuelto programador. Después vaya a *Configuración > Opciones de programador > Depuración en Android* y active esta opción. El dispositivo preguntara para aceptar el computador con la huella digital pertinente, permitir de manera permanente copiara el archivo `$HOME/.android/adbkey.pub` en la carpeta `/data/misc/adb/adb_keys` del dispositivo.
    *   Versiones anterioes: generalmente se activa en *Configuración > Aplicaciones > Desarrollo > Depurado en Android*. Reinicie el teléfono después de activar esta opción para asegurarse que el depurado esta habilitado.

Si el [puente reconoce su dispositivo](#Conectar_dispositivo), o el comando `adb devices` muestra `"device"` y no `"unauthorized"`, o es visible desde el su entorno de desarrollo; la conexión funciona. De lo contrario vea las instrucciones en la parte inferior.

### Descubrimiento de dispositivos

Cada dispositivo de Android tiene una identificación USB de manera vendor/product. Por ejemplo un HTC Evo es:

```
vendor id: 0bb4
product id: 0c8d

```

Conecte su dispositivo y ejecute:

```
$ lsusb

```

Debe mostrar algo parecido:

```
Bus 002 Device 006: ID 0bb4:0c8d High Tech Computer Corp.

```

### Agregar reglas de udev

Use las reglas del paquete [android-udev](https://www.archlinux.org/packages/?name=android-udev) o [android-udev-git](https://aur.archlinux.org/packages/android-udev-git/), instale manualmente desde [desarrollador Android](https://source.android.com/source/initializing#configuring-usb-access), o use la siguiente plantilla para sus [reglas udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)"), simplemente reemplace `[VENDOR ID]` y `[PRODUCT ID]` con los necesarios. Copie estas reglas en el archivo `/etc/udev/rules.d/51-android.rules`:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="[VENDOR ID]", MODE="0660", GROUP="adbusers"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_adb"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_fastboot"

```

Después, cargue nuevamente las reglas udev ejecutando:

```
# udevadm control --reload-rules

```

Asegúrese que su usuario es miembro del [grupo](/index.php/User_group_(Espa%C3%B1ol) "User group (Español)") `adbusers` para acceder dispositivos `adb`.

### Configuración del puente

en lugar de usar reglas de udev, es posible crear/editar `~/.android/adb_usb.ini`. El cual contiene una lista de identificaciones de `vendor`.

 `~/.android/adb_usb.ini` 
```
0x27e8

```

### Descubrimiento de dispositivo

Después de instalar las reglas udev, desconecte y re-conecte su dispositivo a la computadora:

Ahora ejecute:

```
$ adb devices

```

Deberá ver un resultado similar:

```
List of devices attached 
HT07VHL00676    device

```

### Transferencia de archivos

Es posible usar puente para transferir archivos entre la computadora y el dispositivo Android. Para transferir archivos al dispositivo use:

```
$ adb push *<archivo-a-copiar>* *<donde-copiar>*

```

Para transferir archivos desde el dispositivo use:

```
$ adb pull *<archivo-requerido>* *<donde-copiar>*

```

Véase [#Herramientas basadas en el puente](#Herramientas_basadas_en_el_puente).

## Herramientas basadas en el puente

*   [adbfs-rootless](https://github.com/spion/adbfs-rootless) disponible como [adbfs-rootless-git](https://aur.archlinux.org/packages/adbfs-rootless-git/) – sistema de archivos [FUSE](/index.php/FUSE "FUSE") sobre el puente
*   [adb-sync](https://github.com/google/adb-sync) disponible como [adb-sync-git](https://aur.archlinux.org/packages/adb-sync-git/) – Herramienta para sincronizar archivos entre compuutadora y dispositivo Android que usa el puente de depurado.
*   [AndroidScreencast](http://xsavikx.github.io/AndroidScreencast) disponible como [androidscreencast-bin](https://aur.archlinux.org/packages/androidscreencast-bin/) – vea y controle su dispositivo Android desde su PC.