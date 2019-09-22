Artículos relacionados

*   [Kernel modules (Español)](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)")
*   [Kernel parameters (Español)](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)")

Arch Linux provee varios métodos para compilar el kernel. Usar [Arch Build System](#Usando_Arch_Build_System) es el recomendado.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Oficialmente compatibles](#Oficialmente_compatibles)
*   [2 Usando Arch Build System](#Usando_Arch_Build_System)
    *   [2.1 Consiguiendo los ingredientes](#Consiguiendo_los_ingredientes)
    *   [2.2 Modificando el PKGBUILD](#Modificando_el_PKGBUILD)
        *   [2.2.1 Cambiando pkgname](#Cambiando_pkgname)
        *   [2.2.2 Modificando build()](#Modificando_build())
        *   [2.2.3 Cambiando la función package_kernel26()](#Cambiando_la_función_package_kernel26())
    *   [2.3 Compilación](#Compilación)
    *   [2.4 Instalación](#Instalación)
    *   [2.5 Boot Loader](#Boot_Loader)
    *   [2.6 Drivers propietarios de Nvidia](#Drivers_propietarios_de_Nvidia)
*   [3 Usando AUR](#Usando_AUR)
*   [4 Tradicional](#Tradicional)
*   [5 Revisa también](#Revisa_también)

## Oficialmente compatibles

*   **[Estable](https://www.kernel.org/category/releases.html)** — La versión *vanilla* del kernel y los módulos, con pocas modificaciones aplicadas.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **[Hardened](https://kernsec.org/wiki/index.php/Kernel_Self_Protection_Project)** — Un kernel de Linux enfocado en seguridad, aplica parches para mitigar la explotación en el kernel o en el espacio del usuario. También activa mas características de seguridad en comparación con [linux](https://www.archlinux.org/packages/?name=linux), entre otros: *namespaces*, *audit* y [SELinux](/index.php/SELinux "SELinux").

	[https://github.com/copperhead/linux-hardened](https://github.com/copperhead/linux-hardened) || [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

*   **[Larga duración](https://www.kernel.org/category/releases.html)** — Kernel de Linux y módulos con soporte de larga duración (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

*   **[Kernel ZEN](https://liquorix.net/)** — Es el resultado de un esfuerzo colaborativo de varios hackers para hacer el mejor kernel para el uso en sistemas de uso diario.

	[https://github.com/zen-kernel/zen-kernel](https://github.com/zen-kernel/zen-kernel) || [linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

## Usando Arch Build System

Siempre, se han propuesto varios métodos para construir fácilmente un kernel personalizado partiendo del de Arch. En la wiki se pueden encontrar varios ejemplos. Todos ellos son bastante buenos, pero sufren [algunos inconvenientes](https://bugs.archlinux.org/task/12384) que hacen que no estén oficialmente respaldados por los desarrolladores.

Contrariamente, el método descrito en este articulo es mas sólido y seguro, y se construye usando el paquete oficial del [linux](https://www.archlinux.org/packages/?name=linux).

### Consiguiendo los ingredientes

Se va a usar [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)"), siga las recomendaciones allí descritas en primer lugar. Por ejemplo, no se puede ejecutar *makepkg* como root/sudo. Cree un directorio `build` el directorio raiz de su usuario.

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete [asp](https://www.archlinux.org/packages/?name=asp) y el grupo de paquetes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

Se necesita un kernel limpio para poder hacer la personalización. Descargue los archivos del kernel desde ABS en su directorio *build*, ejecute:

```
$ asp checkout linux

```

Después obtenga cualquier otro archivo que considere necesario (v.g. archivos personalizados, parches, configuraciones, etc.) desde sus respectivas fuentes.

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

**Note:** Si descomenta *return 1*, puede cambiar el directorio principal del kernel luego de que makepkg termine las extracciones y luego hacer la configuración con nconfig. Esto te permitirá configurar tu kernel en varias sesiones. Cuando estés listo para compilar, copia el archivo .config sobre el .config que se haya generado automáticamente, o sobre el config.x86_64 (esto dependerá de la arquitectura del procesador), comenta *return 1* y usa **makepkg -i**.

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

### Compilación

Ahora se puede compilar el kernel, con el comando usual `makepkg`

Si usaste un programa interactivo para configurar los parámetros del kernel (como menuconfig), deberás estar allí durante la compilación.

```
 $ makepkg -s

```

El parámetro `-s` descargara cualquier dependencia adicional que no se encuentre en su sistema.

**Nota:**

*   La fuente del kernel contiene [firmas PGP](https://www.kernel.org/signature.html#kernel-org-web-of-trust), y makepkg intentara verificarlas. Vea [verificación de firmas](/index.php/Makepkg_(Espa%C3%B1ol)#Verificación_de_firmas "Makepkg (Español)") para mas información.
*   El kernel necesita un tiempo para compilar, una hora no es inusual.
*   [Compilar simultáneamente](/index.php/Makepkg_(Espa%C3%B1ol)#Recomendaciones "Makepkg (Español)") puede reducir los tiempos de compilación significativamente en sistemas con múltiples núcleos.

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

Este método requiere la descargar manual del tarball y construir el kernel en el directorio home como usuario normal. Una vez configurado, se explican dos métodos de compilación/instalación, el método manual o mediante [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)")/[pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

Más información en [Compilación tradicional](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation").

## Revisa también

*   [Kernels](/index.php/Kernels "Kernels")
*   [O'Reilly - El kernel de linux en una cascara de nuez](http://www.kroah.com/lkn/) (ebook gratuito)