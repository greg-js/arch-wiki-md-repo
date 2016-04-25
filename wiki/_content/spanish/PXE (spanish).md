De [Wikipedia:Preboot Execution Environment](https://en.wikipedia.org/wiki/Preboot_Execution_Environment "wikipedia:Preboot Execution Environment"):

	*Preboot eXecution Environment (PXE) (Entorno de ejecución de prearranque), es un entorno para arrancar e instalar el sistema operativo en ordenadores a través de una red, de manera independiente de los dispositivos de almacenamiento de datos disponibles (como discos duros) o de los sistemas operativos instalados.*

En esta guía, PXE se usa para arrancar los medios de instalación con una Option Rom apropiada que soporte PXE como objetivo.

## Contents

*   [1 Preparación](#Preparaci.C3.B3n)
*   [2 Instalación del servidor](#Instalaci.C3.B3n_del_servidor)
    *   [2.1 Red](#Red)
    *   [2.2 DHCP + TFTP](#DHCP_.2B_TFTP)
    *   [2.3 HTTP](#HTTP)
*   [3 Instalación](#Instalaci.C3.B3n)
    *   [3.1 Arranque](#Arranque)
    *   [3.2 Tras el arranque](#Tras_el_arranque)
*   [4 Métodos Alternativos](#M.C3.A9todos_Alternativos)
    *   [4.1 NFS](#NFS)
    *   [4.2 NBD](#NBD)
    *   [4.3 Memoria baja](#Memoria_baja)

## Preparación

Descarga el medio de instalación más reciente de [aquí](https://www.archlinux.org/download/).

A continuación monta la imagen:

```
# mkdir -p /mnt/archiso
# mount -o loop,ro archlinux-2013.02.01-dual.iso /mnt/archiso
```

## Instalación del servidor

Necesitarás instalar un servidor, TFTP, y HTTP para configurar la red, cargar pxelinux/kernel/initramfs, y finalmente cargar el sistema de archivos de la raíz (respectivamente).

### Red

Activa tu tarjeta de red ethernet, y asignale una dirección apropiada.

```
# ip link set eth0 up
# ip addr add 192.168.0.1/24 dev eth0
```

### DHCP + TFTP

Necesitarás servidores DHCP y TFTP para configurar la red en el directorio de instalación y para facilitar la transferencia de archivos entre PXE servidor y cliente; dnsmasq hace las cos cosas, y es extremadamente fácil de instalar.

Instala [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq):

 `# pacman -S dnsmasq` 

Configura [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq):

 `# vim /etc/dnsmasq.conf` 
```
port=0
interface=eth0
bind-interfaces
dhcp-range=192.168.0.50,192.168.0.150,12h
dhcp-boot=/arch/boot/syslinux/pxelinux.0
dhcp-option-force=209,boot/syslinux/archiso.cfg
dhcp-option-force=210,/arch/
enable-tftp
tftp-root=/mnt/archiso
```

Inicia [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq):

 `# systemctl start dnsmasq.service` 

### HTTP

Gracias a recientes cambios en [archiso](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)"), ahora es posible arrancar desde HTTP (archiso_pxe_http initcpio hook) o NFS (archiso_pxe_nfs initcpio hook); de entre todas las posibilidades, darkhttpd es de lejos el mas sencillo de instalar (y el más ligero).

Primero, instala [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd):

 `# pacman -S darkhttpd` 

Luego inicia [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd) usando /mnt/archiso como raíz de los archivos:

 `# darkhttpd /mnt/archiso` 
```
darkhttpd/1.8, copyright (c) 2003-2011 Emil Mikulic.
listening on: [http://0.0.0.0:80/](http://0.0.0.0:80/)
```

## Instalación

Para esta parte, necesitarás averiguar como decirle al cliente que realice un arranque con PXE; en la esquina de la pantalla junto con los mensajes normales, normalmente habrá alguna pista de que tecla apretar para intentar arrancar primero con PXE. En un IBM x3650 *F12* sale un menú de arranque, la primera opción del cual es *Network* ("Red"); en un Dell PE 1950/2950 apretar *F12* inicia el arranque con PXE directamente.

### Arranque

Leer [journald](/index.php/Systemd_(Espa%C3%B1ol)#Journal "Systemd (Español)") en el servidor PXE debería proveernos de cierta información sobre lo que pasa durante las primeras fases del proceso de arranque de PXE:

 `# journalctl -u dnsmasq -f` 
```
dnsmasq-dhcp[2544]: DHCPDISCOVER(eth1) 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPOFFER(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPREQUEST(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-dhcp[2544]: DHCPACK(eth1) 192.168.0.110 00:1a:64:6a:a2:4d 
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/pxelinux.0 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/whichsys.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe_choose.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/ifcpu64.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe_both_inc.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_head.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe32.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_pxe64.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/archiso_tail.cfg to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/vesamenu.c32 to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/syslinux/splash.png to 192.168.0.110
```

Tras cargar `pxelinux.0` y `archiso.cfg` vía TFTP, se presentará (ojalá) un menú de arranque [syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)") con varias opciones, dos de la cuales nos serán especialmente útiles.

Selecciona

 `Boot Arch Linux (x86_64) (HTTP)` 

o

 `Boot Arch Linux (i686) (HTTP)` 

dependiendo de la arquitectura de tu CPU.

Luego el kernel y initramfs (de acuerdo con la arquitectura seleccionada) serán transferidos vía TFTP:

```
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/x86_64/vmlinuz to 192.168.0.110
dnsmasq-tftp[2544]: sent /mnt/archiso/arch/boot/x86_64/archiso.img to 192.168.0.110
```

Si todo va bien, tras esto deberías ver actividad en darkhttpd proviniente del objetivo PXE; en este momento el kernel debería estar cargado en el objetivo PXE, e iniciado:

```
1348347586 192.168.0.110 "GET /arch/aitab" 200 678 "" "curl/7.27.0"
1348347587 192.168.0.110 "GET /arch/x86_64/root-image.fs.sfs" 200 107860206 "" "curl/7.27.0"
1348347588 192.168.0.110 "GET /arch/x86_64/usr-lib-modules.fs.sfs" 200 36819181 "" "curl/7.27.0"
1348347588 192.168.0.110 "GET /arch/any/usr-share.fs.sfs" 200 63693037 "" "curl/7.27.0"
```

Tras la descarga de la raíz del sistema vía HTTP, finalmente acabarás en un terminal zsh como superusuario, con un fantástico [grml config](https://www.archlinux.org/packages/extra/any/grml-zsh-config/).

### Tras el arranque

A no ser que quieras que todo el tráfico pase por tu servidor PXE (que igualmente no funcionará a no ser que [lo configures correctamente](/index.php/Simple_stateful_firewall#Setting_up_a_NAT_gateway "Simple stateful firewall")), te interesa detener [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) y definir un nuevo asentamiento en el objetivo de la instalación, de acuerdo con el diseño de tu red.

 `# systemctl stop dnsmasq.service` 

También puedes detener [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd); el objetivo ya ha descargado el sistema de archivos base, así que ya no es necesario. Mientras lo haces, también puedes desmontar la imagen de desinstalación:

 `# umount /mnt/archiso` 

Ahora ya puedes seguir la [guía oficial de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

## Métodos Alternativos

Por estar implicado con el menú syslinux, hay varias alternativas más:

### NFS

Necesitarás instalar un [servidor NFS](/index.php/NFS "NFS") exportando la raíz a la raíz de tu medio de instalación montado —sería `/mnt/archiso` si seguiste las [primeras secciones](#Preparaci.C3.B3n) de esta guía—. Después de configurar el servidor, agregue la siguiente línea a su archivo `/etc/exports`:

 `/etc/exports`  `/mnt/archiso 192.168.0.0/24(ro,no_subtree_check)` 

Si el servidor ya estaba en marcha, reexporte los sistemas de archivos con `exportfs -r -a -v`.

La configuración por defecto del instalador espera encontrar el servidor NFS en `/run/archiso/bootmnt`, por lo que tendrá que modificar las opciones de arranque. Para ello, presione la tecla Tab sobre el menú de arranque apropiado para elegir y editar la opción `archiso_nfs_srv` que corresponda:

 `archiso_nfs_srv=${pxeserver}:/mnt/archiso` 

De otro modo, puede utilizar `/run/archiso/bootmnt` para completar el proceso.

Una vez cargado el kernel, la imgen bootstrap de Arch copiará el sistema de archivos root a través de NFS para el arranque del equipo anfitrión. Una vez que esto se haya completado, tendrá un sistema en ejecución.

### NBD

Instala [nbd](https://www.archlinux.org/packages/?name=nbd) y configúralo:

 `# vim /etc/nbd-server/config` 
```
[generic]
[archiso]
    readonly = true
    exportname = /srv/archlinux-2013.02.01-dual.iso
```

### Memoria baja

Puedes usar la opción `copytoram` de [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para controlar si la raíz del sitema de archivos debe copiarse a la ram integramente en el inicio del arranque.

Es muy recomendado dejar esta opción, y solo desactivarla si es realmente necesario (sistemas con menos de ~256MB de memoria RAM). Añade `copytoram=n` a la línea del kernel si quieres hacer esto.