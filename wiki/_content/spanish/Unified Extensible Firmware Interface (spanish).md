**Estado de la traducción**
Este artículo es una traducción de [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), revisada por última vez el **2018-08-31**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Unified_Extensible_Firmware_Interface&diff=0&oldid=538790) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)")
*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [GUID Partition Table (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")
*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")

**Advertencia:** Si bien es cieto que la instalación en modalidad UEFI es la opción a la que se tiende, no obstante, hay que advertir que las primeras implementaciones de UEFI «pueden» tener más inconvenientes que beneficios que su opositor BIOS. Por tanto, es recomendable hacer una búsqueda relacionada con su modelo de placa base particular para obtener información sobre la conveniencia de optar por la modalidad UEFI antes de continuar.

La [Unified Extensible Firmware Interface](http://www.uefi.org/) (UEFI o EFI para abreviar) es un nuevo modelo de interfaz para interactuar entre los sistemas operativos y el firmware. Proporciona un entorno estándar para iniciar un sistema operativo y ejecutar aplicaciones previas al inicio.

Es un método distito del comunmente usado «[código de arranque MBR](/index.php/Partitioning#Master_Boot_Record_.28bootstrap_code.29 "Partitioning")» seguido por los sistemas [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS"). Consulte [Arch boot process](/index.php/Arch_boot_process "Arch boot process") para conocer sus diferencias y el proceso de arranque con UEFI. Para configurar los cargadores de arranque UEFI, vea [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders").

## Contents

*   [1 Versiones de UEFI](#Versiones_de_UEFI)
*   [2 Firmware de UEFI](#Firmware_de_UEFI)
    *   [2.1 Sistemas UEFI que no son Mac](#Sistemas_UEFI_que_no_son_Mac)
    *   [2.2 Mac de Apple](#Mac_de_Apple)
*   [3 Configuración de las opciones del kernel de Linux para UEFI](#Configuraci.C3.B3n_de_las_opciones_del_kernel_de_Linux_para_UEFI)
*   [4 Variables de UEFI](#Variables_de_UEFI)
    *   [4.1 Soporte de las variables UEFI en el kernel de Linux](#Soporte_de_las_variables_UEFI_en_el_kernel_de_Linux)
    *   [4.2 Requisitos para que el soporte de las variables UEFI funcione correctamente](#Requisitos_para_que_el_soporte_de_las_variables_UEFI_funcione_correctamente)
        *   [4.2.1 Montar efivarfs](#Montar_efivarfs)
    *   [4.3 Herramientas en el espacio de usuario](#Herramientas_en_el_espacio_de_usuario)
        *   [4.3.1 efibootmgr](#efibootmgr)
*   [5 Intérprete de órdenes UEFI](#Int.C3.A9rprete_de_.C3.B3rdenes_UEFI)
    *   [5.1 Obtener el intérprete de órdenes UEFI](#Obtener_el_int.C3.A9rprete_de_.C3.B3rdenes_UEFI)
    *   [5.2 Lanzar el intérprete de órdenes UEFI](#Lanzar_el_int.C3.A9rprete_de_.C3.B3rdenes_UEFI)
    *   [5.3 Órdenes importantes del intérprete UEFI](#.C3.93rdenes_importantes_del_int.C3.A9rprete_UEFI)
        *   [5.3.1 bcfg](#bcfg)
        *   [5.3.2 map](#map)
        *   [5.3.3 edit](#edit)
*   [6 Soporte para arrancar UEFI](#Soporte_para_arrancar_UEFI)
    *   [6.1 Crear un USB arrancable con UEFI desde la ISO](#Crear_un_USB_arrancable_con_UEFI_desde_la_ISO)
    *   [6.2 Eliminar el apoyo de arranque de UEFI de una unidad óptica](#Eliminar_el_apoyo_de_arranque_de_UEFI_de_una_unidad_.C3.B3ptica)
    *   [6.3 Arrancar el kernel de 64-bit en UEFI de 32-bit](#Arrancar_el_kernel_de_64-bit_en_UEFI_de_32-bit)
        *   [6.3.1 Utilizar GRUB](#Utilizar_GRUB)
*   [7 Probar UEFI en sistemas sin soporte nativo](#Probar_UEFI_en_sistemas_sin_soporte_nativo)
    *   [7.1 OVMF para máquinas virtuales](#OVMF_para_m.C3.A1quinas_virtuales)
    *   [7.2 DUET para sistemas BIOS únicamente](#DUET_para_sistemas_BIOS_.C3.BAnicamente)
*   [8 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [8.1 Windows 7 no se inicia en la modalidad UEFI](#Windows_7_no_se_inicia_en_la_modalidad_UEFI)
    *   [8.2 Windows cambia el orden de arranque](#Windows_cambia_el_orden_de_arranque)
    *   [8.3 El soporte USB se topa con una pantalla negra](#El_soporte_USB_se_topa_con_una_pantalla_negra)
    *   [8.4 El cargador de arranque UEFI no aparece en el menú del firmware](#El_cargador_de_arranque_UEFI_no_aparece_en_el_men.C3.BA_del_firmware)
*   [9 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Versiones de UEFI

*   UEFI comenzó como EFI de Intel en las versiones 1.x.
*   Luego, un grupo de empresas denominado UEFI Forum, se hizo cargo de su desarrollo, a partir del cual se llamó EFI Unificado desde de la versión 2.0.
*   Salvo que se especifique expresamente como EFI 1.x, los términos EFI y UEFI se utilizarán indistintamente para referirse al firmware 2.x de UEFI .
*   La implementación EFI de Apple no es ni la versión 1.x de EFI ni la versión 2.x, sino una combinación de ambas. Este tipo de firmware no entra dentro de ninguna versión de la especificación (U)EFI uno y, por lo tanto, no es un estándar del firmware de UEFI. A menos que se indique explícitamente, estas instrucciones son generales y algunas de ellas pueden no funcionar o pueden ser diferentes en [Apple Macs](/index.php/MacBook "MacBook").

La última especificación de UEFI se puede encontrar en [http://uefi.org/specifications](http://uefi.org/specifications).

## Firmware de UEFI

Con UEFI, cada programa, ya sea un cargador de sistema operativo o una utilidad (por ejemplo, una aplicación de prueba de memoria o una herramienta de recuperación), debe ser una aplicación EFI correspondiente a la arquitectura/bitness del firmware de UEFI.

La gran mayoría de los firmwares UEFI, incluidos los recientes Macs de Apple, usan el firmware UEFI x86_64\. Los únicos dispositivos conocidos que utilizan UEFI IA32 (32 bits) son Apple Mac antiguos (anteriores a 2008), algunos ultrabooks Intel Cloverfield y algunas tarjetas del servidor Intel antiguo que se sabe que operan con firmware Intel EFI 1.10.

Un firmware UEFI x86_64 no incluye soporte para el inicio de aplicaciones EFI de 32 bits (a diferencia de las versiones de Linux y Windows x86_64, que incluyen dicho soporte). Por lo tanto, la aplicación EFI debe compilarse para el firmware de esa específica arquitectura del procesador.

### Sistemas UEFI que no son Mac

Compruebe si el directorio `/sys/firmware/efi` existe; si existe, significa que el kernel ha arrancado en modalidad UEFI. En ese caso, se presumirá que la arquitectura de UEFI coincidirá con la del kernel (es decir, i686 o x86_64)

**Nota:** El chip del sistema Atom de Intel es entregado con UEFI de 32 bit (desde el 2 de noviembre de 2013). Véase [esta página](#Arrancar_el_kernel_de_64-bit_en_UEFI_de_32-bit) para obtener más información. Vea también [esta publicación del blog de Intel](https://software.intel.com/en-us/blogs/2015/07/22/why-cheap-systems-run-32-bit-uefi-on-x64-systems).

### Mac de Apple

Los [Mac](/index.php/Mac "Mac") anteriores a 2008 tienen, en su mayoría, un firware IA32 EFI, mientras que los Mac >=2008 tienen, en su mayoría, x86_64 EFI. Todos los Mac capaces de ejecutar el kernel de Mac OS X Snow Leopard de 64-bit tienen un firmware EFI 1.x para x86_64.

Para saber la arquitectura del firmware EFI en un Mac, debe arrancar Mac OS X y escribir en un terminal la siguiente orden:

```
$ ioreg -l -p IODeviceTree | grep firmware-abi

```

Si la orden devuelve EFI32, entonces es el firmware EFI IA32 (32 bits). Si devuelve EFI64, entonces es el firmware EFI x86_64\. La mayoría de los Mac no tienen firmware UEFI 2.x ya que la implementación de EFI de Apple no es totalmente compatible con la especificación UEFI 2.x.

## Configuración de las opciones del kernel de Linux para UEFI

Las opciones requeridas para la configuración del kernel de Linux para sistemas UEFI son:

```
CONFIG_RELOCATABLE=y
CONFIG_EFI=y
CONFIG_EFI_STUB=y
CONFIG_FB_EFI=y
CONFIG_FRAMEBUFFER_CONSOLE=y

```

*   Soporte para las *Variables Runtime de UEFI* (el sistema de archivos **efivarfs** —`/sys/firmware/efi/efivars`—). Esta opción es importante, ya que es necesaria para manipular las variables runtime de UEFI usando herramientas como `/usr/bin/efibootmgr`. La opción de configuración siguiente está añadida en el kernel 3.10 y posterior.: `CONFIG_EFIVAR_FS=y` 

*   Soporte para las *Variables Runtime de UEFI* (la interfaz antigua **efivars sysfs** —`/sys/firmware/efi/vars`—). Esta opción debe ser desactivada para evitar posibles problemas entre efivarfs con sysfs-efivars activados.: `CONFIG_EFI_VARS=n` 

*   Opción de configuración de [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) —necesaria para dar soporte a UEFI—: `CONFIG_EFI_PARTITION=y` 

Obtenido de [https://www.kernel.org/doc/Documentation/x86/x86_64/uefi.txt](https://www.kernel.org/doc/Documentation/x86/x86_64/uefi.txt).

**Nota:** Todas las opciones anteriores son necesarias para arrancar Linux con UEFI, y están activadas en los [kernels](/index.php/Kernels "Kernels") de ArchLinux presentes en los repositorios oficiales.

## Variables de UEFI

UEFI define las variables como la interacción de un sistema operativo con el firmware. Las variables de arranque de UEFI (*«UEFI Boot Variables»*) son utilizadas por el cargador de arranque y por el sistema operativo únicamente durante la primera fase de arranque. Las variables «*runtime*» de UEFI permiten a un sistema operativo gestionar ciertos ajustes del firmware, como la gestión del arranque de UEFI o la gestión de las claves para el protocolo «*Boot Secure*» de UEFI, etc. Se puede obtener el listado de las variables utilizando:

```
$ efivar --list

```

### Soporte de las variables UEFI en el kernel de Linux

El kernel de Linux expone los datos de las variables UEFI en el espacio de usuario a través de la interfaz **efivarfs** (**EFI** **VAR**iable **F**ile**S**ystem) (`CONFIG_EFIVAR_FS`) —montada utilizando el módulo del kernel `efivarfs` en `/sys/firmware/efi/efivars`— no tiene límite de tamaño máximo y admite las variables «*Secure Boot*» de UEFI. Introducido en kernel 3.8.

### Requisitos para que el soporte de las variables UEFI funcione correctamente

1.  La [arquitectura](#Firmware_de_UEFI) del procesador del Kernel y del procesador de UEFI deben coincidir.
2.  El kernel debe arrancar en modo EFI (a través de [EFISTUB](/index.php/EFISTUB "EFISTUB") o de cualquier otro [gestor de arranque EFI](/index.php/Boot_loader "Boot loader"), no a través de BIOS/CSM o «bootcamp» de Apple que también es BIOS/CSM)
3.  El soporte para EFI Runtime Services debe estar presente en el kernel (`CONFIG_EFI=y`, compruebe si están presente con `zgrep CONFIG_EFI /proc/config.gz`).
4.  Los EFI Runtime Services del kernel NO DEBEN ser desactivados a través de un terminal, es decir, el parámetro `noefi` del kernel NO DEBE ser usado.
5.  El sistema de archivos `efivarfs` debe estar montado en `/sys/firmware/efi/efivars`, en otro caso, debe [montar efivarfs](#Montar_efivarfs).
6.  `efivar` debe mostar (con la opción `-l`) las variables EFI sin ningún error.

Si el soporte para las variables de EFI no funciona, incluso después de cumplirse las condiciones precedentes, pruebe las siguientes soluciones:

1.  Si cualquier herramienta del espacio de usuario no puede modificar los datos de las variables de EFI, compruebe la existencia de archivos en `/sys/firmware/efi/efivars/dump-*`. Si existen, elimínelos, reinicie y vuelva a intentarlo de nuevo.
2.  Si el paso anterior no resuelve el problema, intente arrancar con el parámetro del kernel `efi_no_storage_paranoia` para desactivar la variable efi del kernel que comprueba el espacio de almacenamiento, la cual puede impedir la escritura/modificación de las variables de efi.

**Advertencia:** `efi_no_storage_paranoia` solo debe utilizarse cuando sea necesario y no se debe dejar como una opción de arranque normal. El efecto de este parámetro en la línea de órdenes del kernel cancela una garantía que se pone en marcha para ayudar a evitar la saturación de las máquinas cuando NVRAM se llena demasiado.

#### Montar efivarfs

Si `efivarfs` no se monta automáticamente en `/sys/firmware/efi/efivars` por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") durante el arranque, entonces necesita montarla manualmente para dejar expuesto el soporte para las variables de UEFI a las herramientas del espacio de usuario tales como *efibootmgr*:

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars

```

**Nota:** La orden anterior debe ejecutarse tanto **fuera (antes)** como **dentro** de [chroot](/index.php/Chroot "Chroot"), si procede.

Consulte [efivarfs.txt](https://www.kernel.org/doc/Documentation/filesystems/efivarfs.txt) para documentarse más sobre el kernel.

### Herramientas en el espacio de usuario

Existen algunas herramientas que permiten acceder/modificar las variables UEFI, como:

*   **efivar** — Herramienta y biblioteca para modificar las variables de UEFI (utilizada por efibootmgr)

	[https://github.com/rhboot/efivar](https://github.com/rhboot/efivar) || [efivar](https://www.archlinux.org/packages/?name=efivar), [efivar-git](https://aur.archlinux.org/packages/efivar-git/)

*   **efibootmgr** — Herramienta para modificar las configuraciones del gestor de arranque del firmware de UEFI

	[https://github.com/rhboot/efibootmgr](https://github.com/rhboot/efibootmgr) || [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)

*   **uefivars** — Vuelca un listado de las variables de EFI con alguna información adicional sobre la PCI (utiliza el código de efibootmgr)

	[https://github.com/fpmurphy/Various/tree/master/uefivars-2.0](https://github.com/fpmurphy/Various/tree/master/uefivars-2.0) || [uefivars-git](https://aur.archlinux.org/packages/uefivars-git/)

*   **efitools** — Herramientas para manipular las plataformas de *secure boot* de UEFI

	[https://git.kernel.org/pub/scm/linux/kernel/git/jejb/efitools.git](https://git.kernel.org/pub/scm/linux/kernel/git/jejb/efitools.git) || [efitools](https://www.archlinux.org/packages/?name=efitools)

*   **Suite de comprobación de firmware, de Ubuntu** — Conjunto de herramientas de comprobación que realiza verificaciones de estado en el firmware de ordenadores con Intel/AMD

	[https://wiki.ubuntu.com/FirmwareTestSuite/](https://wiki.ubuntu.com/FirmwareTestSuite/) || [fwts-git](https://aur.archlinux.org/packages/fwts-git/)

#### efibootmgr

**Nota:**

*   Si `efibootmgr` no funciona en absoluto en su sistema, puede reiniciar en el [intérprete de órdenes UEFI](#Int.C3.A9rprete_de_.C3.B3rdenes_UEFI) y utilizar la orden `bcfg` para crear una entrada de arranque en el gestor de arranque.
*   Si no es posible usar `efibootmgr`, algunos firmwares UEFI permiten a los usuarios gestionar directamente las entradas de inicio de UEFI desde la interfaz que aparece durante el arranque. Por ejemplo, algunas BIOS de ASUS tienen una opción llamada «Add New Boot Option» (*«Añadir nueva opción de arranque»*) que permite seleccionar una partición de sistema EFI local e introducir manualmente la ubicación del código de EFI (por ejemplo `\EFI\refind\refind_x64.efi`).
*   Las siguientes órdenes utilizan el cargador de arranque [rEFInd](/index.php/REFInd "REFInd") como ejemplo.

Para añadir una nueva opción de arranque usando *efibootmgr*, necesita saber tres cosas:

1.  El disco que contiene la [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") (ESP): `/dev/sd*X*`
2.  El número de partición de la ESP en ese disco: la `*Y*` en `/dev/sdX*Y*`
3.  La ruta a la aplicación EFI (relativa a la raíz de la ESP)

Por ejemplo, si desea agregar una opción de arranque para `/efi/EFI/refind/refind_x64.efi` donde `/efi` es el punto de montaje de la partición ESP, ejecute:

 `$ findmnt /efi` 
```
TARGET SOURCE    FSTYPE OPTIONS
/efi   /dev/sda1 vfat   rw,flush,tz=UTC
```

En este ejemplo, esto indica que la partición ESP está en el disco `/dev/sda` y el número de la partición es 1\. La ruta a la aplicación EFI relativa a la raíz de la ESP es `/EFI/refind/refind_x64.efi`. Sabiendo esto, se crearía la entrada de arranque de la siguiente manera:

```
# efibootmgr --create --disk /dev/sda --part 1 --loader /EFI/refind/refind_x64.efi --label "rEFInd Boot Manager" --verbose

```

Consulte [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8) o el archivo [README de efibootmgr](https://raw.githubusercontent.com/rhinstaller/efibootmgr/master/README) para obtener más información.

**Nota:** UEFI utiliza una barra invertida `\` como separador de ruta, pero *efibootmgr* convierte automáticamente los separadores de ruta en barra normal `/` al estilo UNIX.

## Intérprete de órdenes UEFI

El intérprete de órdenes de UEFI es una intérprete/terminal para el firmware, que permite ejecutar aplicaciones UEFI que incluyen los cargadores de arranque UEFI. Aparte de esto, el intérprete también se puede utilizar para obtener información variada sobre el sistema o del firmware del mapa de la memoria (memmap), modificar las variables del gestor de arranque (bcfg), ejecutar programas de gestión de particiones (diskpart), cargar los controladores UEFI, editar archivos de texto (edit), hexedit, etc.

### Obtener el intérprete de órdenes UEFI

Puede descargar un intérprete de órdenes UEFI con licencia BSD de Tianocore de Intel desde el proyecto UDK/EDK2.

*   Paquete de [AUR](/index.php/AUR "AUR") [uefi-shell-git](https://aur.archlinux.org/packages/uefi-shell-git/) (recomendado) —proporciona la shell x86_64 para x86_64 (64-bit) de UEFI y la shell IA32 para IA32 (32-bit) de UEFI— compilado directamente de la última fuente de TianoCore EDK2.
*   Hay copias de la shell v1 y v2 en el directorio EFI en la imagen de instalación de Arch.
*   [Binarios precompilados de la shell v2 de UEFI](https://github.com/tianocore/edk2/tree/master/ShellBinPkg) (puede no estar actualizado).
*   [Binarios precompilados de UEFI Shell v1](https://github.com/tianocore/edk2/tree/master/EdkShellBinPkg) (no actualizado por los desarrolladores).
*   [Binario precompilado de la shell v2 de UEFI con bcfg modificado para trabajar con el firmware UEFI pre-2.3](https://ptpb.pw/~Shell2.zip) —del cargador de arranque Clover EFI—.

La versión 2.0 de la shell únicamente funciona en sistemas UEFI 2.3 + y se recomienda su uso con preferencia a la shell 1.0 en esos sistemas. La versión 1.3 de la shell debería funcionar en todos los sistemas UEFI, independientemente de la especificación de la versión del firmware. Más información en [ShellPkg](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=ShellPkg) y [este correo](http://sourceforge.net/mailarchive/message.php?msg_id=28690732).

### Lanzar el intérprete de órdenes UEFI

Algunas placas base Asus y otras basadas en el firmware UEFI AMI Aptio x86_64 (de Sandy Bridge en adelante) ofrecen una opción llamada `«Launch EFI Shell from filesystem device»`. Para estas placas base, descargue la shell de UEFI x86_64 y cópiela a la partición del sistema UEFI renombrándola como `<UEFI_SYSTEM_PARTITION>/shellx64.efi` (normalmente en la carpeta `/boot/efi/shellx64.efi`).

Los sistemas con un firmware UEFI Phoenix SecureCore Tiano se sabe que llevan integrada la shell de UEFI, la cual se puede iniciar presionando las teclas `F6`, `F11` o `F12`.

**Nota:** Si es incapaz de lanzar la shell de UEFI directamente desde el firmware mediante cualquiera de los métodos mencionados anteriormente, cree una unidad USB formateada con FAT32 conteniendo la `Shell.efi`, copiada con la ruta `(USB)/efi/boot/bootx64.efi`. Este USB debería aparecer en el menú de arranque del firmware. La inicialización de esta opción lanzará la shell de UEFI.

### Órdenes importantes del intérprete UEFI

Las órdenes del intérprete UEFI generalmente dan soporte a la opción `-b` que hace una pausa después de la salida de cada página. Ejecute `help -b` para ver las órdenes disponibles.

Puede obtener más información en [http://software.intel.com/en-us/articles/efi-shells-and-scripting/](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)

#### bcfg

La orden `bcfg` se utiliza para modificar las entradas en la NVRAM de UEFI, lo que permite cambiar las entradas de arranque o las opciones del controlador. Esta orden se describe con detalle en la página 83 (sección 5.3) del documento [UEFI Shell Specification 2.0](http://www.uefi.org/sites/default/files/resources/UEFI_Shell_Spec_2_0.pdf)

**Nota:**

*   Se recomienda probar `bcfg` únicamente si `efibootmgr` no puede crear entradas de inicio que funcionen en el propio sistema.
*   La versión 1 del binario oficial del intérprete de órdenes UEFI no proporciona soporte para la orden `bcfg`. Consulte [#Obtener el intérprete de órdenes UEFI](#Obtener_el_int.C3.A9rprete_de_.C3.B3rdenes_UEFI) para un binario UEFI shell v2 modificado que puede funcionar en UEFI con firmwares anteriores a 2.3.

Para conocer una lista de entradas de arranque actuales:

```
Shell> bcfg boot dump -v

```

Para añadir una entrada para rEFInd (por ejemplo) como cuarta (la numeración empieza desde cero) en el menú de arranque:

```
Shell> bcfg boot add 3 FS0:\EFI\refind\refind_x64.efi "rEFInd"

```

donde `FS0:` es la asignación correspondiente a la partición del sistema UEFI y `FS0:\EFI\refind\refind_x64.efi` es el archivo que se pondrá en marcha.

Para agregar una entrada con el fin de iniciar directamente su sistema, sin un gestor de arranque, configure una opción de arranque utilizando su kernel como [EFISTUB](/index.php/EFISTUB#UEFI_Shell "EFISTUB"):

```
Shell> bcfg boot add **N** fs**V**:\vmlinuz-linux "Arch Linux"
Shell> bcfg boot -opt **N** "root=**/dev/sdX#** initrd=\initramfs-linux.img"

```

donde `N` es la prioridad, `V` es el número de volumen donde se encuetra la partición de sistema EFI, y `/dev/sdX#` es la partición raíz.

Para quitar la opción de arranque cuarta:

```
Shell> bcfg boot rm 3

```

Para mover la opción de arranque #3 a #0 (es decir, a la primera posición o la entrada por defecto en el menú de inicio de UEFI):

```
Shell> bcfg boot mv 3 0

```

Para mostrar el texto de ayuda de bcfg:

```
Shell> help bcfg -v -b

```

o

```
Shell> bcfg -? -v -b

```

#### map

La orden `map` muestra un mapeado de los dispositivos, es decir, los nombres de los sistemas de archivos disponibles (`FS0`) y los dispositivos de almacenamiento (`blk0`).

Antes de ejecutar órdenes relacionadas con el sistema de archivos, como `cd` o `ls`, debe cambiar el intérprete de órdenes al sistema de archivos correspondiente, escribiendo su nombre:

```
Shell> FS0:
FS0:\> cd EFI/

```

#### edit

La orden `edit` proporciona un editor de texto básico, con una interfaz similar al editor de texto nano, pero ligeramente menos funcional. Maneja codificación UTF-8 y se hace cargo del final de la línea LF frente a [CRLF](https://en.wikipedia.org/wiki/es:CRLF "wikipedia:es:CRLF").

Para editar, por ejemplo, `refind.conf` de rEFInd en la partición del sistema UEFI (FS0: en el firmware):

```
Shell> edit FS0:\EFI\refind\refind.conf

```

Escriba `Ctrl-E` para obtener ayuda.

## Soporte para arrancar UEFI

### Crear un USB arrancable con UEFI desde la ISO

Siga las instrucciones del siguiente artículo [USB Installation Media (Español)#Crear USB para arrancar desde sistemas BIOS y UEFI](/index.php/USB_Installation_Media_(Espa%C3%B1ol)#Crear_USB_para_arrancar_desde_sistemas_BIOS_y_UEFI "USB Installation Media (Español)")

### Eliminar el apoyo de arranque de UEFI de una unidad óptica

**Nota:** Esta sección menciona la eliminación de la ayuda de arranque UEFI desde un **CD/DVD únicamente** (soporte óptico), no desde una unidad flash USB.

La mayoría de los Mac EFI de 32-bit y algunos Mac EFI de 64 bits se niegan a arrancar desde un CD/DVD bootable con una combinación de UEFI(X64)+BIOS. Si se desea continuar con la instalación con soportes ópticos, puede que sea necesario, primero, eliminar el apoyo a UEFI.

*   Monte el soporte de instalación oficial y obtenga el `archisolabel` como se muestra en la sección anterior.

```
# mount -o loop *input.iso* /mnt/iso

```

*   Después reconstruya la ISO, excluyendo el soporte de arranque de UEFI de la imágen destinada al disco óptico, utilizando `xorriso` de [libisoburn](https://www.archlinux.org/packages/?name=libisoburn). Asegúrese de configurar el archisolabel correcto, por ejemplo «ARCH_201411» o similar:

```
$ xorriso -as mkisofs -iso-level 3 \
    -full-iso9660-filenames\
    -volid "*archisolabel*" \
    -appid "Arch Linux CD" \
    -publisher "Arch Linux <[https://www.archlinux.org](https://www.archlinux.org)>" \
    -preparer "prepared by $USER" \
    -eltorito-boot isolinux/isolinux.bin \
    -eltorito-catalog isolinux/boot.cat \
    -no-emul-boot -boot-load-size 4 -boot-info-table \
    -isohybrid-mbr "/mnt/iso/isolinux/isohdpfx.bin" \
    -output *output.iso* /mnt/iso/
```

*   Grabe `*output.iso*` en el disco óptico y continúe con la instalación de forma normal.

### Arrancar el kernel de 64-bit en UEFI de 32-bit

La imagen ISO oficial ([Archiso](/index.php/Archiso "Archiso")) no admite el arranque en sistemas UEFI de 32 bits ([FS#53182](https://bugs.archlinux.org/task/53182)) ya que utiliza EFISTUB (a través del administrador de arranque [systemd-boot](/index.php/Systemd-boot "Systemd-boot") para el menú) para arancar el kernel en modo UEFI. Para arrancar un kernel de 64 bits con UEFI de 32 bits, debe usar un gestor de arranque que no se base en el código de arranque de EFI para lanzar los kernel.

**Sugerencia:** la imagen iso de [Archboot](/index.php/Archboot "Archboot") admite el arranque en sistemas UEFI de 32 bits.

#### Utilizar GRUB

Esta sección describe cómo configurar [GRUB](/index.php/GRUB "GRUB") como el cargador de arranque UEFI del USB.

*   [Crear una instalación en un soporte USB modificable](/index.php/USB_flash_installation_media#Using_manual_formatting "USB flash installation media"). Como vamos a usar GRUB, solo tiene que seguir los pasos hasta la parte donde empieza la explicación de `syslinux`.

*   [Crear una imagen independiente de GRUB](/index.php/GRUB/Tips_and_tricks#GRUB_standalone "GRUB/Tips and tricks") para sistemas UEFI de 32 bits:

```
# echo 'configfile ${cmdpath}/grub.cfg' > /tmp/grub.cfg
# grub-mkstandalone -d /usr/lib/grub/i386-efi -O i386-efi --modules="part_gpt part_msdos" --locales="en@quot" --themes="" -o "*/mnt/usb/*EFI/boot/bootia32.efi" "boot/grub/grub.cfg=/tmp/grub.cfg" -v

```

*   Cree `*/mnt/usb*/EFI/boot/grub.cfg` con los siguientes contenidos (sustituya `ARCH_YYYYMM` con la etiqueta archiso adecuada, por ejemplo `ARCH_201507`):

**Sugerencia:**

*   La etiqueta archiso se puede obtener del archivo *.iso* con la herramienta `isoinfo` del paquete [cdrtools](https://www.archlinux.org/packages/?name=cdrtools), o `iso-info` de [libcdio](https://www.archlinux.org/packages/?name=libcdio).
*   Las entradas de configuración dadas también pueden ingresarse dentro de una [shell de GRUB](/index.php/GRUB#Using_the_command_shell "GRUB").

Para el ISO oficial:

 `*/mnt/usb*/EFI/boot/grub.cfg` 
```
insmod part_gpt
insmod part_msdos
insmod fat

insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus

insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
    insmod gfxterm
    set gfxmode="1024x768x32;auto"
    terminal_input console
    terminal_output gfxterm
fi

menuentry "Arch Linux archiso x86_64 UEFI USB" {
    set gfxpayload=keep
    search --no-floppy --set=root --label *ARCH_YYYYMM*
    linux /arch/boot/x86_64/vmlinuz archisobasedir=arch archisolabel=*ARCH_YYYYMM* add_efi_memmap
    initrd /arch/boot/intel_ucode.img /arch/boot/x86_64/archiso.img
}
```

## Probar UEFI en sistemas sin soporte nativo

### OVMF para máquinas virtuales

[OVMF](https://tianocore.github.io/ovmf/) es un proyecto de TianoCore destinado a activar la compatibilidad de UEFI para máquinas virtuales. OVMF contiene una muestra de firmware UEFI para QEMU.

Se puede instalar [ovmf](https://www.archlinux.org/packages/?name=ovmf) desde el repositorio extra.

Es [recomendable](https://www.linux-kvm.org/downloads/lersek/ovmf-whitepaper-c770f8c.txt) hacer una copia local del conjunto de variables no volátiles para su máquina virtual:

```
$ cp /usr/share/ovmf/x64/OVMF_VARS.fd my_uefi_vars.bin

```

Para usar el firmware OVMF y el conjunto de variables, añada la siguiente orden a su QEMU:

```
-drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/x64/OVMF_CODE.fd \
-drive if=pflash,format=raw,file=my_uefi_vars.bin

```

Por ejemplo:

```
$ qemu-system-x86_64 -enable-kvm -m 1G -drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/x64/OVMF_CODE.fd -drive if=pflash,format=raw,file=my_uefi_vars.bin …

```

### DUET para sistemas BIOS únicamente

DUET es un proyecto TianoCore que permite cargar en cadena un entorno UEFI completo desde un sistema BIOS, de manera similar al arranque de los sistemas operativos en entorno BIOS. Este método se está discutiendo ampliamente en [http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/](http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/) . Imágenes DUET precompiladas se pueden descargar de uno de los repositorios de [https://gitorious.org/tianocore_uefi_duet_builds](https://gitorious.org/tianocore_uefi_duet_builds). Instrucciones específicas para la creación de DUET están disponible en [https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt](https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt) .

También puede probar [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/) que proporciona imágenes DUET modificadas que puedan contener algunos arreglos específicos del sistema y son más frecuentemente actualizadas en comparación con las de los repositorios gitorious.

## Solución de problemas

### Windows 7 no se inicia en la modalidad UEFI

Si tiene instalado Windows en un disco duro con particionado GPT y sigue teniendo otro disco duro diferente con particionado MBR en su ordenador, entonces es posible que el firmware (UEFI) está dando su apoyo CSM a este último (para arrancar particiones MBR) y por ello Windows no arranca. Para resolver este problema convierta el particionado de su disco MBR a GPT, o desactive el puerto SATA del disco duro cuando esté conectado, o bien, desenchufe el puerto SATA de este disco duro.

Placas base con este tipo de problema:

*   Gigabyte Z77X-UD3H rev. 1.1 (BIOS UEFI versión F19e)

*   *   La opción *«UEFI Only»* de la BIOS UEFI no pretende hacer que la BIOS UEFI arranque desde CSM.

### Windows cambia el orden de arranque

Si el [arranque dual con Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") y su placa base solo inicia Windows de forma inmediata en lugar mostrar la elección de su aplicación EFI, existen varias causas posibles y soluciones alternativas.

*   Asegúrese de que el [inicio rápido](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") esté desactivado en las opciones de energía de Windows
*   Asegúrese de que [Secure Boot](/index.php/Secure_Boot "Secure Boot") esté desactivado en su BIOS (si no está utilizando un gestor de arranque firmado)
*   Asegúrese de que el orden de arranque de UEFI no tiene establecido primero «*Windows Boot Manager*» utilizando, por ejemplo, [#efibootmgr](#efibootmgr) and what you see in the configuration tool of the UEFI. Algunas placas base anulan, por defecto, cualquier configuración establecida con efibootmgr por Windows, si la detecta. Esto se confirma en una computadora portátil Packard Bell.
*   Si su placa base está iniciando la ruta de inicio predeterminada (`\EFI\BOOT\BOOTX64.EFI`), este archivo puede haber sido sobrescrito con el cargador de arranque de Windows. Intente configurar la ruta de inicio correcta, por ejemplo utilizando [#efibootmgr](#efibootmgr).
*   Si los pasos anteriores no funcionan, puede decirle al gestor de arranque de Windows que ejecute una aplicación EFI diferente. Desde un prompt de órdenes de «Windows Administrator»: `# bcdedit /set "{bootmgr}" path "\EFI\*path*\*to*\*app.efi*"` 
*   Alternativamente, puede establecer una secuencia de órdenes de inicio en Windows que garantice que el orden de inicio esté configurado correctamente cada vez que inicie Windows.
    1.  Abra un promtp de órdenes (símbolo del sistema) con privilegios de administrador. Ejecute `bcdedit /enum firmware` y encuentre la entrada de inicio deseada.
    2.  Copie el Identificador, incluidos los corchetes, por ejemplo `{31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`
    3.  Cree un archivo por lotes con la siguiente orden `bcdedit /set "{fwbootmgr}" DEFAULT "{*copied boot identifier*}"`
    4.  Abra *gpedit.msc* y en *Local Computer Policy > Computer Configuration > Windows Settings > Scripts(Startup/Shutdown)*, seleccione *Startup*
    5.  En la pestaña *Scripts*, seleccione el botón *Add*, y seleccione su archivo por lotes.

### El soporte USB se topa con una pantalla negra

Este problema puede ocurrir debido a un problema con [KMS](/index.php/KMS "KMS"). Pruebe [desactivar KMS](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting") mientras arranca el USB.

### El cargador de arranque UEFI no aparece en el menú del firmware

En ciertas placas base UEFI, como algunas placas con un chipset Intel Z77, agregar entradas con `efibootmgr` o `bcfg` desde la shell de UEFI no funcionará, porque no aparecerán en la lista del menú de arranque después de haber sido agregadas a NVRAM.

Este problema se debe a que las placas base solo pueden cargar Microsoft Windows. Para resolver esto, debe colocar el archivo *.efi* en la ubicación que usa Windows.

Copie el archivo `bootx64.efi` del soporte de instalación de Arch Linux (`FSO:`) en el directorio de Microsoft de la partición [ESP](/index.php/ESP "ESP") de su disco duro (`FS1:`). Haga esto arrancando la shell EFI y escribiendo:

```
Shell> mkdir FS1:\EFI\Microsoft
Shell> mkdir FS1:\EFI\Microsoft\Boot
Shell> cp FS0:\EFI\BOOT\bootx64.efi FS1:\EFI\Microsoft\Boot\bootmgfw.efi

```

Después del reinicio, las entradas agregadas a la NVRAM deben aparecer en el menú de inicio.

## Véase también

*   [Wikipedia:UEFI](https://en.wikipedia.org/wiki/UEFI "wikipedia:UEFI")
*   [UEFI Forum](http://www.uefi.org/home/) - contains the official [UEFI Specifications](http://uefi.org/specifications) - GUID Partition Table is part of UEFI Specification
*   [UEFI boot: how does that actually work, then? - A blog post by AdamW](https://www.happyassassin.net/2014/01/25/uefi-boot-how-does-that-actually-work-then/)
*   [Linux Kernel x86_64 UEFI Documentation](https://www.kernel.org/doc/Documentation/x86/x86_64/uefi.txt)
*   [Intel's page on EFI](https://www.intel.com/content/www/us/en/architecture-and-technology/unified-extensible-firmware-interface/efi-homepage-general-technology.html)
*   [Intel Architecture Firmware Resource Center](https://firmware.intel.com/)
*   [Matt Fleming - The Linux EFI Boot Stub](https://firmware.intel.com/blog/linux-efi-boot-stub)
*   [Matt Fleming - Accessing UEFI Variables from Linux](https://firmware.intel.com/blog/accessing-uefi-variables-linux)
*   [Rod Smith - Linux on UEFI: A Quick Installation Guide](http://www.rodsbooks.com/linux-uefi/)
*   [UEFI Boot problems on some newer machines (LKML)](https://lkml.org/lkml/2011/6/8/322)
*   [LPC 2012 Plumbing UEFI into Linux](https://linuxplumbers.ubicast.tv/videos/plumbing-uefi-into-linux/)
*   [LPC 2012 UEFI Tutorial : part 1](https://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-1/)
*   [LPC 2012 UEFI Tutorial : part 2](https://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-2/)
*   [Intel's TianoCore Project](http://www.tianocore.org/) for Open-Source UEFI firmware which includes DuetPkg for direct BIOS based booting and OvmfPkg used in QEMU and Oracle VirtualBox
*   [FGA: The EFI boot process](https://jdebp.eu/FGA/efi-boot-process.html)
*   [Microsoft's Windows and GPT FAQ](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-and-gpt-faq)
*   [Convert Windows x64 from BIOS-MBR mode to UEFI-GPT mode without Reinstall](https://gitlab.com/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/wikis/Windows_x64_BIOS_to_UEFI)
*   [Create a Linux BIOS+UEFI and Windows x64 BIOS+UEFI bootable USB drive](https://gitlab.com/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/wikis/Linux_Windows_BIOS_UEFI_boot_USB)
*   [Rod Smith - A BIOS to UEFI Transformation](http://rodsbooks.com/bios2uefi/)
*   [EFI Shells and Scripting - Intel Documentation](https://software.intel.com/en-us/articles/efi-shells-and-scripting/)
*   [UEFI Shell - Intel Documentation](https://software.intel.com/en-us/articles/uefi-shell/)
*   [UEFI Shell - bcfg command info](http://www.hpuxtips.es/?q=node/293)