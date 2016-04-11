**Unified Extensible Firmware Interface** (o UEFI para abreviar) es un nuevo tipo de firmware que fue diseñado inicialmente por Intel (conocido con el nombre de EFI entonces) principalmente para los sistemas basados ​​en Itanium. Se introdujeron así nuevas formas de arrancar un sistema operativo distintas del método usado comúnmente desde el «código de arranque del [MBR](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)")», seguido por los sistemas [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS"). Comenzó como EFI de Intel en las versiones 1.x y luego, un grupo de empresas denominado UEFI Forum, se hizo cargo de su desarrollo, a partir del cual se llamó EFI Unificado desde de la versión 2.0\. Hasta el 24 de julio de 2013, la Especificación 2.4 de UEFI (liberada el 11 de julio de 2013) es la versión más reciente.

**Nota:**

*   Esta página explica **qué es UEFI** y **el apoyo de UEFI en el kernel de Linux**. No describe la configuración de los gestores de arranque UEFI. Para obtener esta última información consulte [Boot loaders](/index.php/Boot_loaders "Boot loaders").
*   Salvo que se especifique expresamente como EFI 1.x, los términos EFI y UEFI se utilizarán indistintamente para referirse al firmware 2.x de UEFI . También, a menos que se indique explícitamente, estas instrucciones son de carácter general y no específicas para Mac. Algunas instrucciones pueden no funcionar o pueden ser diferentes en los Mac de Apple. La implementación EFI de Apple no es ni la versión 1.x de EFI ni la versión 2.x, sino una combinación de ambas. Este tipo de firmware no entra dentro de ninguna versión de la especificación UEFI uno y, por lo tanto, no es un estándar del firmware de UEFI.

## Contents

*   [1 Diferencias entre BIOS y UEFI](#Diferencias_entre_BIOS_y_UEFI)
*   [2 Proceso de arranque bajo UEFI](#Proceso_de_arranque_bajo_UEFI)
    *   [2.1 Multiarranque en UEFI](#Multiarranque_en_UEFI)
        *   [2.1.1 Arranque de Microsoft Windows](#Arranque_de_Microsoft_Windows)
    *   [2.2 Detectar la arquitectura del firmware UEFI](#Detectar_la_arquitectura_del_firmware_UEFI)
        *   [2.2.1 Sistemas UEFI que no son Mac](#Sistemas_UEFI_que_no_son_Mac)
        *   [2.2.2 Mac de Apple](#Mac_de_Apple)
    *   [2.3 Secure Boot](#Secure_Boot)
*   [3 Configuración de las opciones del Kernel de Linux para UEFI](#Configuraci.C3.B3n_de_las_opciones_del_Kernel_de_Linux_para_UEFI)
*   [4 Variables de UEFI](#Variables_de_UEFI)
    *   [4.1 Apoyo de las Variables de UEFI en el Kernel](#Apoyo_de_las_Variables_de_UEFI_en_el_Kernel)
        *   [4.1.1 Inconsistencia entre efivarfs y sysfs-efivars](#Inconsistencia_entre_efivarfs_y_sysfs-efivars)
    *   [4.2 Requisitos del soporte de las variables UEFI para que funcione correctamente](#Requisitos_del_soporte_de_las_variables_UEFI_para_que_funcione_correctamente)
        *   [4.2.1 Montar efivarfs](#Montar_efivarfs)
    *   [4.3 Herramientas en el espacio de usuario](#Herramientas_en_el_espacio_de_usuario)
        *   [4.3.1 efibootmgr](#efibootmgr)
*   [5 EFI System Partition](#EFI_System_Partition)
    *   [5.1 Discos particionados para GPT](#Discos_particionados_para_GPT)
    *   [5.2 Discos particionados para MBR](#Discos_particionados_para_MBR)
    *   [5.3 ESP en RAID](#ESP_en_RAID)
*   [6 Shell de UEFI](#Shell_de_UEFI)
    *   [6.1 Obtener la shell de UEFI](#Obtener_la_shell_de_UEFI)
    *   [6.2 Lanzar la shell de UEFI](#Lanzar_la_shell_de_UEFI)
    *   [6.3 Órdenes importantes de la shell de UEFI](#.C3.93rdenes_importantes_de_la_shell_de_UEFI)
        *   [6.3.1 bcfg](#bcfg)
        *   [6.3.2 edit](#edit)
*   [7 Compatibilidad de hardware](#Compatibilidad_de_hardware)
*   [8 Soporte para arrancar UEFI](#Soporte_para_arrancar_UEFI)
    *   [8.1 Crear un USB arrancable con UEFI desde la ISO](#Crear_un_USB_arrancable_con_UEFI_desde_la_ISO)
    *   [8.2 Eliminar el apoyo de arranque de UEFI desde la ISO](#Eliminar_el_apoyo_de_arranque_de_UEFI_desde_la_ISO)
*   [9 Probar UEFI en sistemas sin soporte nativo](#Probar_UEFI_en_sistemas_sin_soporte_nativo)
    *   [9.1 OVMF para máquinas virtuales](#OVMF_para_m.C3.A1quinas_virtuales)
    *   [9.2 DUET para sistemas BIOS únicamente](#DUET_para_sistemas_BIOS_.C3.BAnicamente)
*   [10 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [10.1 Windows 7 no se inicia en la modalidad UEFI](#Windows_7_no_se_inicia_en_la_modalidad_UEFI)
    *   [10.2 Windows cambia el orden de arranque](#Windows_cambia_el_orden_de_arranque)
    *   [10.3 El soporte USB arranca mostrando una pantalla en negro](#El_soporte_USB_arranca_mostrando_una_pantalla_en_negro)
        *   [10.3.1 Utilizar GRUB](#Utilizar_GRUB)
*   [11 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Diferencias entre BIOS y UEFI

Véase [Arch_Boot_Process_(Español)#Tipos_de_firmware](/index.php/Arch_Boot_Process_(Espa%C3%B1ol)#Tipos_de_firmware "Arch Boot Process (Español)") para conocer más detalles.

## Proceso de arranque bajo UEFI

1.  Encendido del sistema — se inicia Power On Self Test — o el proceso [POST](https://en.wikipedia.org/wiki/es:POST "wikipedia:es:POST").
2.  Se carga el firmware UEFI. El firmware inicializa el hardware necesario para el arranque.
3.  El firmware lee el gestor de arranque para determinar qué aplicación UEFI iniciar, y desde dónde (es decir, desde qué disco y partición).
4.  El firmware UEFI inicia la aplicación desde la partición UEFI definida en la entrada de arranque del gestor de arranque del firmware.
5.  La aplicación UEFI puede iniciar otra aplicación (como la shell de UEFI o un gestor de arranque como rEFInd), o el kernel y el initramfs (en el caso de un gestor de arranque como GRUB) en función de cómo se ha configurado la aplicación UEFI.

**Nota:** En algunos sistemas UEFI el único camino posible para iniciar la aplicación UEFI en el arranque (si no tiene una entrada personalizada en el menú de inicio de UEFI) es ponerlo en este lugar fijo: `<PARTICIÓN DEL SISTEMA EFI>/EFI/boot/bootx64.efi` (para sistemas x86 de 64-bit)

### Multiarranque en UEFI

Debido a que cada sistema operativo o fabricante puede mantener sus propios archivos en la partición del sistema EFI (*«EFI System Partition»*) sin afectar a otros sistemas operativos, el multiarranque con UEFI consiste únicamente en lanzar una aplicación UEFI diferente, correspondiente al gestor de arrranque de un particular sistema operativo. Esto elimina la necesidad de recurrir a mecanismos de cargar los sistemas operativos en cadena con un gestor de arranque para iniciar uno u otro.

#### Arranque de Microsoft Windows

Las versiones de 64-bit de Windows Vista (SP1+), 7 y 8, permiten arrancar de forma nativa utilizando el firmware UEFI x86_64\. Windows fuerza el tipo de partición en función del firmware utilizado, es decir, si Windows se inicia en el modo UEFI, es que viene instalado en un disco GPT. Si Windows se inicia en modo BIOS legacy, significa que solo se puede instalar en un disco MBR. Esta es una limitación impuesta por el instalador de Windows. Así Windows soporta bien el arranque UEFI-GPT o solo arranque BIOS-MBR, pero no el arranque UEFI-MRB o BIOS-GPT.

Estas limitaciones no existen en el kernel de Linux, sino que depende del gestor de arranque utilizado. Sin embargo, esta limitación de Windows se debe tener en cuenta si el usuario quiere arrancar Windows y Linux en el mismo disco, ya que la configuración del gestor de arranque en sí depende del tipo de firmware y de la partición del disco utilizada. En el caso de arranque dual de Windows y Linux en el mismo disco, es recomendable seguir el método utilizado por Windows, ya sea el arranque UEFI-GPT o solo arranque BIOS-MBR, no los otros dos casos.

Las versiones de Windows de 32-bit únicamente soportan el arranque en sistemas BIOS-MBR. Siga las instrucciones proporcionadas en el enlace del foro en las secciones apropiadas respecto a cómo hacer esto. Véase [http://support.microsoft.com/kb/2581408](http://support.microsoft.com/kb/2581408) para más información.

### Detectar la arquitectura del firmware UEFI

#### Sistemas UEFI que no son Mac

Compruebe si el directorio `/sys/firmware/efi` existe; si existe, significa que el kernel ha arrancado en modalidad EFI. En ese caso, significa que la arquitectura de UEFI coincide con la del kernel (es decir, i686 o x86_64)

**Nota:** El chip del sistema Atom de Intel es entregado con UEFI de 32 bit (desde el 2 de noviembre de 2013). Véase [esta página](/index.php/Unified_Extensible_Firmware_Interface/Hardware#Intel_Atom_System-on-Chip "Unified Extensible Firmware Interface/Hardware") para obtener más información.

#### Mac de Apple

Los Mac anteriores a 2008 tienen, en su mayoría, un firware i386-efi, mientras que los Mac >=2008 tienen, en su mayoría, x86_64-efi. Todos los Mac capaces de ejecutar el kernel de Mac OS X Snow Leopard 64-bit tienen un firmware EFI 1.x para x86_64.

Para saber la arquitectura del firmware EFI en un Mac, debe arrancar Mac OS X y escribir en un terminal la siguiente orden:

```
ioreg -l -p IODeviceTree | grep firmware-abi

```

Si la orden devuelve EFI32 entonces es un firmware EFI 1.x para i386\. Si devuelve EFI64, entonces es un firmware EFI 1.x para x86_64\. Mac no tiene un firmware 2.x UEFI, porque la implementación del firmware EFI de Apple no es totalmente compatible con la especificación UEFI 2.x.

### Secure Boot

Para una visión general sobre Secure Boot en linux véase [http://www.rodsbooks.com/efi-bootloaders/secureboot.html](http://www.rodsbooks.com/efi-bootloaders/secureboot.html). Esta sección se centra en cómo configurar Secure Boot en Arch Linux. Para empezar se explicará el procedimiento de arranque de archiso con Secure Boot activado. Arrancar la imagen archiso con Secure Boot activado es posible ya que las aplicaciones PreLoader.efi y HashTool.efi se añadieron a la misma. Aparecerá un mensaje que dice «Failed to Start loader... I will now execute HashTool.» Para utilizar HashTool de modo que introduzca el hash de loader.efi y vmlinzu.efi, siga estos pasos:

*   Seleccione `OK`.
*   En el menú principal de HashTool, seleccione `Enroll Hash`, elija `\loader.efi` y confirme con `Yes`. Una vez más, seleccione `Enroll Hash` y `archiso` para entrar en el directorio archiso, y, a continuación, seleccione `vmlinuz-efi` y confirme con `Yes`. Por último, seleccione `Exit` para volver al menú de selección del dispositivo de arranque.
*   En el menú de selección del dispositivo de arranque, seleccione `Arch Linux archiso x86_64 UEFI CD`.

Iniciada la imagen de archiso, se le presentará un prompt de shell, accediendo automáticamente como root. Para comprobar si archiso arrancó con SecureBoot, utilice esta orden:

```
$ od -An -t u1 /sys/firmware/efi/vars/SecureBoot-1234abcde-5678-/data

```

Si es así, esta orde devuelve el número entero 1 al final de una lista de 5, por ejemplo:

```
 6 0 0 0 1

```

Los caracteres denotados por XXXX difieren de una máquina a otra. Para ayudar con esto, se puede usar la implementación del tabulador o listar las variables de efi.

## Configuración de las opciones del Kernel de Linux para UEFI

Las opciones requeridas para la configuración del kernel de Linux para sistemas UEFI son:

```
CONFIG_EFI=y
CONFIG_EFI_STUB=y
CONFIG_RELOCATABLE=y
CONFIG_FB_EFI=y
CONFIG_FRAMEBUFFER_CONSOLE=y

```

*   Soporte para las Variables Runtime de UEFI (sistema de archivos **efivarfs** - `/sys/firmware/efi/efivars`). Esta opción es importante, ya que es necesaria para manipular las Variables Runtime de UEFI usando herramientas como `/usr/bin/gummiboot`. La opción de configuración siguiente está añadida en el kernel 3.10 y posterior: `CONFIG_EFIVAR_FS=y` 

*   Soporte para las Variables Runtime de UEFI (interfaz **efivars sysfs** - `/sys/firmware/efi/vars`). Esta opción debe ser desactivada.: `CONFIG_EFI_VARS=n` 

*   Opción de configuración de GUID Partition Table ([GPT](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")) - necesaria para dar soporte a UEFI: `CONFIG_EFI_PARTITION=y` 

**Nota:** Todas las opciones anteriores son necesarias para arrancar Linux en UEFI, y están activadas en los kernels de ArchLinux presentes en los repositorios oficiales.

Obtenido de [https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt) .

## Variables de UEFI

UEFI define las variables como la interacción de un sistema operativo con el firmware. Las variables de arranque de UEFI (*«UEFI Boot Variables»*) son utilizadas por el cargador de arranque y por el sistema operativo únicamente durante la primera fase de arranque. Las variables runtime de UEFI permiten a un sistema operativo gestionar ciertos ajustes del firmware como la gestión del arranque de UEFI o la gestión de las claves para el protocolo Boot Secure de UEFI, etc. Se puede obtener el listado de variables utilizando:

```
$ efivar -l

```

### Apoyo de las Variables de UEFI en el Kernel

El Kernel de Linux expone los datos de las variables de EFI en el espacio de usuario a través de 2 interfaces:

*   Interfaz **sysfs-efivars ANTIGUA** (CONFIG_EFI_VARS) - completada por el módulo del kernel `efivars` en `/sys/firmware/efi/vars` - con un límite de tamaño de 1024 byte como máximo por dato de variable, sin soporte para las variables de UEFI Secure Boot (debido a la limitación del tamaño) y no recomendado por ningún desarrollador del kernel. Aún así, mantenido por los desarrolladores del kernel ,pero **completamente desactivado en los kernels oficiales de Arch'**.

*   Interfaz **efivarfs NUEVA** (**EFI** **VAR**iable **F**ile**S**ystem) (CONFIG_EFIVAR_FS) - montada usando el módulo del kernel `efivarfs` en `/sys/firmware/efi/efivars` - sustituye a la anterior interfaz, sin limitaciones de tamaño para las variables, con soporte para las variables de UEFI Secure Boot y recomendado por los desarrolladores del kernel. Introducido en el kernel 3.8 y módulo `efivarfs` NUEVO separado del módulo `efivars` ANTIGUO en el kernel 3.10 .

#### Inconsistencia entre efivarfs y sysfs-efivars

Activar tanto sysfs-efivars ANTIGUO como efivarfs NUEVO simultáneamente puede causar problemas de inconsistencia de datos (véase [https://lkml.org/lkml/2013/4/16/473](https://lkml.org/lkml/2013/4/16/473) para más información). Debido a que el VIEJO sysfs-efivars está completamente desactivado en los kernel oficiales de Arch (desde **core/[linux](https://www.archlinux.org/packages/?name=linux)-3.11** y **core/[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)-3.10**), únicamente el NUEVO efivarfs será activado/soportado en lo sucesivo. Todas las variables de UEFI respecto a las herramientas y utilidades disponibles en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)") soportan efivarfs desde el 1 de octubre de 2013.

**Nota:** Como efecto secundario de la desactivación del ANTIGUO sysfs-efivars, el módulo `efi_pstore` también está desactivado en los kernel oficiales de Arch como funcionalidad de EFI pstore.

Si tiene ambas interfaces activadas, deberá desactivar una de ellas, y desactivar y volver a activar la otra interfaz (para actualizar los datos y evitar inconsistencias) antes de acceder a los datos de EFI VAR utilizando cualquier herramienta en el espacio de usuario:

Para desactivar sysfs-efivars y refrescar efivarfs:

```
# modprobe -r efivars

# umount /sys/firmware/efi/efivars
# modprobe -r efivarfs

# modprobe efivarfs
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars

```

Para desactivar efivarfs y refrescar sysfs-efivars:

```
# umount /sys/firmware/efi/efivars
# modprobe -r efivarfs

# modprobe -r efivars
# modprobe efivars

```

### Requisitos del soporte de las variables UEFI para que funcione correctamente

1.  El soporte para EFI Runtime Services debe estar presente en el kernel (`CONFIG_EFI=y`, compruebe si están presente con `zgrep CONFIG_EFI /proc/config.gz`).
2.  La arquitectura del procesador del Kernel y del procesador de EFI deben coincidir.
3.  El kernel debe arrancar en modo EFI (a través de [EFISTUB](/index.php/EFISTUB "EFISTUB") o de cualquier otro [gestor de arranque EFI](/index.php/Boot_loaders "Boot loaders"), no a través de BIOS/CSM o «bootcamp» de Apple que también es BIOS/CSM)
4.  Los EFI Runtime Services del kernel NO DEBEN ser desactivados a través de un terminal, es decir, el parámetro `noefi` del kernel NO DEBE ser usado.
5.  El sistema de archivos `efivarfs` debe estar montado en `/sys/firmware/efi/efivars`, en otro caso, sigua [esta sección](#Montar_efivarfs).
6.  `efivar` debe mostar (con la opción `-l`) las variables EFI sin ningún error. Para una muestra de salida véase [#Sample_List_of_UEFI_Variables](#Sample_List_of_UEFI_Variables).

Si el soporte para las variables de EFI no funciona, incluso después de cumplirse las condiciones precedentes, pruebe las siguientes soluciones:

1.  Si cualquier herramienta del espacio de usuario no puede modificar los datos de las variables de EFI, compruebe la existencia de archivos en `/sys/firmware/efi/efivars/dump-*`. Si existen, elimínelos, reinicie y vuelva a intentarlo de nuevo.
2.  Si el paso anterior no resuelve el problema, intente arrancar con el parámetro del kernel `efi_no_storage_paranoia` para desactivar la variable efi del kernel que comprueba el espacio de almacenamiento, la cual puede impedir la escritura/modificación de las variables de efi.

**Nota:** `efi_no_storage_paranoia` solo debe utilizarse cuando sea necesario y no se debe dejar como una opción de arranque normal. El efecto de este parámetro en la línea de órdenes del kernel cancela una garantía que se pone en marcha para ayudar a evitar la saturación de las máquinas cuando NVRAM se llena demasiado.

#### Montar efivarfs

Si `efivarfs` no se monta automáticamente en `/sys/firmware/efi/efivars` por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") durante el arranque, entonces necesita montarla manualmente para dejar expuesto el soporte para las variables de UEFI a las herramientas del espacio de usuario tales como `efibootmgr`, etc.:

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars

```

**Nota:** La orden anterior debe ejecutarse tanto FUERA (ANTES) como DENTRO de **chroot**, si procede.

También es una buena idea para el montaje automático de `efivarfs` durante el arranque, hacerlo mediante `/etc/fstab`, de la siguiente manera:

 `/etc/fstab` 
```
efivarfs    /sys/firmware/efi/efivars    efivarfs    defaults    0    0

```

### Herramientas en el espacio de usuario

Existen algunas herramientas que permiten acceder/modificar las variables UEFI, como:

1.  **efivar** - Herramienta y biblioteca para modificar las variables de UEFI (usado por efibootmgr de vathpela) - [https://github.com/vathpela/efivar](https://github.com/vathpela/efivar) - [efivar](https://www.archlinux.org/packages/?name=efivar) o [efivar-git](https://aur.archlinux.org/packages/efivar-git/)
2.  **efibootmgr** - Herramienta para modificar las configuraciones del gestor de arranque del firmware de UEFI. Los desarrolladores del código efibootmgr (linuxdell) no proporcionan soporte a efivarfs. Un fork de efibootmgr de Fedora por Peter Jones (vathpela) soporta tanto efivarfs como sysfs-efivars. Actualmente se utiliza, en el repositorio oficial core, el paquete [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) y, en AUR, el paquete [efibootmgr-pjones-git](https://aur.archlinux.org/packages/efibootmgr-pjones-git/) - [https://github.com/vathpela/efibootmgr/tree/libefivars](https://github.com/vathpela/efibootmgr/tree/libefivars)
3.  **uefivars** - Simplemente accede al listado de las variables de EFI con alguna información adicional sobre el PCI (utiliza el código de efibootmgr) - [https://github.com/fpmurphy/Various/tree/master/uefivars-2.0](https://github.com/fpmurphy/Various/tree/master/uefivars-2.0) solo admite efivarfs y [https://github.com/fpmurphy/Various/tree/master/uefivars-1.0](https://github.com/fpmurphy/Various/tree/master/uefivars-1.0) solo admite sysfs-efivars. Paquete de AUR [uefivars-git](https://aur.archlinux.org/packages/uefivars-git/)
4.  **efitools** - Herramientas para crear y configura los propios Certificados Secure Boot de UEFI, Claves y Binarios Firmados (requiere efivarfs) - [efitools-git](https://aur.archlinux.org/packages/efitools-git/)
5.  **Suite de comprobación de firmware, de Ubuntu** - [https://wiki.ubuntu.com/FirmwareTestSuite/](https://wiki.ubuntu.com/FirmwareTestSuite/) - [fwts](https://aur.archlinux.org/packages/fwts/) (junto con [fwts-efi-runtime-dkms](https://aur.archlinux.org/packages/fwts-efi-runtime-dkms/)) o [fwts-git](https://aur.archlinux.org/packages/fwts-git/)

#### efibootmgr

**Advertencia:** Usar `efibootmgr` en los Mac de Apple podría dañar el firmware y podría ser necesario flashear la ROM de la placa base. Ha habido informes de errores con respecto a este bug tracker en Ubuntu/Launchpad. Utilice la orden bless únicamente si tiene un Mac. La utilidad experimental «bless» para Linux es desarrollado por los desarrolladores de Fedora - [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/).

**Nota:**

*   Si `efibootmgr` no funciona en absoluto en su sistema, puede reiniciar en la Shell v2 de UEFI y utilizar la orden `bcfg` para crear una entrada de arranque en el gestor de arranque.
*   Si no es posible usar `efibootmgr`, algunos firmwares UEFI permiten a los usuarios gestionar directamente las opciones de UEFI Boot Manager desde la BIOS. Por ejemplo, algunas BIOS de ASUS tienen una opción llamada «Add New Boot Option» (*«Añadir nueva opción de arranque»*) que permite seleccionar una partición de sistema EFI local e introducir manualmente la ubicación del código de EFI (por ejemplo `\EFI\refind\refind_x64.efi`).
*   Las siguientes órdenes utilizan el cargador de arranque [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) como ejemplo.

Supongamos que el archivo boot-loader para ser lanzado es `/boot/efi/EFI/refind/refind_x64.efi`. El mismo `/boot/efi/EFI/refind/refind_x64.efi` puede ser dividido en `/boot/efi` y `/EFI/refind/refind_x64.efi`, donde `/boot/efi` es el punto de montaje de la partición del sistema UEFI, que se supone que es `/dev/sdXY` (en este caso `X` e `Y` son marcadores de posición para los valores reales - por ejemplo: - en `/dev/sda1`, `X=a`; `Y=1`).

Para determinar la ruta real del dispositivo para la partición del sistema UEFI (debe tener el formato `/dev/sdXY`), pruebe con la orden:

```
# findmnt /boot/efi
TARGET SOURCE  FSTYPE OPTIONS
/boot/efi  /dev/sdXY  vfat         rw,flush,tz=UTC

```

Compruebe que el soporte para las variables de UEFI en el kernel funciona correctamente ejecutando la orden:

```
# efivar -l

```

Si efivar enumera las variables UEFI sin ningún error, entonces se puede continuar. Si no es así, compruebe si todas las condiciones [descritas aquí](#Requisitos_del_soporte_de_las_variables_UEFI_para_que_funcione_correctamente) se cumplen.

A continuación, cree la entrada de arranque usando efibootmgr de la siguiente manera:

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/refind/refind_x64.efi -L "rEFInd"

```

**Nota:** UEFI utiliza la barra invertida `\` como separador de ruta (similar a las rutas de Windows), pero el paquete oficial [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) proporciona soporte a las rutas de estilo unix con barras diagonales `/` como separador de ruta para la opción `-l`. Efibootmgr convierte internamente `/` a `\` antes de codificar la ruta de acceso del cargador. Este importante comportamiento que añadió esta característica a efibootmgr está en [http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/commit/?id=f38f4aaad1dfa677918e417c9faa6e3286411378](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/commit/?id=f38f4aaad1dfa677918e417c9faa6e3286411378) .

En la orden anterior `/boot/efi/EFI/refind/refind_x64.efi` interpreta a `/boot/efi` y a `/EFI/refind/refind_x64.efi`, que, a su vez, lo interpretan como: disco: `/dev/sdX` → partición: `Y` → archivo: `/EFI/refind/refind_x64.efi`.

La «etiqueta» es el nombre de la entrada del menú que se muestra en el menú de inicio UEFI. Este nombre es elegido por el usuario y no afecta al arranque del sistema. Se puede obtener más información a partir de [efibootmgr GIT README](http://linux.dell.com/cgi-bin/cgit.cgi/efibootmgr.git/plain/README).

El sistema de archivos FAT32 no distingue entre mayúsculas y minúsculas, ya que no utiliza codificación UTF-8 de forma predeterminada. En este caso, el firmware utiliza «EFI» en letra mayúscula, en lugar de minúsculas («efi»), por lo tanto, usando `\EFI\refind\refindx64.efi` o `\efi\refind\refind_x64.efi` no hay diferencia (esto cambia si la codificación del sistema de archivos es UTF-8).

## EFI System Partition

La EFI System Partition (*«Partición del Sistema EFI»*) (también llamada ESP o EFISYS) es una particón física formateada con FAT32 (en la tabla de partición principal del disco, no en LVM o RAID software, etc.) desde donde el firmware UEFI lanza las aplicaciones y el gestor de arranque de UEFI. Es una partición independiente del sistema operativo que actúa como el lugar de almacenamiento para los gestores de arranque EFI y las aplicaciones que el firmware lanza después. Es obligatoria para arrancar UEFI. Debe estar marcada como código tipo **EF00** o **ef00** con gdisk, o la etiqueta **boot** si se utiliza GNU Parted (únicamente para discos GPT). Se recomienda mantener el tamaño de ESP en 512 MiB aunque los tamaños más pequeños/grandes también valen (sin embargo, para los tamaños más pequeños, estos tienen que ser mayores que el límite mínimo del tamaño del sistema de archivos de la partición FAT32 (según lo dispuesto por la especificación FAT32 de Microsoft). Para obtener más información, visite este [enlace](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition").

**Nota:**

*   Se recomienda siempre usar GPT para el arranque de UEFI, dado que algunos firmwares UEFI no permiten arranque desde MBR .
*   Con GNU Parted, la etiqueta `boot`, (que no se debe confundir con la etiqueta `legacy_boot`), tiene diferente efecto según se aplique a un disco MBR o a un disco GPT. En discos MBR, marca la partición como activa . En discos GPT, cambia el código del tipo de partición a `EFI System Partition`. Parted no tiene etiqueta para marcar una partición como ESP en discos MBR (esto se puede hacer usando fdisk, sin embargo).
*   La documentación de Microsoft señala el tamaño de ESP: Para unidades «Advanced Format 4K Native drives (4-KB-por-sector)», el tamaño mínimo es de 260 MB, debido a la limitación del formato del archivo FAT32\. El tamaño mínimo de la partición de las unidades FAT32 es calculado con el tamaño del sector (4KB) x 65527 = 256 MB. La unidades «Advanced Format 512e» no se ven afectadas por esta limitación, ya que su tamaño de sector emulado es de 512 bytes. 512 bytes x 65527 = 32 MB, que es inferior a los 100 MB de tamaño mínimo para esta partición. De: [http://technet.microsoft.com/en-us/library/hh824839.aspx#DiskPartitionRules](http://technet.microsoft.com/en-us/library/hh824839.aspx#DiskPartitionRules)
*   En el caso de [EFISTUB](/index.php/EFISTUB "EFISTUB"), los kernels y los archivos initramfs deben ser almacenados en la partición del sistema EFI. En aras de una mayor simplicidad, también se puede utilizar la propia partición ESP como partición `/boot`, en lugar de utilizar una partición `/boot` separada, para arrancar EFISTUB.

### Discos particionados para GPT

*   Crear una partición con el tipo de partición `ef00` o `EF00` usando gdisk (del paquete [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)). Después formatear la partición como FAT32 usando `mkfs.fat -F32 /dev/<PARTICIÓN>`

(o)

*   Crear una partición FAT32 y con GNU Parted establecer/activar la etiqueta `boot` (no la etiqueta `legacy_boot`) en dicha partición.

**Nota:** Si recibe el mensaje `WARNING: Not enough clusters for a 32 bit FAT!`, reduzca el tamaño del clúster con la orden `mkfs.fat -s2 -F32 ...` o `-s1`, de lo contrario la partición puede ser ilegible para UEFI.

### Discos particionados para MBR

Cree una partición asignándole el tipo `0xEF` usando fdisk (del paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux) ). Después formatee esta partición como FAT32 usando `mkfs.fat -F32 /dev/<PARTICIÓN>`

### ESP en RAID

Es posible hacer de ESP una parte de una matriz RAID1, pero ello conlleva el riesgo de corromper los datos, así como otras consideraciones a tener en cuenta cuando se crea la ESP. Véase [https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) and [https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741) para obtener más detalles.

## Shell de UEFI

La Shell de UEFI es una shell/terminal para el firmware que permite ejecutar aplicaciones UEFI que incluyen los cargadores de arranque UEFI. Aparte de esto, la shell también se puede utilizar para obtener información variada sobre el sistema o el firmware del mapa de la memoria (memmap), modificar las variables del gestor de arranque (bcfg), ejecutar programas de gestión de particiones (diskpart), cargar los controladores UEFI, editar archivos de texto (edit), hexedit, etc.

### Obtener la shell de UEFI

Puede descargar una Shell de UEFI con licencia BSD de Tianocore de Intel desde el proyecto Sourceforge.net UDK/EDK2.

*   Paquete **[uefi-shell-svn](https://aur.archlinux.org/packages/uefi-shell-svn/)** desde [AUR](/index.php/AUR "AUR") (recomendado) - proporciona una Shell x86_64 para sistemas x86_64 y una Shell IA32 para sistemas i686 - compilado directamente desde la última fuente SVN EDK2 de Tianocore
*   [Precompiled x86_64 UEFI Shell v2 binary](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/ShellBinPkg/UefiShell/X64/Shell.efi) (puede no estar actualizado)
*   [Precompiled x86_64 UEFI Shell v1 binary](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/EdkShellBinPkg/FullShell/X64/Shell_Full.efi) (no actualizado por los desarrolladores)
*   [Precompiled IA32 UEFI Shell v2 binary](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/ShellBinPkg/UefiShell/Ia32/Shell.efi) (puede no estar actualizado)
*   [Precompiled IA32 UEFI Shell v1 binary](https://edk2.svn.sourceforge.net/svnroot/edk2/trunk/edk2/EdkShellBinPkg/FullShell/Ia32/Shell_Full.efi) (no actualizado por los desarrolladores)

La versión 2.0 de la Shell únicamente funciona en sistemas UEFI 2.3 + y se recomienda su uso con preferencia a la Shell 1.0 en esos sistemas. La versión 1.3 de la Shell debería funcionar en todos los sistemas UEFI, independientemente de la especificación de la versión del firmware. Más información en [ShellPkg](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=ShellPkg) y [este correo](http://sourceforge.net/mailarchive/message.php?msg_id=28690732).

### Lanzar la shell de UEFI

Algunas placas base Asus y otras basadas en el firmware UEFI AMI Aptio x86_64 (de Sandy Bridge en adelante) ofrecen una opción llamada `«Launch EFI Shell from filesystem device»`. Para estas placas base, descargue la Shell de UEFI x86_64 y cópiela a la partición del sistema UEFI como `<UEFI_SYSTEM_PARTITION>/shellx64.efi` (normalmente en la carpeta `/boot/efi/shellx64.efi`).

Los sistemas con un firmware UEFI Phoenix SecureCore Tiano se sabe que llevan integrada la Shell de UEFI, la cual se puede iniciar presionando las teclas `F6`, `F11` o `F12`.

**Nota:** Si es incapaz de lanzar la Shell de UEFI directamente desde el firmware mediante cualquiera de los métodos mencionados anteriormente, cree una unidad USB formateada con FAT32 conteniendo la `Shell.efi` copiada con la ruta `(USB)/efi/boot/bootx64.efi`. Este USB debería aparecer en el menú de arranque del firmware. La inicialización de esta opción lanzará la Shell de UEFI.

### Órdenes importantes de la shell de UEFI

Las órdenes de la Shell de UEFI generalmente dan soporte a la opción `-b` que hace una pausa después de la salida de cada página. `map` que lista los sistemas de archivos reconocidos (`fs0`, ...) y los dispositivos de almacenamiento de datos (`blk0`, ...). Ejecute `help -b` para ver las órdenes disponibles.

Puede obtener más información en [http://software.intel.com/en-us/articles/efi-shells-and-scripting/](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)

#### bcfg

La orden BCFG se utiliza para modificar las entradas en la NVRAM de UEFI, lo que permite cambiar las entradas de arranque o las opciones del controlador. Esta orden se describe con detalle en la página 83 (sección 5.3) del documento pdf «UEFI Shell Specification 2.0».

**Nota:**

*   Se recomienda probar `bcfg` únicamente si `efibootmgr` no puede crear entradas de inicio que funcionen en el propio sistema.
*   La versión 1 del binario oficial de la Shell de UEFI no proporciona soporte para la orden `bcfg`. Puede descargar una [Shell de UEFI modificada](http://dl.dropbox.com/u/17629062/Shell2.zip) que puede trabajar con firmwares pre-2.3 de UEFI.

Para conocer una lista de entradas de arranque actuales:

```
Shell> bcfg boot dump -v

```

Para añadir una entrada en el menú de inicio para rEFInd (por ejemplo) como cuarta (la numeración empieza desde cero) en el menú de arranque:

```
Shell> bcfg boot add 3 fs0:\EFI\refind\refind_x64.efi "rEFInd"

```

donde `fs0:` es la asignación correspondiente a la partición del sistema UEFI y `\EFI\arch\refind\refindx64.efi` es el archivo que se pondrá en marcha.

Para quitar la opción de arranque cuarta:

```
Shell> bcfg boot rm 3

```

Para mover la opción de arranque #3 a #0 (es decir, la primera o la entrada por defecto en el menú de inicio de UEFI):

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

#### edit

La orden EDIT proporciona un editor de texto básico, con una interfaz similar al editor de textos nano, pero ligeramente menos funcional. Maneja codificación UTF-8 y se hace cargo del final de la línea LF frente a [CRLF](https://en.wikipedia.org/wiki/es:CRLF "wikipedia:es:CRLF").

Para editar, por ejemplo, `refind.conf` de rEFInd en la partición del sistema UEFI (fs0: en el firmware):

```
Shell> fs0:
FS0:\> cd \EFI\arch\refind
FS0:\EFI\arch\refind\> edit refind.conf

```

Escriba `Ctrl-E` para obtener ayuda.

## Compatibilidad de hardware

Véase el artículo [Unified Extensible Firmware Interface/Hardware](/index.php/Unified_Extensible_Firmware_Interface/Hardware "Unified Extensible Firmware Interface/Hardware")

## Soporte para arrancar UEFI

### Crear un USB arrancable con UEFI desde la ISO

Siga las instrucciones del siguiente [artículo](/index.php/USB_Installation_Media_(Espa%C3%B1ol)#Crear_USB_arrancable_desde_sistemas_BIOS_y_UEFI "USB Installation Media (Español)")

### Eliminar el apoyo de arranque de UEFI desde la ISO

**Nota:** Esta sección menciona la eliminación de la ayuda de arranque UEFI **únicamente** desde un CD/DVD (soporte óptico), no desde una unidad flash USB.

La mayoría de los Mac EFI de 32-bit y algunos Mac EFI de 64 bits se niegan a arrancar desde un CD/DVD bootable una combinación de UEFI(X64)+BIOS. Si se desea continuar con la instalación mediante medios ópticos, puede que sea necesario, primero, eliminar el apoyo a UEFI.

*   Monte el soporte de instalación oficial y obtenga la `archisolabel` como se muestra en la sección anterior.

```
# mount -o loop *input.iso* /mnt/iso

```

*   Reconstruya la ISO usando `xorriso` desde [libisoburn](https://www.archlinux.org/packages/?name=libisoburn):

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

## Probar UEFI en sistemas sin soporte nativo

### OVMF para máquinas virtuales

OVMF [[1]](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=OVMF) es un proyecto para activar la compatibilidad de UEFI para máquinas virtuales. OVMF contiene una muestra de firmware UEFI para QEMU.

Se puede compilar OVMF (con el apoyo de Secure Boot) con [ovmf-svn](https://aur.archlinux.org/packages/ovmf-svn/) disponible en AUR y ejecutándolo como sigue:

```
qemu-system-x86_64 -enable-kvm -net none -m 1024 -bios /usr/share/ovmf/x86_64/bios.bin

```

### DUET para sistemas BIOS únicamente

DUET es un proyecto tianocore que permite cargar en cadena un entorno UEFI completo desde un sistema BIOS, de manera similar al arranque de los sistemas operativos en entorno BIOS. Este método se está discutiendo ampliamente en [http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/](http://www.insanelymac.com/forum/topic/186440-linux-and-windows-uefi-boot-using-tianocore-duet-firmware/) . Imágenes DUET precompiladas se pueden descargar de uno de los repositorios de [https://gitorious.org/tianocore_uefi_duet_builds](https://gitorious.org/tianocore_uefi_duet_builds) . Instrucciones específicas para la creación de DUET están disponible en [https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt](https://gitorious.org/tianocore_uefi_duet_builds/tianocore_uefi_duet_installer/blobs/raw/master/Migle_BootDuet_INSTALL.txt) .

También puede probar [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/) que proporciona imágenes DUET modificadas que puedan contener algunos arreglos específicos del sistema y son más frecuentemente actualizadas en comparación con las de los repositorios gitorious.

## Solución de problemas

### Windows 7 no se inicia en la modalidad UEFI

Si tiene instalado Windows en un disco duro con particionado GPT y sigue teniendo otro disco duro diferente con particionado MBR en su ordenador, entonces es posible que la BIOS UEFI está dando su apoyo CSM a este último (para arrancar particiones MBR) y por ello Windows no arranca. Para resolver este problema convierta el particionado de su disco MBR a GPT, o desactive el puerto SATA del disco duro cuando esté conectado, o bien, desenchufe el puerto SATA de este disco duro.

Placas base con este tipo de problema:

Gigabyte Z77X-UD3H rev. 1.1 (BIOS UEFI versión F19e)

- La opción *«UEFI Only»* de la BIOS UEFI no pretende hacer que la BIOS UEFI arranque desde CSM.

### Windows cambia el orden de arranque

En algunas placas base (confirmado en ASRock Z77 Extreme4) Windows 8 cambia el orden de inicio en la NVRAM cada vez que se arranca. Esto se puede solucionar haciendo que el Windows Boot Manager sea cargado por otro gestor de arranque en lugar de arrancar con Windows. Ejecutar esta orden en una consola como administrador en Windows:

```
bcdedit /set {bootmgr} path \EFI\boot_app_dir\boot_app.efi

```

### El soporte USB arranca mostrando una pantalla en negro

*   Este fallo puede deberse a un problema con [KMS](/index.php/Kernel_Mode_Setting_(Espa%C3%B1ol) "Kernel Mode Setting (Español)"). Pruebe [desactivando KMS](/index.php/Kernel_Mode_Setting_(Espa%C3%B1ol)#Desactivar_modesetting "Kernel Mode Setting (Español)") durante el arranque del USB.

*   Si el problema no se debe a KMS, entonces puede ser debido a un error en el arranque de [EFISTUB](/index.php/EFISTUB "EFISTUB") (véase [[2]](https://bugs.archlinux.org/task/33745) y [[3]](https://bbs.archlinux.org/viewtopic.php?id=156670) para obtener más información.). Tanto la ISO Oficial ([Archiso](/index.php/Archiso "Archiso")) como la iso de [Archboot](/index.php/Archboot "Archboot") utilizan EFISTUB (mediante el gestor de arranque [Gummiboot](/index.php/Gummiboot "Gummiboot") para el menú) para iniciar el kernel en modalidad UEFI. En tal caso hay que usar [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") como gestor de arranque de UEFI para el USB siguiendo la sección siguiente.

#### Utilizar GRUB

*   Cree un USB arrancable como soporte de la instalación, siguiendo las instrucciones de este [enlace](/index.php/USB_Flash_Installation_Media_(Espa%C3%B1ol) "USB Flash Installation Media (Español)"). Después de eso, siga los pasos siguientes para utilizar GRUB en lugar de Gummiboot.

*   Realice una copia de seguridad de `<USB>/EFI/boot/loader.efi` a `<USB>/EFI/boot/gummiboot.efi`

*   [Cree una imagen autónoma de GRUB](/index.php/GRUB_(Espa%C3%B1ol)#Construir_una_aplicaci.C3.B3n_UEFI_Standalone_para_GRUB "GRUB (Español)") y cópiela en `<USB>/EFI/boot/loader.efi`

*   Cree el archivo `<USB>/EFI/boot/grub.cfg` con el siguiente contenido:

 `grub.cfg para ISO Oficial` 
```
insmod part_gpt
insmod part_msdos
insmod fat

insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus

insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
    insmod gfxterm
    set gfxmode="1024x768x32;auto"
    terminal_input console
    terminal_output gfxterm
fi

menuentry "Arch Linux archiso x86_64" {
    set gfxpayload=keep
    search --no-floppy --set=root --label ARCHISO_XXXXXX
    linux /arch/boot/x86_64/vmlinuz archisobasedir=arch archisolabel=ARCHISO_XXXXXX add_efi_memmap
    initrd /arch/boot/x86_64/archiso.img
}

menuentry "UEFI Shell x86_64 v2" {
    search --no-floppy --set=root --label ARCHISO_XXXXXX
    chainloader /EFI/shellx64_v2.efi
}

menuentry "UEFI Shell x86_64 v1" {
    search --no-floppy --set=root --label ARCHISO_XXXXXX
    chainloader /EFI/shellx64_v1.efi
}

```
 `grub.cfg para ISO de Archboot` 
```
insmod part_gpt
insmod part_msdos
insmod fat

insmod efi_gop
insmod efi_uga
insmod video_bochs
insmod video_cirrus

insmod font

if loadfont "${prefix}/fonts/unicode.pf2" ; then
    insmod gfxterm
    set gfxmode="1024x768x32;auto"
    terminal_input console
    terminal_output gfxterm
fi

menuentry "Arch Linux x86_64 Archboot" {
    set gfxpayload=keep
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    linux /boot/vmlinuz_x86_64 cgroup_disable=memory loglevel=7 add_efi_memmap
    initrd /boot/initramfs_x86_64.img
}

menuentry "UEFI Shell x86_64 v2" {
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    chainloader /EFI/tools/shellx64_v2.efi
}

menuentry "UEFI Shell x86_64 v1" {
    search --no-floppy --set=root --file /boot/vmlinuz_x86_64
    chainloader /EFI/tools/shellx64_v1.efi
}

```

## Véase también

*   [Wikipedia:UEFI](https://en.wikipedia.org/wiki/UEFI "wikipedia:UEFI")
*   [UEFI Forum](http://www.uefi.org/home/) - contains the official [UEFI Specifications](http://www.uefi.org/specs/) - GUID Partition Table is part of UEFI Specification
*   [UEFI boot: how does that actually work, then? - A blog post by AdamW](https://www.happyassassin.net/2014/01/25/uefi-boot-how-does-that-actually-work-then/)
*   [Wikipedia:EFI System partition](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition")
*   [The EFI System Partition and the Default Boot Behavior](http://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)
*   [Linux Kernel x86_64 UEFI Documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/x86/x86_64/uefi.txt)
*   [Intel's page on EFI](http://www.intel.com/technology/efi/)
*   [Intel UEFI Community Resource Center](http://uefidk.intel.com/)
*   [Matt Fleming - The Linux EFI Boot Stub](http://uefidk.intel.com/blog/linux-efi-boot-stub)
*   [Matt Fleming - Accessing UEFI Variables from Linux](http://uefidk.intel.com/blog/accessing-uefi-variables-linux)
*   [Rod Smith - Linux on UEFI: A Quick Installation Guide](http://www.rodsbooks.com/linux-uefi/)
*   [UEFI Boot problems on some newer machines (LKML)](https://lkml.org/lkml/2011/6/8/322)
*   [LPC 2012 Plumbing UEFI into Linux](http://linuxplumbers.ubicast.tv/videos/plumbing-uefi-into-linux/)
*   [LPC 2012 UEFI Tutorial : part 1](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-1/)
*   [LPC 2012 UEFI Tutorial : part 2](http://linuxplumbers.ubicast.tv/videos/uefi-tutorial-part-2/)
*   [Intel's Tianocore Project](http://sourceforge.net/apps/mediawiki/tianocore/index.php?title=Welcome_to_TianoCore) for Open-Source UEFI firmware which includes DuetPkg for direct BIOS based booting and OvmfPkg used in QEMU and Oracle VirtualBox
*   [FGA: The EFI boot process](http://homepage.ntlworld.com/jonathan.deboynepollard/FGA/efi-boot-process.html)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   [Convert Windows x64 from BIOS-MBR mode to UEFI-GPT mode without Reinstall](https://gitorious.org/tianocore_uefi_duet_builds/pages/Windows_x64_BIOS_to_UEFI)
*   [Create a Linux BIOS+UEFI and Windows x64 BIOS+UEFI bootable USB drive](https://gitorious.org/tianocore_uefi_duet_builds/pages/Linux_Windows_BIOS_UEFI_boot_USB)
*   [Rod Smith - A BIOS to UEFI Transformation](http://rodsbooks.com/bios2uefi/)
*   [EFI Shells and Scripting - Intel Documentation](http://software.intel.com/en-us/articles/efi-shells-and-scripting/)
*   [UEFI Shell - Intel Documentation](http://software.intel.com/en-us/articles/uefi-shell/)
*   [UEFI Shell - bcfg command info](http://www.hpuxtips.es/?q=node/293)
*   [UEFI Shell v2 binary with bcfg modified to work with UEFI pre-2.3 firmware - from Clover efiboot](http://dl.dropbox.com/u/17629062/Shell2.zip)