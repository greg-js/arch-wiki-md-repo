**Estado de la traducción**
Este artículo es una traducción de [Syslinux](/index.php/Syslinux "Syslinux"), revisada por última vez el **2015-01-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Syslinux&diff=0&oldid=354890) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Arch Boot Process (Español)](/index.php/Arch_Boot_Process_(Espa%C3%B1ol) "Arch Boot Process (Español)")
*   [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)")

[Syslinux](https://en.wikipedia.org/wiki/es:Syslinux "wikipedia:es:Syslinux") es una colección de cargadores de arranque capaz de iniciar desde discos duros, CDs, y vía network utilizando PXE. Soporta sistema de archivos [FAT](https://en.wikipedia.org/wiki/es:Tabla_de_asignaci%C3%B3n_de_archivos "wikipedia:es:Tabla de asignación de archivos"), [ext2](https://en.wikipedia.org/wiki/es:Ext2 "wikipedia:es:Ext2"), [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4") y [Btrfs](/index.php/Btrfs "Btrfs").

**Nota:** Syslinux no está en condiciones de acceder a los archivos contenidos en una partición diferente de aquella en la cual se ha instalado. Tal característica (llamada multi-fs) no está aún implementada. Para un gestor de arranque alternativo con características multi-fs. véase [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)").

## Contents

*   [1 Sistemas BIOS](#Sistemas_BIOS)
    *   [1.1 Proceso de arranque de Syslinux](#Proceso_de_arranque_de_Syslinux)
    *   [1.2 Instalación](#Instalaci.C3.B3n)
        *   [1.2.1 Instalación automática](#Instalaci.C3.B3n_autom.C3.A1tica)
        *   [1.2.2 Instalación manual](#Instalaci.C3.B3n_manual)
            *   [1.2.2.1 Tabla de particiones MBR](#Tabla_de_particiones_MBR)
            *   [1.2.2.2 Tabla de particiones GUID conocida como GPT](#Tabla_de_particiones_GUID_conocida_como_GPT)
*   [2 Sistemas UEFI](#Sistemas_UEFI)
    *   [2.1 Limitaciones de Syslinux en la modalidad UEFI](#Limitaciones_de_Syslinux_en_la_modalidad_UEFI)
    *   [2.2 Instalación](#Instalaci.C3.B3n_2)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Ejemplos](#Ejemplos)
        *   [3.1.1 Prompt de arranque](#Prompt_de_arranque)
        *   [3.1.2 Menú de arranque en modo texto](#Men.C3.BA_de_arranque_en_modo_texto)
        *   [3.1.3 Menú de arranque en modo gráfico](#Men.C3.BA_de_arranque_en_modo_gr.C3.A1fico)
    *   [3.2 Parámetros del kernel](#Par.C3.A1metros_del_kernel)
    *   [3.3 Arranque automático](#Arranque_autom.C3.A1tico)
    *   [3.4 Seguridad](#Seguridad)
    *   [3.5 Chainloading](#Chainloading)
    *   [3.6 Chainloading de otros sistemas Linux](#Chainloading_de_otros_sistemas_Linux)
    *   [3.7 Usar memtest](#Usar_memtest)
    *   [3.8 HDT](#HDT)
    *   [3.9 Reinicio y apagado](#Reinicio_y_apagado)
    *   [3.10 Limpiar el menú](#Limpiar_el_men.C3.BA)
    *   [3.11 Distribución del teclado](#Distribuci.C3.B3n_del_teclado)
    *   [3.12 Ocultar el menú](#Ocultar_el_men.C3.BA)
    *   [3.13 Pxelinux](#Pxelinux)
    *   [3.14 Arrancar una imágen ISO9660 con memdisk](#Arrancar_una_im.C3.A1gen_ISO9660_con_memdisk)
*   [4 Solución de Problemas](#Soluci.C3.B3n_de_Problemas)
    *   [4.1 Utilizar el prompt de Syslinux](#Utilizar_el_prompt_de_Syslinux)
    *   [4.2 Fallo de fsck en la partición root](#Fallo_de_fsck_en_la_partici.C3.B3n_root)
    *   [4.3 Default o UI no encontrado en su equipo](#Default_o_UI_no_encontrado_en_su_equipo)
    *   [4.4 Missing operating system](#Missing_operating_system)
    *   [4.5 ¡Se inicia Windows en vez de Syslinux!](#.C2.A1Se_inicia_Windows_en_vez_de_Syslinux.21)
    *   [4.6 Entradas del menú sin ningún efecto](#Entradas_del_men.C3.BA_sin_ning.C3.BAn_efecto)
    *   [4.7 Imposible eliminar ldlinux.sys](#Imposible_eliminar_ldlinux.sys)
    *   [4.8 Se visualiza un cuadrado blanco en el ángulo superior izquierdo cuando se utiliza vesamenu](#Se_visualiza_un_cuadrado_blanco_en_el_.C3.A1ngulo_superior_izquierdo_cuando_se_utiliza_vesamenu)
    *   [4.9 Cargar Windows no funciona, cuando se instala en otra unidad](#Cargar_Windows_no_funciona.2C_cuando_se_instala_en_otra_unidad)
    *   [4.10 Leer el registro del gestor de arranque](#Leer_el_registro_del_gestor_de_arranque)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Sistemas BIOS

### Proceso de arranque de Syslinux

1.  **Etapa 1:**
    *   **Fase 1** - **Carga del MBR** - En el arranque del ordenador, la BIOS lee el código de arranque contenido en el [MBR](/index.php/MBR "MBR"), la región de los 440 byte, situada al inicio del disco (donde residen los archivos (`/usr/lib/syslinux/bios/mbr.bin` o `/usr/lib/syslinux/bios/gptmbr.bin`).
    *   **Fase 2** - **Busqueda de la partición activa**. El **Stage 1 MBR boot code** busca la partición marcada como activa (etiqueta «boot» en los discos MBR). En el ejemplo se presume que tal partición corresponde a la que está `/boot`.
2.  **Etapa 2:**
    *   **Fase 1** - **Ejecución del volume boot record** - El **Stage 1 MBR boot code** ejecuta el Volume Boot Record (VBR) de la partición `/boot`. En el caso de syslinux, el VBR boot code está en el inicio del sector definido en el archivo `/boot/syslinux/ldlinux.sys` creado con la orden `extlinux --install`. Advierta que `ldlinux.sys` y `ldlinux.c32` no son lo mismo.
    *   **Fase 2** - **Ejecución de `/boot/syslinux/ldlinux.sys`** - El VBR cargará el resto del archivo `/boot/syslinux/ldlinux.sys`, cuya ubicación en el disco no debe cambiar, de lo contrario syslinux no arrancará.
        **Nota:** En el caso del sistemas de archivos [Btrfs](/index.php/Btrfs "Btrfs"), el método anterior no funcionará ya que los archivos están constantemente moviéndose, de lo que resulta un cambio de la ubicación del archivo `ldlinux.sys`. Por lo tanto, en el caso de BTRFS el código completo de `ldlinux.sys` estará embebido en el espacio que le sigue al VBR y no vendrá instalado en `/boot/syslinux/ldlinux.sys`, a diferencia de otros sistemas de archivos.

3.  **Etapa 3:**
    *   **Carga de `/boot/syslinux/ldlinux.c32`** - El archivo `/boot/syslinux/ldlinux.sys` cargará `/boot/syslinux/ldlinux.c32` (módulo del núcleo) que contiene el resto de la parte del **núcleo** de syslinux que no encaja en `ldlinux.sys` (debido a las limitaciones respecto al tamaño de archivo). El archivo `ldlinux.c32` debe estar presente en todas las instalaciones de syslinux/extlinux y debe coincidir con la versión de `ldlinux.sys` instalada en la partición. De lo contrario syslinux no podrá arrancar. Véase [http://bugzilla.syslinux.org/show_bug.cgi?id=7](http://bugzilla.syslinux.org/show_bug.cgi?id=7) para más información.
4.  **Etapa 4:**
    *   **Localización y carga del archivo de configuración** - Una vez que Syslinux está completamente cargado, buscará `/boot/syslinux/syslinux.cfg` (o `/boot/syslinux/extlinux.conf` en algunos casos) y lo cargará, si lo encuentra. Si no lo encuentra, syslinux lanzará el prompt `boot:`. El paso descrito y el resto de la parte **no principal** de syslinyux (los módulos (`/boot/syslinux/*.c32`, excluyendo los `lib*.c32`, y `ldlinux.c32`) necesitan la presencia de los módulos `/boot/syslinux/lib*.c32` (bibliotecas). Los módulos de las bibliotecas, `lib*.c32`, y los módulos no principales, `*.c32`, deben coincidir con la versión de `ldlinux.sys` instalada en la partición.

### Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [syslinux](https://www.archlinux.org/packages/?name=syslinux) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

**Nota:**

*   A partir de Syslinux 4, Extlinux y Syslinux son la misma cosa.
*   [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) es necesario para proporcionar soporte a [GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") utilizando el script automático.
*   Si su partición boot es FAT, necesita también [mtools](https://www.archlinux.org/packages/?name=mtools).

#### Instalación automática

**Nota:** El script `syslinux-install_update` es un guión específico de Arch, y no es proporcionado/mantenido por los desarrolladores de Syslinux. Por favor, dirija cualquier informe de error específico a Arch Bug Tracker y no a los desarrolladores.

El script `syslinux-install_update` se ocupará de la instalación de Syslinux, de la copia/creación del enlace simbólico para el módulo `*.c32` en `/boot/syslinux`, de la configuración de la etiqueta «boot» y de la instalación del código de arranque en el MBR. Puede gestionar tablas de particiones [MBR](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") y [GPT](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)"), junto con RAID software.

1.  Si se utiliza una partición boot separada, asegúrese de que está montada. Compruébelo con `lsblk`; si no se ve ningún punto de montaje que indique a `/boot`, monte la partición antes de continuar.

2.  Ejecute el script `syslinux-install_update` con los siguientes argumentos: `-i` (instala los archivos), `-a` (marca la partición como *activa* con la etiqueta *boot*), `-m` (instala el código de arranque en el *MBR*): `# syslinux-install_update -i -a -m` Si esta orden falla con el mensaje *Syslinux BIOS install failed*, el problema sea posiblemente que el binario `extlinux` no pudo encontrar la partición que contiene `/boot`:
    ```
    # extlinux --install /boot/syslinux
     extlinux: cannot find device for path /boot/syslinux
     extlinux: cannot open device (null)

    ```
    Esto puede ocurrir, por ejemplo, al actualizar de [LILO](/index.php/LILO "LILO") con un kernel personalizado corriendo, operación que convierte un parámetro de la línea de órdenes del kernel (de ejemplo `root=/dev/sda1`) en su equivalente numérico `root=801`, como se evidencia por las salidas de las órdenes `/proc/cmdline` y `mount`. Es posible remediar este problema ejecutando la instalación manual descrita abajo, cuidando de especificar el parámetro `--device=/dev/sda1` a `extlinux`, o, simplemente, al reiniciar la primera vez el kernel stock de Arch Linux, dado que el uso de su initramfs evita el problema.
3.  Cree o edite `/boot/syslinux/syslinux.cfg` siguiendo las instrucciones de [#Configuración](#Configuraci.C3.B3n).

**Advertencia:** Es importante señalar a Syslinux la partición root correcta, o el sistema no arrancará. Véase [#Parámetros del kernel](#Par.C3.A1metros_del_kernel).

**Nota:**

*   Al reiniciar el sistema ahora, se tendrá un prompt de Syslinux. Para arrancar automáticamente el sistema o conseguir un menú de arranque, todavía habrá que crear un archivo de configuración.
*   Sise está en otro directorio raíz (por ejemplo, si se está utilizando un disco de instalación) instale syslinux dirigiendo al entorno chroot:

```
# syslinux-install_update.sh -i -a -m -c /mnt/

```

#### Instalación manual

**Nota:**

*   Si no está seguro de la tabla de particiones que está utilizando (MBR o GPT), se puede comprobar con la siguiente orden:

```
# blkid -s PTTYPE -o value /dev/sda
gpt

```

*   Si sew está tratando de rescatar un sistema instalado con un live CD, asegúrese de efectuar [chroot](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") antes de ejecutar las siguientes órdenes. Si no efectúa chroot, será necesario anteponer el punto de montaje a todas las rutas especificadas (salvo las que se inician con `/dev/`).

La partición de arranque, en la que se tiene previsto instalar Syslinux, debe estar formateada con un sistema de archivos FAT, ext2, ext3, ext4, o Btrfs. Se debe instalar sobre un directorio montado (y no sobre una partición `/dev/sdXY`). No es necesario instalarlo en el directorio root de un sistema de archivos, por ejemplo, si tenemos la partición `/dev/sda1` montada en `/boot` es posible instalar Syslinux en el directorio `syslinux`:

```
# mkdir /boot/syslinux
# cp -r /usr/lib/syslinux/bios/*.c32 /boot/syslinux/                           ## copy ALL the *.c32 files from /usr/lib/syslinux/bios/, DO NOT SYMLINK
# extlinux --install /boot/syslinux

```

Después de esto, instale el código de arranque de Syslinux, (`mbr.bin` o `gptmbr.bin`), en el Master Boot Record, la región de los 440 byte del disco que alberga el código de arranque (que no se debe confundir con MBR conocida como tabla de particiones msdos).

##### Tabla de particiones MBR

Véase el artículo principal: [Master Boot Record (Español)](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)").

Será necesario marcar la partición boot como activa en la tabla de particiones. Las aplicaciones que incluyen la capacidad de hacer la operación descrita son `fdisk`, `cfdisk`, `sfdisk`, `parted/gparted` (etiqueta «boot»). Debería tener un aspecto como el siguiente:

 `# fdisk -l /dev/sda` 
```
[...]
  Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048      104447       51200   83  Linux
/dev/sda2          104448   625142447   312519000   83  Linux

```

Instale Syslinux en el MBR:

```
# dd bs=440 count=1 conv=notrunc if=/usr/lib/syslinux/mbr.bin of=/dev/sda

```

Syslinux proporciona un MBR alternativo: `altmbr.bin`. Este MBR *no* escanea en busca de particiones booteables, sino que el último byte de la MBR establece un valor que indica la partición desde la cual efectuar el arranque. Aquí está un ejemplo de cómo `altmbr.bin` puede copiar esa posición:

```
# printf '\x5' | cat /usr/lib/syslinux/altmbr.bin - | \
dd bs=440 count=1 iflag=fullblock conv=notrunc of=/dev/sda

```

En este caso, un solo byte de valor 5 se inserta en el contenido del archivo `altmbr.bin` y los restantes 440 bytes se escriben en el MBR del dispositivo `sda`. Syslinux será instalado en la primera partición lógica (`/dev/sda5`) del disco.

##### Tabla de particiones GUID conocida como GPT

Véase el artículo principal: [GUID Partition Table (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)").

Es necesario ajustar el bit 2 a los atributos (atributo «legacy_boot») relativos a la partición `/boot`.

```
# sgdisk /dev/sda --attributes=1:set:2

```

Esto cambiará el atributo *legacy BIOS bootable* en la partición 1\. Para comprobarlo:

 `# sgdisk /dev/sda --attributes=1:show` 
```
 1:2:1 (legacy BIOS bootable)

```

Instalación en el MBR:

```
# dd bs=440 conv=notrunc count=1 if=/usr/lib/syslinux/gptmbr.bin of=/dev/sda

```

Si esto no funciona, pruebe con esto:

```
# syslinux-install_update -i -m

```

## Sistemas UEFI

**Nota:**

*   `$esp` es el punto de montaje de la ESP en las órdenes siguientes.

*   `efi64` indica sistemas UEFI con arquitectura de x86_64, para IA32 (32-bit), sustituya `efi64` con `efi32`.

*   Syslinux, requiere que el kernel y los archivos initramfs residan en la partición ESP, en tanto que syslinux no tiene, actualmente, la capacidad de acceder a los archivos que están fuera de su propia partición (es decir, fuera de ESP, en este caso). Por esta razón, se recomienda montar ESP en `/boot`.

*   El script de instalación automática `/usr/bin/syslinux-install_update` no es compatible para instalar UEFI.

*   La sintaxis de configuración de `syslinux.cfg` para UEFI es la misma que la de la BIOS.

### Limitaciones de Syslinux en la modalidad UEFI

*   La aplicación de Syslinux UEFI, `syslinux.efi`, no puede ser firmada por `sbsign` (paquete sbsigntool) para su uso por UEFI Secure Boot. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=8](http://bugzilla.syslinux.org/show_bug.cgi?id=8)

*   La utilización de la tecla TAB para editar los parámetros del kernel del menú de Syslinux UEFI crea errores en la pantalla (texto encima de otro). Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=9](http://bugzilla.syslinux.org/show_bug.cgi?id=9)

*   Syslinux UEFI no soporta cargar en cadena otras aplicaciones EFI como `UEFI Shell` o `Windows Boot Manager`. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=17](http://bugzilla.syslinux.org/show_bug.cgi?id=17)

*   En algunos casos, puede que Syslinux UEFI no arranque en máquinas virtuales como QEMU/OVMF o VirtualBox o VMware y en algunos entornos de emulación UEFI como DUET. Un contribuidor de Syslinux ha confirmado que estos problemas no están presentes en VMware Workstation 10.0.2 y Syslinux-6.02 o posterior. Bug reports - [http://bugzilla.syslinux.org/show_bug.cgi?id=21](http://bugzilla.syslinux.org/show_bug.cgi?id=21) and [http://bugzilla.syslinux.org/show_bug.cgi?id=23](http://bugzilla.syslinux.org/show_bug.cgi?id=23)

*   Memdisk no está disponible para UEFI. Bug report - [http://bugzilla.syslinux.org/show_bug.cgi?id=30](http://bugzilla.syslinux.org/show_bug.cgi?id=30)

### Instalación

*   Instale el paquete [syslinux](https://www.archlinux.org/packages/?name=syslinux) y configure syslinux en la partición EFI del sistema (ESP) como sigue:

```
# pacman -S syslinux

```

*   Copie los archivos de syslinux a ESP:

```
# mkdir -p $esp/EFI/syslinux
# cp -r /usr/lib/syslinux/efi64/* $esp/EFI/syslinux

```

*   Cree una entrada de arranque para Syslinux utilizando [efibootmgr](#Unified_Extensible_Firmware_Interface.23efibootmgr):

```
# mount -t efivarfs efivarfs /sys/firmware/efi/efivars
# efibootmgr -c -d /dev/sdX -p 1 -l /EFI/syslinux/syslinux.efi -L "Syslinux"

```

*   Cree o modifique `$esp/EFI/syslinux/syslinux.cfg` siguiendo las instrucciones de [#Configuración](#Configuraci.C3.B3n).

**Nota:** El archivo de configuración de UEFI es `$esp/EFI/syslinux/syslinux.cfg`, no `/boot/syslinux/syslinux.cfg`. Los archivos en `/boot/syslinux/` son específicos de BIOS y no están relacionados con UEFI.

## Configuración

El archivo de configuración de syslinux, `syslinux.cfg`, se debe crear en el mismo directorio donde se ha instalado syslinux. En este caso, `/boot/syslinux/` para sistemas BIOS y `$esp/EFI/syslinux/` para sistemas UEFI.

El gestor de arranque buscará el archivo `syslinux.cfg` (preferido) o bien `extlinux.conf`

**Sugerencia:**

*   En lugar de utilizar como palabra clave `LINUX`, se puede utilizar también `KERNEL`. `KERNEL` intenta detectar el tipo del archivo, mientras que `LINUX` siempre espera un kernel Linux como parámetro.
*   El valor `TIMEOUT` está en unidades de **un décimo** de segundo.

### Ejemplos

**Nota:** Cualquier archivo de configuración mostrado en estos ejemplos necesita ser editado para establecer los parámetros adecuados del kernel. Véase la sección [#Parámetros del kernel](#Par.C3.A1metros_del_kernel).

#### Prompt de arranque

Este es un archivo de configuración simple que mostrará un prompt `boot:` y un arranque automático después de 5 segundos. Si desea arrancar directamente sin ver el prompt, ajuste `PROMPT` a `0`.

Configuración:

 `/boot/syslinux/syslinux.cfg` 
```
 PROMPT 1
 TIMEOUT 50
 DEFAULT arch

 LABEL arch
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux.img

 LABEL archfallback
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux-fallback.img

```

#### Menú de arranque en modo texto

Syslinux también le permite utilizar un menú de arranque. Para utilizarlo, copiar el modulo `menu` en el directorio Syslinux:

```
# cp /usr/lib/syslinux/bios/menu.c32 /boot/syslinux/

```

Configuration:

 `/boot/syslinux/syslinux.cfg` 
```
 UI menu.c32
 PROMPT 0

 MENU TITLE Boot Menu
 TIMEOUT 50
 DEFAULT arch

 LABEL arch
         MENU LABEL Arch Linux
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux.img

 LABEL archfallback
         MENU LABEL Arch Linux Fallback
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux-fallback.img

```

Para más detalles sobre el sistema de menús, véase [the Syslinux documentation](http://git.kernel.org/?p=boot/syslinux/syslinux.git;a=blob;f=doc/menu.txt) or [the Syslinux wiki](http://www.syslinux.org/wiki/index.php/Menu).

#### Menú de arranque en modo gráfico

Syslinux permite también el uso de un menú de arranque gráfico. Para usarlo, copie el módulo COM32 `vesamenu` en la carpeta de Syslinux

```
# cp /usr/lib/syslinux/bios/vesamenu.c32 /boot/syslinux/

```

**Nota:** Si utiliza [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)") asegúrese de copiar desde `/usr/lib/syslinux/efi64/` (`efi32` para sistemas i686), de lo contrario se mostrará una pantalla en negro. En ese caso, arranque desde un medio live y utilice [chroot](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") para hacer los cambios apropiados.

Esta configuración utiliza el mismo diseño del menú del CD de instalación de Arch Install, dicha configuración se puede encontrar en [projects.archlinux.org](https://projects.archlinux.org/archiso.git/tree/configs/releng/syslinux). La [imagen de fondo de Arch Linux](https://projects.archlinux.org/archiso.git/plain/configs/releng/syslinux/splash.png) se puede descargar desde allí, también. Copie la imagen a `/boot/syslinux/splash.png`.

Configuración:

 `/boot/syslinux/syslinux.cfg` 
```
 UI vesamenu.c32
 DEFAULT arch
 PROMPT 0
 MENU TITLE Boot Menu
 MENU BACKGROUND splash.png
 TIMEOUT 50

 MENU WIDTH 78
 MENU MARGIN 4
 MENU ROWS 5
 MENU VSHIFT 10
 MENU TIMEOUTROW 13
 MENU TABMSGROW 11
 MENU CMDLINEROW 11
 MENU HELPMSGROW 16
 MENU HELPMSGENDROW 29

 # Refer to http://www.syslinux.org/wiki/index.php/Comboot/menu.c32

 MENU COLOR border       30;44   #40ffffff #a0000000 std
 MENU COLOR title        1;36;44 #9033ccff #a0000000 std
 MENU COLOR sel          7;37;40 #e0ffffff #20ffffff all
 MENU COLOR unsel        37;44   #50ffffff #a0000000 std
 MENU COLOR help         37;40   #c0ffffff #a0000000 std
 MENU COLOR timeout_msg  37;40   #80ffffff #00000000 std
 MENU COLOR timeout      1;37;40 #c0ffffff #00000000 std
 MENU COLOR msg07        37;40   #90ffffff #a0000000 std
 MENU COLOR tabmsg       31;40   #30ffffff #00000000 std

 LABEL arch
         MENU LABEL Arch Linux
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux.img

 LABEL archfallback
         MENU LABEL Arch Linux Fallback
         LINUX ../vmlinuz-linux
         APPEND root=/dev/sda2 rw
         INITRD ../initramfs-linux-fallback.img

```

A partir de Syslinux 3.84, `vesamenu.c32` soporta la directiva `MENU RESOLUTION $WIDTH $HEIGHT`. Para usarla, inserte `MENU RESOLUTION 1440 900` para configurar, por ejemplo, una resolución de 1440x900. La imagen background tendrá que ser de la misma resolución, de otra manera, Syslinux rechazará la carga del menú.

### Parámetros del kernel

Los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") se establecen en la línea `APPEND` de `syslinux.cfg`. Se recomienda realizar los siguientes cambios para la entrada fallback también.

En el caso más simple, el nombre de la partición raiz en el parámetro `root` necesita ser reemplazado. Cambie `/dev/sda2` para que indique la partición root correcta.

```
APPEND root=/dev/sda2

```

Si desea utilizar [UUID](/index.php/UUID "UUID") para [persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") cambie la línea `APPEND` como sigue, sustituyendo `1234` con la `UUID` de la partición root:

```
APPEND root=UUID=*1234* rw

```

Si utiliza el cifrado [LUKS](/index.php/LUKS "LUKS") cambie la línea `APPEND` para utilizar el volumen cifrado:

```
APPEND root=/dev/mapper/*group*-*name* cryptdevice=/dev/sda2:*name* rw

```

Si está utilizando el software [RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID") con [mdadm](http://neil.brown.name/blog/mdadm), cambie la línea `APPEND` para dar cabida a sus matrices RAID. A modo de ejemplo, la siguiente línea tiene capacidad para tres matrices RAID 1 y establece la matriz apropiada para root:

```
APPEND root=/dev/md1 rw md=0,/dev/sda2,/dev/sdb2 md=1,/dev/sda3,/dev/sdb3 md=2,/dev/sda4,/dev/sdb4

```

Si el arranque desde una partición de software RAID falla al utilizar el método de nodo del dispositivo del kernel propuesto arriba como alternativa, una vía más confiable, es usar las etiquetas de las particiones:

```
APPEND root=LABEL=LAETIQUETADELAPARTICIÓNROOT rw

```

### Arranque automático

Si no desea ver el menú de Syslinux en absoluto, comente todas los comandos `UI` y asegúrese de que hay un `DEFAULT` configurado en `syslinux.cfg`.

### Seguridad

Syslinux tiene dos niveles de seguridad para el gestor de arranque: una contraseña maestra para el menú y una contraseña para cada elemento del menú. En `syslinux.cfg`, utilice

```
MENU MASTER PASSWD passwd 

```

para establecer una contraseña maestra del gestor de arranque, y

```
MENU PASSWD passwd 

```

dentro de un bloque `LABEL` para proteger con contraseña los elementos individuales del arranque.

### Chainloading

Si desea cargar en cadena otros sistemas operativos (como Windows) u otros gestores de arranque, copie (o utilice un enlace simbólico) el módulo `chain.c32` en el directorio Syslinux (para más detalles, consulte las instrucciones de la sección anterior). A continuación, cree una sección en el archivo de configuración:

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL windows
         MENU LABEL Windows
         COM32 chain.c32
         APPEND hd0 3
...

```

`hd0 3` representa la tercera partición del primer disco identificado en la BIOS —advierta que, las unidades se cuentan desde cero, pero las particiones se cuentan desde uno—.

**Nota:** En Windows, esto omite el propio gestor de arranque del sistema, (`bootmgr`), que es requerido por algunas actualizaciones importantes ([eg.](http://support.microsoft.com/kb/2883200)) para completar. En tales casos, puede ser aconsejable establecer temporalmente el flag boot del MBR en la partición de Windows (por ejemplo, con [GParted](/index.php/GParted "GParted")), dejando la actualización al finalizar la instalación, y restableciendo luego el flag a la partición syslinux (por ejemplo, desde el propio Windows con [DiskPart](http://www.online-tech-tips.com/computer-tips/set-active-partition-vista-xp)).

Si no está seguro de qué unidad se identifica como la primera de su BIOS, puede utilizar el identificador MBR, o, si utiliza GPT, la etiqueta del sistema de archivos. Para conocer el identificador de MBR, utilice la orden:

 `# fdisk -l /dev/sdb` 
```
 Disk /dev/sdb: 128.0 GB, 128035676160 bytes 
 255 heads, 63 sectors/track, 15566 cylinders, total 250069680 sectors
 Units = sectors of 1 * 512 = 512 bytes
 Sector size (logical/physical): 512 bytes / 512 bytes
 I/O size (minimum/optimal): 512 bytes / 512 bytes
 Disk identifier: 0xf00f1fd3

 Device Boot      Start         End      Blocks   Id  System
 /dev/sdb1            2048     4196351     2097152    7  HPFS/NTFS/exFAT
 /dev/sdb2         4196352   250066943   122935296    7  HPFS/NTFS/exFAT

```

reemplazando `/dev/sdb` con la unidad que desea cargar en cadena. Utilizando el número hexadecimal de Disk identifier: `0xf00f1fd3` en este caso, la sintaxis en `syslinux.cfg` sería:

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL windows
         MENU LABEL Windows
         COM32 chain.c32
         APPEND mbr:0xf00f1fd3
...

```

Para más información sobre chainloading, consulte [la wiki de Syslinux](http://www.syslinux.org/wiki/index.php/Comboot/chain.c32).

Si tiene [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") instalado en la misma partición, se puede cargar en cadena utilizando:

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL grub2
        MENU LABEL Grub2
        COM32 chain.c32
        append file=../grub/boot.img
...

```

Esto puede ser necesario para el arranque a partir de imágenes ISO.

### Chainloading de otros sistemas Linux

Al hacer el chainloading de un gestor de arranque como el de Windows, no hay ningún problema, ya que cuenta con un gestor de arranque para empezar, mientras Syslinux sea capaz de cargar archivos que residan en la misma partición del archivo de configuración. Por lo tanto, si usted tiene otra versión de Linux instalada en una partición diferente y sin `/boot` compartida, debe utilizar Extlinux. En pocas palabras, se puede instalar este último en el superbloque de la partición para poder ser llamado por Syslinux instalado en el MBR. Extlinux es parte del proyecto Syslinux y está incluida en el paquete [syslinux](https://www.archlinux.org/packages/?name=syslinux).

Las instrucciones siguientes presuponen que ya ha instalado Syslinux. Estas instruccións también presumen la típica configuración de Arch Linux de que se está utilizando la ruta de acceso a `/boot/syslinux` y que el chainloaded `/` está en `/dev/sda3`.

Una vez que arranque Linux (la distribución que Syslinux inicia por defecto), se monta otra partición root de la otra distribución en un punto de montaje que desee. En este ejemplo vamos a usar `/mnt`. Tenga en cuenta que si utiliza una partición /boot separada será necesario montarla: El ejemplo supone que ésta es `/dev/sda2`.

```
# mount /dev/sda3 /mnt
# mount /dev/sda2 /mnt/boot (only necessary for separate /boot)

```

Instale extlinux y copie los archivos *.c32 necesarios:

```
# extlinux -i /mnt/boot/syslinux
# cp /usr/lib/syslinux/{chain,menu}.c32 /mnt/boot/syslinux

```

Crearemos `/mnt/boot/syslinux/syslinux.cfg` como sigue:

```
/boot/syslinux/syslinux.cfg **on /dev/sda3**

```

```
timeout 10

ui menu.c32

label Other Linux
    linux /boot/vmlinuz-linux
    initrd /boot/initramfs-linux.img
    append root=/dev/sda3 rw quiet

label MAIN
    com32 chain.c32
    append hd0 0

```

Tratado en la [página de usuario](/index.php/User:Djgera "User:Djgera") de Djgera.

### Usar memtest

Instale [memtest+](https://www.archlinux.org/packages/?name=memtest%2B) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Use la sección`LABEL` para lanzar [memtest](https://en.wikipedia.org/wiki/es:Memtest86%2B "wikipedia:es:Memtest86+"):

 `/boot/syslinux/syslinux.cfg` 
```
...
 LABEL memtest
         MENU LABEL Memtest86+
         LINUX ../memtest86+/memtest.bin
...

```

### HDT

[HDT (Hardware Detection Tool)](http://hdt-project.org/) es un instrumento para visualizar información sobre el hardware. Como siempre, el archivo `.c32` debe ser copiado o debe crearse un enlace simbólico en `/boot/syslinux/`. Para obtener información del dispositivo PCI, o bien copie, o bien cree un enlace simbólico, de `/usr/share/hwdata/pci.ids` a `/boot/syslinux/pci.ids` y añada lo siguiente al archivo de configuración:

 `/boot/syslinux/syslinux.cfg` 
```
 LABEL hdt
         MENU LABEL Hardware Info
         COM32 hdt.c32

```

### Reinicio y apagado

Use la siguiente sección para reiniciar o apagar su equipo:

 `/boot/syslinux/syslinux.cfg` 
```
 LABEL reboot
         MENU LABEL Reboot
         COM32 reboot.c32

 LABEL poweroff
         MENU LABEL Power Off
         COMBOOT poweroff.com

```

### Limpiar el menú

Para borrar la pantalla al salir del menú, añada la siguiente línea:

 `/boot/syslinux/syslinux.cfg` 
```
 MENU CLEAR

```

### Distribución del teclado

Si tiene que editar a menudo sus parámetros de arranque, es posible que desee volver a asignar la distribución del teclado. Esto le permite introducir caracteres como «=», «/» y otros caracteres fácilmente con un teclado no americano.

Primero tiene que crear una distribución de teclado compatible (por ejemplo, con uno español):

**Nota:** `us.kmap` necesita ser creado o no funcionará.

```
$ cp /usr/share/kbd/keymaps/i386/qwertz/es.map.gz .
$ cp /usr/share/kbd/keymaps/i386/qwerty/us.map.gz .
$ gunzip es.map.gz
$ gunzip us.map.gz
$ mv es.map es.kmap
$ mv us.map us.kmap
# keytab-lilo es > es.ktl

```

Con privilegios root, copie `es.ktl` a `/boot/syslinux/` y establezca como propietario a root:

```
# chown root:root /boot/syslinux/es.ktl

```

Ahora edite `syslinux.conf` y añada:

 `/boot/syslinux/syslinux.cfg` 
```
 KBDMAP es.ktl

```

### Ocultar el menú

Utilice la opción:

 `/boot/syslinux/syslinux.cfg` 
```
 MENU HIDDEN

```

para ocultar el menú mientras se muestra sólo el tiempo de espera. Presione cualquier tecla para que aparezca el menú.

### Pxelinux

**Nota:** Pare UEFI, Syslinux utiliza el mismo binario para el arranque del disco y para el arranque a través de red. Para cargar archivos de TFTP u otros protocolos de red se requerirá arrancar Syslinux en modo red.

**PXELINUX** es propocionado por [syslinux](https://www.archlinux.org/packages/?name=syslinux).

Copie el gestor de arranque `{l,}pxelinux.0` (proporcionado por el paquete syslinux) al directorio boot del cliente. Para la versión 5.00 y posteriores, también copie `ldlinux.c32` del mismo paquete:

```
# cp /usr/lib/syslinux/bios/pxelinux.0 "$root/boot"
# cp /usr/lib/syslinux/bios/ldlinux.c32 "$root/boot"
# mkdir "$root/boot/pxelinux.cfg"

```

También crearemos el directorio `pxelinux.cfg`, que es donde pxelinux buscará los archivos de configuración por defecto. Dado que no se intanta hacer distinciones entre distintos MAC de varios equipos, se creará el archivo de configuración `default`.

 `# vim "$root/boot/pxelinux.cfg/default"` 
```
default linux

label linux
kernel vmlinuz-linux
append initrd=initramfs-linux.img quiet ip=:::::eth0:dhcp nfsroot=10.0.0.1:/arch

```

O, si se está usando NBD, utilice la siguiente línea append :

 `append ro initrd=initramfs-linux.img ip=:::::eth0:dhcp nbd_host=10.0.0.1 nbd_name=arch root=/dev/nbd0` 
**Nota:** Tendrá que cambiar `nbd_host` y/o `nfsroot`, respectivamente, para que coincida con la configuración de red (la dirección del servidor NFS/NBD)

La sintaxis de configuración pxelinux es idéntica a syslinux; consulte la documentación de los desarrolladores para obtener más información .

E kernel e initramfs serán transferidos vía TFTP, por lo que las rutas serán las relativas al root del servitor TFTP. En otro caso, el sistema de archivos root puede ser el propio del montado mediante NFS, en cuyo caso la ruta será la relativa al root del servidor NFS.

Para cargar pxelinux, sustituya `filename "/grub/i386-pc/core.0";` en `/etc/dhcpd.conf` con `filename "/pxelinux.0"`

### Arrancar una imágen ISO9660 con memdisk

Syslinux permite arrancar imágenes ISO directamente con el módulo [memdisk](http://www.syslinux.org/wiki/index.php/MEMDISK), véase [Multiboot USB drive#Using Syslinux and memdisk](/index.php/Multiboot_USB_drive#Using_Syslinux_and_memdisk "Multiboot USB drive") para obtener ejemplos.

## Solución de Problemas

### Utilizar el prompt de Syslinux

Es posible escribir el valor del parámetro `LABEL` correspondiente al sistema operativo que se quiere ejecutar (según su `syslinux.cfg`). Si ha usado la configuración de ejemplo, escriba:

```
boot: arch

```

Si se obtiene un error al cargar el archivo de configuración, es posible pasar manualmente el parámetro del boot, por ejemplo:

```
boot: ../vmlinuz-linux root=/dev/sda2 ro initrd=../initramfs-linux.img

```

Si no se tiene acceso a `boot:` en ramfs, y cuando sea incapaz temporalmente de arrancar el kernel, prosiga como sigue:

	1\. Cree un directorio temporal, donde montar la partición root (si no existe ya):

```
 # mkdir -p /new_root

```

	2\. Monte `/` en `/new_root` (en el caso de que `/boot/` esté en una partición separada, tendrá que montar ambas):

**Nota:** Si `/boot` está en una partición ext2 entonces busybox no se puede montar.

```
 # mount /dev/sd[a-z][1-9] /new_root

```

	3\. Use `vim` y modifique `syslinux.cfg` de acuerdo a sus necesidades y guarde el archivo.

	4\. Reinicie.

### Fallo de fsck en la partición root

En el caso de una eventual partición root gravemente dañada (con el journal dañado), abra la shell de emergencia de Syslinux y monte el sistema de archivo root:

```
# mount /dev/root partition /new_root

```

Y obtenga el ejecutable tune2fs binary que se encuentra en la partición root partition (el cual no está incluido en Syslinux):

```
# cp /new_root/sbin/tune2fs /sbin/

```

Siga con las instrucciones descritas en [ext2fs: no external journal](/index.php/Fsck#ext2fs_:_no_external_journal "Fsck") para crear un journal nuevo para la partición root.

### Default o UI no encontrado en su equipo

Algunos fabricantes de placas madre no proporcionan buena compatibilidad para arrancar desde dispositivos USB u otros. Mientras que una unidad USB con formato ext4 puede permitir el arranque en un equipo más reciente, algunos equipos antiguos pueden bloquearse si la partición de arranque que contiene el *kernel* y el *initrd* no está en una partición FAT16\. Para evitar que una máquina antigua cargándose con `ldlinux` falle al leer `syslinux.cfg`, use `cfdisk` para crear una partición FAT16 (<= 2GB) y formatearla usando [dosfstools](https://www.archlinux.org/packages/?name=dosfstools):

```
# mkfs.msdos -F 16 /dev/sda1

```

a continuación, instale y configure Syslinux.

### Missing operating system

Si aparece este mensaje, compruebe si la partición que contiene `/boot` tiene el flag de arranque habilitado. Si el flag está activado, entonces, tal vez, esta partición comienza en el sector 1 en vez del 63 o 2048\. Compruebe esta circunstancia con `fdisk -l`. Si se inicia en el sector 1, se puede mover la partición(s) con `gparted` desde un disco de rescate. O bien, si tiene una partición boot separada, puede hacer una copia de seguridad de `/boot` con:

```
# cp -a /boot /boot.bak

```

y luego arrancar con el disco de instalación de Arch. A continuación, use `cfdisk` para borrar la partición `/boot`, y volver a crearla. Esta vez se debe comenzar en el sector adecuado, **63**. Ahora monte sus particiones y efectue un `chroot` en el sistema montado, como se describe en la Beginners guide (guía de principiantes). Restaure `/boot` con la orden:

```
# cp -a /boot.bak/* /boot

```

Compruebe que `/etc/fstab` es correcto. Entonces, ejecute:

```
# syslinux-install_update -iam

```

y reinicie.

También recibirá este error si está tratando de arrancar desde una matriz [RAID](/index.php/RAID "RAID") md 1 creada con una versión de los metadatos no soportada por Syslinux. A partir de agosto de 2013 mdadm creará, de forma predeterminada, una matriz con la versión 1.2 de los metadatos, pero Syslinux tan solo soporta la versión 1.0\. Si este es el caso, tendrá que volver a crear su matriz [RAID](/index.php/RAID "RAID") pasando la opción `--metadata=1.0` para mdadm.

### ¡Se inicia Windows en vez de Syslinux!

**Solución:** Asegúrese de que la partición que contiene `/boot` tiene el indicador (flag) boot activo. También, asegúrese de que el indicador boot no está activado en la partición de Windows. Consulte la sección de instalación anterior.

El MBR que viene con Syslinux busca la primera partición activa que tiene el flag boot habilitado. Es probable que Syslinux encontrase primero la partición de Windows y que la misma tuviese el flag boot activo. Si lo desea, es posible utilizar tambien el MBR porporcionado por Windows o MS-DOS `fdisk`.

### Entradas del menú sin ningún efecto

Si se selecciona una entrada del menú de arranque y no sucede nada, tan solo «refresque» el menú, probablemente signifique que tiene un error en el archivo `syslinux.cfg`. Presione `Tab` y modifique los parámetros del arranque. Alternativamente, pulse `Esc` y escriba en el `LABEL` de su entrada de arranque (por ejemplo, *arch*). Otra causa podría ser que no se tiene un kernel instalado. Encuentre una manera de acceder a su sistema de archivos (a través de live CD, etc.) y asegúrese de que existe `/mount/vmlinuz-linux` y no tiene un tamaño de 0\. Si este es el caso, [reinstale su kernel](/index.php/Kernel_Panics#Option_2:_Reinstall_kernel "Kernel Panics").

### Imposible eliminar ldlinux.sys

El archivo `ldlinux.sys` tiene establecido el atributo de inmutable, para prevenir que pueda ser borrado o sobrescrito. Esto implica que el sector en el que reside el archivo en cuestión no debe cambiar, de lo contrario Syslinux tendrá que ser reinstalado. Para ello tendrá que eliminarlo, ejecutando las siguientes órdenes:

```
# chattr -i /boot/syslinux/ldlinux.sys
# rm /boot/syslinux/ldlinux.sys

```

### Se visualiza un cuadrado blanco en el ángulo superior izquierdo cuando se utiliza vesamenu

Problemas: *A partir de linux-3.0, el controlador de modesetting trata de mantener el contenido actual de la pantalla después de cambiar la resolución (por lo menos, lo hace con mi Intel, al tener Syslinux en modo texto). Parece que esto va mal cuando se combina con el módulo vesamenu en Syslinux (el bloque blanco es, en realidad, un intento de mantener el menú de Syslinux, pero el controlador no logra captar la imagen de la modalidad gráfica vesa).*

Si tiene una resolución personalizada y se utiliza `vesamenu` junto con modesetting, pruebe insertando lo siguiente en `syslinux.cfg` para remover el bloque blanco y continuar el arranque en modo gráfico:

```
APPEND root=/dev/sda6 ro 5 **vga=current** quiet splash

```

### Cargar Windows no funciona, cuando se instala en otra unidad

Si Windows está instalado en una unidad diferente a la de Arch y tiene problemas para cargarlo, pruebe la siguiente configuración:

```
LABEL Windows
       MENU LABEL Windows
       COM32 chain.c32
       APPEND mbr:0xdfc1ba9e swap

```

sustituya el código mbr con el de la unidad de windows (puede ver cómo [más arriba](#Chainloading)), y añada `swap` a las opciones.

### Leer el registro del gestor de arranque

En algunos casos, por ejemplo, el gestor de arranque no puede arrancar el kernel, es muy conveniente obtener más información sobre el proceso de arranque. *Syslinux* vuelca mensajes de error en la pantalla, pero sobrescribe rápidamente el texto. Para evitar la pérdida de la información del registro hay que desactivar `menu UI` en `syslinux.cfg` y utilizar "command-line" por defecto del prompt. Esto implica:

*   evitar la directiva UI
*   evitar ONTIMEOUT
*   evitar ONERROR
*   evitar MENU CLEAR
*   utilizar un TIMEOUT superior
*   utilizar PROMPT 1
*   utilizar DEFAULT <etiqueta_problemática>

Para obtener un registro más detallado de depuración de errores se necesita recompilar el paquete [syslinux](https://www.archlinux.org/packages/?name=syslinux) con la adición de CFLAGS:

## Véase también

*   [Official website](http://www.syslinux.org)
*   [PXELinux configuration](http://www.josephn.net/scrapbook/pxelinux_stuff)
*   [Multiboot USB using Syslinux](http://blog.jak.me/2013/01/03/creating-a-multiboot-usb-stick-using-syslinux/)