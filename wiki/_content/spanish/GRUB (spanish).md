**Estado de la traducción**
Este artículo es una traducción de [GRUB](/index.php/GRUB "GRUB"), revisada por última vez el **2018-08-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GRUB&diff=0&oldid=534863) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)")
*   [Master Boot Record (Español)](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)")
*   [GUID Partition Table (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")
*   [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")
*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")
*   [GRUB/EFI examples](/index.php/GRUB/EFI_examples "GRUB/EFI examples")
*   [GRUB/Tips and tricks (Español)](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol) "GRUB/Tips and tricks (Español)")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

[GRUB](https://www.gnu.org/software/grub/) (GRand Unified Bootloader) es un [gestor multiarranque](/index.php/Category:Boot_loaders_(Espa%C3%B1ol) "Category:Boot loaders (Español)"). Procede de [PUPA](http://www.nongnu.org/pupa/), el cual fue un proyecto de investigación desarrollado para reemplazar lo que hoy se conoce como [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"). Este último resultó demasiado difícil de mantener y GRUB se reescribió desde cero con el objetivo de proporcionarle modularidad y portabilidad [[1]](https://www.gnu.org/software/grub/grub-faq.html#q1). Al GRUB actual también se le conoce como GRUB 2, mientras que GRUB Legacy corresponde a las versiones 0.9x.

**Nota:** En el presente artículo, la expresión `*esp*` indica el punto de montaje de la [partición EFI del sistema (*«EFI system partition»*)](/index.php/EFI_system_partition "EFI system partition") conocida por sus siglas en ingles «**ESP**».

## Contents

*   [1 Sistemas BIOS](#Sistemas_BIOS)
    *   [1.1 Instrucciones específicas para GUID Partition Table (GPT)](#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29)
    *   [1.2 Instrucciones específicas para Master Boot Record (MBR)](#Instrucciones_espec.C3.ADficas_para_Master_Boot_Record_.28MBR.29)
    *   [1.3 Instalación](#Instalaci.C3.B3n)
*   [2 Sistemas UEFI](#Sistemas_UEFI)
    *   [2.1 Comprobar si se está utilizando una partición EFI del sistema](#Comprobar_si_se_est.C3.A1_utilizando_una_partici.C3.B3n_EFI_del_sistema)
    *   [2.2 Instalación](#Instalaci.C3.B3n_2)
*   [3 Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal)
*   [4 Configuración](#Configuraci.C3.B3n)
    *   [4.1 Argumentos adicionales](#Argumentos_adicionales)
    *   [4.2 LVM](#LVM)
    *   [4.3 RAID](#RAID)
    *   [4.4 Encriptación](#Encriptaci.C3.B3n)
        *   [4.4.1 Partición raíz](#Partici.C3.B3n_ra.C3.ADz)
        *   [4.4.2 Partición de arranque](#Partici.C3.B3n_de_arranque)
    *   [4.5 Entradas múltiples](#Entradas_m.C3.BAltiples)
    *   [4.6 Cargar en cadena un archivo .efi de Arch Linux](#Cargar_en_cadena_un_archivo_.efi_de_Arch_Linux)
    *   [4.7 Arranque dual](#Arranque_dual)
        *   [4.7.1 Entrada de menú para «Apagar»](#Entrada_de_men.C3.BA_para_.C2.ABApagar.C2.BB)
        *   [4.7.2 Entrada de menú para «Reiniciar»](#Entrada_de_men.C3.BA_para_.C2.ABReiniciar.C2.BB)
        *   [4.7.3 Entrada de menú para «configurar Firmware» (solo para UEFI)](#Entrada_de_men.C3.BA_para_.C2.ABconfigurar_Firmware.C2.BB_.28solo_para_UEFI.29)
        *   [4.7.4 Entrada de menú para GNU/Linux](#Entrada_de_men.C3.BA_para_GNU.2FLinux)
        *   [4.7.5 Entrada de menú para Windows instalado en modo UEFI/GPT](#Entrada_de_men.C3.BA_para_Windows_instalado_en_modo_UEFI.2FGPT)
        *   [4.7.6 Entrada de menú para Windows instalado en modo BIOS-MBR](#Entrada_de_men.C3.BA_para_Windows_instalado_en_modo_BIOS-MBR)
*   [5 Utilizar la consola de intérprete de órdenes](#Utilizar_la_consola_de_int.C3.A9rprete_de_.C3.B3rdenes)
    *   [5.1 Soporte para «pager»](#Soporte_para_.C2.ABpager.C2.BB)
    *   [5.2 Usar el entorno de la consola de intérprete de órdenes para arrancar distintos sistemas operativos](#Usar_el_entorno_de_la_consola_de_int.C3.A9rprete_de_.C3.B3rdenes_para_arrancar_distintos_sistemas_operativos)
        *   [5.2.1 Alternar el arranque desde una partition](#Alternar_el_arranque_desde_una_partition)
        *   [5.2.2 Alternar el arranque desde un disco/unidad](#Alternar_el_arranque_desde_un_disco.2Funidad)
        *   [5.2.3 Alternar el arranque de Windows/Linux instalados en modalidad UEFI](#Alternar_el_arranque_de_Windows.2FLinux_instalados_en_modalidad_UEFI)
        *   [5.2.4 Cargar en modo normal](#Cargar_en_modo_normal)
    *   [5.3 Utilizar la consola de rescate](#Utilizar_la_consola_de_rescate)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 F2FS y otros sistemas de archivos sin soporte](#F2FS_y_otros_sistemas_de_archivos_sin_soporte)
    *   [6.2 La BIOS de Intel no arranca con GPT](#La_BIOS_de_Intel_no_arranca_con_GPT)
    *   [6.3 Activar mensajes de depuración de errores](#Activar_mensajes_de_depuraci.C3.B3n_de_errores)
    *   [6.4 Corregir el error de GRUB: «no suitable mode found»](#Corregir_el_error_de_GRUB:_.C2.ABno_suitable_mode_found.C2.BB)
    *   [6.5 Mensaje de error msdos-style](#Mensaje_de_error_msdos-style)
    *   [6.6 UEFI](#UEFI)
        *   [6.6.1 Errores comunes de instalación](#Errores_comunes_de_instalaci.C3.B3n)
        *   [6.6.2 Salta la consola de emergencia](#Salta_la_consola_de_emergencia)
        *   [6.6.3 GRUB UEFI no se carga](#GRUB_UEFI_no_se_carga)
        *   [6.6.4 Ruta de arranque default/fallback](#Ruta_de_arranque_default.2Ffallback)
    *   [6.7 Invalid signature](#Invalid_signature)
    *   [6.8 Bloqueos al arrancar](#Bloqueos_al_arrancar)
    *   [6.9 Arch no es detectado por otros sistemas operativos](#Arch_no_es_detectado_por_otros_sistemas_operativos)
    *   [6.10 Advertencias cuando se instala en entorno chroot](#Advertencias_cuando_se_instala_en_entorno_chroot)
    *   [6.11 GRUB carga lentamente](#GRUB_carga_lentamente)
    *   [6.12 error: unknown filesystem](#error:_unknown_filesystem)
    *   [6.13 grub-reboot no reinicia](#grub-reboot_no_reinicia)
    *   [6.14 El sistema de archivos BTRFS antiguo presiste en la instalación](#El_sistema_de_archivos_BTRFS_antiguo_presiste_en_la_instalaci.C3.B3n)
    *   [6.15 Windows 8/10 no es encontrado](#Windows_8.2F10_no_es_encontrado)
    *   [6.16 Modalidad EFI en VirtualBox](#Modalidad_EFI_en_VirtualBox)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Sistemas BIOS

### Instrucciones específicas para GUID Partition Table (GPT)

En una configuración BIOS/[GPT](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)"), es necesaria crear una [*BIOS boot partition* (partición de arranque BIOS](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation)). GRUB incrusta su propia `core.img` en esta partición.

**Nota:**

*   Antes de intentar este método tenga en cuenta que no todos los sistemas serán capaces de soportar este esquema de particionado. Lea más sobre [GUID partition table](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)").
*   Esta partición adicional solo la necesita GRUB, en un esquema de particionado BIOS/GPT. Anteriormente, GRUB, en un esquema de particionado BIOS/MBR, usaba el espacio posterior al MBR para insertar su `core.img`. En una tabla de particionado GPT, sin embargo, no se puede garantizar que exista espacio suficiente (después del MBR y) antes de la primera partición.
*   Para sistemas [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") esta partición adicional no es necesaria, ya que en este caso no se lleva a cabo su incustración en los sectores de arranque. Sin embargo, los sistemas UEFI aún requieren una partición EFI del sistema «*[EFI system partition](/index.php/EFI_system_partition "EFI system partition")*».

Cree una partición de un mebibyte (MiB) (`+1M` con *fdisk* o *gdisk*) en el disco, sin formatearla con un sistema de archivos y con el GUID `21686148-6449-6E6F-744E-656564454649`.

*   Seleccione para dicha partición el tipo `BIOS boot` con [fdisk](/index.php/Fdisk "Fdisk"), `ef02` con [gdisk](/index.php/Gdisk "Gdisk").
*   Con [parted](/index.php/Parted "Parted") establezca/active el flag `bios_grub`.

Esta partición puede estar colocada en cualquier parte del disco, pero tiene que estar en los primeros 2 TiB. Dicha partición debe ser creada antes instalar GRUB. Cuando la partición esté lista, instale el gestor de arranque de acuerdo con las instrucciones de abajo.

El espacio previo de la primera partición también se puede usar como la partición de arranque del BIOS («*BIOS boot partition*»), aunque no se ajustará a las especificaciones de GPT sobre la alineación de la partición. Dado que no se accederá con regularidad a la partición, es posible ignorar el impacto sobre el rendimiento, aunque algunas utilidades de disco mostrarán una advertencia al respecto. Con *fdisk* o *gdisk* cree una partición nueva que se iniciará en el sector 34 y se extenderá hasta el 2047, y asígnele el tipo indicado antes. Para tener las particiones visibles al comienzo, considere la posibilidad de crear esta partición la última.

### Instrucciones específicas para Master Boot Record (MBR)

Por lo general, el espacio disponilbe después del [MBR](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") (después de los 512 bytes dedicados a ella, y antes de la primera partición), en cualquier sistema particionado con MBR (o etiquetado como 'msdos') es de 31 Kb, de modo que si hay algún problema de alineación de los cilindros se resuelven en la tabla de particiones. Sin embargo, se recomienda mantener una distancia de aproximadamente 1 a 2 MiB que proporcionará el espacio suficiente para contener la `core.img` de GRUB ([FS#24103](https://bugs.archlinux.org/task/24103)). Es recomendable utilizar una herramienta de particionado que permita la alineación de una partición de 1 MiB después del MBR, de modo que se pueda obtener el espacio necesario, y resolver otros problemas fuera de los primeros 512 bytes (que son ajenos a la incrustación de `core.img`).

### Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [grub](https://www.archlinux.org/packages/?name=grub). Este reemplazará a [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/), si está instalado. Después ejecute:

```
# grub-install --target=i386-pc /dev/sd**X**

```

donde `/dev/sd**X**` es el disco donde se instalará grub (por ejemplo, el disco `/dev/sda` y **no** la partición `/dev/sda1`).

Ahora genere [el archivo principal de configuración](#Generar_el_archivo_de_configuraci.C3.B3n_principal).

Si usa [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") para `/boot`, puede instalar GRUB en varios discos físicos.

**Sugerencia:** Consulte [GRUB/Tips and tricks (Español)#Métodos alternativos de instalación](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#M.C3.A9todos_alternativos_de_instalaci.C3.B3n "GRUB/Tips and tricks (Español)") para conocer otras formas de instalar GRUB, como en una memoria USB.

Consulte [grub-install(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grub-install.8) y el [Manual de GRUB](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation) para obtener más detalles sobre la orden *grub-install*.

## Sistemas UEFI

**Nota:**

*   Es recomendable consultar las páginas [UEFI (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), [GPT (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)") y [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)") antes de seguir esta parte.
*   Si desea realizar la instalación con UEFI, es importante arrancar el ordenador en la modalidad UEFI al cargar la imagen de instalación. El soporte de instalación de Arch Linux dispone de UEFI con capacidad de arranque.

### Comprobar si se está utilizando una partición EFI del sistema

Para arrancar desde un disco usando UEFI, la tabla de particiones de disco recomendada es GPT y este es el esquema que se asume en este artículo. Se requiere una [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) en cada disco de arranque. Si está instalando Arch Linux en un equipo con capacidad UEFI con un sistema operativo instalado, como Windows 10, por ejemplo, es muy probable que ya tenga un ESP.

Para averiguar el esquema de partición del disco y la partición del sistema, utilice `parted` como superusuario (root) sobre el disco desde el que desea iniciar:

```
# parted /dev/sd*x* print

```

La orden le devolverá:

*   El esquema de la partición del disco: si el disco es GPT, indica `Partition Table: gpt`.
*   La lista de particiones del disco: busque la partición del sistema EFI en la lista, es una partición pequeña (generalmente de aproximadamente 100-550 MiB) con un sistema de archivos `fat32` y con el flag `esp` activado. Para confirmar que se trata de ESP, móntela y verifique si contiene un directorio llamado `EFI`, y si es así, definitivamente es la ESP.

Una vez encontrada, **tome nota del número de la partición**, lo necesitará para la [instalación de GRUB](#Instalaci.C3.B3n_2). Si no tiene una ESP, tendrá que crear una. Vea el artículo de [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

### Instalación

**Nota:**

*   Es bien sabido que los fabricantes de placas base no implementan los firmware de UEFI de modo homogéneo. Los ejemplos de instalación descritos a continuación están destinados a trabajar en la más amplia gama de sistemas UEFI posibles. Se anima a los usuarios que experimenten problemas, a pesar de la aplicación de los métodos descritos, a compartir información detallada de sus casos específicos de hardware, cuando hayan encontrado solución a sus problemas. Para estos casos especiales se ha proporcionado un página de [ejemplos para GRUB EFI](/index.php/GRUB_EFI_Examples "GRUB EFI Examples").
*   Esta sección asume que está instalando GRUB para sistemas x86_64 (x86_64-efi). Para sistemas EFI IA32 (32-bit) (no confundir con CPU de 32-bit), sustituya `x86_64-efi` con `i386-efi` donde proceda.

Primero, [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") los paquetes [grub](https://www.archlinux.org/packages/?name=grub) y [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr): *GRUB* es el gestor de arranque, mientras que *efibootmgr* es utilizado por el script de instalación de GRUB para escribir entradas de arranque a NVRAM.

A continuación, siga los siguientes pasos para instalar GRUB:

1.  [Monte la partición del sistema EFI](/index.php/EFI_system_partition#Mount_the_partition "EFI system partition") y en el resto de esta sección, sustituya `*esp* `por su punto de montaje.
2.  Elija un identificador para el gestor de arranque, que aquí llamaremos `***GRUB***`. Se creará un directorio con ese nombre para almacenar el binario de EFI en la ESP y este es el nombre que aparecerá en el menú de arranque de UEFI para identificar la entrada de arranque de GRUB.
3.  Ejecute la siguiente orden para instalar la aplicación `grubx64.efi` de GRUB EFI en `*esp*/EFI/***GRUB***/` e instale sus módulos en `/boot/grub/x86_64-efi/`.

```
# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=***GRUB***

```

Después de completar la instalación anterior, el directorio principal de GRUB se encuentrará en `/boot/grub/`.Tenga en cuenta que `grub-install` también intenta [crear una entrada en el gestor de arranque del firmware](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Crear_una_entrada_GRUB_en_el_gestor_de_arranque_del_firmware "GRUB/Tips and tricks (Español)"), llamado `***GRUB***` siguiendo el ejemplo anterior.

Recuerde [Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal) al terminar la [configuración](#Configuraci.C3.B3n).

**Sugerencia:** Si usa la opción `--removable`, GRUB se instalará en `*esp*/EFI/BOOT/BOOTX64.EFI` (o `*esp*/EFI/BOOT/BOOTIA32.EFI` para la arquitectura `i386-efi`) y tendrá la capacidad adicional de poder arrancar desde la unidad, en caso de que las variables EFI se reseteen o se mueva la unidad a otro equipo. Por lo general, puede hacer esto seleccionando la unidad en sí de manera similar a como lo haría con la BIOS. Si tiene un arranque dual con Windows, tenga en cuenta que Windows generalmente tiene una carpeta `BOOT` dentro de la carpeta `EFI` en la partición del sistema EFI, pero su único propósito es recrear la entrada de arranque UEFI para Windows.

**Nota:**

*   `--efi-directory` y `--bootloader-id` son opciones específicas de GRUB UEFI, `--efi-directory` reemplaza a `--root- directorio` que está en desuso.
*   Puede notar la ausencia de una opción *ruta_al_dispositivo* (por ejemplo, a `/dev/sda`) en la orden `grub-install`. De hecho, cualquier *ruta_al_dispositivo* proporcionada será ignorada por el script de instalación GRUB UEFI. Es más, los cargadores de arranque UEFI no usan un código de arranque MBR o sector de arranque de partición en absoluto.

Consulte la sección sobre [solución de problemas de UEFI](#UEFI) si tiene problemas. Vea también [GRUB/Tips and tricks (Español)#Lecturas adicionales de UEFI](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Lecturas_adicionales_de_UEFI "GRUB/Tips and tricks (Español)").

## Generar el archivo de configuración principal

Después de instalar GRUB, se debe crear el archivo de configuración principal `grub.cfg`. El proceso de generación puede verse influido por una variedad de opciones presentes en `/etc/default/grub` y de scripts presentes en `/etc/grub.d/`; Consulte [#Configuración](#Configuraci.C3.B3n).

Si no se ha hecho una configuración adicional, la generación automática determinará el sistema de archivos raíz del sistema que el archivo de configuración arrancará. Para que esto tenga éxito, es importante que el sistema o bien sea arrancable o bien se haga dentro de chroot.

**Nota:** Recuerde que `grub.cfg` tiene que ser regenerado cada vez que se haga cualquier cambio en el archivo `/etc/default/grub` o en los archivos presentes en `/etc/grub.d/`.

UTilice la herramienta *grub-mkconfig* para generar `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Por defecto, los scripts de generación añaden automáticamente las entradas de menú para Arch Linux a cualquier configuración generada. Consulte [Multiboot USB drive#Boot entries](/index.php/Multiboot_USB_drive#Boot_entries "Multiboot USB drive") y [#Arranque dual](#Arranque_dual) para entradas de menú personalizadas para otros sistemas.

**Sugerencia:** Para que *grub-mkconfig* busque otros sistemas instalados y los añada automáticamente al menú, [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [os-prober](https://www.archlinux.org/packages/?name=os-prober) y [monte](/index.php/Mount "Mount") las particiones que contienen otros sistemas.

**Nota:**

*   La ruta predeterminada del archivo es `/boot/grub/grub.cfg`, no `/boot/grub/i386-pc/grub.cfg`. El paquete [grub](https://www.archlinux.org/packages/?name=grub) incluye una muestra `/boot/grub/grub.cfg`; asegúrese de que los cambios intencionados estén escritos en este archivo.
*   Si está intentando ejecutar *grub-mkconfig* en un entorno chroot o un contenedor *systemd-nspawn*, podrá advertir que no funciona, avisándole de que *grub-probe* no puede obtener «canonical path of /dev/sdaX». En este caso, pruebe usando *arch-chroot* como se describe en la [publicación BBS](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067).

## Configuración

Esta sección cubre solo la edición del archivo de configuración `/etc/default/grub`. Consulte [GRUB/Tips and tricks (Español)](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol) "GRUB/Tips and tricks (Español)") si necesita más opciones.

Recuerde siempre [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal) después de realizar cambios en `/etc/default/grub`.

### Argumentos adicionales

Para pasar argumentos adicionales personalizados a la imagen de Linux, se pueden ajustar las variables `GRUB_CMDLINE_LINUX` + `GRUB_CMDLINE_LINUX_DEFAULT` en `/etc/default/grub`. Los dos parámetros se anexan al archivo y se pasan al kérnel al generar las entradas de arranque regulares. Para la *recuperación* del sistema, basta con usar la variable `GRUB_CMDLINE_LINUX`.

No es necesario el uso de ambos, pero puede ser útil. Por ejemplo , podría utilizar `GRUB_CMDLINE_LINUX_DEFAULT="resume=/dev/sdaX quiet"` cuando `sda**X**` es la partición de intercambio (swap) para activar la reanudación del sistema tras la hibernación. Esto generaría una entrada de arranque de reanudación y con el parámetro *quiet* no mostraría los mensajes del kérnel durante el arranque desde esa entrada. Sin embargo, las otras entradas del menú (regulares) seguirían teniendo las opciones normales.

Por defecto, *grub-mkconfig* determina el [UUID](/index.php/UUID "UUID") del sistema de archivos raíz para la configuración. Para desactivar esto, descomente `GRUB_DISABLE_LINUX_UUID=true`.

Para generar la entrada de recuperación en GRUB hay que comentar `#GRUB_DISABLE_RECOVERY=true` en `/etc/default/grub`.

También se puede usar `GRUB_CMDLINE_LINUX="resume=UUID=*uuid-of-swap-partition*"`

Consulte [Kernel parameters (Español)](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para obtener más información.

### LVM

Si utiliza [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") para `/boot` o para la partición raíz `/` , asegúrese de que el módulo `lvm` se carga antes:

 `/etc/default/grub`  `GRUB_PRELOAD_MODULES="... lvm"` 

### RAID

GRUB permite tratar los volúmenes en una configuración [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)") de una manera sencilla. Necesita cargar los módulos de GRUB `mdraid09` o `mdraid1x` para poder abordar el volumen de forma nativa:

 `/etc/default/grub`  `GRUB_PRELOAD_MODULES="... mdraid09 mdraid1x"` 

Por ejemplo, `/dev/md0` se convierte en:

```
set root=(md/0)

```

mientras que un volumen de RAID particionado (por ejemplo, `/dev/md0p1`) se convierte en:

```
set root=(md/0,1)

```

Para instalar grub al usar RAID1 en la partición `/boot` (o utulizando `/boot` alojado en una partición raíz RAID1), en sistemas BIOS, simplemente ejecute *grub-install* en ambas unidades, así:

```
# grub-install --target=i386-pc --debug /dev/sda
# grub-install --target=i386-pc --debug /dev/sdb

```

Donde el alojamiento de la matriz RAID 1 `/boot` está ubicado en `/dev/sda` y `/dev/sdb`.

**Nota:** GRUB admite el inicio desde [Btrfs](/index.php/Btrfs "Btrfs") con RAID 0/1/10, pero *no* con RAID 5/6\. Puede usar [mdadm](/index.php/Mdadm "Mdadm") para RAID 5/6, que admite GRUB.

### Encriptación

#### Partición raíz

Para cifrar un sistema de archivos raíz que arranque con GRUB, agregue el hook `encrypt`, o `sd-encrypt` (si usa los hooks de systemd), a [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"). Consulte [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para obtener más información, y [Mkinitcpio (Español)#Hooks más comunes](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Hooks_m.C3.A1s_comunes "Mkinitcpio (Español)") para los hooks de cifrado alternativos.

Si usa el hook `encrypt`, añada el parámetro `cryptdevice` a `/etc/default/grub`.

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="cryptdevice=UUID=*UUID_del_DISPOSITIVO*:cryptroot"` 

Si usa el hook `sd-encrypt`, adañada `rd.luks.name`:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="rd.luks.name=*UUID_del_DISPOSITIVO*=cryptroot"` 

donde *UUID_del_DISPOSITIVO* es el UUID del dispositivo cifrado con LUKS.

Asegúrese de [volver a generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal) cuando haya terminado.

Para obtener más información acerca de la configuración del gestor de arranque para dispositivos cifrados, consulte [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

**Nota:** Si desea cifrar `/boot` bien como una partición separada o como parte de la partición raíz `/`, se requiere una configuración adicional. Consulte [#Partición de arranque](#Partici.C3.B3n_de_arranque).

**Sugerencia:** Si está actualizando desde una configuración de GRUB Legacy en funcionamiento, compruebe `/boot/grub/menu.lst.pacsave` para agregar el dispositivo/etiqueta correcto. Localícelo después del texto `kernel /vmlinuz-linux`.

#### Partición de arranque

GRUB puede configurarse para solicitar una contraseña para abrir un dispositivo de bloque [LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)") a fin de leer su configuración y cargar cualquier [initramfs](/index.php/Initramfs "Initramfs") y [kernel](/index.php/Kernel "Kernel") desde él. Esta opción intenta resolver el problema de tener una [partición de arranque sin cifrar](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"). `/boot` **no** necesita estar en una partición separada; puede estar en el mismo árbol de directorios del sistema raíz `/`.

**Advertencia:** GRUB no admite encabezados LUKS2\. Asegúrese de no especificar `luks2` en la línea de parámetros al crear la partición cifrada usando la orden `cryptsetup luksFormat`.

Para activar esta función, encripte la partición en la que resida `/boot` utilizando [LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)") de forma normal. A continuación, agregue la siguiente opción a `/etc/default/grub`:

 `/etc/default/grub`  `GRUB_ENABLE_CRYPTODISK=y` 

Asegúrese de [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuraci.C3.B3n_principal) cuando la partición que contiene `/boot` esté montada

Sin más cambios, se le solicitará dos veces una contraseña: la primera para GRUB para desbloquear el punto de montaje `/boot` en el arranque temprano, y la segunda para desbloquear el sistema de archivos raíz como se describe en [#Partición raíz](#Partici.C3.B3n_ra.C3.ADz). Puede utilizar un [keyfile](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") para evitar esta doble contraseña.

**Nota:**

*   Si utiliza una distribución de teclado distinta de la predeterminada (US), una instalación predeterminada de GRUB no lo sabrá. Esto es relevante para saber cómo introducir la contraseña para desbloquear el dispositivo de bloque cifrado con LUKS.
*   Para realizar actualizaciones del sistema que afecten el punto de montaje `/boot`, asegúrese de que `/boot` cifrado esté desbloqueado y montado antes de realizar una actualización. Con una partición `/boot` separada, esto puede lograrse automáticamente al arrancar usando [crypttab](/index.php/Crypttab "Crypttab") con un [archivo de claves](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption").
*   Si tiene problemas para que la solicitud de una contraseña se muestre en la pantalla (errores relacionados con cryptouuid, cryptodisk o «device not found»), pruebe volviendo a instalar grub como se indica a continuación, agregando lo siguiente al final de la orden de instalación:

 `# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=grub **--modules="part_gpt part_msdos"**` 

### Entradas múltiples

Para obtener sugerencias sobre la administración de varias entradas de GRUB, por ejemplo, al usar tanto kernel [linux](https://www.archlinux.org/packages/?name=linux) como [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernels, consulte [GRUB/Tips and tricks (Español)#Múltiples entradas](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#M.C3.BAltiples_entradas "GRUB/Tips and tricks (Español)").

### Cargar en cadena un archivo .efi de Arch Linux

Si tiene un archivo *.efi* generado a partir de [Secure Boot](/index.php/Secure_Boot "Secure Boot") u otros medios, se puede editar `/etc/grub.d/40_custom` para agregar una nueva entrada de menú antes de regenerar `grub.cfg` con `grub-mkconfig`.

 `/etc/grub.d/40_custom` 
```
menuentry 'Arch Linux .efi' {
insmod part_gpt
insmod chain
set root='(hdX,gptY)'
chainloader /EFI/*path*/*file*.efi
}
```

### Arranque dual

La mejor forma de agregar otras entradas es editando `/etc/grub.d/40_custom` o `/boot/grub/custom.cfg`. Las entradas en este archivo se agregarán automáticamente después de volver a ejecutar `grub-mkconfig`.

#### Entrada de menú para «Apagar»

```
menuentry "System shutdown" {
	echo "System shutting down..."
	halt
}

```

#### Entrada de menú para «Reiniciar»

```
menuentry "System restart" {
	echo "System rebooting..."
	reboot
}

```

#### Entrada de menú para «configurar Firmware» (solo para UEFI)

```
menuentry "Firmware setup" {
	fwsetup
}

```

#### Entrada de menú para GNU/Linux

Suponiendo que la otra distribución está en la partición`sda2`:

```
menuentry "Otro Linux" {
	set root=(hd0,2)
	linux /boot/vmlinuz (añada aquí otras opciones necesarias)
	initrd /boot/initrd.img (si el otro kernel utiliza/necesita uno)
}
```

Alternativamente, deje que GRUB busque la partición correcta por *UUID* o *label*:

```
menuentry "Otro Linux" {
        # suponiendo que UUID es 763A-9CB6
	search --set=root --fs-uuid 763A-9CB6

        # búsqueda por etiqueta OTRO_LINUX (asegúrese de que la etiqueta de la partición no sea ambigua)
        #search --set=root --label OTHER_LINUX

	linux /boot/vmlinuz (añada otras opciones aquí si es necesario, por ejemplo: root=UUID=763A-9CB6)
	initrd /boot/initrd.img (si el otro kernel utiliza/necesita uno)
}
```

#### Entrada de menú para Windows instalado en modo UEFI/GPT

Este modo determina dónde reside el gestor de arranque de Windows y permite alternar su carga después de Grub cuando se selecciona su entrada en el menú. La principal tarea aquí es encontrar la partición EFI y ejecutar el gestor de arranque desde allí.

**Nota:** Este «menuentry» solo funcionará en modo de arranque UEFI y solo si el bit de Windows coincide con el bit de UEFI. No funcionará en sistemas BIOS con GRUB instalado. Consulte [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") y [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows") para obtener más información.

```
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1 UEFI/GPT" {
		insmod part_gpt
		insmod fat
		insmod search_fs_uuid
		insmod chain
		search --fs-uuid --set=root $hints_string $fs_uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi
```

donde `$hints_string` y `$fs_uuid` se obtienen con las dos siguientes órdenes.

La orden `$fs_uuid` determinará el UUID de la partición EFI:

 `# grub-probe --target=fs_uuid *esp*/EFI/Microsoft/Boot/bootmgfw.efi`  `1ce5-7f28` 

De otra forma, se puede ejecutar `blkid` (como root) y leer el UUID de la partición del sistema EFI desde allí.

La orden `$hints_string` determinará la ubicación de la partición del sistema EFI, en este caso, el disco duro es 0:

 `# grub-probe --target=hints_string *esp*/EFI/Microsoft/Boot/bootmgfw.efi`  `--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1` 

Estas dos órdenes suponen que el uso de la ESP de Windows está montada en `*esp*`. Puede haber diferencias entre mayúsculas y minúsculas en la ruta al archivo EFI de Windows, what with being Windows, and all.

#### Entrada de menú para Windows instalado en modo BIOS-MBR

**Nota:** GRUB admite el arranque de `bootmgr` directamente y ya no es necesario [alternar la carga](https://www.gnu.org/software/grub/manual/grub.html#Chain_002dloading) del sector de arranque de la partición para iniciar Windows en una configuración de BIOS/MBR.

**Advertencia:** Esta es la **system partition** que contiene `/bootmgr`, no la partición de Windows «real» (generalmente C:). En la salida de `blkid`, la partición del sistema es la que tiene `LABEL="SYSTEM RESERVED"` o `LABEL="SYSTEM"` y solo tiene entre 100 y 200 MB de tamaño (muy parecido a la partición de arranque para Arch). Consulte [Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") para más información.

A lo largo de esta sección, presumiremos que la partición de Windows es `/dev/sda1`. Una partición diferente cambiará cada instancia de hd0, msdos1\. Agregue el código correspondiente a `/etc/grub.d/40_custom` o a `/boot/grub/custom.cfg` y regenere `grub.cfg` con `grub-mkconfig`, como se explicó anteriormente, para arrancar Windows (XP, Vista, 7, 8 o 10) instalado en la modalidad BIOS/MBR:

**Nota:** Estas entradas del menú funcionarán solo en la modalidad de arranque de sistemas BIOS. No funcionará en UEFI con GRUB instalado. Consulte [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") y [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows") .

En ambos ejemplos `*XXXXXXXXXXXXXXXX*` es el UUID del sistema de archivos, que se puede encontrar con la orden `lsblk --fs`.

Para Windows Vista/7/8/8.1/10:

```
if [ "${grub_platform}" == "pc" ]; then
  menuentry "Microsoft Windows Vista/7/8/8.1/10 BIOS/MBR" {
    insmod part_msdos
    insmod ntfs
    insmod search_fs_uuid
    insmod ntldr     
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 *XXXXXXXXXXXXXXXX*
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
    search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 *XXXXXXXXXXXXXXXX*
    ntldr /ntldr
  }
fi

```

**Nota:** En algunos casos, GRUB puede instalarse sin un Windows 8 limpio, en cuyo caso no puede iniciar Windows sin tener un error con `\boot\bcd` (código de error `0xc000000f`). Puede solucionarlo acudiendo a la consola de recuperación de Windows -Windows Recovery Console- (`cmd.exe` desde el disco de instalación) y ejecutando:
```
X:\> bootrec.exe /fixboot
X:\> bootrec.exe /RebuildBcd

```

«No» utilice `bootrec.exe /Fixmbr` porque borrará GRUB. O puede usar la función de Reparación de Arranque («Boot Repair») en el menú Solución de Problemas -no eliminará GRUB sino que arreglará la mayoría de los errores-. Además, será mejor que permanezca **TAN SOLO** conectado al disco duro de destinoy al dispositivo de arranque. Windows normalmente no puede reparar la información de arranque si hay otros dispositivos conectados.

`/etc/grub.d/40_custom` puede ser usado como plantilla para crear `/etc/grub.d/*nn*_custom`. Donde `*nn*` define el orden de prelación, indicando el orden en que se ejecuta el script. El orden de ejecución de los scripts determinan su ubicación en el menú de inicio de grub.

**Nota:** `nn` debe ser mayor a 06 para garantizar que los scripts necesarios se ejecuten primero.

## Utilizar la consola de intérprete de órdenes

Como el MBR es demasiado pequeño para almacenar todos los módulos de GRUB, solo el menú y algunas órdenes básicas residen allí. La mayoría de la funcionalidad de GRUB está contenida en los módulos ubicados en `/boot/grub`, que se cargarán cuando sean necesarios. En condiciones de error (por ejemplo, si el diseño de la partición cambia), GRUB puede no iniciarse. Cuando esto sucede, puede lanzar una consola.

GRUB ofrece múltiples shells/prompts. Si hay un problema al leer el menú, pero el gestor de arranque puede encontrar el disco, es probable que se le presente la consola «normal»:

```
grub>

```

Si hay un problema más grave (por ejemplo, GRUB no puede encontrar los archivos requeridos), en su lugar puede presentar la consola de «rescate»:

```
grub rescue>

```

La consola de rescate es una versión reducida de la normal, y ofrece, por lo tanto, un número reducido de funcionalidades. Si se presenta la consola de rescate, primero trate de cargar el módulo «normal» y, a continuación, inicie la consola clásica:

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/i386-pc/normal.mod
rescue:grub> normal

```

### Soporte para «pager»

GRUB es compatible con «*pager*» (paginador o localizador) que permite la lectura de las órdenes que proporcionan «salidas» extensas (como la orden `help`). Tenga en cuenta que esta característica solo está disponible en la consola normal y no en la de rescate. Para activar pager, escriba en la consola de órdenes de GRUB:

```
sh:grub> set pager=1

```

### Usar el entorno de la consola de intérprete de órdenes para arrancar distintos sistemas operativos

```
grub>

```

El entorno de la consola de GRUB se puede usar para arrancar sistemas operativos. Un escenario común puede ser iniciar Windows/Linux almacenado en una unidad/partición a través de **carga alternativa**.

La *carga alternativa* («*Chainloading*») significa poder cargar otro cargador de arranque desde el que está corriendo, es decir, cargar en cadena.

El otro gestor de arranque puede estar incrustado al inicio del disco (MBR) o al comienzo de una partición o como un binario EFI en la ESP en el caso de UEFI.

#### Alternar el arranque desde una partition

```
set root=(hdX,Y)
chainloader +1
boot

```

X=0,1,2... Y=1,2,3...

Por ejemplo, cargar alternativamente Windows almacenado en la primera partición del primer disco duro,

```
set root=(hd0,1)
chainloader +1
boot

```

Del mismo modo, se puede alternar la carga de GRUB instalado en una partición.

#### Alternar el arranque desde un disco/unidad

```
set root=hdX
chainloader +1
boot

```

#### Alternar el arranque de Windows/Linux instalados en modalidad UEFI

```
insmod ntfs
set root=(hd0,gpt4)
chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
boot

```

`insmod ntfs` se usa para cargar el módulo de sistema de archivos ntfs para Windows. (hd0,gpt4) o /dev/sda4 es la partición de mi sistema EFI (ESP). La entrada en la línea *chainloader* especifica la ruta del archivo *.efi* cuya carga se alternará.

#### Cargar en modo normal

Consulte el ejemplo en [#Utilizar la consola de rescate](#Utilizar_la_consola_de_rescate)

### Utilizar la consola de rescate

Consulte primero [#Utilizar la consola de rescate](#Utilizar_la_consola_de_rescate) más arriba. Si no es capaz de iniciar la shell estándar, una posible solución es arrancar un liv eCD o alguna otra distribución a modo de recuperación para corregir los errores de configuración y reinstalar GRUB. Sin embargo, un disco de recuperación no siempre es posible (ni necesario), y la consola de emergencia es sorprendentemente robusta.

Las órdenes disponibles en esta modalidad incluyen `insmod`, `ls`, `set` y `unset`. Este ejemplo utiliza `set` y `insmod`. `set` cambia el valor de las variables, mientras que `insmod` añade nuevos módulos para ampliar la funcionalidad básica.

Antes de comenzar, es necesario que conozca la ubicación de `/boot` (ya esté en una partición separada o en un directorio dentro de la partición raíz):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

donde X es el número de la unidad y la Y de la partición.

**Nota:** Si está usando una partición de arranque separada, se omite `/boot` en la ruta. (por ejemplo, `set prefix=(hdX,Y)/grub`).

Para ampliar las capacidades de la consola, inserte el módulo `linux`:

```
grub rescue> insmod i386-pc/linux.mod

```

o simplemente:

```
grub rescue> insmod linux

```

Esto proporciona órdenes de `linux` y `initrd`, con las que debe estar familiarizado.

Un ejemplo de inicio de Arch Linux:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot

```

De nuevo, en el caso de partición de arranque separada (por ejemplo, usando UEFI), cambie las órdenes en consecuencia:

**Nota:** Cuando el arranque es desde una partición separada y no parte de la partición raíz, debe direccionar a la partición de arranque manualmente, indicando la variable correspondiente.

```
set root=(hd0,5)
linux (hdX,Y)/vmlinuz-linux root=/dev/sda6
initrd (hdX,Y)/initramfs-linux.img
boot

```

**Nota:** Si se experimentó el mensaje `error: premature end of file /EL_NOMBRE_DEL_KERNEL` durante la ejecución de la orden `linux`, pruebe usuando `linux16` en su lugar.

Tras el lanzamiento con éxito de una instalación de Arch Linux, los usuarios pueden corregir `grub.cfg` si fuese necesario y proceder a reinstalar GRUB.

Para reinstalar GRUB y arreglar completamente el problema, cambie `/dev/sda` de acuerdo a sus propias necesidades. Consulte el apartado sobre [#Instalación](#Instalaci.C3.B3n) para más detalles.

## Solución de problemas

### F2FS y otros sistemas de archivos sin soporte

GRUB no es compatible con el sistema de archivos [F2FS](/index.php/F2FS "F2FS"). En caso de que la partición raíz corra sobre un sistema de archivos no compatible, se debe crear una partición `/boot` alternativa formateada con un sistema de archivos compatible. En algunos casos, la versión de desarrollo de GRUB, [grub-git](https://aur.archlinux.org/packages/grub-git/), puede tener soporte nativo para el sistema de archivos.

### La BIOS de Intel no arranca con GPT

Algunas BIOS de Intel requieren, al menos, una partición MBR marcada como booteable en el arranque, cosa no habitual en las configuraciones basadas en GPT, que provocan que la partición GPT no se inicie.

Es posible solucionar el problema mediante el uso de (por ejemplo) fdisk para marcar como «bootable» en el MBR una de las particiones GPT (preferiblemente la partición de 1007 KiB que ya se ha creado para GRUB). Esto se puede lograr, utilizando fdisk, mediante las siguientes órdenes: inicie fdisk sobre el disco donde va a realizar la instalación, por ejemplo `fdisk /dev/sda`, presione `a` y seleccione la partición que desea marcar como booteable (seguramente #1) pulsando el número correspondiente, para terminar pulse `w` para escribir los cambios en el MBR.

**Nota:** La marca de «bootable» puede hacerse en `fdisk` o similar, no con GParted u otros, ya que no configurarán el marcador de inicio en el MBR.

Con cfdisk, los pasos son similares, bastando con `cfdisk/dev/sda`, elija el dispositivo de arranque (a la izquierda) en el disco duro deseado y salga guardando.

Con la versión más reciente de parted, puede usar la opción `disk_toggle pmbr_boot`. Luego verifique que los indicadores del disco muestren pmbr_boot.

```
# parted /dev/sd*x* disk_toggle pmbr_boot
# parted /dev/sd*x* print

```

Para más información consulte [esto](http://www.rodsbooks.com/gdisk/bios.html)

### Activar mensajes de depuración de errores

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

Ahora, copie `/usr/share/grub/unicode.pf2` en `${GRUB2_PREFIX_DIR}` (`/boot/grub` de los sistema BIOS y UEFI). Si GRUB UEFI se instala con la opción `--boot-directory` activada, entonces la ruta sería `*esp*/EFI/grub/`:

```
# cp /usr/share/grub/unicode.pf2 ${GRUB_PREFIX_DIR}

```

Si el archivo `/usr/share/grub/unicode.pf2` no existe, instale el paquete [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) y proceda a la creación y copia del mismo en `${GRUB2_PREFIX_DIR}`.

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

En el archivo `grub.cfg`, agregue las líneas siguientes para permitir a GRUB que pase correctamente la modalidad de vídeo al kérnel, de lo contrario obtendrá una pantalla en negro (sin salidat) aunque el arranque (en curso) se haga con normalidad, sin que el sistema se bloquee:

BIOS systems:

```
insmod vbe

```

UEFI systems:

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

Como puede ver, para que `gfxterm` funcione correctamente, la fuente `unicode.pf2` debe existir en `${GRUB_PREFIX_DIR`}.

### Mensaje de error msdos-style

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding will not be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

Este problema se produce cuando se intenta instalar GRUB en VMWare. Más información [aquí](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). También puede ocurrir cuando la partición comienza justo después del MBR (bloque 63), sin dejar un espacio de alrededor de 1 MB (2048 bloques) antes de la primera partición. Consulte [#Instrucciones específicas para Master Boot Record (MBR)](#Instrucciones_espec.C3.ADficas_para_Master_Boot_Record_.28MBR.29).

### UEFI

#### Errores comunes de instalación

*   Si tiene un problema cuando se ejecuta *grub-install* con *sysfs* o *procfs* y le avisa que debe ejecutar `modprobe efivars`, pruebe [montando efivarfs](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Montar_efivarfs "Unified Extensible Firmware Interface (Español)").
*   Sin las opciones `--target` o `--directory`, no se puede determinar en qué firmware se instalará. En tales casos, `grub-install` advertirá que `source_dir does not exist. Please specify --target or --directory`.
*   Si después de ejecutar grub-install le dice que la partición no se ve como una partición EFI, entonces es muy probable que la partición no esté formateada con `Fat32`.

#### Salta la consola de emergencia

Si GRUB carga, pero le deja en la consola de rescate sin errores, puede deberse a dos razones:

*   Que falte o esté fuera de lugar el archivo `grub.cfg`. Esto sucederá si GRUB UEFI se instaló con `--boot-directory` y `grub.cfg` no se encuentra.
*   Que la identificación de la partición de arranque, que está codificada en el archivo `grubx64.efi`, haya cambiado.

#### GRUB UEFI no se carga

He aquí un ejemplo de EFI funcional:

 `# efibootmgr -v` 
```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* Grub HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\efi\grub\grub.efi)
Boot0001* Shell HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EfiShell.efi)
Boot0002* Festplatte BIOS(2,0,00)P0: SAMSUNG HD204UI

```

Si la pantalla deviene en negro durante unos segundos y GRUB pasa a la siguiente opción del arranque, como se describe en [este post](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), mover GRUB a la partición raíz podría ayudar. La opción de arranque debería ser eliminada y regenerada después de la operación. La entrada para GRUB debería verse así:

```
Boot0000* Grub HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

#### Ruta de arranque default/fallback

Algunos firmwares UEFI requieren un archivo de arranque en una ubicación conocida antes de que se muestren las entradas de arranque UEFI NVRAM. Si este es el caso, `grub-install` solicitará que `efibootmgr` haya agregado una entrada para iniciar GRUB, sin embargo, la entrada no se mostrará en el selector del orden de arranque de VisualBIOS. La solución es instalar GRUB en la ruta de arranque default/fallback:

```
# grub-install --target=x86_64-efi --efi-directory=*esp* **--removable**

```

De forma alternativa, puede mover un ejecutable de GRUB EFI ya instalado a la ruta default/fallback:

```
# mv *esp*/EFI/grub *esp*/EFI/BOOT
# mv *esp*/EFI/BOOT/grubx64.efi *esp*/EFI/BOOT/BOOTX64.EFI

```

### Invalid signature

Si recibe el error *«invalid signature»* al intentar iniciar Windows, por ejemplo, si se ha alterado la tabla de particiones después de agregar otras particiones o discos duros, trate de eliminar la configuración de GRUB sobre los dispositivos y deje que la regenere él mismo:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig` debería ahora mostrar todas las opciones de arranque, incluyendo Windows. Si el problema está resuelto, elimine `/boot/grub/device.map-old`.

### Bloqueos al arrancar

Si el arranque se bloquea sin ningún mensaje de error, después de que GRUB cargue el kernel y el ramdisk inicial, pruebe eliminando `add_efi_memmap` de los parámetros del kernel.

### Arch no es detectado por otros sistemas operativos

Algunos usuarios han informado que otras distribuciones tienen problemas para encontrar Arch Linux automáticamente con `os-prober`. Si surge este problema, es posible mejorar la detección con la creación del archivo `/etc/lsb-release`. Este archivo y las herramientas de actualización están disponibles con el paquete [lsb-release](https://www.archlinux.org/packages/?name=lsb-release).

### Advertencias cuando se instala en entorno chroot

Durante la instalación de GRUB en un sistema LVM dentro de un entorno chroot (por ejemplo, durante la instalación del sistema), puede recibir advertencias como

```
/run/lvm/lvmetad.socket: connect failed: No such file or directory

```

o

```
WARNING: failed to connect to lvmetad: No such file or directory. Falling back to internal scanning.

```

Esto se debe a que `/run` no está disponible dentro del entorno chroot. Estas advertencias no impedirán que el sistema arranque, siempre que todo se haya hecho correctamente, por lo que puede continuar con la instalación.

### GRUB carga lentamente

GRUB puede tardar mucho tiempo en cargarse cuando el espacio en disco es pequeño. Compruebe si tiene suficiente espacio libre en el disco en su partición `/boot` o `/` cuando está teniendo problemas.

### error: unknown filesystem

GRUB puede mostrar la salida `error: unknown filesystem` y negarse a arrancar por varias razones. Si está seguro de que todas las [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)") son correctas y todos los sistemas de archivos son válidos y soportados, puede ser debido a que su [BIOS Boot Partition](#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29) se encuentra fuera de los primeros 2TB de su unidad [[2]](https://bbs.archlinux.org/viewtopic.php?id=195948). Utilice una herramienta de particionado de su elección para asegurarse de que esta partición se encuentra totalmente dentro de los primeros 2TB, y luego reinstale y reconfigure GRUB.

### grub-reboot no reinicia

GRUB parece incapaz de escribir a particiones root en BTRFS [[3]](https://bbs.archlinux.org/viewtopic.php?id=166131). Si usa grub-reboot para reiniciar en otra entrada no podra actualizar su entorno en-disco. Por lo tanto ejecute grub-reboot desde la otra entrada (por ejemplo, al cambiar entre varias distribuciones) o considere un sistema de archivos distinto. Es posible resetear una entrada "pegajosa" ejecutando `grub-editenv create` y estableciendo `GRUB_DEFAULT=0` en su `/etc/default/grub` (recuerde ejecutar `grub-mkconfig -o /boot/grub/grub.cfg`).

### El sistema de archivos BTRFS antiguo presiste en la instalación

Si una unidad fue formateada con BTRFS sin haber creado una tabla de particiones (por ejemplo /dev/sdx), y, porteriormente, se reescribe (con otro sistema de archivos) sobre dicha tabla de particiones, habrá partes del formato BTRFS que permanecerán. La mayoría de las utilidades y sistemas operativos no ven esto, pero GRUB se negará a instalar, incluso con la opción --force

```
# grub-install: warning: Attempting to install GRUB to a disk with multiple partition labels. This is not supported yet..
# grub-install: error: filesystem `btrfs' does not support blocklists.

```

Puede borrar con ceros la unidad, pero la solución más sencilla que deja en blanco sus datos es borrar la superbloque BTRFS con `wipefs -o 0x10040 /dev/sdx`

### Windows 8/10 no es encontrado

Una configuración en Windows 8/10 llamada «Hiberboot», «Hybrid Boot» or «Fast Boot» puede evitar que se monte la partición de Windows, por lo que `grub-mkconfig` no encontrará una instalación de Windows. La desactivación de Hiberboot en Windows permitirá que se agregue al menú de GRUB.

### Modalidad EFI en VirtualBox

Instale GRUB en la [ruta de arranque default/fallback](#Ruta_de_arranque_default.2Ffallback).

Consulte también [VirtualBox#Installation in EFI mode](/index.php/VirtualBox#Installation_in_EFI_mode "VirtualBox").

## Véase también

*   [Wikipedia:GNU GRUB](https://en.wikipedia.org/wiki/GNU_GRUB "wikipedia:GNU GRUB")
*   [Manual oficial de GRUB](https://www.gnu.org/software/grub/manual/grub.html)
*   [Página wiki de Ubuntu sobre GRUB](https://help.ubuntu.com/community/Grub2)
*   [Página wiki de GRUB donde explica cómo compilarlo para sistemas UEFI](https://help.ubuntu.com/community/UEFIBooting)
*   [Wikipedia:BIOS boot partition](https://en.wikipedia.org/wiki/BIOS_boot_partition "wikipedia:BIOS boot partition")
*   [Cómo configurar GRUB](http://web.archive.org/web/20160424042444/http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html#Editing_etcgrub.d05_debian_theme)
*   [Arrancar con GRUB](http://www.linuxjournal.com/article/4622)