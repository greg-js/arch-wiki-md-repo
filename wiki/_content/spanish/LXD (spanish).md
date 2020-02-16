**Estado de la traducción**
Este artículo es una traducción de [LXD](/index.php/LXD "LXD"), revisada por última vez el **2020-02-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=LXD&diff=0&oldid=597151) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**[LXD](https://linuxcontainers.org/lxd/)** es un «hipervisor» de contenedores y máquinas virtuales, además de una nueva experiencia de usuario para los [contenedores de Linux](/index.php/Linux_Containers "Linux Containers").

Artículos relacionados

*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparación](#Preparación)
    *   [1.1 Software requerido](#Software_requerido)
    *   [1.2 Método alternativo de instalación](#Método_alternativo_de_instalación)
    *   [1.3 Configurar LXD](#Configurar_LXD)
    *   [1.4 Accediendo a LXD como un usuario sin privilegios](#Accediendo_a_LXD_como_un_usuario_sin_privilegios)
*   [2 Utilización](#Utilización)
    *   [2.1 Crear contenedor](#Crear_contenedor)
    *   [2.2 Redes en LXD](#Redes_en_LXD)
    *   [2.3 lxd-agent dentro de una VM](#lxd-agent_dentro_de_una_VM)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Comprobar la configuración del kernel](#Comprobar_la_configuración_del_kernel)
    *   [3.2 Lanzar un contenedor sin CONFIG_USER_NS](#Lanzar_un_contenedor_sin_CONFIG_USER_NS)
    *   [3.3 Los límites de recursos no se aplican cuando se ven desde dentro de un contenedor](#Los_límites_de_recursos_no_se_aplican_cuando_se_ven_desde_dentro_de_un_contenedor)
    *   [3.4 Fallo en el inicio de una VM](#Fallo_en_el_inicio_de_una_VM)
    *   [3.5 Sin IPv4 con systemd-networkd](#Sin_IPv4_con_systemd-networkd)
*   [4 Desinstalar](#Desinstalar)
*   [5 Véase también](#Véase_también)

## Preparación

### Software requerido

Instale [LXC](/index.php/LXC "LXC") y el paquete [lxd](https://www.archlinux.org/packages/?name=lxd), entonces [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `lxd.service`.

Véase [Linux Containers#Enable support to run unprivileged containers (optional)](/index.php/Linux_Containers#Enable_support_to_run_unprivileged_containers_(optional) "Linux Containers") si desea ejecutar contenedores *sin privilegios*. De lo contrario véase [#Lanzar un contenedor sin CONFIG_USER_NS](#Lanzar_un_contenedor_sin_CONFIG_USER_NS).

### Método alternativo de instalación

Un método alternativo de instalación es a través de [snapd](/index.php/Snapd "Snapd"), instalando el paquete [snapd](https://aur.archlinux.org/packages/snapd/) y ejecutando:

```
# snap install lxd

```

### Configurar LXD

LXD necesita configurar un grupo de almacenamiento y (si desea acceso a Internet) la configuración de red. Para ello, ejecute lo siguiente como superusuario:

```
# lxd init

```

### Accediendo a LXD como un usuario sin privilegios

Por defecto, el demonio LXD permite el acceso a los usuarios del grupo `lxd`, así que añada su usuario al grupo:

```
# usermod -a -G lxd <usuario>

```

**Advertencia:** Cualquiera añadido al grupo `lxd` es equivalente al superusuario. Más información [aquí](https://github.com/lxc/lxd#security) y [aquí](https://bugs.launchpad.net/ubuntu/+source/lxd/+bug/1829071).

## Utilización

### Crear contenedor

LXD tiene dos partes, el demonio (el binario lxd) y el cliente (el binario lxc). Ahora que el demonio está configurado y en ejecución, puede crear un contenedor:

```
$ lxc launch ubuntu:16.04

```

Alternativamente, también puede usar un host LXD remoto como fuente de imágenes. Viene uno preconfigurado en LXD, llamado "images" (images.linuxcontainers.org)

```
$ lxc launch images:centos/7/amd64 centos

```

Para crear un contenedor Arch de amd64:

```
$ lxc launch images:archlinux/current/amd64 arch

```

### Redes en LXD

LXD utiliza las capacidades de red de LXC. Por defecto, conecta contenedores al dispositivo de red `lxcbr0`. Consulte la documentación de LXC en la [configuración de la red](/index.php/Linux_Containers#Host_network_configuration "Linux Containers") para configurar un puente *(bridge)* para sus contenedores.

Si desea utilizar una interfaz diferente a `lxcbr0`, edite la predeterminada utilizando la herramienta de línea de órdenes lxc:

```
$ lxc profile edit default

```

Se abrirá un editor con un archivo de configuración que, de forma predeterminada, contiene:

```
name: default
config: {}
devices:
  eth0:
    name: eth0
    nictype: bridged
    parent: lxcbr0
    type: nic

```

Puede establecer el parámetro `parent` al puente que desee que LXD conecte los contenedores de forma predeterminada.

### lxd-agent dentro de una VM

Dentro de las VMs `lxd-agent` no está instalado por defecto en el sistema operativo. Este se puede instalar en el equipo montando un recurso de red compartido `9p`. Esto requiere acceso a la consola con un usuario válido.

```
   $ lxc console v1
   To detach from the console, press: <ctrl>+a q

   Ubuntu 18.04.3 LTS v1 ttyS0

   v1 login: ubuntu
   Password: 
   Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-74-generic x86_64)

   ubuntu@v1:~$ sudo -i
   root@v1:~# mount -t 9p config /mnt/
   root@v1:~# cd /mnt/
   root@v1:/mnt# ./install.sh 
   Created symlink /etc/systemd/system/multi-user.target.wants/lxd-agent.service → /lib/systemd/system/lxd-agent.service.
   Created symlink /etc/systemd/system/multi-user.target.wants/lxd-agent-9p.service → /lib/systemd/system/lxd-agent-9p.service.

   LXD agent has been installed, reboot to confirm setup.
   To start it now, unmount this filesystem and run: systemctl start lxd-agent-9p lxd-agent
   root@v1:/mnt# reboot

```

Tras esto `lxd-agent` estará disponible y `lxc exec` funcionará dentro de la VM.

## Solución de problemas

### Comprobar la configuración del kernel

Por defecto, el kernel de Arch Linux está compilado correctamente para los contenedores de Linux y su interfaz LXD. Sin embargo, si está utilizando un kernel personalizado o con opciones modificadas, el kernel podría estar configurado incorrectamente. Verifique que el kernel en ejecución esté correctamente configurado para ejecutar un contenedor:

```
$ lxc-checkconfig

```

### Lanzar un contenedor sin CONFIG_USER_NS

Para lanzar imágenes debe proporcionar `security.privileged=true` durante la creación de la imagen:

```
$ lxc launch ubuntu:16.04 ubuntu -c security.privileged=true

```

O para una imagen ya existente puede editar la configuración:

 `$ lxc config edit ubuntu` 
```
name: ubuntu
profiles:
- default
config:
  ...
  security.privileged: "true"
  ...
devices:
  root:
    path: /
    type: disk
ephemeral: false

```

O para activar `security.privileged=true` para los nuevos contenedores, edite la configuración para el perfil predeterminado *(default)*:

```
$ lxc profile edit default

```

### Los límites de recursos no se aplican cuando se ven desde dentro de un contenedor

El servicio lxcfs (encontrado en el repositorio Community) necesita ser instalado e iniciado:

```
$ systemctl start lxcfs

```

lxd tendrá que ser reiniciado. Active lxcfs para que el servicio se inicie en el arranque.

### Fallo en el inicio de una VM

Arch Linux no distribuye el firmware ovmf firmado para inicio seguro, así que para arrancar máquinas virtuales debe desactivar el arranque seguro por el momento.

```
$ lxc launch ubuntu:18.04 test-vm --vm -c security.secureboot=false

```

Esto también se puede añadir al perfil predeterminado.

### Sin IPv4 con systemd-networkd

A partir de la versión 244.1, systemd detecta si los contenedores pueden escribir en `/sys`. Si es así, udev se inicia automáticamente y rompe IPv4 en contenedores sin privilegios. Véase [commit bf331d8](https://github.com/systemd/systemd-stable/commit/96d7083c5499b264ecebd6a30a92e0e8fda14cd5) y el [debate en linuxcontainers](https://discuss.linuxcontainers.org/t/no-ipv4-on-arch-linux-containers/6395).

En los contenedores creados a partir de 2020, ya debería haber un anulador de `systemd.networkd.service` para solucionar este problema, debe crearlo si no es así:

 `/etc/systemd/system/systemd-networkd.service.d/lxc.conf` 
```
[Service]
BindReadOnlyPaths=/sys
```

También podría solucionar este problema estableciendo `raw.lxc: lxc.mount.auto = proc:rw sys:ro` en el perfil del contenedor para asegurarse de que `/sys` es de solo lectura para todo el contenedor, aunque esto podría ser problemático, según el debate vinculado arriba.

## Desinstalar

[Detenga](/index.php/Stop_(Espa%C3%B1ol) "Stop (Español)") y desactive `lxd.service` y `lxd.socket`:

Luego desinstale el paquete a través de pacman:

```
 # pacman -R lxd

```

Si desinstaló el paquete sin desactivar el servicio, es posible que tenga un enlace simbólico roto en `/etc/systemd/system/multi-user.wants/lxd.service`.

Si desea eliminar todos los datos:

```
 # rm -r /var/lib/lxd

```

Si utilizó alguna de las configuraciones de red de ejemplo, debería eliminarla también.

## Véase también

*   [Documentation oficial](https://lxd.readthedocs.io)
*   [La página oficial de LXD](https://linuxcontainers.org/lxd/)
*   [La página en GitHub de LXD](https://github.com/lxc/lxd)