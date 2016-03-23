**Estado de la traducción:** este artículo es una versión traducida de [Archboot](/index.php/Archboot "Archboot"). Fecha de la última traducción/revisión: **2014-12-26**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Archboot&diff=0&oldid=345108).

## Contents

*   [1 ¿Qué es Archboot?](#.C2.BFQu.C3.A9_es_Archboot.3F)
*   [2 Diferencias con el soporte de instalación de archiso](#Diferencias_con_el_soporte_de_instalaci.C3.B3n_de_archiso)
*   [3 Lanzamientos de la ISO de Archboot](#Lanzamientos_de_la_ISO_de_Archboot)
    *   [3.1 Grabar lanzamiento](#Grabar_lanzamiento)
    *   [3.2 Arrancar PXE/sistema de rescate](#Arrancar_PXE.2Fsistema_de_rescate)
    *   [3.3 Modos de arranque soportados por el soporte de Archboot](#Modos_de_arranque_soportados_por_el_soporte_de_Archboot)
    *   [3.4 ¿Cómo hacer una instalación remota con ssh?](#.C2.BFC.C3.B3mo_hacer_una_instalaci.C3.B3n_remota_con_ssh.3F)
    *   [3.5 Características del configurador interactivo](#Caracter.C3.ADsticas_del_configurador_interactivo)
    *   [3.6 FAQ, limitaciones y problemas conocidos](#FAQ.2C_limitaciones_y_problemas_conocidos)
    *   [3.7 Antecedentes](#Antecedentes)
    *   [3.8 Errores](#Errores)
*   [4 Lanzamientos BETA de la ISO de Archboot](#Lanzamientos_BETA_de_la_ISO_de_Archboot)
*   [5 Enlaces](#Enlaces)
*   [6 HOWTO: crear archivos de imagen](#HOWTO:_crear_archivos_de_imagen)
    *   [6.1 Requisitos](#Requisitos)
    *   [6.2 Crear entornos chroot para archboot](#Crear_entornos_chroot_para_archboot)
    *   [6.3 Instalar archboot y actualizar a los últimos paquetes](#Instalar_archboot_y_actualizar_a_los_.C3.BAltimos_paquetes)
    *   [6.4 Generar imágenes](#Generar_im.C3.A1genes)

## ¿Qué es Archboot?

*   Archboot es un conjunto de scripts para generar medios de almacenamiento booteables en CD/USB/PXE.
*   Está diseñado para operaciones de instalación o de rescate.
*   Solo funciona en la memoria RAM, sin ningún tipo de sistemas de archivos especiales del tipo squashfs, por lo que se limita al alcance de la memoria RAM que esté instalada en su sistema.

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [archboot](https://www.archlinux.org/packages/?name=archboot) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Diferencias con el soporte de instalación de archiso

*   Proporciona una instalación interactiva adicional y script quickinst.
*   Contiene el repositorio [core] en el soporte.
*   Se ejecuta un sistema Arch Linux modificado en initramfs.
*   Se limita a usar la memoria RAM, todo lo que no es necesario, como manuales, páginas de información, etc., no se proporcionan.
*   No se monta nada durante el proceso de arranque.
*   Es compatible con la instalación remota a través de ssh.

## Lanzamientos de la ISO de Archboot

*   Se proporcionan archivos de imagen híbrida y torrents, que incluyen i686/x86_64 y repositorio [core],

	imágenes de network labeled no se incluyen en el repositorio [core].

*   Por favor, revise md5sum antes de usarlo.
*   [Download 2015.09](http://ftp.u-strasbg.fr/linux/distributions/archlinux/iso/archboot/2015.09/) / [Changelog](http://ftp.u-strasbg.fr/linux/distributions/archlinux/iso/archboot/Changelog-2015.09-1.txt) / [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=182439)

	kernel: 3.17.3-1

	pacman: 4.1.2-6

	systemd: 217-6

	RAM recomendada: 640 MB

### Grabar lanzamiento

El archivo de imagen híbrida es una imagen de CD grabable estándar y también una imagen de disco cruda.

*   Puede ser quemado en un soporte CD (RW) utilizando alguna de las utilidades de grabación de CD.
*   Puede ser escrito en crudo en una unidad usando 'dd' o utilidades similares. Este método está diseñado para utilizarse con unidades flash USB.

 `'dd if=<imagefile> of=/dev/<yourdevice> bs=1M'` 

### Arrancar PXE/sistema de rescate

[Descargue 2014.11 „2k14-R5“](https://downloads.archlinux.de/iso/archboot/2014.11/boot) los archivos necesarios del directorio.

*   vmlinuz_i686 + initramfs_i686.img (i686)
*   vmlinuz_x86_64 + initramfs_x86_64.img(x86_64)
*   Para arranque PXE añadir el kernel e initrd a la configuración TFTP y obtendrá la ejecución de la instalación/sistema de rescate.
*   Para el arranque de rescate agregar una entrada a su gestor de arranque que apunte al kernel e initrd.

### Modos de arranque soportados por el soporte de Archboot

*   Soporta el arranque de BIOS con syslinux.
*   Soporta el arranque de UEFI/UEFI_CD con [Gummiboot](/index.php/Gummiboot "Gummiboot") y [EFISTUB](/index.php/EFISTUB "EFISTUB").
*   Soporta el arranque de UEFI_MIX_MODE con grub.
*   Soporta arranque Secure Boot con prebootloader.
*   Soporta el apoyo de loopback de la iso para grub(2).

	variables utilizadas (siguiendo el ejemplo):

	iso_loop_dev=PARTUUID=XXXX

	iso_loop_path=/blah/archboot.iso

```
menuentry "Archboot" --class iso {
loopback loop (hdX,X)/<archboot.iso>
linux (loop)/boot/vmlinuz_x86_64 iso_loop_dev=/dev/sdXX iso_loop_path=/<archboot.iso>
initrd (loop)/boot/initramfs_x86_64.img
}
```

*   Soporta el arranque usando memdisk de syslinux (solo en la modalidad BIOS).

```
menuentry "Archboot Memdisk" {
   linux16 /memdisk iso
   initrd16 hd(X,X)/<archboot.iso>
}
```

### ¿Cómo hacer una instalación remota con ssh?

*   Durante el inicio, todas las interfaces de red tratarán de obtener una dirección IP mediante DHCP.
*   La contraseña de root no se establece por defecto. Establecer una contraseña, ya que se necesita para obtener privacidad durante la instalación.

 `'ssh root@<yourip>'` 

### Características del configurador interactivo

*   Modo de instalación a través del soporte y de conexión de red
*   Cambiar de la distribución del teclado y tipo de letra de la consola
*   Cambiar hora y fecha
*   Configurar conexión de red con netctl
*   Preparar el disco de almacenamiento, como la preparación automática, el particionamiento, soporte GUID (GPT), compatibilidad con unidades de sector de 4k, etc.
*   Creación de dispositivos de raid software/particiones raid, dispositivos lvm2 y dispositivos encriptados con luks
*   Soporte para linux estándar, raid/raid_partitions,dmraid/fakeraid,lvm2 y dispositivos cifrados
*   Soporte para sistema de archivos: ext2/3/4, btrfs, f2fs, nilfs2, reiserfs,xfs,jfs,ntfs-3g,vfat
*   Soporte para esquema de nombres: PARTUUID, PARTLABEL, FSUUID, FSLABEL and KERNEL
*   Soporte para el montaje del soporte de instalación con grub(2), loopback y memdisk
*   Soporte para selección de paquetes
*   Script hwdetect usado para preconfiguración
*   Auto/preconfiguración de fstab, modo kms, ssd, mkinitcpio.conf, systemd, crypttab y mdadm.conf
*   Configuración de los archivos básicos del sistema
*   Configuración de la contraseña root
*   Soporte para los gestores de arranque grub(2) (BIOS y UEFI), refind-efi, gummiboot, syslinux (BIOS y UEFI)

### FAQ, limitaciones y problemas conocidos

*   Problemas y soluciones específicas conocidas del lanzamiento se publican en los archivos changelog.
*   Verifique también los hilos del foro para los arreglos y soluciones publicadas.
*   ¿Por qué la pantalla se queda en negro o le suceden otros problemas raros a la pantalla?

	Algunos dispositivos no casan bien con la activación KMS, en estos caso utilice radeon.modeset=0, i915.modeset=0 o nouveau.modeset=0 en el prompt de arranque.

*   Dmraid/fakeraid podría romperse con algunas placas, la compatibilidad no es perfecta aquí.

	La razón es que hay tantos componentes de hardware diferentes como proveedores. Hasta el momento, 1.0.0rc16 ha sido incluido con el último conjunto de parches de fedora, pero el desarrollo ha sido detenido.

	Mdadm soporta algunos chipsets fakeraid isw y ddf, pero el montaje durante el arranque se desactiva en /etc/mdadm.conf

*   Grub(2) no detecta correctamente el orden de arranque de la BIOS:

	Puede suceder que las entradas hd

(x,x) no sean correctas, por lo tanto, el primer reinicio puede no funcionar.

	Razón: grub no pueden detectar el orden de arranque de la BIOS.

	Arreglo: o bien, cambie el orden de arranque de la bios, o bien, cambie el archivo menu.lst para corregir las entradas después de un arranque con éxito. Esto no se puede arreglar, es una restricción en grub(2).

*   ¿Por qué se utilizada parted en rutina de instalación, en lugar de cfdisk para la tabla de particionado en la modalidad msdos?

	parted es el único programa de partición de Linux que puede manejar todo tipo de opciones de las ofrecidas en la rutina de configuración.

	cfdisk no puede manejar GPT/GUID ni puede alinear particiones correctas con espacios de 1MB para discos de sector de 4k.

	cfdisk es una buena herramienta, pero es demasiado limitada para ser la herramienta de particionado estándar sin más.

	cfdisk, aún así, está incluido, pero tiene que ser ejecutado en otro terminal.

### Antecedentes

El historial de versiones antiguas se puede encontrar [aquí](ftp://ftp.archlinux.org/iso/archboot/history).

### Errores

[Arch Linux Bugtracker](https://bugs.archlinux.org)

## Lanzamientos BETA de la ISO de Archboot

*   El archivo de imagen híbrido proporcionado solo admite la instalación a través de conexión de red.
*   Por favor, lea los archivos Changelog para conocer las limitaciones de la memoria RAM.
*   Por favor, revise md5sum antes de usarlo.
*   Sin ISO beta disponible en este momento.

## Enlaces

*   [Repositorio GIT](https://projects.archlinux.org/archboot.git/)

## [HOWTO](https://en.wikipedia.org/wiki/es:HOWTO "wikipedia:es:HOWTO"): crear archivos de imagen

(Regeneración rápida del soporte de instalación con los últimos paquetes básicos disponibles)

### Requisitos

*   Arquitectura x86_64
*   Espacio libre en el disco ~ 3GB

### Crear entornos chroot para archboot

```
# Instalar archboot
pacman -S archboot
mkdir <x86_64_chroot>
pacman --root "<x86_64_chroot>" -S base --noconfirm --noprogressbar
mkdir <i686_chroot>
linux32 pacman --root "<i686_chroot>" -S base --noconfirm --noprogressbar

```

*   Entrar en el contenedor 86_64 de archboot:

```
systemd-nspawn --capability=CAP_MKNOD --register=no -M $1-$(uname -m) -D <x86_64_chroot>

```

*   Entrar en el contenedor i686 de archboot:

```
linux32 systemd-nspawn --capability=CAP_MKNOD --register=no -M $1-$(uname -m) -D <i686_chroot>

```

### Instalar archboot y actualizar a los últimos paquetes

```
# Instalar para ambas arquitecturas en entornos enjaulados de archboot:
pacman -S archboot
# Actualizar para ambas arquitecturas en entornos enjaulados los paquetes más recientes disponibles
pacman -Syu

```

### Generar imágenes

```
# Ejecutar para ambas arquitecturas en entornos enjaulados (necesita bastante tiempo...)
archboot-allinone.sh -t
# Poner los tarballs generados en un directorio y ejecutarlos (necesita bastante tiempo...)
archboot-allinone.sh -g

```

*   Una vez finalizado obtendrá un conjunto de imágenes.

¡Disfrútelo!
tpowa
(Desarrollador de Archboot)