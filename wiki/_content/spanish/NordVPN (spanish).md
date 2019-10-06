**Estado de la traducción**
Este artículo es una traducción de [NordVPN](/index.php/NordVPN "NordVPN"), revisada por última vez el **2019-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=NordVPN&diff=0&oldid=584431) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

NordVPN es un proveedor de servicios de red privada virtual personal. NordVPN tiene su sede en Panamá. El país no tiene leyes obligatorias de retención de datos y no participa en las alianzas [Five Eyes](https://en.wikipedia.org/wiki/es:Five_Eyes "wikipedia:es:Five Eyes") o Fourteen Eyes. La versión de Linux solo usa la línea de órdenes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Crear una cuenta](#Crear_una_cuenta)
*   [2 Instalación](#Instalación)
*   [3 Systemd](#Systemd)
*   [4 Configuration](#Configuration)
    *   [4.1 Iniciar/cerrar sesión](#Iniciar/cerrar_sesión)
    *   [4.2 Activar NordLynx](#Activar_NordLynx)
    *   [4.3 Conectarse a VPN](#Conectarse_a_VPN)
    *   [4.4 Configuración](#Configuración)
    *   [4.5 Lista de servidores](#Lista_de_servidores)
*   [5 Método alternativo: conectarse a NordVPN usando NetworkManager](#Método_alternativo:_conectarse_a_NordVPN_usando_NetworkManager)
    *   [5.1 Instalación](#Instalación_2)
    *   [5.2 Configuración](#Configuración_2)
    *   [5.3 Evite la fuga de DNS](#Evite_la_fuga_de_DNS)
    *   [5.4 Conexión automática a VPN](#Conexión_automática_a_VPN)
    *   [5.5 Desactivar ipv6](#Desactivar_ipv6)
    *   [5.6 Utilizar un killswitch](#Utilizar_un_killswitch)
    *   [5.7 Probar la configuración](#Probar_la_configuración)

## Crear una cuenta

Para utilizar NordVPN, debe crear su propia cuenta en el sitio web oficial de NordVPN. [http://nordvpn.com](http://nordvpn.com)

Hay diferentes opciones de pago para elegir.

## Instalación

NordVPN se puede instalar con un paquete [nordvpn-bin](https://aur.archlinux.org/packages/nordvpn-bin/), disponible en [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Systemd

Para usar NordVPN debe [activar](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") el servicio `nordvpnd`.

```
$ sudo systemctl enable nordvpnd.service
$ sudo systemctl start nordvpnd.service

```

## Configuration

Aquí hay muchas órdenes diferentes para utilizar NordVPN.

### Iniciar/cerrar sesión

```
$ nordvpn login

```

Inicia sesión en su cuenta NordVPN.

```
$ nordvpn logout

```

Cierra la sesión de su cuenta NordVPN.

### Activar NordLynx

NordVPN tiene [introducida](https://nordvpn.com/blog/nordlynx-protocol-wireguard/) la tecnología NordLynx que se basa en el protocolo [Wireguard](/index.php/Wireguard "Wireguard"). NordLynx proporciona una latencia más baja, velocidades más altas y una mejor estabilidad de la conexión.

Actívela con la siguiente orden:

```
$ nordvpn set technology nordlynx

```

Para ver todas las tecnologías disponibles:

```
$ nordvpn set technology --help

```

### Conectarse a VPN

 `$ nordvpn connect [[country]/[server]/[country_code]/[city] o [country] [city]]` 
```
Proporcione un argumento [country] para conectarse automáticamente a un país específico. Por ejemplo: 'nordvpn set autoconnect on Australia'
Proporcione un argumento [country_code] para conectarse automáticamente a un país específico. Por ejemplo: 'nordvpn set autoconnect on us'
Proporcione un argumento [city] para conectarse automáticamente a una ciudad específica. Por ejemplo:  'nordvpn set autoconnect on Hungary Budapest'
```

Se connecta a una VPN.

```
$ nordvpn disconnect

```

Se desconecta de la VPN.

```
$ nordvpn status

```

Muestra el estado de la conexión.

### Configuración

 `$ nordvpn set protocol [protocol]` 
```
Valores admitidos para [protocol]: TCP, UDP
Ejemplo: nordvpn set protocol TCP
```

Establece el protocolo.

 `$ nordvpn set killswitch [enabled]/[disabled]` 
```
Valores admitidos para [disabled]: 0, false, disable, off, disabled
Ejemplo: nordvpn set killswitch off

Valores admitidos para [enabled]: 1, true, enable, on, enabled
Ejemplo: nordvpn set killswitch on
```

Activa o desactiva Kill Switch. Esta característica de seguridad impide que su dispositivo acceda a Internet fuera del túnel VPN seguro, en caso de que se pierda la conexión con un servidor VPN.

 `$ nordvpn set cybersec [enabled]/[disabled]` 
```
Valores admitidos para [disabled]: 0, false, disable, off, disabled
Example: nordvpn set cybersec off

Valores admitidos para [enabled]: 1, true, enable, on, enabled
Example: nordvpn set cybersec on
```

Activa o desactiva CyberSec. Cuando está activada, la función CyberSec bloqueará automáticamente los sitios web sospechosos para que ningún malware u otras amenazas cibernéticas puedan infectar su dispositivo. Además, no aparecerán anuncios llamativos. Más información sobre cómo funciona esto en: [https://nordvpn.com/features/cybersec/](https://nordvpn.com/features/cybersec/).

 `$ nordvpn set autoconnect [enabled]/[disabled] [[country]/[server]/[country_code]/[city] o [country] [city]]` 
```
Valores admitidos para [disabled]: 0, false, disable, off, disabled
Ejemplo: nordvpn set autoconnect off

Valores admitidos para [enabled]: 1, true, enable, on, enabled
Ejemplo: nordvpn set autoconnect on

Proporcione un argumento [country] para conectarse automáticamente a un país específico. Por ejemplo: 'nordvpn set autoconnect on Australia'
Proporcione un argumento [country_code] para conectarse automáticamente a un país específico. Por ejemplo: 'nordvpn set autoconnect on us'
Proporcione un argumento [city] para conectarse automáticamente a una ciudad específica. Por ejemplo: 'nordvpn set autoconnect on Hungary Budapest'
```

Activa o desactiva la conexión automática. Cuando está activada, esta función intentará conectarse automáticamente a VPN al iniciar el sistema operativo.

 `$ nordvpn set obfuscate [enabled]/[disabled]` 
```
Valores admitidos para [disabled]: 0, false, disable, off, disabled
Ejemplo: nordvpn set obfuscate off

Valores admitidos para [enabled]: 1, true, enable, on, enabled
Ejemplo: nordvpn set obfuscate on
```

Activa o desactiva la [ofuscación](https://en.wikipedia.org/wiki/es:Ofuscaci%C3%B3n "wikipedia:es:Ofuscación"). Cuando está activada, esta característica permite omitir los sensores de tráfico de red que tienen como objetivo detectar el uso del protocolo y registrarlo, estrangularlo o bloquearlo.

 `$ nordvpn set dns [servers]/[disabled]` 
```
Valores admitidos para [disabled]: 0, false, disable, off, disabled
Ejemplo: nordvpn set dns off

El argumento [servers] es una lista de direcciones IP separadas por espacio
Ejemplo:  nordvpn set dns 0.0.0.0 1.2.3.4
```

Se establecen los servidores DNS.

 `$ nordvpn whitelist command [command options] [arguments...]` 
```
Órdenes:
     add     Añade la opción a la lista blanca
     remove  Elimina la opción de la lista blanca
```

Se añade o elimina la opción a la lista blanca.

```
$ nordvpn settings

```

Muestra la configuración actual.

### Lista de servidores

```
$ nordvpn countries

```

Muestra la lista de países.

 `$ nordvpn cities [country]` 
```
Utilice esta orden para mostrar ciudades de un país específico.
Ejemplo: nordvpn cities United_States
```

Muestra la lista de ciudades.

## Método alternativo: conectarse a NordVPN usando NetworkManager

### Instalación

1\. [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) y [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn).

2\. Elija un servidor apropiado usando la página de servidores de NordVPN: [https://nordvpn.com/servers/](https://nordvpn.com/servers/) Descargue el archivo de configuración de openvpn correspondiente del sitio NordVPN: [https://nordvpn.com/ovpn/](https://nordvpn.com/ovpn/). Guarde el archivo en un lugar en su directorio personal en otro lugar que pueda recordar en el futuro.

### Configuración

1\. Haga clic con el botón secundario del ratón sobre el applet de NetworkManager desde su entorno de escritorio y haga clic en «Editar Conexiones». Haga clic en el signo más en la esquina inferior izquierda de la ventana «Conexiones de red» que aparece.

2\. Cuando elija un tipo de conexión, haga clic en el menú desplegable y desplácese hasta llegar a «Importar una configuración VPN guardada». Seleccione esa opción. Ahora, haga clic en «Crear».

3\. Navegue hasta el directorio donde extrajo todos los archivos openvpn anteriormente, luego abra uno de los archivos de esa carpeta. En términos generales, querrá abrir el archivo asociado con la conexión que desea específicamente.

4\. Después de abrir uno de los archivos openvpn, la ventana que aparece debería ser «Editar <tipo de conexión>». Escriba el nombre de usuario y contraseña de NordVPN. Hay un icono en el cuadro de contraseña que indica el permiso del usuario de las credenciales; cambie la configuración como desee («Guardar para todos los usuarios» si no desea ingresar su contraseña cada vez que se conecte).

### Evite la fuga de DNS

Para evitar fugas de DNS debe:

1\. Hacer clic en «configuración de ipv4».

2\. En el método: elija «solo direcciones automáticas (VPN)» e ingrese manualmente las direcciones DNS de NordVPN en «servidores DNS»: «103.86.96.100, 103.86.99.100» (separados por un coma).

3\. Haga clic en Guardar en la parte inferior izquierda de la ventana «Editar <tipo de conexión>».

### Conexión automática a VPN

1\. Haga clic con el botón secundario del ratón sobre el applet de NetworkManager desde su entorno de escritorio y luego haga clic en «Editar Conexionesx.

2\. Haga doble clic en la conexión Ethernet o Wifi para la que desea conectarse automáticamente a la VPN.

3\. En la pestaña «General», haga clic en «Conectarse automáticamente a VPN cuando use esta conexión» en cada conexión que desee, y elija el archivo de configuración correcto.

4\. Repita la operación para las otras conexiones que usará con la VPN.

### Desactivar ipv6

NordVPN no es compatible con ipv6\. Es posible que desee [desactivarlo por completo](/index.php/IPv6#Disable_IPv6 "IPv6").

O también puede:

1\. Hacer clic con el botón secundario del ratón sobre el applet de NetworkManager desde su entorno de escritorio y haga clic en «Editar Conexiones».

2\. Hacer doble clic en la conexión Ethernet o Wifi para la que desea conectarse automáticamente a la VPN.

3\. En la pestaña «ipv6», elija «ignorar» en el recuadro de método.

### Utilizar un killswitch

El Killswitch NordVPN no funcionará con este método, tendrá que crear el suyo utilizando [ufw](/index.php/Ufw "Ufw") o [iptables](/index.php/Iptables "Iptables").

Aquí hay un [ejemplo con UFW](https://www.smarthomebeginner.com/vpn-kill-switch-with-ufw/#Gather_information_about_your_IP_addresses).

### Probar la configuración

Puede usar estos sitios:

[https://ipleak.net/](https://ipleak.net/)

[https://www.dnsleaktest.com/](https://www.dnsleaktest.com/)

[http://ipv6leak.com/](http://ipv6leak.com/)