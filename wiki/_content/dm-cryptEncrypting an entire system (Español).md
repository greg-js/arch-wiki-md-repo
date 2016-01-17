# dm-crypt/Encrypting an entire system (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**Estado de la traducción:** este artículo es una versión traducida de [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"). Fecha de la última traducción/revisión: **2015-06-27**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_an_entire_system&diff=0&oldid=379213).

Volver a [dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)").

Los siguientes son ejemplos de escenarios comunes en el cifrado completo de un sistema con _dm-crypt_. Se explican todas las adaptaciones que se necesitan hacer al [proceso de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"). Todas las herramientas necesarias para ello están presentes en la [imagen de instalación](https://www.archlinux.org/download/).

## Contents

*   [1 Descripción general](#Descripci.C3.B3n_general)
*   [2 Esquema de particionado simple con LUKS](#Esquema_de_particionado_simple_con_LUKS)
    *   [2.1 Preparar el disco](#Preparar_el_disco)
    *   [2.2 Preparar las particiones que no son boot](#Preparar_las_particiones_que_no_son_boot)
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
*   [6 Plain dm-crypt](#Plain_dm-crypt)
    *   [6.1 Preparar el disco](#Preparar_el_disco_4)
    *   [6.2 Preparar las particiones que no son boot](#Preparar_las_particiones_que_no_son_boot_2)
    *   [6.3 Preparar la partición de arranque](#Preparar_la_partici.C3.B3n_de_arranque_4)
    *   [6.4 Configurar mkinitcpio](#Configurar_mkinitcpio_4)
    *   [6.5 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_4)
    *   [6.6 Posinstalación](#Posinstalaci.C3.B3n)
*   [7 Cifrar partición de arranque (GRUB)](#Cifrar_partici.C3.B3n_de_arranque_.28GRUB.29)
    *   [7.1 Preparar el disco](#Preparar_el_disco_5)
    *   [7.2 Preparar los volúmenes lógicos](#Preparar_los_vol.C3.BAmenes_l.C3.B3gicos_3)
    *   [7.3 Preparar la partición de arranque](#Preparar_la_partici.C3.B3n_de_arranque_5)
    *   [7.4 Configurar mkinitcpio](#Configurar_mkinitcpio_5)
    *   [7.5 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque_5)
    *   [7.6 Configurar fstab y crypttab](#Configurar_fstab_y_crypttab_2)

## Descripción general

Asegurar un sistema de archivos root es donde _dm-crypt_ sobresale, en cuanto a características y rendimiento. Cuando el sistema de archivos de un sistema (root) está en un dispositivo dm-crypt, prácticamente todos los archivos del sistema están cifrados. A diferencia del cifrado de forma selectiva de los sistemas de archivos no root, un sistema de archivos root cifrado puede ocultar información, tales como qué programas se instalan, los nombres de los usuarios y todas sus cuentas, y los vectores de vuelcos de datos comunes, tales como [mlocate](/index.php/Mlocate "Mlocate") y `/var/log/`. Además, un sistema de archivos root cifrado hace que la manipulación del sistema sea mucho más difícil, al estar todo cifrado, con las excepciones del [gestor de arranque](/index.php/Boot_loader "Boot loader") y (normalmente) el kérnel.

En la siguiente tabla se ilustran las ventajas de todos los escenarios posibles, diferenciando los pros y contras de cada uno:

<table class="wikitable">

<tbody>

<tr>

<th>Escenarios</th>

<th>Ventajas</th>

<th>Desventajas</th>

</tr>

<tr>

<td>[LUKS](#Esquema_de_particionado_simple_con_LUKS)

muestra una configuración sencilla y básica de una partición root completamente cifrada con LUKS.

</td>

<td>

*   Particionado y configuración sencilla

</td>

<td>

*   Rigidez; el espacio del disco a cifrar debe estar preasignado

</td>

</tr>

<tr>

<td>[LVM sobre LUKS](#LVM_sobre_LUKS)

logra un particionado flexible usando LVM dentro de una única partición cifrada con LUKS.

</td>

<td>

*   Particionado sencillo con la ductilidad de LVM
*   Solo es necesaria una clave para desbloquear todos los volúmenes (por ejemplo, configuración fácil para restaurar desde disco)
*   El esquema del volumen no es transparente cuando está bloqueado  

</td>

<td>

*   LVM añade una capa y un hook adicional de mapeo
*   Poco útil si un volumen particular necesita una clave separada

</td>

</tr>

<tr>

<td>[LUKS sobre LVM](#LUKS_sobre_LVM)

utiliza dm-crypt solo después de que LVM se ha configurado.

</td>

<td>

*   LVM puede utilizarse para tener cifrado volúmenes que abarquen varios discos
*   Facilidad para mezclar grupos de volúmenes cifrados/descifrados

</td>

<td>

*   Complejo; cambiar volúmenes requiere cambiar demasiados mapeados cifrados
*   Los volúmenes requieren claves propias cada uno
*   El esquema LVM es transparente cuando está bloqueado

</td>

</tr>

<tr>

<td>[Plain dm-crypt](#Plain_dm-crypt)

utiliza la modalidad plain de dm-crypt, es decir, sin una cabecera LUKS y sus opciones para múltiples claves.  
Este escenario también permite emplear dispositivos USB para /boot y almacenamiento de claves, que se puede aplicar a los otros escenarios.

</td>

<td>

*   Capacidad de recuperación de los datos para los casos en que pueda dañarse un encabezado LUKS
*   Permite [cifrado negable](https://en.wikipedia.org/wiki/es:Deniable_encryption "wikipedia:es:Deniable encryption")

</td>

<td>

*   Es necesaria una alta competencia en todos los parámetros de cifrado
*   Clave de cifrado única y sin opción de cambiarla

</td>

</tr>

<tr>

<td>[Cifrar partición de arranque (GRUB)](#Cifrar_partici.C3.B3n_de_arranque_.28GRUB.29)

muestra cómo cifrar la partición de arranque usando el gestor de arranque GRUB.  
Este escenario también emplea una partición ESP, que se puede aplicar a los otros escenarios.

</td>

<td>

*   Las mismas ventajas que las descritas para el escenario de la instalación basada en LVM sobre LUKS (para este ejemplo en particular)
*   Se dejan menos datos sin cifrar, es decir, el gestor de arranque y la partición ESP, si está presente

</td>

<td>

*   Las mismas desventajas que las descritas para el escenario de la instalación basada en LVM sobre LUKS (para este ejemplo en particular)
*   Configuración más complicada
*   No es compatible con otros gestores de arranque

</td>

</tr>

</tbody>

</table>

Si bien todos los escenarios anteriores proporcionan una protección mucho mayor contra las amenazas externas que los sistemas de archivos cifrados secundariamente, también comparten una desventaja común: cualquier usuario en posesión de la clave de cifrado puede descifrar toda la unidad y, por lo tanto, puede acceder a los datos de otros usuarios. Si esto es motivo de preocupación, es posible utilizar una combinación de cifrado de dispositivos de bloques y sistema de archivos apilados, y recoger las ventajas de ambos. Véase [Disk encryption](/index.php/Disk_encryption "Disk encryption") para planificar las opciones.

Véase [Dm-crypt/Drive preparation#Partitioning](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation") para tener una visión general de las estrategias de particionado utilizados en los escenarios.

Otra área a considerar es si se debe configurar una partición de intercambio cifrado y de qué tipo. Véase [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") para conocer alternativas.

Si quiere avanzar en la protección de los datos del sistema no solo contra el robo físico, sino también previniéndose contra la manipulación lógica, vea [Dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties") para conocer más posibilidades después de seguir uno de los escenarios.

## Esquema de particionado simple con LUKS

Este ejemplo explica cómo cifrar un sistema completo con _dmcrypt_ + LUKS en un esquema de particionado simple::

```
+----------------------+--------------------------+------------------------------+
|Partición de arranque |Partición del sistema     |Espacio libre opcional        |
|boot                  |cifrada con LUKS          |para configurar posteriormente|
|/dev/sdaY             |/dev/sdaX                 |swap o particiones adicionales|
+----------------------+--------------------------+------------------------------+

```

Los primeros pasos se pueden realizar directamente después de arrancar la imagen de instalación de Arch Linux.

### Preparar el disco

Antes de crear las particiones, debe informarse sobre la importancia y los métodos para borrar de forma segura el disco, descrito en [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

A continuación, cree las particiones necesarias, al menos una para `/` (por ejemplo, `/dev/sdaX`) y otra para `/boot` (`/dev/sdaY`), véase [Partitioning](/index.php/Partitioning "Partitioning").

### Preparar las particiones que no son boot

Las siguientes órdenes crean y montan la partición root cifrada. Se corresponden con el proceso descrito con detalle en [Dm-crypt/Encrypting a non-root file system#Partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") (que, a pesar del título, _se puede_ aplicar a particiones root, siempre y cuando [mkinitcpio](#Configuring_mkinitcpio) y el [gestor de arranque](#Configuring_the_boot_loader) estén configurados correctamente). Si desea utilizar determinadas opciones de cifrado no predeterminadas (por ejemplo, respecto al algoritmo de cifrado, longitud de la clave, etc.), consulte [opciones de cifrado](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de ejecutar la primera orden:

```
# cryptsetup -y -v luksFormat /dev/sdaX
# cryptsetup open /dev/sdaX cryptroot
# mkfs -t ext4 /dev/mapper/cryptroot
# mount -t ext4 /dev/mapper/cryptroot /mnt

```

Compruebe que el mapeado funciona según lo previsto:

```
# umount /mnt
# cryptsetup close cryptroot
# cryptsetup open /dev/sdaX cryptroot
# mount -t ext4 /dev/mapper/cryptroot /mnt

```

Si ha creado particiones separadas (por ejemplo, `/home`), estos pasos tienen que ser adaptados y repetidos para todas ellas, a _excepción_ de `/boot`. Véase [Dm-crypt/Encrypting_a_non-root_file_system#Automated_unlocking_and_mounting](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Automated_unlocking_and_mounting "Dm-crypt/Encrypting a non-root file system") para saber cómo manejar particiones adicionales en el arranque.

Tenga en cuenta que cada dispositivo de bloque requiere su propia contraseña. Esto puede ser un inconveniente, porque da lugar a una frase de acceso separada para cada uno, que hay que introducir durante el inicio. Una alternativa es utilizar un archivo de claves almacenada en la partición del sistema para desbloquear la partición separada mediante `crypttab`. Vease [Dm-crypt/Device encryption#Using LUKS to Format Partitions_with a Keyfile](/index.php/Dm-crypt/Device_encryption#Using_LUKS_to_Format_Partitions_with_a_Keyfile "Dm-crypt/Device encryption") para obtener instrucciones.

### Preparar la partición de arranque

Lo que no se puede es configurar la partición `/boot` sin cifrar, que se necesita para una partición root cifrada. Para una partición estándar `/boot` [MBR/no-EFI](/index.php/EFI "EFI"), por ejemplo, ejecute:

```
# mkfs -t ext4 /dev/sdaY
# mkdir /mnt/boot
# mount -t ext4 /dev/sdaY /mnt/boot

```

### Montar los dispositivos

Como en [Installation guide (Español)#Montar las particiones](/index.php/Installation_guide_(Espa%C3%B1ol)#Montar_las_particiones "Installation guide (Español)"), hay que montar los dispositivos mapeados, no las particiones subyacentes. En cambio `/boot`, que no está cifrado, se monta directamente como de costumbre.

### Configurar mkinitcpio

Añada el hook `encrypt` en [mkinitcpio.conf](/index.php/Mkinitcpio "Mkinitcpio"):

 `etc/mkinitcpio.conf`  `HOOKS="... **encrypt** ... filesystems ..."` 

Dependiendo de qué otros hooks se utilizan, el orden de los mismos puede ser relevante. Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que pueda necesitar.

### Configurar el gestor de arranque

Para arrancar la partición root cifrada, el siguiente parámetro del kérnel tiene que ser pasado al gestor de arranque:

```
cryptdevice=/dev/sdaX:cryptroot

```

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para conocer más detalles y otros parmámetros que pueda necesitar.

## LVM sobre LUKS

El método sencillo es crear [LVM](/index.php/LVM "LVM") sobre la partición cifrada y no al revés. Técnicamente, LVM se configura sobre un gran dispositivo cifrado. Por lo tanto, LVM no es transparente hasta que el dispositivo de bloque se desbloquea y la estructura del volumen subyacente se escanea y se monta durante el arranque.

El esquema de particionado del disco en este ejemplo sería:

```
+------------------------------------------------------------------------------------- + +--------------+
|Volumen lógico 1        |Volumen lógico 2          |Volumen lógico3                   | |              |
|/dev/MyStorage/rootvol  |/dev/MyStorage/homevol    |/dev/MyStorage/mediavol           | | Partición    |
|_ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ | | de arranque  |
|                                                                                      | | boot         |
|                        Partición cifrada con LUKS                                    | |              |
|                               /dev/sdaX                                              | | /dev/sdaY    |
+--------------------------------------------------------------------------------------+ +--------------+

```

Este método no permite abarcar volúmenes lógicos distribuidos en varios discos, ni siquiera posteriormente. El método [#LUKS sobre LVM](#LUKS_sobre_LVM) no tiene esta limitación.

**Sugerencia:** Existen dos variantes de esta configuración:

*   Las instrucciones de [Dm-crypt/Specialties#Encrypted system using a remote LUKS header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_remote_LUKS_header "Dm-crypt/Specialties") utilizan esta configuración con un encabezado LUKS remoto sobre un dispositivo USB para lograr una autenticación de dos factores con él.
*   Las instrucciones de [Pavel Kogan's blog](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/) muestran cómo cifrar la partición `/boot` mientras se mantiene sobre la partición principal de LUKS utilizando GRUB, pero sea consciente de este fallo [FS#43663](https://bugs.archlinux.org/task/43663).
*   Las instrucciones de [Downgrading packages](/index.php/Downgrading_packages#Downgrading_the_kernel_on_a_system_using_LVM_on_LUKS "Downgrading packages") muestran cómo realizar el mantenimiento, desde la ISO, del sistema instalado.

### Preparar el disco

Antes de crear las particiones, debe informarse sobre la importancia y los métodos sobre cómo borrar de forma segura el disco, descrito en [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Cuando se utiliza el gestor de arranque [GRUB](/index.php/GRUB "GRUB") junto con [GPT](/index.php/GPT "GPT"), cree una partición BIOS boot partition como se explica en [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB").

Cree una partición con punto de montaje en `/boot`, del tipo `8300`, con un tamaño de 100 MB o más.

Cree otra partición del tipo `8E00`, en la que luego residirá el contenedor cifrado.

Cree un contenedor cifrado con LUKS en la partición del «sistema». Introduzca la contraseña elegida dos veces.

```
# cryptsetup luksFormat /dev/_sdaX_

```

Para obtener más información sobre las opciones disponibles de cryptsetup vea las [opciones de cifrado de LUKS](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de ejecutar la orden de arriba.

Abra el contenedor:

```
# cryptsetup open --type luks /dev/_sdaX_ lvm

```

El contenedor descifrado estará ahora disponible como `/dev/mapper/lvm`.

### Preparar los volúmenes lógicos

Cree un volumen físico sobre el contenedor LUKS abierto:

```
# pvcreate /dev/mapper/lvm

```

Cree un grupo de volúmenes llamado (por ejemplo) `MyStorage`, sobre el volumen físico creado con anterioridad:

```
# vgcreate MyStorage /dev/mapper/lvm

```

Cree varios volúmenes lógicos en el grupo de volúmenes:

```
# lvcreate -L 8G MyStorage -n swapvol
# lvcreate -L 15G MyStorage -n rootvol
# lvcreate -l +100%FREE MyStorage -n homevol

```

Cree un sistema de archivos para cada volumen lógico:

```
# mkfs.ext4 /dev/mapper/MyStorage-rootvol
# mkfs.ext4 /dev/mapper/MyStorage-homevol
# mkswap /dev/mapper/MyStorage-swapvol

```

Monte los sistemas de archivos:

```
# mount /dev/MyStorage/rootvol /mnt
# mkdir /mnt/home
# mount /dev/MyStorage/homevol /mnt/home
# swapon /dev/MyStorage/swapvol

```

### Preparar la partición de arranque

El gestor de arranque carga el kérnel, [initramfs](/index.php/Initramfs "Initramfs") y sus propios archivos de configuración desde el directorio `/boot`. Este directorio debe estar ubicado en un sistema de archivos separado sin cifrar.

Cree un sistema de archivos Ext2 en la partición destinada a `/boot`. Cualquier sistema de archivos que pueda ser leído por el gestor de arranque vale.

```
# mkfs.ext2 /dev/_sdaY_

```

Cree el directorio `/mnt/boot`:

```
# mkdir /mnt/boot

```

Monte la partición para `/mnt/boot`:

```
# mount /dev/_sdaY_ /mnt/boot

```

Después continúe con el proceso de instalación hasta el paso mkinitcpio.

### Configurar mkinitcpio

Agregue los hooks `encrypt` y `lvm2` a [mkinitcpio.conf](/index.php/Mkinitcpio "Mkinitcpio"):

 `/etc/mkinitcpio.conf`  `HOOKS="... **encrypt** **lvm2** ... filesystems ..."` 

**Nota:** El orden de los dos hooks ya no importa con la implementación actual de `lvm2`.

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que se puedan necesitar.

### Configurar el gestor de arranque

Con el fin de desbloquear en el arranque la partición root cifrada, es necesario pasar los siguientes parámetros del kérnel al gestor de arranque:

```
cryptdevice=/dev/_partición_:MyStorage root=/dev/mapper/MyStorage-rootvol

```

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para más detalles.

## LUKS sobre LVM

Para utilizar el cifrado sobre [LVM](/index.php/LVM "LVM"), los volúmenes LVM se establecen primero y luego se usan como base para las particiones cifradas. De esta manera, es posible mezclar particiones/volúmenes cifrados/sin cifrar. A diferencia de [#LVM sobre LUKS](#LVM_sobre_LUKS), este método permite que los volúmenes lógicos puedan abarcar con normalidad varios discos.

En el siguiente ejemplo se configura LUKS sobre LVM combinándose con el uso de un archivo de claves para la partición /home y para los volúmenes cifrados temporales como `/tmp` y `/swap`. Este último es considerado deseable desde una perspectiva de seguridad, ya que hay datos temporales que pueden contener información sensible y que sobreviven al reinicio hasta tanto se vuelve a reinicializar el cifrado. Si tiene experiencia con LVM, será capaz de ignorar/reemplazar LVM y otras especialidades de acuerdo a su propósito. Si desea extender un volumen lógico sobre múltiples discos durante la configuración, existe un procedimiento para ello que se describe en [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The intro of this scenario needs some adjustment now that a comparison has been added to [#Overview](#Overview). A suggested structure is to make it similar to the [#Simple partition layout with LUKS](#Simple_partition_layout_with_LUKS) intro. (Discuss in [Talk:Dm-crypt/Encrypting an entire system (Español)#](https://wiki.archlinux.org/index.php/Talk:Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)))

### Preparar el disco

Esquema de particionado:

*   `/dev/sda1` -> `/boot`
*   `/dev/sda2` -> LVM

Escriba aleatóriamente la partición `/dev/sda2` como indica el artículo [Dm-crypt/Drive preparation#dm-crypt_wipe_before_installation](/index.php/Dm-crypt/Drive_preparation#dm-crypt_wipe_before_installation "Dm-crypt/Drive preparation").

### Preparar los volúmenes lógicos

```
lvm pvcreate /dev/sda2
lvm vgcreate lvm /dev/sda2
lvm lvcreate -L 10G -n root lvm
lvm lvcreate -L 500M -n swap lvm
lvm lvcreate -L 500M -n tmp lvm
lvm lvcreate -l 100%FREE -n home lvm

```

```
cryptsetup luksFormat -c aes-xts-plain64 -s 512 /dev/lvm/root
cryptsetup open --type luks /dev/lvm/root root
mkreiserfs /dev/mapper/root
mount /dev/mapper/root /mnt

```

Más información acerca de las opciones de cifrado se puede encontrar en [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption"). Tenga en cuenta que `/home` será cifrada en [#Cifrar el volumen lógico /home](#Cifrar_el_volumen_l.C3.B3gico_.2Fhome). Además, observe que si alguna vez tiene que acceder a la raíz cifrada desde la ISO de Arch, la anterior acción `open` le permitirá a continuación [mostrar los volúmenes de LVM](/index.php/LVM#Logical_Volumes_do_not_show_up "LVM").

### Preparar la partición de arranque

```
dd if=/dev/zero of=/dev/sda1 bs=1M
mkreiserfs /dev/sda1
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot

```

Ahora, después de configurar el particionado LVM cifrado, sería el momento de instalar: [Arch Install Scripts](/index.php/Installation_guide#Mount_the_partitions "Installation guide").

### Configurar mkinitcpio

Añada los hooks `lvm2` y `encrypt` a [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `etc/mkinitcpio.conf`  `HOOKS="... **lvm2** **encrypt** ... filesystems ..."` 

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que se puedan necesitar.

### Configurar el gestor de arranque

Para el ejemplo anterior, cambie las opciones del kérnel en la instalación del gestor de arranque así:

```
cryptdevice=/dev/lvm/root:root root=/dev/mapper/root

```

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para conocer más detalles.

### Configurar fstab y crypttab

 `/etc/fstab` 

```
 /dev/mapper/root        /       ext4            defaults        0       1
 /dev/sda1               /boot   ext4            defaults        0       2
 /dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
 /dev/mapper/swap        none    swap            sw              0       0
```

Las siguientes opciones de [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") volverán a cifrar los sistemas de archivos temporales en cada reinicio:

 `/etc/crypttab` 

```
 swap	/dev/lvm/swap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256
 tmp	/dev/lvm/tmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256
```

### Cifrar el volúmen lógico /home

Desde este escenario se utiliza LVM como el primer mapeador y dm-crypt como el segundo, cada volumen lógico cifrado requiere su propio cifrado. Sin embargo, a diferencia de los sistemas de archivos temporales configurados con cifrado volátil anteriormente, el volumen lógico para `/home` debe ser persistente, por supuesto. Lo siguiente asume que se ha reiniciado al sistema instalado, de lo contrario se tienen que ajustar las rutas. Para asegurarnos de que se introduce una segunda frase de acceso en el arranque para dicho volumen, creamos un [archivo de claves](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") :

```
mkdir -m 700 /etc/luks-keys
dd if=/dev/random of=/etc/luks-keys/home bs=1 count=256

```

El volumen lógico se cifra con dicho archivo de clave:

```
cryptsetup luksFormat -v -s 512 /dev/lvm/home /etc/luks-keys/home
cryptsetup -d /etc/luks-keys/home open --type luks /dev/lvm/home home
mkfs -t ext4 /dev/mapper/home
mount /dev/mapper/home /home

```

El punto de montaje cifrado será configurado en [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration"):

 `/etc/crypttab`  `home	/dev/lvm/home   /etc/luks-keys/home`  `/etc/fstab`  `/dev/mapper/home        /home   ext4        defaults        0       2` 

y ya está terminada la configuración.

Si en el futuro desea ampliar el volumen lógico para `/home` (o cualquier otro volumen), es importante tener en cuenta que la parte cifrada con LUKS tiene que ser redimensionada también. Para conocer un procedimiento vea [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

## LUKS sobre RAID por software

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Some references: [RAID](/index.php/RAID "RAID"), [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM"), [http://jasonwryan.com/blog/2012/02/11/lvm/](http://jasonwryan.com/blog/2012/02/11/lvm/) (Discuss in [Talk:Dm-crypt/Encrypting an entire system (Español)#](https://wiki.archlinux.org/index.php/Talk:Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)))

## Plain dm-crypt

Este escenario configura un sistema en un disco completo sobre dm-crypt con la modalidad de cifrado _plain_. Tenga en cuenta que para la mayoría de los casos al uso, los métodos que utilizan LUKS descritas anteriormente son las mejores opciones para el cifrado del sistema y las particiones cifradas. Características de LUKS como la gestión de claves con múltiples pass-phrases/key-files no están disponibles con la modalidad _plain_.

La modalidad _plain_ de dm-crypt no requiere una cabecera en el disco cifrado: esto significa que un disco cifrado sin particionar será indistinguible de un disco lleno con datos aleatorios, que es el atributo deseado para este escenario. Véase también [Wikipedia:Deniable encryption](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption").

Los discos cifrados con dm-crypt _plain_ pueden ser más resistentes a los daños que los discos cifrados con LUKS, ya que no se basan en una clave maestra de cifrado la cual constituye un punto único de fallo si se daña. Sin embargo, utilizando el modo _plain_ también se requiere una configuración más manual de las opciones de cifrado para lograr la misma fuerza criptográfica. Véase también [Disk encryption#Cryptographic metadata](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption").

**Tip:** Si el cifrado sin cabeceras es su objetivo, pero no está seguro acerca de la falta de derivación de clave con el modo _plain_, entonces dispone de dos alternativas:

*   [tcplay](/index.php/Tcplay "Tcplay") que ofrece cifrado sin cabeceras, pero con la función PBKDF2, o
*   la modalidad LUKS de dm-crypt utilizando la opción `--header` de _cryptsetup_. No se podrá utilizar el hook estándar _encrypt_, pero dicho hook [puede ser modificado](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_remote_LUKS_header "Dm-crypt/Specialties").

El escenario utiliza una memoria USB para el dispositivo de arranque y otra para almacenar la clave de cifrado. El esquema de particionado del disco es:

```
+--------------------+------------------+--------------------+ +---------------------+ +---------------------+
|Volumen 1:          |Volumen 2:        |Volumen 3:          | |Dispositivo de       | |Almacen para archivo |
|                    |                  |                    | |Arranque             | |de claves cifradas   |
|root                |swap              |home                | |/boot                | |(sin particionar     |
|                    |                  |                    | |                     | |en el ejemplo)       |
|/dev/store/root     |/dev/store/swap   |/dev/store/home     | |/dev/sdY1            | |/dev/sdZ             |
|--------------------+------------------+--------------------| |---------------------| |---------------------|
|unidad /dev/sdaX cifrada usando modalidad plain y LVM       | |Lápiz USB 1          | |Lápiz USB 2          |
+------------------------------------------------------------+ +---------------------+ +---------------------+

```

`/boot` y el gestor de arranque no pueden ser guardados en la unidad cifrada, a menos que se anule el propósito de utilizar el modo _plain_ para el cifrado negable. Esto también permite almacenar las opciones necesarias para abrir/desbloquear el dispositivo cifrado plain en la configuración del gestor de arranque, ya que escribiéndolos en cada arranque sería propenso a errores.

Este escenario también utiliza un archivo de clave, suponiendo que se almacena como bits sin procesar en una segunda memoria USB, de modo que a los ojos de un atacante este ignorará que está delante de la memoria usb-llave por que la clave de cifrado aparecerá en forma de datos aleatorios en lugar de ser visible como un archivo normal. Véase también [Wikipedia:Security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity"), y [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") para preparar el archivo de claves.

**Sugerencia:**

*   También es posible utilizar una sola llave USB mediante la copia del archivo de claves a la initram directamente. Un ejemplo de archivo de claves `/etc/keyfile` copiado a la imagen initram se hace estableciendo `FILES="/etc/keyfile"` en `/etc/mkinitcpio.conf`. La manera de instruir al hook `encrypt` para que lea el archivo de claves en la imagen initram es utilizando el prefijo `rootfs:` delante del nombre del archivo, por ejemplo `cryptkey=rootfs:/etc/keyfile`.
*   Otra opción es usar una frase de acceso con buena [entropía](/index.php/Disk_encryption#Choosing_a_strong_passphrase "Disk encryption").

### Preparar el disco

Es de vital importancia que el dispositivo mapeado está lleno de datos. En particular, esto se aplica al caso que nos afecta.

Véase [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") y [Dm-crypt/Drive preparation#dm-crypt_specific_methods](/index.php/Dm-crypt/Drive_preparation#dm-crypt_specific_methods "Dm-crypt/Drive preparation")

### Preparar las particiones que no son boot

Véase [Dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") para más detalles.

Utilizando el dispositivo `/dev/sd_X_`, cifrándolo con [twofish](https://en.wikipedia.org/wiki/es:Twofish "wikipedia:es:Twofish") en modo xts, con un tamaño de clave de 512 bit y el uso de un archivo de claves, se tienen las siguientes opciones para este escenario:

 `# cryptsetup --hash=sha512 --cipher=twofish-xts-plain64 --offset=0 --key-file=/dev/sd_Z_ --key-size=512 open --type=plain /dev/sdX enc` 

A diferencia del cifrado LUKS, la orden anterior debe ejecutarse en _su totalidad_ cada vez que el mapeo tiene que ser reestablecido, por lo que es importante tener en cuenta el cifrado, hash y el archivo de claves detallados.

Ahora podemos comprobar que la entrada del mapeado se ha hecho para `/dev/mapper/enc`:

```
# fdisk -l

```

A continuación, configure los volúmenes lógicos de [LVM](/index.php/LVM "LVM") sobre el dispositivo mapeado, véase [Lvm#Installing_Arch_Linux_on_LVM](/index.php/Lvm#Installing_Arch_Linux_on_LVM "Lvm") para más detalles:

```
# pvcreate /dev/mapper/enc
# vgcreate store /dev/mapper/enc
# lvcreate -L 20G store -n root
# lvcreate -C y -L 10G store -n swap
# lvcreate -l +100%FREE store -n home

```

Para formatear y montar los volúmenes, así como activar el espacio de intercambio, véase [File systems#Format a device](/index.php/File_systems#Format_a_device "File systems") para más detalles:

```
# mkfs.ext4 /dev/store/root
# mkfs.ext4 /dev/store/home
# mount /dev/store/root /mnt
# mkdir /mnt/home
# mount /dev/store/home /mnt/home
# mkswap /dev/store/swap
# swapon /dev/store/swap

```

### Preparar la partición de arranque

La partición `/boot` se puede instalar en la partición vfat estándar de una memoria USB, si es necesario. Pero si se ve en la necesidad de realizar el particionado manualmente, entonces podría crear una pequeña partición de 200MB, lo que sería suficiente. Cree la partición utilizando una [utilidad de particionado](/index.php/Partitioning#Partitioning_tools "Partitioning") de su elección.

Elegimos un sistema de archivos no journalling para preservar la memoria flash de la partición `/boot`, si no está ya formateada como vfat:

```
# mkfs.ext2 /dev/sd_Y_1
# mkdir /mnt/boot
# mount /dev/sd_Y_1 /mnt/boot

```

### Configurar mkinitcpio

Agregue los hooks `encrypt` y `lvm2` a [mkinitcpio.conf](/index.php/Mkinitcpio "Mkinitcpio"):

 `etc/mkinitcpio.conf`  `HOOKS="... **encrypt** **lvm2** ... filesystems ..."` 

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para conocer más detalles y otros hooks que pueda necesitar.

### Configurar el gestor de arranque

Para arrancar la partición de root cifrada, los siguientes parámetros del kérnel son necesarios pasarlos al gestor de arranque:

```
cryptdevice=/dev/sd_X_:enc cryptkey=/dev/sd_Z_:0:512 crypto=sha512:twofish-xts-plain64:512:0:

```

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para conocer más detalles y otros parámetros que puede necesitar

**Tip:** Si se utiliza GRUB, puede instalarlo en el mismo USB como partición `/boot` con:

```
# grub-install --recheck /dev/sd_Y_

```

### Posinstalación

Podemos retirar la memoria USB después de arrancar. Ya que la partición `/boot`, generalmente, no se necesita, la opción `noauto` se puede agregar en la línea correspondiente de `/etc/fstab`:

 `/etc/fstab` 

```
# /dev/sd_Yn_
/dev/sdYn /boot ext2 **noauto**,rw,noatime 0 2
```

Sin embargo, cuando se requiere una actualización del kérnel o del cargador de arranque, la partición `/boot` debe estar presente y montada. Como la entrada en `fstab` ya existe, se puede montar de forma sencilla con:

```
# mount /boot

```

## Cifrar partición de arranque (GRUB)

Esta configuración utiliza el mismo diseño de partición y configuración que para la partición raíz del sistema en la sección anterior [#LVM sobre LUKS](#LVM_sobre_LUKS), con dos claras diferencias:

1.  La configuración se realiza para un sistema [UEFI](/index.php/UEFI "UEFI"), y
2.  Una característica especial del gestor de arranque [GRUB](/index.php/GRUB "GRUB") es utilizada para cifrar adicionalmente la partición de arranque `/boot`. Vea también [GRUB (Español)#Partición de arranque](/index.php/GRUB_(Espa%C3%B1ol)#Partici.C3.B3n_de_arranque "GRUB (Español)").

La distribución del disco en este ejemplo es:

```
+--------------------+----------------------+----------------+----------------+----------------+
|Partición ESP:      |Partición de arranque:|Volumen 1:      |Volumen 2:      |Volumen 3:      |
|                    |                      |                |                |                |
|/boot/efi           |/boot                 |root            |swap            |home            |
|                    |                      |                |                |                |
|                    |                      |/dev/store/root |/dev/store/swap |/dev/store/home |
|/dev/sdaX           |/dev/sdaY             +----------------+----------------+----------------+
|**des**cifrado          |cifrado con LUKS      |/dev/sdaZ cifrado utilizando LVM sobre LUKS       |
+--------------------+----------------------+--------------------------------------------------+

```

**Tip:** Todos los escenarios tienen el propósito de ejemplos. Es, por supuesto, posible combinar los dos pasos anteriores de las distintas instalaciones con otros escenarios posibles. Ver también las variantes asociadas a [#LVM sobre LUKS](#LVM_sobre_LUKS).

### Preparar el disco

Antes de crear las particiones, debe informarse sobre la importancia y los métodos para borrar de forma segura el disco, descrito en [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Cree una [EFI System Partition (ESP)](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") con un tamaño adecuado, que más tarde se montará en `/boot/efi`.

Cree una partición para montar en `/boot`, del tipo `8300`, con un tamaño de 100 MB o más.

**Sugerencia:** Si utilizamos el gestor de arranque [GRUB](/index.php/GRUB "GRUB") junto con un sistema BIOS/[GPT](/index.php/GPT "GPT"), hay que crear una BIOS boot partition como se explica en [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB"), en lugar de la ESP.

Cree una partición del tipo `8E00`, que más tarde va a contener el contenedor cifrado.

Cree el contenedor cifrado con LUKS en la partición del «sistema».

```
# cryptsetup luksFormat /dev/_sdaZ_

```

Para obtener más información sobre las opciones disponibles de cryptsetup vea [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de ejecutar la orden anterior.

Su esquema de particinado debería ser similar a esto:

 ` gdisk /dev/sda ` 

```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem
   3         1460224        41943006   19.3 GiB    8E00  Linux LVM

```

Abra el contenedor:

```
# cryptsetup open --type luks /dev/_sdaZ_ lvm

```

El contenedor desbloqueado estará ahora disponible como `/dev/mapper/lvm`.

### Preparar los volúmenes lógicos

Los volúmenes lógicos LVM de este ejemplo siguen el mismo esquema descrito en el escenario anterior. Por lo tanto, siga la sección [Preparar los volúmenes lógicos](#Preparar_los_vol.C3.BAmenes_l.C3.B3gicos) de arriba o haga los ajustes necesarios.

### Preparar la partición de arranque

El gestor de arranque carga el kérnel, [initramfs](/index.php/Initramfs "Initramfs") y sus propios archivos de configuración desde el directorio `/boot`.

En primer lugar, cree el contenedor LUKS donde estarán ubicados e instalados los archivos:

```
# cryptsetup luksFormat /dev/sda_Y_ 

```

A continuación, ábralo:

```
# cryptsetup open /dev/sda_Y_ cryptboot 

```

Cree un sistema de archivos en la partición destinada a `/boot`. Cualquier sistema de archivos que puede ser leído por el gestor de arranque es elegible:

```
# mkfs.ext2 /dev/mapper/_cryptboot_

```

Cree el directorio `/mnt/boot`:

```
# mkdir /mnt/boot

```

Monte la partición para `/mnt/boot`:

```
# mount /dev/mapper/_cryptboot_ /mnt/boot

```

Cree el punto de montaje para la [ESP](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") en `/boot/efi` para que sea compatible con `grub-install`, y móntela:

```
# mkdir /mnt/boot/efi
# mount /dev/_sdbX_ /mnt/boot/efi

```

En este punto, debe tener las siguientes particiones y volúmenes lógicos dentro de `/mnt`:

 `lsblk` 

```
NAME              	  MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                       8:0      0   200G  0 disk  
├─sda1                    8:1      0   512M  0 part  /boot/efi
├─sda2                    8:2      0   200M  0 part  
│ └─boot		  254:0    0   198M  0 crypt /boot
└─sda3                    8:3      0   100G  0 part  
  └─lvm                   254:1    0   100G  0 crypt 
    ├─MyStorage-swapvol   254:2    0     8G  0 lvm   [SWAP]
    ├─MyStorage-rootvol   254:3    0    15G  0 lvm   /
    └─MyStorage-homevol   254:4    0    77G  0 lvm   /home

```

Luego, continue con el procedimiento de instalación hasta el paso de mkinitcpio.

### Configurar mkinitcpio

Añada los hooks `encrypt` y `lvm2` a [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS="... **encrypt** **lvm2** ... filesystems ..."` 

Véase [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para más detalles y otros hooks que pueda necesitar.

### Configurar el gestor de arranque

Con el fin de desbloquear la partición raíz cifrada en el arranque, los siguientes parámetros del kérnel hay que pasarlos al gestor de arranque:

```
cryptdevice=/dev/_partition_:MyStorage root=/dev/mapper/MyStorage-rootvol

```

Véase [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para obtener más detalles.

Ahora, preparamos la instalación del gestor de arranque GRUB para que reconozca la partición `/boot` cifrada con LUKS de acuerdo con [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB").

Abra `/etc/default/grub` y añada el parámetro siguiente al final:

`GRUB_ENABLE_CRYPTODISK=y`

Cree el archivo de configuración del menú de GRUB:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

[Instale GRUB](/index.php/GRUB#Installation_2 "GRUB") para la ESP montada:

```
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub --recheck

```

Si todo terminó sin errores, GRUB le pedirá la contraseña para desbloquear la partición `/boot` en el siguiente reinicio.

### Configurar fstab y crypttab

Esta sección trata de la configuración extra para dejar que el sistema _monte_ `/boot` cifrado.

Mientras GRUB pide una contraseña para desbloquear la partición `/boot` cifrada, siguiendo las instrucciones anteriores, el desbloqueo de la partición no se transmite a los initramfs. Por lo tanto, `/boot` no estará disponible después de que el sistema haya re/iniciado, porque el hook `encrypt` solo desbloquea la raíz del sistema.

Si ha utilizado el script _genfstab_ durante la instalación, se habrán generado ya en `/etc/fstab` las entradas para el montaje de `/boot` y `/boot/efi`, pero el sistema no podrá encontrar el mapeador de dispositivos generado por la partición de arranque. Para que esté disponible, agréguelo a [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration"). Por ejemplo:

 `/etc/crypttab`  `cryptboot  /dev/sdaY      none        luks` 

lo que hará que el sistema pida la contraseña de nuevo (es decir, tiene que introducir dos veces la contraseña en el arranque: una vez para GRUB y otra para la inicialización de systemd). Para evitar la repetición de la contraseña para desbloquear `/boot`, siga las instrucciones descritas en [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"):

1.  cree un [archivo de claves de texto aleatorio](/index.php/Dm-crypt/Device_encryption#Storing_the_keyfile_on_a_filesystem "Dm-crypt/Device encryption");
2.  añada el archivo de claves a la [cabecera LUKS de la partición boot](/index.php/Dm-crypt/Device_encryption#Configuring_LUKS_to_make_use_of_the_keyfile "Dm-crypt/Device encryption") (`/dev/sdaY`), y
3.  compruebe la entrada `/etc/fstab` y añada la línea `/etc/crypttab` para [desbloquearla automáticamente en el arranque](/index.php/Dm-crypt/Device_encryption#Unlock_at_boot "Dm-crypt/Device encryption").

Si por alguna razón el archivo de claves no puede desbloquear la partición de arranque, systemd se repliega para pedir una contraseña para desbloquear y, en caso de que sea correcta, continuar el arranque.

**Sugerencia:** Pasos opcionales posinstalación:

*   Puede que valga la pena considerar añadir el gestor de arranque GRUB a la lista de ignorados en `/etc/pacman.conf` con el fin de atender de forma especial el control de cuándo el gestor de arranque (que incluye sus propios módulos de cifrado) se actualiza.
*   Si desea cifrar la partición `/boot` para protegerse contra amenazas de manipulación offline, el hook [mkinitcpio-chkcryptoboot](/index.php/Dm-crypt/Specialties#mkinitcpio-chkcryptoboot "Dm-crypt/Specialties") puede serle de ayuda.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_an_entire_system_(Español)&oldid=415635](https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_an_entire_system_(Español)&oldid=415635)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Encryption (Español)](/index.php/Category:Encryption_(Espa%C3%B1ol) "Category:Encryption (Español)")
*   [File systems (Español)](/index.php/Category:File_systems_(Espa%C3%B1ol) "Category:File systems (Español)")
*   [Getting and installing Arch (Español)](/index.php/Category:Getting_and_installing_Arch_(Espa%C3%B1ol) "Category:Getting and installing Arch (Español)")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")