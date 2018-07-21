Artículos relacionados

*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [pacman](/index.php/Pacman "Pacman")
*   [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine")

Antes de desactualizar uno o varios paquetes, considere por qué desea hacerlo. Si se debe a un error, busque en [rastreador de errores](https://bugs.archlinux.org/) las tareas existentes. Si no hay ninguna, agregue un nueva tarea; es mejor corregir los errores, o al menos advertir a otros usuarios de posibles problemas.

**Advertencia:**

*   La desactualización de un paquete puede requerir que sus dependencias también sean desactualizadas. Cuando el número de paquetes a desactualizar es grande, considere usar una instantánea. Ver [Cómo restaurar todos los paquetes a una fecha específica.](/index.php/Arch_Linux_Archive#How_to_restore_all_packages_to_a_specific_date "Arch Linux Archive").
*   Tenga cuidado con los cambios en los archivos de configuración y scripts. Por ahora, *pacman* se encargará de esto por nosotros, siempre y cuando no eludamos sus medidas de seguridad.
*   Si la desactualización implica un cambio de nombre, toda dependencia puede necesitar ser desactualizada o también [reconstruida](/index.php/Frequently_asked_questions_(Espa%C3%B1ol)#.C2.BFQu.C3.A9_pasa_si_ejecuto_una_actualizaci.C3.B3n_completa_del_sistema_y_hay_una_actualizaci.C3.B3n_de_una_biblioteca_compartida.2C_pero_no_para_las_aplicaciones_que_dependen_de_ella.3F "Frequently asked questions (Español)") .

## Contents

*   [1 Volver a una versión anterior del paquete](#Volver_a_una_versi.C3.B3n_anterior_del_paquete)
    *   [1.1 Usando la caché de pacman](#Usando_la_cach.C3.A9_de_pacman)
    *   [1.2 Desactualizando el kernel](#Desactualizando_el_kernel)
    *   [1.3 Archivo Arch Linux](#Archivo_Arch_Linux)
    *   [1.4 Reconstrucción del paquete](#Reconstrucci.C3.B3n_del_paquete)
    *   [1.5 Automatización](#Automatizaci.C3.B3n)
*   [2 Volver de [testing]](#Volver_de_.5Btesting.5D)

## Volver a una versión anterior del paquete

### Usando la caché de pacman

Si un paquete se instaló anteriormente, y la [caché de pacman](/index.php/Pacman_(Espa%C3%B1ol)#Limpiar_la_memoria_cach.C3.A9_de_los_paquetes "Pacman (Español)") no se ha limpiado, instale una versión anterior de `/var/cache/pacman/pkg/`.

Este proceso eliminará el paquete actual e instalará la versión anterior. Los cambios de dependencia serán gestionados, pero [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") no gestionará conflictos de versión. Si una librería u otro paquete necesita ser desactualizado con los paquetes, por favor tenga en cuenta que usted también tendrá que desactualizarlo.

```
# pacman -U /var/cache/pacman/pkg/*package*-*old_version*.pkg.tar.xz

```

Una vez revertido el paquete, añádalo temporalmente al archivo [IgnorePkg section](/index.php/Pacman_(Espa%C3%B1ol)#Evitar_la_actualizaci.C3.B3n_de_un_paquete "Pacman (Español)") de `pacman.conf`, hasta que se resuelva el problema con el paquete actualizado.

### Desactualizando el kernel

En caso de problemas con un nuevo kernel, los paquetes de Linux pueden ser desactualizados a los últimos que funcionen [#Usando la caché de pacman](#Usando_la_cach.C3.A9_de_pacman). Vaya al directorio `/var/cache/pacman/pkg` y desactualice al menos [linux](https://www.archlinux.org/packages/?name=linux), [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) y cualquier módulo del núcleo. Por ejemplo:

```
# pacman -U linux-4.15.8-1-x86_64.pkg.tar.xz linux-headers-4.15.8-1-x86_64.pkg.tar.xz virtualbox-host-modules-arch-5.2.8-4-x86_64.pkg.tar.xz

```

**Sugerencia:** Si no puede arrancar después de una actualización del núcleo, puede desactualizarlo haciendo un [chrooting](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") al sistema.Arranque usando un Arch Linux [USB flash installation media](/index.php/USB_flash_installation_media_(Espa%C3%B1ol) "USB flash installation media (Español)") y monte la partición donde está instalado su sistema en `/mnt`. Si tiene `/boot` o `/var` en particiones separadas, móntelas también en `/mnt`. (por ejemplo, `mount /dev/sdc3 /mnt/boot`). Luego haga *chroot* en el sistema usando: `# arch-chroot /mnt /bin/bash` Ahora puede ir al directorio de caché de *pacman* y desactualizar los paquetes de Linux usando el comando indicado arriba. Una vez hecho esto, salga del chroot (con `exit`) y reinicie.

### Archivo Arch Linux

El [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") es una instantánea diaria de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Puede usarse para [instalar una versión anterior de un paquete](/index.php/Arch_Linux_Archive#How_to_downgrade_one_package "Arch Linux Archive"), o [restaurar el sistema a una fecha anterior](/index.php/Arch_Linux_Archive#How_to_restore_all_packages_to_a_specific_date "Arch Linux Archive").

### Reconstrucción del paquete

Si el paquete no está disponible, busque el [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") correcto y reconstrúyalo con [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)").

Para los paquetes de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), recupere el *PKGBUILD* con [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") y cambie la versión del software. Alternativamente, busque el paquete en el sitio web [Paquetes](https://www.archlinux.org/packages), haga clic en "Ver cambios" y navegue hasta la versión deseada. Los archivos están disponibles a través de una instantánea `.tar.gz` y a través de la vista *Árbol*.

Consulte también [Arch Build System (Español)#Revisión de un paquete antiguo](/index.php/Arch_Build_System_(Espa%C3%B1ol)#Revisi.C3.B3n_de_un_paquete_antiguo "Arch Build System (Español)").

Los paquetes antiguos de AUR pueden construirse revisando un compromiso antiguo en el repositorio de GIT del paquete AUR. Para los PKGBUILD anteriores a 2015 AUR3 PKGBUILDs, consulte los [Arch User Repository#Git repositories for AUR3 packages](/index.php/Arch_User_Repository#Git_repositories_for_AUR3_packages "Arch User Repository").

### Automatización

[downgrader](https://aur.archlinux.org/packages/downgrader/) es una herramienta que funciona con libalpm, admite el registro de pacman y desactualiza los paquetes usando la caché local [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") y [ARM](http://repo-arm.archlinuxcn.org).

El paquete [downgrade](https://aur.archlinux.org/packages/downgrade/) es un script Bash para desactualizar uno (o varios) paquetes, utilizando el caché pacman o el [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine").Vea `man downgrade` para más detalles.

[agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/) lista rápidamente / obtiene / instala paquetes desde [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive").

## Volver de [testing]

Ver [Official repositories#Disabling testing repositories](/index.php/Official_repositories#Disabling_testing_repositories "Official repositories").