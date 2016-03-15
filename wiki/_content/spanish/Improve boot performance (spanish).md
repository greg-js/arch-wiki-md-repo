## Contents

*   [1 Prefacio](#Prefacio)
*   [2 Modificación de los archivos de arranque](#Modificaci.C3.B3n_de_los_archivos_de_arranque)
    *   [2.1 /boot/grub/menu.lst](#.2Fboot.2Fgrub.2Fmenu.lst)
    *   [2.2 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
*   [3 Compilación de un kernel personalizado](#Compilaci.C3.B3n_de_un_kernel_personalizado)
*   [4 Additional Resources](#Additional_Resources)

## Prefacio

Mejorar el rendimiento de arranque de un sistema puede proporcionar reducido los tiempos de espera de arranque y un medio para aprender más acerca de cómo ciertos ficheros del sistema y scripts interactúan entre sí. Este artículo trata de los métodos globales sobre cómo mejorar el rendimiento de arranque de un sistema.

## Modificación de los archivos de arranque

### /boot/grub/menu.lst

Este archivo le permite modificar la línea de comandos del kernel en el arranque. Un par de maneras de acelerar el tiempo de arranque usando el archivo a modificar el núcleo de línea de comandos es eliminar las entradas de framebuffer, y establecer el nivel de registro de núcleo a un bajo nivel de registro con **quiet**. Para más parámetros del núcleo y `/boot/grub/menu.lst` ejemplos echa un vistazo a la página de archlinux en [GRUB](/index.php/GRUB "GRUB"). Eliminar los actuales <tt>vga=</tt> [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") entradas resolución y **logo.nologo**, los parámetros para el kernel que desee:

```
kernel /vmlinuz26 root=/dev/disk/by-uuid/UUID ro logo.nologo quiet

```

### /etc/mkinitcpio.conf

Eliminar los HOOKS que no es necesario, y considerar el uso de sólo la base (a veces es necesario también udev), junto con los módulos que necesite para su dispositivo raíz (y el teclado, en lugar de usbinput).

Más información en el [mkinitcpio article](/index.php/Mkinitcpio "Mkinitcpio").

## Compilación de un kernel personalizado

TPara reducir el tiempo de arranque, un núcleo desnudo es una necesidad. [leer mas sobre copilar el kernel.](/index.php/Kernel_Compilation_From_Source "Kernel Compilation From Source")

## Additional Resources

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [udev](/index.php/Udev "Udev")
*   [Daemons](/index.php/Daemons "Daemons")
*   [rc.conf](/index.php/Rc.conf "Rc.conf")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [Maximizing performance](/index.php/Maximizing_performance "Maximizing performance")
*   [Systemd](/index.php/Systemd "Systemd")