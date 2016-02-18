Arch Linux provee varios metodos para compilar el kernel. Usar [Arch Build System](/index.php/Arch_Build_System "Arch Build System") es el recomendado.

## Contents

*   [1 Usando Arch Build System](#Usando_Arch_Build_System)
    *   [1.1 Instalando Arch Build System](#Instalando_Arch_Build_System)
    *   [1.2 Consiguiendo los ingredientes](#Consiguiendo_los_ingredientes)
    *   [1.3 Modificando el PKGBUILD](#Modificando_el_PKGBUILD)
        *   [1.3.1 Cambiando pkgname](#Cambiando_pkgname)
        *   [1.3.2 Modificando build()](#Modificando_build.28.29)
        *   [1.3.3 Cambiando la función package_kernel26()](#Cambiando_la_funci.C3.B3n_package_kernel26.28.29)
    *   [1.4 Compilando con varios núcleos](#Compilando_con_varios_n.C3.BAcleos)
    *   [1.5 Compilación](#Compilaci.C3.B3n)
    *   [1.6 Instalación](#Instalaci.C3.B3n)
    *   [1.7 Boot Loader](#Boot_Loader)
    *   [1.8 Drivers propietarios de Nvidia](#Drivers_propietarios_de_Nvidia)
*   [2 Usando AUR](#Usando_AUR)
*   [3 Tradicional](#Tradicional)
*   [4 Revisa también](#Revisa_tambi.C3.A9n)

## Usando [Arch Build System](/index.php/Arch_Build_System "Arch Build System")

Siempre, se han propuesto varios métodos para construir fácilmente un kernel personalizado partiendo del de Arch. En la wiki se pueden encontrar varios ejemplos. Todos ellos son bastante buenos, pero sufren [algunos inconvenientes](https://bugs.archlinux.org/task/12384) que hacen que no estén oficialmente respaldados por los desarrolladores.

Contrariamente, el método descrito en este articulo es mas sólido y seguro, y se construye usando el paquete oficial del [linux](https://www.archlinux.org/packages/?name=linux).

### Instalando Arch Build System

[Instala](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") los paquetes [abs](https://www.archlinux.org/packages/?name=abs) y [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

Para obtener todo el árbol de ABS, ejecuta:

```
# abs

```

Revisa [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") para mas información.

### Consiguiendo los ingredientes

Antes que nada, necesitamos un kernel limpio para empezar a personalizarlo. En este articulo asumiré que usaras el [linux](https://www.archlinux.org/packages/?name=linux) oficial de Arch. Entonces creamos una carpeta para trabajar, y obtenemos los archivos del kernel desde ABS (luego de la sincronización):

```
cp /var/abs/core/linux/* <directorio_de_trabajo>/

```

Luego, pongan aquí cualquier paquete que se necesite (ej. archivos de configuración personalizada, parches, etc.)

### Modificando el PKGBUILD

Modifica el [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") del paquete oficial del [linux](https://www.archlinux.org/packages/?name=linux).

#### Cambiando pkgname

Las primeras lineas se pareceran a estas:

 `PKGBUILD` 
```
# $Id: PKGBUILD 130991 2011-07-09 12:23:51Z thomas $
# Maintainer: Tobias Powalowski <tpowa@archlinux.org>
# Maintainer: Thomas Baechler <thomas@archlinux.org>

pkgbase=linux
pkgname=('linux' 'linux-headers' 'linux-docs') # Build stock -ARCH kernel
# pkgname=linux-custom       # Build kernel with a different name
_kernelname=${pkgname#linux}
...

```

Como ves, hay un comentario para construir un kernel con diferente nombre (# Build kernel with a different name), todo lo que debemos hacer es descomentar esa linea, cambie el sufijo '-custom' por el nombre que quieras, y comentar la linea anterior ( osea el primer pkgname):

 `PKGBUILD build()` 
```
...
#pkgname=('linux' 'linux-headers' 'linux-docs') # Build stock -ARCH kernel
pkgname=linux-test       # Build kernel with a different name
...

```

**Note:** Esto asume que no vas a recompilar los [linux-headers](https://www.archlinux.org/packages/?name=linux-headers), -manpages or -docs. Si los queres recompilar, agregalos.

Ahora, todas las variables de tu paquete serán cambiadas de acuerdo al nuevo nombre. Por ejemplo, luego de instalar el paquete, los módulos seran alojados en `/lib/modules/<kernel_release>-test/`.

#### Modificando build()

Probablemente necesites un archivo ".config" personalizado para tu kernel. Podes descomentar una de las posibilidades mostradas en la función `build()` del [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"), por ejemplo:

 `PKGBUILD` 
```
...
# load configuration
# Configure the kernel. Replace the line below with one of your choice.
#make menuconfig # CLI menu for configuration
make nconfig # new CLI menu for configuration
#make xconfig # X-based configuration
#make oldconfig # using old config from previous kernel version
# ... or manually edit .config
...

```

Si ya tenias un archivo de configuración para el kernel. Te sugiero descomentar una de las herramientas de configuración interactiva, como nconfig, y cargar tu configuración desde allí. Eso evitará problemas con el nombre del kernel.

**Note:** Si descomentas *return 1*, podes cambiar el directoria principal del kernel luego de que makepkg termine las extracciones y luego hacer la configuración con nconfig. Esto te permitirá configurar tu kernel en varias sesiones. Cuando estés listo para compilar, copia el archivo .config sobre el .config que se haya generado automáticamente, o sobre el config.x86_64 (esto dependerá de la arquitectura del procesador), comenta *return 1* y usa **makepkg -i**.

#### Cambiando la función package_kernel26()

Debemos escribir una función personalizada para decirle al sistema como instalar el paquete. Esto es muy simple de hacer, solo debemos cambiarle el nombre a la función package_kernel26() por el de package_kernel26-test(),(test, recordemos es el nombre del kernel personalizado) y adaptar las instrucciones a tus necesidades. Si no quieres cambiar nada, la función debería quedar así:

 `PKGBUILD package_kernel26-test()` 
```
...
package_linux-test() {
 pkgdesc="The Linux Kernel and modules"
...
}

```

### Compilando con varios núcleos

Para decirle al compilador que use todos los núcleos al momento de compilar, usamos el flag -j<numero_de_nucleos>. El numero debe ser de n+1, donde n es la cantidad de núcleos de tu procesador.

Por ejemplo un procesador de 2 núcleos (2+1=3):

 `/etc/makepkg.conf` 
```
...
#-- Make Flags: change this for DistCC/SMP systems
MAKEFLAGS="-j3"
...

```

### Compilación

Ahora podemos compilar el kernel, con los comandos usuales: `makepkg` Si usaste un programa interactivo para configurar los parámetros del kernel (como menuconfig), deberás estar allí durante la compilación.

**Note:** El kernel necesita un tiempo para compilar, una hora no es inusual.

### Instalación

Luego de `makepkg`, podes revisar el archivo `linux.install`. Veras que algunas variables han cambiado. Ahora, solo debemos instalar con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"):

```
#pacman -U <paquete_del_kernel>

```

### Boot Loader

Las carpetas y archivos de nuestro kernel personalizado han sido creadas, ej. `/boot/kernel26-test-img`. Para testear el kernel, debemos actualizar el bootloader (`/boot/grub/menu.lst` para [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)")) y agregar las nuevas entradas ('default' y 'fallback') para nuestro kernel. De esta manera, podes tener ambos kernels el ya instalado y el de personalizado en paralelo.

### Drivers propietarios de Nvidia

Revisar [Instalacion alternativa: kernel personalizado](/index.php/NVIDIA "NVIDIA").

## Usando AUR

En el [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") hay algunos paquetes de los kernels mas conocidos. Podes instalarlos como están, o usarlos como base para tu kernel personalizado.

[Kernels en el AUR](/index.php/Kernels "Kernels")

## Tradicional

[La manera tradicional](/index.php/Kernel_Compilation_(Espa%C3%B1ol) "Kernel Compilation (Español)") es simple y directa.

Este método requiere de la descarga manual del tarbal, y la contrucción en tu directorio home como usuario normal. Una vez configurado, se explican dos métodos de compilación/instalación, el método manual y el de makepkg/[pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

Si sos nuevo en este proceso, [la manera tradicional para nuevos usuarios](/index.php/Kernel_Compilation_From_Source_For_New_Users_Guide "Kernel Compilation From Source For New Users Guide") es la apropiada.

## Revisa también

*   [Kernels](/index.php/Kernels "Kernels")
*   [O'Reilly - El kernel de linux en una cascara de nuez](http://www.kroah.com/lkn/) (ebook gratuito)