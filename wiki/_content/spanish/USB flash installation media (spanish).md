**Estado de la traducción**
Este artículo es una traducción de [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media"), revisada por última vez el **2018-11-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=USB_flash_installation_media&diff=0&oldid=548021) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Optical disc drive (Español)](/index.php/Optical_disc_drive_(Espa%C3%B1ol) "Optical disc drive (Español)")
*   [Archiso (Español)](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)")
*   [Multiboot USB drive (Español)](/index.php/Multiboot_USB_drive_(Espa%C3%B1ol) "Multiboot USB drive (Español)")

Esta página aborda varios métodos sobre cómo grabar la instatánea de Arch Linux en una unidad USB (también conocida por *«unidad flash», «lápiz USB», «llave USB»*, etc.) El resultado será un sistema de tipo LiveCD (*«LiveUSB»*, si se prefiere) que, debido a la naturaleza de [SquashFS](https://en.wikipedia.org/wiki/es:SquashFS "wikipedia:es:SquashFS"), descarta todos los cambios una vez que se apaga el equipo.

Si desea realizar una instalación completa de Arch Linux desde una unidad USB (es decir, con valores persistentes), véase [Installing Arch Linux on a USB key (Español)](/index.php/Installing_Arch_Linux_on_a_USB_key_(Espa%C3%B1ol) "Installing Arch Linux on a USB key (Español)"). Si desea usar la memoria USB arrancable de Arch Linux como un USB de rescate, consulte [chroot (Español)](/index.php/Chroot_(Espa%C3%B1ol) "Chroot (Español)").

## Contents

*   [1 Crear USB para arrancar desde sistemas BIOS y UEFI](#Crear_USB_para_arrancar_desde_sistemas_BIOS_y_UEFI)
    *   [1.1 Utilizar herramientas automatizadas](#Utilizar_herramientas_automatizadas)
        *   [1.1.1 En GNU/Linux](#En_GNU.2FLinux)
            *   [1.1.1.1 Utilizar dd](#Utilizar_dd)
            *   [1.1.1.2 Utilizar etcher](#Utilizar_etcher)
        *   [1.1.2 En Windows](#En_Windows)
            *   [1.1.2.1 Utilizar Rufus](#Utilizar_Rufus)
            *   [1.1.2.2 Utilizar USBwriter](#Utilizar_USBwriter)
            *   [1.1.2.3 Utilizar win32diskimager](#Utilizar_win32diskimager)
            *   [1.1.2.4 Utilizar Cygwin](#Utilizar_Cygwin)
            *   [1.1.2.5 dd para Windows](#dd_para_Windows)
        *   [1.1.3 En macOS](#En_macOS)
    *   [1.2 Realizar formateo manual](#Realizar_formateo_manual)
        *   [1.2.1 En GNU/Linux](#En_GNU.2FLinux_2)
        *   [1.2.2 En Windows](#En_Windows_2)
*   [2 Otros métodos para sistemas BIOS](#Otros_m.C3.A9todos_para_sistemas_BIOS)
    *   [2.1 En GNU/Linux](#En_GNU.2FLinux_3)
        *   [2.1.1 Utilizar una unidad USB multiarranque](#Utilizar_una_unidad_USB_multiarranque)
        *   [2.1.2 Utilizar la utilidad de GNOME «Disk Utility»](#Utilizar_la_utilidad_de_GNOME_.C2.ABDisk_Utility.C2.BB)
        *   [2.1.3 Fabricar una unidad USB-ZIP](#Fabricar_una_unidad_USB-ZIP)
        *   [2.1.4 Utilizar UNetbootin](#Utilizar_UNetbootin)
    *   [2.2 En Windows](#En_Windows_3)
        *   [2.2.1 El método Flashnul](#El_m.C3.A9todo_Flashnul)
        *   [2.2.2 Cargar el soporte de instalación desde la RAM](#Cargar_el_soporte_de_instalaci.C3.B3n_desde_la_RAM)
            *   [2.2.2.1 Preparar la unidad USB](#Preparar_la_unidad_USB)
            *   [2.2.2.2 Copiar los archivos necesarios a la unidad USB](#Copiar_los_archivos_necesarios_a_la_unidad_USB)
            *   [2.2.2.3 Crear el archivo de configuración](#Crear_el_archivo_de_configuraci.C3.B3n)
            *   [2.2.2.4 Paso final](#Paso_final)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Crear USB para arrancar desde sistemas BIOS y UEFI

### Utilizar herramientas automatizadas

#### En GNU/Linux

##### Utilizar dd

**Nota:** de los dos métodos este es el recomendable por su simplicidad. Si no funciona cambie al método alternativo [#Realizar formateo manual](#Realizar_formateo_manual).

**Advertencia:** esta acción destruirá irreversiblemente todos los datos en `/dev/sd**x**`. Para restaurar la unidad USB como un dispositivo de almacenamiento vacío y utilizable después de usar la imagen ISO Arch, la firma del sistema de archivos ISO 9660 debe eliminarse ejecutando `wipefs --all /dev/**sdx**` como root, antes de [reparticionar](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") y [reformatear](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") la unidad USB.

**Sugerencia:** encuentre el nombre de su unidad USB con la orden `lsblk`. Asegúrese de que **no** esté montada.

Ejecute la siguiente orden, reemplazando `/dev/**sdx**` con su unidad, por ejemplo. `/dev/sdb`. **No** agregue un número de partición, así que **no** use algo como `/dev/sdb**1**`.

```
# dd bs=4M if=/path/to/archlinux.iso of=/dev/**sdx** status=progress oflag=sync

```

Consulte [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) para obtener más información sobre [dd](/index.php/Dd "Dd"). Consulte [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1#DESCRIPTION) para obtener más información sobre `oflag=sync`.

##### Utilizar etcher

[Etcher](https://etcher.io/) es un grabador de imagen del sistema operativo construido con node.js y Electron, capaz de cargar una tarjeta SD o una unidad USB. Le protege de escribir accidentalmente en sus discos duros y garantiza que cada byte de datos se ha escrito correctamente.

#### En Windows

##### Utilizar Rufus

[Rufus](https://rufus.akeo.ie/) es una grabadora de ISO en USB para diferentes propósitos. Basta con seleccionar el archivo ISO de Arch Linux, la unidad USB en la que desea grabar la imagen de Arch Linux arrancable y hacer clic en *START*.

Como a Rufus no le importa si la unidad está formateada correctamente o no y proporciona una interfaz gráfica, puede ser la herramienta más fácil y robusta de usar.

**Nota:** la imagen debe transferirse en modo **DD Image mode**.

*   Para la versión Rufus ≥ 3.0, seleccione *GPT* en el menú desplegable *Partition scheme*. Después de hacer clic en *START* aparecerá el cuadro de diálogo de selección de modo, seleccione *DD Image mode*.
*   Para la versión Rufus <3.0, seleccione el modo *DD Image* del menú desplegable en la parte inferior.

##### Utilizar USBwriter

Este método no requiere ninguna instrucción y es tan sencillo como realizar `dd` en Linux. Simplemente descargue la ISO de Arch Linux y, con los derechos de administrador local, use la herramienta [USBwriter](https://sourceforge.net/p/usbwriter/wiki/Documentation/) para grabarla en la memoria flash USB.

##### Utilizar win32diskimager

[win32diskimager](https://sourceforge.net/projects/win32diskimager/) es otra herramienta gráfica de grabación de ISO en USB para Windows. Simplemente seleccione la imagen ISO y la letra de la unidad USB de destino (es posible que tenga que formatearla primero para asignarle una letra de unidad) y haga clic en «*Write*».

##### Utilizar Cygwin

Asegúrese de que la instalación de [Cygwin](http://www.cygwin.com/) contiene el paquete dd.

**Sugerencia:** si no se desea instalar Cygwin, solo tiene que descargar `dd` para Windows desde [aquí](http://www.chrysocome.net/dd). Véase la siguiente sección para más información.

Coloque el archivo de imagen en su directorio personal, por ejemplo:

```
C:\cygwin\home
ombre_de_usuario\

```

Ejecute cygwin como administrador (necesario para que cygwin pueda acceder al hardware). Para grabar en el disco USB utilice la siguiente orden:

```
dd if=image.iso of=\\.\**x**: bs=4M

```

donde `image.iso` es la ruta al archivo de imagen ISO en el directorio cygwin y `\\.\[**x**]:` es el dispositivo USB donde **x** es la letra designada por windows, que en el ejemplo seguido es: `\\.\d:`.

En cygwin 6.0 busque la salida de la partición correcta con:

```
cat /proc/partitions

```

y escriba la imagen ISO con la información obtenida de la salida.

Ejemplo:

**Advertencia:** la orden de abajo borra irreversiblemente todos los archivos de la memoria USB, así que asegúrese de que no tiene archivos importantes en su USB antes de realizar esta operación.

```
dd if=image.iso of=/dev/sdb bs=4M

```

##### dd para Windows

**Nota:** algunos usuarios tienen un problema que indica que «isolinux.bin missing or corrupt» (*isolinux.bin falta o está dañado*) al arrancar el soporte con este método.

Una versión dd con licencia GPL para Windows está disponible en [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd). La ventaja de este sobre Cygwin es que la descarga es más pequeña. Úselo como se indica para las instrucciones de Cygwin mencionadas más arriba.

Para comenzar, descargue la última versión de dd para Windows. Una vez descargado, extraiga el contenido del archivo en la carpeta *Descargas* o en otra carpeta.

Ahora, inicie un `prompt de órdenes` como administrador. A continuación, muevase al directorio (con la orden `cd`) de Descargas (o a la carpeta donde haya extraido el paquete).

Si la ISO de Arch Linux está en otra carpeta, distinta de la de Descargas, es posible que deba indicar la ruta completa; por tanto, por comodidad es posible que desee poner la ISO de Arch Linux en la misma carpeta que el ejecutable dd. El formato básico de la orden se verá así:

```
# dd if=*archlinux-2017-XX-YY-x86_64.iso* od=\\.\*x*: bs=4M

```

**Nota:** las letras de la unidad de Windows están vinculadas a una partición. Para permitir la selección de todo el disco, *dd para Windows* proporciona el parámetro `od`, que se usa en las órdenes anteriores. Sin embargo, tenga en cuenta que este parámetro es específico de «dd para Windows» y no se puede encontrar en otras implementaciones de «dd».

**Advertencia:** como se usa `od`, todas las particiones en el disco seleccionado serán destruidas. Asegúrese de estar dirigiendo dd a la unidad correcta antes de ejecutar la orden.

Basta con reemplazar los distintos puntos vacíos (indicados con una «x») con la fecha correcta y la letra de unidad correcta. He aquí un ejemplo completo.

```
# dd if=ISOs\archlinux-2017.04.01-x86_64.iso od=\\.\d: bs=4M

```

**Nota:** alternativamente, reemplace la letra de la unidad con `\\.\PhysicalDrive*X*`, donde `*X*` es el número de la unidad física (comienza desde 0). Ejemplo: `# dd if=ISOs\archlinux-2017.04.01-x86_64.iso of=\\.\PhysicalDrive1 bs=4M` 

Puede averiguar el número de unidad física escribiendo `wmic diskdrive list brief` en el términal o con `dd --list`

Cualquier ventana del del navegador «Explorer» debe estar cerrada o dd devolverá un error.

#### En macOS

Primero, necesita identificar el dispositivo USB. Abra `/Applications/Utilities/Terminal` y enumere todos los dispositivos de almacenamiento con la orden:

```
$ diskutil list

```

Su dispositivo USB aparecerá como algo así como `/dev/disk2 (external, physical)`. Verifique que este sea el dispositivo que desea borrar comprobando su nombre y tamaño, y luego use su identificador para las órdenes a continuación en lugar de /dev/diskX.

Un dispositivo USB normalmente se monta automáticamente en macOS, y se debe desmontar (no expulsarlo) antes de grabarlo en bloque con `dd`. En el Terminal, escriba:

```
$ diskutil unmountDisk /dev/diskX

```

Ahora copie el archivo de imagen ISO en el dispositivo. La orden `dd` es similar a su contraparte de Linux, pero observe la 'r' antes del 'disk' para el modo raw, lo que hace que la transferencia sea mucho más rápida:

```
# dd if=path/to/arch.iso of=/dev/**r**diskX bs=1m

```

Tenga en cuenta que `diskX` aquí no debe incluir el sufijo `s1`, de lo contrario, el dispositivo USB solo podrá iniciarse en modo UEFI y no «*legacy*». Una vez completado, macOS puede quejarse de que «The disk you inserted was not readable by this computer» («*el disco que insertó no se puede leer en este equipo*»). Seleccione 'Ignorar'. El dispositivo USB será de arranque.

### Realizar formateo manual

#### En GNU/Linux

Este método es un poco más complicado que grabar la imagen directamente con `dd`, pero, en cambio, mantiene la unidad utilizable para el almacenamiento de datos (that is, the ISO is installed in a specific partition within the already [partitioned device](/index.php/Partitioning "Partitioning") without altering other partitions).

**Nota:** aquí, indicaremos la partición objetivo como `/dev/sd **Xn**`. En cualquiera de las siguientes órdenes, ajuste **X** y **n** de acuerdo con su sistema.

*   Asegúrese de que tiene el paquete más reciente de [syslinux](https://www.archlinux.org/packages/?name=syslinux) instalado en el sistema.

*   Si aún no ha terminado, cree la tabla de partición y / o la partición en el dispositivo antes de continuar. La partición `/dev/sd**Xn**` debe estar formateada en [FAT32](/index.php/FAT32 "FAT32").

*   Monte la imagen ISO, monte el sistema de archivos FAT32 ubicado en el dispositivo USB y copie en él el contenido de la imagen ISO. Luego desmonte la imagen ISO, pero mantenga la partición FAT32 montada (esto se usará en los pasos posteriores). Por ejemplo:

```
# mkdir -p /mnt/{iso,usb}
# mount -o loop archlinux-2017.04.01-x86_64.iso /mnt/iso
# mount /dev/sd**Xn** /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/iso

```

Para arrancar es necesario o bien una etiqueta o bien un [UUID](/index.php/UUID "UUID") para seleccionar la partición desde la que arrancar. Por defecto, se utiliza la etiqueta `ARCH_2017**XX**` con el mes de publicación adecuado). Por lo tanto, la etiqueta de la partición debe establecerse a drede, por ejemplo, utilizando "gparted". Alternativamente, puede cambiar este comportamiento modificando las líneas que terminan con `archisolabel=ARCH_2017**XX**` en el archivo `/mnt/usb/arch/boot/syslinux/archiso_sys.cfg` (para el arranque BIOS), y en `/mnt/usb/loader/entries/archiso-x86_64.conf` (para el arranque UEFI). Para usar un UUID en su lugar, reemplace esas fragmentos de líneas con `archiso*device*=/dev/disk/by-uuid/**YOUR-UUID**`. El UUID se puede obtener con `blkid -o value -s UUID /dev/sd**Xn**`.

**Advertencia:** las etiquetas que no coincidan o un UUID incorrecto impiden el arranque desde el soporte creado.

Syslinux ya está preinstalado en `/mnt/usb/arch/boot/syslinux`. Instálelo completamente en esa carpeta siguiendo [Syslinux#Manual install](/index.php/Syslinux#Manual_install "Syslinux"). Las instrucciones se reproducen aquí para mayor comodidad.

*   Sobrescriba los módulos Syslinux existentes (archivos *.c32*) presentes en el USB (desde la ISO) con los del paquete [syslinux](https://www.archlinux.org/packages/?name=syslinux) (que se encuentran en `/usr/lib/syslinux/bios/`). Esto es necesario para evitar un error de arranque debido a una posible discrepancia de versiones.

```
# cp /usr/lib/syslinux/bios/*.c32 /mnt/usb/arch/boot/syslinux/

```

*   Ejecute:

```
# extlinux --install /mnt/usb/arch/boot/syslinux

```

*   Desmonte la partición (`umount /mnt/usb`).
*   Marque la partición como activa (o «boteable»).

#### En Windows

**Nota:**

*   No utilice cualquier **Bootable USB Creator utility** para crear el USB de arranque UEFI. Para el formateo manual, no utilice *dd para Windows* para transferir la ISO a la unidad USB.
*   En las siguientes órdenes **X** se supone que es la unidad USB en Windows.
*   Windows usa la barra diagonal invertida `\` como separación de la ruta, por lo que la misma se utiliza en las órdenes de abajo.
*   Todas las órdenes se deben ejecutar en el prompt de órdenes de Windows **como administrador**.
*   `>` indica el prompt de órdenes de Windows.

*   Particione y formatee la unidad USB utilizando [Rufus USB partitioner](http://rufus.akeo.ie/). Seleccione la opción del esquema de particionado como **MBR for BIOS and UEFI** y el sistema de archivos como **FAT32**. Desmarque las opciones «Create a bootable disk using ISO image» y «Create extended label and icon files».

*   Cambie **Volume Label** de la unidad USB `X:` para hacerla coincidir con el LABEL mencionado en `archisolabel=` parte de `<ISO>\loader\entries\archiso-x86_64.conf`. Este paso es necesario para la ISO Oficial ([Archiso (Español)](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)")). Este paso también se puede realizar utilizando Rufus, durante el paso anterior de «partición y formateo».

*   Extraiga la ISO (de modo similar a como se extrae un archivo ZIP) en la unidad USB (utilizando [7-Zip](http://7-zip.org/)).

*   Descargue los binarios oficiales (archivo zip) mas recientes de syslinux 6.xx desde [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) y extráigalos. La versión de Syslinux debe ser la misma que la versión utilizada en la imagen ISO.

*   Ejecute las siguientes órdenes (en el prompt de órdenes de Windows, como administrador):

```
> cd bios\
> for /r %Y in (*.c32) do copy "%Y" "X:\arch\boot\syslinux\" /y
> copy mbr\*.bin X:\arch\boot\syslinux\ /y

```

*   Instale Syslinux en el USB para poder ejecutarlo (utilice `win64/syslinux64.exe` en Windows x64):

```
> cd bios\
> win32/syslinux.exe -d /boot/syslinux -i -a -m X:

```

**Nota:**

*   El paso anterior instala `ldlinux.sys` de Syslinux en el VBR de la partición USB, establece la partición como activa/arrancable en la tabla de particiones MBR, y escribe el código de arranque del MBR en los primeros 400 bytes, la región del código de arranque del USB.
*   El parámetro `-d` convierte la ruta esperada a la ruta con la barra invertida de separación como en los sistemas *unix.

## Otros métodos para sistemas BIOS

### En GNU/Linux

#### Utilizar una unidad USB multiarranque

Esto permite arrancar múltiples ISO desde un solo dispositivo USB, incluido archiso. Actualizar una unidad USB existente con una ISO más reciente es más simple que con la mayoría de los otros métodos. Consulte [Multiboot USB drive (Español)](/index.php/Multiboot_USB_drive_(Espa%C3%B1ol) "Multiboot USB drive (Español)").

#### Utilizar la utilidad de GNOME «Disk Utility»

Las distribuciones de Linux que ejecutan GNOME pueden crear fácilmente un CD live a través de [nautilus](https://www.archlinux.org/packages/?name=nautilus) y [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility). Basta con hacer clic con el botón secundario del ratón sobre el archivo *.iso*, y seleccionar **Abrir con Disk Image Writer**. Cuando se abra la utilidad de disco de GNOME, especifique la unidad USB en *Destino* del menú desplegable y haga clic en *Iniciar restauración*.

#### Fabricar una unidad USB-ZIP

Para algunos sistemas BIOS antiguos, solo se admite el arranque desde unidades USB-ZIP. Este método le permite arrancar desde una unidad de disco duro USB.

**Advertencia:** esto destruirá toda la información de su unidad USB.

*   Descargue [syslinux](https://www.archlinux.org/packages/?name=syslinux) y [mtools](https://www.archlinux.org/packages/?name=mtools) de los repositorios oficiales.
*   Encuentra la unidad USB con `lsblk`.
*   Escriba `mkdiskimage -4 /dev/sd**x** 0 64 32` (reemplaza x con la letra de su disco). Esto llevará un rato.

Desde aquí continúe con el método de formateo manual. La partición será `/dev/sd**x**4` debido a la forma en que funcionan las unidades ZIP.

**Nota:** no formatee la unidad como FAT32; manténgala como FAT16.

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
```

En `/dev/sd**x1**` debe sustituir **x** con la primera letra libre después de la última letra en uso en el sistema en el que va a instalar Arch Linux (por ejemplo, si tiene dos unidades de disco duro, utilice `c`). Puede hacer este cambio durante la primera fase del arranque pulsando `Tab` cuando se muestra el menú.

### En Windows

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

Una vez que haya determinado qué dispositivo es el correcto, puede grabar la imagen en la unidad, invocando la orden flashnul, con la letra del dispositivo, el parámetro `-L`, y la ruta a la imagen. En este caso, sería:

```
C:\>flashnul **E:** -L *ruta\a\arch.iso*

```

Si está realmente seguro de que desea grabar los datos, escriba *«yes»*, y luego espere un poco para que pueda grabar. Si se obtiene un error de *«access denied error»*, cierre todas las ventanas que tenga abiertas con «Explorer».

Si está en Vista o Win7, debe abrir la consola como administrador, o de lo contrario flashnul fallará al abrir la memoria usb como si fuese un dispositivo de bloque y solo será capaz de grabarlo a través del manejo de la unidad proporcionada por Windows.

**Nota:** necesita utilizar la letra de la unidad en lugar del número. flashnul 1rc1, Windows 7 x64.

#### Cargar el soporte de instalación desde la RAM

Este método utiliza [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)") y un [Ramdisk](/index.php/Tmpfs_(Espa%C3%B1ol) "Tmpfs (Español)") ([MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)) para cargar toda la imagen ISO de Arch Linux ISO en la memoria RAM. Dado que esto se ejecuta por completo desde la memoria del sistema, tendrá que asegurarse de que dicha memoria del sistema cuenta con una cantidad adecuada. Una cantidad mínima de RAM entre 500 MB y 1 GB debería ser suficiente para instalar Arch Linux desde un MEMDISK.

Para obtener más información sobre los requisitos del sistema de Arch Linux, así como los de MEMDISK véase la [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") y [esto](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries). Para referencia, aquí está el [hilo anterior del foro](https://bbs.archlinux.org/viewtopic.php?id=135266).

**Sugerencia:** una vez que se realiza la carga y aparece el menú gráfico se puede simplemente retirar la memoria USB y, tal vez, incluso utilizarla en otro equipo para iniciar el proceso de nuevo. Por lo tanto, utilizar MEMDISK permite también el arranque y la instalación de Arch desde (y para) el mismo soporte USB.

##### Preparar la unidad USB

Formatee la memoria USB con **FAT32** y cree las siguientes carpetas en la unidad recien formateada:

*   `Boot`
    *   `Boot/ISOs`
    *   `Boot/Settings`

##### Copiar los archivos necesarios a la unidad USB

Copie la imagen ISO que desea arrancar a la carpeta `Boot/ISOs`, y extraiga los archivos la última liberación de [syslinux](https://www.archlinux.org/packages/?name=syslinux) desde [aquí](http://www.kernel.org/pub/linux/utils/boot/syslinux/) y cópielos en las siguientes carpetas:

*   `./win32/syslinux.exe` podría ubicarse en el «Escritorio» o en la carpeta «Descargas» de su equipo.

*   `./memdisk/memdisk` iría a la carpeta `Settings` de la unidad USB.

##### Crear el archivo de configuración

Después de copiar los archivos necesarios, navegue por la unidad USB a /boot/Settings y cree un archivo `syslinux.cfg`.

**Advertencia:** en la línea `INITRD`, asegúrese de usar el nombre del archivo ISO que copió en la carpeta `ISOs`.
 `/Boot/Settings/syslinux.cfg` 
```
DEFAULT arch_iso

LABEL arch_iso
        MENU LABEL Arch Setup
        LINUX memdisk
        INITRD /Boot/ISOs/archlinux-2017.04.01-x86_64.iso
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

## Solución de problemas

*   Si aparece el error «device did not show up after 30 seconds» debido a que `/dev/disk/by-label/ARCH_XXXXYY` no se monta, intente cambiar el nombre de su dispositivo USB a `ARCH_XXXXYY` (por ejemplo, `ARCH_201501`).
*   Si obtiene errores, intente usar otro dispositivo USB. Hay escenarios donde se resolvieron los problemas así.

## Véase también

*   [Wiki de Gentoo — LiveUSB/HOWTO](https://wiki.gentoo.org/wiki/LiveUSB/HOWTO)
*   [Fedora wiki — Cómo crear y usar un USB Live](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)
*   [Wiki de openSUSE — SDB:Live USB stick](https://en.opensuse.org/SDB:Live_USB_stick)