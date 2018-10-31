**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

[Cifrar dispositivo](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol) "Dm-crypt/Device encryption (Español)") – [Preparar dispositivo](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – <a class="mw-selflink selflink">Cifrar un sistema completo</a> – [Montar y acceder](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)") – [Especialidades](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol) "Dm-crypt/Specialties (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)") – [Configurar el sistema](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"), revisada por última vez el **2018-10-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_an_entire_system&diff=0&oldid=543729) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Los siguientes son ejemplos de escenarios comunes en el cifrado completo de un sistema con *dm-crypt*. Se explican todas las adaptaciones que se necesitan introducir en el [proceso de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"). Todas las herramientas necesarias para ello están presentes en la [imagen de instalación](https://www.archlinux.org/download/).

## Contents

*   [1 Descripción general](#Descripci.C3.B3n_general)
*   [2 Esquema de particionado simple con LUKS](#Esquema_de_particionado_simple_con_LUKS)
    *   [2.1 Preparar el disco](#Preparar_el_disco)
    *   [2.2 Preparar las particiones que no son de arranque (boot)](#Preparar_las_particiones_que_no_son_de_arranque_.28boot.29)
    *   [2.3 Preparar la partición de arranque](#Preparar_la_partici.C3.B3n_de_arranque)
    *   [2.4 Montar los dispositivos](#Montar_los_dispositivos)
    *   [2.5 Configurar mkinitcpio](#Configurar_mkinitcpio)
    *   [2.6 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque)
*   [3 LVM sobre LUKS](#LVM_sobre_LUKS)
    *   [3.1 Preparar el disco](#Preparar_el_disco_2)
    *   [3.2 Preparar los volúmenes lógicos](#Preparar_los_vol.C3.BAmenes_l.C3.B3gicos)
    *   [3.3 Preparar la partición de arranque](#Preparar_la_partici.C3.B3n_de_arranque_2)
    *   [3.4 Configurar mkinitcpio](#Configurar_mkinitcpio_2)
    *   [3.5 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_2)
*   [4 LUKS sobre LVM](#LUKS_sobre_LVM)
    *   [4.1 Preparar el disco](#Preparar_el_disco_3)
    *   [4.2 Preparar los volúmenes lógicos](#Preparar_los_vol.C3.BAmenes_l.C3.B3gicos_2)
    *   [4.3 Preparar la partición de arranque](#Preparar_la_partici.C3.B3n_de_arranque_3)
    *   [4.4 Configurar mkinitcpio](#Configurar_mkinitcpio_3)
    *   [4.5 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_3)
    *   [4.6 Configurar fstab y crypttab](#Configurar_fstab_y_crypttab)
    *   [4.7 Cifrar el volúmen lógico /home](#Cifrar_el_vol.C3.BAmen_l.C3.B3gico_.2Fhome)
*   [5 LUKS sobre RAID por software](#LUKS_sobre_RAID_por_software)
    *   [5.1 Preparar los discos](#Preparar_los_discos)
    *   [5.2 Compilar la matriz RAID](#Compilar_la_matriz_RAID)
    *   [5.3 Preparar los dispositivos de bloque](#Preparar_los_dispositivos_de_bloque)
    *   [5.4 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_4)
    *   [5.5 Crear los archivos de claves](#Crear_los_archivos_de_claves)
    *   [5.6 Configurar el sistema](#Configurar_el_sistema)
*   [6 Modalidad plain de dm-crypt](#Modalidad_plain_de_dm-crypt)
    *   [6.1 Preparar el disco](#Preparar_el_disco_4)
    *   [6.2 Preparar las particiones que no son de arranque (boot)](#Preparar_las_particiones_que_no_son_de_arranque_.28boot.29_2)
    *   [6.3 Preparar la partición de arranque](#Preparar_la_partici.C3.B3n_de_arranque_4)
    *   [6.4 Configurar mkinitcpio](#Configurar_mkinitcpio_4)
    *   [6.5 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_5)
    *   [6.6 Posinstalación](#Posinstalaci.C3.B3n)
*   [7 Cifrar partición de arranque (GRUB)](#Cifrar_partici.C3.B3n_de_arranque_.28GRUB.29)
    *   [7.1 Preparar el disco](#Preparar_el_disco_5)
    *   [7.2 Preparar los volúmenes lógicos](#Preparar_los_vol.C3.BAmenes_l.C3.B3gicos_3)
    *   [7.3 Preparar la partición de arranque](#Preparar_la_partici.C3.B3n_de_arranque_5)
    *   [7.4 Configurar mkinitcpio](#Configurar_mkinitcpio_5)
    *   [7.5 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_6)
    *   [7.6 Configurar fstab y crypttab](#Configurar_fstab_y_crypttab_2)
*   [8 Subvolúmenes btrfs con espacio de intercambio](#Subvol.C3.BAmenes_btrfs_con_espacio_de_intercambio)
    *   [8.1 Preparar el disco](#Preparar_el_disco_6)
    *   [8.2 Preparar la partición del sistema](#Preparar_la_partici.C3.B3n_del_sistema)
        *   [8.2.1 Crear contenedor LUKS](#Crear_contenedor_LUKS)
        *   [8.2.2 Desbloquear el contenedor LUKS](#Desbloquear_el_contenedor_LUKS)
        *   [8.2.3 Formatear el dispositivo mapeado](#Formatear_el_dispositivo_mapeado)
        *   [8.2.4 Montar el dispositivo mapeado](#Montar_el_dispositivo_mapeado)
    *   [8.3 Crear subvolúmenes btrfs](#Crear_subvol.C3.BAmenes_btrfs)
        *   [8.3.1 Esquema](#Esquema)
        *   [8.3.2 Crear subvolumenes de nivel superior](#Crear_subvolumenes_de_nivel_superior)
        *   [8.3.3 Montar subvolúmenes de nivel superior](#Montar_subvol.C3.BAmenes_de_nivel_superior)
        *   [8.3.4 Crear subvolúmenes anidados](#Crear_subvol.C3.BAmenes_anidados)
        *   [8.3.5 Montar ESP](#Montar_ESP)
    *   [8.4 Configurar mkinitcpio](#Configurar_mkinitcpio_6)
        *   [8.4.1 Crear archivo de claves](#Crear_archivo_de_claves)
        *   [8.4.2 Editar mkinitcpio.conf](#Editar_mkinitcpio.conf)
    *   [8.5 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_7)
    *   [8.6 Configurar el espacio de intercambio](#Configurar_el_espacio_de_intercambio)

## Descripción general

Asegurar un sistema de archivos raíz es donde *dm-crypt* sobresale, en cuanto a características y rendimiento. Cuando el sistema de archivos de un sistema (raíz) está en un dispositivo dm-crypt, prácticamente todos los archivos del sistema están cifrados. A diferencia del cifrado de forma selectiva de los sistemas de archivos no raíz, un sistema de archivos raíz cifrado puede ocultar información, tales como qué programas se instalan, los nombres de los usuarios y todas sus cuentas, y los vectores de vuelcos de datos comunes, tales como [mlocate (Español)](/index.php/Mlocate_(Espa%C3%B1ol) "Mlocate (Español)") y `/var/log/`. Además, un sistema de archivos raíz cifrado hace que la manipulación del sistema sea mucho más difícil, al estar todo cifrado, con las excepciones del [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") y (normalmente) el kernel.

En la siguiente tabla se ilustran las ventajas de todos los escenarios posibles, diferenciando los pros y contras de cada uno:

| Escenarios | Ventajas | Desventajas |
| [#Esquema de particionado simple con LUKS](#Esquema_de_particionado_simple_con_LUKS)

muestra una configuración sencilla y básica de una partición raíz completamente cifrada con LUKS.

 | 

*   Particionado y configuración sencilla

 | 

*   Rigidez; el espacio del disco a cifrar debe estar preasignado

 |
| [#LVM sobre LUKS](#LVM_sobre_LUKS)

logra un particionado flexible usando LVM dentro de una única partición cifrada con LUKS.

 | 

*   Particionado sencillo con la ductilidad de LVM
*   Solo es necesaria una clave para desbloquear todos los volúmenes (por ejemplo, configuración fácil para restaurar desde disco)
*   El esquema del volumen no es transparente cuando está bloqueado
*   El método más fácil para permitir la [suspensión en el disco](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption")

 | 

*   LVM añade una capa y un hook adicional de mapeo
*   Poco útil si un volumen particular necesita una clave separada

 |
| [#LUKS sobre LVM](#LUKS_sobre_LVM)

utiliza dm-crypt solo después de configurar LVM.

 | 

*   LVM puede utilizarse para tener cifrado volúmenes que abarquen varios discos
*   Facilidad para mezclar grupos de volúmenes cifrados/descifrados

 | 

*   Complejo; cambiar volúmenes requiere cambiar demasiados mapeados cifrados
*   Los volúmenes requieren claves propias cada uno
*   El esquema LVM es transparente cuando está bloqueado

 |
| [#LUKS sobre RAID por software](#LUKS_sobre_RAID_por_software)

utiliza dm-crypt solo después de configurar RAID.

 | 

*   Similar a [#LUKS sobre LVM](#LUKS_sobre_LVM)

 | 

*   Similar a [#LUKS sobre LVM](#LUKS_sobre_LVM)

 |
| [#Plain dm-crypt](#Plain_dm-crypt)

utiliza la modalidad plain de dm-crypt, es decir, sin una cabecera LUKS y sus opciones para múltiples claves.
Este escenario también permite emplear dispositivos USB para `/boot` y almacenamiento de claves, que se puede aplicar a los otros escenarios.

 | 

*   Capacidad de recuperación de los datos para los casos en que pueda dañarse un encabezado LUKS
*   Permite el [cifrado completo de disco](https://en.wikipedia.org/wiki/es:Cifrado_de_disco#Completo_cifrado_de_disco "wikipedia:es:Cifrado de disco")
*   Ayuda a abordar [problemas](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") con unidades SSD

 | 

*   Es necesaria una alta competencia en todos los parámetros de cifrado
*   Clave de cifrado única y sin opción de cambiarla

 |
| [#Cifrar partición de arranque (GRUB)](#Cifrar_partici.C3.B3n_de_arranque_.28GRUB.29)

muestra cómo cifrar la partición de arranque utilizando el gestor de arranque GRUB.
Este escenario también emplea una partición ESP, que se puede aplicar a los otros escenarios.

 | 

*   Las mismas ventajas que las descritas para el escenario de la instalación basada en LVM sobre LUKS (para este ejemplo en particular)
*   Se dejan menos datos sin cifrar, es decir, el gestor de arranque y la partición ESP, si está presente

 | 

*   Las mismas desventajas que las descritas para el escenario de la instalación basada en LVM sobre LUKS (para este ejemplo en particular)
*   Configuración más complicada
*   No es compatible con otros gestores de arranque

 |
| [#Subvolúmenes btrfs con espacio de intercambio](#Subvol.C3.BAmenes_btrfs_con_espacio_de_intercambio)

muestra cómo cifrar un sistema [Btrfs](/index.php/Btrfs "Btrfs"), incluyendo el directorio `/boot`, también agrega una partición de intercambio, en el hardware UEFI.

 | 

*   Ventajas similares a [#Cifrar partición de arranque (GRUB)](#Cifrar_partici.C3.B3n_de_arranque_.28GRUB.29)
*   Disponibilidad de las características de Btrfs

 | 

*   Desventajas similares a [#Cifrar partición de arranque (GRUB)](#Cifrar_partici.C3.B3n_de_arranque_.28GRUB.29)

 |

Si bien todos los escenarios anteriores proporcionan una protección mucho mayor contra las amenazas externas que los sistemas de archivos cifrados secundariamente, también comparten una desventaja común: cualquier usuario en posesión de la clave de cifrado puede descifrar toda la unidad y, por lo tanto, puede acceder a los datos de otros usuarios. Si esto es motivo de preocupación, es posible utilizar una combinación de cifrado de dispositivos de bloques y sistema de archivos apilados, y recoger las ventajas de ambos. Véase [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)") para planificar las opciones.

Véase [Dm-crypt/Drive preparation (Español)#Particionar](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol)#Particionar "Dm-crypt/Drive preparation (Español)") para tener una visión general de las estrategias de particionado utilizados en los escenarios.

Otra área a considerar es si se debe configurar una partición de intercambio cifrado y de qué tipo. Véase [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") para conocer alternativas.

Si quiere avanzar en la protección de los datos del sistema no solo contra el robo físico, sino también previniéndose contra la manipulación lógica, vea [Dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties") para conocer más posibilidades después de seguir uno de los escenarios.

Para [solid state drives](/index.php/Solid_state_drive "Solid state drive") es posible que desee considerar activar la compatibilidad con TRIM, pero tenga en cuenta que existen posibles implicaciones de seguridad. Consulte [dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") para obtener más información.

**Advertencia:** En cualquier situación, nunca utilice software de reparación del sistema de archivos como [fsck](/index.php/Fsck "Fsck") directamente sobre un volumen cifrado, o destruirá cualquier medio para recuperar la clave utilizada para descifrar sus archivos. En su lugar, utilice estas herramientas en el dispositivo una vez desencriptado (abierto).

## Esquema de particionado simple con LUKS

Este ejemplo explica cómo cifrar un sistema completo con *dmcrypt* + LUKS en un esquema de particionado simple:

```
 +----------------------+--------------------------+-------------------------------+
 | Partición de arranque| Partición del sistema    |Espacio libre opcional         |
 |                      | cifrada con LUKS         |para configurar posteriormente |
 |                      |                          |particiones de intercambio     |
 | /boot                | /                        |o particiones adicionales      |
 |                      |                          |                               |
 |                      | /dev/mapper/cryptroot    |                               |
 |                      |--------------------------|                               |
 | /dev/sda1            | /dev/sda2                |                               |
 +----------------------+--------------------------+-------------------------------+

```

Los primeros pasos se pueden realizar directamente después de arrancar la imagen de instalación de Arch Linux.

### Preparar el disco

Antes de crear las particiones, debe informarse sobre la importancia y los métodos para borrar de forma segura el disco, descrito en [Dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)").

A continuación, cree las particiones necesarias, al menos una para `/` (por ejemplo, `/dev/sda2`) y otra para `/boot` (`/dev/sda1`). Véase [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)").

### Preparar las particiones que no son de arranque (boot)

Las siguientes órdenes crean y montan la partición raíz cifrada. Se corresponden con el proceso descrito con detalle en [Dm-crypt/Encrypting a non-root file system (Español)#Partición](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol)#Partici.C3.B3n "Dm-crypt/Encrypting a non-root file system (Español)") (que, a pesar del título, *se puede* aplicar a particiones raíz, siempre y cuando [mkinitcpio](#Configurar_mkinitcpio) y el [gestor de arranque](#Configurar_el_gestor_de_arranque) estén configurados correctamente). Si desea utilizar determinadas opciones de cifrado no predeterminadas (por ejemplo, respecto al algoritmo de cifrado, longitud de la clave, etc.), consulte [opciones de cifrado](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de ejecutar la primera orden:

```
# cryptsetup -y -v luksFormat --type luks2 /dev/sda2
# cryptsetup open /dev/sda2 cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Compruebe que el mapeado funciona según lo previsto:

```
# umount /mnt
# cryptsetup close cryptroot
# cryptsetup open /dev/sda2 cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Si ha creado particiones separadas (por ejemplo, `/home`), estos pasos tienen que ser adaptados y repetidos para todas ellas, a *excepción* de `/boot`. Véase [dm-crypt/Encrypting a non-root file system (Español)#Desbloqueo y montaje automatizados](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol)#Desbloqueo_y_montaje_automatizados "Dm-crypt/Encrypting a non-root file system (Español)") para saber cómo manejar particiones adicionales en el arranque.

Tenga en cuenta que cada dispositivo de bloque requiere su propia contraseña. Esto puede ser un inconveniente, porque da lugar a una frase de acceso separada para cada uno, que hay que introducir durante el inicio. Una alternativa es utilizar un archivo de claves almacenada en la partición del sistema para desbloquear la partición separada mediante `crypttab`. Vease [Dm-crypt/Device encryption#Using LUKS to format partitions with a keyfile](/index.php/Dm-crypt/Device_encryption#Using_LUKS_to_format_partitions_with_a_keyfile "Dm-crypt/Device encryption") para obtener instrucciones.

### Preparar la partición de arranque

Lo que tiene que hacer es configurar la partición `/boot` sin cifrar, que se necesita para una partición raíz cifrada. Para una partición estándar `/boot` [MBR/no-EFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), por ejemplo, ejecute:

```
# mkfs.ext4 /dev/sda1
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

### Montar los dispositivos

Como en [Installation guide (Español)#Montar las particiones](/index.php/Installation_guide_(Espa%C3%B1ol)#Montar_las_particiones "Installation guide (Español)"), hay que montar los dispositivos mapeados, no las particiones subyacentes. En cambio `/boot`, al no estar cifrado, se monta directamente como de costumbre.

### Configurar mkinitcpio

Añada los hooks `keyboard`, `keymap` y `encrypt` a [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"). Si la distribución de teclado predeterminado de EE.UU. está bien para usted, puede omitir el hook `keymap` .

```
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt** filesystems fsck)

```

Si utiliza el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") con initramfs basado en systemd, en su lugar debe establecerse lo siguiente:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** filesystems fsck)

```

Dependiendo de qué otros hooks se utilicen, el orden de los mismos puede ser relevante. Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que pueda necesitar.

### Configurar el gestor de arranque

Con el fin de desbloquear en el arranque la partición raíz cifrada, es necesario pasar los siguientes parámetros del kernel al gestor de arranque:

```
cryptdevice=UUID=device-UUID:cryptroot root=/dev/mapper/cryptroot

```

Si utiliza el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") con initramfs basado en systemd, en su lugar debe establecerse lo siguiente:

```
rd.luks.name=*device-UUID*=cryptroot root=/dev/mapper/cryptroot

```

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para conocer más detalles.

El `*device-UUID*` se está refiriendo al UUID de `/dev/sda2`. Véase [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") para conocer más detalles.

## LVM sobre LUKS

El método sencillo es crear [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") sobre la partición cifrada y no al revés. Técnicamente, LVM se configura sobre un gran dispositivo cifrado. Por lo tanto, LVM no es transparente hasta que el dispositivo de bloque se desbloquea y la estructura del volumen subyacente se escanea y se monta durante el arranque.

El esquema de particionado del disco en este ejemplo sería:

```

+-----------------------------------------------------------------------+ +-----------------------+
| Volumen lógico 1      | Volumen lógico 2      | Volumen lógico 3      | | Partición de arranque |     
|                       |                       |                       | |                       |
| [SWAP]                | /                     | /home                 | | /boot                 |
|                       |                       |                       | |                       |
| /dev/MyVolGroup/swap  | /dev/MyVolGroup/root  | /dev/MyVolGroup/home  | |                       |
|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _| | (puede estar en otro  |
|                                                                       | | dispositivo)          |
|                         Partición cifrada con LUKS                    | |                       |
|                           /dev/sda1                                   | | /dev/sdb1             |
+-----------------------------------------------------------------------+ +-----------------------+

```

**Nota:** Al usar el hook `encrypt` este método no le permite abarcar los volúmenes lógicos en varios discos; use [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") o vea [dm-crypt/Specialties#Modifying the encrypt hook for multiple partitions](/index.php/Dm-crypt/Specialties#Modifying_the_encrypt_hook_for_multiple_partitions "Dm-crypt/Specialties").

**Sugerencia:** Existen tres variantes de esta configuración:

*   Las instrucciones de [Dm-crypt/Specialties#Encrypted system using a detached LUKS header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") utilizan esta configuración con un encabezado LUKS remoto sobre un dispositivo USB para lograr una autenticación de dos factores con él.
*   Las instrucciones del [blog de Pavel Kogan](https://web.archive.org/web/20180103175714/http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/) muestran cómo encriptar la partición `/boot` mientras se mantiene en la partición LUKS principal cuando se usa GRUB.
*   Las instrucciones de [dm-crypt/Specialties#Encrypted /boot and a detached LUKS header on USB](/index.php/Dm-crypt/Specialties#Encrypted_.2Fboot_and_a_detached_LUKS_header_on_USB "Dm-crypt/Specialties") usan esta configuración con un encabezado LUKS separado, una partición `/boot` cifrada y un archivo de clave encriptado todo en un dispositivo USB.

### Preparar el disco

Antes de crear las particiones, debe informarse sobre la importancia y los métodos sobre cómo borrar de forma segura el disco, descrito en [Dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)").

**Sugerencia:** Cuando se utiliza el gestor de arranque [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") junto con [GPT](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)"), debe crear una partición [BIOS boot partition](/index.php/GRUB_(Espa%C3%B1ol)#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29 "GRUB (Español)").

Cree una partición con punto de montaje en `/boot`, del tipo `8300`, con un tamaño de 200 MiB o más.

Cree otra partición del tipo `8E00`, en la que luego residirá el contenedor cifrado.

Cree un contenedor cifrado con LUKS en la partición del «sistema». Introduzca la contraseña elegida dos veces.

```
# cryptsetup luksFormat --type luks2 /dev/sda1

```

Para obtener más información sobre las opciones disponibles de cryptsetup vea las [opciones de cifrado de LUKS](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de ejecutar la orden de arriba.

Abra el contenedor:

```
# cryptsetup open --type luks /dev/*sdaX* lvm

```

El contenedor descifrado estará ahora disponible como `/dev/mapper/lvm`.

### Preparar los volúmenes lógicos

Cree un volumen físico sobre el contenedor LUKS abierto:

```
# pvcreate /dev/mapper/cryptlvm

```

Cree un grupo de volúmenes llamado (por ejemplo) `MyVolGroup`, sobre el volumen físico creado con anterioridad:

```
# vgcreate MyVolGroup /dev/mapper/cryptlvm

```

Cree varios volúmenes lógicos en el grupo de volúmenes:

```
# lvcreate -L 8G MyVolGroup -n swap
# lvcreate -L 32G MyVolGroup -n root
# lvcreate -l 100%FREE MyVolGroup -n home

```

Cree un sistema de archivos para cada volumen lógico:

```
# mkfs.ext4 /dev/MyVolGroup/root
# mkfs.ext4 /dev/MyVolGroup/home
# mkswap /dev/MyVolGroup/swap

```

Monte los sistemas de archivos:

```
# mount /dev/MyVolGroup/root /mnt
# mkdir /mnt/home
# mount /dev/MyVolGroup/home /mnt/home
# swapon /dev/MyVolGroup/swap

```

### Preparar la partición de arranque

El gestor de arranque carga el kernel, [initramfs](/index.php/Initramfs "Initramfs") y sus propios archivos de configuración desde el directorio `/boot`. Este directorio debe estar ubicado en un sistema de archivos separado sin cifrar.

Cree un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") en la partición destinada a `/boot`. Cualquier sistema de archivos que pueda ser leído por el gestor de arranque vale.

```
# mkfs.ext4 /dev/sdb1

```

Cree el directorio `/mnt/boot`:

```
# mkdir /mnt/boot

```

Monte la partición para `/mnt/boot`:

```
# mount /dev/sdb1 /mnt/boot

```

### Configurar mkinitcpio

Añada los hooks `keyboard`, `encrypt` y `lvm2` a [mkinitcpio.conf](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"):

```
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

Si utiliza el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), se debe configurar lo siguiente en su lugar:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que se puedan necesitar.

### Configurar el gestor de arranque

Con el fin de desbloquear en el arranque la partición raíz cifrada, es necesario pasar los siguientes parámetros del kernel al gestor de arranque:

```
cryptdevice=UUID=*device-UUID*:cryptlvm root=/dev/MyVolGroup/root

```

Si utiliza el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), lo siguiente debe establecerse en su lugar:

```
rd.luks.name=*device-UUID*=cryptlvm root=/dev/MyVolGroup/root

```

El `*device-UUID*` se refiere al UUID de `/dev/sda1`. Véase [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") para más detalles.

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para más detalles.

## LUKS sobre LVM

Para utilizar el cifrado sobre [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), los volúmenes LVM se establecen primero y luego se usan como base para las particiones cifradas. De esta manera, es posible mezclar particiones/volúmenes cifrados/sin cifrar.

**Sugerencia:** A diferencia de [#LVM sobre LUKS](#LVM_sobre_LUKS), este método permite que los volúmenes lógicos puedan abarcar con normalidad varios discos.

El siguiente ejemplo se crea una configuración LUKS sobre LVM, donde se entremezcla el uso de un archivo de claves para desbloquear la partición /home, por un lado, con volúmenes temporales cifrados para `/tmp` y `/swap`, por otro. Esto último se considera deseable desde una perspectiva de seguridad, ya que ningún dato temporal potencialmente sensible sobrevivirá al reinicio, cuando el cifrado se reinicializa. Si tiene experiencia con LVM, podrá ignorar/reemplazar LVM y otros detalles de acuerdo con su plan.

Si desea que un volumen lógico abarque varios discos que ya se han configurado, o ampliar el volumen lógico para `/home` (o cualquier otro volumen), en [dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties") se describe un procedimiento para hacerlo. Es importante tener en cuenta que el contenedor cifrado con LUKS también debe redimensionarse.

### Preparar el disco

Esquema de particionado:

```
+-----------------------+--------------------------------------------------------------------------------------------------------------+
| Partición de arranque | volumen cifrado con plain dm-crypt | volumen cifrado con LUKS           | volumen cifrado con LUKS           |
|                       |                                    |                                    |                                    |
| /boot                 | [SWAP]                             | /                                  | /home                              |
|                       |                                    |                                    |                                    |
|                       | /dev/mapper/swap                   | /dev/mapper/root                   | /dev/mapper/home                   |
|                       |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |
|                       | Volumen lógico 1                   | Volumen lógico 2                   | Volumen lógico 3                   |
|                       | /dev/MyVolGroup/cryptswap          | /dev/MyVolGroup/cryptroot          | /dev/MyVolGroup/crypthome          |
|                       |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |
|                       |                                                                                                              |
|   /dev/sda1           |                                   /dev/sda2                                                                  |
+-----------------------+--------------------------------------------------------------------------------------------------------------+

```

Escriba aleatóriamente la partición `/dev/sda2` como indica el artículo [dm-crypt/Drive preparation (Español)#Limpiar un disco o partición vacía con dm-crypt](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol)#Limpiar_un_disco_o_partici.C3.B3n_vac.C3.ADa_con_dm-crypt "Dm-crypt/Drive preparation (Español)").

### Preparar los volúmenes lógicos

```
# pvcreate /dev/sda2
# vgcreate MyVolGroup /dev/sda2
# lvcreate -L 32G -n cryptroot MyVolGroup
# lvcreate -L 500M -n cryptswap MyVolGroup
# lvcreate -L 500M -n crypttmp MyVolGroup
# lvcreate -l 100%FREE -n crypthome MyVolGroup

```

```
# cryptsetup luksFormat --type luks2 /dev/MyVolGroup/cryptroot
# cryptsetup open /dev/MyVolGroup/cryptroot root
# mkfs.ext4 /dev/mapper/root
# mount /dev/mapper/root /mnt

```

Más información acerca de las opciones de cifrado se puede encontrar en [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption"). Tenga en cuenta se indicará cómo cifrar `/home` en [#Cifrar el volúmen lógico /home](#Cifrar_el_vol.C3.BAmen_l.C3.B3gico_.2Fhome).

**Sugerencia:** Además, observe que si alguna vez tiene que acceder a la raíz cifrada desde la ISO de Arch, la anterior acción `open` le permitirá a continuación [mostrar los volúmenes de LVM](/index.php/LVM_(Espa%C3%B1ol)#No_se_muestran_los_vol.C3.BAmenes_l.C3.B3gicos "LVM (Español)").

### Preparar la partición de arranque

```
# dd if=/dev/zero of=/dev/sda1 bs=1M status=progress
# mkfs.ext4 /dev/sda1
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

### Configurar mkinitcpio

Añada los hooks `keyboard`, `lvm2` y `encrypt` a [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"):

```
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **lvm2** **encrypt** filesystems fsck)

```

Si usa el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") con initramfs basado en systemd, en su lugar debe establecerse lo siguiente:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que se puedan necesitar.

### Configurar el gestor de arranque

Con el fin de desbloquear en el arranque la partición raíz cifrada, es necesario pasar los siguientes parámetros del kernel al gestor de arranque:

```
cryptdevice=/dev/MyVolGroup/cryptroot:root root=/dev/mapper/root

```

Si utiliza el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), se debe configurar lo siguiente en su lugar:

```
rd.luks.name=*device-UUID*=root root=/dev/mapper/root

```

El `*device-UUID*` hace referencia al UUID de `/dev/MyVolGroup/cryptroot`. Consulte [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") para más detalles.

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para conocer más detalles.

### Configurar fstab y crypttab

Ambas entradas, para [crypttab](/index.php/Crypttab "Crypttab") y [fstab](/index.php/Fstab "Fstab"), son necesarias tanto para desbloquear el dispositivo como para montar los sistemas de archivos, respectivamente. Las siguientes líneas volverán a reencriptar los sistemas de archivos temporales en cada reinicio:

 `/etc/crypttab` 
```
swap	/dev/MyVolGroup/cryptswap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256
tmp	/dev/MyVolGroup/crypttmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256
```
 `/etc/fstab` 
```
/dev/mapper/root        /       ext4            defaults        0       1
/dev/sda1               /boot   ext4            defaults        0       2
/dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
/dev/mapper/swap        none    swap            sw              0       0

```

### Cifrar el volúmen lógico /home

Desde este escenario se utiliza LVM como el primer mapeador y dm-crypt como el segundo, cada volumen lógico cifrado requiere su propio cifrado. Sin embargo, a diferencia de los sistemas de archivos temporales configurados con cifrado volátil anteriormente, el volumen lógico para `/home` debe ser persistente, por supuesto. Lo siguiente asume que se ha reiniciado el sistema instalado, de lo contrario se tienen que ajustar las rutas. Para asegurarnos de que se introduce una segunda frase de acceso en el arranque para dicho volumen, creamos un [archivo de claves](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"):

```
# mkdir -m 700 /etc/luks-keys
# dd if=/dev/random of=/etc/luks-keys/home bs=1 count=256 status=progress

```

El volumen lógico se cifra con dicho archivo de clave:

```
# cryptsetup luksFormat --type luks2 -v /dev/MyVolGroup/crypthome /etc/luks-keys/home
# cryptsetup -d /etc/luks-keys/home open /dev/MyVolGroup/crypthome home
# mkfs.ext4 /dev/mapper/home
# mount /dev/mapper/home /home

```

El montaje encriptado será configurado tanto en [crypttab](/index.php/Crypttab "Crypttab") como en [fstab](/index.php/Fstab "Fstab"):

 `/etc/crypttab` 
```
home	/dev/MyVolGroup/crypthome   /etc/luks-keys/home

```
 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

## LUKS sobre RAID por software

Este ejemplo se basa en una configuración real para un portátil destinado a funcionar como una estación de trabajo equipado con dos unidades SSD de igual tamaño y una unidad de disco duro (HDD) adicional para almacenamiento masivo. El resultado final es el cifrado del disco completo basado en LUKS (incluyendo `/boot`) para todas las unidades, con las unidades SSD en una matriz [RAID0](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)") y los archivos de clave utilizados para desbloquear toda la encriptación después de que [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") recibe una frase de contraseña correcta en el arranque.

Esta configuración utiliza un esquema de particionado muy simplificado, con todo el almacenamiento RAID disponible montado en `/` (sin partición `/boot` separada, y el disco HDD descifrado montado en `/mnt/data`. También vale la pena mencionar que el sistema en este ejemplo arranca en modo BIOS y las unidades están particionadas con la tabla de particiones [GPT](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)").

Tenga en cuenta que es muy importante en este tipo de configuraciones realizar [copias de seguridad del sistema](/index.php/System_backup "System backup") regulares. Si cualquiera de los SSD falla, los datos contenidos en el conjunto RAID serán prácticamente imposibles de recuperar. Es posible que desee seleccionar un [nivel RAID](/index.php/RAID_(Espa%C3%B1ol)#Niveles_RAID_est.C3.A1ndar "RAID (Español)") diferente si la tolerancia a los fallos es importante para usted.

El cifrado no es denegable en esta configuración.

Para el ejemplo de las siguientes instrucciones, se utilizan los siguientes dispositivos de bloques:

```
/dev/sda = primer SSD
/dev/sdb = segundo SSD
/dev/sdc = HDD

```

Asegúrese de sustituirlos por las designaciones de dispositivo apropiadas para su configuración, ya que pueden ser diferentes.

### Preparar los discos

Antes de crear cualquier partición, debe informarse acerca de la importancia y los métodos para borrar de forma segura el disco, descrito en [dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)").

Al usar el gestor de arranque [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") junto con [GPT](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)"), cree una [BIOS boot partition](/index.php/GRUB_(Espa%C3%B1ol)#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29 "GRUB (Español)"). Para esta configuración, esto incluye una partición de 1 MiB para el arranque de BIOS/GPT en `/dev/sda1` y el espacio restante de la unidad que está siendo particionada para «Linux RAID» en `/dev/sda2`.

Una vez que se ha creado las particiones en `/dev/sda`, se pueden usar las siguientes órdenes para clonarlas en `/dev/sdb`

```
# sfdisk -d /dev/sda > sda.dump
# sfdisk /dev/sdb < sda.dump

```

El disco HDD está preparado con una sola partición de Linux que cubre todo el disco en `/dev/sdc1`.

### Compilar la matriz RAID

Cree la matriz RAID para las unidades SSD. Este ejemplo utiliza RAID0, aunque puede que desee sustituirlo por un nivel diferente según sus preferencias o requisitos.

```
# mdadm --create --verbose --level=0 --metadata=1.2 --raid-devices=2 /dev/md0 /dev/sda2 /dev/sdb2

```

### Preparar los dispositivos de bloque

Como se explica en [dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)"), los dispositivos se limpian con datos aleatorios utilizando `/dev/zero` y un dispositivo de cifrado con una clave aleatoria. Alternativamente, puede usar `dd` con `/dev/random` o `/dev/urandom`, aunque será mucho más lento.

```
# cryptsetup open --type plain /dev/md0 container --key-file /dev/random
# dd if=/dev/zero of=/dev/mapper/container bs=1M status=progress
# cryptsetup close container

```

Y repita lo anterior para la unidad HDD (`/dev/sdc1` en este ejemplo).

Configure el cifrado para `/dev/md0`:

```
# cryptsetup -y -v luksFormat --type luks2 /dev/md0
# cryptsetup open /dev/md0 cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Y repítalo para la unidad HDD:

```
# cryptsetup -y -v luksFormat --type luks2 /dev/sdc1
# cryptsetup open /dev/sdc1 cryptdata
# mkfs.ext4 /dev/mapper/cryptdata
# mkdir -p /mnt/mnt/data
# mount /dev/mapper/cryptdata /mnt/mnt/data

```

### Configurar el gestor de arranque

Configure [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") para el sistema cifrado, modificando `/etc/default/grub` con lo siguiente:

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/md0:cryptroot root=/dev/mapper/cryptroot"
GRUB_ENABLE_CRYPTODISK=y

```

Consulte [dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") y [GRUB (Español)#Partición de arranque](/index.php/GRUB_(Espa%C3%B1ol)#Partici.C3.B3n_de_arranque "GRUB (Español)") para obtener más detalles.

Complete la instalación de GRUB en ambas unidades SSD (en realidad, la instalación solo para `/dev/sda` funcionará).

```
# grub-install --target=i386-pc /dev/sda
# grub-install --target=i386-pc /dev/sdb
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Crear los archivos de claves

Los próximos pasos le ahorran que tenga que ingresar su contraseña dos veces cuando inicia el sistema (una vez para que GRUB pueda desbloquear el cifrado, y la segunda vez cuando initramfs asume el control del sistema). Esto se hace creando un [archivo de claves](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") para el cifrado y añadiéndolo a la imagen de initramfs para permitir que el hook encrypt desbloquee el dispositivo raíz. Consulte [dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") para más detalles.

*   Cree el [archivo de claves](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") y agregue la clave para `/dev/md0`.
*   Cree otro archivo de claves para la unidad HDD (`/dev/sdc1`) para que también se pueda desbloquear al arrancar. Para su comodidad, deje la contraseña creada anteriormente en su lugar, ya que esto puede facilitar la recuperación si alguna vez la necesita. Modifique `/etc/crypttab` para descifrar la unidad HDD al arrancar. Vea [dm-crypt/Device encryption#Unlocking a secondary partition at boot](/index.php/Dm-crypt/Device_encryption#Unlocking_a_secondary_partition_at_boot "Dm-crypt/Device encryption").

### Configurar el sistema

Modifique [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") para montar los dispositivos de bloques cryptroot y cryptdata:

```
/dev/mapper/cryptroot  /           ext4    rw,noatime  0   1 
/dev/mapper/cryptdata  /mnt/data   ext4    defaults            0   2  

```

Guarde la configuración de RAID:

```
# mdadm --detail --scan > /etc/mdadm.conf 

```

Modifique [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para incluir su archivo de claves y agregar los hooks adecuados:

```
FILES=(/crypto_keyfile.bin)
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **mdadm_udev** **encrypt** filesystems fsck)

```

Consulte [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles.

## Modalidad plain de dm-crypt

Contrariamente a LUKS, la modalidad *plain* de dm-crypt no requiere una cabecera en el disco cifrado: esto significa que un disco cifrado sin particionar será indistinguible de un disco lleno con datos aleatorios, que podría permitir [cifrado negable](https://en.wikipedia.org/wiki/es:Cifrado_negable "wikipedia:es:Cifrado negable"). Véase también [wikipedia:es:Cifrado de disco#Completo cifrado de disco](https://en.wikipedia.org/wiki/es:Cifrado_de_disco#Completo_cifrado_de_disco "wikipedia:es:Cifrado de disco").

Tenga en cuenta que si no necesita cifrar el disco completo, los métodos que utilizan LUKS descritos anteriormente son las mejores opciones para el cifrado del sistema y de las particiones. Características de LUKS como la gestión de claves con múltiples frases de contraseñas/archivos de claves no están disponibles con la modalidad *plain*.

Los discos cifrados con la modalidad *plain* de dm-crypt pueden ser más resistentes a los daños que los discos cifrados con LUKS, ya que no se basan en una clave maestra de cifrado, la cual constituye un punto vulnerable único de fallo si se daña. Sin embargo, utilizando el modo *plain* también se requiere una configuración más manual de las opciones de cifrado para lograr la misma fuerza criptográfica. Véase también [Disk encryption (Español)#Metadatos criptográficos](/index.php/Disk_encryption_(Espa%C3%B1ol)#Metadatos_criptogr.C3.A1ficos "Disk encryption (Español)"). También se puede considerar el uso de la modalidad *plain* si se trata de los problemas explicados en [dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties").

**Sugerencia:** Si el cifrado sin cabeceras es su objetivo, pero no está seguro acerca de la falta de derivación de clave con el modo *plain*, entonces dispone de dos alternativas:

*   [tcplay](/index.php/Tcplay "Tcplay") que ofrece cifrado sin cabeceras, pero con la función PBKDF2, o
*   la modalidad LUKS de dm-crypt utilizando la opción `--header` de *cryptsetup*. No se podrá utilizar el hook estándar *encrypt*, pero dicho hook [puede ser modificado](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties").

El escenario utiliza una memoria USB:

*   una para el dispositivo de arranque que también permite almacenar las opciones necesarias para abrir/desbloquear el dispositivo cifrado simple en la configuración del gestor de arranque, ya que escribirlos en cada arranque sería propenso a errores;
*   y otra para almacenar la clave de cifrado asumiendo que está almacenada como bits en bruto de modo que a los ojos de un atacante que no esté al tanto que quiera obtener la clave usb, la clave de cifrado se mostrará como datos aleatorios en lugar de ser visible como un archivo normal. Véase también [Wikipedia:es:Seguridad por oscuridad](https://en.wikipedia.org/wiki/es:Seguridad_por_oscuridad "wikipedia:es:Seguridad por oscuridad"), y siga con [dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") para preparar el archivo de claves.

El esquema de particionado del disco es:

```
+----------------------+----------------------+----------------------+ +-------------------------+ +--------------------------+
| Volumen lógico 1     | Volumen lógico 2     | Volumen lógico 3     | | Dispositivo de arranque | | Depósito para el archivo |
|                      |                      |                      | |                         | | de claves de cifrado     |
| /                    | [SWAP]               | /home                | | /boot                   | | (sin particionar         |
|                      |                      |                      | |                         | | en el ejemplo)           |
| /dev/MyVolGroup/root | /dev/MyVolGroup/swap | /dev/MyVolGroup/home | | /dev/sdb1               | | /dev/sdc                 |
|----------------------+----------------------+----------------------| |-------------------------| |--------------------------|
| unidad/disco /dev/sda cifrado con modo plain y LVM                 | | USB 1                   | | USB 2                    |
+--------------------------------------------------------------------+ +-------------------------+ +--------------------------+

```

**Sugerencia:**

*   También es posible utilizar una sola llave USB mediante la copia del archivo de claves a la initram directamente. Un ejemplo de archivo de claves `/etc/keyfile` copiado a la imagen initram se hace estableciendo `FILES="/etc/keyfile"` en `/etc/mkinitcpio.conf`. La manera de instruir al hook `encrypt` para que lea el archivo de claves en la imagen initram es utilizando el prefijo `rootfs:` delante del nombre del archivo, por ejemplo `cryptkey=rootfs:/etc/keyfile`.
*   Otra opción es usar una frase de acceso con buena [entropía](/index.php/Disk_encryption_(Espa%C3%B1ol)#Elegir_una_frase_de_acceso_s.C3.B3lida "Disk encryption (Español)").

### Preparar el disco

Es de vital importancia que el dispositivo mapeado está lleno de datos. En particular, esto se aplica al caso que nos afecta.

Véase [Dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") y [Dm-crypt/Drive preparation (Español)#Métodos específicos de dm-crypt](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol)#M.C3.A9todos_espec.C3.ADficos_de_dm-crypt "Dm-crypt/Drive preparation (Español)")

### Preparar las particiones que no son de arranque (boot)

Consulte [dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") para más detalles.

Utilizando el dispositivo `/dev/sda`, con el cifrado twofish-xts con un tamaño de clave de 512 bits, y un archivo de clave, tenemos las siguientes opciones para este escenario:

```
# cryptsetup --hash=sha512 --cipher=twofish-xts-plain64 --offset=0 --key-file=/dev/sdc --key-size=512 open --type=plain /dev/sda cryptlvm

```

A diferencia del cifrado con LUKS, la orden anterior se debe ejecutar *en su totalidad* siempre que sea necesario restablecer el mapeado, por lo que es importante recordar los detalles del cifrado, el hash y el archivo de claves.

Ahora podemos comprobar que se ha realizado una entrada de mapeo para `/dev/mapper/cryptlvm`:

```
# fdisk -l

```

A continuación, configuramos volúmenes lógicos [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") en el dispositivo mapeado. Consulte [LVM (Español)#Instalar Arch Linux sobre LVM](/index.php/LVM_(Espa%C3%B1ol)#Instalar_Arch_Linux_sobre_LVM "LVM (Español)") para obtener más detalles:

```
# pvcreate /dev/mapper/cryptlvm
# vgcreate MyVolGroup /dev/mapper/cryptlvm
# lvcreate -L 32G MyVolGroup -n root
# lvcreate -L 10G MyVolGroup -n swap
# lvcreate -l 100%FREE MyVolGroup -n home

```

Formateamos y montamos y, luego, activamos el espacio de intercambio. Consulte [File systems (Español)#Crear un sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") para más detalles:

```
# mkfs.ext4 /dev/MyVolGroup/root
# mkfs.ext4 /dev/MyVolGroup/home
# mount /dev/MyVolGroup/root /mnt
# mkdir /mnt/home
# mount /dev/MyVolGroup/home /mnt/home
# mkswap /dev/MyVolGroup/swap
# swapon /dev/MyVolGroup/swap

```

### Preparar la partición de arranque

La partición `/boot` se puede instalar en la partición vfat estándar de una memoria USB, si es necesario. Pero si se ve en la necesidad de realizar el particionado manualmente, entonces podría crear una pequeña partición de 200 MiB, lo que sería suficiente. Cree la partición utilizando una [utilidad de particionado](/index.php/Partitioning_(Espa%C3%B1ol)#Herramientas_de_particionado "Partitioning (Español)") de su elección.

Cree un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") en la partición destinada a `/boot`, si no está ya formateada como vfat:

```
# mkfs.ext4 /dev/sdb1
# mkdir /mnt/boot
# mount /dev/sdb1 /mnt/boot

```

### Configurar mkinitcpio

Añada los hooks `keyboard`, `encrypt` and `lvm2` a [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"):

```
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que pueda necesitar.

### Configurar el gestor de arranque

Con el fin de desbloquear la partición raíz cifrada en el arranque, es necesario pasar los siguientes parámetros del kernel al gestor de arranque:

```
cryptdevice=/dev/disk/by-id/*disk-ID-of-sda*:cryptlvm cryptkey=/dev/disk/by-id/*disk-ID-of-sdc*:0:512 crypto=sha512:twofish-xts-plain64:512:0:

```

El `*disk-ID-of-**disk***` se refiere a la identificación del disco al que se hace referencia. Véase [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") par más detalles.

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para conocer más detalles y otros parámetros que pueda necesitar

**Sugerencia:** Si se utiliza GRUB, puede instalarlo en el mismo USB utilizado como partición `/boot` con:
```
# grub-install --recheck /dev/sdb

```

### Posinstalación

Podemos retirar la memoria USB después de arrancar. Ya que la partición `/boot`, generalmente, no se necesita, la opción `noauto` se puede agregar en la línea correspondiente de `/etc/fstab`:

 `/etc/fstab` 
```
# /dev/sdb1
/dev/sdb1 /boot ext4 **noauto**,rw,noatime 0 2

```

Sin embargo, cuando se requiere una actualización del kernel o del cargador de arranque, la partición `/boot` debe estar presente y montada. Como la entrada en `fstab` ya existe, se puede montar de forma sencilla con:

```
# mount /boot

```

## Cifrar partición de arranque (GRUB)

Esta configuración utiliza el mismo diseño de partición y configuración que para la partición raíz del sistema en la sección anterior [#LVM sobre LUKS](#LVM_sobre_LUKS), con la clara diferencia una característica especial del gestor de arranque [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") es utilizada para cifrar adicionalmente la partición de arranque `/boot`. Vea también [GRUB (Español)#Partición de arranque](/index.php/GRUB_(Espa%C3%B1ol)#Partici.C3.B3n_de_arranque "GRUB (Español)").

La distribución del disco en este ejemplo es:

```
+---------------------+----------------------+----------------+----------------------+----------------------+----------------------+
| Partición           | Partición            | Partición      | Volumen lógico 1     | Volumen lógico 2     | Volumen lógico 3     |
| BIOS boot partition | EFI system particion | de arranque    |                      |                      |                      |
|                     | /efi                 | /boot          | /root                | [SWAP]               | /home                |
|                     |                      |                |                      |                      |                      |
|                     |                      |                | /dev/MyVolGroup/root | /dev/MyVolGroup/swap | /dev/MyVolGroup/home |
| /dev/sda1           | /dev/sda2            | /dev/sda3      +----------------------+----------------------+----------------------+
| sin cifrar          | sin cifrar           |cifrado con LUKS| /dev/sda4 cifrado usando LVM sobre LUKS                            |
+---------------------+----------------------+----------------+--------------------------------------------------------------------+

```

**Sugerencia:**

*   Todos los escenarios tienen el propósito de ejemplos. Es, por supuesto, posible combinar los dos pasos anteriores de las distintas instalaciones con otros escenarios posibles. Ver también las variantes asociadas a [#LVM sobre LUKS](#LVM_sobre_LUKS)
*   Puede utilizar el script `cryptboot` del paquete [cryptboot](https://aur.archlinux.org/packages/cryptboot/) para una administración de arranque cifrada simplificada (montaje, desmontaje, actualización de paquetes) y como defensa contra ataques de [Evil Maid](https://www.schneier.com/blog/archives/2009/10/evil_maid_attac.html) con [Secure Boot de UEFI](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"). Para obtener más información y limitaciones, consulte la página [cryptboot project](https://github.com/xmikos/cryptboot).

### Preparar el disco

Antes de crear las particiones, debe informarse sobre la importancia y los métodos para borrar de forma segura el disco, descrito en [Dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)").

Para [sistemas BIOS](/index.php/GRUB_(Espa%C3%B1ol)#Sistemas_BIOS "GRUB (Español)") cree una [BIOS boot partition](/index.php/GRUB_(Espa%C3%B1ol)#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29 "GRUB (Español)") con tamaño de 1 MiB para GRUB para almacenar la segunda etapa del gestor de arranque BIOS. No monte la partición.

Para [sistemas UEFI](/index.php/GRUB_(Espa%C3%B1ol)#Sistemas_UEFI "GRUB (Español)") cree una [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") con un tamaño apropiado, para luego montarla en `/efi`.

Cree una partición para montar en `/boot`, del tipo `8300`, con un tamaño de 200 MiB o más.

Cree una partición del tipo `8E00`, que más tarde va a contener el contenedor cifrado.

Cree el contenedor cifrado con LUKS en la partición del «sistema».

```
# cryptsetup luksFormat --type luks2 /dev/sda4

```

Para obtener más información sobre las opciones disponibles de cryptsetup vea [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de ejecutar la orden anterior.

Su esquema de particinado debería ser similar a esto:

 `# gdisk /dev/sda` 
```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048            4095   1024.0 KiB  EF02  BIOS boot partition
   2            4096         1130495   550.0 MiB   EF00  EFI System
   3         1130496         1540095   200.0 MiB   8300  Linux filesystem
   4         1540096        69205982   32.3 GiB    8E00  Linux LVM

```

Abra el contenedor:

```
# cryptsetup open /dev/sda4 cryptlvm

```

El contenedor desbloqueado estará ahora disponible como `/dev/mapper/cryptlvm`.

### Preparar los volúmenes lógicos

Los volúmenes lógicos LVM de este ejemplo siguen el mismo esquema descrito en el escenario [#LVM sobre LUKS](#LVM_sobre_LUKS). Por lo tanto, siga la sección [#Preparar los volúmenes lógicos](#Preparar_los_vol.C3.BAmenes_l.C3.B3gicos) de arriba o haga los ajustes necesarios.

### Preparar la partición de arranque

**Advertencia:** GRUB no es compatible con LUKS2\. No utilice LUKS2 en las particiones a las que GRUB debe acceder.

El gestor de arranque carga el kernel, [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") y sus propios archivos de configuración desde el directorio `/boot`.

En primer lugar, cree el contenedor LUKS donde estarán ubicados e instalados los archivos:

```
# cryptsetup luksFormat /dev/sda3

```

A continuación, ábralo:

```
# cryptsetup open /dev/sda3 cryptboot

```

Cree un sistema de archivos en la partición destinada a `/boot`. Cualquier sistema de archivos que puede ser leído por el gestor de arranque es elegible:

```
# mkfs.ext4 /dev/mapper/*cryptboot*

```

Cree el directorio `/mnt/boot`:

```
# mkdir /mnt/boot

```

Monte la partición para `/mnt/boot`:

```
# mount /dev/mapper/*cryptboot* /mnt/boot

```

Cree el punto de montaje para la [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") en `/efi` para que sea compatible con `grub-install`, y móntela:

```
# mkdir /mnt/efi
# mount /dev/sda2 /mnt/efi

```

En este punto, debe tener las siguientes particiones y volúmenes lógicos dentro de `/mnt`:

 `$ lsblk` 
```
NAME                  MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                   8:0      0   200G  0 disk
├─sda1                8:1      0     1M  0 part
├─sda2                8:2      0   550M  0 part  /efi
├─sda3                8:3      0   200M  0 part
│ └─cryptboot         254:0    0   198M  0 crypt /boot
└─sda4                8:4      0   100G  0 part
  └─cryptlvm          254:1    0   100G  0 crypt
    ├─MyVolGroup-swap 254:2    0     8G  0 lvm   [SWAP]
    ├─MyVolGroup-root 254:3    0    32G  0 lvm   /
    └─MyVolGroup-home 254:4    0    60G  0 lvm   /home

```

### Configurar mkinitcpio

Añada los hooks `keyboard`, `encrypt` y `lvm2` a [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"):

```
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

Si utiliza el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") con initramfs basado en systemd se debe establecer lo siguiente en su lugar:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para más detalles y otros hooks que pueda necesitar.

### Configurar el gestor de arranque

Configure GRUB para que reconozca la partición `/boot` cifrada con LUKS y desbloquee la partición raíz cifrada al arranque:

 `/etc/default/grub` 
```
GRUB_CMDLINE_LINUX="... cryptdevice=UUID=*device-UUID*:cryptlvm ..."
GRUB_ENABLE_CRYPTODISK=y
```

Si utiliza el hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), se debe configurar lo siguiente en su lugar:

 `/etc/default/grub` 
```
GRUB_CMDLINE_LINUX="... rd.luks.name=*device-UUID*=cryptlvm" ...
GRUB_ENABLE_CRYPTODISK=y
```

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") y [GRUB (Español)#Partición de arranque](/index.php/GRUB_(Espa%C3%B1ol)#Partici.C3.B3n_de_arranque "GRUB (Español)") para obtener más detalles. El `*device-UUID*` hace referencia al UUID de `/dev/sda4` (la partición que aloja el lvm, la cual contiene a su vez el sistema de archivos raíz). Vea [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)").

Genere el archivo de [configuration](/index.php/GRUB_(Espa%C3%B1ol)#Generar_el_archivo_de_configuraci.C3.B3n_principal "GRUB (Español)") de GRUB :

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

[Instale GRUB](/index.php/GRUB_(Espa%C3%B1ol)#Instalaci.C3.B3n_2 "GRUB (Español)") con la ESP montada para arrancar UEFI:

```
# grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB --recheck

```

[Instale GRUB](/index.php/GRUB#Instalaci.C3.B3n "GRUB") en el disco para arrancar BIOS:

```
# grub-install --target=i386-pc --recheck /dev/sda

```

Si todo terminó sin errores, GRUB le pedirá la contraseña para desbloquear la partición `/boot` en el siguiente reinicio.

### Configurar fstab y crypttab

Esta sección trata de la configuración extra para dejar que el sistema *monte* `/boot` cifrado.

Mientras GRUB pide una contraseña para desbloquear la partición `/boot` cifrada, siguiendo las instrucciones anteriores, el desbloqueo de la partición no se transmite a los initramfs. Por lo tanto, `/boot` no estará disponible después de que el sistema haya re/iniciado, porque el hook `encrypt` solo desbloquea la raíz del sistema.

Si ha utilizado el script *genfstab* durante la instalación, se habrán generado ya en `/etc/fstab` las entradas para el montaje de `/boot` y `/boot/efi`, pero el sistema no podrá encontrar el mapeador de dispositivos generado por la partición de arranque. Para que esté disponible, agréguelo a [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration"). Por ejemplo:

 `/etc/crypttab` 
```
cryptboot  /dev/sda3      none        luks

```

lo que hará que el sistema pida la contraseña de nuevo (es decir, tiene que introducir dos veces la contraseña en el arranque: una vez para GRUB y otra para la inicialización de systemd). Para evitar la repetición de la contraseña para desbloquear `/boot`, siga las instrucciones descritas en [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"):

1.  cree un [archivo de claves de texto aleatorio](/index.php/Dm-crypt/Device_encryption#Storing_the_keyfile_on_a_filesystem "Dm-crypt/Device encryption");
2.  añada el archivo de claves a la [cabecera LUKS de la partición boot](/index.php/Dm-crypt/Device_encryption#Configuring_LUKS_to_make_use_of_the_keyfile "Dm-crypt/Device encryption") (`/dev/sda3`), y
3.  compruebe la entrada `/etc/fstab` y añada la línea `/etc/crypttab` para [desbloquearla automáticamente en el arranque](/index.php/Dm-crypt/Device_encryption#Unlocking_a_secondary_partition_at_boot "Dm-crypt/Device encryption").

Si por alguna razón el archivo de claves no puede desbloquear la partición de arranque, systemd se repliega para pedir una contraseña para desbloquear y, en caso de que sea correcta, continuar el arranque.

**Sugerencia:** Pasos opcionales posinstalación:

*   Puede que valga la pena considerar añadir el gestor de arranque GRUB a la lista de ignorados en `/etc/pacman.conf` con el fin de atender de forma especial el control de cuándo el gestor de arranque (que incluye sus propios módulos de cifrado) se actualiza.
*   Si desea cifrar la partición `/boot` para protegerse contra amenazas de manipulación offline, el hook [mkinitcpio-chkcryptoboot](/index.php/Dm-crypt/Specialties#mkinitcpio-chkcryptoboot "Dm-crypt/Specialties") puede serle de ayuda.

## Subvolúmenes btrfs con espacio de intercambio

El siguiente ejemplo crea un cifrado completo del sistema con LUKS utilizando subvolúmenes [Btrfs](/index.php/Btrfs "Btrfs") como una [simulación de particiones](/index.php/Btrfs#Mounting_subvolumes "Btrfs").

Si utiliza UEFI, se requiere una [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") (siglas en inglés ESP). El mismo `/boot` puede residir en la raíz `/` y estar cifrado; sin embargo, la ESP no puede cifrase. En este esquema propuesto de ejemplo, la ESP es `/dev/sda1` y está montada en `/efi`. `/boot` se encuentra en la partición del sistema, `/dev/sda2`.

Dado que `/boot` reside en la raiz `/` cifrada, [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") debe usarse como gestor de arranque, porque solo GRUB puede cargar los módulos necesarios para descifrar `/boot` (por ejemplo, crypto.mod, cryptodisk.mod y luks.mod) [[1]](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/).

Además, se el esquema muestra una partición opcional de [Swap (Español)](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)") cifrada con plain.

**Advertencia:** No utilice un [archivo de intercambio](/index.php/Swap_(Espa%C3%B1ol)#Archivo_swap "Swap (Español)") en lugar de una partición separada, ya que esto puede ocasionar la pérdida de datos. Vea [Btrfs#Swap file](/index.php/Btrfs#Swap_file "Btrfs").

```
+----------------------+----------------------+-----------------------+
| Partición EFI system | Partición del sistema| Partición intercambio |
| sin cifrar           | cifrada con LUKS     | cifrada con plain     |
|                      |                      |                       |
| /efi                 | /                    | [SWAP]                |
| /dev/sda1            | /dev/sda2            | /dev/sda3             |
|----------------------+----------------------+-----------------------+

```

### Preparar el disco

**Nota:** No es posible utilizar btrfs para particionar como se describe en [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") cuando se utiliza LUKS. Se debe utilizar la partición tradicional, incluso si solo se trata de crear una partición.

Antes de crear cualquier partición, debe informarse acerca de la importancia y los métodos para borrar de forma segura el disco, descrito en [dm-crypt/Drive preparation (Español)](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)"). Si está utilizando [UEFI (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), cree una [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") con un tamaño apropiado. Posteriormente se montará en `/efi`. Si va a crear una partición de intercambio cifrada, crea la partición para ella, pero **no** la marque como *swap*, ya que se usará la modalidad plain de *dm-crypt* para cifrar la partición.

Cree las particiones necesarias, al menos una para la raíz `/` (por ejemplo, `/dev/sda2`). Vea el artículo [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)").

### Preparar la partición del sistema

#### Crear contenedor LUKS

Siga la sección [dm-crypt/Device encryption#Encrypting devices with LUKS mode](/index.php/Dm-crypt/Device_encryption#Encrypting_devices_with_LUKS_mode "Dm-crypt/Device encryption") para configurar `/dev/sda2` para LUKS. Consulte [dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de hacerlo para obtener una lista de opciones de cifrado.

#### Desbloquear el contenedor LUKS

Ahora siga las instrucciones de [dm-crypt/Device encryption#Unlocking/Mapping LUKS partitions with the device mapper](/index.php/Dm-crypt/Device_encryption#Unlocking.2FMapping_LUKS_partitions_with_the_device_mapper "Dm-crypt/Device encryption") para desbloquear el contenedor LUKS y mapearlo.

#### Formatear el dispositivo mapeado

Proceda a formatear el dispositivo mapeado como se describe en [Btrfs#File system on a single device](/index.php/Btrfs#File_system_on_a_single_device "Btrfs"), donde `*/dev/partition*` es el nombre del dispositivo mapeado (es decir, `cryptroot`) y **no** `/dev/sda2`.

#### Montar el dispositivo mapeado

Finalmente, [[mount|monte] el dispositivo mapeado ahora formateado (es decir, `/dev/mapper/cryptroot`) en `/mnt`.

**Sugerencia:** Es posible que desee utilizar la opción de montaje `compress=lzo`. Vea [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs") para más información.

### Crear subvolúmenes btrfs

#### Esquema

Los [subvolúmenes](/index.php/Btrfs#Subvolumes "Btrfs") se usarán para simular particiones, pero también se crearán otros subvolúmenes (anidados). Aquí hay una representación parcial de lo que generará el siguiente ejemplo:

```
subvolid=5 (/dev/sda2)
   |
   ├── @ (montado como /)
   |       |
   |       ├── /bin (directorio)
   |       |
   |       ├── /home (montado subvolumen @home)
   |       |
   |       ├── /usr (directorio)
   |       |
   |       ├── /.snapshots (montado subvolumen @snapshots)
   |       |
   |       ├── /var/cache/pacman/pkg (subvolumen anidado)
   |       |
   |       ├── ... (otros directorios y subvolúmenes anidados)
   |
   ├── @snapshots (montado como /.snapshots)
   |
   ├── @home (montado como /home)
   |
   └── @... (subvolúmenes adicionales que desee usar como puntos de montaje)

```

Esta sección sigue la sección [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper"), que es más útil cuando se usa con [Snapper](/index.php/Snapper "Snapper"). También debe consultar [Btrfs Wiki SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout).

#### Crear subvolumenes de nivel superior

Aquí estamos usando la convención de prefijo `@` para los nombres de subvolumen que se usarán como puntos de montaje, y `@` será el subvolumen que se monta como `/`.

Siguiendo el artículo [Btrfs#Creating a subvolume](/index.php/Btrfs#Creating_a_subvolume "Btrfs"), cree subvolúmenes en `/mnt/@`, `/mnt/@snapshots`, y `/mnt/@home`.

Cree cualquier subvolúmenes adicional que desee usar como puntos de montaje ahora.

#### Montar subvolúmenes de nivel superior

Desmonte la partición del sistema de `/mnt`.

Ahora monte el subvolumen `@` recién creado que servirá como raíz `/` en `/mnt` utilizando la opción de montaje `subvol=`. Suponiendo que el dispositivo mapeado se llama `cryptroot`, la orden se emitiría así:

```
# mount -o compress=lzo,subvol=@ /dev/mapper/cryptroot /mnt

```

Consulte [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs") para obtener más detalles.

Monte también los otros subvolúmenes en sus respectivos puntos de montaje: `@home` en `/mnt/home` y `@snapshots` en `/mnt/.snapshots`.

#### Crear subvolúmenes anidados

Cree cualquier subvolumen del que **no** quiera tener instantáneas de cuando haga instantánea de la raíz `/`. Por ejemplo, probablemente no desee tomar instantáneas de `/var/cache/pacman/pkg`. Estos subvolúmenes estarán anidados bajo el subvolumen `@`, pero con la misma facilidad podrían haber sido creados anteriormente al mismo nivel que `@` de acuerdo con sus preferencia.

Dado que el subvolumen `@` está montado en `/mnt`, necesitará [crear un subvolumen](/index.php/Create_a_subvolume "Create a subvolume") en `/mnt/var/cache/pacman/pkg` para este ejemplo. Es posible que primero tenga que crear cualquier directorio padre.

Otros directorios con los que puede hacer esto son `/var/abs`, `/var/tmp`, and `/srv`.

#### Montar ESP

Si preparó una partición de sistema EFI anteriormente, cree su punto de montaje y móntela ahora.

**Nota:** Las instantáneas de Btrfs excluirán `/efi`, ya que no es un sistema de archivos btrfs.

En el paso de la instalación con [pacstrap](/index.php/Installation_guide_(Espa%C3%B1ol)#Instalar_los_paquetes_del_sistema_base "Installation guide (Español)"), debe instalarse el paquete [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) además del grupo base.

### Configurar mkinitcpio

#### Crear archivo de claves

Para que GRUB abra la partición LUKS sin que el usuario tenga que ingresar dos veces su contraseña, usaremos un archivo de clave incrustado en initramfs. Siga [dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") y asegúrese de agregar la clave de `/dev/sda2` en el paso *luksAddKey*.

#### Editar mkinitcpio.conf

Después de crear, agregar e incrustar la clave como se describe arriba, añada el hook `encrypt` en [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"), así como cualquier otro hook que necesite. Consulte [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para obtener información detallada.

**Sugerencia:** Es posible que desee añadir `BINARIES=(/usr/bin/btrfs)` a `mkinitcpio.conf`.Consulte el artículo [Btrfs#Corruption recovery](/index.php/Btrfs#Corruption_recovery "Btrfs").

### Configurar el gestor de arranque

Instale [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") en `/dev/sda`. A continuación, modifique `/etc/default/grub` como se indica en el artículo [GRUB (Español)# Encriptación](/index.php/GRUB_(Espa%C3%B1ol)#_Encriptaci.C3.B3n "GRUB (Español)"), siguiendo las instrucciones de una partición raíz y de arranque cifrada. Finalmente, genere el archivo de configuración GRUB.

### Configurar el espacio de intercambio

Si creó una partición de intercambio cifrada, ahora es el momento de configurarla. Siga las instrucciones dadas en [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").