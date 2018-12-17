**Estado de la traducción**
Este artículo es una traducción de [GRUB](/index.php/GRUB "GRUB"), revisada por última vez el **2018-12-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GRUB&diff=0&oldid=558675) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [Master Boot Record (Español)](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)")
*   [GUID Partition Table (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")
*   [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")
*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")
*   [GRUB/EFI examples](/index.php/GRUB/EFI_examples "GRUB/EFI examples")
*   [GRUB/Tips and tricks (Español)](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol) "GRUB/Tips and tricks (Español)")
*   [Multiboot USB drive (Español)](/index.php/Multiboot_USB_drive_(Espa%C3%B1ol) "Multiboot USB drive (Español)")

[GRUB](https://www.gnu.org/software/grub/) (GRand Unified Bootloader) es un [gestor multiarranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)"). Procede de [PUPA](http://www.nongnu.org/pupa/), el cual fue un proyecto de investigación desarrollado para reemplazar lo que hoy se conoce como [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"). Este último resultó demasiado difícil de mantener y GRUB se reescribió desde cero con el objetivo de proporcionarle modularidad y portabilidad [[1]](https://www.gnu.org/software/grub/grub-faq.html#q1). Al GRUB actual también se le conoce como GRUB 2, mientras que GRUB Legacy corresponde a las versiones 0.9x.

**Nota:** en el presente artículo, la expresión `*esp*` indica el punto de montaje de la [partición del sistema EFI (*«EFI system partition»*)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") conocida por sus siglas en ingles «**ESP**».

## Contents

*   [1 Sistemas BIOS](#Sistemas_BIOS)
    *   [1.1 Instrucciones específicas para GUID Partition Table (GPT)](#Instrucciones_específicas_para_GUID_Partition_Table_(GPT))
    *   [1.2 Instrucciones específicas para Master Boot Record (MBR)](#Instrucciones_específicas_para_Master_Boot_Record_(MBR))
    *   [1.3 Instalación](#Instalación)
*   [2 Sistemas UEFI](#Sistemas_UEFI)
    *   [2.1 Instalación](#Instalación_2)
*   [3 Configuration](#Configuration)
    *   [3.1 Archivo grub.cfg predeterminado](#Archivo_grub.cfg_predeterminado)
        *   [3.1.1 Generar el archivo de configuración principal](#Generar_el_archivo_de_configuración_principal)
        *   [3.1.2 Detectar otros sistemas operativos](#Detectar_otros_sistemas_operativos)
            *   [3.1.2.1 MS Windows](#MS_Windows)
        *   [3.1.3 Argumentos adicionales](#Argumentos_adicionales)
        *   [3.1.4 LVM](#LVM)
        *   [3.1.5 RAID](#RAID)
        *   [3.1.6 /boot cifrado](#/boot_cifrado)
    *   [3.2 Archivo grub.cfg personalizado](#Archivo_grub.cfg_personalizado)
        *   [3.2.1 Entradas del menú de arranque](#Entradas_del_menú_de_arranque)
            *   [3.2.1.1 Órdenes de GRUB](#Órdenes_de_GRUB)
                *   [3.2.1.1.1 Entrada de menú para «Apagar»](#Entrada_de_menú_para_«Apagar»)
                *   [3.2.1.1.2 Entrada de menú para «Reiniciar»](#Entrada_de_menú_para_«Reiniciar»)
                *   [3.2.1.1.3 Entrada de menú para «configurar el Firmware» (solo para UEFI)](#Entrada_de_menú_para_«configurar_el_Firmware»_(solo_para_UEFI))
            *   [3.2.1.2 Binarios de EFI](#Binarios_de_EFI)
                *   [3.2.1.2.1 Intérprete de órdenes de UEFI](#Intérprete_de_órdenes_de_UEFI)
                *   [3.2.1.2.2 gdisk](#gdisk)
                *   [3.2.1.2.3 Cargar en cadena un archivo .efi de Arch Linux](#Cargar_en_cadena_un_archivo_.efi_de_Arch_Linux)
            *   [3.2.1.3 Arranque dual](#Arranque_dual)
                *   [3.2.1.3.1 GNU/Linux](#GNU/Linux)
                *   [3.2.1.3.2 Windows instalado en modo UEFI/GPT](#Windows_instalado_en_modo_UEFI/GPT)
                *   [3.2.1.3.3 Windows instalado en modo BIOS-MBR](#Windows_instalado_en_modo_BIOS-MBR)
*   [4 Utilizar la consola de intérprete de órdenes](#Utilizar_la_consola_de_intérprete_de_órdenes)
    *   [4.1 Soporte para «pager»](#Soporte_para_«pager»)
    *   [4.2 Usar el entorno de la consola de intérprete de órdenes para arrancar distintos sistemas operativos](#Usar_el_entorno_de_la_consola_de_intérprete_de_órdenes_para_arrancar_distintos_sistemas_operativos)
        *   [4.2.1 Alternar el arranque desde una partition](#Alternar_el_arranque_desde_una_partition)
        *   [4.2.2 Alternar el arranque desde un disco/unidad](#Alternar_el_arranque_desde_un_disco/unidad)
        *   [4.2.3 Alternar el arranque de Windows/Linux instalados en modalidad UEFI](#Alternar_el_arranque_de_Windows/Linux_instalados_en_modalidad_UEFI)
        *   [4.2.4 Cargar en modo normal](#Cargar_en_modo_normal)
    *   [4.3 Utilizar la consola de rescate](#Utilizar_la_consola_de_rescate)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 F2FS y otros sistemas de archivos sin soporte](#F2FS_y_otros_sistemas_de_archivos_sin_soporte)
    *   [5.2 La BIOS de Intel no arranca con GPT](#La_BIOS_de_Intel_no_arranca_con_GPT)
    *   [5.3 Activar mensajes de depuración de errores](#Activar_mensajes_de_depuración_de_errores)
    *   [5.4 Corregir el error de GRUB: «no suitable mode found»](#Corregir_el_error_de_GRUB:_«no_suitable_mode_found»)
    *   [5.5 Mensaje de error msdos-style](#Mensaje_de_error_msdos-style)
    *   [5.6 UEFI](#UEFI)
        *   [5.6.1 Errores comunes de instalación](#Errores_comunes_de_instalación)
        *   [5.6.2 Salta la consola de emergencia](#Salta_la_consola_de_emergencia)
        *   [5.6.3 GRUB UEFI no se carga](#GRUB_UEFI_no_se_carga)
        *   [5.6.4 Ruta de arranque default/fallback](#Ruta_de_arranque_default/fallback)
    *   [5.7 Invalid signature](#Invalid_signature)
    *   [5.8 Bloqueos al arrancar](#Bloqueos_al_arrancar)
    *   [5.9 Arch no es detectado por otros sistemas operativos](#Arch_no_es_detectado_por_otros_sistemas_operativos)
    *   [5.10 Advertencias cuando se instala en entorno chroot](#Advertencias_cuando_se_instala_en_entorno_chroot)
    *   [5.11 GRUB carga lentamente](#GRUB_carga_lentamente)
    *   [5.12 error: unknown filesystem](#error:_unknown_filesystem)
    *   [5.13 grub-reboot no reinicia](#grub-reboot_no_reinicia)
    *   [5.14 El sistema de archivos BTRFS antiguo persiste en la instalación](#El_sistema_de_archivos_BTRFS_antiguo_persiste_en_la_instalación)
    *   [5.15 Windows 8/10 no es encontrado](#Windows_8/10_no_es_encontrado)
    *   [5.16 Modalidad EFI en VirtualBox](#Modalidad_EFI_en_VirtualBox)
*   [6 Véase también](#Véase_también)

## Sistemas BIOS

### Instrucciones específicas para GUID Partition Table (GPT)

En una configuración BIOS/[GPT](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)"), es necesaria crear una [*BIOS boot partition* (partición de arranque BIOS](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation)). GRUB incrusta su propia `core.img` en esta partición.

**Nota:**

*   Antes de intentar este método tenga en cuenta que no todos los sistemas serán capaces de soportar este esquema de particionado. Lea más sobre [Partitioning (Español)#GUID Partition Table](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)").
*   Esta partición adicional solo la necesita GRUB, en un esquema de particionado BIOS/GPT. Anteriormente, GRUB, en un esquema de particionado BIOS/MBR, usaba el espacio posterior al MBR para insertar su `core.img`. En una tabla de particionado GPT, sin embargo, no se puede garantizar que exista espacio suficiente (después del MBR y) antes de la primera partición.
*   Para sistemas [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") esta partición adicional no es necesaria, ya que en este caso no se lleva a cabo su incustración en los sectores de arranque. Sin embargo, los sistemas UEFI aún requieren una partición del sistema EFI «*[EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)")*».

Cree una partición de un mebibyte (MiB) (`+1M` con *fdisk* o *gdisk*) en el disco, sin formatearla con un sistema de archivos y con el GUID `21686148-6449-6E6F-744E-656564454649`.

*   Seleccione el código de tipo `BIOS boot` con [fdisk](/index.php/Fdisk "Fdisk").
*   Seleccione el código de tipo `ef02` con [gdisk](/index.php/Gdisk "Gdisk").
*   Con [parted](/index.php/Parted "Parted") establezca/active el flag `bios_grub`.

Esta partición puede estar colocada en cualquier parte del disco, pero tiene que estar en los primeros 2 TiB. Dicha partición debe ser creada antes instalar GRUB. Cuando la partición esté lista, instale el gestor de arranque de acuerdo con las instrucciones de abajo.

El espacio previo de la primera partición también se puede usar como la partición de arranque de la BIOS («*BIOS boot partition*»), aunque no se ajustará a las especificaciones de GPT sobre la alineación de la partición. Dado que no se accederá con regularidad a la partición, es posible ignorar el impacto sobre el rendimiento, aunque algunas utilidades de disco mostrarán una advertencia al respecto. Con *fdisk* o *gdisk* cree una partición nueva que se iniciará en el sector 34 y se extenderá hasta el 2047, y asígnele el tipo indicado antes. Para tener las particiones visibles al comienzo, considere la posibilidad de crear esta partición la última.

### Instrucciones específicas para Master Boot Record (MBR)

Por lo general, el espacio disponilbe después del [MBR](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") (después de los 512 bytes dedicados a ella, y antes de la primera partición), en cualquier sistema particionado con MBR es de 31 Kb, de modo que si hay algún problema de alineación de los cilindros se resuelven en la tabla de particiones. Sin embargo, se recomienda mantener una distancia de aproximadamente 1 a 2 MiB que proporcionará el espacio suficiente para contener la `core.img` de GRUB ([FS#24103](https://bugs.archlinux.org/task/24103)). Es recomendable utilizar una herramienta de particionado que permita la [alineación de una partición](/index.php/Partitioning_(Espa%C3%B1ol)#Alineamiento_de_las_particiones "Partitioning (Español)") de 1 MiB después del MBR, de modo que se pueda obtener el espacio necesario, y resolver otros problemas fuera de los primeros 512 bytes (que son ajenos a la incrustación de `core.img`).

### Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete [grub](https://www.archlinux.org/packages/?name=grub). Este reemplazará a [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/), si está instalado. Después ejecute:

```
# grub-install --target=i386-pc /dev/sd**X**

```

donde `/dev/sd**X**` es el disco donde se instalará grub (por ejemplo, el disco `/dev/sda` y **no** la partición `/dev/sda1`).

Ahora debe [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuración_principal).

Si usa [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") para `/boot`, puede instalar GRUB en varios discos físicos.

**Sugerencia:** consulte [GRUB/Tips and tricks (Español)#Métodos alternativos de instalación](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Métodos_alternativos_de_instalación "GRUB/Tips and tricks (Español)") para conocer otras formas de instalar GRUB, como en una memoria USB.

Consulte [grub-install(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grub-install.8) y el [manual de GRUB](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation) para obtener más detalles sobre la orden *grub-install*.

## Sistemas UEFI

**Nota:**

*   Es recomendable consultar y conocer las páginas [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), [Partitioning (Español)#GUID Partition Table](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)") y [Arch boot process (Español)#Bajo UEFI](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Bajo_UEFI "Arch boot process (Español)").
*   Si desea realizar la instalación con UEFI, es importante arrancar el soporte de instalación en la modalidad UEFI, de lo contrario *efibootmgr* no podrá agregar la entrada de inicio GRUB UEFI. La instalación en la [ruta de arranque fallback](#Ruta_de_arranque_default/fallback) seguirá funcionando incluso en el modo BIOS, ya que no toca la NVRAM.
*   Para arrancar desde un disco utilizando UEFI, se requiere una partición del sistema EFI. Siga [EFI system partition (Español)#Comprobar la existencia de una partición](/index.php/EFI_system_partition_(Espa%C3%B1ol)#Comprobar_la_existencia_de_una_partición "EFI system partition (Español)") para averiguar si ya tiene una; de lo contrario, deberá crearla.

### Instalación

**Nota:**

*   Es bien sabido que los fabricantes de placas base no implementan los firmware de UEFI de modo homogéneo. Los ejemplos de instalación descritos a continuación están destinados a trabajar en la más amplia gama de sistemas UEFI posibles. Se anima a los usuarios que experimenten problemas, a pesar de la aplicación de los métodos descritos, a compartir información detallada de sus casos específicos de hardware, cuando hayan encontrado solución a sus problemas. Para estos casos especiales se ha proporcionado un página de [ejemplos para GRUB EFI](/index.php/GRUB_EFI_Examples "GRUB EFI Examples").
*   Esta sección asume que está instalando GRUB para sistemas x86_64 (x86_64-efi). Para sistemas UEFI IA32 (32-bit) (no confundir con CPU de 32-bit), sustituya `x86_64-efi` con `i386-efi` donde proceda.

Primero, [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") los paquetes [grub](https://www.archlinux.org/packages/?name=grub) y [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr): *GRUB* es el gestor de arranque, mientras que *efibootmgr* es utilizado por el script de instalación de GRUB para escribir entradas de arranque a NVRAM.

A continuación, siga los siguientes pasos para instalar GRUB:

1.  [Monte la partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol)#Montar_la_partition "EFI system partition (Español)") y en el resto de esta sección, sustituya `*esp* `por su punto de montaje.
2.  Elija un identificador para el gestor de arranque, que aquí llamaremos `GRUB`. Se creará un directorio con ese nombre para almacenar el binario de EFI en la `*esp*/EFI/` y este es el nombre que aparecerá en el menú de arranque de UEFI para identificar la entrada de arranque de GRUB.
3.  Ejecute la siguiente orden para instalar la aplicación `grubx64.efi` de GRUB EFI en `*esp*/EFI/GRUB/` e instale sus módulos en `/boot/grub/x86_64-efi/`.

```
# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=GRUB

```

Después de completar la instalación anterior, el directorio principal de GRUB se encontrará en `/boot/grub/`.Tenga en cuenta que `grub-install` también intentará [crear una entrada en el gestor de arranque del firmware](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Crear_una_entrada_GRUB_en_el_gestor_de_arranque_del_firmware "GRUB/Tips and tricks (Español)"), llamada `GRUB` siguiendo el ejemplo anterior.

Recuerde [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuración_principal) al terminar la configuración.

**Sugerencia:** si usa la opción `--removable`, GRUB se instalará en `*esp*/EFI/BOOT/BOOTX64.EFI` (o `*esp*/EFI/BOOT/BOOTIA32.EFI` para la arquitectura `i386-efi`) y tendrá la capacidad adicional de poder arrancar desde la unidad, para el caso de que las variables EFI se reseteen o se mueva la unidad a otro equipo. Por lo general, puede hacer esto seleccionando la unidad en sí de manera similar a como lo haría con la BIOS. Si tiene un arranque dual con Windows, tenga en cuenta que Windows generalmente tiene una carpeta `BOOT` dentro de la carpeta `EFI` en la partición del sistema EFI, pero su único propósito es recrear la entrada de arranque UEFI para Windows.

**Nota:**

*   `--efi-directory` y `--bootloader-id` son opciones específicas de GRUB UEFI, `--efi-directory` reemplaza a `--root- directorio` que está en desuso.
*   Puede notar la ausencia de una opción *ruta_al_dispositivo* (por ejemplo, a `/dev/sda`) en la orden `grub-install`. De hecho, cualquier *ruta_al_dispositivo* proporcionada será ignorada por el script de instalación GRUB UEFI. Es más, los cargadores de arranque UEFI no usan un código de arranque MBR o sector de arranque de partición en absoluto.

Consulte la sección sobre [solución de problemas de UEFI](#UEFI) si tiene problemas. Vea también [GRUB/Tips and tricks (Español)#Lecturas adicionales de UEFI](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Lecturas_adicionales_de_UEFI "GRUB/Tips and tricks (Español)").

## Configuration

En un sistema instalado, GRUB carga el archivo de configuración `/boot/grub/grub.cfg` en cada arranque. Puede seguir [#Archivo grub.cfg predeterminado](#Archivo_grub.cfg_predeterminado) para una creación automática, o [#Archivo grub.cfg personalizado](#Archivo_grub.cfg_personalizado) para una creación manual.

### Archivo grub.cfg predeterminado

Esta sección cubre solo la edición del archivo de configuración `/etc/default/grub`. Consulte [GRUB/Tips and tricks (Español)](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol) "GRUB/Tips and tricks (Español)") si necesita más opciones.

Recuerde siempre [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuración_principal) después de realizar cambios en `/etc/default/grub`.

#### Generar el archivo de configuración principal

Después de instalar GRUB, se debe crear el archivo de configuración principal `grub.cfg`. El proceso de generación puede verse influido por una variedad de opciones presentes en `/etc/default/grub` y de scripts presentes en `/etc/grub.d/`.

Si no se ha hecho una configuración adicional, la generación automática determinará el sistema de archivos raíz del sistema que el archivo de configuración arrancará. Para que esto tenga éxito, es importante que el sistema o bien sea arrancable o bien se haga dentro de chroot.

**Nota:**

*   Recuerde que `grub.cfg` tiene que ser regenerado cada vez que se haga cualquier cambio en el archivo `/etc/default/grub` o en los archivos presentes en `/etc/grub.d/`
*   La ruta predeterminada del archivo es `/boot/grub/grub.cfg`, no `/boot/grub/i386-pc/grub.cfg`.
*   Si está intentando ejecutar *grub-mkconfig* en un entorno chroot o en un contenedor *systemd-nspawn*, puede notar que no funciona, avisando de que *grub-probe* no puede obtener la «canonical path of /dev/sdaX». En este caso, intente usar *arch-chroot* como se describe en [BBS post](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067).

Utilice la herramienta *grub-mkconfig* para generar `/boot/grub/grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Por defecto, los scripts de generación añaden automáticamente las entradas de menú para Arch Linux a cualquier configuración generada.

**Sugerencia:**

*   Después de instalar o eliminar un [kernel](/index.php/Kernel "Kernel"), solo necesita volver a ejecutar la orden *grub-mkconfig*.
*   Para obtener sugerencias sobre la gestión de múltiples entradas para GRUB, por ejemplo, al usar tanto el kernel [linux](https://www.archlinux.org/packages/?name=linux) como [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), vea [GRUB/Tips and tricks (Español)#Múltiples entradas](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Múltiples_entradas "GRUB/Tips and tricks (Español)").

Para agregar automáticamente entradas para otros sistemas operativos instalados, consulte [#Detectar otros sistemas operativos](#Detectar_otros_sistemas_operativos).

Puede agregar entradas de menú personalizadas adicionales editando `/etc/grub.d/40_custom` y regenerar `/boot/grub/grub.cfg`. O puede crear `/boot/grub/custom.cfg` y agregarlos allí. Los cambios en `/boot/grub/custom.cfg` no requieren que se vuelva a ejecutar *grub-mkconfig*, dado que `/etc/grub.d/40_custom` añade la declaración `source` necesaria al archivo de confiruación generado.

**Sugerencia:** `/etc/grub.d/40_custom` se puede usar como plantilla para crear `/etc/grub.d/*nn*_custom`. Donde `*nn*` define la prioridad, lo que indica el orden en que se ejecuta cada script. El orden en que se ejecutan los scripts determinan su ubicación en el menú de inicio de GRUB. `*nn*` debe ser mayor de `06` para garantizar que los scripts necesarios se ejecuten primero.

Consulte [#Entradas del menú de arranque](#Entradas_del_menú_de_arranque) para ver ejemplos de entradas de menú personalizadas.

#### Detectar otros sistemas operativos

Para que *grub-mkconfig* busque otros sistemas instalados y los agregue automáticamente al menú, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [os-prober](https://www.archlinux.org/packages/?name=os-prober) y [monte](/index.php/Mount "Mount") las particiones que contienen los otros sistemas. Luego vuelva a ejecutar *grub-mkconfig*.

##### MS Windows

Las particiones que contienen Windows deberían ser descubiertas automáticamente por [os-prober](https://www.archlinux.org/packages/?name=os-prober). Sin embargo, si la partición está encriptada, es posible que tenga que descifrarla antes del montaje. Para BitLocker, esto se puede hacer con [dislocker](https://aur.archlinux.org/packages/dislocker/). Esto debería ser suficiente para que [os-prober](https://www.archlinux.org/packages/?name=os-prober) agregue la entrada correcta.

#### Argumentos adicionales

Para pasar argumentos adicionales personalizados a la imagen de Linux, se pueden ajustar las variables `GRUB_CMDLINE_LINUX` + `GRUB_CMDLINE_LINUX_DEFAULT` en `/etc/default/grub`. Los dos parámetros se anexan al archivo y se pasan al kernel al generar las entradas de arranque regulares. Para la *recuperación* del sistema, basta con usar la variable `GRUB_CMDLINE_LINUX`.

No es necesario el uso de ambos, pero puede ser útil. Por ejemplo , podría utilizar`GRUB_CMDLINE_LINUX_DEFAULT="resume=UUID=*uuid-of-swap-partition* quiet"` cuando `*uuid-of-swap-partition*` es la partición de intercambio (swap) para activar la reanudación del sistema tras la hibernación. Esto generaría una entrada de arranque de reanudación y con el parámetro `quiet` no mostraría los mensajes del kernel durante el arranque desde esa entrada. Sin embargo, las otras entradas del menú (regulares) seguirían teniendo las opciones normales.

Por defecto, *grub-mkconfig* determina el [UUID](/index.php/UUID "UUID") del sistema de archivos raíz para la configuración. Para desactivar esto, descomente `GRUB_DISABLE_LINUX_UUID=true`.

Para generar la entrada de recuperación en GRUB asegúrese de que `GRUB_DISABLE_RECOVERY` en `/etc/default/grub` está definido como `true`.

Consulte [Kernel parameters (Español)](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para obtener más información.

#### LVM

**Advertencia:** GRUB no admite volúmenes lógicos de aprovisionamiento.

Si utiliza [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") para `/boot` o para la partición raíz `/` , asegúrese de que el módulo `lvm` se carga antes:

 `/etc/default/grub`  `GRUB_PRELOAD_MODULES="... lvm"` 

#### RAID

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

#### /boot cifrado

GRUB puede configurarse para solicitar una contraseña para abrir un dispositivo de bloque [LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)") a fin de leer su configuración y cargar cualquier [initramfs](/index.php/Initramfs "Initramfs") y [kernel](/index.php/Kernel "Kernel") desde él. Esta opción intenta resolver el problema de tener una [partición de arranque sin cifrar](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

**Nota:** `/boot` **no** necesita estar en una partición separada; puede estar en el mismo árbol de directorios del sistema raíz `/`.

**Advertencia:** GRUB no admite encabezados LUKS2; vea [GRUB bug #55093](https://savannah.gnu.org/bugs/?55093). Asegúrese de no especificar `luks2` en la línea de parámetros al crear la partición cifrada usando la orden `cryptsetup luksFormat`.

Para activar esta función, encripte la partición en la que resida `/boot` utilizando [LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)") de forma normal. A continuación, agregue la siguiente opción a `/etc/default/grub`:

 `/etc/default/grub`  `GRUB_ENABLE_CRYPTODISK=y` 

Grub-install utiliza esta opción para generar la imagen `core.img` de GRUB, de modo que asegúrese de [instalar GRUB](#Instalación) después de modificar esta opción.

Sin más cambios, se le solicitará dos veces una contraseña: la primera para GRUB para desbloquear el punto de montaje `/boot` en el arranque temprano, y la segunda para desbloquear el sistema de archivos raíz como se describe en [#Partición raíz](#Partición_raíz). Puede utilizar un [keyfile](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") para evitar esta doble contraseña.

**Advertencia:**

*   Si desea [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuración_principal), asegúrese de que `/boot` está montado.
*   Para realizar actualizaciones del sistema que incluyan el punto de montaje `/boot`, asegúrese de que `/boot` cifrado esté desbloqueado y montado antes de realizar una actualización. Con una partición separada `/boot`, esto puede lograrse automáticamente en el arranque usando [crypttab](/index.php/Crypttab "Crypttab") con un [archivo de claves](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol)#Con_un_archivo_de_clave_incrustado_en_initramfs "Dm-crypt/Device encryption (Español)").

**Nota:**

*   Si utiliza una distribución de teclado distinta de la predefinida, una instalación predeterminada de GRUB no lo sabrá. Esto es relevante para saber cómo introducir la contraseña para desbloquear el dispositivo de bloque cifrado con LUKS.
*   Si tiene problemas para que la solicitud de una contraseña se muestre en la pantalla (errores relacionados con cryptouuid, cryptodisk o «device not found»), pruebe volviendo a instalar GRUB como se indica a continuación, agregando lo siguiente `--modules="part_gpt part_msdos"` al final de la orden de instalación `grub-install`.

**Sugerencia:** puede usar [hooks de pacman](https://bbs.archlinux.org/viewtopic.php?id=234607) para montar automáticamente `/boot` cuando las actualizaciones necesiten acceder a archivos relacionados.

### Archivo grub.cfg personalizado

Esta sección describe la creación manual de entradas de inicio de GRUB en `/boot/grub/grub.cfg` en lugar de dejarlo en manos de *grub-mkconfig*.

Un archivo de configuración GRUB básico utiliza las siguientes opciones:

*   `(hd*X*,*Y*)` es la partición *Y* en el disco *X*, los números de las particiones comienzan en 1, los números de los discos comienzan en 0.
*   `set default=*N*` es la entrada de inicio predeterminada que se elige después del tiempo de espera como la acción definida por usuario.
*   `set timeout=*M*` es el tiempo *M* para esperar en segundos la selección del usuario antes de que se inicie el valor predeterminado.
*   `menuentry "title" {entry options}` es una entrada de inicio titulada `title`.
*   `set root=(hd*X*,*Y*)` establece la partición de inicio, donde se almacenan el kernel y los módulos de GRUB (el arranque no necesita ser desde una partición separada, y puede simplemente ser desde un directorio dentro de la partición «raíz» [`/`])

#### Entradas del menú de arranque

**Sugerencia:** estas entradas de inicio también se pueden usar cuando se utiliza `/boot/grub/grub.cfg` generado por *grub-mkconfig*. Agréguelas a `/etc/grub.d/40_custom` y vuelva a [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuración_principal) o añádalas a `/boot/grub/custom.cfg`.

Para obtener sugerencias sobre la gestión de múltiples entradas de GRUB, por ejemplo, al usar tanto el kernel [linux](https://www.archlinux.org/packages/?name=linux) como el [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), consulte [GRUB/Tips and tricks (Español)#Múltiples entradas](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Múltiples_entradas "GRUB/Tips and tricks (Español)").

Para las entradas del menú de inicio de [Archiso (Español)](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)") y [Archboot (Español)](/index.php/Archboot_(Espa%C3%B1ol) "Archboot (Español)"), consulte [Multiboot USB drive (Español)#Entradas de arranque](/index.php/Multiboot_USB_drive_(Espa%C3%B1ol)#Entradas_de_arranque "Multiboot USB drive (Español)").

##### Órdenes de GRUB

###### Entrada de menú para «Apagar»

```
menuentry "Apagar sistema" {
	echo "Apagando el sistema..."
	halt
}

```

###### Entrada de menú para «Reiniciar»

```
menuentry "Reiniciar sistema" {
	echo "Reiniciando el sistema..."
	reboot
}

```

###### Entrada de menú para «configurar el Firmware» (solo para UEFI)

```
if [ ${grub_platform} == "efi" ]; then
	menuentry "Configurar el firmware" {
		fwsetup
	}
fi
```

##### Binarios de EFI

Cuando se lanza en modo UEFI, GRUB puede cargar otros binarios de EFI.

**Sugerencia:** para mostrar estas entradas de menú solo cuando GRUB se inicia en modo UEFI, enciérrelas en la siguiente declaración `if`:
```
if [ ${grub_platform} == "efi" ]; then
	*coloque las entradas del menú solo de UEFI aquí*
fi
```

###### Intérprete de órdenes de UEFI

Puede iniciar el [intérprete de órdenes de UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Intérprete_de_órdenes_UEFI "Unified Extensible Firmware Interface (Español)") colocándolo en la raíz de la [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") y añadiendo esta entrada de menú:

```
menuentry "UEFI Shell" {
	insmod fat
	insmod chain
	search --no-floppy --set=root --file /shellx64.efi
	chainloader /shellx64.efi
}
```

###### gdisk

Descargue la [aplicación gdisk para EFI](/index.php/Gdisk#gdisk_EFI_application "Gdisk") y copie `gdisk_x64.efi` a `*esp*/EFI/tools/`.

```
menuentry "gdisk" {
	insmod fat
	insmod chain
	search --no-floppy --set=root --file /EFI/tools/gdisk_x64.efi
	chainloader /EFI/tools/gdisk_x64.efi
}
```

###### Cargar en cadena un archivo .efi de Arch Linux

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

##### Arranque dual

###### GNU/Linux

Suponiendo que la otra distribución está en la partición`sda2`:

```
menuentry "Otro Linux" {
	set root=(hd0,2)
	linux /boot/vmlinuz (añada aquí otras opciones necesarias)
	initrd /boot/initrd.img (si el otro kernel utiliza/necesita uno)
}
```

Alternativamente, deje que GRUB busque la partición correcta por *UUID* o *label* (etiqueta):

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

###### Windows instalado en modo UEFI/GPT

Este modo determina dónde reside el gestor de arranque de Windows y permite alternar su carga después de Grub cuando se selecciona su entrada en el menú. La principal tarea aquí es encontrar la partición EFI y ejecutar el gestor de arranque desde allí.

**Nota:** esta entrada de menú («menuentry») solo funcionará en modo de arranque UEFI y solo si el bit de Windows coincide con el bit de UEFI. No funcionará en sistemas BIOS con GRUB instalado. Consulte [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") y [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows") para obtener más información.

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

###### Windows instalado en modo BIOS-MBR

**Nota:** GRUB admite el arranque de `bootmgr` directamente y ya no es necesario [alternar la carga](https://www.gnu.org/software/grub/manual/grub.html#Chain_002dloading) del sector de arranque de la partición para iniciar Windows en una configuración de BIOS/MBR.

**Advertencia:** esta es la **system partition** que contiene `/bootmgr`, no la partición de Windows «real» (generalmente C:). En la salida de `blkid`, la partición del sistema es la que tiene `LABEL="SYSTEM RESERVED"` o `LABEL="SYSTEM"` y solo tiene entre 100 y 200 MB de tamaño (muy parecido a la partición de arranque para Arch). Consulte [Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") para más información.

A lo largo de esta sección, se supone que su partición de Windows es `/dev/sda1`. Una partición diferente cambiará cada instancia de `hd0,msdos1`.

**Nota:** estas entradas del menú funcionarán solo en la modalidad de arranque de sistemas BIOS. No funcionará en UEFI con GRUB instalado. Consulte [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") y [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows") .

En ambos ejemplos `*XXXXXXXXXXXXXXXX*` es el UUID del sistema de archivos, que se puede encontrar con la orden `lsblk --fs`.

Para Windows Vista/7/8/8.1/10:

```
if [ "${grub_platform}" == "pc" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1/10 BIOS/MBR" {
		insmod part_msdos
		insmod ntfs
		insmod ntldr     
		search --no-floppy --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 *XXXXXXXXXXXXXXXX*
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
		insmod ntldr     
		search --no-floppy --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 *XXXXXXXXXXXXXXXX*
		ntldr /ntldr
	}
fi
```

**Nota:** en algunos casos, GRUB puede instalarse sin un Windows 8 limpio, en cuyo caso no puede iniciar Windows sin tener un error con `\boot\bcd` (código de error `0xc000000f`). Puede solucionarlo acudiendo a la consola de recuperación de Windows -Windows Recovery Console- (`cmd.exe` desde el disco de instalación) y ejecutando:
```
X:\> bootrec.exe /fixboot
X:\> bootrec.exe /RebuildBcd

```

**No** utilice `bootrec.exe /Fixmbr` porque borrará GRUB. O puede usar la función de Reparación de Arranque («Boot Repair») en el menú Solución de Problemas -no eliminará GRUB sino que arreglará la mayoría de los errores-. Además, será mejor que permanezca **TAN SOLO** conectado al disco duro de destino y al dispositivo de arranque. Windows normalmente no puede reparar la información de arranque si hay otros dispositivos conectados.

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

Consulte primero [#Utilizar la consola de intérprete de órdenes](#Utilizar_la_consola_de_intérprete_de_órdenes) más arriba. Si no es capaz de iniciar la consola estándar, una posible solución es arrancar un CD live o alguna otra distribución a modo de recuperación para corregir los errores de configuración y reinstalar GRUB. Sin embargo, un disco de recuperación no siempre es posible (ni necesario), y la consola de emergencia es sorprendentemente robusta.

Las órdenes disponibles en esta modalidad incluyen `insmod`, `ls`, `set` y `unset`. Este ejemplo utiliza `set` y `insmod`. `set` cambia el valor de las variables, mientras que `insmod` añade nuevos módulos para ampliar la funcionalidad básica.

Antes de comenzar, es necesario que conozca la ubicación de `/boot` (ya esté en una partición separada o en un subdirectorio dentro de la partición raíz):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

donde X es el número de la unidad y la Y de la partición.

**Nota:** si está usando una partición de arranque separada, se omite `/boot` en la ruta. (por ejemplo, `set prefix=(hdX,Y)/grub`).

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

**Nota:** cuando el arranque es desde una partición separada y no parte de la partición raíz, debe direccionar a la partición de arranque manualmente, indicando la variable correspondiente.

```
set root=(hd0,5)
linux (hdX,Y)/vmlinuz-linux root=/dev/sda6
initrd (hdX,Y)/initramfs-linux.img
boot

```

**Nota:** si se experimentó el mensaje `error: premature end of file /EL_NOMBRE_DEL_KERNEL` durante la ejecución de la orden `linux`, pruebe usuando `linux16` en su lugar.

Tras el lanzamiento con éxito de una instalación de Arch Linux, los usuarios pueden corregir `grub.cfg` si fuese necesario y proceder a reinstalar GRUB.

Para reinstalar GRUB y arreglar completamente el problema, cambie `/dev/sda` de acuerdo a sus propias necesidades. Consulte el apartado sobre [#Instalación](#Instalación) para más detalles.

## Solución de problemas

### F2FS y otros sistemas de archivos sin soporte

GRUB no es compatible con el sistema de archivos [F2FS](/index.php/F2FS "F2FS"). En caso de que la partición raíz corra sobre un sistema de archivos no compatible, se debe crear una partición `/boot` alternativa formateada con un sistema de archivos compatible. En algunos casos, la versión de desarrollo de GRUB, [grub-git](https://aur.archlinux.org/packages/grub-git/), puede tener soporte nativo para el sistema de archivos.

Si se usa GRUB con un sistema de archivos no compatible, este no puede extraer el [UUID](/index.php/UUID "UUID") de su unidad, por lo que usará los nombres clásicos `/dev/*sdXx*` no persistentes. En este caso, es posible que tenga que editar manualmente `/boot/grub/grub.cfg` y sustituir `root=/dev/*sdXx*` por `root=UUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*`. Puede usar la orden `blkid` para obtener el UUID de su dispositivo, consulte [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)").

### La BIOS de Intel no arranca con GPT

Algunas BIOS de Intel requieren, al menos, una partición MBR marcada como booteable en el arranque, cosa no habitual en las configuraciones basadas en GPT, que provocan que la partición GPT no se inicie.

Es posible solucionar el problema mediante el uso de (por ejemplo) fdisk para marcar como «bootable» en el MBR una de las particiones GPT (preferiblemente la partición de 1007 KiB que ya se ha creado para GRUB). Esto se puede lograr, utilizando fdisk, mediante las siguientes órdenes: inicie fdisk sobre el disco donde va a realizar la instalación, por ejemplo `fdisk /dev/sda`, presione `a` y seleccione la partición que desea marcar como booteable (seguramente #1) pulsando el número correspondiente, para terminar pulse `w` para escribir los cambios en el MBR.

**Nota:** la marca de «bootable» puede hacerse en `fdisk` o similar, no con GParted u otros, ya que no configurarán el marcador de iniciable en el MBR.

Con cfdisk, los pasos son similares, bastando con `cfdisk/dev/sda`, elija el dispositivo de arranque (a la izquierda) en el disco duro deseado y salga guardando.

Con la versión más reciente de parted, puede usar la opción `disk_toggle pmbr_boot`. Luego verifique que los indicadores del disco muestren pmbr_boot.

```
# parted /dev/sd*x* disk_toggle pmbr_boot
# parted /dev/sd*x* print

```

Para más información consulte [esto](http://www.rodsbooks.com/gdisk/bios.html)

### Activar mensajes de depuración de errores

**Nota:** este cambio se sobrescribe al [#Generar el archivo de configuración principal](#Generar_el_archivo_de_configuración_principal).

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

A continuación, se debe iniciar el terminal gráfico GRUB (`gfxterm`), utilizando un modo de vídeo adecuado (`gfxmode`). Este se transmite de GRUB al kernel de Linux usando la opción `gfxpayload`. En sistemas UEFI, si la modalidad de video de GRUB no está inicializada, se mostrarán los mensajes de arranque del kernel (al menos hasta la activación de KMS).

Ahora, copie `/usr/share/grub/unicode.pf2` en `${GRUB2_PREFIX_DIR}` (`/boot/grub` de los sistema BIOS y UEFI). Si GRUB UEFI se instala con la opción `--boot-directory` activada, entonces la ruta sería `*esp*/EFI/grub/`:

```
# cp /usr/share/grub/unicode.pf2 ${GRUB_PREFIX_DIR}

```

Si el archivo `/usr/share/grub/unicode.pf2` no existe, instale el paquete [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) y proceda a la creación y copia del mismo en `${GRUB2_PREFIX_DIR}`.

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

En el archivo `grub.cfg`, agregue las líneas siguientes para permitir a GRUB que pase correctamente la modalidad de vídeo al kernel, de lo contrario obtendrá una pantalla en negro (sin salidat) aunque el arranque (en curso) se haga con normalidad, sin que el sistema se bloquee:

A continuación, agregue el siguiente código (común a los sistemas BIOS y UEFI)

```
loadfont "unicode"
set gfxmode=auto
set gfxpayload=keep
insmod all_video
insmod gfxterm
terminal_output gfxterm
```

### Mensaje de error msdos-style

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding will not be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

Este problema se produce cuando se intenta instalar GRUB en VMWare. Más información [aquí](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). También puede ocurrir cuando la partición comienza justo después del MBR (bloque 63), sin dejar un espacio de alrededor de 1 MB (2048 bloques) antes de la primera partición. Consulte [#Instrucciones específicas para Master Boot Record (MBR)](#Instrucciones_específicas_para_Master_Boot_Record_(MBR)).

### UEFI

#### Errores comunes de instalación

*   Si tiene un problema cuando se ejecuta *grub-install* con *sysfs* o *procfs* y le avisa que debe ejecutar `modprobe efivars`, pruebe [Unified Extensible Firmware Interface (Español)#Montar efivarfs](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Montar_efivarfs "Unified Extensible Firmware Interface (Español)").
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
Boot0000* GRUB HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EFI\GRUB\grubx64.efi)
Boot0001* Shell HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\shellx64.efi)
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

GRUB puede mostrar la salida `error: unknown filesystem` y negarse a arrancar por varias razones. Si está seguro de que todas las [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)") son correctas y todos los sistemas de archivos son válidos y soportados, puede ser debido a que su [BIOS Boot Partition](#Instrucciones_específicas_para_GUID_Partition_Table_(GPT)) se encuentra fuera de los primeros 2 TiB de su unidad [[2]](https://bbs.archlinux.org/viewtopic.php?id=195948). Utilice una herramienta de particionado de su elección para asegurarse de que esta partición se encuentra totalmente dentro de los primeros 2 TiB, y luego reinstale y reconfigure GRUB.

### grub-reboot no reinicia

GRUB parece incapaz de escribir a particiones root en BTRFS [[3]](https://bbs.archlinux.org/viewtopic.php?id=166131). Si usa grub-reboot para reiniciar en otra entrada no podra actualizar su entorno en-disco. Por lo tanto ejecute grub-reboot desde la otra entrada (por ejemplo, al cambiar entre varias distribuciones) o considere un sistema de archivos distinto. Es posible resetear una entrada "pegajosa" ejecutando `grub-editenv create` y estableciendo `GRUB_DEFAULT=0` en su `/etc/default/grub` (recuerde ejecutar `grub-mkconfig -o /boot/grub/grub.cfg`).

### El sistema de archivos BTRFS antiguo persiste en la instalación

Si una unidad fue formateada con BTRFS sin haber creado una tabla de particiones (por ejemplo /dev/sdx), y, porteriormente, se reescribe (con otro sistema de archivos) sobre dicha tabla de particiones, habrá partes del formato BTRFS que permanecerán. La mayoría de las utilidades y sistemas operativos no ven esto, pero GRUB se negará a instalar, incluso con la opción --force

```
# grub-install: warning: Attempting to install GRUB to a disk with multiple partition labels. This is not supported yet..
# grub-install: error: filesystem `btrfs' does not support blocklists.

```

Puede borrar con ceros la unidad, pero la solución más sencilla que deja en blanco sus datos es borrar la superbloque BTRFS con `wipefs -o 0x10040 /dev/sdx`

### Windows 8/10 no es encontrado

Una configuración en Windows 8/10 llamada «Hiberboot», «Hybrid Boot» o «Fast Boot» puede evitar que se monte la partición de Windows, por lo que `grub-mkconfig` no encontrará una instalación de Windows. La desactivación de Hiberboot en Windows permitirá que se agregue al menú de GRUB.

### Modalidad EFI en VirtualBox

Instale GRUB en la [ruta de arranque default/fallback](#Ruta_de_arranque_default/fallback).

Consulte también [VirtualBox (Español)#Instalación en modo EFI](/index.php/VirtualBox_(Espa%C3%B1ol)#Instalación_en_modo_EFI "VirtualBox (Español)").

## Véase también

*   [Wikipedia:GNU GRUB](https://en.wikipedia.org/wiki/GNU_GRUB "wikipedia:GNU GRUB")
*   [Manual oficial de GRUB](https://www.gnu.org/software/grub/manual/grub.html)
*   [Página wiki de Ubuntu sobre GRUB](https://help.ubuntu.com/community/Grub2)
*   [Página wiki de GRUB donde explica cómo compilarlo para sistemas UEFI](https://help.ubuntu.com/community/UEFIBooting)
*   [Wikipedia:BIOS boot partition](https://en.wikipedia.org/wiki/BIOS_boot_partition "wikipedia:BIOS boot partition")
*   [Cómo configurar GRUB](http://web.archive.org/web/20160424042444/http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html#Editing_etcgrub.d05_debian_theme)
*   [Arrancar con GRUB](http://www.linuxjournal.com/article/4622)