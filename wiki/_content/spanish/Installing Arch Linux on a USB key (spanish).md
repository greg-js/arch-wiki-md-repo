Esta página describe cómo realizar una instalación normal de Arch en una llave USB (o «unidad flash»). A diferencia de un [USB como soporte de instalación](/index.php/USB_Installation_Media_(Espa%C3%B1ol) "USB Installation Media (Español)"), el liveusb daría como resultado la instalación de un sistema de forma permanente en unidad flash USB idéntica a una instalación normal sobre un disco duro.

## Contents

*   [1 Preparación](#Preparaci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 GRUB legacy](#GRUB_legacy)
    *   [3.2 Syslinux](#Syslinux)
*   [4 Consejos](#Consejos)
    *   [4.1 Usar la instalación USB en varias máquinas](#Usar_la_instalaci.C3.B3n_USB_en_varias_m.C3.A1quinas)
        *   [4.1.1 Arquitectura](#Arquitectura)
        *   [4.1.2 Controladores de entrada](#Controladores_de_entrada)
        *   [4.1.3 Controladores de vídeo](#Controladores_de_v.C3.ADdeo)
        *   [4.1.4 Nombres permanentes para los dispositivos de bloques](#Nombres_permanentes_para_los_dispositivos_de_bloques)
        *   [4.1.5 Parámetros del kernel](#Par.C3.A1metros_del_kernel)
    *   [4.2 Compatibilidad](#Compatibilidad)
    *   [4.3 Optimizar la vida útil de la memoria flash](#Optimizar_la_vida_.C3.BAtil_de_la_memoria_flash)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Preparación

**Nota:** Se recomiendan, al menos, 2 GB de espacio de almacenamiento. Nos ajustaremos a un modesto conjunto de paquetes, dejando un pequeño espacio libre para el almacenamiento.

Hay varias maneras de instalar Arch en una memoria USB, la más sencilla es desde dentro del propio Arch:

*   Si ya estamos ejecutando Arch, bastará con instalar [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) y continuar con la [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") al igual que lo haríamos desde la imagen iso, pero sin utilizar /dev/sda. Utilizaremos `lsblk` para obtener el nombre de /dev/sd* de la llave USB antes de proceder a la instalación.

**Advertencia:** Si por error formateamos /dev/sda, es probable que eliminemos todo el contenido del disco duro.

*   Podemos también utilizar un CD/USB de Arch Linux para instalar Arch en la llave USB, arrancando el CD/USB y siguiendo las instrucciones de la [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"). Si arrancamos desde un Live USB, la instalación tendrá que hacerse en una memoria USB diferente.
*   O bien, si tenemos otro equipo disponible con linux (que no tiene por que ser con Arch), podemos seguir las instrucciones para [instalar desde un sistema linux existente](/index.php/Install_from_existing_Linux "Install from existing Linux"), y, a continuación, seguiremos en la sección de configuración.

## Instalación

Siga la [Guía de Instalación](/index.php/Installation_guide "Installation guide") como lo haría normalmente, con las siguientes excepciones:

*   Si cfdisk falla devolviendo el error fatal *«Partition ends in the final partial cylinder»*, la única manera de proceder es cerrar a todas las particiones en el disco usb. Abra otra terminal presionando (`Alt+F2`), escriba `fdisk/dev/sdX` (donde `sdX` es el disco USB), imprima la tabla de particiones (p), compruebe que todo está bien, bórrelo (d) y escribir los cambios (w). Ahora regrese a cfdisk.
*   Se recomienda revisar el artículo sobre los [Consejos para minimizar la lectura/escritura del SSD](#Optimizar_la_vida_.C3.BAtil_de_la_memoria_flash) del artículo de la wiki [SSD](/index.php/SSD "SSD") antes de seleccionar un sistema de archivos. En resumen, ext4 con un sistema journal, puede ser adecuado. Recuerde que el flash usb tiene un número limitado de escrituras, y un sistema de archivos journaling utilizará una parte de ellos cada vez que actualice. Por esta misma razón, lo mejor es renunciar a una partición de intercambio. Tenga en cuenta que esto no afecta a la instalación en un disco duro USB.
*   Antes de crear el disco RAM inicial con la orden `# mkinitcpio -p linux`, edite el archivo `/etc/mkinitcpio.conf` y agregue `block` en la matriz hooks despues de udev. Esto es necesario para cargar el módulo correspondiente en el primer espacio de usuario.
*   Si quiere ser capaz de seguir utilizando el dispositivo UFD como una unidad extraíble multiplataforma, esto se puede lograr mediante la creación de una partición que aloje un sistema de archivos adecuado (lo más probable NTFS). Tenga en cuenta que la partición de datos puede tener que ser la primera partición en el dispositivo, dado que Windows asume que solo puede haber una partición en un dispositivo extraíble, y realizará el automount de una partición del sistema EFI en dicho lugar. Recuerde instalar [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) y [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g).

## Configuración

*   Asegúrese de que el archivo `/etc/fstab` incluye la información de la partición correcta para `/` y para cualquier otra partición en la llave USB. Si la llave USB va a ser usada para arrancar en varias máquinas, es muy probable que los dispositivos y el número de los discos duros disponibles varíen. Por lo tanto, es aconsejable el uso de UUID o etiquetas:

*   Para obtener los UUID apropiados de las particiones utilice la orden **blkid**.

**Nota:**

*   Cuando GRUB es instalado en la llave USB, la llave será siempre `hd0,0`
*   Parece que las versiones actuales de GRUB usan automáticamente, por defecto, uuid. Las instrucciones siguientes son para GRUB legacy.

### GRUB legacy

`menu.lst`, el archivo de configuración de GRUB legacy, debe ser modificado para que coincida (más o menos) con el siguiente:

Con la partición /dev/sdaX estática:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/sda1 ro
initrd /boot/initramfs-linux.img

```

Cuando se utiliza la etiqueta (*«label»*), el archivo *menu.lst* debería mostrar este aspecto:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/**Arch** ro
initrd /boot/initramfs-linux.img

```

Y, si se usa UUID, debería mostrar este otro:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
initrd /boot/initramfs-linux.img

```

### Syslinux

Con la partición /dev/sdaX estática:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=/dev/sdax ro
        INITRD ../initramfs-linux.img

```

Usando la UUID:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=UUID=3a9f8929-627b-4667-9db4-388c4eaaf9fa ro
        INITRD ../initramfs-linux.img

```

## Consejos

### Usar la instalación USB en varias máquinas

#### Arquitectura

Para hacer más versátil la compatibilidad, es recomendable que instale la arquitectura x86_64 con el apoyo de [multilib](/index.php/Multilib "Multilib"), ya que se ejecutará en ambas arquitecturas de 32 y 64 bits.

**Nota:** Si ha instalado la arquitectura i686 y desea migrar a x86_64, consulte el artículo de la wiki [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling") para obtener ayuda.

#### Controladores de entrada

Para uso con el portátil (o para utilizar una pantalla táctil), necesitará el paquete [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para trabajar con la pantalla/panel táctil.

Para obtener instrucciones sobre puesta a punto o problemas del touchpad, consulte el artículo [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)").

#### Controladores de vídeo

**Nota:** El uso de controladores de vídeo propietarios **no** es recomendable para este tipo de instalación.

Los controladores de vídeo recomendados son: [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), [mesa](https://www.archlinux.org/packages/?name=mesa), [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) y [xf86-video-nv](https://www.archlinux.org/packages/?name=xf86-video-nv).

Para hacer más versátil la compatibilidad, instale todos los controladores de vídeo de código abierto, incluyendo sus homólogos multilib: [lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri), [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) y [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri).

#### Nombres permanentes para los dispositivos de bloques

Se recomienda utilizar [UUID](/index.php/UUID "UUID"), tanto en [fstab](/index.php/Fstab "Fstab") como en la configuración del gestor de arranque. Véase [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") para obtener más detalles.

Como alternativa, puede crear reglas udev para crear un enlace simbólico personalizado para la llave USB. A continuación, utilice este enlace simbólico en fstab y en la configuración del gestor de arranque. Véase [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev") para obtener más detalles.

#### Parámetros del kernel

Es posible que desee desactivar KMS, por diversas razones, tales como evitar una pantalla en blanco o un error de «no signal» en la pantalla, al usar algunas tarjetas de vídeo Intel, etc. Para desactivar KMS, añada `nomodeset` como parámetro del kernel. Consulte el artículo sobre los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para obtener más información.

**Advertencia:** Algunos controladores de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") no funcionan con KMS desactivado. Consulte la página wiki de su controlador específico para más detalles. Nouveau, en particular, necesita KMS para determinar la resolución de pantalla correcta. Si agrega `nomodeset` como un parámetro del kernel, a modo de medida preventiva, puede que tenga que ajustar la resolución de la pantalla manualmente cuando utiliza máquinas con tarjetas de vídeo Nvidia. Véase [Xrandr](/index.php/Xrandr "Xrandr") para más información.

### Compatibilidad

La imagen fallback se debe utilizar para obtener una máxima compatibilidad.

### Optimizar la vida útil de la memoria flash

*   De nuevo, se recomienda revisar los [Consejos para minimizar la lectura/escritura del SSD](/index.php/SSD#Tips_for_minimizing_disk_reads.2Fwrites "SSD") del artículo de la wiki [SSD](/index.php/SSD "SSD").

## Véase también

*   [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")