**Estado de la traducción**
Este artículo es una traducción de [LXD](/index.php/LXD "LXD"), revisada por última vez el **2019-03-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=LXD&diff=0&oldid=568311) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**[LXD](https://linuxcontainers.org/lxd/)** es un «hipervisor» de contenedores y una nueva experiencia de usuario para los [contenedores de Linux](/index.php/Linux_Containers "Linux Containers").

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
*   [2 Utilización básica](#Utilización_básica)
    *   [2.1 Crear contenedor](#Crear_contenedor)
*   [3 Utilización avanzada](#Utilización_avanzada)
    *   [3.1 Redes en LXD](#Redes_en_LXD)
        *   [3.1.1 Ejemplo de configuración de red](#Ejemplo_de_configuración_de_red)
    *   [3.2 Modificar procesos y limites de archivos](#Modificar_procesos_y_limites_de_archivos)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Comprobar la configuración del kernel](#Comprobar_la_configuración_del_kernel)
    *   [4.2 Lanzar un contenedor sin CONFIG_USER_NS](#Lanzar_un_contenedor_sin_CONFIG_USER_NS)
    *   [4.3 Sin ipv4 en un contenedor Arch no privilegiado](#Sin_ipv4_en_un_contenedor_Arch_no_privilegiado)
    *   [4.4 Los límites de recursos no se aplican cuando se ven desde dentro de un contenedor](#Los_límites_de_recursos_no_se_aplican_cuando_se_ven_desde_dentro_de_un_contenedor)
*   [5 Desinstalar](#Desinstalar)
*   [6 Véase también](#Véase_también)

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

## Utilización básica

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

## Utilización avanzada

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

#### Ejemplo de configuración de red

Gracias a @jpic, el paquete LXD proporciona ahora algunos ejemplos de configuración de red en `/usr/share/lxd/`. Para utilizar esta configuración ejecute las siguientes órdenes:

```
$ ln -s /usr/share/lxd/dnsmasq-lxd.conf /etc/dnsmasq-lxd.conf
$ ln -s /usr/share/lxd/systemd/system/dnsmasq@lxd.service /etc/systemd/system/dnsmasq@lxd.service 
$ ln -s /usr/share/lxd/netctl/lxd  /etc/netctl/lxd
$ ln -s /usr/share/lxd/dbus-1/system.d/dnsmasq-lxd.conf /etc/dbus-1/system.d/dnsmasq-lxd.conf

```

Si utiliza [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)"), haga también un enlace simbólico al siguiente archivo:

```
$ ln -s /usr/share/lxd/NetworkManager/dnsmasq.d/lxd.conf /etc/NetworkManager/dnsmasq.d/lxd.conf

```

Cambie `parent: lxcbr0` a `parent: lxd`:

```
$ lxc profile edit default

```

Finalmente, [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `dnsmasq@lxd.service` y `netctl@lxd.service`.

Si encuentra algún problema con la configuración de ejemplo proporcionada o si tiene sugerencias para mejorarla, deje un comentario en la página [lxd](https://www.archlinux.org/packages/?name=lxd).

### Modificar procesos y limites de archivos

Es posible que desee aumentar el límite del descriptor de archivo o el límite máximo de procesos de usuario, ya que el límite del descriptor de archivo predeterminado es 1024 en Arch Linux.

[Edite](/index.php/Edit_(Espa%C3%B1ol) "Edit (Español)") `lxd.service`:

 `# systemctl edit lxd.service` 
```
[Service]
LimitNOFILE=infinity
LimitNPROC=infinity
TasksMax=infinity
```

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

### Sin ipv4 en un contenedor Arch no privilegiado

Esto fue probado y validado en LXD v.2.20\. El contenedor no puede iniciar el servicio `systemd-networkd` por lo que no obtiene una dirección ipv4 válida. Stéphane Graber ([Problema en Github](https://github.com/lxc/lxd/issues/4071)) sugirió una solución alternativa, ejecute en el host y reinicie el contenedor:

```
$ lxc profile set default security.syscalls.blacklist "keyctl errno 38"

```

	stgraber: "La razón es que la unidad networkd de systemd de alguna manera hace uso del llavero del núcleo, que no funciona dentro de contenedores sin privilegios en este momento. La línea anterior hace que la llamada al sistema devuelva no-implementado, lo cual es una solución suficiente para que las cosas vuelvan a funcionar."

### Los límites de recursos no se aplican cuando se ven desde dentro de un contenedor

El servicio lxcfs (encontrado en el repositorio Community) necesita ser instalado e iniciado:

```
$ systemctl start lxcfs

```

lxd tendrá que ser reiniciado. Active lxcfs para que el servicio se inicie en el arranque.

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