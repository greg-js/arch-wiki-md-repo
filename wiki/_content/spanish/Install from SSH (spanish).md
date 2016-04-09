## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Arrancar desde el soporte de instalación](#Arrancar_desde_el_soporte_de_instalaci.C3.B3n)
*   [3 Configurar el entorno live para usar SSH](#Configurar_el_entorno_live_para_usar_SSH)
*   [4 Conectar al PC de destino a través de SSH](#Conectar_al_PC_de_destino_a_trav.C3.A9s_de_SSH)
    *   [4.1 Notas](#Notas)
*   [5 Siguientes pasos](#Siguientes_pasos)

## Introducción

Este artículo está destinado a mostrar a los usuarios cómo instalar Arch de forma remota a través de una conexión SSH. Considere este enfoque sobre las normas estándar en escenarios tales como los siguientes:

Configuración de Arch sobre...

*   HTPC sin un monitor adecuado (es decir, un SDTV).
*   Un PC que se encuentra en otra ciudad, estado, país (casa de un amigo, casa de los padres, etc.).
*   Un PC que lo configuraría mejor de forma remota, por ejemplo, desde la comodidad de la propia estación de trabajo con la facilidad de copiar/pegar las indicaciones de Arch Wiki.

**Nota:** Los dos primeros pasos requieren el acceso físico a la máquina. Obviamente, si se encuentra físicamente en otro lugar, esto tendrá que ser coordinado con otra persona.

## Arrancar desde el soporte de instalación

Arranque en un entorno live de Arch a través de un [CD live/imagen USB](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Preparar_el_soporte_de_instalaci.C3.B3n_m.C3.A1s_reciente "Beginners' guide (Español)").

## Configurar el entorno live para usar SSH

**Nota:** Las siguientes órdenes deben ser ejecutadas como usuario root, de ahí el signo **#** antes de las órdenes.

Se debe haber iniciado sesión como root en este punto. (Este es el usuario por defecto cuando se ejecuta el livecd)

En primer lugar, configure la red en la máquina de destino.

Suponiendo que tenga una conexión por cable, ejecutar `dhclient` o `dhcpcd` debería ser suficiente para conseguir conexión. Para obtener más información, visite [Configuring Network (Español)](/index.php/Configuring_Network_(Espa%C3%B1ol) "Configuring Network (Español)").

Si dispone de una conexión inalámbrica, vea [Wireless network configuration (Español)](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)") y [WPA supplicant (Español)](/index.php/WPA_supplicant_(Espa%C3%B1ol) "WPA supplicant (Español)") para obtener más información sobre cómo establecer una conexión con su punto de acceso.

En segundo lugar, establezca una contraseña de root necesaria para una conexión ssh; la contraseña por defecto de Arch para root está vacía.

```
passwd

```

Por último, inicie el demonio openssh:

```
# systemctl start sshd

```

## Conectar al PC de destino a través de SSH

Conéctese a la máquina de destino a través de la siguiente orden:

```
$ ssh root@dirección.ip.de.destino

```

A partir de aquí, se presenta el mensaje de bienvenida del entorno live y será capaz de administrar el equipo de destino como si estuviera frente a su teclado físico.

```
ssh root@10.1.10.105
root@10.1.10.105's password: 
Last login: Thu Dec 23 08:33:02 2010 from 10.1.10.200
[root@archiso ~]#
```

### Notas

*   Si el equipo de destino está detrás de un firewall/router, dado que el puerto ssh por defecto es 22, obviamente, tendrá que redirigirse a la dirección IP de la LAN de la máquina de destino. La gestión del reenvío de puertos no se trata en esta guía.
*   Se puede editar `/etc/ssh/sshd_config` en el entorno live antes de iniciar el demonio por ejemplo, para ejecutarlo en un puerto no estándar si se desea.

## Siguientes pasos

El cielo es el límite. Si la intención es simplemente instalar Arch desde el soporte live, siga la [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"). Si la intención es modificar la instalación de un Linux existente que se rompió, siga el artículo de la wiki [Install from existing Linux (Español)](/index.php/Install_from_existing_Linux_(Espa%C3%B1ol) "Install from existing Linux (Español)").

¿Quiere [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") o la capacidad de utilizar discos duros con [GPT](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)")?

*   Particione manualmente el HDD/SDD de destino mediante la utilidad **gdisk** instalándola con *pacman -S gdisk* antes de iniciar el programa de instalación de Arch y, cuando se le presente la opción de instalar un gestor de arranque en el marco de la instalación, simplemente no lo haga, y vuelva de nuevo al prompt de root del entorno live.
*   La instalación de grub(2) es trivial en este punto. Simplemente efectúe chroot en el recién instalado sistema Arch (por defecto premontado si saliera del programa de instalación) y, después, instale y configure grub2:

```
cd /mnt
rm console ; mknod -m 600 console c 5 1
rm null ; mknod -m 666 null c 1 3
rm zero ; mknod -m 666 zero c 1 5
mount -t proc proc /mnt/proc
mount -t sysfs sys /mnt/sys
mount -o bind /dev /mnt/dev
chroot /mnt /bin/bash

```

Ahora, dentro de chroot de Arch:

```
pacman -S grub2
grep -v rootfs /proc/mounts > /etc/mtab

```

Editar `/etc/default/grub` a su gusto. Instalar grub y generar un archivo grub.cfg

```
grub-install /dev/sdX --no-floppy
grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:** Lo anterior supone que si el usuario tiene la intención de arrancar desde un disco GPT, debe haber leído y entendido los artículos de la wiki antes mencionados y habrá creado una partición BIOS boot partition tipo ef02 de 1M para grub(2).

Cuando esté listo para reiniciar la nueva instalación de Arch, salga de chroot y desmonte las particiones antes de un reinicio del sistema.

```
exit
umount /mnt/boot   # si está montada esta o cualquier otra partición separada
umount /mnt/{proc,sys,dev}
umount /mnt

```