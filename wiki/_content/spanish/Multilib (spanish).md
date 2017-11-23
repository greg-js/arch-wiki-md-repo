Related articles

*   [Install bundled 32-bit system in Arch64](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64")

Habilitando el repositorio multilib permite al usuario ejecutar y utilizar aplicaciones de 32-bits en las compilaciones de 64-btis en las instalaciones de Arch Linux.

## Contents

*   [1 Estructura de Directorios](#Estructura_de_Directorios)
*   [2 Activación](#Activaci.C3.B3n)
*   [3 Desactivación](#Desactivaci.C3.B3n)
*   [4 Ver también](#Ver_tambi.C3.A9n)

## Estructura de Directorios

La instalación de Arch Linux de 64-btis con *multilib* activada sigue una estructura de directorios similar a Debian. Las librerias compatibles de 32-bits se encuentran en `/usr/lib32/` y las librerías nativas en `/usr/lib/`.

## Activación

Para utilizar el [multilib](/index.php/Official_repositories_(Espa%C3%B1ol)#.5Bmultilib.5D "Official repositories (Español)"), eliminamos el *#* del archivo `/etc/pacman.conf` (Por favor asegúrate de eliminar el # de ambas líneas):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Luego actualizamos nuestro listado de paquetes con `pacman -Syu`.

**Nota:** No ejecutemos `pacman -Sy`, ver [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance").

## Desactivación

Para revertir ésto y dejar nuestro sistema sólo con paquetes de 64-bits, desintalamos *multilib*:

Ejecutamos el siguiente comando para eliminar todos los paquetes que se instalaron desde *multilib*:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

Si tenemos conflictos con gcc-libs, instalamos nuevamente la version de 64-bits y repetimos el comando anterior:

```
# pacman -S gcc-libs base-devel

```

Comentamos nuevamente `[multilib]` del archivo `/etc/pacman.conf` quedando así:

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

Luego actualizamos el listado de paquetes con `pacman -Syu`.

## Ver también

*   [Makepkg#Build 32-bit packages on a 64-bit system](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg")
*   [64-bit FAQ](/index.php/64-bit_FAQ "64-bit FAQ")
*   [arch-multilib](//mailman.archlinux.org/mailman/listinfo/arch-multilib) mailing list