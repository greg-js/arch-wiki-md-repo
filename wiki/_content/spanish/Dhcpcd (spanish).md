Artículos relacionados

*   [Network configuration (Español)](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)")
*   [Wireless network configuration (Español)](/index.php/Wireless_network_configuration_(Espa%C3%B1ol) "Wireless network configuration (Español)")
*   [dhcpd](/index.php/Dhcpd "Dhcpd")

*dhcpcd* es un cliente DHCP y DHCPv6\. Actualmente es el cliente DHCP de código abierto que más características tiene, vea su [página](https://roy.marples.name/projects/dhcpcd) para una lista completa de características.

**Nota:** *dhcpcd* (DHCP **client** daemon) no es lo mismo que [dhcpd](/index.php/Dhcpd "Dhcpd") (DHCP **(server)** daemon).

## Contents

*   [1 Instalación](#Instalación)
*   [2 Iniciar](#Iniciar)
*   [3 Configuración](#Configuración)
    *   [3.1 Ruta(s) estática DHCP](#Ruta(s)_estática_DHCP)
    *   [3.2 Identificador de cliente DHCP](#Identificador_de_cliente_DHCP)
    *   [3.3 Perfil estático](#Perfil_estático)
        *   [3.3.1 Volver al perfil anterior](#Volver_al_perfil_anterior)
*   [4 Hooks](#Hooks)
    *   [4.1 10-wpa_supplicant](#10-wpa_supplicant)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Acelerar DHCP deshabilitando la exploración ARP](#Acelerar_DHCP_deshabilitando_la_exploración_ARP)
    *   [5.2 Remove old DHCP lease](#Remove_old_DHCP_lease)
    *   [5.3 Different IPs when multi-booting](#Different_IPs_when_multi-booting)
    *   [5.4 resolv.conf](#resolv.conf)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Client ID](#Client_ID)
    *   [6.2 Check DHCP problem by releasing IP first](#Check_DHCP_problem_by_releasing_IP_first)
    *   [6.3 Problems with noncompliant routers](#Problems_with_noncompliant_routers)
    *   [6.4 dhcpcd y interfaces de red con systemd](#dhcpcd_y_interfaces_de_red_con_systemd)
    *   [6.5 Timeout delay](#Timeout_delay)
*   [7 Known issues](#Known_issues)
    *   [7.1 dhcpcd@.service causes slow startup](#dhcpcd@.service_causes_slow_startup)
*   [8 See also](#See_also)

## Instalación

El paquete [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) es parte del grupo [base](https://www.archlinux.org/groups/x86_64/base/), por lo tanto ya esta [instalado](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") en su sistema.

[dhcpcd-ui](https://aur.archlinux.org/packages/dhcpcd-ui/) es una interfaz [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)") del demonio *dhcpcd*, y opcionalmente [WPA supplicant](/index.php/WPA_supplicant_(Espa%C3%B1ol) "WPA supplicant (Español)"). Estas interfaces ofrecen un diálogo de configuración y la capacidad de introducir una contraseña para las redes inalámbricas.

[dhcpcd-ui-patched](https://aur.archlinux.org/packages/dhcpcd-ui-patched/) es una versión parcheada del paquete [dhcpcd-ui](https://aur.archlinux.org/packages/dhcpcd-ui/). Esta utiliza AppIndicator en vez de GtkStatusIcon y compila con gtk3\. Posee un icono nítido para la bandeja del sistema cuando se utiliza con [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)").

## Iniciar

Para iniciar el demonio para *todas* las interfaces red, [Inicia/Activa](/index.php/Start/enable_(Espa%C3%B1ol) "Start/enable (Español)") `dhcpcd.service`.

Para iniciar el demonio para solo una interfaz específica de red, [Inicia/Activa](/index.php/Start/enable_(Espa%C3%B1ol) "Start/enable (Español)") `dhcpcd@*interfaz*.service`, donde *interfaz* se puede encontrar con [Configuración de red #Listar dispositivos](/index.php/Network_configuration_(Espa%C3%B1ol)#Nombres_de_los_dispositivos "Network configuration (Español)").

Es recomendable utilizar la unidad de la plantilla, vea [#dhcpcd y interfaces de red con systemd](#dhcpcd_y_interfaces_de_red_con_systemd) para más detalles.

Otra forma es iniciar *dhcpcd* manualmente, ejecute el siguiente comando:

```
# dhcpcd *interfaz*

```

En todo lo de arriba, le será asignado una dirección IP dinámica. Para establecer una dirección IP estática, vea [#Perfil estático](#Perfil_estático).

## Configuración

La configuración principal se hace en `/etc/dhcpcd.conf`. Vea [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5) para más detalles. Algunas de las opciones frecuentemente utilizadas están resaltadas abajo.

### Ruta(s) estática DHCP

Si necesita añadir una ruta estática en el lado del cliente, añádelo a `/etc/dhcpcd.exit-hook`. En el ejemplo se observa un hook-script nuevo que añade una ruta estática a una subred VPN en `10.11.12.0/24` via a la puerta de entrada de la maquina a `192.168.192.5`:

 `/etc/dhcpcd.exit-hook` 
```
ip route add 10.11.12.0/24 via 192.168.192.5

```

Puedes añadir múltiples rutas en este archivo.

### Identificador de cliente DHCP

El cliente DHCP puede identificarse de diferentes formas por el servidor:

1.  hostname (o el valor del nombre del host enviado por el cliente),
2.  por la dirección MAC del controlador de la interfaz de red con la que se está realizando la conexión, vinculado al
3.  ID de Asociación de Identidad (IAID), que es una capa de abstracción para diferenciar usos/casos y/o interfaces en un solo host,
4.  Identificador único de DHCP (DUID).

Para una descripción más extensa, vea [RFC 3315](https://tools.ietf.org/html/rfc3315#section-4.2).

Dependiendo de la configuración del servidor DHCP algunas opciones serán opcionales u obligatorias para solicitar una concesión de IP a DHCP.

**Nota:** La configuración por defecto de *dhcpcd* debería ser suficiente. La lista de identificadores son determinados automáticamente y solo se requiere cambiar la configuración manualmente en caso de experimentar problemas.

Si la configuración por defecto de *dhcpcd* falla al obtener una IP, las siguientes opciones están disponibles para usarse en `dhcpcd.conf`:

*   `hostname` envia el nombre del host establecido en `/etc/hostname`
*   `clientid` envia la dirección MAC como identificador
*   `iaid <interface>` deriva el IAID para utilizarlo en el detector DHCP. Se tiene que utilizar en un block de la interfaz (iniciada por `interface <interface>`, vea [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1388376#p1388376)), pero normalmente se utiliza la siguiente opción:
*   El disparador `duid` utiliza una combinación de DUID y IAID como identificador.

El valor DUID esta establecido en `/var/lib/dhcpcd/duid`. Para la eficiencia en la operación de concesión DHCP es importante que sea único para el sistema y se aplique a todas las interfaces de red iguales, mientras el IAID representa un identificador para cada interfaz del sistema (vea [RFC 4361](https://tools.ietf.org/html/rfc4361#section-6.1)).

Tenga mucho cuidado en una red en funcionamiento con [DNS dinámicos](https://en.wikipedia.org/wiki/Dynamic_DNS "wikipedia:Dynamic DNS") en asegurarse de que los tres IDs son únicos. Si se presenta valores duplicados DUID en el servidor DNS, por ejemplo, en el caso donde una máquina virtual ha sido clonada y el nombre del host y la MAC se han hecho únicos pero el DUID no se ha cambiado, cada cliente con el DUID duplicado requiere que el servidor elimine el predecesor del registro DNS.

### Perfil estático

Los ajustes necesarios están explicados en [Configuración de red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)"). Normalmente incluye el nombre de la [interfaz de red](/index.php/Network_configuration_(Espa%C3%B1ol)#Interfaces_de_red "Network configuration (Español)"), *dirección IP*, *dirección del router*, y el *nombre del servidor*.

El perfil estático para *dhcpcd* se configura en `/etc/dhcpcd.conf`, por ejemplo:

 `/etc/dhcpcd.conf` 
```
interface eth0
static ip_address=192.168.0.10/24	
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8.8
```

Es posible realizar configuraciones más complicadas, por ejemplo combinar con la opción `arping`. Vea [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5) para más información.

#### Volver al perfil anterior

Es posible configurar un perfil estático dentro de *dhcpcd* y regresar al perfil anterior cuando el requerimiento de DHCP falle. Esto es particularmente útil para [máquinas sin monitor (en inglés)](https://en.wikipedia.org/wiki/Headless_computer "wikipedia:Headless computer"), donde el perfil estático se puede utilizar como un perfil de "recuperación" para asegurarse de que siempre sea posible conectarse a la máquina.

El siguiente ejemplo configura un perfil `estático_eth0` con `192.168.1.23` como dirección IP, `192.168.1.1` como puerta y nombre de servidor, y hace que este perfil sea un respaldo para la interfaz `eth0`.

 `/etc/dhcpcd.conf` 
```
# define un perfil estático
profile static_eth0
static ip_address=192.168.1.23/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1

# respaldo para el perfil estático en eth0
interface *eth0*
fallback static_eth0
```

## Hooks

*dhcpcd* ejecuta todos los scripts que encuentra en `/usr/lib/dhcpcd/dhcpcd-hooks/` en un orden léxico. Vea [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5) y [dhcpcd-run-hooks(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd-run-hooks.8) para más información.

**Nota:**

*   Cada script puede desactivarse utilizando la opción `nohook` en `dhcpcd.conf`.
*   La opción `env` se puede utilizar para establecer una variable de entorno para **todos** los hooks. Por ejemplo, puedes forzar el que el hook hostname siempre establezca en nombre del host con `env force_hostname=YES`.

### 10-wpa_supplicant

Activar este hook creando un enlace simbólico (para asegurarse de que siempre se utilice la versión actual, incluso despues de actualizaciones):

```
# ln -s /usr/share/dhcpcd/hooks/10-wpa_supplicant /usr/lib/dhcpcd/dhcpcd-hooks/

```

El hook `10-wpa_supplicant`, si esta activado, ejecuta automáticamente [WPA supplicant (Español)](/index.php/WPA_supplicant_(Espa%C3%B1ol) "WPA supplicant (Español)") en las interfaces de red inalámbricas. Se inicia solo si:

*   Ningún proceso *wpa_supplicant* esta escuchando a esa interfaz.
*   existe un archivo de configuración *wpa_supplicant*. *dhcpcd* comprueba

```
/etc/wpa_supplicant/wpa_supplicant-*interface*.conf
/etc/wpa_supplicant/wpa_supplicant.conf
/etc/wpa_supplicant-*interface*.conf
/etc/wpa_supplicant.conf

```

por defecto, y en ese orden, pero se puede configurar un parche personalizado añadiendo `env wpa_supplicant_conf=*archivo_de_configuración_del_parche*` en `/etc/dhcpcd.conf`.

**Nota:** El hook se para cuando encuentra el primer archivo de configuración, por lo tanto ha de tenerlo en cuenta si usted tiene bastantes archivos de configuración *wpa_supplicant*, de otra forma puede que al final *dhcpcd* utilice el archivo incorrecto.

Si *wpa_supplicant* maneja conexiones inalámbricas por si mismo, el hook puede crear eventos de conexiones no deseadas. Por ejemplo, si para *wpa_supplicant* el hook puede iniciar la interfaz otra vez. Incluso si utiliza [netctl-auto (en inglés)](/index.php/Netctl#Special_systemd_units "Netctl"), *wpa_supplicant* se inicia automáticamente con `/run/network/wpa_supplicant_*interface*.conf` por la configuración, por lo tanto iniciarlo otra vez desde el hook no es necesario y puede causar errores en el booteo al analizar el archivo `/etc/wpa_supplicant/wpa_supplicant.conf`, que solo contiene valores ficticios en la versión por defecto.

Para desactivar el hook, añade `nohook wpa_supplicant` en `dhcpcd.conf`.

## Consejos y trucos

### Acelerar DHCP deshabilitando la exploración ARP

*Dhcpcd* contiene una implementación como recomendación del estándar DHCP ([RFC2131](https://www.ietf.org/rfc/rfc2131.txt) sección 2.2) para comprobar vía ARP si la dirección IP asignada no esta realmente ocupada. Esto puede no ser útil en las redes domésticas, por lo tanto se puede ahorrar alrededor de 5 segundos en cada conexión añadiendo la siguiente linea a `/etc/dhcpcd.conf`:

```
noarp

```

Esto es equivalente si le pasa `--noarp` a `dhcpcd`, y desactiva la prueba ARP descrita, aumentando la velocidad de la conexiones a redes con DHCP.

### Remove old DHCP lease

The file `/var/lib/dhcpcd/*interface*.lease`, where `*interface*` is the name of the interface on which you have a lease, contains the actual DHCP lease reply sent by the DHCP server. For a wireless interface, the filename is `/var/lib/dhcpcd/*interface*-*ssid*.lease`, where `*ssid*` is the name of the wireless network. It is used to determine the last lease from the server, and its `mtime` attribute is used to determine when it was issued. This last lease information is then used to request the same IP address previously held on a network, if it is available. If you do not want that, simply delete this file.

If the DHCP server still assigns the same IP address, this may happen because it is configured to keep the assignment stable and recognizes the requesting DHCP client id or DUID (see [#DHCP Client Identifier](#DHCP_Client_Identifier)). You can test it by stopping *dhcpcd* and removing or renaming `/var/lib/dhcpcd/duid`. *dhcpcd* will generate a new one on next run.

Keep in mind that the DUID is intended as persistent machine identifier across reboots and interfaces. If you are transferring the system to new computer, preserving this file should make it appear as old one.

### Different IPs when multi-booting

If you are dualbooting Arch and OS X or Windows and want each to receive different IP addresses, you can exert control about the IPs leased by specifying a different DUID in each operating system installation.

In Windows (post XP) the DUID should be stored in the

```
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\Dhcpv6DUID 

```

registry key.

On OS X it is directly accessible in `Network\adapter\dhcp preferences panel`.

If you are using a [dnsmasq](/index.php/Dnsmasq "Dnsmasq") DHCP server, the different DUIDs can be used in appropriate `dhcp-host=` rules in its configuration.

### resolv.conf

*dhcpcd'* by default overwrites [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

This can be stopped by adding the following to the last section of `/etc/dhcpcd.conf`:

```
nohook resolv.conf

```

Alternatively, you can create a file called `/etc/resolv.conf.head` containing your DNS servers. *dhcpcd* will prepend this file to the beginning of `/etc/resolv.conf`.

Or you can configure dhcpcd to use the same DNS servers every time. To do this, add the following line at the end of your `/etc/dhcpcd.conf`, where `*dns-server-ip-addressses*` is a space separated list of DNS IP addresses.

```
static domain_name_servers=*dns-server-ip-addresses*

```

For example, to set it to Google's DNS servers:

```
static domain_name_servers=8.8.8.8 8.8.4.4

```

## Troubleshooting

### Client ID

If you are on a network with DHCPv4 that filters Client IDs based on MAC addresses, you may need to change the following line:

 `/etc/dhcpcd.conf` 
```
# Use the same DUID + IAID as set in DHCPv6 for DHCPv4 Client ID as per RFC4361\. 
duid

```

To:

 `/etc/dhcpcd.conf` 
```
# Use the hardware address of the interface for the Client ID (DHCPv4).
clientid

```

Else, you may not obtain a lease since the DHCP server may not read your [DHCPv6-style](https://en.wikipedia.org/wiki/DHCPv6 "wikipedia:DHCPv6") Client ID correctly. See [RFC 4361](https://tools.ietf.org/html/rfc4361) for more information.

### Check DHCP problem by releasing IP first

A problem may occur when DHCP gets a wrong IP assignment, such as when two routers are tied together through a VPN. The router that is connected through the VPN may be assigning IP address. To fix it, as root, release the IP address:

```
# dhcpcd -k

```

Then request a new one:

```
# dhcpcd

```

You may have to run those two commands many times.

### Problems with noncompliant routers

For some (noncompliant) routers, you will not be able to connect properly unless you comment the line

```
require dhcp_server_identifier

```

in `/etc/dhcpcd.conf`. This should not cause issues unless you have multiple DHCP servers on your network (not typical); see [this page](https://technet.microsoft.com/en-us/library/cc977442.aspx) for more information.

### dhcpcd y interfaces de red con systemd

`dhcpcd.service` can be [enabled](/index.php/Enabled "Enabled") without specifying an interface. This may, however, create a race condition at boot with *systemd-udevd* trying to apply a predictable network interface name:

```
error changing net interface name wlan0 to wlp4s0: Device or resource busy" 

```

To avoid it, enable *dhcpcd* per interface it should bind to as described in [#Running](#Running). The downside of the template unit is, however, that it does not support hot-plugging of a wired connection and will fail if the network cable is not connected. To work-around the failure, see [#Timeout delay](#Timeout_delay).

It is also possible to use `denyinterfaces` or `allowinterfaces` in [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5) to stop dhcpcd from binding to kernel names, for example

```
denyinterfaces wlan* eth*

```

### Timeout delay

If *dhcpcd* operates on a single interface and fails to obtain a lease after 30 seconds (for example when the server is not ready or the cable not plugged), it will exit with an error.

To have *dhcpcd* wait indefinitely for one-time, [edit](/index.php/Edit "Edit") the unit and set the `timeout` option to `0`:

 `/etc/systemd/system/dhcpcd@.service.d/timeout.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dhcpcd -w -q **-t 0** %I
```

To have it wait indefinitely, let the unit restart after it exited:

 `/etc/systemd/system/dhcpcd@.service.d/dhcpcdrestart.conf` 
```
[Service]
Restart=always
```

## Known issues

### dhcpcd@.service causes slow startup

By default the `dhcpcd@.service` waits to get an IP address before forking into the background via the `-w` flag for *dhcpcd*. If the unit is enabled, this may cause the boot to wait for an IP address before continuing. To fix this, create a [drop-in file](/index.php/Systemd#Drop-in_files "Systemd") for the unit with the following:

 `/etc/systemd/system/dhcpcd@.service.d/no-wait.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dhcpcd -b -q %I
```

See also [FS#49685](https://bugs.archlinux.org/task/49685).

## See also

*   [dhcpcd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.8)
*   [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5)