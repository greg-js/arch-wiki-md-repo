**Estado de la traducción**
Este artículo es una traducción de [Snap](/index.php/Snap "Snap"), revisada por última vez el **2019-02-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Snap&diff=0&oldid=568314) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Flatpak](/index.php/Flatpak "Flatpak")
*   [AppArmor](/index.php/AppArmor "AppArmor")

[Snap](https://snapcraft.io/) es un sistema de despliegue y manejo de paquetes. Los paquetes son llamados 'snaps' y la herramienta para usarlos es 'snapd', la cual funciona en una amplia gama de distribuciones Linux y permite, por lo tanto, el despliege ascendente de software agnóstico a la distribución. Snap fue originalmente diseñado y desarrollado por Canonical.

[snapd](https://github.com/snapcore/snapd) es un demonio REST API para la administración de paquetes snaps. Los usuarios pueden interactuar con él al usar el cliente *snap*, el cual es parte del mismo paquete.

Los snaps pueden ser confinados usando [AppArmor](/index.php/AppArmor "AppArmor") el cual ahora es habilitado por el kernel predeterminado. Consulte las páginas wiki relevantes para encontrar instrucciones para habilitar [AppArmor](/index.php/AppArmor "AppArmor") en su sistema.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Utilización](#Utilización)
    *   [3.1 Buscando](#Buscando)
    *   [3.2 Instalando](#Instalando)
    *   [3.3 Actualización](#Actualización)
    *   [3.4 Eliminando](#Eliminando)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Snaps Clásicas](#Snaps_Clásicas)
    *   [4.2 Confinamiento](#Confinamiento)
*   [5 Administración Gráfica](#Administración_Gráfica)
*   [6 Soporte](#Soporte)
*   [7 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [snapd](https://aur.archlinux.org/packages/snapd/) o [snapd-git](https://aur.archlinux.org/packages/snapd-git/).

**Sugerencia:** `snapd` instala un script en `/etc/profile.d/snapd.sh` para exportar las rutas de los binarios instalados con el paquete snapd y los accesos directos. Reinicie una vez para que el cambio surta efecto.

Desde la versión 2.36, `snapd` habilita el soporte AppArmor para Arch Linux. Para usarlo, tiene que habilitar AppArmor en su sistema, vea [AppArmor#Instalación](/index.php?title=AppArmor_(Espa%C3%B1ol)&action=edit&redlink=1 "AppArmor (Español) (page does not exist)").

**Nota:** Si AppArmor no está habilitado en su sistema todas las snaps se ejecutarán en modo `devel` lo que significa que tendrán el mismo, acceso sin restricciones a su sistema como las aplicaciones instaladas desde los repositorios Arch Linux.

Si está usando [AppArmor](/index.php/AppArmor "AppArmor"):

```
 $ systemctl enable --now apparmor.service
 $ systemctl enable --now snapd.apparmor.service

```

## Configuración

Para lanzar el demonio `snapd` cuando *snap* intente usarlo, [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") y/o [habilite](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `snapd.socket`

## Utilización

La herramienta *snap* es utilizada para administrar las snaps.

### Buscando

Para encontrar snaps para instalar, puede consultar Ubuntu Store con:

```
$ snap find *searchterm*

```

### Instalando

Una vez haya encontrado la snap que busca puede instalarla con:

```
# snap install *snapname*

```

Esto requiere privilegios de root. La instalación de snaps por usuario no es posible, aún. Descargará la snap en `/var/lib/snapd/snaps` y la montará en `/var/lib/snapd/snap/*snapname*` para que esté disponible en el sistema.

También creará unidades de montaje por cada snap y las agregará a `/etc/systemd/system/multi-user.target.wants/` como enlaces simbólicos para que todas las snaps estén disponibles cuando su sistema es iniciado.

Una vez hecho esto debería encontrarla en la lista de snaps instaladas junto con su número de versión, revisión y desarollador usando:

```
$ snap list

```

También puede cargar snaps desde su disco duro local con:

```
# snap install --dangerous */path/to/snap*

```

### Actualización

Para actualizar su snap manualmente use:

```
# snap refresh

```

Las snaps se actualizan automáticamente de acuerdo a la configuración snap `refresh.timer`.

Para ver el siguiente/último tiempo de actualización use:

```
# snap refresh --time

```

Para establecer un tiempo de actualización diferente, ej. dos veces al día:

```
# snap set core refresh.timer=0:00~24:00/2

```

Vea [página de documentación de opciones de sistema](https://forum.snapcraft.io/t/system-options/87) para detalles sobre como personalizar el tiempo de actualización.

### Eliminando

Los snaps pueden ser eliminados al ejecutar:

```
# snap remove *snapname*

```

## Consejos y trucos

### Snaps Clásicas

Algunas snaps (e.j. Skype y Pycharm) usan el confinamiento clásico. Sin embargo, el confinamiento clásico requiere el directorio `/snap`, que no es compatible con FHS. Por lo tanto, el paquete snapd no lleva éste directorio. Sin embargo, si el usuario lo desea, puede crear manualmente un enlace simbólico de `/snap` a `/var/lib/snapd/snap`, para permitir la instalación de snaps clásicas:

```
# ln -s /var/lib/snapd/snap /snap

```

### Confinamiento

Cuando se utiliza [AppArmor](/index.php/AppArmor "AppArmor"), snapd (2.36+) generará los mismos perfiles para las snaps como en Ubuntu. El analizador de [AppArmor](/index.php/AppArmor "AppArmor") es suficientemente inteligente para eliminar las reglas que aún no son compatibles por la línea principal del kernel.

Para verificar si el confinamiento básico está funcionando, instale la snap *hello-world*. Luego ejecute lo siguiente:

```
 $ hello-world.evil
 Hello Evil World!
 This example demonstrates the app confinement
 You should see a permission denied error next
 /snap/hello-world/27/bin/evil: 9: /snap/hello-world/27/bin/evil: cannot create /var/tmp/myevil.txt: Permission denied

```

La denegación fue causada por AppArmor y debería haber sido registrada.

```
 $ dmesg
 ...
 [  +0.000003] audit: type=1327 audit(1540469583.966:257): proctitle=2F62696E2F7368002F736E61702F68656C6C6F2D776F726C642F32372F62696E2F6576696C
 [ +12.268939] audit: type=1400 audit(1540469596.236:258): apparmor="DENIED" operation="open" profile="snap.hello-world.evil" name="/var/tmp/myevil.txt" pid=10835 comm="evil" requested_mask="wc" denied_mask="wc" fsuid=1000 ouid=1000
 [  +0.000006] audit: type=1300 audit(1540469596.236:258): arch=c000003e syscall=2 success=no exit=-13 a0=55d991ba6bc8 a1=241 a2=1b6 a3=55d991ba6be0 items=0 ppid=31349 pid=10835 auid=1000 uid=1000 gid=1000 euid=1000 suid=1000 fsuid=1000 egid=1000 sgid=1000 fsgid=1000 tty=pts2 ses=3 comm="evil" exe="/bin/dash" subj==snap.hello-world.evil (enforce)
 ...

```

Si no ve ningúna denegación, verifique que los perfiles se hayan cargado.

```
  $ sudo aa-status |grep snap.hello-world
    snap.hello-world.env
    snap.hello-world.evil
    snap.hello-world.hello-world
    snap.hello-world.sh

```

Además, puede verificar que las características sandbox están disponibles en el sistema de acuerdo a snapd:

```
 $ snap debug sandbox-features
 apparmor:             kernel:caps kernel:domain kernel:file kernel:mount kernel:namespaces kernel:network_v8 kernel:policy kernel:ptrace kernel:query kernel:rlimit kernel:signal parser:unsafe policy:default support-level:partial
 confinement-options:  devmode
 dbus:                 mediated-bus-access
 kmod:                 mediated-modprobe
 mount:                freezer-cgroup-v1 layouts mount-namespace per-snap-persistency per-snap-profiles per-snap-updates per-snap-user-profiles stale-base-invalidation
 seccomp:              bpf-argument-filtering kernel:allow kernel:errno kernel:kill_process kernel:kill_thread kernel:log kernel:trace kernel:trap

```

## Administración Gráfica

Tanto Gnome Software Center como KDE Discover pueden proporcionar soporte nativo de snap con los paquetes [gnome-software-snap](https://aur.archlinux.org/packages/gnome-software-snap/) o [discover-snap](https://aur.archlinux.org/packages/discover-snap/).

## Soporte

Arch Linux related mailing lists and other official Arch Linux support channels aren't an appropriate place to request help with snaps on Arch Linux. An appropriate place to ask for support is the [Snapcraft forum](https://forum.snapcraft.io).

Las listas de correo relacionadas con Arch Linux y otros canales oficiales de soporte de Arch Linux no son lugar apropiado para solicitar ayuda sobre snaps en Arch Linux. Un lugar apropiado para solicitar ayuda de soporte es el [foro Snapcraft](https://forum.snapcraft.io).

## Véase también

*   [Sitio oficial](https://snapcraft.io/)
*   [Repositorio GitHub](https://github.com/snapcore/snapd)
*   [Artículo de arstechnica](http://arstechnica.com/information-technology/2016/06/goodbye-apt-and-yum-ubuntus-snap-apps-are-coming-to-distros-everywhere/) (06/16) acerca de snaps de Ubuntu que estarán disponibles para Arch y otras distribuciones