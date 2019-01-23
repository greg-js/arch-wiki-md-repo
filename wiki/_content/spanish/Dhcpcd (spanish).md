**Estado de la traducción**
Este artículo es una traducción de [dhcpcd](/index.php/Dhcpcd "Dhcpcd"), revisada por última vez el **2019-1-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dhcpcd&diff=0&oldid=562094) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

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
    *   [5.2 Quitar el arrendamiento antiguo de DHCP](#Quitar_el_arrendamiento_antiguo_de_DHCP)
    *   [5.3 Diferentes IPs cuando se multi-bootea](#Diferentes_IPs_cuando_se_multi-bootea)
    *   [5.4 resolv.conf](#resolv.conf)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 ID del cliente](#ID_del_cliente)
    *   [6.2 Comprobar un problema de DHCP soltando primero la IP](#Comprobar_un_problema_de_DHCP_soltando_primero_la_IP)
    *   [6.3 Problemas con routers no obedientes](#Problemas_con_routers_no_obedientes)
    *   [6.4 dhcpcd y interfaces de red con systemd](#dhcpcd_y_interfaces_de_red_con_systemd)
    *   [6.5 Tiempo de espera](#Tiempo_de_espera)
*   [7 Problemas conocidos](#Problemas_conocidos)
    *   [7.1 dhcpcd@.service causa un inicio lento](#dhcpcd@.service_causa_un_inicio_lento)
*   [8 Véase también](#Véase_también)

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

### Quitar el arrendamiento antiguo de DHCP

El archivo `/var/lib/dhcpcd/*interfaz*.lease`, donde `*interfaz*` es el nombre de la interfaz que tiene el arrendamiento, contiene la respuesta enviada por el servidor DHCP del actual arrendamiento de DHCP. Para una interfaz inalámbrica, el nombre del archivo es `/var/lib/dhcpcd/*interfaz*-*ssid*.lease`, donde `*ssid*` es el nombre de la red inalámbrica. Se usa para determinar el último arrendamiento del servidor, y su atributo `mtime` se usa para determinar cuando se ha resuelto. La última información de arrendamiento se usa para pedir la misma dirección IP previamente retenida en la red, si está disponible. Si no quiere eso, simplemente elimine este archivo.

Si el servidor DHCP aún le asigna la misma dirección IP, puede deberse a que está configurado para mantener la asignación estable y reconoce el requerimiento del id del cliente DHCP o DUID (vea [#Identificador de cliente DHCP](#Identificador_de_cliente_DHCP)). Puedes probarlo parando *dhcpcd* y eliminando o renombrando `/var/lib/dhcpcd/duid`. *Dhcpcd* generará uno nuevo en la siguiente ejecución.

Tenga en cuenta que el DUID está destinado a ser un identificador persistente sobre los reinicios e interfaces. Si estás transfiriendo el sistema a un nuevo ordenador, preservar este archivo debería hacer que el ordenador se parezca al antiguo.

### Diferentes IPs cuando se multi-bootea

Si está dualbooteando Arch y OS X o Windows y quiere que cada uno reciba direcciones IP distintas, puedes ejercer control sobre el arrendamiento de IPs especificando un DUID diferente para cada sistema operativo.

En Windows (en XP) el DUID debería estar guardado en

```
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\Dhcpv6DUID 

```

registro clave.

En OS X es directamente accesible en `Network\adapter\dhcp preferences panel`.

Si está utilizando un servidor [dnsmasq](/index.php/Dnsmasq_(Espa%C3%B1ol) "Dnsmasq (Español)") DHCP, los DUIDs diferentes pueden utilizar las reglas apropiadas `dhcp-host=` en su cpnfiguración.

### resolv.conf

*dhcpcd'* por defecto sobrescribe [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

Se puede parar añadiendo lo siguiente a la última sección de `/etc/dhcpcd.conf`:

```
nohook resolv.conf

```

Alternativamente, puede crear un archivo llamado `/etc/resolv.conf.head` conteniendo sus servidores DNS. *Dhcpcd* antepone este archivo al comienzo de `/etc/resolv.conf`.

O puede configurar dhcpcd para utilizar el mismo servidor DNS siempre. Para hacer esto, añade la siguiente linea al final de su `/etc/dhcpcd.conf`, donde `*dns-server-ip-addressses*` es una lista deparada por espacios de las direcciones IP DNS.

```
static domain_name_servers=*dns-server-ip-addresses*

```

Por ejemplo, para establecer el servidor DNS de Google:

```
static domain_name_servers=8.8.8.8 8.8.4.4

```

## Solución de problemas

### ID del cliente

Si está en una red con DHCPv4 If you are on a network with DHCPv4 que filtra las IDs de los clientes basados en direcciones MAC, necesita cambiar la siguiente linea:

 `/etc/dhcpcd.conf` 
```
# Use el mismo DUID + IAID como se establece en DHCPv6 para el ID del cliente DHCPv4 igual que RFC4361\. 
duid

```

A:

 `/etc/dhcpcd.conf` 
```
# Utilice la dirección de la interfaz del hardware para el ID del cliente (DHCPv4).
clientid

```

Si no, puede no obtener ningún arrendamiento desde que el servidor DHCP no lea su ID del cliente [estilo-DHCPv6](https://en.wikipedia.org/wiki/es:DHCPv6 "wikipedia:es:DHCPv6") correctamente. Vea [RFC 4361](https://tools.ietf.org/html/rfc4361) para más información.

### Comprobar un problema de DHCP soltando primero la IP

Puede ocurrir un problema cuando DHCP obtiene una asignación IP incorrecta, como que dos routers están enlazados juntos a una VPN. El router que está conectado a través de la VPN puede haber asignado una dirección IP. Para arreglarlo, como root, suelte la dirección IP:

```
# dhcpcd -k

```

Luego pida una nueva:

```
# dhcpcd

```

Puede que tengas que ejecutar estos dos comandos varias veces.

### Problemas con routers no obedientes

Para algunos routers (desobedientes), no podrá conectarse apropiadamente a no haya ser que comentes la linea

```
require dhcp_server_identifier

```

en `/etc/dhcpcd.conf`. Esto no debería causarle problemas a no ser que tenga múltiples servidores DHCP en su red (no es típico); vea [esta página](https://technet.microsoft.com/en-us/library/cc977442.aspx) para más información.

### dhcpcd y interfaces de red con systemd

`dhcpcd.service` puede [activarse](/index.php?title=Activarse&action=edit&redlink=1 "Activarse (page does not exist)") sin especificar una interfaz. Esto puede, sin embargo, crear una condición en el booteo intentando aplicar un nombre predictivo de la interfaz de red con *system-udev*:

```
error changing net interface name wlan0 to wlp4s0: Device or resource busy" 

```

Para evitarlo, habilita *dhcpcd* por interfaz que debería enlazar como se ha descrito en [#Iniciar](#Iniciar). La plantilla de abajo, sin embargo, no soporta la conexión en caliente de una conexión por cable y fallará si el cable de red no está conectado. Para tratar el fallo, vea [#Tiempo de espera](#Tiempo_de_espera).

También es posible utilizar `denyinterfaces` o `allowinterfaces` en [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5) para parar dhcpcd vinculando a los nombres del kernel, por ejemplo

```
denyinterfaces wlan* eth*

```

### Tiempo de espera

Si *dhcpcd* opera en una única interfaz y falla al obtener el arrendamiento (lease time) después de 30 segundos (por ejemplo cuando el servidor no está preparado o el cable no está conectado), saldrá con un error.

Para hacer que *dhcpcd* espere indefinidamente por una vez, [edite](/index.php/Edite "Edite") la unidad y establece la opción `timeout` a `0`:

 `/etc/systemd/system/dhcpcd@.service.d/timeout.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dhcpcd -w -q **-t 0** %I
```

Para hacer que espere indefinidamente, deja que la unidad se reinicie después de salir:

 `/etc/systemd/system/dhcpcd@.service.d/dhcpcdrestart.conf` 
```
[Service]
Restart=always
```

## Problemas conocidos

### dhcpcd@.service causa un inicio lento

Por defecto `dhcpcd@.service` espera hasta obtener una dirección IP antes de pasar a segundo plano vía parámetro `-w` para *dhcpcd*. Si la unidad está habilitada, puede causar que en el arranque espere a obtener una dirección IP antes de continuar. Para arreglarlo, crea un [archivo de inserción](/index.php/Systemd_(Espa%C3%B1ol)#Archivos_insertados "Systemd (Español)") para la unidad con lo siguiente:

 `/etc/systemd/system/dhcpcd@.service.d/no-wait.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dhcpcd -b -q %I
```

Vea también [FS#49685](https://bugs.archlinux.org/task/49685).

## Véase también

*   [dhcpcd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.8)
*   [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5)