**Estado de la traducción:** este artículo es una versión traducida de [GRUB](/index.php/GRUB "GRUB"). Fecha de la última traducción/revisión: **2015-06-23**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=GRUB&diff=0&oldid=379250).

[GRUB](https://www.gnu.org/software/grub/) —no confundir con [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")— es la nueva generación de GRand Unified Bootloader (GRUB). GRUB deriva de [PUPA](http://www.nongnu.org/pupa/), un proyecto de investigación destinado a mejorar lo que hoy es GRUB Legacy. GRUB ha sido totalmente reescrito a fin de proporcionar una mayor modularidad y portabilidad [[1]](https://www.gnu.org/software/grub/grub-faq).

## Contents

*   [1 Prefacio](#Prefacio)
*   [2 Sistemas BIOS](#Sistemas_BIOS)
    *   [2.1 Instrucciones específicas para GUID Partition Table (GPT)](#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29)
    *   [2.2 Instrucciones específicas para Master Boot Record (MBR)](#Instrucciones_espec.C3.ADficas_para_Master_Boot_Record_.28MBR.29)
    *   [2.3 Instalación](#Instalaci.C3.B3n)
        *   [2.3.1 Instalar los archivos de arranque de grub](#Instalar_los_archivos_de_arranque_de_grub)
            *   [2.3.1.1 Instalación en el disco](#Instalaci.C3.B3n_en_el_disco)
            *   [2.3.1.2 Instalación en una llave USB](#Instalaci.C3.B3n_en_una_llave_USB)
            *   [2.3.1.3 Instalación en una partición o disco sin particiones](#Instalaci.C3.B3n_en_una_partici.C3.B3n_o_disco_sin_particiones)
            *   [2.3.1.4 Generar únicamente core.img](#Generar_.C3.BAnicamente_core.img)
*   [3 Sistemas UEFI](#Sistemas_UEFI)
    *   [3.1 Comprobar si se está utilizando GPT y una partición EFI del sistema (ESP)](#Comprobar_si_se_est.C3.A1_utilizando_GPT_y_una_partici.C3.B3n_EFI_del_sistema_.28ESP.29)
    *   [3.2 Crear una EFI System partition](#Crear_una_EFI_System_partition)
    *   [3.3 Instalación](#Instalaci.C3.B3n_2)
    *   [3.4 Lecturas complementarias](#Lecturas_complementarias)
        *   [3.4.1 Método alternativo de instalación](#M.C3.A9todo_alternativo_de_instalaci.C3.B3n)
        *   [3.4.2 Solución alternativa a firmware de UEFI](#Soluci.C3.B3n_alternativa_a_firmware_de_UEFI)
        *   [3.4.3 Crear una entrada de GRUB en el gestor de arranque del firmware](#Crear_una_entrada_de_GRUB_en_el_gestor_de_arranque_del_firmware)
        *   [3.4.4 GRUB Standalone](#GRUB_Standalone)
        *   [3.4.5 Información Técnica](#Informaci.C3.B3n_T.C3.A9cnica)
*   [4 Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal)
*   [5 Configuración](#Configuraci.C3.B3n)
    *   [5.1 Argumentos adicionales](#Argumentos_adicionales)
    *   [5.2 Arranque dual](#Arranque_dual)
        *   [5.2.1 Generación automática utilizando /etc/grub.d/40_custom y grub-mkconfig](#Generaci.C3.B3n_autom.C3.A1tica_utilizando_.2Fetc.2Fgrub.d.2F40_custom_y_grub-mkconfig)
            *   [5.2.1.1 Entrada de menú para GNU/Línux](#Entrada_de_men.C3.BA_para_GNU.2FL.C3.ADnux)
            *   [5.2.1.2 Entrada de menú para FreeBSD](#Entrada_de_men.C3.BA_para_FreeBSD)
                *   [5.2.1.2.1 Cargar directamente el kérnel](#Cargar_directamente_el_k.C3.A9rnel)
                *   [5.2.1.2.2 Cargar en cadena el registro de arranque embebido](#Cargar_en_cadena_el_registro_de_arranque_embebido)
            *   [5.2.1.3 Entrada de menú para Windows XP](#Entrada_de_men.C3.BA_para_Windows_XP)
            *   [5.2.1.4 Entrada de menú para Windows instalado en modo UEFI-GPT](#Entrada_de_men.C3.BA_para_Windows_instalado_en_modo_UEFI-GPT)
            *   [5.2.1.5 Entrada de menú para «Apagar»](#Entrada_de_men.C3.BA_para_.C2.ABApagar.C2.BB)
            *   [5.2.1.6 Entrada de menú para «Reiniciar»](#Entrada_de_men.C3.BA_para_.C2.ABReiniciar.C2.BB)
            *   [5.2.1.7 Entrada de menú para Windows instalado en modo BIOS-MBR](#Entrada_de_men.C3.BA_para_Windows_instalado_en_modo_BIOS-MBR)
        *   [5.2.2 Con Windows usando EasyBCD y NeoGRUB](#Con_Windows_usando_EasyBCD_y_NeoGRUB)
        *   [5.2.3 parttool para mostrar/ocultar particiones](#parttool_para_mostrar.2Focultar_particiones)
    *   [5.3 LVM](#LVM)
    *   [5.4 RAID](#RAID)
    *   [5.5 Múltiples entradas](#M.C3.BAltiples_entradas)
    *   [5.6 Encriptación](#Encriptaci.C3.B3n)
        *   [5.6.1 Partición raíz](#Partici.C3.B3n_ra.C3.ADz)
        *   [5.6.2 Partición de arranque](#Partici.C3.B3n_de_arranque)
*   [6 Utilizar la shell de órdenes](#Utilizar_la_shell_de_.C3.B3rdenes)
    *   [6.1 Soporte para Pager](#Soporte_para_Pager)
    *   [6.2 Usar el entorno de la shell de órdenes para arrancar distintos sistemas operativos](#Usar_el_entorno_de_la_shell_de_.C3.B3rdenes_para_arrancar_distintos_sistemas_operativos)
        *   [6.2.1 Cargar una partition](#Cargar_una_partition)
        *   [6.2.2 Cargar un disco/unidad](#Cargar_un_disco.2Funidad)
        *   [6.2.3 Cargar en cadena Windows/Línux instalados en modalidad UEFI](#Cargar_en_cadena_Windows.2FL.C3.ADnux_instalados_en_modalidad_UEFI)
        *   [6.2.4 Carga normal](#Carga_normal)
    *   [6.3 Utilizar la consola de emergencia](#Utilizar_la_consola_de_emergencia)
*   [7 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [7.1 Algunas BIOS de Intel no efectúan el arranque de la partición GPT](#Algunas_BIOS_de_Intel_no_efect.C3.BAan_el_arranque_de_la_partici.C3.B3n_GPT)
        *   [7.1.1 MBR](#MBR)
        *   [7.1.2 Ruta EFI](#Ruta_EFI)
    *   [7.2 Activar mensajes de depuración de errores en GRUB](#Activar_mensajes_de_depuraci.C3.B3n_de_errores_en_GRUB)
    *   [7.3 Corregir el error de GRUB: «no suitable mode found»](#Corregir_el_error_de_GRUB:_.C2.ABno_suitable_mode_found.C2.BB)
    *   [7.4 Mensaje de error msdos-style](#Mensaje_de_error_msdos-style)
    *   [7.5 UEFI](#UEFI)
        *   [7.5.1 Errores comunes de instalación](#Errores_comunes_de_instalaci.C3.B3n)
        *   [7.5.2 Salta la shell de recate](#Salta_la_shell_de_recate)
        *   [7.5.3 GRUB UEFI no se carga](#GRUB_UEFI_no_se_carga)
    *   [7.6 Invalid signature](#Invalid_signature)
    *   [7.7 Bloqueos al arrancar](#Bloqueos_al_arrancar)
    *   [7.8 Arch no es detectado por otros sistemas operativos](#Arch_no_es_detectado_por_otros_sistemas_operativos)
    *   [7.9 Advertencias cuando se instala en entorno chroot](#Advertencias_cuando_se_instala_en_entorno_chroot)
    *   [7.10 GRUB carga lentamente](#GRUB_carga_lentamente)
    *   [7.11 error: unknown filesystem](#error:_unknown_filesystem)
    *   [7.12 grub-reboot no reinicia](#grub-reboot_no_reinicia)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Prefacio

*   El *gestor de arranque* («bootloader») es el primer programa que se ejecuta cuando se inicia el equipo. Es el responsable de cargar y transferir el control al kérnel de Línux, que, a su vez, inicializa el resto del sistema operativo.

*   El nombre de *GRUB* oficialmente se refiere a la versión 2 del software, consulte [[2]](https://www.gnu.org/software/grub/). Si se está buscando el artículo sobre la versión legacy, consulte [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

*   GRUB soporta el uso del sistema de archivos [Btrfs](/index.php/Btrfs "Btrfs") para la partición root (sin necesidad de una partición `/boot` separada con sistema de archivos distinto) compatible con los algoritmos de compresión zlib o LZO.

*   GRUB no soporta particiones root formateadas con [F2FS](/index.php/F2FS "F2FS"), por lo que será necesario crear una partición `/boot` separada usando un sistema de archivos compatible.

## Sistemas BIOS

### Instrucciones específicas para GUID Partition Table (GPT)

En una configuración BIOS/[GPT](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)") es necesaria crear una [BIOS boot partition](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html). GRUB incrusta su propio `core.img` en esta partición.

**Nota:**

*   Antes de intentar este método tenga en cuenta que no todos los sistemas serán capaces de soportar este esquema de particionado. Lea más sobre [GUID partition table](/index.php/GUID_Partition_Table_(Espa%C3%B1ol)#Sistemas_BIOS "GUID Partition Table (Español)").
*   Esta partición adicional solo la necesita GRUB, en un esquema de particionado BIOS/GPT. Anteriormente, GRUB, en un esquema de particionado BIOS/MBR, usaba el espacio pos-MBR para insertar su `core.img`. Sin embargo, GRUB para GPT, no utiliza el espacio pos-GPT porque dicho espacio no se ajusta a las especificaciones de GPT sobre los límites de 1_mebibyte/2048_sector del disco.
*   Para sistemas [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") esta partición adicional no es necesaria ya que no se lleva a cabo en este caso su incustración en los sectores de arranque.

Cree una partición de un mebibyte (`+1M` con `fdisk` o `gdisk`) en el disco, sin formatearla con un sistema de archivos y asignándole el tipo de partición BIOS boot (`BIOS boot` con fdisk, `ef02` con gdisk (o `bios_grub` si utiliza `parted`). Esta partición puede estar colocada en cualquier parte del disco, pero tiene que estar en los primeros 2 TiB. Esta partición debe ser creada antes instalar GRUB. Cuando la partición esté lista, instale el gestor de arranque de acuerdo con las instrucciones de abajo.

También se puede utilizar el espacio pos-GPT como la partición de arranque BIOS, aunque, como se dijo, no se ajustará a las especificaciones de GPT sobre la alineación de la partición. Debido a que no se puede acceder con regularidad a la partición es posible ignorar el impacto sobre el rendimiento (aunque algunas utilidades de disco mostrarán una advertencia al respecto). Con `fdisk` o `gdisk` cree una partición **n**ew (nueva) que se iniciará en el sector 34 y se extenderá hasta el 2047 y asígnele el tipo indicado. Para tener las particiones visibles al comienzo, considere la posibilidad de crear esta partición la última.

### Instrucciones específicas para Master Boot Record (MBR)

Por lo general, el espacio usable después del [MBR](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") (después de los 512 bytes dedicados a ella, y antes de la primera partición), en cualquier sistema particionado con MBR (o etiquetado como 'msdos') es de 31 Kb, de modo que si hay algún problema de alineación de los cilindros se resuelven en la tabla de particiones. Sin embargo, se recomienda mantener una distancia de aproximadamente 1 a 2 MiB que proporcionará el espacio suficiente para contener `core.img` de GRUB ([FS#24103](https://bugs.archlinux.org/task/24103)). Es recomendable utilizar una herramienta de particionado que permita la alineación de una partición de 1 MiB después del MBR, de modo que se pueda obtener el espacio necesario, y resolver otros problemas fuera de los primeros 512 bytes (que son ajenos a la incrustación de `core.img`).

### Instalación

[Instala](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [grub](https://www.archlinux.org/packages/?name=grub). Este reemplazará a [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/), si está instalado.

**Nota:** La simple instalación del paquete mencionado no actualiza el archivo `/boot/grub/i386-pc/core.img` o los módulos de GRUB en `/boot/grub/i386-pc`. Para ello es necesario actualizarlo de forma explícita utilizando `grub-install`, como se explica a continuación.

#### Instalar los archivos de arranque de grub

Hay cuatro formas de instalar los archivos de arranque de GRUB en un sistema BIOS :

*   [Instalación en el disco](#Instalaci.C3.B3n_en_el_disco) (recomendado),
*   [Instalación en una llave USB](#Instalaci.C3.B3n_en_una_llave_USB) (para rescate)
*   Instalación en una partición o disco sin particiones (no recomendado),
*   [Generar únicamente core.img](#Generar_.C3.BAnicamente_core.img) (el método más seguro, pero requiere de un gestor de arranque diferente, como [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)"), que permitirá interactuar con `/boot/grub/i386-pc/core.img`).

**Nota:** Véase [http://www.gnu.org/software/grub/manual/grub.html#BIOS-installation](http://www.gnu.org/software/grub/manual/grub.html#BIOS-installation) para documentación adicional.

##### Instalación en el disco

**Nota:** El método es específico para la instalación de GRUB en un disco ya particionado (con MBR o GPT), con los archivos de GRUB instalados en `/boot/grub` y los respectivos códigos instalados en la región de los primeros 440 bytes del [MBR](https://en.wikipedia.org/wiki/es:Registro_de_arranque_principal "wikipedia:es:Registro de arranque principal") (no debe confundirse con la tabla de particiones MBR).

Para instalar `grub` en la región de los 440 bytes relativa al código de arranque, también llamada Master Boot Record (siglas en inglés de *«registro de arranque principal»*), tenemos que poblar la carpeta `/boot/grub`, crear `/boot/grub/i386-pc/core.img`, insértela en el sector de los 31KiB (el tamaño mínimo varía dependiendo de la alineación de las particiones) después del MBR, en el caso de disco particionado con MBR (o BIOS Boot Partition en el caso de GPT, indicada con la etiqueta `bios_grub` con parted y con el código `EF02` con gdisk), ejecute:

```
# grub-install --target=i386-pc --recheck --debug /dev/sd*x*
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:** El parámetro `--target=i386-pc` alecciona a `grub-install` para la instalación de GRUB únicamente en sistemas BIOS. Se recomienda siempre usar esta opción para evitar la ambigüedad en grub-install.

Si utiliza [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") para `/boot`, puede instalar GRUB en varios discos físicos.

##### Instalación en una llave USB

Se presume que la primera partición de su llave USB está formateada con FAT32 y es /dev/sdy1

```
# mkdir -p /mnt/usb ; mount /dev/sdy1 /mnt/usb 
# grub-install --target=i386-pc --recheck --debug --boot-directory=/mnt/usb/boot /dev/sdy
# grub-mkconfig -o /mnt/usb/boot/grub/grub.cfg

```

```
# opcional, copia de respaldo de los archivos de configuración de grub.cfg
# mkdir -p /mnt/usb/etc/default
# cp /etc/default/grub /mnt/usb/etc/default
# cp -a /etc/grub.d /mnt/usb/etc

```

```
#  sync ; umount /mnt/usb

```

##### Instalación en una partición o disco sin particiones

**Advertencia:** GRUB **desaconseja seriamente** ser instalado en el sector de arranque de una partición o disco sin particiones, contrariamente a lo que hace GRUB Legacy o Syslinux. Este tipo de configuración es propensa a la ruptura, sobre todo durante las actualizaciones, y **no es tratado** por los desarrolladores de Arch.

Para instalar grub en el sector de arranque de una partición o disco sin particiones (por ejemplo, superfloppy), hay que ejecutar (suponiendo que el dispositivo es `/dev/sdaX` y que corresponde a la partición `/boot`):

```
# chattr -i /boot/grub/i386-pc/core.img
# grub-install --target=i386-pc --recheck --debug --force /dev/sdaX
# chattr +i /boot/grub/i386-pc/core.img

```

**Nota:**

*   El dispositivo `/dev/sdaX` es usado únicamente como ejemplo.
*   El parámetro `--target=i386-pc` instruye a `grub-install` para la instalación de GRUB únicamente en sistemas BIOS. Se recomienda siempre usar esta opción para eliminar la ambigüedad en *grub-install*.

Necesitará la opción `--force` para permitir el uso de blocklists, pero no se debe usar `--grub-setup=/bin/true` (lo que equivale a generar únicamente `core.img`).

`grub-install` emitirá los mensajes de advertencia que sirven para explicar los riesgos de este enfoque:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists. 
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

Sin la opción `--force`, recibirá el siguiente error y, consiguientemente, `grub-setup` no podrá instalar su propio código en el MBR.

```
/sbin/grub-setup: error: will not proceed with blocklists

```

Especificando `--force`, sin embargo, debe obtener:

```
Installation finished. No error reported.

```

El motivo de ello es porque `grub-setup` no realiza automáticamente esta operación al instalar el gestor de arranque en una partición, o en un disco sin particiones, ya que `grub` se basa en los mismos blocklists integrados en el sector de arranque de la partición para localizar `/boot/grub/i386-pc/core.img` y la ruta del directorio `/boot/grub`. Las áreas que contienen los archivos de arriba pueden cambiar en caso de alteración de la partición (al copiar o borrar archivos, etc.) Para obtener más información, consulte [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) y [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915).

La solución propuesta consiste en establecer una etiqueta permanente a `/boot/grub/i386-pc/core.img`, de modo que la posición de `core.img` en el disco no se vea alterada. La etiqueta permanente de `/boot/grub/i386-pc/core.img` es necesaria establecerla solo si `grub` se encuentra instalado en el sector de arranque de una partition o disco sin particiones, y no en el caso de una instalación sencilla en el MBR o de la generación de `core.img` sin incorporarla en ningún sector de arranque (mencionado anteriormente).

Por desgracia, el archivo grub.cfg creado no contendrá el UUID apropiado que permita el arranque, aunque no se emitan informes de errores. Vea [https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604](https://bbs.archlinux.org/viewtopic.php?pid=1294604#p1294604). Con el fin de solucionar este problema ejecute las siguientes órdenes:

```
# mount /dev/sdxY /mnt        #Partición root.
# mount /dev/sdxZ /mnt/boot   #Partición boot (si se tiene una).
# arch-chroot /mnt
# pacman -S linux
# grub-mkconfig -o /boot/grub/grub.cfg

```

##### Generar únicamente core.img

Para completar la carpeta `/boot/grub` y generar un archivo `/boot/grub/i386-pc/core.img` **sin** instalar `grub` en el MBR, añada `--grub-setup=/bin/true` a `grub-install`:

```
# grub-install --target=i386-pc --grub-setup=/bin/true --recheck --debug /dev/sda

```

**Nota:**

*   El dispositivo `/dev/sdaX` es usado únicamente como ejemplo.
*   El parámetro `--target=i386-pc` instruye a `grub-install` para la instalación de GRUB únicamente en sistemas BIOS. Se recomienda siempre usar esta opción para eliminar la ambigüedad en grub-install.

A continuación, puede realizar el traslado de `core.img` de GRUB desde GRUB Legacy o syslinux como si fuese un kérnel de Línux o un kérnel multiarranque.

## Sistemas UEFI

**Nota:**

*   Es recomendable consultar las páginas [UEFI (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), [GPT (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)") y [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)") antes de seguir esta parte.
*   Al instalar utilizar UEFI es importante iniciar la instalación con el ordenador en la modalidad UEFI. El soporte de instalación de Arch Linux dispone de UEFI con capacidad de arranque.

### Comprobar si se está utilizando GPT y una partición EFI del sistema (ESP)

Se necesita una partición de sistema EFI (ESP) en cada disco que quiera arrancar con EFI. Una tabla de particiones GPT no es estrictamente necesaria, pero es muy recomendable y es el único método actualmente apoyado en este artículo. Si va a instalar Archlinux en un equipo EFI-compatible con un sistema operativo ya funcionando, como Windows 8, por ejemplo, es muy probable que ya tenga una ESP. Para comprobar si usa GPT y una ESP (siglas en inglés de *EFI System partition* —partición EFI del sistema—), utilice `parted` como root para imprimir la tabla de particiones del disco que desea arrancar (en el ejemplo utilizado aquí se denomina `/dev/sda`.)

```
# parted /dev/sda print

```

Si se utiliza GPT, la orden debe informar: «Partition Table: GPT». Para saber si se usa la modalidad EFI, busque una pequeña partición (de 512 MiB o menos), con un sistema de archivos vfat y la etiqueta «boot» activada. En ella, debe haber una carpeta llamada «EFI». Si se cumplen estos criterios, esta es la ESP. Tome nota del número de la partición, pues tendrá que saber cuál es para que pueda montarla, más adelante, durante la instalación de GRUB en ella.

### Crear una EFI System partition

Si no se tiene una ESP, tendrá que crearla. Siga las instrucciones de [Unified Extensible Firmware Interface (Español)#EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#EFI_System_Partition "Unified Extensible Firmware Interface (Español)") para saber cómo crear una.

### Instalación

**Nota:** Es bien sabido que los fabricantes de placas base no implementan los firmware de UEFI de modo homogéneo. Los ejemplos de instalación descritos a continuación están destinados a trabajar en la más amplia gama de sistemas UEFI posibles. Se anima a los usuarios que experimenten problemas, a pesar de la aplicación de los métodos descritos, a compartir información detallada de sus casos específicos de hardware, cuando hayan encontrado solución a sus problemas. Para estos casos especiales se ha proporcionado un página de [ejemplos para GRUB EFI](/index.php/GRUB_EFI_Examples "GRUB EFI Examples").

Esta sección asume que está instalando GRUB para sistemas x86_64 (x86_64-efi). Para sistemas i686, sustituya `x86_64-efi` con `i386-efi` donde proceda.

Asegúrese de que está en una shell de [bash](/index.php/Bash "Bash"). Por ejemplo, cuando se arranca desde la ISO de Arch:

```
# arch-chroot /mnt /bin/bash

```

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") los paquetes [grub](https://www.archlinux.org/packages/?name=grub) y [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr). *GRUB* es el gestor de arranque, *efibootmgr* crea las entradas stub `.efi` con capacidad de arranque usadas por el script de instalación de GRUB.

Los siguientes pasos instalan la aplicación GRUB UEFI en `**$esp**/EFI/grub`, instala los módulos en `/boot/grub/x86_64-efi`, y coloca el stub `grubx64.efi` booteable en `**$esp**/EFI/grub_uefi`.

En primer lugar, le decimos a GRUB que utilice UEFI, que establezca el directorio de arranque y que establezca el ID. del gestor de arranque. Cambie `$esp` con su partición efi (normalmente `/boot`):

```
# grub-install --target=x86_64-efi --efi-directory=**$esp** --bootloader-id=**grub_uefi** --recheck

```

La identificación del gestor de arranque es el que aparece en las opciones de arranque para identificar la opción de arranque de GRUB EFI; asegurarse de que esto es algo que pueda reconocer más tarde.

Después de lo anterior, la instalación completa el directorio principal de GRUB localizado en `/boot/grub/`.

No se olvide de [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal) después de finalizar la configuración adicional dependiendo de su [#Configuración](#Configuraci.C3.B3n).

**Nota:**

*   Mientras que algunas distribuciones requieren un directorio `/boot/efi` o `/boot/EFI`, Arch no lo necesita.
*   `--efi-directory` y `--bootloader-id` son específicos de GRUB UEFI. `--efi-directory` especifica el punto de montaje de la ESP. Este sustituye a `--root-directory`, que está obsoleto. `--bootloader-id` especifica el nombre del directorio utilizado para guardar el archivo `grubx64.efi`.
*   Es posible que note la ausencia de una opción <device_path> (por ejemplo: `/dev/sda`) en la orden `grub-install`. De hecho cualquier <device_path> proporcionado será ignorado por el script de instalación de GRUB, dado que los gestores de arranque de UEFI no utilizan un MBR o sector de arranque de la partición en absoluto.

Véase [solución de problemas de UEFI](#UEFI_.28Espa.C3.B1ol.29) en caso de problemas.

### Lecturas complementarias

A continuación se muestra otra información pertinente relativa a la instalación de Arch a través de UEFI

#### Método alternativo de instalación

Por lo general, GRUB guarda todos los archivos, incluyendo los archivos de configuración, en `/boot`, independientemente del lugar donde se monta EFI System Partition.

Si desea guardar estos archivos dentro de la misma partición UEFI del sistema, añada `--boot-directory=$esp` a la orden grub-install:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub --boot-directory=$esp --recheck --debug

```

De este modo, los archivos de GRUB vendrán instalados en `$esp/grub` en lugar de `/boot/grub`. Usando este método, grub.cfg se guarda en la partición UEFI del sistema, así que asegúrese de que señala el lugar correcto en *grub-mkconfig* durante la fase de configuración:

```
# grub-mkconfig -o $esp/grub/grub.cfg

```

El resto de la configuración es idéntica.

#### Solución alternativa a firmware de UEFI

Algunos firmware UEFI requieren que el código de arranque `.efi` tenga un nombre específico y está colocado en un lugar específico: `$esp/EFI/boot/bootx64.efi` (donde `$esp` es el punto de montaje de la partición UEFI). Si no se hace así, se traducirá, en estos casos, en una instalación que no arranca. Afortunadamente, esto no va a causar ningún problema con otros firmware que no necesitan estas condiciones.

Para solucionar de momento este escollo, debe crear primero el directorio necesario, y luego copiar el código `.efi` de grub, renombrándolo adecuadamente durante este proceso:

```
# mkdir $esp/EFI/boot
# cp $esp/EFI/arch_grub/grubx64.efi  $esp/EFI/boot/bootx64.efi

```

#### Crear una entrada de GRUB en el gestor de arranque del firmware

`grub-install` intentará crear automáticamente una entrada de menú en el gestor de arranque. Si no es así, véase [Unified Extensible Firmware Interface (Español)#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#efibootmgr "Unified Extensible Firmware Interface (Español)") para obtener instrucciones sobre cómo usar `efibootmgr` a fin de crear una entrada en el menú. De todas formas, el problema probablemente sea que no se ha arrancado el CD/USB en la modalidad UEFI, como se indica en [Unified Extensible Firmware Interface (Español)#Crear un USB arrancable con UEFI desde la ISO](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Crear_un_USB_arrancable_con_UEFI_desde_la_ISO "Unified Extensible Firmware Interface (Español)")

#### GRUB Standalone

Esta sección asume que está creando un GRUB independiente para sistemas x86_64 (x86_64-efi). Para los sistemas i686, sustituya `x86_64-efi` con `i386-efi` en su caso.

Es posible crear una aplicación `grubx64_standalone.efi` que tiene todos los módulos integrados en un archivo tar dentro de la aplicación UEFI, eliminando así la necesidad de tener un directorio aparte para contener todos los módulos de UEFI GRUB y otros archivos relacionados. Esto se hace usando la orden `grub-mkstandalone` (incluida en [grub](https://www.archlinux.org/packages/?name=grub)) como sigue:

```
# echo 'configfile ${cmdpath}/grub.cfg' > /tmp/grub.cfg                                ## utilice comillas simples, ${cmdpath} debe estar presente tal cual es
# grub-mkstandalone -d /usr/lib/grub/x86_64-efi/ -O x86_64-efi --modules="part_gpt part_msdos" --fonts="unicode" --locales="en@quot" --themes="" -o "$esp/EFI/grub/grubx64_standalone.efi"  "/boot/grub/grub.cfg=/tmp/grub.cfg" -v

```

A continuación, copie el archivo de configuración de GRUB a `$esp/EFI/grub/grub.cfg` y cree una entrada en el gestor de arranque de UEFI para `$esp/EFI/grub/grubx64_standalone.efi` utilizando [efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#efibootmgr "Unified Extensible Firmware Interface (Español)").

**Nota:** La opción `--modules="part_gpt part_msdos"` (con las comillas) es necesaria para que la característica `${cmdpath}` funcione correctamente.

**Advertencia:** Puede encontrarse que el archivo `grub.cfg` no se carga debido a que falta una barra `${cmdpath}` (por ejemplo, `(hd1,msdos2)EFI/Boot` en lugar de `(hd1,msdos2)/EFI/Boot`), razón por lo que no se lanza en un shell de GRUB. Si esto sucede, verifique cúal es el ajuste de `${cmdpath}` (con la orden `echo ${cmdpath}` ) y luego cargue manualmente la configuración manual del archivo (por ejemplo, `configfile (hd1,msdos2)/EFI/Boot/grub.cfg`).

#### Información Técnica

El archivo GRUB EFI siempre espera que su archivo de configuración esté en `${prefix}/grub.cfg`. Sin embargo, en el archivo EFI de GRUB standalone, el `${prefix}` se encuentra dentro de un archivo tar incrustado en el propio archivo EFI de GRUB standalone (dentro de grub se reconoce por `"(memdisk)"`, sin comillas). Este archivo tar contiene todos los archivos que se almacenan normalmente en `/boot/grub` en el caso de una instalación normal de GRUB EFI.

Debido a esta incorporación del contenido de `/boot/grub` dentro de la propia imagen standalone, dicho contenido no está presente en `/boot/grub` (externo) para nada. Así, tanto el archivo EFI de GRUB standalone, `${prefix}==(memdisk)/boot/grub`, como el resto de archivos EFI de GRUB standalone leídos, esperan que el archivo de configuración se encuentre en `${prefix}/grub.cfg==(memdisk)/boot/grub/grub.cfg`.

Para asegurarse que el archivo EFI de GRUB standalone lea el archivo `grub.cfg` externo ubicado en el mismo directorio que el archivo EFI (reconocido en grub como `${cmdpath}` ), crearemos un simple archivo `/tmp/grub.cfg` que oblique a GRUB a utilizar `${cmdpath}/grub.cfg` como su archivo de configuración (al ejecutar la orden `configfile ${cmdpath}/grub.cfg` en `(memdisk)/boot/grub/grub.cfg`). Entonces indicamos a grub-mkstandalone que copie el archivo `/tmp/grub.cfg` a `${prefix}/grub.cfg` (que en realidad es `(memdisk)/boot/grub/grub.cfg`) utilizando la opción `"/boot/grub/grub.cfg=/tmp/grub.cfg"`.

De esta manera el archivo EFI de GRUB standalone y el archivo `grub.cfg` vigente se pueden almacenar en cualquier directorio dentro de la partición EFI del sistema (siempre que se encuentren en el mismo directorio), lo que los hace portables.

## Generar el archivo de configuración principal

Después de la instalación, necesita crear el archivo de configuración principal `grub.cfg`. El proceso de generación puede estar influenciada por una variedad de opciones presentes en `/etc/default/grub` y de scripts en `/etc/grub.d/`, lo cual se trata en la sección [#Configuración](#Configuraci.C3.B3n)

Si no se ha hecho una configuración adicional, la generación automática determinará el sistema de archivos raíz del sistema que el archivo de configuración arrancará. Para que esto tenga éxito es importante que el sistema o bien sea arrancable o bien se haga dentro de chroot.

**Nota:** Recuerde que `grub.cfg` tiene que ser regenerado después de realizar cualquier cambio en los archivos `/etc/default/grub` o `/etc/grub.d/*`.

Utilice la utilidad *grub-mkconfig* para generar el archivo `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:**

*   La ruta del archivo es `/boot/grub/grub.cfg`, no `/boot/grub/i386-pc/grub.cfg`.
*   Si se está tratando de ejecutar *grub-mkconfig* en entorno chroot o en un contenedor *systemd-nspawn*, es posible que advierta que no funciona, avisándole de que *grub-probe* no puede obtener el "canonical path of /dev/sdaX". En este caso, pruebe usando *arch-chroot* como se describe [aquí](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067).

Por defecto, los scripts de generación añaden automáticamente las entradas de menú para Arch Linux a cualquier configuración generada. Véase [#Arranque dual](#Arranque_dual) para configuraciones avanzadas.

## Configuración

Esta sección cubre solo la edición del archivo de configuración `/etc/default/grub`. Véase [GRUB/Tips and tricks (Español)](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol) "GRUB/Tips and tricks (Español)") si necesita más opciones.

Recuerde siempre [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal) después de realizar cambios en `/etc/default/grub`.

### Argumentos adicionales

Para pasar argumentos adicionales personalizados a la imagen de Línux, se pueden ajustar las variables `GRUB_CMDLINE_LINUX` + `GRUB_CMDLINE_LINUX_DEFAULT` en `/etc/default/grub`. Los dos parámetros se anexan al archivo y se pasan al kérnel al generar las entradas de arranque regulares. Para la *recuperación* del sistema, solo se usa la variable `GRUB_CMDLINE_LINUX`.

No es necesario el uso de ambos, pero puede ser útil . Por ejemplo , podría utilizar `GRUB_CMDLINE_LINUX_DEFAULT="resume=/dev/sdaX quiet"` cuando `sda**X**` es la partición de intercambio (swap) para activar la reanuddación del sistema tras la hibernación. Esto generaría una entrada de arranque de reanudación y sin el parámetro *quiet* que no mostraría los mensajes del kérnel durante el arranque desde esa entrada. Sin embargo, las otras entradas del menú (regulares) seguirían teniendo las demás opciones.

Para generar la entrada de recuperación en GRUB también hay que comentar `#GRUB_DISABLE_RECOVERY=true` en `/etc/default/grub`.

También se puede usar `GRUB_CMDLINE_LINUX="resume=/dev/disk/by-uuid/${swap_uuid}"`, cuando `${swap_uuid}` es la [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") de la partición de intercambio.

Las entradas múltiples se separan por espacios dentro de comillas dobles. Por lo tanto, si desea usar tanto la función de reanuación como systemd, se vería así: `GRUB_CMDLINE_LINUX="resume=/dev/sdaX init=/usr/lib/systemd/systemd"`

Véase [Kernel parameters (Español)](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para obtener más información.

### Arranque dual

**Sugerencia:** Si desea que *grub-mkconfig* busque sistemas operativos instalados, debe instalar el paquete [os-prober](https://www.archlinux.org/packages/?name=os-prober).

#### Generación automática utilizando /etc/grub.d/40_custom y grub-mkconfig

La mejor manera de agregar otras entradas está editando el archivo `/etc/grub.d/40_custom` o `/boot/grub/custom.cfg`. El contenido de estos archivos se agregan automáticamente al ejecuta r`grub-mkconfig`. Después de añadir las nuevas líneas, ejecute:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

o, para modalidad UEFI-GPT:

 `# grub-mkconfig -o /boot/efi/EFI/GRUB/grub.cfg` 

para actualizar `grub.cfg`.

Por ejemplo, un típico archivo `/etc/grub.d/40_custom`, podría ser similar a uno como el siguiente, creado para [HP Pavilion 15-e056sl Notebook PC](http://h10025.www1.hp.com/ewfrf/wc/product?cc=us&destPage=product&lc=en&product=5402703&tmp_docname=), originalmente con Microsoft Windows 8 preinstalado. Cada `menuentry` debe mantener una estructura similar a una de las de abajo. Tenga en cuenta que la partición UEFI `/dev/sda2` dentro de GRUB se llama `hd0,gpt2` y `ahci0,gpt2` (véase [esto](#Windows_Installed_in_UEFI-GPT_Mode_menu_entry) para obtener más información).

 `/etc/grub.d/40_custom` 
```
#!/bin/sh
exec tail -n +3 $0
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.

menuentry "HP / Microsoft Windows 8.1" {
	echo "Cargando HP / Microsoft Windows 8.1..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader /EFI/Microsoft/Boot/bootmgfw.efi
}

menuentry "HP / Microsoft Control Center" {
	echo "Cargando HP / Microsoft Control Center..."
	insmod part_gpt
	insmod fat
	insmod search_fs_uuid
	insmod chain
	search --fs-uuid --no-floppy --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2 763A-9CB6
	chainloader /EFI/HP/boot/bootmgfw.efi
}

menuentry "Apagar sistema" {
	echo "Apagando el sistema..."
	halt
}

menuentry "Reiniciar sistema" {
	echo "Reiniciando el sistema..."
	reboot
}
```

##### Entrada de menú para GNU/Línux

Suponiendo que la otra distribución está en la partición `sda2`:

```
menuentry "Otro Línux" {
	set root=(hd0,2)
	linux /boot/vmlinuz (añadir otras opciones aquí necesarias)
	initrd /boot/initrd.img (si el otro kérnel utiliza/necesita una)
}
```

De otra forma, puede dejar que grub busque la partición correcto por la *UUID* o *label*:

```
menuentry "Otro Línux" {
        # suponiendo que la UUID es 763A-9CB6
	search --set=root --fs-uuid 763A-9CB6

        # buscar por label OTRO_LINUX (asegúrese de que la etiqueta de la partición no es ambigua)
        #search --set=root --label OTRO_LINUX

	linux /boot/vmlinuz (añadir otras opciones aquí necesarias, por ejemplo: root=UUID=763A-9CB6)
	initrd /boot/initrd.img (si el otro kérnel utiliza/necesita una)
}
```

##### Entrada de menú para FreeBSD

Requiere que FreeBSD está instalado en una partición con UFS. Suponiendo que está instalado en `sda4`:

###### Cargar directamente el kérnel

```
menuentry 'FreeBSD' {
	insmod ufs2
	set root='hd0,gpt4,bsd1'
	## o 'hd0,msdos4,bsd1', si utiliza una tabla de particiones estilo IBM-PC (MS-DOS)
	kfreebsd /boot/kernel/kernel
	kfreebsd_loadenv /boot/device.hints
	set kFreeBSD.vfs.root.mountfrom=ufs:/dev/ada0s4a
	set kFreeBSD.vfs.root.mountfrom.options=rw
}
```

###### Cargar en cadena el registro de arranque embebido

```
menuentry 'FreeBSD' {
	insmod ufs2
	set root='hd0,gpt4,bsd1'
	chainloader +1
}
```

##### Entrada de menú para Windows XP

Asumimos que la partición de Windows es `sda3`. Recuerde que necesita señalar «set root» y «chainloader» con relación a la partición del sistema de reserva que windows hizo cuando se instaló, no la partición donde Windows está instalado. Este ejemplo funciona si la partición de reserva del sistema es `sda3`.

```
# (2) Windows XP
menuentry "Windows XP" {
	set root="(hd0,3)"
	chainloader +1
}
```

Si el gestor de arranque de Windows está activo en un disco duro completamente diferente a donde está instalado GRUB, puede ser necesario engañar a Windows haciéndole creer que se trata de la primera unidad del disco duro. Esto es posible con `drivemap`. Suponiendo que GRUB está activo en `hd0` y Windows en `hd2`, es necesario añadir lo siguiente después de `set root`:

 `drivemap -s hd0 hd2` 

##### Entrada de menú para Windows instalado en modo UEFI-GPT

**Nota:** Estas «menuentry» (*entradas*) solo funcionarán en el modo de inicio de UEFI y solo si el valor de bits de Windows coincide con el valor de bits de UEFI. Sin embarbo, esto **NO FUNCIONA** en grub(2) instalado en sistemas BIOS. Véase [esto](/index.php/Windows_and_Arch_Dual_Boot#Windows_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot") y [esto](/index.php/Windows_and_Arch_Dual_Boot#Bootloader_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot") para más información.

```
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8 x86_64 UEFI-GPT" {
		insmod part_gpt
		insmod fat
		insmod search_fs_uuid
		insmod chain
		search --fs-uuid --set=root $hints_string $uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi
```

donde `$hints_string` y `$uuid` se obtienen de las siguientes dos órdenes. Orden para obtener `$uuid`:

```
# grub-probe --target=fs_uuid $esp/EFI/Microsoft/Boot/bootmgfw.efi
1ce5-7f28
```

Orden para obtener `$hints_string`:

```
# grub-probe --target=hints_string $esp/EFI/Microsoft/Boot/bootmgfw.efi
 --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1
```

Estas dos órdenes asumen que la ESP que utiliza Windows está montada en $esp. Puede haber casos diferentes en la ruta al archivo EFI de Windows, lo que afectaría al comienzo de Windows, y al resto.

##### Entrada de menú para «Apagar»

```
menuentry "Apagar sistema" {
	echo "Apagando el sistema..."
	halt
}
```

##### Entrada de menú para «Reiniciar»

```
menuentry "Reiniciar sistema" {
	echo "Reiniciando el sistema..."
	reboot
}
```

##### Entrada de menú para Windows instalado en modo BIOS-MBR

**Nota:** GRUB soporta el arranque de `bootmgr` y ya no es necesario cargar el sector de arranque de la partición para iniciar Windows en una configuración de BIOS-MBR.

**Advertencia:** La **system partition**, donde está `bootmgr`, no es la partición «real» de Windows (normalmente C:). Al mostrar las particiones con la orden `blkid`, dicha partición del sistema es la señalada como `LABEL="SYSTEM RESERVED"` o `LABEL="SYSTEM"` y cuenta con 100 a 200 MB de tamaño (como la partición boot de Arch). Véase [Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") para obtener más información.

A lo largo de esta sección, se asume que la partición de Windows es `/dev/sda1`. Una partición diferente, cambiar todas las instancias de hd0,msdos1\. En primer lugar, encontre el UUID del sistema de archivos NTFS de la SYSTEM PARTITION de Windows donde reside `bootmgr` y sus archivo. Por ejemplo, si `bootmgr` de Windows está presente en `/media/SYSTEM_RESERVED/bootmgr`:

Para Windows Vista/7/8/8.1:

```
# grub-probe --target=fs_uuid /media/SYSTEM_RESERVED/bootmgr
69B235F6749E84CE

```

```
# grub-probe --target=hints_string /media/SYSTEM_RESERVED/bootmgr
--hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1

```

**Nota:** Para Windows XP, sustituya `bootmgr` con `NTLDR` en la órdenes anteriores. Y tenga en cuenta que puede no haber una partición SYSTEM_RESERVED separada; bastaría con analizar el archivo NTLDR en la partición de Windows.

A continuación, agregue el siguiente código en `/etc/grub.d/40_custom` o `/boot/grub/custom.cfg` y regenere `grub.cfg` con `grub-mkconfig` como se explicó anteriormente para iniciar Windows (XP, Vista, 7 o 8) instalado en modalidad BIOS-MBR:

**Nota:** Estas entradas solo funcionarán en la modalidad de arranque de Legacy BIOS. NO FUNCIONARÁN en grub(2) instalado en modalidad UEFI. Véase [esto](/index.php/Windows_and_Arch_Dual_Boot#Windows_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot") y [esto](/index.php/Windows_and_Arch_Dual_Boot#Bootloader_UEFI_vs_BIOS_limitations "Windows and Arch Dual Boot").

Para Windows Vista/7/8/8.1:

```
if [ "${grub_platform}" == "pc" ]; then
 menuentry "Microsoft Windows Vista/7/8/8.1 BIOS-MBR" {
   insmod part_msdos
   insmod ntfs
   insmod search_fs_uuid
   insmod ntldr     
   search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
   ntldr /bootmgr
  }
fi

```

Para Windows XP:

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows XP" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
    ntldr /bootmgr
  }
fi

```

**Nota:** En algunos casos, al intalar GRUB antes de una instalación limpia de Windows 8, da como resultado que no arranque Windows, provocando un error con `\boot\bcd` (código de error `0xc000000f`). Se puede arreglar llamando a la consola de recuperación de Windows (cmd desde disco de instalación) y ejecutando:
```
x:\> "bootrec.exe /fixboot" 
x:\> "bootrec.exe /RebuildBcd".

```
**No** haga uso de `bootrec.exe /Fixmbr` porque dejará GRUB al margen.

El archivo `/etc/grub.d/40_custom` se puede utilizar como una plantilla para crear `/etc/grub.d/nn_custom`. Donde `nn` define la prelación, que indica el orden en que los scritps se ejecutan. El orden de los scripts al ejecutarse determina su lugar en el menú de arranque de grub.

**Nota:** `nn` debe ser mayor que 06 para asegurarse de que los scripts necesarios se ejecutan primero.

#### Con Windows usando EasyBCD y NeoGRUB

Puede que NeoGRUB de EasyBCD no entienda el nuevo formato del menú de GRUB, por lo que será necesario efectuar la carga de GRUB, reemplazando el contenido de su `C:\NST\menu.lst` con:

```
default 0
timeout 1

```

```
title       Cargar en cadena con GRUB v2
root        (hd0,7)
kernel      /boot/grub/i386-pc/core.img

```

Por último, [regenere el archivo principal de GRUB](#Generar_el_archivo_de_configuraci.C3.B3n_principal).

#### parttool para mostrar/ocultar particiones

Si tiene instalado Windows 9x con el disco `C:\` oculto, GRUB dispone de las opciones `hide/unhide` usando `parttool`. Por ejemplo, para efectuar el arranque del tercer disco `C:\` de tres sistema Windows 9x instalados, se inicia la consola y se escribe:

```
parttool hd0,1 hidden+ boot-
parttool hd0,2 hidden+ boot-
parttool hd0,3 hidden- boot+
set root=hd0,3
chainloader +1
boot
```

### LVM

Si utiliza [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") para `/boot`, asegúrese de que el módulo `lvm` se carga antes:

 `/etc/default/grub`  `GRUB_PRELOAD_MODULES="lvm"` 

y especifíque el parámetro del kérnel `root`:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="root=lvm/*lvm_group_name*-*lvm_logical_boot_partition_name* ..."` 

### RAID

GRUB permite tratar los volúmenes en una configuración RAID de una manera sencilla. Añadimos `insmod raid` a `grub.cfg` que hará referencia al volumen de forma nativa. Por ejemplo, `/dev/md0` se convierte en:

```
set root=(md0)

```

mientras que un volumen RAID particionado (por ejemplo, `/dev/md0p1`) se convierte en:

```
set root=(md0,1)

```

Para instalar GRUB cuando se utiliza RAID 1 como partición `/boot` (o usando `/boot` alojado en una partición root RAID1), en dispositivos con GPT ef02/'BIOS boot partition', basta ejecutar *grub-install* en ambas unidades, así:

```
# grub-install --target=i386-pc --recheck --debug /dev/sda
# grub-install --target=i386-pc --recheck --debug /dev/sdb

```

donde la matriz RAID1 que aloja `/boot` se encuentra en `/dev/sda` y `/dev/sdb`.

### Múltiples entradas

Para obtener consejos sobre la gestión de múltiples entradas de GRUB, por ejemplo cuando se utiliza kernels tanto [linux](https://www.archlinux.org/packages/?name=linux) como [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), vea [GRUB/Tips and tricks#Multiple entries](/index.php/GRUB/Tips_and_tricks#Multiple_entries "GRUB/Tips and tricks").

### Encriptación

#### Partición raíz

Para cifrar el sistema de archivos root, es necesario editar `/etc/default/grub` con los parámetros necesarios para desbloquear el sistema de archivos cifrados durante el arranque. Por ejemplo, si el hook `encrypt` es usado en [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"), el parámetro `cryptdevice` debe ser añadido a la orden `GRUB_CMDLINE_LINUX=""`. En el siguiente ejemplo, la partición `sda2` se ha cifrado como `/dev/mapper/cryptroot`:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:cryptroot"` 

Una vez que `/etc/default/grub` ha sido enmendado, entonces será necesario [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal).

Para más información sobre la configuración del gestor de arranque para los dispositivos cifrados, ver [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

**Sugerencia:** Si está actualizando la configuración GRUB Legacy a GRUB, compruebe `/boot/grub/menu.lst.pacsave` para la correcta identificación del dispositivo/etiqueta a añadir. Búsquelos después del texto `kernel /vmlinuz-linux`.

#### Partición de arranque

El [parámetro](https://dada.cs.washington.edu/doc/grub2-tools-2.02/grub.html#Simple-configuration) `GRUB_ENABLE_CRYPTODISK` de GRUB se puede utilizar para permitir a GRUB que pida una contraseña para abrir un dispositivo de bloque [LUKS](/index.php/LUKS "LUKS") para leer su configuración y cargar cualquier [initramfs](/index.php/Initramfs "Initramfs") y [kernel](/index.php/Kernel "Kernel") desde él. Esta opción trata de resolver el problema de tener una [partición de arranque sin cifrar](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

La función se activa añadiendo:

```
GRUB_ENABLE_CRYPTODISK=y

```

para `/etc/default/grub`. Después de esta configuración es necesario ejecutar *grub-mkconfig* para [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal) mientras la partición `/boot` cifrada está montada.

**Nota:** `GRUB_ENABLE_CRYPTODISK=1` [no funcionará](https://savannah.gnu.org/bugs/?41524) en oposición a la solicitud mostrada en GRUB 2.02-beta2.

Dependiendo de la configuración de su sistema, tenga en cuenta lo siguiente:

*   Para que la caraterística funcione no es necesario que `/boot` se encuentre en una partición separada, también puede permanecer dentro del árbol de directorios `/` del sistema. Sin embargo, en ambos casos se requiere la introducción de dos contraseñas para arrancar. La primera para GRUB, para desbloquear el punto de arranque `/boot` en la fase temprana del arranque, la segunda para desbloquear el propio sistema de archivos raíz como se describe en [#Partición raíz](#Partici.C3.B3n_ra.C3.ADz).

*   Con el fin de realizar las actualizaciones del sistema que afecten al punto de montaje `/boot`, hay que asegurarse de que `/boot` cifrado esté desbloqueado para volver a montarlo para el initramfs y el kérnel durante el arranque. Con una partición `/boot` separada, esto se puede lograr añadiendo una entrada a `/etc/crypttab` con un archivo de claves. Ver [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration").

*   Si utiliza una distribución de teclado especial, una instalación predeterminada de GRUB no lo sabrá. Esto es relevante para saber cómo introducir la contraseña para desbloquear el dispositivo de bloque de LUKS.

## Utilizar la shell de órdenes

Dado que el MBR es demasiado pequeño para contener todas los módulos de GRUB, solo el menú y los comanos básicos residen allí. La mayor parte de la funcionalidad de GRUB está contenida en los módulos ubicados en `/boot/grub`, que se cargan cuando son necesarios. En caso de errores (por ejemplo, si la tabla de particiones se altera), GRUB puede fallar al arrancar, e lanzar una shell en lugar del clásico menú.

GRUB ofrece diferentes tipos de shell. Si tiene problemas para leer el menú, pero el gestor de arranque es todavía capaz de encontrar el disco donde GRUB reside, es probable que lance una shell «normal»:

```
sh:grub>

```

En caso de problemas más serios (GRUB no puede encontrar los archivos necesarios), puede aparecer la shell de emergencia:

```
grub rescue>

```

La shell de emergencia es una versión reducida de la normal, y ofrece, por lo tanto, un número reducido de funcionalidades. Trate de cargar el módulo `normal`, e iniciar la shell clásica:

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/i386-pc/normal.mod
rescue:grub> normal
```

### Soporte para Pager

GRUB apoya pager (paginador o localizador) que permite la lectura de las órdenes que proveen *«salidas»* extensas (como la orden `help`). Tenga en cuenta que esta característica solo está disponible en la consola normal, y no en una de emergencia. Para activar pager, escriba en una shell de órdenes de GRUB:

```
sh:grub> set pager=1

```

### Usar el entorno de la shell de órdenes para arrancar distintos sistemas operativos

```
grub> 

```

El entorno de la shell de órdenes de GRUB puede utilizarse para arrancar sistemas operativos. Un escenario común puede iniciar Windows/Línux localizado en una unidad/partición a través de **chainloading**.

*Chainloading* significa cargar otro sistema de arranque desde el vigente, es decir, cargar en cadena.

El otro cargador de arranque puede estar incrustado en el principio del disco (MBR) o en el principio de una partición.

#### Cargar una partition

```
set root=(hdX,Y)
chainloader +1
boot

```

X=0,1,2... Y=1,2,3...

Por ejemplo, para cargar Windows localizado en la primera particion del primer disco duro,

```
set root=(hd0,1)
chainloader +1
boot

```

Del mismo modo, puede ser cargado GRUB instalado en una partición.

#### Cargar un disco/unidad

```
set root=hdX
chainloader +1
boot

```

#### Cargar en cadena Windows/Línux instalados en modalidad UEFI

```
insmod ntfs
set root=(hd0,gpt4)
chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
boot

```

*insmod ntfs* se utiliza para cargar el módulo del sistema de archivos NTFS para cargar Windows. (hd0,gpt4) o /dev/sda4 es la EFI System Partition (ESP). La entrada en la línea *chainloader* especifica la ruta del archivo .efi para ser cargado.

#### Carga normal

Véanse los ejemplos mostrados en el apartado de [#Utilizar la consola de emergencia](#Utilizar_la_consola_de_emergencia)

### Utilizar la consola de emergencia

Véase primero [#Utilizar la shell de órdenes](#Utilizar_la_shell_de_.C3.B3rdenes) más arriba. Si no es capaz de iniciar la shell estándar, una posible solución es arrancar un LiveCD o alguna otra distribución a modo de recuperación para corregir los errores de configuración y reinstalar GRUB. Sin embargo, un disco de recuperación no siempre es posible (ni necesario), y la consola de emergencia es sorprendentemente robusta.

Las órdenes disponibles en esta modalidad incluyen `insmod`, `ls`, `set` y `unset`. Este ejemplo utiliza `set` y `insmod`. `set` cambia el valor de las variables, mientras que `insmod` añade nuevos módulos para ampliar la funcionalidad básica.

Antes de comenzar, es necesario que conozca la ubicación de `/boot` (ya esté en una partición separada o en un directorio dentro de la partición de root):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

Donde X es el número de la unidad y la Y de la partición. Para ampliar las capacidades de la consola, inserte el módulo `linux`.

```
grub rescue> insmod (hdX,Y)/boot/grub/linux.mod

```

**Nota:** Si está usando una partición de arranque separada, se omite `/boot` en la ruta. (por ejemplo, `set prefix=(hdX,Y)/grub`).

Esto proporciona órdenes de `linux` y `initrd`, con las que debe estar familiarizado (véase [#Configuración](#Configuraci.C3.B3n)).

Un ejemplo de inicio de Arch Linux:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot

```

De nuevo, en el caso de partición de arranque separada, cambie las órdenes en consecuencia:

```
set root=(hd0,5)
linux /vmlinuz-linux root=/dev/sda6
initrd /initramfs-linux.img
boot

```

**Nota:** Si se experimentó `error: premature end of file /YOUR_KERNEL_NAME` durante la ejecución de la orden `linux`, pruebe usuando `linux16` en su lugar.

Tras el lanzamiento de una instalación correcta de Arch Linux, puede arreglar `grub.cfg` y proceder a la reinstalación de GRUB.

Para reinstalar GRUB y arreglar completamente el problema, cambie `/dev/sda` de acuerdo a sus propias necesidades. Consulte el apartado sobre [#Instalación](#Instalaci.C3.B3n) para más detalles.

## Solución de problemas

### Algunas BIOS de Intel no efectúan el arranque de la partición GPT

#### MBR

Algunas BIOS de Intel requieren, al menos, una partición MBR marcada como booteable en el arranque, cosa no habitual en las configuraciones basadas en GPT, que provocan que la partición GPT no se inicie.

Es posible solucionar el problema mediante el uso de (por ejemplo) fdisk para marcar como bootable en el MBR una de las particiones GPT (preferiblemente la partición de 1007KiB que ya se ha creado para GRUB). Esto se puede lograr, utilizando fdisk, mediante las siguientes órdenes: Inicie fdisk sobre el disco donde va a realizar la instalación, por ejemplo `fdisk /dev/sda`, presione `a` y seleccione la partición que desea marcar como booteable (seguramente #1) pulsando el número correspondiente, para terminar pulse `w` para escribir los cambios en el MBR.

**Nota:** Debemos tener en cuenta que para marcar como booteable una partición hay que hacerlo con la utilidad `fdisk` o similar, no se puede hacer con GParted o equivalentes, ya que estos últimos no establecen el indicador de booteable en el MBR.

Para más información consulte [esto](http://www.rodsbooks.com/gdisk/bios.html)

#### Ruta EFI

Algunos firmware UEFI requieren un archivo de arranque en una ubicación conocida antes de poder mostrar las entradas de arranque UEFI NVRAM. Si este es el caso, `grub-install` indicará a `efibootmgr` que ha añadido una entrada para arrancar GRUB, sin embargo, la entrada no se mostrará en el selector VisualBIOS para el esquema del orden de arranque. La solución es colocar un archivo en uno de los lugares conocidos. Suponiendo que la partición EFI es en `/boot/efi/`, la siguiente orden solucionará el problema:

```
mkdir /boot/efi/EFI/boot
cp /boot/efi/EFI/grub/grubx64.efi /boot/efi/EFI/boot/bootx64.efi

```

Esta solución funcionó para una placa base Intel DH87MC con firmware fechado en enero de 2014.

### Activar mensajes de depuración de errores en GRUB

**Nota:** Este cambio se sobrescribe al [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal).

Añada:

```
set pager=1
set debug=all

```

en `grub.cfg`.

### Corregir el error de GRUB: «no suitable mode found»

Si recibe este error en la elección de una opción de arranque:

```
error: no suitable mode found
Booting however

```

A continuación, se debe iniciar el terminal gráfico GRUB (`gfxterm`), utilizando un modo de vídeo adecuado (`gfxmode`). Este se transmite de GRUB al kérnel de Línux usando la opción `gfxpayload`. En sistemas UEFI, si la modalidad de video de GRUB no está inicializada, se mostrarán los mensajes de arranque del kérnel (al menos hasta la activación de KMS).

Ahora, copie `/usr/share/grub/unicode.pf2` en `${GRUB2_PREFIX_DIR}` (`/boot/grub` de los sistema BIOS y UEFI). Si GRUB UEFI se instala con la opción `--boot-directory` activada, entonces la ruta es `$esp/EFI/grub`):

```
# cp /usr/share/grub/unicode.pf2 ${GRUB2_PREFIX_DIR}

```

Si el archivo `/usr/share/grub/unicode.pf2` no existe, instale el paquete [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) y proceda a la creación y copia del mismo en `${GRUB2_PREFIX_DIR}`.

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

En el archivo `grub.cfg`, agregue las líneas siguientes para permitir a GRUB que pase correctamente la modalidad de vídeo al kérnel, de lo contrario obtendrá una pantalla en negro, aunque el arranque se haga con normalidad, sin que el sistema se bloquee:

Sistemas BIOS:

```
insmod vbe

```

Sistemas UEFI:

```
insmod efi_gop
insmod efi_uga

```

A continuación, agregue el siguiente código (común a los sistemas BIOS y UEFI)

```
insmod font

```

```
if loadfont ${prefix}/fonts/unicode.pf2
then
    insmod gfxterm
    set gfxmode=auto
    set gfxpayload=keep
    terminal_output gfxterm
fi

```

Como puede ver, para que `gfxterm` funcione correctamente, la fuente `unicode.pf2` debe existir en `${GRUB2_PREFIX_DIR}`.

### Mensaje de error msdos-style

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding won't be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

Este problema se produce cuando se intenta instalar GRUB en VMWare. Más información [aquí](https://bbs.archlinux.org/viewtopic.php?pid=581760#). Se espera una solución pronto.

También puede ocurrir cuando la partición comienza justo después del MBR (bloque 63), sin dejar un espacio de alrededor de 1 MB (2048 bloques) antes de la primera partición. Véase [#Instrucciones específicas para Master Boot Record (MBR)](#Instrucciones_espec.C3.ADficas_para_Master_Boot_Record_.28MBR.29)

### UEFI

#### Errores comunes de instalación

*   Si tiene un problema cuando se ejecuta grub-install con sysfs o procfs y le avisa que debe ejecutar `modprobe efivars`, pruebe [Unified Extensible Firmware Interface (Español)#Variables de UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Variables_de_UEFI "Unified Extensible Firmware Interface (Español)").
*   Sin las opciones `--target` o `--directory`, no se puede determinar en qué firmware se instalará. En tales casos, `grub-install` advertirá que `source_dir does not exist. Please specify --target or --directory`.
*   Si después de ejecutar grub-install le dice que la partición no se ve como una partición EFI, entonces es muy probable que la partición no esté formateada con `Fat32`.

#### Salta la shell de recate

Si GRUB carga, pero le deja en la consola de rescate sin errores, puede ser debido a que falte o esté fuera de lugar el archivo `grub.cfg`. Esto sucederá si GRUB UEFI se instaló con `--boot-directory` y `grub.cfg` no se encuentra o si el número de la partición donde reside la partición de arranque ha cambiado (que está codificada en el archivo `grubx64.efi`).

#### GRUB UEFI no se carga

He aquí un ejemplo de EFI funcional:

 `# efibootmgr -v` 
```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\efi\grub\grub.efi)
Boot0001* Shell	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EfiShell.efi)
Boot0002* Festplatte	BIOS(2,0,00)P0: SAMSUNG HD204UI

```

Si la pantalla deviene en negro durante unos segundos y GRUB pasa a la siguiente opción del arranque, como se describe [en este post](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), mover GRUB a la partición raíz podría ayudar. La opción de arranque debería ser eliminada y regenerada después de la operación. El campo relativo a grub debería ahora ser similar a esto:

```
 Boot0000* Grub HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

### Invalid signature

Si recibe el error *«invalid signature»* al intentar iniciar Windows, por ejemplo, si se ha alterado la tabla de particiones después de agregar otras particiones o discos duros, trate de eliminar la configuración de GRUB sobre los dispositivos y deje que la regenere él mismo:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig` debería ahora mostrar todas las opciones de arranque, incluyendo Windows. Si el problema está resuelto, elimine `/boot/grub/device.map-old`.

### Bloqueos al arrancar

Si el arranque se bloquea sin ningún mensaje de error, después de que GRUB cargue el kérnel y el ramdisk inicial, pruebe eliminando `add_efi_memmap` de los parámetros del kérnel.

### Arch no es detectado por otros sistemas operativos

Algunos usuarios han informado que otras distribuciones tienen problemas para encontrar Arch Linux automáticamente con `os-prober`. Si surge este problema, es posible mejorar la detección con la creación del archivo `/etc/lsb-release`. Este archivo y las herramientas de actualización están disponibles con el paquete [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

### Advertencias cuando se instala en entorno chroot

Durante la instalación de GRUB en un sistema LVM dentro de un entorno chroot (por ejemplo, durante la instalación del sistema), puede recibir advertencias como `/run/lvm/lvmetad.socket: connect failed: No such file or directory` o `WARNING: failed to connect to lvmetad: No such file or directory. Falling back to internal scanning.` Esto se debe a que `/run` no está disponible dentro del entorno chroot. Estas advertencias no impedirán que el sistema arranque, siempre que todo se haya hecho correctamente, por lo que puede continuar con la instalación.

### GRUB carga lentamente

GRUB puede tardar mucho tiempo en cargarse cuando el espacio en disco es pequeño. Compruebe si tiene suficiente espacio libre en el disco en su partición `/boot` o `/` cuando está teniendo problemas.

### error: unknown filesystem

GRUB puede mostrar la salida `error: unknown filesystem` y negarse a arrancar por varias razones. Si está seguro de que todas las [UUID](/index.php/UUID "UUID") son correctas y todos los sistemas de archivos son válidos y soportados, puede ser debido a que su [BIOS Boot Partition](#GUID_Partition_Table_.28GPT.29_specific_instructions) se encuentra fuera de los primeros 2TB de su unidad [[3]](https://bbs.archlinux.org/viewtopic.php?id=195948). Utilice una herramienta de particionado de su elección para asegurarse de que esta partición se encuentra totalmente dentro de los primeros 2TB, y luego reinstale y reconfigure GRUB.

### grub-reboot no reinicia

GRUB parece incapaz de escribir a particiones root en BTRFS [[4]](https://bbs.archlinux.org/viewtopic.php?id=166131). Si usa grub-reboot para reiniciar en otra entrada no podra actualizar su entorno en-disco. Por lo tanto ejecute grub-reboot desde la otra entrada (por ejemplo, al cambiar entre varias distribuciones) o considere un sistema de archivos distinto. Es posible resetear una entrada "pegajosa" ejecutando `grub-editenv create` y estableciendo `GRUB_DEFAULT=0` en su `/etc/default/grub` (recuerde ejecutar `grub-mkconfig -o /boot/grub/grub.cfg`).

## Véase también

*   Manual oficial de GRUB - [http://www.gnu.org/software/grub/manual/grub.html](http://www.gnu.org/software/grub/manual/grub.html)
*   Página wiki de Ubuntu sobre GRUB - [https://help.ubuntu.com/community/Grub](https://help.ubuntu.com/community/Grub)
*   Página wiki de GRUB donde explica cómo compilarlo para sistemas UEFI - [http://help.ubuntu.com/community/UEFIBooting](http://help.ubuntu.com/community/UEFIBooting)
*   Página de Wikipedia sobre la [partición de inicio de la BIOS.](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html) - descripción bastante completa de cómo configurar GRUB.