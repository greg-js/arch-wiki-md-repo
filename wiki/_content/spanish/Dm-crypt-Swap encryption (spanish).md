**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

[Preparar dispositivo](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") – [Cifrar dispositivo](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol) "Dm-crypt/Device encryption (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") – <a class="mw-selflink selflink">Cifrar espacio de intercambio</a> – [Montar y acceder a /home cifrado](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)") – [Configurar el sistema](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)") – [Especialidades](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol) "Dm-crypt/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption"), revisada por última vez el **2018-10-19**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/Swap_encryption&diff=0&oldid=548465) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Dependiendo de los requisitos, se pueden usar diferentes métodos para cifrar la partición [de intercambio](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)"), los cuales se describen a continuación. Una configuración en la que el cifrado del espacio de intercambio se reinicializa en cada arranque (con un nuevo cifrado) proporciona una mayor protección de datos, ya que evita los fragmentos de archivos confidenciales que pueden haber sido intercambiados hace tiempo sin sobrescribirlos. Sin embargo, volver a cifrar el espacio de intercambio también inhibe el uso de una función de suspensión en disco en general.

## Contents

*   [1 Sin soporte para suspensión en disco](#Sin_soporte_para_suspensión_en_disco)
    *   [1.1 UUID y LABEL](#UUID_y_LABEL)
*   [2 Con soporte para suspensión en disco](#Con_soporte_para_suspensión_en_disco)
    *   [2.1 LVM sobre LUKS](#LVM_sobre_LUKS)
    *   [2.2 Hook de mkinitcpio](#Hook_de_mkinitcpio)
    *   [2.3 Utilizar un archivo de intercambio](#Utilizar_un_archivo_de_intercambio)
*   [3 Problemas conocidos](#Problemas_conocidos)

## Sin soporte para suspensión en disco

En los sistemas en los que la suspensión en disco (hibernación) no es una función deseada, se puede configurar `/etc/crypttab` para descifrar la partición de intercambio con una contraseña aleatoria en el momento del arranque con la modalidad plain de dm-crypt. La contraseña aleatoria se descarta al cerrarse, dejando solo datos cifrados e inaccesibles en el dispositivo de intercambio.

Para activar esta función, simplemente elimine el comentario de la línea que comienza con `swap` en `/etc/crypttab`. Cambie el parámetro `<dispositivo>` con el nombre de su dispositivo de intercambio. Por ejemplo, se verá algo como esto:

 `/etc/crypttab` 
```
# <name>  <device>     <password>     <options>
swap      /dev/sd*X#*    /dev/urandom   swap,cipher=aes-xts-plain64,size=256
```

Esto mapeará `/dev/sd*X#*` en `/dev/mapper/swap` como una partición de intercambio que se puede agregar en `/etc/fstab` como un espacio de intercambio normal. Si antes tenía una partición de intercambio no cifrada, no olvide desactivarla, o reutilice la entrada de [fstab](/index.php/Fstab "Fstab") cambiando el dispositivo a `/dev/mapper/swap`. Las opciones predeterminadas deben ser suficientes para la mayoría al uso. Para otras opciones y una explicación de cada columna, vea [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5) así como [point cryptsetup FAQ 2.3](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup).

**Advertencia:** Todo el contenido del dispositivo nombrado se **eliminará** permanentemente. Es peligroso usar el nombre simple dado por el kernel para un dispositivo de intercambio, ya que el orden de su nombre (*por ejemplo* `/dev/sda`, `/dev/sdb`) cambia en cada arranque . Las opciones son:

*   Utilice las rutas `by-id` y `by-path`. Sin embargo, ambos son susceptibles a los cambios de hardware. Consulte [Persistent block device naming (Español)#by-id y by-path](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-id_y_by-path "Persistent block device naming (Español)").
*   Use el nombre del volumen lógico [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)").
*   Utilice el método descrito en [#UUID y LABEL](#UUID_y_LABEL). Las etiquetas (label) y [UUIDS](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)") **no pueden** utilizarse directamente debido a la recreación y recifrado del dispositivo de intercambio en cada inicio con `mkswap`, consulte [FAQ de cryptsetup](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup).

Para usar un nombre de dispositivo persistente `by-id` en lugar del nombre simple dado por el kernel, primero identifique el dispositivo de intercambio:

 `# find -L /dev/disk -samefile /dev/*sdaX*` 
```
/dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part*X*
/dev/disk/by-id/wwn-0x60015ee0000b237f-part*X*

```

Luego utilice como una referencia persistente para la partición de ejemplo `/dev/sd*X#*` (si se devuelven dos resultados como lo anterior, elija uno de ellos):

 `/etc/crypttab` 
```
# <name>  <device>                                                         <password>     <options>
swap      /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-partX  /dev/urandom   swap,cipher=aes-cbc-essiv:sha256,size=256
```

Después de reiniciar para activar el espacio intercambio cifrado, observará que al ejecutar la orden `swapon -s` se muestra una entrada de mapeado de dispositivo arbitraria (por ejemplo, `/dev/dm-1`), mientras que la orden `lsblk` muestra **crypt** en la columna `FSTYPE`. Debido a que se cifra en cada inicio, el UUID para `/dev/mapper/swap` cambiará cada vez.

**Nota:** Si la partición elegida para el intercambio era anteriormente una partición LUKS, crypttab no sobrescribirá la partición para crear una partición de intercambio. Esta es una medida de seguridad para evitar la pérdida de datos por una identificación errónea accidental de la partición de intercambio en crypttab. Para utilizar una partición de este tipo, el [encabezado LUKS debe sobrescribirse](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol)#Limpiar_el_encabezado_LUKS "Dm-crypt/Drive preparation (Español)") al menos una vez.

### UUID y LABEL

Es peligroso utilizar el espacio intercambio en el archivo crypttab con los simples nombres de los dispositivos proporcionados por el kernel tales como `/dev/sdX#` o incluso `/dev/disk/by-id/ata-SERIAL-partX`. Un pequeño cambio en los nombres de los dispositivos o en el diseño de la partición y `/etc/crypttab` hará que sus valiosos datos sean formateados en el próximo arranque. Lo mismo cabe decir si usa PARTUUID y luego decide usar esa partición para otra cosa sin eliminar primero su entrada en crypttab.

Es más confiable identificar la partición correcta al darle un UUID o ETIQUETA (LABEL en inglés) genuino. Por defecto, eso no funciona porque dm-crypt y `mkswap` simplemente sobrescribirían cualquier contenido en esa partición que eliminaría también el UUID y el LABEL; sin embargo, es posible especificar un [offset](https://en.wikipedia.org/wiki/es:Offset_(inform%C3%A1tica) (desplazamiento) para el espacio de intercambio. Esto permite crear un sistema de archivos muy pequeño, vacío y falso, sin otro propósito que el de proporcionar un UUID o una ETIQUETA persistentes para el cifrado del espacio intercambio.

Cree un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") con la etiqueta («*L* de *label*») de su elección:

```
# mkfs.ext2 -L *cryptswap* /dev/sd*X#* 1M

```

El parámetro poco habitual que hay después del nombre del dispositivo, limita el tamaño del sistema de archivos a 1 MiB, dejando un hueco para el espacio de intercambio cifrado.

 `# blkid /dev/sdX#`  `/dev/sdX#: LABEL="cryptswap" UUID="b72c384e-bd3c-49aa-b7a7-a28ea81a2605" TYPE="ext2"` 

Con esto, `/dev/sdX#` puede ahora ser identificado fácilmente por su UUID o LABEL, independientemente de cómo pueda cambiar en el futuro el nombre del dispositivo o incluso el número de la partición. Lo relevante serán dichas entradas en `/etc/crypttab` y `/etc/fstab`:

 `/etc/crypttab` 
```
# <name> <device>         <password>    <options>
swap     LABEL=*cryptswap*  /dev/urandom  swap,offset=2048,cipher=aes-xts-plain64,size=512
```

Nota sobre offset: este espacio es de 2048 sectores de 512 bytes, por lo tanto 1 MiB. De esta manera, el espacio de intercambio que se cifrará no afectará al UUID/LABEL del sistema de archivos (que queda dentro del espacio offset), y la alineación de los datos también funcionará.

 `/etc/fstab` 
```
# <filesystem>    <dir>  <type>  <options>  <dump>  <pass>
/dev/mapper/swap  none   swap    defaults   0       0
```

Usando esta configuración, el cifrado del espacio de intercambio solo intentará usar la partición con la ETIQUETA («*LABEL*») correspondiente, independientemente de cuál sea el nombre del dispositivo. En caso de que decida utilizar la partición para otra cosa, al formatearla también se eliminará el LABEL utilizado para el crifrado, por lo que cryptswap no lo sobrescribirá en su próximo arranque.

## Con soporte para suspensión en disco

Para poder reanudar después de suspender el equipo en el disco (hibernación), es necesario mantener el espacio de intercambio intacto. Por lo tanto, se requiere tener una partición o archivo de intercambio preexistente cifrado con LUKS, que se pueda almacenar en el disco o ingresar manualmente al reanudar.

Los siguientes tres métodos son alternativas para configurar un espacio de intercambio cifrado para suspender en disco. Si aplica alguno de ellos, tenga en cuenta que los datos críticos intercambiados por el sistema pueden permanecer en el espacio de intercambio durante un período de tiempo prolongado (es decir, hasta que se vuelva a sobrescribir). Para reducir este riesgo, considere configurar un «*job*» (trabajo) del sistema que vuelva a cifrar el espacio de intercambio, por ejemplo, cada vez que el sistema entre en un cierre regular, junto con el método de su elección.

### LVM sobre LUKS

Una forma sencilla de realizar un espacio de intercambio cifrado con soporte para suspensión en disco es mediante el uso de un dispositivo de intercambio [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") en la misma capa de cifrado que el volumen raíz, de modo que ambos se abren mediante el hook `encrypt` en el arranque. Siga las instrucciones de [Dm-crypt/Encrypting an entire system (Español)#LVM sobre LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LVM_sobre_LUKS "Dm-crypt/Encrypting an entire system (Español)") y luego configure los [parámetros de kernel necesarios](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate").

Suponiendo que ha configurado LVM sobre LUKS con un volumen lógico de intercambio (en `/dev/MyStorage/swap` por ejemplo), todo lo que debe hacer es agregar el hook **resume** a [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") y añadir el parámetro del kernel `resume=/dev/MyStorage/swap` a su cargador de arranque. Para [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), esto se puede hacer agregando la variable a la línea `GRUB_CMDLINE_LINUX_DEFAULT` en `/etc/default/grub`:

 ` / etc / default / grub `  `GRUB_CMDLINE_LINUX_DEFAULT = "... resume = / dev / MyStorage / swap"` 

luego ejecute `grub-mkconfig -o /boot/grub/grub.cfg` para actualizar el archivo de configuración de GRUB. Para agregar el hook a mkinitcpio, modifique la siguiente línea en el archivo `mkinitcpio.conf`:

 `/etc/mkinitcpio.conf`  `HOOKS=(... encrypt lvm2 **resume** ... filesystems ...)` 

después [regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

### Hook de mkinitcpio

**Nota:** Esta sección solo es aplicable cuando se utiliza el hook `encrypt`, que solo puede desbloquear un único dispositivo ([FS#23182](https://bugs.archlinux.org/task/23182)). Con `sd-encrypt` se pueden desbloquear varios dispositivos (consulte [Dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration")), pero la autodetección del espacio de intercambio aún no está disponible. [número de systemd 4878](https://github.com/systemd/systemd/issues/4878)

Si el dispositivo de intercambio está en un dispositivo diferente al del sistema de archivos raíz, no se abrirá con el hook `encrypt`, es decir, la reanudación se realizará antes de que `/etc/crypttab` se pueda usar, por lo tanto, se requiere crear un hook en `/etc/mkinitcpio.conf` para abrir el dispositivo de intercambio LUKS antes de reanudar.

Si desea usar una partición que actualmente esté usando el sistema, primero debe desactivarla:

```
# swapoff /dev/<dispositivo>

```

También debe asegurarse de eliminar cualquier línea en `/etc/crypttab` que apunte a dicho dispositivo.

Si está reutilizando una [partición](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") de intercambio existente, y si la partición está en una tabla de particionado GPT, necesitará usar [gdisk](/index.php/Gdisk "Gdisk") para ajustar el [atributo 63 de la partición para «que no se monte automáticamente»](/index.php/Gdisk#Prevent_GPT_partition_automounting "Gdisk") en ella. Esto evitará que systemd-gpt-auto-generator descubra y active la partición en el arranque.

La siguiente configuración tiene la desventaja de tener que insertar una contraseña adicional para la partición de intercambio manualmente en cada arranque.

**Advertencia:** No utilice esta configuración con un archivo de claves si `/boot` no está cifrado. Lea acerca del problema reportado [aquí](https://wiki.archlinux.org/index.php?title=Talk:Dm-crypt&oldid=255742#Suspend_to_disk_instructions_are_insecure). Alternativamente, use un archivo de claves cifrado con gnupg según [https://bbs.archlinux.org/viewtopic.php?id=120181](https://bbs.archlinux.org/viewtopic.php?id=120181)

Para formatear el contenedor encriptado, destinado a la partición de intercambio, cree un ranura de clave («*keyslot*») para una frase de contraseña memorizable por el usuario.

```
# cryptsetup luksFormat --type luks2 /dev/<dispositivo>

```

Abra la partición en `/dev/mapper`:

```
# cryptsetup open /dev/<dispositivo> swapDevice

```

Cree un sistema de archivos de intercambio en la partición mapeada:

```
# mkswap /dev/mapper/swapDevice

```

Ahora tiene que crear un hook para abrir el espacio de intercambio en el momento del arranque. Puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") y configurar [mkinitcpio-openswap](https://aur.archlinux.org/packages/mkinitcpio-openswap/), o seguir las siguientes instrucciones. Cree un archivo de hook que contenga la orden de abrir:

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    cryptsetup open /dev/<dispositivo> swapDevice
}

```

para abrir el dispositivo de intercambio escribiendo su contraseña o

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    ## Optional: To avoid race conditions
    x=0;
    while [ ! -b /dev/mapper/<root-device> ] && [ $x -le 10 ]; do
       x=$((x+1))
       sleep .2
    done
    ## End of optional

    mkdir crypto_key_device
    mount /dev/mapper/<root-device> crypto_key_device
    cryptsetup open --key-file crypto_key_device/<path-to-the-key> /dev/<device> swapDevice
    umount crypto_key_device
}

```

para abrir el dispositivo de intercambio cargando un archivo de claves desde un dispositivo raíz cifrado.

En algunos equipos, las condiciones de velocidad pueden hacer que mkinitcpio intente montar el dispositivo antes de que se complete el proceso de descifrado y de numeración del dispositivo. El bloque *Optional* comentado retrasará el proceso de arranque hasta 2 segundos, momento en el que el dispositivo raíz estará listo para montarse.

**Nota:** Si el espacio de intercambio está en un disco de estado sólido (SSD) y se desea utilizar la orden Discard/[TRIM](https://en.wikipedia.org/wiki/es:TRIM "wikipedia:es:TRIM"), la opción `--allow-discards` debe agregarse a la línea de cryptsetup antes del hook openswap. Consulte [Dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties") o [Solid state drive](/index.php/Solid_state_drive "Solid state drive") para obtener más información sobre «discard». Además, debe agregar la opción de montaje 'discard' a su entrada de fstab para el dispositivo de intercambio.

Luego cree y edite el archivo de configuración del hook:

 `/etc/initcpio/install/openswap` 
```
build ()
{
   add_runscript
}
help ()
{
cat<<HELPEOF
  Esto abre la partición de intercambio cifrada /dev/<dispositivo> en /dev/mapper/swapDevice
HELPEOF
}

```

Agregue el hook `openswap` en la matriz `HOOKS` en el archivo `/etc/mkinitcpio.conf`, antes de `filesystem` pero después de `encrypt`. No olvide agregar el hook `resume` después de `openswap`.

```
HOOKS=(... encrypt openswap resume filesystems ...)

```

[Regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

Añada la partición mapeada a `/etc/fstab` agregando la siguiente línea:

```
/dev/mapper/swapDevice swap swap defaults 0 0

```

Configure su sistema para reanudar desde `/dev/mapper/swapDevice`. Por ejemplo, si usa [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") con el soporte de hibernación del kernel, añada el parámetro del kernel `resume=/dev/mapper/swapDevice` a GRUB en la línea `GRUB_CMDLINE_LINUX_DEFAULT` del archivo `/etc/default/grub`. Una línea del kernel con particiones raíz y de intercambio cifradas puede verse así:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/swapDevice ro

```

En el momento del arranque, el hook `openswap` abrirá la partición de intercambio, por lo que se podrá usar la «reanudación» del kernel. Si utiliza hook especiales para reanudar desde la hibernación, asegúrese de que estén colocados **después de** `openswap` en la matriz `HOOKS`. Tenga en cuenta que debido a la apertura del espacio de intercambio de initrd, no es necesaria ninguna entrada para swapDevice en `/etc/crypttab` en este caso.

### Utilizar un archivo de intercambio

Se puede utilizar un archivo de intercambio para reservar un espacio de intercambio dentro de una partición existente y también se puede configurar dentro de una partición cifrada. Al reanudar desde un archivo de intercambio, se debe proporcionar el hook `resume` con la contraseña para desbloquear el dispositivo donde se encuentra el archivo de intercambio.

**Advertencia:** [Btrfs](/index.php/Dm-crypt/Drive_preparation#Btrfs_subvolumes "Dm-crypt/Drive preparation") no admite archivos de intercambio. Si no se toma en cuenta esta advertencia, se puede dañar el sistema de archivos. Si bien se puede usar un archivo de intercambio en [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") cuando se monta a través de un dispositivo loop, esto dará como resultado un rendimiento de intercambio muy degradado.

Para crearlo, primero elija una partición mapeada (por ejemplo, `/dev/mapper/rootDevice`) cuyo sistema de archivos montado (por ejemplo, en `/`) contenga suficiente espacio libre como para crear un archivo de intercambio con el tamaño deseado.

Ahora [cree el archivo de intercambio](/index.php/Swap_(Espa%C3%B1ol)#Creación_de_un_archivo_swap "Swap (Español)") (por ejemplo, `/swapfile`) dentro del sistema de archivos montado de la partición mapeada elegida. Asegúrese de activarlo con `swapon` y también agrege su archivo a `/etc/fstab` más adelante. Tenga en cuenta que el contenido anterior del archivo de intercambio permanece transparente durante los reinicios.

Configure su sistema para reanudar desde la partición mapeada elegida. Por ejemplo, si utiliza [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") con soporte para hibernación del kernel, agregue `resume=`*su partición mapeada elegida* y `resume_offset=`*vea el cálculo de la orden siguiente* a la línea del kernel en la configuración de GRUB (generalmente en `/etc/default/grub`). Una línea con una partición raíz encriptada puede verse así:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/rootDevice resume_offset=123456789 ro

```

El `resume_offset` del archivo de intercambio apunta al inicio (extensión cero) del archivo y puede identificarse así:

```
# filefrag -v /swapfile | awk '{if($1=="0:"){print $4}}'

```

Agregue el hook `resume` al archivo `etc/mkinitcpio.conf` y [regenere initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)") después:

```
HOOKS=(... encrypt **resume** ... filesystems ...)

```

Si usa un teclado USB para introducir su contraseña de descifrado, entonces el módulo `keyboard` **debe** colocarse delante del hook `encrypt`, como se muestra a continuación. De lo contrario, no podrá iniciar su sistema porque no podrá ingresar la contraseña de descifrado para desbloquear la partición raíz de Linux. (Si aún tiene este problema después de agregar `keyboard`, intente con `usbinput`, aunque este está en desuso).

```
HOOKS=(... **keyboard** encrypt ...)

```

## Problemas conocidos

*   `Stopped (with error) /dev/dm-1` en los registros. Consulte [systemd issue 1620](https://github.com/systemd/systemd/issues/1620).