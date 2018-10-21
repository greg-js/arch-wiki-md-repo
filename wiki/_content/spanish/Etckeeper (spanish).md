**Estado de la traducción**
Este artículo es una traducción de [Etckeeper](/index.php/Etckeeper "Etckeeper"), revisada por última vez el **2018-10-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Etckeeper&diff=0&oldid=548963) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Git](/index.php/Git_(Espa%C3%B1ol) "Git (Español)")
*   [Cron](/index.php/Cron "Cron")

[Etckeeper](http://etckeeper.branchable.com/) le permite mantener `/etc` bajo el control de versiones.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Utilización](#Utilizaci.C3.B3n)
    *   [3.1 systemd](#systemd)
    *   [3.2 Cron](#Cron)
    *   [3.3 Incron](#Incron)
    *   [3.4 Escritura automática en un repositorio remoto](#Escritura_autom.C3.A1tica_en_un_repositorio_remoto)
        *   [3.4.1 Utilizando el hook proporcionado por etckeeper](#Utilizando_el_hook_proporcionado_por_etckeeper)
        *   [3.4.2 A través de un hook personalizado](#A_trav.C3.A9s_de_un_hook_personalizado)
    *   [3.5 Script contenedor](#Script_contenedor)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [etckeeper](https://www.archlinux.org/packages/?name=etckeeper).

## Configuración

El sistema de control de versiones preferido (el predeterminado es [git](/index.php/Git_(Espa%C3%B1ol) "Git (Español)")) y otras opciones se configura en `/etc/etckeeper/etckeeper.conf`.

Etckeeper admite el uso de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") como `LOWLEVEL_PACKAGE_MANAGER` y `HIGHLEVEL_PACKAGE_MANAGER` en `etckeeper.conf`.

## Utilización

Después de la configuración, el repositorio de la ruta `/etc` debe inicializarse:

```
# etckeeper init

```

A partir de la versión 1.18.3-1 de *etckeeper*, los [hooks de pacman](/index.php/Pacman_(Espa%C3%B1ol)#Hooks "Pacman (Español)") de antes y después de la instalación se ejecutan automáticamente en la instalación, actualización y eliminación de paquetes. Ya no es necesario un [#Script contenedor](#Script_contenedor) manual.

Para rastrear otros cambios en la ruta `/etc`, debe confirmar los cambios manualmente (véase la página de manual [etckeeper(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/etckeeper.8) para las órdenes) o utilice una de las soluciones de interrupción siguientes.

### systemd

Las unidades de servicio y temporizador están incluidas en el paquete. Simplemente [habilite](/index.php/Systemd/Timers#Management "Systemd/Timers") `etckeeper.timer`.

Véase [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") para obtener más información y [Modificar los archivos de unidad suministrados](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)") si desea editar las unidades proporcionadas.

### Cron

Hay un `[script de cron](https://git.joeyh.name/index.cgi/etckeeper.git/tree/debian/cron.daily)` en la distribución de origen. Puede utilizar este script para confirmar automáticamente los cambios en una programación.

Por ejemplo, para hacerlo funcionar diariamente:

1.  Tenga [cron](/index.php/Cron "Cron") instalado y habilitado.
2.  Coloque el script como `/etc/cron.daily/*nombre_del_script*`
3.  Permita la ejecución del archivo para el superusuario *root* (`# chmod u+x /etc/cron.daily/'nombre_del_script `*).*

Véase [cron#Cronie](/index.php/Cron#Cronie "Cron"), [cron](/index.php/Cron "Cron") para más información.

### Incron

Para crear confirmaciones automáticamente en **cada** modificación de los archivos dentro de `/etc/`, utilice [incron](https://www.archlinux.org/packages/?name=incron). Este utiliza la señalización nativa del sistema de archivos a través de [inotify(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotify.7).

Véase: [[1]](http://inotify.aiken.cz/?section=incron&page=doc&lang=en), [[2]](https://linux.die.net/man/8/incrond)

### Escritura automática en un repositorio remoto

Si bien tener una copia de seguridad local en `/etc/.git` es un buen primer paso, etckeeper puede enviar automáticamente los cambios en cada confirmación a un repositorio remoto como Github.

Primero, edite `etc/.git` y añada su repositorio remoto de Github:

```
# git remote add origin *https://github.com/user/repo.git*

```

A continuación, se debe usar o configurar un *hook* para escribir.

#### Utilizando el hook proporcionado por etckeeper

Edite la opción `PUSH_REMOTE` en `/etc/etckeeper/etckeeper.conf`, con el nombre del repositorio remoto en el que desea que etckeeper escriba. Por ejemplo:

```
PUSH_REMOTE="*origin*"

```

Se pueden añadir múltiples repositorios remotos separados con espacios.

#### A través de un hook personalizado

Cree un archivo ejecutable `/etc/etckeeper/commit.d/40github-push`:

```
#!/bin/sh
set -e

if [ "$VCS" = git ] && [ -d .git ]; then
  cd /etc/
  git push origin master
fi

```

Ahora, cada vez que ejecute su script contenedor o el alias de antes, los cambios se asignarán automáticamente a su repositorio de Github.

### Script contenedor

Si desea realizar el seguimiento de los cambios de una orden ejecutada frecuentemente (por ejemplo, `*orden*`), un simple script contenedor puede ayudar a automatizarlo. Por ejemplo, cree:

 `/usr/local/bin/checketc.sh` 
```
#!/bin/bash

etckeeper pre-install
*orden*
etckeeper post-install
```

y hágalo ejecutable. Alternativamente, puede llamar las órdenes de Etckeeper a través de un alias o función bash, véase [Alias en Bash](/index.php/Bash_(Espa%C3%B1ol)#Alias "Bash (Español)") para obtener más información.

**Nota:** Antes de la versión 1.18.3-1 de Etckeeper, dicho script contenedor manual era necesario para la integración con Pacman. Ahora los hooks de Pacman ejecutan las órdenes automáticamente.