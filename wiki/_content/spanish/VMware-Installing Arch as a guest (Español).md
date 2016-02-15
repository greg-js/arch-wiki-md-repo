Este artículo trata sobre la instalación de Arch Linux en un producto [VMware](/index.php/VMware "VMware"), como [Player (Plus)](http://www.vmware.com/products/player/), [Fusion](http://www.vmware.com/products/fusion/) o [Workstation](http://www.vmware.com/products/workstation/).

## Contents

*   [1 Controladores en el kernel](#Controladores_en_el_kernel)
*   [2 Herramientas VMware frente a Open-VM-Tools](#Herramientas_VMware_frente_a_Open-VM-Tools)
*   [3 Open-VM-Tools](#Open-VM-Tools)
    *   [3.1 Módulos](#M.C3.B3dulos)
    *   [3.2 Utilidades](#Utilidades)
    *   [3.3 Instalación](#Instalaci.C3.B3n)
*   [4 Herramientas oficiales de VMware](#Herramientas_oficiales_de_VMware)
    *   [4.1 Módulos](#M.C3.B3dulos_2)
    *   [4.2 Instalación (desde el huésped)](#Instalaci.C3.B3n_.28desde_el_hu.C3.A9sped.29)
*   [5 Configuración de Xorg](#Configuraci.C3.B3n_de_Xorg)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Carpetas compartidas](#Carpetas_compartidas)
        *   [6.1.1 Activar en el arranque](#Activar_en_el_arranque)
        *   [6.1.2 Base de datos mlocate prune](#Base_de_datos_mlocate_prune)
    *   [6.2 Aceleración 3D](#Aceleraci.C3.B3n_3D)
    *   [6.3 Sincronizar la hora](#Sincronizar_la_hora)
        *   [6.3.1 Máquina anfitriona como fuente de la hora](#M.C3.A1quina_anfitriona_como_fuente_de_la_hora)
        *   [6.3.2 Servidor externo como fuente de la hora](#Servidor_externo_como_fuente_de_la_hora)
    *   [6.4 Adaptador SCSI Paravirtual](#Adaptador_SCSI_Paravirtual)
*   [7 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [7.1 Problemas con el ratón](#Problemas_con_el_rat.C3.B3n)
        *   [7.1.1 Botones desaparecidos](#Botones_desaparecidos)
    *   [7.2 Problemas en el arranque](#Problemas_en_el_arranque)
        *   [7.2.1 Tiempo de arranque lento](#Tiempo_de_arranque_lento)
        *   [7.2.2 Cuelgues al apagar/reiniciar](#Cuelgues_al_apagar.2Freiniciar)
    *   [7.3 Problemas de reajuste automático](#Problemas_de_reajuste_autom.C3.A1tico)

## Controladores en el kernel

*   `vmw_balloon` - Controlador de gestión de la memoria física. Actúa como un «globo» que puede inflarse para recuperar [páginas de memoria](https://en.wikipedia.org/wiki/es:Paginaci%C3%B3n_de_memoria "wikipedia:es:Paginación de memoria") física reservándolas en el sistema huésped e invalidándolas en el monitor, liberando las páginas de la máquina subyacente para que puedan ser destinadas a otros huéspedes. También se puede desinflar para permitir el uso de más memoria física para los huéspedes. La memoria de la máquina virtual desasignada puede ser reutilizada en el anfitrión sin necesidad de terminar el huésped.
*   `vmw_pvscsi` - Para usar Paravirtual SCSI (PVSCSI) HBA de VMware.
*   `vmw_vmci` - Interfaz de comunicación de la máquina virtual. Permite la comunicación de alta velocidad entre anfitrión y huésped en un entorno virtual a través del dispositivo virtual VMCI.
*   `vsock` - Protocolo [Socket](https://en.wikipedia.org/wiki/es:Socket_de_Internet "wikipedia:es:Socket de Internet") Virtual. Es similar al protocolo de conexión TCP/IP, que permite la comunicación entre máquinas virtuales e hipervisor o anfitrión.
*   `vmw_vsock_vmci_transport` - Implementa un transporte VMCI para sockets virtuales.
*   `vmwgfx` - Para la aceleración 3D. Se trata de activar un modo KMS por controlador DRM para el hardware virtual VMware SVGA2.
*   `vmxnet3` - Para configurar la tarjeta de red virtual ethernet vmxnet3 de VMware.

## Herramientas VMware frente a Open-VM-Tools

En 2007, VMware lanzó grandes particiones de [VMware Tools](http://kb.vmware.com/kb/340) bajo licencia LGPL como [Open-VM-Tools](http://sourceforge.net/projects/open-vm-tools/). Las herramientas oficiales no están disponibles [separadamente](http://packages.vmware.com/tools/esx/latest/repos/index.html) para Arch Linux.

Originalmente, las herramientas de VMware proporcionaban los mejores controladores de red y de almacenamiento, junto con funcionalidades para otras características como la sincronización horaria. Sin embargo, desde hace tiempo los controladores para el adaptador de red/SCSI son parte del kernel de Linux, y las herramientas de VMware solo son necesarias para incorporar características adicionales.

## Open-VM-Tools

### Módulos

El paquete [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) viene con los siguientes módulos:

*   `vmblock` - Controlador del sistema de archivos. Permite la funcionalidad de arrastrar y soltar entre anfitrión y huésped ([sustituido](https://www.mail-archive.com/open-vm-tools-devel@lists.sourceforge.net/msg00213.html) por la utilidad `vmware-vmblock-fuse`).
*   `vmci` - Interfaz de comunicación de alto rendimiento entre el anfitrión y el huésped.
*   `vmhgfs` - Controlador del sistema de archivos. Permite compartir recursos entre anfitrión y huésped.
*   `vsock` - Sockets para VMCI (Virtual Machine Communication Interface).
*   `vmsync` - Controlador experimental de sincronización del sistema de archivos. Activa el sistema de archivos [quiescing](https://en.wikipedia.org/wiki/quiescing "wikipedia:quiescing") cuando crea copias de seguridad e instantáneas.
*   `vmxnet` - Soporte para el viejo adaptador de red VMXNET.

### Utilidades

El paquete [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) viene concretamente con las siguientes utilidades:

*   `vmtoolsd` - Servicio responsable de informar del estado de la máquina virtual.
*   `vmware-checkvm` - Herramienta para comprobar si un programa se está ejecutando en el sistema huésped.
*   `vmware-toolbox-cmd` - Herramienta para obtener información de la máquina virtual por el anfitrión.
*   `vmware-user-suid-wrapper` - Herramienta para activar el uso compartido del portapapeles (copiar/pegar) entre anfitrión y huésped.
*   `vmware-vmblock-fuse` - Utilidad del sistema de archivos. Permite la funcionalidad arrastrar y soltar entre anfitrión y huésped a través de [FUSE](https://en.wikipedia.org/wiki/es:Sistema_de_archivos_en_el_espacio_de_usuario "wikipedia:es:Sistema de archivos en el espacio de usuario") (sistema de archivos en el espacio de usuario).
*   `vmware-xferlogs` - Volcado de la información del registro/depuración de errores del archivo de registro de la máquina virtual.

### Instalación

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") y [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

Open-VM-Tools lee la información sobre la versión desde `/etc/arch-release`, que está vacía:

```
# cat /proc/version > /etc/arch-release

```

[Inície](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") `vmtoolsd.service` y actívelo en el arranque, si lo desea.

**Nota:** Hay un error en `vmtoolsd`, donde el servicio no es capaz de apagar correctamente y se cuelga durante 60 segundos. Una solución rápida se describe en [el foro](https://bbs.archlinux.org/viewtopic.php?pid=1206006#p1206006).

## Herramientas oficiales de VMware

### Módulos

*   `vmblock` - Controlador del sistema de archivos. Permite la funcionalidad de arrastrar y soltar entre anfitrión y huésped ([sustituido](https://www.mail-archive.com/open-vm-tools-devel@lists.sourceforge.net/msg00213.html) por la utilidad `vmware-vmblock-fuse`).
*   `vmci` - Interfaz de comunicación de alto rendimiento entre anfitrión y huésped.
*   `vmmon` - Monitor de la máquina virtual.
*   `vmnet` - Controlador de red.
*   `vsock` - Sockets de VMCI.

### Instalación (desde el huésped)

Instale las dependencias: [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) (para compilar), [net-tools](https://www.archlinux.org/packages/?name=net-tools) (para `ifconfig`, usado por el programa de instalación) y [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (para las cabeceras del kernel).

A continuación, cree los directorios de inicio _bogus_ para el instalador:

```
# for x in {0..6}; do mkdir -p /etc/init.d/rc$x.d; done

```

El instalador se puede montar entonces:

```
# mount /dev/cdrom /mnt

```

Extráigalo (por ejemplo en `/root`):

```
# tar xf /mnt/VMwareTools*.tar.gz -C /root

```

E, inícielo:

```
# perl /root/vmware-tools-distrib/vmware-install.pl

```

Puede ignorar los siguientes fallos de compilación:

*   Tarjeta de red virtual VMNEXT 3
*   "Warning: This script could not find mkinitrd or update-initramfs and cannot remake the initrd file!"

Reinicie la máquina virtual:

```
# systemctl reboot

```

Inicie sesión y ejecute VMware Tools:

```
# /etc/init.d/rc6.d/K99vmware-tools start

```

**Sugerencia:** También hay un [proyecto](https://github.com/rasa/vmware-tools-patches) en GitHub tratando de automatizar todo esto.

## Configuración de Xorg

**Nota:** Para utilizar Xorg en una máquina virtual, se necesita un mínimo de memoria de 32MB para VGA.

Instale las dependencias: [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse), [xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware) y [svga-dri](https://www.archlinux.org/packages/?name=svga-dri).

Si arranca con `graphical.target`, esto está casi terminado. `/etc/xdg/autostart/vmware-user.desktop` obtendrá al arranque la configuración de la mayor parte de las cosas que se necesitan para trabajar con la máquina virtual.

Sin embargo, si el arranque es con `multi-user.target` o utilizando una configuración poco frecuente (por ejemplo, varios monitores), entonces, `vmtoolsd.service` tiene que ser [activado](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)").

## Consejos y trucos

### Carpetas compartidas

**Nota:** Esta funcionalidad solo está disponible en VMware Workstation y Fusion

Compartimos una carpeta seleccionando _Edit virtual machine settings > Options > Shared Folders > Always enabled_, creando así un nuevo recurso compartido.

Ahora, debería ser capaz de ver las carpetas compartidas mediante la ejecución de la orden vmware-hgfsclient:

```
$ vmware-hgfsclient

```

Añadir una regla para cada recurso compartido:

 `/etc/fstab` 

```
.host:/_<shared_folder>_ _/home/user1/shares_ vmhgfs defaults 0 0

```

Crear y montar las carpetas compartidas:

```
# mkdir /home/user1/shares
# mount /home/user1/shares

```

También es posible montarlas temporalmente:

```
# mount -t vmhgfs .host:/_<shared_folder>_ /home/user1/shares

```

**Nota:** Puede ver «Error: cannot mount filesystem: No such device», si el módulo vmhgfs no esta en el kernel de Linux aún antes de tratar de montar las carpetas.

Esto se puede resolver temporalmente ejecutando la orden «modprobe vmhgfs», pero para que sea cargado automáticamente durante el arranque, es necesario agregar el módulo vmhgfs a mkinitcpio.conf.

#### Activar en el arranque

Para que las carpetas compartidas funcionen es necesario haber cargado el controlador `vmhgfs`. Solo tiene que crear los siguientes `.service`:

 `/etc/systemd/system/mnt-hgfs.mount` 

```
[Unit]
Description=Load VMware shared folders
ConditionPathExists=.host:/_<shared_folder>_
ConditionVirtualization=vmware

[Mount]
What=.host:/_<shared_folder>_
Where=_/home/user1/shares_
Type=vmhgfs
Options=defaults,noatime

[Install]
WantedBy=multi-user.target
```

 `/etc/systemd/system/mnt-hgfs.automount` 

```
[Unit]
Description=Load VMware shared folders
ConditionPathExists=.host:/_<shared_folder>_
ConditionVirtualization=vmware

[Automount]
Where=_/home/user1/shares_

[Install]
WantedBy=multi-user.target
```

Activar el target de montaje con:

```
# systemctl enable mnt-hgfs.automount

```

#### Base de datos mlocate prune

Al usar [mlocate](/index.php/Mlocate "Mlocate"), es inútil tratar de indexar los directorios compartidos en `locate DB`. Por lo tanto, añada los directorios de `PRUNEPATHS` en `/etc/updatedb`.

### Aceleración 3D

Si no se selecciona en el huésped al tiempo de crearlo, la aceleración 3D se puede activar en: _Edit virtual machine settings > Hardware > Display > Accelerate 3D graphics_.

### Sincronizar la hora

Configurar la sincronización horaria en una máquina virtual es importante; las fluctuaciones son inevitables al producirse con mayor facilidad en un sistema huésped, en comparación con un equipo físico. Esto se debe principalmente al uso compartido de la CPU por más de un sistema huésped.

Hay 2 opciones para configurar la sincronización horaria: desde el sistema anfitrión o desde una fuente externa.

#### Máquina anfitriona como fuente de la hora

Para utilizar el sistema anfitrión como fuente del tiempo:

```
# vmware-toolbox-cmd timesync enable

```

Para sincronizar el sistema huésped después de suspender el anfitrión:

```
# hwclock --hctosys --localtime

```

#### Servidor externo como fuente de la hora

Ver [NTP](/index.php/NTP "NTP").

### Adaptador SCSI Paravirtual

[VMware Paravirtual SCSI (PVSCSI) adapters](http://kb.vmware.com/kb/1010398) son los adaptadores de almacenamiento de alto rendimiento para VMware ESXi que pueden dar como resultado un mayor rendimiento y menor utilización de CPU. Los adaptadores PVSCSI son los más adecuados para los entornos, donde el hardware o las aplicaciones demandan una cantidad muy alta de rendimiento de E/S. cpio -p linux

El tipo de adaptador SCSI de `VMware Paravirtual` está disponible en la configuración de la máquina virtual.

## Solución de problemas

### Problemas con el ratón

Los siguientes problemas pueden ocurrir con el ratón:

*   La característica automática de agarrar/soltar no mantiene el agarre automáticamente cuando el cursor entra en la ventana.
*   Imput con retraso.
*   Los clics no se registran en algunas aplicaciones.

VMware intenta optimizar automáticamente el ratón para juegos. Si experimenta problemas, se recomienda su desactivación: _Edit > Preferences > Input > Optimize mouse for games: Never_

En otro caso, podría ser necesario [desactivar](http://www.spinics.net/lists/xorg/msg53932.html) el evento `catchall` en `10-evdev.conf`:

 `/etc/X11/xorg.conf.d/10-evdev.conf` 

```
#Section "InputClass"
#        Identifier "evdev pointer catchall"
#        MatchIsPointer "on"
#        MatchDevicePath "/dev/input/event*"
#        Driver "evdev"
#EndSection

```

#### Botones desaparecidos

Si no es por defecto, todos los botones del ratón deberían estar funcionando después de añadir `[mouse.vusb.useBasicMouse = "FALSE"](https://communities.vmware.com/thread/457313?start=15&tstart=0)` a `.vmx`.

 `~/vmware/_<Virtual Machine name>_/_<Virtual Machine name>_.vmx`  `mouse.vusb.useBasicMouse = "FALSE"` 

### Problemas en el arranque

#### Tiempo de arranque lento

Es posible que vea los siguientes errores si la función hot-add de la memoria de VMWare está activada.

*   add_memory failed
*   acpi_memory_enable_device() error

Desactive la función hot-add de la memoria ajustando `mem.hotadd = "FALSE"` en `.vmx`.

 `~/vmware/_<Virtual Machine name>_/_<Virtual Machine name>_.vmx`  `mem.hotadd = "FALSE"` 

#### Cuelgues al apagar/reiniciar

Ajuste el tiempo de espera para el servicio vmtoolsd (por defecto 90 segundos).

 `/etc/systemd/system/vmtoolsd.service.d/timeout.conf` 

```
[Service]
TimeoutStopSec=1
```

### Problemas de reajuste automático

Si VMWare se está estirando en lugar de cambiar la resolución, incluso con el servicio del sistema activado, puede que tenga que añadir los módulos a mkinitcpio.conf.

 `/etc/mkinitcpio.conf`  `MODULES="vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx"` 

No se olvide de ejecutar:

 `# mkinitcpio -p linux`