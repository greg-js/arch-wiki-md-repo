Related articles

*   [GNUnet](/index.php/GNUnet "GNUnet")
*   [I2P](/index.php/I2P "I2P")
*   [Freenet](/index.php/Freenet "Freenet")

[Tor](https://www.torproject.org)es una implementación 'open source' de 2da generación del [enrutamiento de cebolla](https://es.wikipedia.org/wiki/Encaminamiento_de_cebolla) que provee libre acceso a una red proxy anónimos. Su principal objetivo es proteger el [anónimato en Internet](https://en.wikipedia.org/wiki/Anonymity#Anonymity_on_the_Internet) del [análisis de tráfico](https://es.wikipedia.org/wiki/Análisis_de_tráfico).

## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Configuración de Relevos](#Configuraci.C3.B3n_de_Relevos)
*   [4 Corriendo Tor en un Chroot](#Corriendo_Tor_en_un_Chroot)
*   [5 Corriendo Tor en un contenedor systemd-nspawn con una interfaz de red virtual](#Corriendo_Tor_en_un_contenedor_systemd-nspawn_con_una_interfaz_de_red_virtual)
    *   [5.1 Instalación y Configuración del Servidor](#Instalaci.C3.B3n_y_Configuraci.C3.B3n_del_Servidor)
        *   [5.1.1 Interfaz de red virtual](#Interfaz_de_red_virtual)

## Introducción

Los usuarios de la Red Tor ejecutan un enrutamiento de cebolla (*onion proxy* en ingles) en sus computadoras. Este software se conecta a Tor, periódicamente negocia un circuito virtual a través de la red Tor. Tor emplea criptografía en forma de capas (de ahí la analogía con la cebolla), lo que garantiza confidencialidad directa entre los routers. Al mismo tiempo, el software proxy onion presenta una interfaz [SOCKS](https://es.wikipedia.org/wiki/SOCKS) a sus clientes. Las aplicaciones que funcionan en SOCKS pueden apuntar a Tor, quien luego multiplexa el tráfico a través de un circuito virtual Tor.

**Advertencia:** Tor en si mismo no es todo lo que necesitas para mantener el anonimato. Hay otros escollos que te debes cuidar (ver: [¿Quieres que Tor funcione realmente?](https://www.torproject.org/download/download.html.en#warning)).

A través de este proceso el *onion proxy* maneja el trafico en la red para brindar anonimato al usuario final. El anonimato del usuario se mantiene encriptando el trafico, enviadolo a traves de otros nodos de la red Tor, y desencriptandolo en un último nodo para recibir tu tráfico antes de reenviarlo al servidor que fue especificado. Aunque Tor es considerado más seguro que las conexiones directas DNS (sin proxy) comunmente usadas, pueden ser considerablemente más lentas debido a la gran cantidad de tráfico re encaminado. Además, aunque Tor provee protección contra el análisis del tráfico, no puede evitar la confirmación en los límites de la red Tor (entrando y saliendo de la red).

Vea [Wikipedia:Tor](https://es.wikipedia.org/wiki/Tor)para más información.

## Instalación

[Instalar](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [tor](https://www.archlinux.org/packages/?name=tor) está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Usually, you will access Tor using Tor Browser, available as the [tor-browser](https://www.archlinux.org/packages/?name=tor-browser) package or a [portable executable](https://www.torproject.org/projects/torbrowser.html.en).

El [arm](https://www.archlinux.org/packages/?name=arm) (de sus siglas en ingles Anonymizing Relay Monitor) es un paquete que provee una terminal para monitorear el uso de banda ancha, detalles de la conexión y más.

## Configuración

Por defecto Tor lee la configuración del archivo `/etc/tor/torrc`. Las opciones de configuración se encuentran explicadas en [tor(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tor.1) en el [la página de Tor](https://torproject.org/docs/tor-manual.html.en). La configuración por defecto debería funcionar bien para la mayoría de los usuarios de Tor.

Hay potenciales conflictos entre configuraciones dentro de `torrc` y aquellas en `tor.service`.

*   En `torrc`, el `RunAsDaemon` debería por defecto estar puesta en `0`, ya que `Type=simple` está colocado en el `[Service]` sección dentro del archivo `tor.service`.
*   En `torrc`, `User` no debería ser activado, a menos que `User=` este puesto en `root` en la `[Service]` sección dentro de `tor.service`.

### Configuración de Relevos

El máximo número de descriptores de archivos que pueden ser abiertos por Tor puede ser fijado con `LimitNOFILE` en `tor.service`. Relevos rápidos pueden requerir aumentar este valor.

Si su ordenador no está corriendo un servidor web, y no ha colocado`AccountingMax`, considere cambiar su `ORPort` a `443` y/o su `DirPort` a `80`. Muchos usuarios de Tor quedan retenidos detrás de cortafuegos que solo les permite navegar en la web, y este cambio les permitirá alcanzar su sesión Tor. Si ya está usando los puertos `80` y `443`,otros puertos útiles son `22`, `110`, y `143`.[[1]](https://www.torproject.org/docs/tor-relay-debian) Estos no son puertos con privilegio, por lo que para serlos Tor debe correrse como root, colocando `User=root` en el archivo `tor.service` y `User tor` en el archivo `torrc`.

Tal vez le guste revisar [Ciclo de Vida de un Nuevo Relevo](https://blog.torproject.org/blog/lifecycle-of-a-new-relay) de la documentación Tor.

## Corriendo Tor en un Chroot

**Advertencia:** Conectarse vía telnet al puerto local ControlPort parece no funcionar cuando se usa Tor en un chroot

Por motivos de seguridad puede ser deseable correr Tor en un [Chroot](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)"). El siguiente script creará un chroot apropiado en `/opt/torchroot`:

 `~/torchroot-setup.sh` 
```
#!/bin/bash
export TORCHROOT=/opt/torchroot

mkdir -p $TORCHROOT
mkdir -p $TORCHROOT/etc/tor
mkdir -p $TORCHROOT/dev
mkdir -p $TORCHROOT/usr/bin
mkdir -p $TORCHROOT/usr/lib
mkdir -p $TORCHROOT/usr/share/tor
mkdir -p $TORCHROOT/var/lib

ln -s /usr/lib  $TORCHROOT/lib
cp /etc/hosts           $TORCHROOT/etc/
cp /etc/host.conf       $TORCHROOT/etc/
cp /etc/localtime       $TORCHROOT/etc/
cp /etc/nsswitch.conf   $TORCHROOT/etc/
cp /etc/resolv.conf     $TORCHROOT/etc/
cp /etc/tor/torrc       $TORCHROOT/etc/tor/

cp /usr/bin/tor         $TORCHROOT/usr/bin/
cp /usr/share/tor/geoip* $TORCHROOT/usr/share/tor/
cp /lib/libnss* /lib/libnsl* /lib/ld-linux-*.so* /lib/libresolv* /lib/libgcc_s.so* $TORCHROOT/usr/lib/
cp $(ldd /usr/bin/tor | awk '{print $3}'|grep --color=never "^/") $TORCHROOT/usr/lib/
cp -r /var/lib/tor      $TORCHROOT/var/lib/
chown -R tor:tor $TORCHROOT/var/lib/tor

sh -c "grep --color=never ^tor /etc/passwd > $TORCHROOT/etc/passwd"
sh -c "grep --color=never ^tor /etc/group > $TORCHROOT/etc/group"

mknod -m 644 $TORCHROOT/dev/random c 1 8
mknod -m 644 $TORCHROOT/dev/urandom c 1 9
mknod -m 666 $TORCHROOT/dev/null c 1 3

if [[ "$(uname -m)" == "x86_64" ]]; then
  cp /usr/lib/ld-linux-x86-64.so* $TORCHROOT/usr/lib/.
  ln -sr /usr/lib64 $TORCHROOT/lib64
  ln -s $TORCHROOT/usr/lib ${TORCHROOT}/usr/lib64
fi

```

Luego de correr el script como root, Tor puede ser ejecutado en [chroot](/index.php/Chroot "Chroot") con el comando:

```
# chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor

```

o si utiliza systemd recargue el servicio:

 `/etc/systemd/system/tor.service.d/chroot.conf` 
```
[Service]
User=root
ExecStart=
ExecStart=/usr/bin/sh -c "chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor -f /etc/tor/torrc"
KillSignal=SIGINT

```

## Corriendo Tor en un contenedor systemd-nspawn con una interfaz de red virtual

En este ejemplo crearemos un contenedor [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") llamado `tor-exit` con una interfaz de red virtual macvlan.

Vea [Systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") y [systemd-networkd](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") para documentación completa.

### Instalación y Configuración del Servidor

En este ejemplo el contenedor se alojará en `/srv/container`:

```
# mkdir /srv/container/tor-exit

```

[Instalar](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Instale [base](https://www.archlinux.org/groups/x86_64/base/), [tor](https://www.archlinux.org/packages/?name=tor) y [arm](https://www.archlinux.org/packages/?name=arm) y deselecione [linux](https://www.archlinux.org/packages/?name=linux) como en [Systemd-nspawn#Create and boot a minimal Arch Linux distribution in a container](/index.php/Systemd-nspawn#Create_and_boot_a_minimal_Arch_Linux_distribution_in_a_container "Systemd-nspawn") (en inglés):

```
# pacstrap -i -c -d /srv/container/tor-exit base tor arm

```

Cree el directorio si no existe:

```
# mkdir /var/lib/container

```

**Nota:** Los Symlinks para `nspawn` actualmente están dañados (como en 2016-02-04; vea [https://github.com/systemd/systemd/issues/2001](https://github.com/systemd/systemd/issues/2001)), y recibirá el error "too many levels of symlinks". Como una (posiblemente insegura) solución, simplemente "pacstrap" su instalación en el directorio contenedor.

Symlink al registro del contenedor del servidor, como en [Systemd-nspawn#Enable container on boot](/index.php/Systemd-nspawn#Enable_container_on_boot "Systemd-nspawn")(en inglés):

```
# ln -s /srv/container/tor-exit /var/lib/container/tor-exit

```

#### Interfaz de red virtual

Crea un directorio de Deposito para el servicio de contenedor:

```
# mkdir /etc/systemd/system/systemd-nspawn@tor-exit.service.d

```
 `/etc/systemd/system/systemd-nspawn@tor-exit.service.d/tor-exit.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/systemd-nspawn --quiet --keep-unit --boot --link-journal=guest --network-macvlan=$INTERFACE --private-network --directory=/var/lib/container/%i
LimitNOFILE=32768

```

`--network-macvlan=$INTERFACE --private-network` crea automáticamente un macvlan llamado `mv-$INTERFACE` dentro del contenedor, el cual no es visible desde el servidor. `--private-network` está implícito por `--network-macvlan=` de acuerdo con [systemd-nspawn(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1). Esto es aconsejable por seguridad ya que le permitirá dar una IP privada al contenedor, y no conocerá la IP de su máquina. Esto ayudará a esconder pedidos de DNS.

`LimitNOFILE=32768` por [#Raise maximum number of open file descriptors](#Raise_maximum_number_of_open_file_descriptors).

Ponga a punto [systemd-networkd](/index.php/Systemd-networkd_(Espa%C3%B1ol) "Systemd-networkd (Español)") de acuerdo con su red en `/srv/container/tor-exit/etc/systemd/network/mv-$INTERFACE.network`.