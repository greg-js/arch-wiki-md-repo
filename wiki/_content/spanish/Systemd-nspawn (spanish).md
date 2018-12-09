Artículos relacionados

*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [systemd-networkd (Español)](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)")
*   [Docker](/index.php/Docker "Docker")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")

*systemd-nspawn* es parecido al comando [chroot](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)"), pero es un *chroot en esteroides*.

*systemd-nspawn* puede ser usado para ejecutar un comando o un sistema operativo en contenedor de *namespace* muy ligero. Es mas poderoso que [chroot](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") ya que virtualiza toda estructura del sistema de archivos, así como el árbol de procesos, los sub sistemas IPC y los nombres de dominio y del servidor.

*systemd-nspawn* limita el acceso a varias interfaces del kernel como `/sys`, `/proc/sys` o `/sys/fs/selinux` en modo de lectura unicamente. Interfaces de red y el tiempo del sistema no se pueden modificar desde el contenedor. Nodos de dispositivos no se pueden crear. El sistema anfitrión no se puede reiniciar y módulos del kernel no se pueden montar desde el contenedor.

Este mecanismo difiere de [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd") o [Libvirt](/index.php/Libvirt "Libvirt")-lxc, ya que es una herramienta mucho mas fácil de configurar.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Ejemplos](#Ejemplos)
    *   [2.1 Crear e iniciar Arch Linux en un contenedor](#Crear_e_iniciar_Arch_Linux_en_un_contenedor)
        *   [2.1.1 Crear un Arch Linux i686 dentro de un anfitrión x86_64](#Crear_un_Arch_Linux_i686_dentro_de_un_anfitrión_x86_64)
    *   [2.2 Crear un ambiente Debian o Ubuntu](#Crear_un_ambiente_Debian_o_Ubuntu)
    *   [2.3 Activar inicio automático de los contenedores](#Activar_inicio_automático_de_los_contenedores)
*   [3 Manejo de contenedores](#Manejo_de_contenedores)
    *   [3.1 machinectl](#machinectl)
    *   [3.2 Utilidades de systemd](#Utilidades_de_systemd)

## Instalación

*systemd-nspawn* es parte y viene empaquetado con [systemd](https://www.archlinux.org/packages/?name=systemd).

## Ejemplos

### Crear e iniciar Arch Linux en un contenedor

En primer lugar [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Cree un directorio para mantener el contenedor. En este ejemplo se usará `~/MyContainer`.

Use *pacstrap* para instalar un sistema básico de arch dentro del contenedor. Como mínimo es necesario instalar el grupo de paquetes [base](https://www.archlinux.org/groups/x86_64/base/).

```
# pacstrap -i -c -d ~/MyContainer base [pkgs/grupos adicionales]

```

**Sugerencia:** El parametro `-i` **omitira** auto confirmación en la selección de paquetes. Ya que no es necesario instalar el kernel en el contenedor, lo puede remover de la lista de selección para ahorrar espacio. Vea [pacman#Utilización](/index.php/Pacman_(Espa%C3%B1ol)#Utilización "Pacman (Español)").

**Nota:** El paquete [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) requerido por [linux](https://www.archlinux.org/packages/?name=linux), que esta incluido en el grupo de paquetes [base](https://www.archlinux.org/groups/x86_64/base/) no es necesario para ejecutar el contenedor. Este causa algunos problemas con `systemd-tmpfiles-setup.service` durante el arranque del contenedor con `systemd-nspawn`. Es posible instalar el grupo [base](https://www.archlinux.org/groups/x86_64/base/) excluyendo el paquete [linux](https://www.archlinux.org/packages/?name=linux) y sus dependecias al construir el contenedor con `# pacstrap -i -c -d ~/MyContainer base --ignore linux [additional pkgs/groups]`. El parámetro `--ignore` es pasado a [pacman](https://www.archlinux.org/packages/?name=pacman). Vea [FS#46591](https://bugs.archlinux.org/task/46591) para más información.

Cuando la instalación ha finalizado, arranque el contenedor ejecutando:

```
# systemd-nspawn -b -D ~/MyContainer

```

El parámetro `-b` arranca el contenedor (v.g. ejecuta `systemd` como PID=1), en lugar de simplemente iniciar una shell, y el parámetro `-D` especifica el directorio que se usara como directorio raíz del contenedor.

Después que el contenedor arranque, inicie sesión con el usuario "root" sin contraseña.

El contenedor se puede apagar ejecutando `poweroff` desde dentro del contenedor. Desde el sistema anfitrión, los contenedores se pueden controlar con la herramienta [machinectl](#machinectl).

**Nota:** Para terminar la *sesión* estando dentro del contenedor, oprima `Ctrl` y rápidamente presione `]` tres veces. Teclados con disposición diferente a US, deben usar `%` en lugar de `]`.

#### Crear un Arch Linux i686 dentro de un anfitrión x86_64

Es posible instalar un sistema mínimo de Arch Linux i686 dentro de un directorio y usarlo como un contenedor de systemd-nspawn en lugar de usar [chroot](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)") o [virtualización](/index.php/Virtualization "Virtualization"). Esto es útil para examinar la compilación de `PKGBUILD` en un sistema de i686\. Este seguro de usar `pacman.conf` **sin** el repositorio `multilib`.

```
 # pacman_conf=/tmp/pacman.conf # este es pacman.conf sin multilib
 # mkdir /mnt/i686-archlinux
 # linux32 pacstrap -C "$pacman_conf" -di /mnt/i686-archlinux base base-devel

```

Se puede dejar el paquete `linux` fuera del grupo `base`, ya que el sistema creado no pretende ser encendido en hardware real o virtual.

Para arrancar el sistema i686 resultante como una instancia de systemd-nspawn, ejecute:

```
 # linux32 systemd-nspawn -D /mnt/i686-archlinux

```

### Crear un ambiente Debian o Ubuntu

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") [debootstrap](https://www.archlinux.org/packages/?name=debootstrap), [gnupg1](https://aur.archlinux.org/packages/gnupg1/), y uno de estos paquetes: [debian-archive-keyring](https://www.archlinux.org/packages/?name=debian-archive-keyring) o [ubuntu-keyring](https://www.archlinux.org/packages/?name=ubuntu-keyring) (obviamente instale el llavero del distro que quiere).

**Nota:** *systemd-nspawn* requiere que el sistema operativo dentro del contenedor ejecute systemd como PID 1 y que *systemd-nspawn* este instalado en el contenedor. Esto quiere decir que Ubuntu antes de la version 15.04 no funcionaran, y configuraciones extras para cambiar de upstart a systemd son necesarias. También asegurese que el paquete `systemd-container` esta instalado en el contenedor.

Desde este punto es relativamente trivial crear un ambiente con Debian o Ubuntu:

```
# cd /var/lib/machines
# debootstrap <nombrecodigo> myContainer <url-repositorio>

```

Para Debian nombres código validos son "stable" o "testing", también nombres de publicaciones "stretch" and "sid". Para Ubuntu el nombre código puede ser "xenial" o "zesty". Una lista completa de nombres codigo esta en `/usr/share/debootstrap/scripts`.

En caso de una imagen de Debian la "url-repositorio" puede ser `[http://deb.debian.org/debian/](http://deb.debian.org/debian/)`. Para Ubuntu la "url-repositorio" puede ser `[http://archive.ubuntu.com/ubuntu/](http://archive.ubuntu.com/ubuntu/)`.

A diferencia de Arch, Debian y Ubuntu no dejaran iniciar sesión sin una contraseña. Para establecer la contraseña de root inicie sesión con el parámetro `-b` y cambie la contraseña:

```
# systemd-nspawn -D myContainer
# passwd
# logout

```

Si los comandos de arriba no funcionaron, es posible arrancar el contenedor y ejecutar estos comandos:

```
# systemd-nspawn -b -D myContainer  # Arranca el contenedor
# machinectl shell root@myContainer /bin/bash  # Obtenga una shell con root
# passwd
# logout

```

### Activar inicio automático de los contenedores

Al usar un contenedor frecuentemente, seria deseable iniciarlo al arrancar el sistema anfitrión.

[Active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") el target `machines.target`, después ejecute `systemd-nspawn@*myContainer*.service`, donde `myContainer` es un contenedor de nspawn ubicado en `/var/lib/machines`.

**Sugerencia:** Para personalizar el arranque de los contenedores, edite `/etc/systemd/nspawn/*myContainer*.nspawn`. Vea [systemd.nspawn(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.nspawn.5) para todas las opciones.

## Manejo de contenedores

### machinectl

**Nota:** La herramienta *machinectl* requiere [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") y que el paquete [dbus](https://www.archlinux.org/packages/?name=dbus) este instalado en el contenedor. Vea [[1]](https://github.com/systemd/systemd/issues/685) para más detalles en la discusión.

El manejo de contenedores es efectuado principalmente con el comando `machinectl`. Vea [machinectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/machinectl.1) para más detalles.

Ejemplos:

Inicie una shell dentro de un contenedor que ya ha iniciado:

```
$ machinectl login *MyContainer*

```

Mostrar informacion detallada sobre un contenedor:

```
$ machinectl status *MyContainer*

```

Reinicie un contenedor:

```
$ machinectl reboot *MyContainer*

```

Apague un contenedor:

```
$ machinectl poweroff *MyContainer*

```

**Sugerencia:** Apagar y reiniciar se pueden ejecutar desde dentro de una sesión del contenedor, ejecutando los comandos de *systemctl* `poweroff` o `reboot`.

Descargar una imagen:

```
# machinectl pull-tar *URL* *name*

```

### Utilidades de systemd

Bastantes de las utilidades de systemd han sido actualizadas para que funcionen con contenedores. Herramientas que generalmente proporcionan un parámetro `-M, --machine=` tomaran el nombre del contenedor como argumento.

Ejemplos.

Ver el histórico de una maquina especifica:

```
$ journalctl -M *MyContainer*

```

Mostrar el contenido del grupo de control:

```
$ systemd-cgls -M *MyContainer*

```

Mostrar el tiempo de arranque del contenedor:

```
$ systemd-analyze -M *MyContainer*

```

Para una perspectiva de los recursos usados:

```
$ systemd-cgtop

```