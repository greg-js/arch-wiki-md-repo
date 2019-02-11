**Estado de la traducción**
Este artículo es una traducción de [EFISTUB](/index.php/EFISTUB "EFISTUB"), revisada por última vez el **2018-11-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=EFISTUB&diff=0&oldid=544457) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Arch boot process (Español)](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)")
*   [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")

El kernel de Linux admite arrancar con EFISTUB (EFI BOOT STUB). Esta característica permite que el firmware EFI cargue el kernel como un ejecutable EFI. La opción está activada de forma predeterminada en los kernels de Arch Linux o se puede activar mediante el establecimiento de la variable `CONFIG_EFI_STUB=y` en la configuración del kernel. Vea [The EFI Boot Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt) para más información.

Con EFISTUB un kernel se puede arrancar directamente por una placa base UEFI o indirectamente usando un [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)"). Este último es recomendado si se tienen múltiples pares de kernel/initramfs y el menú de inicio UEFI de su placa base no es fácil de usar.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prepararse para EFISTUB](#Prepararse_para_EFISTUB)
*   [2 Arrancar EFISTUB](#Arrancar_EFISTUB)
    *   [2.1 Utilizar un gestor de arranque](#Utilizar_un_gestor_de_arranque)
    *   [2.2 Utilizar directamente UEFI](#Utilizar_directamente_UEFI)
        *   [2.2.1 efibootmgr](#efibootmgr)
        *   [2.2.2 efibootmgr con el archivo .efi](#efibootmgr_con_el_archivo_.efi)
        *   [2.2.3 Intérprete de órdenes de UEFI](#Intérprete_de_órdenes_de_UEFI)
        *   [2.2.4 Utilizar un script startup.nsh](#Utilizar_un_script_startup.nsh)
*   [3 Véase también](#Véase_también)

## Prepararse para EFISTUB

Primero, debe crear una [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") y elegir cómo se monta. Vea [EFI system partition (Español)#Montar la partición](/index.php/EFI_system_partition_(Espa%C3%B1ol)#Montar_la_partición "EFI system partition (Español)") para todas las opciones de montaje disponibles.

**Sugerencia:**

*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") actualizará directamente el kernel que leerá el firmware EFI si monta la partición ESP en `/boot`.
*   Puede mantener el kernel e initramfs fuera de la partición ESP si utiliza un gestor de arranque que tenga un controlador de sistema de archivos para la partición donde residan, por ejemplo [rEFInd](/index.php/REFInd "REFInd").

## Arrancar EFISTUB

**Nota:** la ruta a initramfs para EFISTUB debe ser relativa con respecto a la raíz de la «*EFI System Partition*» y usar barras invertidas (de acuerdo con los estándares de EFI). Por ejemplo, si initramfs se encuentra en `*esp*/EFI/arch/initramfs-linux.img`, la línea correspondiente a UEFI debe ser `initrd=\EFI\arch\initramfs-linux.img`. En los siguientes ejemplos asumiremos que todo está en `*esp*/`.

### Utilizar un gestor de arranque

Existen varios gestores de arranque UEFI que pueden proporcionar opciones adicionales o simplificar el proceso de arranque UEFI —especialmente si tiene múltiples kernels/sistemas operativos—. Vea [Arch boot process (Español)#Gestor de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque "Arch boot process (Español)") para más información.

Es posible lanzar un kernel EFISTUB desde el intérprete de órdenes de UEFI como si fuera una aplicación normal UEFI. En este caso, los parámetros del kernel se pasan como parámetros normales al archivo del kernel EFISTUB lanzado.

```
> fs0:
> \vmlinuz-linux root=PARTUUID=3518bb68-d01e-45c9-b973-0b5d918aae96 rw initrd=\initramfs-linux.img

```

Para evitar tener que recordar todos los parámetros del kernel una y otra vez, puede guardar la orden ejecutable como un script de intérprete de órdenes (por ejemplo, como `archlinux.nsh`) en la partición del sistema UEFI, luego ejecútelo con:

```
> fs0:
> archlinux

```

### Utilizar directamente UEFI

UEFI está diseñado para eliminar la necesidad de tener un gestor de arranque intermediario como, por ejemplo, [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"). Si su placa base tiene una buena implementación UEFI, es posible incluir los parámetros del kernel dentro de una entrada de arranque UEFI para que la placa base arranque Arch directamente. Puede utilizar `efibootmgr` o UEFI Shell v2 para modificar las entradas de arranque de su placa base (para que incluya a Arch).

#### efibootmgr

La orden sería como sigue:

```
# efibootmgr --disk */dev/sdX* --part *Y* --create --label "Arch Linux" --loader /vmlinuz-linux --unicode 'root=PARTUUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* rw initrd=\initramfs-linux.img' --verbose

```

Donde `*/dev/sdX*` and `*Y*` se deben cambiar para reflejar el disco y la partición donde se encuentra la ESP. Cambie el parámetro `root=` para reflejar la raiz de Linux. Tenga en cuenta que el argumento `-u`/`--unicode` entre comillas es solo un ejemplo de la lista de los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), por lo que es posible que deba agregar parámetros adicionales (por ejemplo, para [suspender en disco](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate") o [Microcode (Español)](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)")).

**Sugerencia:** guarde la orden para crear su entrada de arranque en un script de intérprete de órdenes en algún lugar, lo que facilitará su modificación (por ejemplo, al cambiar los parámetros del kernel

Después de agregar la entrada de inicio, puede verificar que dicha entrada se añadió correctamente con:

```
# efibootmgr --verbose

```

**Nota:** algunas combinaciones de kernel y `efibootmgr` podrían negarse a crear nuevas entradas de inicio. Esto podría ser debido a la falta de espacio libre en la memoria NVRAM. Podría tratar de eliminar cualquier archivo de volcado de EFI:
```
# rm /sys/firmware/efi/efivars/dump-*

```
O, como último recurso, arrancar con el parámetro del kermel `efi_no_storage_paranoia`. También puede intentar degradar su instalación de efibootmgr a la versión 0.11.0 si la tiene disponible en su memoria caché. Esta versión funciona con la versión 4.0.6 de Linux. Véase el bug de la discusión [FS#34641](https://bugs.archlinux.org/task/34641) para más información.

Para establecer el orden de arranque, ejecute:

```
# efibootmgr --bootorder *XXXX*,*XXXX* --verbose

```

donde *XXXX* es el número que aparece en la salida de la orden `efibootmgr` de cada entrada.

Más información sobre efibootmgr en [Unified Extensible Firmware Interface (Español)#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#efibootmgr "Unified Extensible Firmware Interface (Español)"). Publicación del foro: [https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040](https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040) .

#### efibootmgr con el archivo .efi

Si usa [cryptboot](https://aur.archlinux.org/packages/cryptboot/) y [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/) para generar sus propias claves para [Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot") y firma con ellas initramfs y el kernel, cree, luego, una imagen *.efi* de arranque, [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) puede usarse directamente para arrancar el archivo *.efi* file:

```
# efibootmgr --create --disk /dev/sdX --part *partition_number* --label "*label*" --loader "EFI\*folder*\*file*.efi" --verbose

```

Véase [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8) para obtener una explicación de las opciones.

#### Intérprete de órdenes de UEFI

Algunas implementaciones de UEFI hacen que sea difícil modificar la NVRAM con éxito usando efibootmgr. Si efibootmgr no puede crear una entrada con éxito, puede usar la orden [bcfg](/index.php/UEFI#bcfg "UEFI") en UEFI Shell v2 (es decir, desde la imagen iso live de Arch Linux).

Primero, averigüe el número de dispositivo donde reside la [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)"), usando:

```
Shell> map

```

En este ejemplo, `1` se utiliza como número de dispositivo. Para listar los contenidos de [EFI system partition (Español)](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") escriba:

```
Shell> ls fs1:

```

Para ver las entradas de arranque actuales escriba:

```
Shell> bcfg boot dump

```

Para agregar una entrada para el kernel, utilice:

```
Shell> bcfg boot add *N* fs1:\vmlinuz-linux "Arch Linux"

```

donde `*N*` es la ubicación donde se agregará la entrada en el menú de inicio. 0 es el primer elemento del menú. Los elementos de menú ya existentes se desplazarán en el menú sin que se descarten.

Para agregar las opciones de kernel necesarias, primero cree un archivo en la ESP:

```
Shell> edit fs1:\options.txt

```

En el archivo agregue la línea de arranque. Por ejemplo:

```
root=/dev/sda2 ro initrd=\initramfs-linux.img

```

**Nota:** añada espacios adicionales al principio de la línea en el archivo. Hay una marca de demanda de bytes al principio de la línea que captará cualquier carácter que esté a su lado, lo que causará un error al iniciar.

Presione `F2` para guardar y luego `F3` para salir.

Para agregar estas opciones a su entrada anterior, haga lo siguiente:

```
Shell> bcfg boot -opt *N* fs1:\options.txt

```

Repita este proceso para cualquier entrada adicional.

Para eliminar un elemento previamente agregado, escriba:

```
Shell> bcfg boot rm *N*

```

#### Utilizar un script startup.nsh

Algunas implementaciones de UEFI no retienen las variables de EFI entre los arranques en frío (por ejemplo, [VirtualBox (Español)](/index.php/VirtualBox_(Espa%C3%B1ol) "VirtualBox (Español)")) y cualquier cosa que se haya configurado a través de la interfaz del firmware de UEFI se perderá durante el apagado.

La [UEFI Shell Specification 2.0](http://www.uefi.org/sites/default/files/resources/UEFI_Shell_Spec_2_0.pdf) establece que un script llamado `startup.nsh` en la raíz de la partición de ESP siempre debe interpretarse y puede contener instrucciones arbitrarias; entre las que se puede establecer una línea de carga de arranque. Asegúrese de montar la partición ESP en `/boot` y cree un script `startup.nsh` que contenga una línea de carga de arranque del kernel. Por ejemplo:

```
vmlinuz-linux rw root=/dev/sdX [rootfs=myfs] [rootflags=myrootflags] \
 [kernel.flag=foo] [mymodule.flag=bar] \
 [initrd=\intel-ucode.img] initrd=\initramfs-linux.img

```

Este método funcionará con casi todas las versiones de firmware UEFI que pueda encontrar en hardware real, por lo que puede usarlo como último recurso. **El script debe ser una única línea larga.** Las secciones entre paréntesis son opcionales y se ofrecen solo como una guía. Los saltos de línea de estilo shell son solo para clarificación visual. Los sistemas de archivos FAT utilizan la barra invertida como separador de ruta y, en este caso, la barra diagonal inversa declara que el initramfs se encuentra en la raíz de la partición ESP. Solo se carga el microcódigo de Intel en la línea de parámetros de arranque; El microcódigo de AMD se lee del disco más tarde durante el proceso de arranque; Esto se hace automáticamente por el kernel.

## Véase también

*   [Linux Kernel Documentation on EFISTUB](https://www.kernel.org/doc/Documentation/efi-stub.txt)
*   [Linux Kernel EFISTUB Git Commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=291f36325f9f252bd76ef5f603995f37e453fc60;hp=55839d515495e766605d7aaabd9c2758370a8d27)
*   [Rod Smith's page on EFISTUB](http://www.rodsbooks.com/efi-bootloaders/efistub.html)