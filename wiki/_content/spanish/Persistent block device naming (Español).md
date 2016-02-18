En este artículo se describe cómo utilizar nombres permanentes para sus dispositivos de bloques. Esto ha sido posible gracias a la introducción de udev y tiene algunas ventajas sobre los nombres basados en el bus de conexión. Si el equipo tiene más de una controladora de disco SATA, SCSI o IDE, el orden en que se añaden sus correspondientes nodos de dispositivos es arbitraria. Esto puede dar lugar a nombres de dispositivos como `/dev/**sda**` y `/dev/**sdb**` conmutando aleatoriamente en cada arranque, que puede terminar en una nominación de los dispositivos que impida el arranque del sistema, en pánico del kernel o en una desaparición del dispositivo de bloque. La nomenclatura permanente resuelve estos problemas.

**Nota:** Si está usando [LVM2](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), este artículo no es relevante, dado que LVM se encarga de esto automáticamente.

## Contents

*   [1 Métodos para nombrar los dispositivos de forma permanente](#M.C3.A9todos_para_nombrar_los_dispositivos_de_forma_permanente)
    *   [1.1 by-label](#by-label)
    *   [1.2 by-uuid](#by-uuid)
    *   [1.3 by-id y by-path](#by-id_y_by-path)
    *   [1.4 by-partlabel](#by-partlabel)
    *   [1.5 by-partuuid](#by-partuuid)
    *   [1.6 Nombres estáticos de los dispositivos con udev](#Nombres_est.C3.A1ticos_de_los_dispositivos_con_udev)
*   [2 Usar nomenclatura permanente](#Usar_nomenclatura_permanente)
    *   [2.1 fstab](#fstab)
    *   [2.2 Gestores de arranque](#Gestores_de_arranque)

## Métodos para nombrar los dispositivos de forma permanente

Hay cuatro esquemas diferentes para nombrar de forma permanente los dispositivos: [by-label](#by-label), [by-uuid](#by-uuid), [by-id y by-path](#by-id_and_by-path). Para aquellos que utilizan discos con [tabla de particiones GUID (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table"), pueden usar dos esquemas adicionales [by-partlabel](#by-partlabel) y [by-partuuid](#by-partuuid). También puede utilizar [nombres estáticos de dispositivos utilizando udev](#Static_device_names_with_Udev).

Las siguientes secciones describen lo que son y cómo se utilizan los diferentes métodos de asignación de nombres permanentes.

La orden `lsblk -f` se puede utilizar para la visualización gráfica de los primeros esquemas nombres persistentes:

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL  UUID                                 MOUNTPOINT
sda                                                       
├─sda1 vfat          CBB6-24F2                            /boot
├─sda2 ext4   SYSTEM 0a3407de-014b-458b-b5c1-848e92a327a3 /
├─sda3 ext4   DATA   b411dc99-f0a0-4c87-9e05-184977be8539 /home
└─sda4 swap          f9fe0b69-a280-415d-a03a-a32752370dee [SWAP]

```

Para aquellos que utilizan [GPT](/index.php/GUID_Partition_Table "GUID Partition Table"), utilice la orden `blkid`. Este último es más eficiente para los scripts, pero más difícil de leer.

 `$ blkid` 
```
/dev/sda1: UUID="CBB6-24F2" TYPE="vfat" PARTLABEL="EFI SYSTEM PARTITION" PARTUUID="d0d0d110-0a71-4ed6-936a-304969ea36af" 
/dev/sda2: LABEL="SYSTEM" UUID="0a3407de-014b-458b-b5c1-848e92a327a3" TYPE="ext4" PARTLABEL="GNU/LINUX" PARTUUID="98a81274-10f7-40db-872a-03df048df366" 
/dev/sda3: LABEL="DATA" UUID="b411dc99-f0a0-4c87-9e05-184977be8539" TYPE="ext4" PARTLABEL="HOME" PARTUUID="7280201c-fc5d-40f2-a9b2-466611d3d49e" 
/dev/sda4: UUID="f9fe0b69-a280-415d-a03a-a32752370dee" TYPE="swap" PARTLABEL="SWAP" PARTUUID="039b6c1c-7553-4455-9537-1befbc9fbc5b"

```

### by-label

Casi todos los tipos de sistemas de archivos pueden tener una etiqueta. Todas las particiones que tienen una se enumeran en el directorio `/dev/disk/by-label`. Este directorio se crea y se destruye de forma dinámica, en función de si tiene particiones con etiquetas adjuntas.

 `$ ls -l /dev/disk/by-label` 
```

total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 DATA -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 SYSTEM -> ../../sda2

```

Las etiquetas de los sistemas de archivos se pueden cambiar. Los siguientes son algunos métodos para cambiar las etiquetas de los sistemas de archivos comunes:

	swap 

	`swaplabel -L <etiqueta> /dev/XXX` usando [util-linux](https://www.archlinux.org/packages/?name=util-linux)

	ext2/3/4 

	`e2label /dev/XXX <etiqueta>` usando [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

	btrfs 

	`btrfs filesystem label /dev/XXX <etiqueta>` usando [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

	reiserfs 

	`reiserfstune -l <etiqueta> /dev/XXX` usando [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

	jfs 

	`jfs_tune -L <etiqueta> /dev/XXX` usando [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

	xfs 

	`xfs_admin -L <etiqueta> /dev/XXX` usando [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

	fat/vfat 

	`dosfslabel /dev/XXX <etiqueta>` usando [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

	fat/vfat 

	`mlabel -i /dev/XXX ::<etiqueta>` usando [mtools](https://www.archlinux.org/packages/?name=mtools)

	ntfs 

	`ntfslabel /dev/XXX <etiqueta>` usando [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

**Nota:**

*   El cambio de etiqueta de un sistema de archivos de la partición raíz tiene que ser hecho desde una distribución GNU/Linux «live», ya que dicha partición necesita ser desmontada primero.
*   Las etiquetas tienen que ser inequívocas (sin ambigüedades) para evitar posibles conflictos.
*   Las etiquetas pueden tener una longitud de hasta 16 caracteres.

### by-uuid

[UUID](https://en.wikipedia.org/wiki/es:Universally_unique_identifier "wikipedia:es:Universally unique identifier") es un mecanismo para dotar a cada sistema de archivos de un identificador único. Estos identificadores son generados por las utilidades del sistema de archivos (por ejemplo, `mkfs.*`) cuando la partición se formatea y se ha diseñado de manera que evite conflictos. Todos los sistemas de archivos de GNU/Linux (incluyendo swap y las cabeceras LUKS de dispositivos cifrados en bruto) soportan UUID. Los sistemas de archivos FAT y NTFS (*fat* y etiqueta *windows* del ejemplo de abajo) no son compatibles con UUID, pero todavía se enumeran en `/dev/disk/by-uuid` con un UID más corto (identificador único):

 `$ ls -l /dev/disk/by-uuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 0a3407de-014b-458b-b5c1-848e92a327a3 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 b411dc99-f0a0-4c87-9e05-184977be8539 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 CBB6-24F2 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 f9fe0b69-a280-415d-a03a-a32752370dee -> ../../sda4

```

La ventaja de usar el método UUID es que es mucho menos probable que se produzcan colisiones de nombres que con las etiquetas. Además, se genera automáticamente en la creación del sistema de archivos. Será, por ejemplo, el único indicador, incluso si el dispositivo está conectado a otro sistema (el cual, tal vez, puede tener un dispositivo con la misma etiqueta).

La desventaja es que UUID hace largas líneas de código difícil de leer y rompe el formato en muchos archivos de configuración (por ejemplo fstab o crypttab). También, cada vez que una partición se redimensiona o reformatea, se genera un nuevo UUID y las configuraciones tienen que volver a ajustarse (manualmente).

**Sugerencia:** En caso de que su partición de intercambio no tenga un UUID asignado, tendrá que restablecer la partición de swap usando la utilidad [mkswap](/index.php/Swap_(Espa%C3%B1ol)#Partici.C3.B3n_swap "Swap (Español)").

### by-id y by-path

`by-id` crea un nombre único en función del número de serie del hardware, `by-path` crea un nombre único en función de la ruta física más corta (de acuerdo con sysfs). Ambos contienen cadenas para indicar el subsistema al que pertenecen (es decir, `-ide-` para `by-path`, y `-ata-` para `by-id`) y, por lo tanto, no son adecuados para la solución de los problemas mencionados al comienzo de este artículo. Estos problemas no son objeto de discusión aquí.

### by-partlabel

**Nota:** Este método solo se refiere a los discos con [tabla de particiones GUID (GPT)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)").

Las etiquetas de las particiones se pueden definir en la cabecera de la entrada de la partición en discos GPT.

Véase también [Wikipedia:GUID Partition Table#Partition entries](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries "wikipedia:GUID Partition Table").

Este método es muy similar al de las [etiquetas de los sistemas de archivos](#by-label), excepto en que el directorio dinámico es `/dev/disk/by-partlabel`.

 `ls -l /dev/disk/by-partlabel/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 EFI\x20SYSTEM\x20PARTITION -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 GNU\x2fLINUX -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 HOME -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 SWAP -> ../../sda4

```

**Nota:**

*   Las etiquetas de las particiones GPT también tienen que ser diferentes para evitar conflictos. Para cambiar la etiqueta de una partición, puede utilizar `gdisk` o la versión basada en ncurse `cgdisk`. Ambas utilidades están disponibles en el paquete [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk). Vea [Partitioning (Español)#Herramientas de particionado](/index.php/Partitioning_(Espa%C3%B1ol)#Herramientas_de_particionado "Partitioning (Español)").
*   De acuerdo con la especificación, las etiquetas de las particiones GPT pueden tener hasta 72 caracteres de longitud.

### by-partuuid

**Nota:** Este método solo se refiere a los discos con [tabla de particiones GUID (GPT)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)").

Al igual que con las [etiquetas de particiones GPT](#by-partlabel), el UUID de la partición se define en la entrada de la partición en discos GPT.

Véase también [Wikipedia:GUID Partition Table#Partition entries](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries "wikipedia:GUID Partition Table").

El directorio dinámico es similar al de los otros métodos y, al igual que con el [UUID de los sistemas de archivos](#by-uuid), el uso del UUID de las particiones es preferido sobre el de las etiquetas.

 `ls -l /dev/disk/by-partuuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 039b6c1c-7553-4455-9537-1befbc9fbc5b -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 7280201c-fc5d-40f2-a9b2-466611d3d49e -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 98a81274-10f7-40db-872a-03df048df366 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 d0d0d110-0a71-4ed6-936a-304969ea36af -> ../../sda1

```

### Nombres estáticos de los dispositivos con udev

Véase [Udev (Español)#Configurar nombres estáticos para los dispositivos](/index.php/Udev_(Espa%C3%B1ol)#Configurar_nombres_est.C3.A1ticos_para_los_dispositivos "Udev (Español)").

## Usar nomenclatura permanente

Existen varias aplicaciones que se pueden configurar mediante el uso la nomenclatura permanente. Los siguientes son algunos ejemplos de cómo configurarlos.

### fstab

Ver el artículo principal: [fstab (Español)#UUID](/index.php/Fstab_(Espa%C3%B1ol)#UUID "Fstab (Español)")

### Gestores de arranque

Para utilizar nombres permanentes en su gestor de arranque, deben cumplirse los siguientes requisitos:

*   estar utilizando [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Configuraci.C3.B3n "Mkinitcpio (Español)") para generar la imagen de disco RAM inicial;
*   tener el hook udev activado en el archivo `/etc/mkinitcpio.conf`.

En el ejemplo anterior, `/dev/sda1` es la partición raíz. En el archivo `grub.cfg` de [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), la línea *linux* se parecerá a esto:

```
linux /boot/vmlinuz-linux root=/dev/sda1 rw quiet

```

Dependiendo de qué esquema de nombres prefiera, cambie a uno de los siguientes:

```
linux /boot/vmlinuz-linux root=/dev/disk/by-label/root_myhost rw quiet

```

o:

```
linux /boot/vmlinuz-linux root=UUID=2d781b26-0285-421a-b9d0-d4a0d3b55680 rw quiet

```

Si está usando [LILO (Español)](/index.php/LILO_(Espa%C3%B1ol) "LILO (Español)"), entonces no intente esto con la opción de configuración `root=...`; no va a funcionar. Utilice `append="root=..."` o `addappend="root=..."` en su lugar. Lea la página de manual de LILO para más información sobre `append` y `addappend`.

Hay una forma alternativa de utilizar la etiqueta incrustada en el sistema de archivos. Por ejemplo, si (como el anterior) el sistema de archivos en `/dev/sda1` se etiqueta `root_myhost`, daría como resultado esta línea en GRUB:

```
linux /boot/vmlinuz-linux root=LABEL=root_myhost rw quiet

```