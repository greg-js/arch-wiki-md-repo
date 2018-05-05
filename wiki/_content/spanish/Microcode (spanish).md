El [microcódigo del procesador](https://en.wikipedia.org/wiki/es:Microc%C3%B3digo "wikipedia:es:Microcódigo") es similar al firmware del procesador. El kernel es capaz de actualizar el firmware del procesador sin necesidad de actualizarlo a través de una actualización de la BIOS.

	*El archivo de datos del microcódigo contiene las definiciones más recientes de microcódigo para todos los procesadores de Intel. Intel lanza actualizaciones de microcódigo para corregir el comportamiento del procesador como se documenta en las respectivas actualizaciones de las especificaciones del procesador. Mientras que el método ordinario para obtener esta actualización de microcódigo es a través de una actualización de la BIOS, Intel da cuenta de que esto puede ser una molestia administrativa. El sistema operativo Linux y los productos de VMware ESX tienen un mecanismo para actualizar el microcódigo después de arrancar. Por ejemplo, este archivo será utilizado por el mecanismo del sistema operativo si el archivo se coloca en el directorio /etc/firmware del sistema Linux.* ~[Intel](https://downloadcenter.intel.com/Detail_Desc.aspx?DwnldID=23082)

## Contents

*   [1 Actualización del microcódigo](#Actualizaci.C3.B3n_del_microc.C3.B3digo)
    *   [1.1 Activación de las actualizaciones del microcódigo de Intel](#Activaci.C3.B3n_de_las_actualizaciones_del_microc.C3.B3digo_de_Intel)
    *   [1.2 Ejemplos específicos](#Ejemplos_espec.C3.ADficos)
        *   [1.2.1 EFI boot stub / EFI handover](#EFI_boot_stub_.2F_EFI_handover)
        *   [1.2.2 Gummiboot](#Gummiboot)
        *   [1.2.3 rEFInd](#rEFInd)
        *   [1.2.4 GRUB](#GRUB)
        *   [1.2.5 Método automático](#M.C3.A9todo_autom.C3.A1tico)
        *   [1.2.6 Método manual](#M.C3.A9todo_manual)
        *   [1.2.7 Syslinux](#Syslinux)
*   [2 Verificar qué microcódigo quedó actualizado en el arranque](#Verificar_qu.C3.A9_microc.C3.B3digo_qued.C3.B3_actualizado_en_el_arranque)
*   [3 ¿Qué CPU aceptan actualizaciones de microcódigo?](#.C2.BFQu.C3.A9_CPU_aceptan_actualizaciones_de_microc.C3.B3digo.3F)
    *   [3.1 Detectar la actualización del microcódigo disponible](#Detectar_la_actualizaci.C3.B3n_del_microc.C3.B3digo_disponible)
    *   [3.2 Activación de la carga de Intel Early Microcode en Kernels personalizados](#Activaci.C3.B3n_de_la_carga_de_Intel_Early_Microcode_en_Kernels_personalizados)

## Actualización del microcódigo

Para los procesadores de Intel, [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Para los procesadores de AMD, las actualizaciones del microcódigo están disponibles en el paquete [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware), que se instala como parte del sistema base.

### Activación de las actualizaciones del microcódigo de Intel

**Advertencia:** Desde linux 3.17-2, linux-lts 3.14.21-2 y siguientes, las actualizaciones del microcódigo de Intel no están activadas de forma automática. Algunos kernels disponibles en AUR han seguido el camino de los kernels oficiales de ARCH en este sentido: desde linux-ck 3.16.6-3, las actualizaciones del microcódigo de Intel no se activan automáticamente.

Estas actualizaciones deben ser activadas añadiendo `/boot/intel-ucode.img` como el primer initrd en el archivo de configuración del gestor de arranque. Este se añade además del archivo initrd normal.

### Ejemplos específicos

#### EFI boot stub / EFI handover

Añada dos opciones `initrd=`:

 `initrd=/intel-ucode.img initrd=/initramfs-linux.img` 

#### Gummiboot

Utilice la opción `initrd` dos veces en `/boot/loader/entries/*.conf`:

```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options ...
```

#### rEFInd

Edite las opciones de arranque en `/boot/refind_linux.conf` según se indica arriba para EFI boot stub, ejemplo:

 `"Boot with standard options" "ro root=UUID=(...) quiet initrd=/intel-ucode.img initrd=/initramfs-linux.img"` 

Los usuarios que emplean stanza manuales en /boot/refind.conf para definir los kernels, simplemente deben añadir initrd=/intel-ucode.img o /boot/intel-ucode.img, según se requiera, a la línea options, y no en la parte principal de stanza.

#### GRUB

#### Método automático

Con el lanzamiento de grub-1:2.02-beta2-5, `/usr/bin/grub-mkconfig` manejará automáticamente la actualización del microcódigo.

`grub-mkconfig` detectará automáticamente las actualizaciones de microcódigo y configurará [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") apropiadamente. Después de [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode), es necesario regenerar la configuración de GRUB para activar la carga del microcódigo con el comando:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### Método manual

Alternativamente, los usuarios que deseen gestionar el archivo de configuración de grub manualmente pueden añadir `/intel-ucode.img` o `/boot/intel-ucode.img` a `grub.cfg` como sigue:

```
	[...]
	echo	'Loading initial ramdisk ...'
	initrd	/intel-ucode.img /initramfs-linux.img
	[...]

```

**Nota:** Repítalo para cada entrada del menú.

**Advertencia:** Este archivo será automáticamente sobrescrito por `/usr/bin/grub-mkconfig` durante ciertas actualizaciones negando los cambios.

#### Syslinux

Múltiples initrd pueden estar separados por comas en `/boot/syslinux/syslinux.cfg`:

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD ../intel-ucode.img,../initramfs-linux.img
    APPEND ...
```

## Verificar qué microcódigo quedó actualizado en el arranque

Utilice `/usr/bin/dmesg` para ver si el microcódigo se ha actualizado: `dmesg | grep microcode`

En los sistemas Intel se debe ver algo similar a lo siguiente, lo que indica que el microcódigo se actualiza tempranamente:

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
[    0.507335] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
```

Es completamente posible, en particular con hardware más nuevo, que no haya actualizaciones del microcódigo para la CPU. En esos caso, la salida puede tener este aspecto:

```
[    0.292893] microcode: CPU0 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292899] microcode: CPU1 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292906] microcode: CPU2 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292912] microcode: CPU3 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292956] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
```

En los sistemas AMD, el microcódigo se actualiza un poco más adelante en el proceso de arranque, por lo que la salida sería algo como esto:

```
[    0.807879] microcode: CPU0: patch_level=0x01000098
[    0.807888] microcode: CPU1: patch_level=0x01000098
[    0.807983] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
[   16.150642] microcode: CPU0: new patch_level=0x010000c7
[   16.150682] microcode: CPU1: new patch_level=0x010000c7
```

**Nota:** La fecha emitida no se corresponde con la versión del paquete [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) instalado. Lo que muestra es la última vez que Intel actualizó el microcódigo que se corresponde con el hardware específico que es objeto de actualización.

## ¿Qué CPU aceptan actualizaciones de microcódigo?

Los usuarios pueden consultar, ya sea Intel o AMD, en los siguientes enlaces para ver si es soportado un modelo en particular:

*   [AMD's Operating System Research Center](http://www.amd64.org/microcode.html).
*   [Intel's download center](https://downloadcenter.intel.com/Detail_Desc.aspx?DwnldID=24290&lang=eng).

#### Detectar la actualización del microcódigo disponible

Es posible saber si intel-ucode.img contiene una imagen de microcódigo para la cpu sobre la que corre con [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/).

*   Instale [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) (no es necesario cambiar initrd para la detección)
*   Instale [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/) disponible en [AUR](/index.php/AUR "AUR")
*   `# modprobe cpuid`
*   `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -`
    (Extrae la imagen microcode y la busca para su cpuid)
*   Si hay una actualización disponible, debería aparecer debajo de *selected microcodes*

#### Activación de la carga de Intel Early Microcode en Kernels personalizados

A fin de que la carga temprana funcione en kernels personalizados, necesita que «CPU microcode loading support» sea compilado en el kernel mismo NO como módulo del kernel. Esto activará el prompt «Early load microcode» que debe ser ajustado a «Y».

```
CONFIG_MICROCODE=y
CONFIG_MICROCODE_INTEL=y
CONFIG_MICROCODE_INTEL_EARLY=y
CONFIG_MICROCODE_EARLY=y

```