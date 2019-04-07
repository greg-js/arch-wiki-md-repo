Artículos relacionados

*   [Network Configuration (Español)](/index.php/Network_Configuration_(Espa%C3%B1ol) "Network Configuration (Español)")
*   [Wireless Setup (Español)](/index.php/Wireless_Setup_(Espa%C3%B1ol) "Wireless Setup (Español)")
*   [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)")
*   [Wicd (Español)](/index.php/Wicd_(Espa%C3%B1ol) "Wicd (Español)")
*   [Bridge with netctl](/index.php/Bridge_with_netctl "Bridge with netctl")

*netctl* es una herramienta basada en CLI (*«intérprete de línea de órdenes»*, esto es, a través de consola)) utilizada para configurar y gestionar las conexiones de red mediante perfiles. Es la apuesta de Arch Linux para sustituir a *netcfg*. *netctl* supone el futuro (y el presente) de la gestión de conexiones de red.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Bibliografía altamente recomendada](#Bibliografía_altamente_recomendada)
*   [3 Configuración](#Configuración)
    *   [3.1 Automatizar las conexiones](#Automatizar_las_conexiones)
        *   [3.1.1 Método básico](#Método_básico)
        *   [3.1.2 Cambio automático de perfiles](#Cambio_automático_de_perfiles)
    *   [3.2 Migración de netcfg a netctl](#Migración_de_netcfg_a_netctl)
    *   [3.3 Contraseñas encriptadas (PSK de 256-bits)](#Contraseñas_encriptadas_(PSK_de_256-bits))
*   [4 Consejos y trucos útiles](#Consejos_y_trucos_útiles)
    *   [4.1 Sustituir 'netcfg current'](#Sustituir_'netcfg_current')
    *   [4.2 Eduroam](#Eduroam)
    *   [4.3 Bonding](#Bonding)
        *   [4.3.1 Equilibrar la carga](#Equilibrar_la_carga)
        *   [4.3.2 Pasar a la conexión inalámbrica cuando la conexión cableada falla](#Pasar_a_la_conexión_inalámbrica_cuando_la_conexión_cableada_falla)
    *   [4.4 Quitar direcciones antiguas de dhcpcd](#Quitar_direcciones_antiguas_de_dhcpcd)
    *   [4.5 Problemas de espera con DHCP](#Problemas_de_espera_con_DHCP)
*   [5 Véase también](#Véase_también)

## Instalación

El paquete [netctl](https://www.archlinux.org/packages/?name=netctl) se puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") y está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). netctl sustituirá a [netcfg](https://aur.archlinux.org/packages/netcfg/) una vez se instale en el equipo.

[netctl](https://www.archlinux.org/packages/?name=netctl) y [netcfg](https://aur.archlinux.org/packages/netcfg/) son paquetes incompatibles y conflictivos. Si los perfiles de las conexiones de red no están correctamente configurados, lo más probable es que el usuario se quede sin conexión a internet después de instalar **netctl**.

**Nota:** Puede ser una buena idea usar `systemctl --type=service` para asegurarse de que ningún otro servicio de configuración de red está en ejecución. La presencia de varios servicios de gestión de redes entrarán en conflicto.

## Bibliografía altamente recomendada

Se ha puesto mucho empeño e interés en redactar unas páginas man muy completas. Se recomienda encarecidamente a los usuarios que estén interesados en usar netctl que lean las siguientes páginas man antes de lanzarse a probarlo:

*   [netctl](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.1.txt)
*   [netctl.profile](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt)
*   [netctl.special](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.special.7.txt)

## Configuración

El uso de `netctl` va dirigido a controlar y observar a fondo el estado de los servicios de systemd que gestionan los perfiles de las conexiones de red. El paquete incluye varios ficheros de configuración ejemplo para ayudar al usuario a la hora de configurar sus conexiones de red. Dichos ejemplos de ficheros de configuración de perfiles se encuentran en el directorio `/etc/netctl/examples/`. Entre las configuraciones más típicas se pueden encontrar las siguientes:

*   ethernet-dhcp
*   ethernet-static
*   wireless-wpa
*   wireless-wpa-static

Para usar un fichero ejemplo de un perfil de una conexión de red hay que copiar el fichero en cuestión de `/etc/netctl/examples/<nombre del perfil de conexión de red>` al directorio `/etc/netctl/<nombre del perfil de conexión de red>` y editarlo para configurarlo de acuerdo con las necesidades específicas de cada usuario:

```
# cp /etc/netctl/examples/wireless-wpa /etc/netctl/mi-wireless-wpa

```

**Sugerencia:** Para las configuraciones de las redes inalámbricas, utilice `wifi-menu -o` que creará un fichero de configuración en `/etc/netctl/`.

**Advertencia:** `wifi-menu -o` generará el fichero de perfil en `/etc/netctl/` con '-' en el nombre. Esto dará problemas con la configuración automática. Se recomienda cambiar el nombre del fichero.

Una vez que se ha creado el perfil de configuración para una conexión de red concreta hay que intentar establecer la conexión usando dicho perfil. Para ello:

```
# netctl start <nombre del perfil de la conexión de red>

```

**Nota:** El «perfil» es el nombre del fichero, sin incluir la ruta completa. Si se facilita la ruta completa, ello provocará que netctl devuelva un código de error.

En caso de obtener un error al ejecutar la orden anterior, es posible acceder a una explicación detallada de lo que ha provocado el fallo. Para ello se pueden usar las órdenes `journalctl -xn` y `netctl status <nombre del perfil de la conexión de red>`. Una vez que se ha encontrado el fallo tan solo hay que hacer las correcciones pertinentes en el perfil de la conexión de red y volver a intentarlo.

### Automatizar las conexiones

Si solo se está usando un perfil de conexión de red (por interfaz) o se desea cambiar de perfil manualmente, el [método básico](#Método_básico) es el acertado. Entre los ejemplos más comunes se encuentran los servidores, estaciones de trabajo, routers, etc.

Si se necesita cambiar entre varios perfiles con frecuencia, utilice el método del [cambio automático de perfiles](#Cambio_automático_de_perfiles). Los ejemplos más comunes son los ordenadores portátiles.

#### Método básico

Con este método, se puede comenzar un solo perfil con dirección estática por interfaz. Primero compruebe manualmente que el perfil se puede iniciar con éxito, y después actívelo usando la orden:

```
# netctl enable *nombre del perfil de la conexión de red*

```

Esto creará y activará un servicio de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), servicio que se iniciará cuando arranque el equipo. Los cambios en el fichero de este perfil no se transmitirán automáticamente a dicho fichero de servicio. Si se realizan cambios, es necesario volver a activar el perfil con la orden:

```
# netctl reenable *nombre del perfil de la conexión de red*

```

**Nota:** La conexión solo se establecerá si el perfil se puede iniciar con éxito en el arranque (o cuando se inicia el servicio). Esto significa concretamente, que, en el caso de una conexión por cable, el cable debe estar enchufado, y, en el caso de una conexión inalámbrica, la red debe estar dentro del rango.

**Sugerencia:** Para activar el perfil de la IP estática en la interfaz cableada, sin importar si el cable de red está o no conectado, pase la opción `SkipNoCarrier=yes` a su perfil.

#### Cambio automático de perfiles

*netctl* ofrece dos servicos especiales de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") para la conmutación automática de perfiles:

*   Para las interfaces cableadas: `netctl-ifplugd@*interfaz*.service`. El uso de estos perfiles de netctl se intercambian cuando se enchufa/desenchufa el cable de red.
*   Para las interfaces inalámbricas: `netctl-auto@*interfaz*.service`. El uso de estos perfiles de netctl se intercambian al pasar del rango de una red dentro del alcance de rango de otra red.

**Nota:** *netcfg* utiliza `net-auto-wireless.service` y `net-auto-wired.service` para estos fines.

Primero [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") los paquetes necesarios:

*   El paquete [wpa_actiond](https://aur.archlinux.org/packages/wpa_actiond/) es necesario para usar `netctl-auto@*interfaz*.service`.
*   El paquete [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) es necesario para usar `netctl-ifplugd@*interfaz*.service`.

Ahora configure todos los perfiles que `netctl-auto@*interfaz*.service` o `netctl-ifplugd@*interfaz*.service` desea que inicien.

Si algún perfil inalámbrico **no** se inicia automáticamente por `netctl-auto@*interfaz*.service`, tiene que agregar explícitamente la variable `ExcludeAuto=yes` para ese perfil. Puede utilizar la variable `Priority=` para establecer la prioridad de algún perfil cuando existen varios perfiles disponibles. `netctl-ifplugd@*interfaz*.service` preferirá perfiles que utilicen [DHCP](https://en.wikipedia.org/wiki/DHCP "wikipedia:DHCP"). Para preferir un perfil con una dirección IP estática, puede utilizar la variable `AutoWired=yes`. Consulte `netctl.profile(5)` para obtener más detalles.

**Advertencia:** La selección automática de un perfil compatible con WPA por *netctl-auto* no es posible con la opción `Security=wpa-config`, sino que hay que usar, en su lugar, la opción `Security=wpa-configsection`.

Una vez que ha establecido y comprobrado que sus perfiles funcionan correctamente, solo tiene que activar estos servicios utilizando *systemctl*:

```
# systemctl enable netctl-auto@*interfaz*.service 
# systemctl enable netctl-ifplugd@*interfaz*.service  

```

**Advertencia:**

*   Si alguno de los perfiles contienen errores, como por ejemplo, una variable `Key=` vacía, la unidad no se cargará durante el arranque.
*   Este método entra en conflicto con el [Método básico](#Método_básico). Si ha activado previamente un perfil a través de *netctl*, ejecute `netctl disable *profile*` para evitar que el perfil se cargue dos veces en el arranque.

Desde netctl 1.3, es posible controlar manualmente una interfaz gestionada de otra manera por netctl-auto sin tener que detener el servicio netctl-auto. Esto se hace usando la orden netctl-auto. Para obtener una lista de acciones disponibles basta con ejecutar:

```
 # netctl-auto --help

```

### Migración de netcfg a netctl

*netctl* se vale del directorio `/etc/netctl` para almacenar los distintos perfiles de las conexiones de red **en lugar de** `/etc/network.d`, (el cual era el directorio en el cual *netcfg* almacenaba los perfiles de las conexiones de red).

Para migrar de netcfg a *netctl* es necesario, al menos, lo siguiente:

*   Desactivar el servicio netcfg: `systemctl disable netcfg.service`.
*   Desinstalar *netcfg* e instalar *netctl*.
*   Mover los perfiles de las conexiones de red al nuevo directorio.
*   Renombrar las variables de dichos ficheros perfil de conexiones de red de acuerdo con las instrucciones en `netctl.profile(5)`. La gran mayoría tan solo han pasado de tener todo en letras mayúsculas a tener solo la primera letra. Un ejemplo: `CONNECTION` pasa a ser `Connection`.
*   Para la configuración de la IP estática asegúrese de que las variables `Address` tienen una máscara de red después de la IP (por ejemplo, `Address=('192.168.1.23**/24'** '192.168.1.87**/24'**)` en el perfil de ejemplo).
*   Si configura un perfil para una red inalámbrica siguiendo el ejemplo de `wireless-wpa-configsection`, tenga en cuenta que ello sobrescribe las opciones de `wpa_supplicant` definidas antes de los corchetes. Para una conexión a una red inalámbrica oculta, agregue `scan_ssid=1` a las opciones en `wireless-wpa-configsection`; `Hidden=yes` si no funciona allí.
*   Quitar las comillas de las variables de las distintas interfaces y otras variables que no necesitan de forma estricta las comillas. Esto no es más que una cuestión de estilo.
*   Ejecutar `netctl enable *nombre del perfil de la conexión de red*` para cada uno de los perfiles de conexión de red en la antigua línea `NETWORKS`. *«last»* ya no tiene la función que tenía. Para más infomación leer `netctl.special(7)`.
*   Usar `netctl list` y/o `netctl start <nombre del perfil de la conexión de red>`, en lugar de *netcfg-menu*. No obstante, *wifi-menu* seguirá disponible.
*   A diferencia de `netcfg`, `netctl`, por defecto, no levanta un [NIC](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller") cuando este no está conectado a otro NIC potencialmente abierto. Para resolver este problema, añada `SkipNoCarrier=yes` al final del fichero de perfil `/etc/netctl/*fichero-de-perfil*`.

### Contraseñas encriptadas (PSK de 256-bits)

**Nota:** Aunque «cifrada», la clave que se pone en la configuración del perfil es suficiente para conectarse a una red WPA-PSK, lo que significa que este procedimiento solo sirve para ocultar la versión legible de la frase de contraseña o passphrase, pero no evita que cualquier usuario con permisos de lectura acceda a este fichero para conectarse a la red. Debemos preguntarnos si hay alguna utilidad en este procedimiento, ya que usar la misma contraseña para todo suele ser una medida de seguridad muy pobre.

Los usuarios que **no** quieran tener sus contraseñas guardadas en *texto plano* tienen la posibilidad de generar una clave precompartida o PSK —del inglés, *Pre-Shared Key*— con encriptación de 256-bits, que se calcula a partir de la frase de contraseña («passphrase») y el nombre de la red («SSID») utilizando algoritmos estándar.

*   Método 1: Utilice `wifi-menu -o` para crear un fichero de configuración en la carpeta `/etc/netctl`.
*   Método 2: Configuración manual como sigue.

Para ambos métodos es recomendable el uso de la orden `chmod 600 /etc/netctl/<config_file>`, a fin de evitar el acceso a la contraseña por parte de otros usuarios.

A continuación, se generará la PSK con encriptación de 256-bits usando [wpa_passphrase](/index.php/WPA_supplicant#Configuration "WPA supplicant"):

 `$ wpa_passphrase *your_essid* *passphrase*` 
```
network={
  ssid="*your_essid*"
  #psk="*passphrase*"
  psk=64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
}
```

**Nota:** Esta información será utilizada en su perfil para que no cierre el terminal.

En otra consola, copiar el fichero ejemplo de perfil de conexión de red `wireless-wpa` de `/etc/netctl/examples` al directorio `/etc/netctl`.

```
# cp /etc/netctl/examples/wireless-wpa /etc/netctl/wireless-wpa

```

Será necesario editar el fichero `/etc/netctl/wireless-wpa` con el editor de texto que prefiera el usuario y añadir la clave precompartida encriptada o *Encrypted Pre-shared Key* que se ha generado previamente con wpa_passphrase a la variable `Key` del perfil de conexión de red.

Una vez terminada la edición del perfil de conexión de red `wireless-wpa` que contiene la PSK con encriptación de 256-bits, debería quedar algo así:

 `/etc/netctl/wireless-wpa` 
```
Description='A simple WPA encrypted wireless connection using 256-bit PSK'
Interface=wlp2s2
Connection=wireless
Security=wpa
IP=dhcp
ESSID=*your_essid*
Key=\"64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
```

**Nota:**

*   Hay que asegurarse de usar las directrices especiales sin entrecomillar o **special quoted rules** para la variable `Key=` como se explica al final de la página man [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt).
*   Si la contraseña no funciona, pruebe eliminar el signo `\"` en la variable `Key`.

## Consejos y trucos útiles

### Sustituir 'netcfg current'

Si ha utilizado `netcfg current` en el pasado, puede utilizar `# netctl-auto current` como un reemplazo para las conexiones iniciadas con `netctl-auto` (funcional desde netctl-1.3).

Para analizar manualmente las conexiones, también se puede utilizar:

```
# netctl list | awk '/*/ {print $2}'

```

### Eduroam

Algunas universidades utilizan un sistema llamado «Eduroam» para la gestión de sus redes inalámbricas. Para este sistema, un perfil de WPA config-section con el siguiente formato suele ser útil:

 `/etc/netctl/wlan0-eduroam` 
```
Description='Eduroam-profile for <user>'
Interface=wlan0
Connection=wireless
Security=wpa-configsection
IP=dhcp
WPAConfigSection=(
 'ssid="eduroam"'
 'proto=RSN'
 'key_mgmt=WPA-EAP'
 'pairwise=CCMP'
 'auth_alg=OPEN'
 'eap=PEAP'
 'identity="<user>"'
 'password="<password>"'
)

```

**Sugerencia:** Para evitar el almacenamiento de la contraseña en texto plano, puede generar un algoritmo para la contraseña con `$ echo -n <password> | iconv -t utf16le | openssl md4`. Después utilícelo como `'password=hash:<hash>'`.

Para perfiles TTLS y universidades certificadas esta configuración funciona:

 `/etc/netctl/wlan0-eduroam` 
```
Description='Eduroam university'
Interface=wlan0 
Connection=wireless
Security=wpa-configsection
IP=dhcp
ESSID=eduroam
WPAConfigSection=(
    'ssid="eduroam"'
    'key_mgmt=WPA-EAP'
    'eap=TTLS'
    'group=TKIP'
    'anonymous_identity="anonymous@domain_university"'
    'identity="XXX@domain_university"'
    'password="XXX"'
    'ca_cert="Path/to/the/certificate"'
    'phase2="auth=PAP"'
)

```

### Bonding

De [kernel documentation](https://www.kernel.org/doc/Documentation/networking/bonding.txt):

	*El controlador bonding de Linux proporciona un método para agregar múltiples interfaces de red en una sola interfaz lógica «vinculada». El comportamiento de la interfaz* bonded *depende de la modalidad. En términos generales, las modalidades proporcionan tanto una espera activa como servicios de equilibrio de carga. Además, permite llevar a cabo un monitoreo integral del enlace'.*

#### Equilibrar la carga

Para utilizar bonding con netctl, se necesita un paquete adicional disponible en los repositorios oficiales: [ifenslave](https://www.archlinux.org/packages/?name=ifenslave).

Copie el fichero `/etc/netctl/examples/bonding` a la carpeta `/etc/netctl/bonding`, y modifíquelo, por ejemplo, como se indica a continuación:

 `/etc/netctl/bonding` 
```
Description='Bond Interface'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'eth1')
IP=dhcp
IP6=stateless
```

Ahora se puede desactivar y detener su configuración antigua y establecer *bonding* para que se inicie automáticamente. Para cambiar al nuevo perfil, por ejemplo bonding, ejecute:

```
# netctl switch-to bonding

```

**Nota:** Este sistema utiliza la política de round-robin, que es el valor predeterminado para el controlador `bonding`. Véase [official documentation](https://www.kernel.org/doc/Documentation/networking/bonding.txt) para obtener más detalles.

**Sugerencia:** Para comprobar el estado y la modalidad de bonding, ejecute: `$ cat /proc/net/bonding/bond0` 

#### Pasar a la conexión inalámbrica cuando la conexión cableada falla

Este ejemplo describe cómo usar *bonding* como respaldo de la red inalámbrica para cuando la red cableada se cae, sirve también para detectar la presencia de cualquier conexión de red e iniciar dhcpcd cuando una o ambas redes se conecten.

Necesitaremos los paquetes ~~[ifplugd](https://www.archlinux.org/packages/?name=ifplugd)~~, [ifenslave](https://www.archlinux.org/packages/?name=ifenslave), y [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) disponibles en los repositorios oficiales.

Primero, configuraremos el controlador `bonding` para usar `active-backup`:

 `/etc/modprobe.d/bonding.conf` 
```
options bonding mode=active-backup
options bonding miimon=100
options bonding primary=eth0
options bonding max_bonds=0
```

La opción `max_bonds` evita obtener el error `Interface bond0 already exists`. Se puede añadir el ajuste `fail_over_mac=active` si se usa el filtrado MAC.

Luego, configuraremos un perfil de netctl para subordinar las dos interfaces del hardware:

 `/etc/netctl/failover` 
```
Description='A wired connection with failover to wireless'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'wlan0')
IP='no'
SkipNoCarrier='no'
```

Activamos el perfil en el arranque:

```
# netctl enable failover

```

Configuraremos *wpa_supplicant* para asociarla con redes conocidas. Esto se puede hacer con un perfil netcfg (recuerde usar `IP='no'`), con un servicio *wpa_supplicant* funcionando constantemente, o bajo demanda con *wpa_cli*. Las maneras para hacer esto están tratadas en la página de [wpa_supplicant](/index.php/WPA_supplicant_(Espa%C3%B1ol) "WPA supplicant (Español)"). Para mantener *wpa_supplicant* ejecutándose constántemente, cree el fichero de configuración de *wpa_supplicant* `/etc/wpa_supplicant/wpa_supplicant-wlan0.conf` y después ejecute:

```
# systemctl enable wpa_supplicant@wlan0

```

Ajuste `IP='no'` en el perfil de la conexión de red cableada. La dirección IP debe asignarse únicamente a la interfaz *bond0*.

A partir de ahora, si tenemos una conexión por cable e inalámbrica conectadas a la misma red, es probable que podamos desconectar y reconectar la conexión por cable sin perder la conectividad. ¡En la mayoría de los casos, incluso la transmisión de música se realizará sin saltos!

### Quitar direcciones antiguas de dhcpcd

El fichero `/var/lib/dhcpcd/dhcpcd-[interface].lease`, donde `[interface]` es el nombre de la interfaz con la que se tiene el vínculo, contiene la dirección DHCP vigente, que es la respuesta enviada por el servidor DHCP. Se utiliza para determinar la última concesión del servidor, y su atributo `mtime` se utiliza para determinar cuándo se expidió. Esta última información se utiliza para solicitar la misma dirección IP anterior, si está disponible. Si no se quiere eso, simplemente borre este fichero. Por ejemplo :

```
# rm /var/lib/dhcpcd/dhcpcd-wlan0.lease

```

Esto elimina la última dirección dhcpcd concedida a la interfaz `wlan0` interface.

### Problemas de espera con DHCP

Si se están teniendo problemas de tiempo de espera al solicitar concesiones a través de DHCP, se puede establecer un valor de tiempo de espera mayor que el que netctl establece de forma predeterminada, que es de 30 segundos. Cree un fichero en `/etc/netctl/hooks/` o `/etc/netctl/interfaces/`, y añada `TimeoutDHCP=40` para disponer de un tiempo de espera de 40 segundos, y hágalo ejecutable.

## Véase también

*   [Hilo sobre información oficial](https://bbs.archlinux.org/viewtopic.php?id=157670)
*   Hay un applet de cinnamon disponible en AUR: [cinnamon-applet-netctl-systray-menu](https://aur.archlinux.org/packages/cinnamon-applet-netctl-systray-menu/)