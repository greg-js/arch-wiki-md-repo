**Fbsplash** (anteriormente gensplash) es una implementación en espacio de usuario de una pantalla _splash_ para sistemas Linux. Provee un ambiente gráfico durante el arranque del sistema usando la capa framebuffer de Linux.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Fbsplash](#Fbsplash)
    *   [1.2 _Scripts_](#Scripts)
    *   [1.3 Temas](#Temas)
    *   [1.4 Suspender al Disco](#Suspender_al_Disco)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Línea de comandos del Kernel](#L.C3.ADnea_de_comandos_del_Kernel)
    *   [2.2 Archivos de configuración](#Archivos_de_configuraci.C3.B3n)
*   [3 Ejecutando Fbsplash temprano en el initcpio](#Ejecutando_Fbsplash_temprano_en_el_initcpio)
*   [4 Fondos de Consola](#Fondos_de_Consola)

# Instalación

## Fbsplash

Instale fbsplash con yaourt o aurbuild, o descargue el [fbsplash paquete](https://aur.archlinux.org/packages.php?ID=13541) del [AUR](/index.php/AUR "AUR") y compilelo e instalelo con makepkg.

## _Scripts_

El paquete fbsplash provee los _scripts_ para un funcionamiento básico. Si desea mayor funcionalidad, como progreso fluido, mensajes del progreso de revisión de sistemas de archivos, soporte para servicios de arranque/íconos de 'demonios' y _scripts_ gancho de tema, puede instalar el paquete [fbsplash-extras](https://aur.archlinux.org/packages/fbsplash-extras/).

## Temas

Instale uno o más temas Fbsplash. Se pueden encontrar algunos en [buscando en el AUR 'fbsplash-theme'](https://aur.archlinux.org/packages.php?O=0&K=fbsplash-theme&do_Search=Go), desde [GNOME-Look.org](http://gnome-look.org) o en [KDE-Look.org](http://kde-look.org).

**Nota:** El paquete fbsplash no contiene un tema por defecto.

## Suspender al Disco

Si desea suspender al disco con Fbsplash, instale el paquete [uswsusp-fbsplash](https://aur.archlinux.org/packages/uswsusp-fbsplash/) desde el AUR. Para mayor información vea [Pm-utils](/index.php?title=Pm-utils_(Espa%C3%B1ol)&action=edit&redlink=1 "Pm-utils (Español) (page does not exist)") o [Suspender al disco](/index.php?title=Suspend_to_Disk_(Espa%C3%B1ol)&action=edit&redlink=1 "Suspend to Disk (Español) (page does not exist)"). Adicionalmente hay soporte limitado para usar un tema Fbsplash en el paquete [tuxonice-userui](https://aur.archlinux.org/packages/tuxonice-userui/) para aquellos usando un kernel con el parche TuxOnIce.

# Configuración

## Línea de comandos del Kernel

Agregue algo como esto a su línea kernel en /boot/grub/menu.lst or /etc/lilo.conf:

```
logo.nologo quiet nomodeset vga=792 console=tty1 splash=silent,fadein,fadeout,theme:arch-banner-icons

```

para habilitar el splash usando un _framebuffer_ en modo VESA de 1024x768\. Para otras resoluciones de pantalla vea [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)").

Si está usando KMS, agregue algo así:

```
logo.nologo quiet video=1280x800 console=tty1 splash=silent,fadein,fadeout,theme:arch-banner-icons

```

**Nota:** El parámetro **logo.nologo** no es necesario si está usando kernel26-fbcondecor, porque no se incluye un logo en este kernel. El parámetro **video** eso necesario solamente para evitar una resolución errónea si está conectada otra pantalla o un equipo de televisión.

## Archivos de configuración

Coloque uno o más de los temas que instaló en **/etc/conf.d/splash**. Puede también especificar resoluciones de pantalla para preservar algún espacio initcpio:

```
SPLASH_THEMES=(
   arch-black
   arch-banner-icons/1280x1024.cfg
   arch-banner-noicons/1280x1024.cfg
)

```

**Nota:** El tema arch-banner-icons contiene principalmente enlaces simbólicos a arch-banner-noicons. Así que si uno de ellos está incluido en total, no se preservará mucho espacio al limitar al otro a algunas resoluciones de pantalla.

# Ejecutando Fbsplash temprano en el initcpio

Agregue _fbsplash_ a la línea `HOOKS=` en /etc/mkinitcpio.conf :

```
HOOKS="base udev fbsplash ..."

```

Or if using [uswsusp-fbsplash](https://aur.archlinux.org/packages/uswsusp-fbsplash/): O si está usando [uswsusp-fbsplash](https://aur.archlinux.org/packages/uswsusp-fbsplash/):

```
HOOKS="base udev ... uresume fbsplash ..." 

```

Recompile su initcpio con mkinitcpio. Vea el artículo [Mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)").

**Nota:** El gancho **udev** es necesario para detectar cualquier parche Fbcondecor del kernel para evitar ejecutar el asistente Fbcondecor dos veces (re-dibujado de la pantalla _splash_ visible) y también es útil para cargar los modulos del kernel necesarios (KMS, radeonfb, ...). El gancho **uresume** provisto por uswsusp-fbsplash siempre esperará a que termine el asistente Fbcondecor (termine la transición) para evitar interferencia. Es recomendado poner 'fbsplash' detraás de 'uswsusp' o incluso quitar **fadein** si se usa un kernel Fbcondecor para obtener un _resume_ rápido.

# Fondos de Consola

Si tiene un kernel que soporta Fbcondecor, puede configurar una agradable fondo de consola gráfica además de la pantalla _splash_. Busque en el AUR por [fbcondecor](https://aur.archlinux.org/packages.php?O=0&K=fbcondecor&do_Search=Go)

Después de instalar su kernel parchado y fbsplash, agregue _fbcondecor_ a su arreglo DAEMONS en rc.conf:

```
DAEMONS=(... fbcondecor ...)

```

Ahí hay también un archivo de configuración /etc/conf.d/fbcondecor para configurar los terminales virtuales a ser usados.

Puede incluso arrancar el sistema con un agradable fondo de consola y los mensajes de arranque normales de Arch Linux en vez de una pantalla _splash_. Sólo cambie su línea del kernel en /boot/grub/menu.lst para que use el modo _verbose_:

```
quiet console=tty1 splash=verbose,theme:arch-banner-icons

```