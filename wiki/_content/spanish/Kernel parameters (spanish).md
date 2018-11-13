Hay tres formas de pasar opciones al núcleo (también conocido por su nombre en inglés, *kernel*) y de ese modo controlar su comportamiento:

1.  Durante la compilación del núcleo.
2.  Al arrancar el núcleo (por lo general, cuando se invoca desde un gestor de arranque).
3.  En tiempo de ejecución (a través de los archivos en `/proc` y `/sys`).

Esta página explica con más detalle el segundo método y muestra una lista de los parámetros del núcleo más utilizados en Arch Linux.

## Contents

*   [1 Configuración](#Configuración)
    *   [1.1 Syslinux](#Syslinux)
    *   [1.2 GRUB](#GRUB)
    *   [1.3 GRUB Legacy](#GRUB_Legacy)
    *   [1.4 LILO](#LILO)
    *   [1.5 Gummiboot](#Gummiboot)
    *   [1.6 rEFInd](#rEFInd)
*   [2 Lista de parámetros](#Lista_de_parámetros)
*   [3 Véase también](#Véase_también)

## Configuración

Los parámetros del núcleo se pueden configurar de forma temporal mediante la edición del menú de arranque cuando se muestra, o, de forma permanente, modificando el archivo de configuración del gestor de arranque.

Aquí vamos a añadir los parámetros `quiet` y `splash` en [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)"), [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") y [LILO](/index.php/LILO "LILO").

#### Syslinux

*   Pulse `Tab` cuando el menú se visualice y agregue los parámetros al final de la cadena:

	 `> .linux ../vmlinuz-linux root=/dev/sda3 ro initrd=../initramfs-linux.img *quiet splash*` 

	Pulse `Intro` para arrancar con estos parámetros.

*   Para hacer permanente la modificación al reiniciar el sistema, edite `/boot/syslinux/syslinux.cfg` y añada los parámetros a la línea `APPEND`:

	 `APPEND root=/dev/sda3 ro *quiet splash*` 

Para obtener más información sobre la configuración de Syslinux, consulte el artículo [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)").

#### GRUB

*   Pulse `e` cuando el menú se visualice+ y agregue los parámetros al final de la línea `linux`:

	 `linux   /boot/vmlinuz-linux root=UUID=978e3e81-8048-4ae1-8a06-aa727458e8ff ro  *quiet splash*` 

	Pulse `b` para arrancar con estos parámetros.

*   Para hacer el cambio permanente después de reiniciar el sistema, se *podría* modificar manualmente `/boot/grub/grub.cfg` con la línea exacta vista arriba, para los principiantes se recomienda:

	Editar `/etc/default/grub` y añadir las opciones del *kernel* para la línea `GRUB_CMDLINE_LINUX_DEFAULT`:

	 `GRUB_CMDLINE_LINUX_DEFAULT="*quiet splash*"` 

	Y después vuelva a regenerar automáticamente el archivo `grub.cfg` con la orden:

	 `# grub-mkconfig -o /boot/grub/grub.cfg` 

Para obtener más información sobre la configuración de GRUB, consulte el artículo [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)").

#### GRUB Legacy

*   Pulse `e` cuando el menú aparece y agregue los parámetros al final de la línea `kernel`:

	 `kernel /boot/vmlinuz-linux root=/dev/sda3 ro *quiet splash*` 

	Pulse `b` para arrancar con estos parámetros.

*   Para hacer el cambio permanentes después de reiniciar el sistema, edite `/boot/grub/menu.lst` y añada a la línea del `kernel` los parámetros , exactamente igual que antes.

Para obtener más información sobre la configuración de GRUB Legacy, consulte el artículo [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

#### LILO

*   Añada a `/etc/lilo.conf`:

```
image=/boot/vmlinuz-linux
        ...
        *quiet splash*
```

Para obtener más información sobre la configuración de LILO, consulte el artículo [LILO](/index.php/LILO "LILO").

#### Gummiboot

*   Pulse `e` cuando aparezca el menú y agregue los parámetros al final de la cadena:

	 `initrd=\initramfs-linux.img root=/dev/sda2 rw *quiet splash*` 

	Presione `Intro` para arrancar con dichos parámetros.

**Nota:** Si no tiene establecido un tiempo de espera del menú, necesitará mantener pulsada la barra `Espaciadora` durante el arranque para que el menú de Gummiboot aparezca.

*   Para hacer que los cambios permanezcan tras el reinicio, edite `/boot/loader/entries/arch.conf` (suponiendo que haya establecido la [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#EFI_System_Partition "Unified Extensible Firmware Interface (Español)") y configurado lo archivos de acuerdo a las instrucciones de la [guía para principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Gummiboot "Beginners' guide (Español)")) y añada lo siguiente a la línea `options`:

	 `options root=/dev/sda2 rw *quiet splash*` 

Para obtener más información sobre la configuración de Gummiboot, consulte el artículo [Gummiboot](/index.php/Gummiboot "Gummiboot").

#### rEFInd

*   Para hacer que el cambio permanezca al reiniciar el sistema, edite `/boot/EFI/arch/refind_linux.conf` y añada a todas las líneas o a las que lo necesiten, por ejemplo:

	 `"Boot to X"   "root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff ro rootfstype=ext4 quiet splash` 

*   Si ha desactivado la detección automática de los sistemas operativos en rEFInd y se han definido, en su lugar, dichos sistemas operativos por párrafos en el archivo `/boot/EFI/refind/refind.conf`, entonces, para cargar su sistema operativo, puede editar el archivo como sigue:

```
menuentry "Arch" {
	loader /EFI/arch/vmlinuz-arch.efi
	options "quiet splash ro root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff"
```

Para obtener más información sobre la configuración de los parámetros del núcleo en rEFInd, véase

1.  [Configuring the rEFInd Bootmanager](http://www.rodsbooks.com/refind/linux.html)
2.  [Methods of Booting Linux](http://www.rodsbooks.com/refind/linux.html)

## Lista de parámetros

Los parámetros siempre vienen como `parameter` o `parameter=value`. Todos estos parámetros distinguen entre mayúsculas y minúsculas.

**Nota:** No todas las opciones de la lista están siempre disponibles. La mayoría se asocian con los subsistemas y funcionan solo si el kernel está configurado con los subsistemas compilados en los mismos. También dependen de la presencia del hardware al que estén asociado.

| parámetro | Descripción |
| `root=` | Sistema de archivos root. |
| `ro` | Monta el dispositivo root como solo lectura en el arranque. |
| `rw` | Monta el dispositivo root como lectura-escritura en el arranque (por defecto). |
| `initrd=` | Especifica la ubicación del disco RAM inicial. |
| `init=` | Ejecuta el binario especificado en lugar de `/sbin/init` (enlace simbólico a [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") en Arch) como proceso init. |
| `init=/bin/sh` | Arranca en modo shell. |
| `systemd.unit=` |
| `systemd.unit=multi-user` | Arranca en el runlevel especificado. |
| `systemd.unit=rescue` | Arranca en modo usuario único (root). |
| `nomodeset` | Desactiva [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). |

Para obtener una lista completa de todas las opciones, consulte la [documentación del núcleo Linux](https://www.kernel.org/doc/Documentation/kernel-parameters.txt).

## Véase también

*   [sysctl](/index.php/Sysctl "Sysctl")
*   [Power saving#Kernel parameters](/index.php/Power_saving#Kernel_parameters "Power saving")
*   [Lista de parámetros del núcleo Linux con más explicaciones y agrupados por opciones similares](http://files.kroah.com/lkn/lkn_pdf/ch09.pdf)