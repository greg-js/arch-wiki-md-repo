**Estado de la traducción**
Este artículo es una traducción de [Microcode](/index.php/Microcode "Microcode"), revisada por última vez el **2019-03-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Microcode&diff=0&oldid=568726) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Los fabricantes de procesadores lanzan actualizaciones de estabilidad y seguridad para el [microcódigo](https://en.wikipedia.org/wiki/es:Microc%C3%B3digo "wikipedia:es:Microcódigo") del procesador. Si bien el microcódigo se puede actualizar a través de BIOS, el kernel de Linux también puede aplicar estas actualizaciones durante el arranque. Estas actualizaciones proporcionan correcciones de errores que pueden ser críticas para la estabilidad de su sistema. Sin estas actualizaciones, puede experimentar falsos errores o paradas inesperadas del sistema que pueden ser difíciles de rastrear.

Los usuarios de las CPU que pertenecen a las familias de procesadores Intel Haswell y Broadwell en particular deben instalar estas actualizaciones de microcódigo para garantizar la estabilidad del sistema. Pero todos los usuarios deben instalar las actualizaciones como una cuestión de rutina.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Habilitar las actualizaciones de microcódigo tempranas](#Habilitar_las_actualizaciones_de_microcódigo_tempranas)
    *   [2.1 GRUB](#GRUB)
        *   [2.1.1 Método automático](#Método_automático)
        *   [2.1.2 Método manual](#Método_manual)
    *   [2.2 systemd-boot](#systemd-boot)
    *   [2.3 EFISTUB](#EFISTUB)
    *   [2.4 rEFInd](#rEFInd)
    *   [2.5 Syslinux](#Syslinux)
    *   [2.6 LILO](#LILO)
*   [3 Actualizaciones de microcódigo tardías](#Actualizaciones_de_microcódigo_tardías)
    *   [3.1 Activar las actualizaciones de microcódigo tardías](#Activar_las_actualizaciones_de_microcódigo_tardías)
    *   [3.2 Desactivar las actualizaciones de microcódigo tardías](#Desactivar_las_actualizaciones_de_microcódigo_tardías)
*   [4 Comprobar que el microcódigo se actualizó en el arranque](#Comprobar_que_el_microcódigo_se_actualizó_en_el_arranque)
*   [5 Cuales CPU aceptan actualizaciones de microcódigo](#Cuales_CPU_aceptan_actualizaciones_de_microcódigo)
    *   [5.1 Detectar actualización de microcódigo disponible](#Detectar_actualización_de_microcódigo_disponible)
*   [6 Activar la carga temprana de microcódigo en kernels personalizados](#Activar_la_carga_temprana_de_microcódigo_en_kernels_personalizados)
*   [7 Véase también](#Véase_también)

## Instalación

Para los procesadores AMD, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode).

Para los procesadores Intel, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode).

Si su instalación de Arch es [en una unidad extraíble](/index.php/Installing_Arch_Linux_on_a_USB_key_(Espa%C3%B1ol) "Installing Arch Linux on a USB key (Español)") que necesita tener microcódigo para ambos fabricantes de procesadores, instale ambos paquetes.

## Habilitar las actualizaciones de microcódigo tempranas

El [cargador de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") debe cargar el microcódigo. Debido a la gran variabilidad en la configuración de inicio de los usuarios, las actualizaciones de microcódigo pueden no ser activadas automáticamente por la configuración predeterminada de Arch. Muchos kernel de AUR han seguido el camino de los [kernels](/index.php/Kernels_(Espa%C3%B1ol) "Kernels (Español)") oficiales de Arch en este sentido.

Estas actualizaciones deben activarse añadiendo `/boot/amd-ucode.img` o `/boot/intel-ucode.img` como el **primer initrd en el archivo de configuración del cargador de arranque**. Esto es un añadido al archivo initrd normal. Véase a continuación las instrucciones para los cargadores de arranque más comunes.

**Nota:** En las secciones siguientes reemplace `*fabricante_cpu*` con su fabricante de CPU, es decir, `amd` o `intel`.

**Sugerencia:** Para [Arch Linux en una unidad extraíble](/index.php/Installing_Arch_Linux_on_a_USB_key_(Espa%C3%B1ol) "Installing Arch Linux on a USB key (Español)") añada ambos archivos de microcódigo como `initrd` a la configuración del cargador de arranque. Su orden no importa siempre y cuando ambos estén especificados antes de la imagen real de initramfs.

### GRUB

#### Método automático

*grub-mkconfig* detectará automáticamente la actualización del microcódigo y configurará [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") de manera apropiada. Después de instalar el paquete de microcódigo, vuelva a generar la configuración de GRUB para activar la carga de la actualización de microcódigo ejecutando:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### Método manual

Alternativamente, los usuarios que administran su archivo de configuración GRUB manualmente pueden añadir `/boot/*fabricante_cpu*-ucode.img` (o `/*fabricante_cpu*-ucode.img` si `/boot` es una partición separada) como sigue:

 `/boot/grub/grub.cfg` 
```
...
echo 'Cargando ramdisk inicial'
initrd	**/boot/*fabricante_cpu*-ucode.img** /boot/initramfs-linux.img
...

```

Repítalo para cada entrada del menú.

### systemd-boot

Utilice la opción `initrd` para cargar el microcódigo, antes del ramdisk inicial, de la siguiente manera:

 `/boot/loader/entries/*entrada*.conf` 
```
title   Arch Linux
linux   /vmlinuz-linux
**initrd  /*fabricante_cpu*-ucode.img**
initrd  /initramfs-linux.img
...

```

El último microcódigo `*fabricante_cpu*-ucode.img` debe estar disponible durante el arranque en su [partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") (ESP). El ESP se debe montar como `/boot` para que el microcódigo se actualice cada vez que se actualice [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) o [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode). De lo contrario, copie `/boot/*fabricante_cpu*-ucode.img` a su ESP en cada actualización del paquete de microcódigo.

### EFISTUB

Añada dos opciones `initrd=`:

```
**initrd=/*fabricante_cpu*-ucode.img** initrd=/initramfs-linux.img

```

Para [kernels que se han generado como un solo archivo](/index.php/Systemd-boot_(Espa%C3%B1ol)#Preparar_los_kernels_para_/EFI/Linux "Systemd-boot (Español)") que contiene todos los initrd, cmdline y kernel, genere primero el initrd para integrarlo creando uno nuevo de la siguiente manera:

```
cat /boot/*fabricante_cpu*-ucode.img /boot/initramfs-linux.img > mi_nuevo_initrd
objcopy ... --add-section .initrd=mi_nuevo_initrd
```

### rEFInd

Edite las opciones de arranque en `/boot/refind_linux.conf` según el siguiente ejemplo:

```
"Arrancar utilizando las opciones predeterminadas" "rw root=PARTUUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* rw add_efi_memmap **initrd=/boot/*fabricante_cpu*-ucode.img** initrd=/boot/initramfs-linux.img"

```

Los usuarios que empleen [estancias manuales](/index.php/REFInd#Manual_boot_stanzas "REFInd") en `*esp*/EFI/refind/refind.conf` para definir los kernels deben añadir simplemente `initrd=/boot/*fabricante_cpu*-ucode.img` (o `/*fabricante_cpu*-ucode.img` si `/boot` es una partición separada) según sea necesario para las líneas de opciones, y no en la parte principal de la estancia. Por ejemplo:

```
options  "root=PARTUUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* rw add_efi_memmap **initrd=/boot/*fabricante_cpu*-ucode.img**"

```

### Syslinux

**Nota:** No debe haber espacios entre los archivos initrd `*fabricante_cpu*-ucode.img` y `initramfs-linux.img`. La línea `INITRD` debe ser exactamente como se ilustra a continuación.

Los múltiples initrd pueden estar separados por comas en `/boot/syslinux/syslinux.cfg`:

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD **../*fabricante_cpu*-ucode.img**,../initramfs-linux.img
...

```

### LILO

[LILO](/index.php/LILO "LILO") y posiblemente otros cargadores de arranque antiguos no admitan varias imágenes initrd. En ese caso, `*fabricante_cpu*-ucode.img` y `initramfs-linux.img` deberán combinarse en una imagen.

**Advertencia:** ¡La imagen fusionada debe recrearse después de cada actualización del kernel!

**Nota:** El orden es importante. La imagen original `initramfs-linux.img` debe estar concatenada **sobre** la imagen `*fabricante_cpu*-ucode.img`.

Para combinar ambas imágenes en una imagen llamada `initramfs-combinada.img`, se puede utilizar el siguiente comando:

```
# cat /boot/*fabricante_cpu*-ucode.img /boot/initramfs-linux.img > /boot/initramfs-combinada.img

```

Ahora, edite `/etc/lilo.conf` para cargar la nueva imagen.

```
...
initrd=/boot/initramfs-combinada.img
...

```

Y ejecute `lilo` como superusuario *(root)*:

```
# lilo

```

## Actualizaciones de microcódigo tardías

La carga tardía de las actualizaciones de microcódigo ocurre después de que el sistema se haya iniciado. Utiliza archivos en `/usr/lib/firmware/amd-ucode/` y `/usr/lib/firmware/intel-ucode/`.

Para los procesadores AMD, los archivos de actualización de microcódigo son proporcionados por [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

Para los procesadores Intel, ningún paquete proporciona los archivos de actualización de microcódigo ([FS#59841](https://bugs.archlinux.org/task/59841)). Para utilizar la carga tardía, debe extraer manualmente `intel-ucode/` del archivo provisto por Intel.

### Activar las actualizaciones de microcódigo tardías

A diferencia de la carga temprana, la carga tardía de las actualizaciones de microcódigo en Arch Linux se activa de manera predeterminada utilizando `/usr/lib/tmpfiles.d/linux-firmware.conf`. Después del arranque, el archivo se analiza mediante [systemd-tmpfiles-setup.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles-setup.service.8) y se actualiza el microcódigo de la CPU.

Para actualizar manualmente el microcódigo en un sistema en marcha, ejecute:

```
# echo 1 > /sys/devices/system/cpu/microcode/reload

```

Esto permite aplicar actualizaciones de microcódigo después de que [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) se haya actualizado sin reiniciar el sistema. Incluso puede automatizarlo con un [hook de pacman](/index.php?title=Pacman_hook_(Espa%C3%B1ol)&action=edit&redlink=1 "Pacman hook (Español) (page does not exist)"), por ejemplo:

 `/etc/pacman.d/hooks/microcode_reload.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Operation = Remove
Type = File
Target = usr/lib/firmware/amd-ucode/*

[Action]
Description = Aplicando actualizaciones de microcódigo de CPU...
When = PostTransaction
Depends = sh
Exec = /bin/sh -c 'echo 1 > /sys/devices/system/cpu/microcode/reload'
```

### Desactivar las actualizaciones de microcódigo tardías

Para los sistemas AMD, el microcódigo de la CPU se actualizará incluso si [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) no está instalado ya que los archivos son provistos por [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) ([FS#59840](https://bugs.archlinux.org/task/59840)). Para desactivar la carga tardía, debe anular el [archivo temporal](/index.php/Tmpfile_(Espa%C3%B1ol) "Tmpfile (Español)") `/usr/lib/tmpfiles.d/linux-firmware.conf`. Se puede hacer creando un archivo con el mismo nombre en `/etc/tmpfiles.d/`:

```
# ln -s /dev/null /etc/tmpfiles.d/linux-firmware.conf

```

## Comprobar que el microcódigo se actualizó en el arranque

Utilice *dmesg* para ver si el microcódigo se ha actualizado:

```
$ dmesg | grep microcode

```

En los sistemas Intel, se debería ver algo similar a lo siguiente en cada inicio, lo que indica que el microcódigo se actualiza muy pronto:

```
[    0.000000] CPU0 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.221951] CPU1 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.242064] CPU2 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.262349] CPU3 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.507267] microcode: CPU0 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507272] microcode: CPU1 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507276] microcode: CPU2 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507281] microcode: CPU3 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507286] microcode: CPU4 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507292] microcode: CPU5 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507296] microcode: CPU6 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507300] microcode: CPU7 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507335] microcode: Microcode Update Driver: v2.2.

```

**Nota:** La fecha mostrada no corresponde a la versión del paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) instalado. Muestra la última vez que Intel actualizó el microcódigo que corresponde al hardware específico que se está actualizando.

Es totalmente posible, particularmente con hardware más nuevo, que no haya una actualización de microcódigo para la CPU. En ese caso, la salida puede verse así:

```
[    0.292893] microcode: CPU0 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292899] microcode: CPU1 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292906] microcode: CPU2 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292912] microcode: CPU3 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292956] microcode: Microcode Update Driver: v2.2.

```

En los sistemas AMD que utilizan la carga temprana, la salida se vería así:

```
[    2.119089] microcode: microcode updated early to new patch_level=0x0700010f
[    2.119157] microcode: CPU0: patch_level=0x0700010f
[    2.119171] microcode: CPU1: patch_level=0x0700010f
[    2.119183] microcode: CPU2: patch_level=0x0700010f
[    2.119189] microcode: CPU3: patch_level=0x0700010f
[    2.119269] microcode: Microcode Update Driver: v2.2.

```

En los sistemas AMD que utilizan la carga tardía, la salida mostrará la versión del microcódigo anterior antes de volver a cargar el microcódigo y el nuevo una vez que se vuelva a cargar. Se vería algo como esto:

```
[    2.112919] microcode: CPU0: patch_level=0x0700010b
[    2.112931] microcode: CPU1: patch_level=0x0700010b
[    2.112940] microcode: CPU2: patch_level=0x0700010b
[    2.112951] microcode: CPU3: patch_level=0x0700010b
[    2.113043] microcode: Microcode Update Driver: v2.2.
[    6.429109] microcode: CPU2: new patch_level=0x0700010f
[    6.430416] microcode: CPU0: new patch_level=0x0700010f
[    6.431722] microcode: CPU1: new patch_level=0x0700010f
[    6.433029] microcode: CPU3: new patch_level=0x0700010f
[    6.433073] x86/CPU: CPU features have changed after loading microcode, but might not take effect.

```

## Cuales CPU aceptan actualizaciones de microcódigo

Los usuarios pueden consultar a Intel o AMD en los siguientes enlaces para ver si un modelo en particular es compatible:

*   [Centro de Investigación de Sistemas Operativos de AMD](http://www.amd64.org/microcode.html).
*   [Centro de descarga de Intel](https://downloadcenter.intel.com/SearchResult.aspx?lang=eng&keyword=processor%20microcode%20data%20file).

### Detectar actualización de microcódigo disponible

Es posible averiguar si `intel-ucode.img` contiene una imagen de microcódigo para la CPU en ejecución con [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool).

1.  [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) (no es necesario cambiar initrd para la detección)
2.  [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool)
3.  `# modprobe cpuid` 
4.  Extraiga la imagen de microcódigo y busque su cpuid:
     `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -` 
5.  Si hay una actualización disponible, debería aparecer debajo de *selected microcodes*
6.  Es posible que el microcódigo ya esté en la BIOS de su proveedor y no aparezca cargando en dmesg. Compárelo con el microcódigo actual ejecutando `grep microcode /proc/cpuinfo`

## Activar la carga temprana de microcódigo en kernels personalizados

Para que la carga temprana funcione en kernels personalizados, "CPU microcode loading support" debe compilarse en el kernel, **no** compilado como un módulo. Esto activará la opción "Early load microcode" que se debe establecer en `Y`.

```
CONFIG_BLK_DEV_INITRD=Y
CONFIG_MICROCODE=y
CONFIG_MICROCODE_INTEL=Y
CONFIG_MICROCODE_AMD=y

```

## Véase también

*   [Actualización de microcódigos - Experiencias en la comunidad](https://flossexperiences.wordpress.com/2013/11/17/updating-microcodes/)
*   [Notas sobre actualizaciones de microcódigo de Intel – Ben Hawkes](http://inertiawar.com/microcode/)
*   [Cargador de microcódigo del kernel - documentación del kernel](https://www.kernel.org/doc/Documentation/x86/microcode.txt)
*   [Errata encontrada en Haswell/Broadwell – AnandTech](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly)
*   [Proyecto iucode-tool en GitLab](https://gitlab.com/iucode-tool/iucode-tool)