Artículos relacionados

*   [Optical Disc Drive (Español)](/index.php/Optical_Disc_Drive_(Espa%C3%B1ol) "Optical Disc Drive (Español)")
*   [Archiso (Español)](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

Esta página aborda varios métodos sobre cómo escribir la instatánea de Arch Linux en una unidad USB (también conocida por *«unidad flash», «lápiz USB», «llave USB»*, etc.) El resultado será un sistema de tipo LiveCD (*«LiveUSB»*, si se prefiere) que, debido a la naturaleza de [SquashFS](https://en.wikipedia.org/wiki/es:SquashFS "wikipedia:es:SquashFS"), descarta todos los cambios una vez que se apaga el equipo.

Si desea realizar una instalación completa de Arch Linux desde una unidad USB (es decir, con valores persistentes), véase [Intatar Arch Linux en una llave USB](/index.php/Installing_Arch_Linux_on_a_USB_key_(Espa%C3%B1ol) "Installing Arch Linux on a USB key (Español)"). Si desea usar la llave USB arrancable de Arch Linux como un USB de rescate, consulte [Change Root](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)").

## Contents

*   [1 Crear USB para arrancar desde sistemas BIOS y UEFI](#Crear_USB_para_arrancar_desde_sistemas_BIOS_y_UEFI)
    *   [1.1 Utilizar dd](#Utilizar_dd)
        *   [1.1.1 En GNU/Linux](#En_GNU.2FLinux)
        *   [1.1.2 En Windows](#En_Windows)
            *   [1.1.2.1 Utilizar Cygwin](#Utilizar_Cygwin)
            *   [1.1.2.2 dd para Windows](#dd_para_Windows)
        *   [1.1.3 En Mac OS X](#En_Mac_OS_X)
        *   [1.1.4 Cómo restaurar la unidad USB](#C.C3.B3mo_restaurar_la_unidad_USB)
    *   [1.2 Utilizar método manual](#Utilizar_m.C3.A9todo_manual)
        *   [1.2.1 En GNU/Linux](#En_GNU.2FLinux_2)
        *   [1.2.2 En Windows](#En_Windows_2)
*   [2 Otros métodos para sistemas BIOS](#Otros_m.C3.A9todos_para_sistemas_BIOS)
    *   [2.1 En GNU/Linux](#En_GNU.2FLinux_3)
        *   [2.1.1 Utilizar UNetbootin](#Utilizar_UNetbootin)
    *   [2.2 En Windows](#En_Windows_3)
        *   [2.2.1 Win32 Disk Imager](#Win32_Disk_Imager)
        *   [2.2.2 USBWriter para Windows](#USBWriter_para_Windows)
        *   [2.2.3 El método Flashnul](#El_m.C3.A9todo_Flashnul)
        *   [2.2.4 Cargar el soporte de instalación desde la RAM](#Cargar_el_soporte_de_instalaci.C3.B3n_desde_la_RAM)
            *   [2.2.4.1 Preparar la unidad flash USB](#Preparar_la_unidad_flash_USB)
            *   [2.2.4.2 Copiar los archivos necesarios a la unidad flash USB](#Copiar_los_archivos_necesarios_a_la_unidad_flash_USB)
            *   [2.2.4.3 Crear el archivo de configuración](#Crear_el_archivo_de_configuraci.C3.B3n)
            *   [2.2.4.4 Paso final](#Paso_final)
        *   [2.2.5 Universal USB Installer](#Universal_USB_Installer)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Crear USB para arrancar desde sistemas BIOS y UEFI

### Utilizar dd

**Nota:** De los dos métodos este es el recomendable por su simplicidad. Si no funciona cambie al método alternativo [#Utilizar formato manual](#Utilizar_formato_manual).

**Advertencia:** Esta acción destruirá irreversiblemente todos los datos en `/dev/sd**x**`.

#### En GNU/Linux

**Sugerencia:** Compruebe con la orden `lsblk` que el soporte de instalación de la llave USB **no** está montado.

**Nota:** Utilice `/dev/sd**x**` en lugar de `/dev/sd**x1**`, y ajuste **x** para reflejar el dispositivo de destino.

```
# dd bs=4M if=/ruta/a/archlinux.iso of=/dev/sd**x** && sync

```

#### En Windows

##### Utilizar Cygwin

Asegúrese de que la instalación de [Cygwin](http://www.cygwin.com/) contiene el paquete dd.

**Sugerencia:** Si no se desea instalar Cygwin, solo tiene que descargar `dd` para Windows desde [aquí](http://www.chrysocome.net/dd). Véase la siguiente sección para más información.

Coloque el archivo de imagen en su directorio personal, por ejemplo:

```
C:\cygwin\home
ombre_de_usuario\

```

Ejecute cygwin como administrador (necesario para que cygwin pueda acceder al hardware). Para escribir en el disco USB utilice la siguiente orden:

```
dd if=image.iso of=\\.\[x]: bs=4M

```

donde `image.iso` es la ruta al archivo de imagen ISO en el directorio cygwin y `\\.\[**x**]:` es el dispositivo USB donde **x** es la letra designada por windows, que en el ejemplo seguido es: `\\.\d:`.

En cygwin 6.0 busque la salida de la partición correcta con:

```
cat /proc/partitions

```

y escriba la imagen ISO con la información obtenida de la salida.

Ejemplo:

**Advertencia:** La orden de abajo borra irremediablemente todos los archivos de la memoria USB, así que asegúrese de que no tiene archivos importantes en el lápiz usb antes de hacer esta operación.

```
dd if=image.iso of=/dev/sdb bs=4M

```

##### dd para Windows

**Nota:** Algunos usuarios tienen un problema que indica que «isolinux.bin missing or corrupt» (*isolinux.bin falta o está dañado*) al arrancar el soporte con este método.

Una versión dd con licencia GPL para Windows está disponible en [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd). La ventaja de este sobre Cygwin es que la descarga es más pequeña. Úselo como se indica para las instrucciones de Cygwin mencionadas más arriba.

Para comenzar, descargue la última versión de dd para Windows. Una vez descargado, extraiga el contenido del archivo en la carpeta *Descargas* o en otra carpeta.

Ahora, inicie un `prompt de órdenes` como administrador. A continuación, muevase al directorio (con la orden `cd`) de Descargas (o a la carpeta donde haya extraido el paquete).

Si la ISO de Arch Linux está en otra carpeta, distinta de la de Descargas, es posible que deba indicar la ruta completa; por tanto, por comodidad es posible que desee poner la ISO de Arch Linux en la misma carpeta que el ejecutable dd. El formato básico de la orden se verá así:

 `dd if=archlinux-2013-XX-xx-dual.iso of=\\.\x: bs=4m` 
**Advertencia:** Esta orden reemplaza los contenidos de la unidad y la formatea con la imagen ISO. Es probable que no pueda recuperar su contenido en el caso de una copia accidental. Por lo tanto, debe estar completamente seguro de que está dirigiendo dd a la unidad correcta antes de ejecutarla.

Basta con reemplazar los distintos puntos vacíos (indicados con una «x») con la fecha correcta y la letra de unidad correcta.

He aquí un ejemplo completo.

 `dd if=ISOs\archlinux-2013.08.01-dual.iso of=\\.\d: bs=4M` 

#### En Mac OS X

Para poder utilizar la orden `dd` sobre un dispositivo USB en un Mac, tiene que hacer algunas operaciones especiales. En primer lugar, inserte el dispositivo USB, OS X lo montará automáticamente, y en `Terminal.app` ejecute:

```
$ diskutil list

```

Hay que averiguar cómo se llama el dispositivo USB con las órdenes `mount` o `sudo dmesg | tail`, y desmonte las particiones en el dispositivo (por ejemplo, /dev/disk1s1) mientras se mantiene montado el dispositivo adecuado (es decir, /dev/disk1).

```
$ diskutil unmountDisk /dev/disk1

```

Ahora se puede continuar de acuerdo con las instrucciones anteriores para Linux (pero use `bs=8192` con la orden `dd`, si está utilizando el OS X, el número viene de `1024*8`).

 `dd if=image.iso of=/dev/disk1 bs=8192` 
```
20480+0 records in
20480+0 records out
167772160 bytes transferred in 220.016918 secs (762542 bytes/sec)

```

Es probablemente una buena idea expulsar el disco en este momento antes de la extracción física :

```
$ diskutil eject /dev/disk1

```

#### Cómo restaurar la unidad USB

Debido a que la imagen ISO es un híbrido que puede ser grabada en un disco o escribirse directamente en una unidad USB, no incluye una tabla de particiones por defecto.

Después de instalar Arch Linux y, por tanto, se ha terminado de utilizar la unidad USB a este fin, en esta se debe ajustar a cero los primeros 512 bytes *(es decir, donde se ubica el código de arranque del MBR y la tabla de particiones no estándar)* si desea restaurar la funcionalidad del USB completamente:

```
# dd count=1 bs=512 if=/dev/zero of=/dev/sdx && sync

```

A continuación, cree una nueva tabla de particiones (por ejemplo, «msdos») y un sistema de archivos (por ejemplo, EXT4, FAT32) utilizando [gparted](https://www.archlinux.org/packages/?name=gparted), o desde un terminal:

*   Para EXT2/3/4 (ajústelo en consecuencia), sería:

```
# cfdisk /dev/sd**x**
# mkfs.ext4 /dev/sd**x1**
# e2label /dev/sd**x1** USB_STICK

```

*   Para FAT32, instale el paquete [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) y ejecute:

```
# cfdisk /dev/sd**x**
# mkfs.vfat -F32 /dev/sd**x1**
# dosfslabel /dev/sd**x1** USB_STICK

```

### Utilizar método manual

#### En GNU/Linux

Este método es un poco más complicado que escribir la imagen directamente con `dd`, pero, en cambio, mantiene la unidad utilizable para el almacenamiento de datos.

*   Asegúrese de que tiene el paquete más reciente de *syslinux* (versión 6.02 o posterior) instalado.

*   Cree una tabla de particiones MBR (msdos) con, al menos, una partición en el USB que contenga un sistema de archivos FAT32\. Si no es así, cree la partición y/o sistema de archivos antes de continuar.

*   Monte la imagen ISO:

```
# mkdir -p /mnt/{usb,iso}
# mount -o loop archlinux-2013.10.01-dual.iso /mnt/iso

```

**Nota:** En cualquiera de las siguientes órdenes, ajuste `/dev/sd**X**1` de acuerdo a su sistema.

*   Monte la partición FAT32 del USB recién creada y copie el contenido del soporte de instalación al dispositivo USB.

```
# mkdir -p /mnt/usb
# mount /dev/sd**X**1 /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/{usb,iso}

```

*   Ajuste los archivos de configuración. Estas órdenes reemplazan la parte `archisolabel=ARCH_2013XX` con su equivalente `archiso**device**=/dev/disk/by-uuid/47FA-4071` para ambos archivos de configuración, al mismo tiempo, utilizando una sola orden:

**Advertencia:** Si se equivoca al etiquetar la unidad "`ARCH_2013XX`" (con el apropiado mes de lanzamiento) o al usar [UUID](/index.php/UUID "UUID") (al reetiquetarlo según su preferencia) impedirá el arranque desde el medio creado.

```
$ sed -i "s|label=ARCH_.*|device=/dev/disk/by-uuid/$(blkid -o value -s UUID /dev/sd**X**1)|" archiso_sys{32,64}.cfg

```

**Nota:** Una vez más, ajuste `/dev/sd**X**1`.

*   Instale Syslinux en el USB siguiendo las instrucciones de [Syslinux (Español)#Instalación manual](/index.php/Syslinux_(Espa%C3%B1ol)#Instalaci.C3.B3n_manual "Syslinux (Español)"). Sobrescriba los módulos existentes de syslinux (archivos `*.c32`) presentes en el USB (que se han copiado desde la ISO) con las del paquete Syslinux, para evitar los errores de inicio relacionados con versiones no concordantes.

*   Marque la partición USB como activa siguiendo [Syslinux (Español)#Tabla de particiones MBR](/index.php/Syslinux_(Espa%C3%B1ol)#Tabla_de_particiones_MBR "Syslinux (Español)")

#### En Windows

**Nota:**

*   No utilice cualquier **Bootable USB Creator utility** para crear el USB de arranque UEFI. No utilice *dd en Windows* para transferir la ISO a la unidad USB.

*   En las siguientes órdenes **X** se supone que es la unidad flash USB en Windows.

*   Windows usa la barra diagonal invertida `\` como separación de la ruta, por lo que la misma se utiliza en las órdenes de abajo.

*   Todas las órdenes se deben ejecutar en el prompt de órdenes de Windows **como administrador**.

*   `>` indica el prompt de órdenes de Windows.

*   Particione y formatee la unidad USB utilizando [Rufus USB partitioner](http://rufus.akeo.ie/). Seleccione la opción del esquema de particionado como **MBR for BIOS and UEFI** y el sistema de archivos como **FAT32**. Desmarque las opciones «Create a bootable disk using ISO image» y «Create extended label and icon files».

*   Cambie **Volume Label** de la unidad flash USB `X:` para hacerla coincidir con el LABEL mencionado en `archisolabel=` parte de `<ISO>\loader\entries\archiso-x86_64.conf`. Este paso es necesario para la ISO Oficial ([Archiso](/index.php/Archiso "Archiso")).

*   Extraiga la ISO (de modo similar a como se extrae un archivo ZIP) en la unidad flash USB (utilizando [7-Zip](http://7-zip.org/)).

*   Descargue los binarios oficiales (archivo zip) mas recientes de syslinux 6.xx desde [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) y extráigalos.

*   Ejecute las siguientes órdenes (en el prompt de órdenes de Windows, como administrador):

```
> cd bios\
> for /r %Y in (*.c32) do copy "%Y" "X:\boot\syslinux\" /y
> copy mbr\*.bin X:\boot\syslinux\ /y

```

*   Instale Syslinux en el USB para poder ejecutarlo (utilice `win64/syslinux64.exe` en Windows x64):

```
> cd bios\
> win32/syslinux.exe -d /boot/syslinux -i -a -m X:

```

**Nota:**

*   El paso anterior instala Syslinux `ldlinux.sys` en el VBR de la partición USB, establece la partición como activa/arrancable en la tabla de particiones MBR, y escribe el código de arranque del MBR en los primeros 400 bytes, la región del código de arranque del USB.

*   El parámetro `-d` convierte la ruta esperada a la ruta con la barra invertida de separación como en los sistemas *unix.

## Otros métodos para sistemas BIOS

### En GNU/Linux

#### Utilizar UNetbootin

UNetbootin se puede utilizar en cualquier distribución de Linux o Windows para copiar la ISO en un dispositivo USB. Sin embargo, Unetbootin sobrescribe syslinux.cfg, por lo que crea un dispositivo USB que no arranca correctamente. Por esta razón, **Unetbootin no se recomienda** —en su lugar, use `dd` o uno de los métodos descritos abajo—.

**Advertencia:** UNetbootin escribe, por defecto, `syslinux.cfg`; este debe ser restaurado antes, a fin de que el dispositivo USB arranque correctamente.

Edite `syslinux.cfg`:

 `sysconfig.cfg` 
```
default menu.c32
prompt 0
menu title Archlinux Installer
timeout 100

label unetbootindefault
menu label Archlinux_x86_64
kernel /arch/boot/x86_64/vmlinuz
append initrd=/arch/boot/x86_64/archiso.img archisodevice=/dev/sd**x1** ../../

label ubnentry0
menu label Archlinux_i686
kernel /arch/boot/i686/vmlinuz
append initrd=/arch/boot/i686/archiso.img archisodevice=/dev/sd**x1** ../../
```

En `/dev/sd**x1**` debe sustituir **x** con la primera letra libre después de la última letra en uso en el sistema en el que va a instalar Arch Linux (por ejemplo, si tiene dos unidades de disco duro, utilice `c`). Puede hacer este cambio durante la primera fase del arranque pulsando `Tab` cuando se muestra el menú.

### En Windows

#### Win32 Disk Imager

**Advertencia:** Esto destruirá toda la información en su unidad flash USB

En primer lugar, descargar el programa desde [aquí](http://sourceforge.net/projects/win32diskimager/). A continuación, extraiga el archivo y ejecute el ejecutable. Ahora, seleccione la ISO de Arch Linux en la sección `Image File` y la letra del dispositivo flash USB (por ejemplo [D:\]) en la sección `Device`. Por último, haga clic en `Write` cuando esté listo.

**Sugerencia:** Por defecto, el navegador de archivos Win32 Disk Imager asume que los archivos de la imagen del disco terminan con la extensión `.img`. Sin embargo, puede diferenciar simplemente los `Files of type` desplegando una lista con `*.*` y continuar con la selección de la ISO de Arch Linux.

**Nota:** Después de la instalación, es posible que tenga que restaurar la unidad flash USB siguiendo un proceso similar al que se indica [aquí](#C.C3.B3mo_restaurar_la_unidad_USB).

#### USBWriter para Windows

Descargue el programa desde [http://sourceforge.net/projects/usbwriter/](http://sourceforge.net/projects/usbwriter/) y ejecútelo. Seleccione el archivo de imagen de Arch Linux, la memoria USB de destino, y pulse el botón `write`. Ahora debería ser capaz de arrancar desde el dispositivo USB e instalar Arch Linux desde el mismo.

#### El método Flashnul

[flashnul](http://shounen.ru/soft/flashnul/) es una utilidad para comprobar la funcionalidad y el mantenimiento de memorias flash (USB-Flash, IDE-Flash, SecureDigital, MMC, MemoryStick, SmartMedia, XD, CompactFlash, etc.).

Desde un intérprete de órdenes, invoque flashnul con el parámetro `-p`, y determine qué dispositivo indica como unidad USB. Por ejemplo:

 `C:\>flashnul -p` 
```
Avaible physical drives:
Avaible logical disks:
C:\
D:\
E:\

```

En este caso, la unidad USB es E:

Una vez que haya determinado qué dispositivo es el correcto, puede escribir la imagen al disco, invocando la orden flashnul, con la letra del dispotivo, el parámetro *-L*, y la ruta a la imagen. En este caso, sería:

```
C:\>flashnul **E:** -L *ruta\a\arch.iso*

```

Si está realmente seguro de que desea escribir los datos, escriba *«yes»*, y luego esperar un poco para que pueda escribir. Si se obtiene un error de *«access denied error»*, cierre todas las ventanas que tenga abiertas con Explorer.

Si está en Vista o Win7, debe abrir la consola como administrador, o de lo contrario flashnul fallará al abrir el lápiz usb como si fuese un dispositivo de bloque y solo será capaz de escribir a través del manejo de la unidad proporcionada por Windows.

**Nota:** Necesita utilizar la letra de la unidad en lugar del número. flashnul 1rc1, Windows 7 x64.

#### Cargar el soporte de instalación desde la RAM

Este método utiliza [Syslinux](/index.php/Syslinux "Syslinux") y un [Ramdisk](/index.php/Ramdisk "Ramdisk") ([MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)) para cargar toda la imagen ISO de Arch Linux ISO en la memoria RAM. Dado que esto se ejecuta por completo desde la memoria del sistema, tendrá que asegurarse de que dicha memoria del sistema cuenta con una cantidad adecuada. Una cantidad mínima de RAM entre 500 MB y 1 GB debería ser suficiente para instalar Arch Linux desde un MEMDISK.

Para obtener más información sobre los requisitos del sistema de Arch Linux, así como los de MEMDISK véase la [Guía para Principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)") y [esto](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries).

**Sugerencia:** Una vez que se realiza la carga y aparece el menú gráfico se puede simplemente retirar la memoria USB y, tal vez, incluso utilizarla en otro equipo para iniciar el proceso de nuevo. Por lo tanto, utilizar MEMDISK permite también el arranque y la instalación de Arch desde (y para) el mismo lápiz USB.

##### Preparar la unidad flash USB

Formatee la memoria flash USB con **FAT32** y cree las siguientes carpetas en la unidad recien formateada:

*   `Boot`
    *   `Boot/ISOs`
    *   `Boot/Settings`

##### Copiar los archivos necesarios a la unidad flash USB

Copie la imagen ISO que desea arrancar a la carpeta `Boot/ISOs`, y extraiga los archivos la última liberación de [syslinux](https://www.archlinux.org/packages/?name=syslinux) desde **[aquí](http://www.kernel.org/pub/linux/utils/boot/syslinux/)** y cópielos en las siguientes carpetas:

*   `./win32/syslinux.exe` podría ubicarse en el «Escritorio» o en la carpeta «Descargas» de su equipo.

*   `./memdisk/memdisk` iría a la carpeta `Settings` de la unidad flash USB.

##### Crear el archivo de configuración

Después de copiar los archivos necesarios, navegue por la unidad flash USB a /boot/Settings y cree un archivo `syslinux.cfg` .

**Advertencia:** En la ínea `INITRD`, asegúrese de usar el nombre del archivo ISO que copió en la carpeta `ISOs`.
 `/Boot/Settings/syslinux.cfg` 
```
DEFAULT arch_iso

LABEL arch_iso
        MENU LABEL Arch Setup
        LINUX memdisk
        INITRD /Boot/ISOs/archlinux-2013.08.01-dual.iso
        APPEND iso
```

Para más información sobre Syslinux véase el [artículo de Arch Wiki](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)").

##### Paso final

Por último, cree un archivo `*.bat` en la carpeta donde esté ubicado `syslinux.exe` y ejecútelo («ejecute como administrador» si está en Vista o Windows 7):

 `C:\Documents and Settings\username\Desktop\install.bat` 
```
@echo off
syslinux.exe -m -a -d /Boot/Settings X:
```

#### Universal USB Installer

La herramienta de Windows [[1]](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/) se puede utilizar para crear fácilmente un dispositivo USB live, con múltiples Instaladores de distintas distribuciones de Linux. Una vez creada, los Instaladores pueden ser añadidos o eliminados sin formatear la unidad USB.

## Solución de problemas

*   Para el [Método MEMDISK](#Boot_the_entire_ISO_from_RAM), si obtiene el famoso error «30 seconds», intente arrancar la versión i686, para lo cual pulse la tecla `Tab` para desplazarse hasta la entrada `Boot Arch Linux (i686)` y añada `vmalloc=448M` al final. Como referencia: *Si la imagen es más grande de 128MB y tiene un Sistema Operativo de 32 bits, entonces tiene que aumentar el uso de la memoria máxima de vmalloc*. [(*)](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)
*   Si obtiene el error «30 seconds» debido a que no se monta `/dev/disk/by-label/ARCH_XXXXXX`, pruebe cambiando el nombre del soporte USB a `ARCH_XXXXXX` (por ejemplo, `ARCH_201302`).

## Véase también

*   [Documento Gentoo liveusb](http://www.gentoo.org/doc/en/liveusb.xml)