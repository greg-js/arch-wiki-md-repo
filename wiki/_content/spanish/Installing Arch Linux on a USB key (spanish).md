**Estado de la traducción**
Este artículo es una traducción de [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key"), revisada por última vez el **2018-11-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Installing_Arch_Linux_on_a_USB_key&diff=0&oldid=543740) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)")
*   [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)")
*   [General troubleshooting (Español)](/index.php/General_troubleshooting_(Espa%C3%B1ol) "General troubleshooting (Español)")

Esta página describe cómo realizar una instalación normal de Arch en una llave USB (o «unidad flash»). A diferencia de un [USB como soporte de instalación](/index.php/USB_Installation_Media_(Espa%C3%B1ol) "USB Installation Media (Español)"), el usb live daría como resultado la instalación de un sistema de forma permanente en unidad flash USB idéntica a como resultaría una instalación normal sobre un disco duro.

## Contents

*   [1 Instalación](#Instalación)
    *   [1.1 Ajustes de instalación](#Ajustes_de_instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 GRUB legacy](#GRUB_legacy)
    *   [2.2 GRUB](#GRUB)
    *   [2.3 Syslinux](#Syslinux)
*   [3 Consejos](#Consejos)
    *   [3.1 Usar la instalación USB en varias máquinas](#Usar_la_instalación_USB_en_varias_máquinas)
        *   [3.1.1 Controladores de entrada](#Controladores_de_entrada)
        *   [3.1.2 Controladores de vídeo](#Controladores_de_vídeo)
        *   [3.1.3 Nombres permanentes para los dispositivos de bloques](#Nombres_permanentes_para_los_dispositivos_de_bloques)
        *   [3.1.4 Parámetros del kernel](#Parámetros_del_kernel)
        *   [3.1.5 Arranque desde medios USB 3](#Arranque_desde_medios_USB_3)
    *   [3.2 Compatibilidad](#Compatibilidad)
    *   [3.3 Optimizar la vida útil de la memoria flash](#Optimizar_la_vida_útil_de_la_memoria_flash)
*   [4 Véase también](#Véase_también)

## Instalación

**Nota:** se recomiendan, al menos, 2 GiB de espacio de almacenamiento. Nos ajustaremos a un modesto conjunto de paquetes, dejando un pequeño espacio libre para el almacenamiento.

Hay varias maneras de instalar Arch en una memoria USB, dependiendo del sistema operativo disponible:

*   Si tenemos otro equipo disponible con linux (que no tiene por que ser con Arch), podemos seguir las instrucciones para [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux").
*   Podemos también utilizar un CD/USB de Arch Linux para instalar Arch en la llave USB, arrancando el CD/USB y siguiendo las instrucciones de la [installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"). Si arrancamos desde un Live USB, la instalación tendrá que hacerse en una memoria USB diferente
*   Si ejecuta Windows o un sistema operativo X, descargue VirtualBox, instale VirtualBox Extensions, agregue la unidad USB a una máquina virtual que ejecuta Arch (por ejemplo, ejecutandola desde una iso), apunte la instalación a la unidad USB mientras usa las instrucciones de [installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

### Ajustes de instalación

*   Antes de crear el disco RAM inicial `# mkinitcpio -p linux`, en `/etc/mkinitcpio.conf` agregue el hook `block` a la matriz de HOOK justo después de udev. Esto es necesario para la carga apropiada del módulo en el espacio de usuario temprano.
*   Se recomienda encarecidamente revisar el artículo wiki [reduce las lecturas/escrituras del disco](/index.php/Improving_performance#Reduce_disk_reads.2Fwrites "Improving performance") antes de seleccionar un sistema de archivos. Para resumir, [ext4 sin journal](http://fenidik.blogspot.com/2010/03/ext4-disable-journal.html) debe estar bien, que puede crearse con `# mkfs.ext4 -O "^has_journal" /dev/sdXX`. El inconveniente obvio de usar un sistema de archivos con el journal inhabilitado es la pérdida de datos como resultado de un desmontaje forzoso. Hay que reconocer que una unidad flash tiene un número limitado de escrituras, y un sistema de archivos con journald tomará algunas de estas a medida que se actualice el diario. Por esta misma razón, es mejor olvidar la partición de intercambio. Tenga en cuenta que esto no afecta a la instalación en una unidad USB.
*   Si desea poder seguir utilizando el dispositivo UFD como unidad extraíble multiplataforma, puede lograrse mediante la creación de una partición que contenga un sistema de archivos adecuado (probablemente NTFS o exFAT). Tenga en cuenta que la partición de datos puede necesitar ser la primera partición en el dispositivo, ya que Windows asume que solo puede haber una partición en un dispositivo extraíble, y de lo contrario montará automáticamente una partición del sistema EFI. Recuerde instalar [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) y [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). Algunas herramientas están disponibles en línea que pueden permitirle cambiar sobre la marcha el bit de medios extraíbles en su dispositivo UFD. Esto engañaría a los sistemas operativos para tratar su dispositivo UFD como un disco duro externo y le permitiría usar cualquier esquema de partición que elija.

**Advertencia:** si no es posible cambiar sobre la marcha el bit de medios extraíbles en todos los dispositivos UFD, tratar de usar software que sea incompatible con su dispositivo puede dañarlo. Intentar voltear el bit de medios extraíbles **no** se recomienda.

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

### GRUB

En GPT con instalaciones UEFI, asegúrese de seguir las instrucciones de [GRUB (Español)#Sistemas UEFI](/index.php/GRUB_(Espa%C3%B1ol)#Sistemas_UEFI "GRUB (Español)") e incluya la opción `--removable` ya que, de lo contrario, puede romper las instalaciones existentes de GRUB, como en la siguiente órden:

```
# grub-install --target=x86_64-efi --efi-directory=$esp --bootloader-id=grub **--removable** --recheck

```

### Syslinux

Con la partición `/dev/sdaX` estática:

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

#### Controladores de entrada

Para uso con el portátil (o para utilizar una pantalla táctil), necesitará el paquete [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para trabajar con la pantalla/panel táctil.

Para obtener instrucciones sobre puesta a punto o problemas del touchpad, consulte el artículo [Touchpad Synaptics (Español)](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)").

#### Controladores de vídeo

**Nota:** el uso de controladores de vídeo propietarios **no** es recomendable para este tipo de instalación.

Para admitir las GPU más comunes, instale[xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu), and [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) (y su homólogo multilib: [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa)).

#### Nombres permanentes para los dispositivos de bloques

Se recomienda utilizar [UUID](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-uuid "Persistent block device naming (Español)"), tanto en [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") como en la configuración del gestor de arranque. Véase [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") para obtener más detalles.

Como alternativa, puede crear reglas udev para crear un enlace simbólico personalizado para la llave USB. A continuación, utilice este enlace simbólico en fstab y en la configuración del gestor de arranque. Véase [udev (Español)#Configurar nombres estáticos para los dispositivos](/index.php/Udev_(Espa%C3%B1ol)#Configurar_nombres_estáticos_para_los_dispositivos "Udev (Español)") para obtener más detalles.

#### Parámetros del kernel

Es posible que desee desactivar KMS, por diversas razones, tales como evitar una pantalla en blanco o un error de «no signal» en la pantalla, al usar algunas tarjetas de vídeo Intel, etc. Para desactivar KMS, añada `nomodeset` como parámetro del kernel. Consulte el artículo sobre los [Kernel parameters (Español)](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") para obtener más información.

**Advertencia:** Algunos controladores de [Xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") no funcionan con KMS desactivado. Consulte la página wiki de su controlador específico para más detalles. Nouveau, en particular, necesita KMS para determinar la resolución de pantalla correcta. Si agrega `nomodeset` como un parámetro del kernel, a modo de medida preventiva, puede que tenga que ajustar la resolución de la pantalla manualmente cuando utiliza máquinas con tarjetas de vídeo Nvidia. Véase [Xrandr](/index.php/Xrandr "Xrandr") para más información.

#### Arranque desde medios USB 3

Véa [[1]](http://www.wyae.de/docs/boot-usb3/).

### Compatibilidad

La imagen fallback se debe utilizar para obtener una máxima compatibilidad.

### Optimizar la vida útil de la memoria flash

*   Es posible que desee configurar [journald](/index.php/Systemd_(Espa%C3%B1ol)#Journal "Systemd (Español)") para almacenar sus diarios en la RAM, por ejemplo, creando un archivo de configuración personalizado:

 `/etc/systemd/journald.conf.d/usbstick.conf` 
```
[Journal]
Storage=volatile
RuntimeMaxUse=30M
```

*   Para desactivar `fsync` y las llamadas al sistema relacionadas en los navegadores web y otras aplicaciones que no escriben datos esenciales, use la orden *eatmydata* de [libeatmydata](https://www.archlinux.org/packages/?name=libeatmydata) para evitar tales llamadas al sistema:

```
$ eatmydata firefox

```

## Véase también

*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")