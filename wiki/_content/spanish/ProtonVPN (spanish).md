**Estado de la traducción**
Este artículo es una traducción de [ProtonVPN](/index.php/ProtonVPN "ProtonVPN"), revisada por última vez el **2019-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ProtonVPN&diff=0&oldid=580520) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [OpenVPN](/index.php/OpenVPN "OpenVPN")

[ProtonVPN](https://www.protonvpn.com) es un proveedor de [VPN](https://en.wikipedia.org/wiki/es:Red_privada_virtual "wikipedia:es:Red privada virtual") que utiliza el protocolo [OpenVPN](https://en.wikipedia.org/wiki/es:OpenVPN "wikipedia:es:OpenVPN").

Cada solución requiere una cuenta ProtonVPN y el paquete [openvpn](https://www.archlinux.org/packages/?name=openvpn).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Interfaz de línea de órdenes de OpenVPN](#Interfaz_de_línea_de_órdenes_de_OpenVPN)
    *   [1.1 Configuración](#Configuración)
    *   [1.2 Utilización](#Utilización)
    *   [1.3 Consejos y trucos](#Consejos_y_trucos)
        *   [1.3.1 Guardar autenticación de OpenVPN](#Guardar_autenticación_de_OpenVPN)
        *   [1.3.2 Activar VPN en el arranque](#Activar_VPN_en_el_arranque)
*   [2 protonvpn-cli](#protonvpn-cli)
    *   [2.1 Configuración](#Configuración_2)
    *   [2.2 Utilización](#Utilización_2)
*   [3 Interfaz gráfica](#Interfaz_gráfica)

## Interfaz de línea de órdenes de OpenVPN

La conexión VPN se puede ejecutar manualmente con la interfaz proporcionada por el paquete [openvpn](https://www.archlinux.org/packages/?name=openvpn).

### Configuración

Descargue uno o más archivos de configuración de OpenVPN desde la [página de descargas de ProtonVPN](https://account.protonvpn.com/downloads).

Copie los archivos de configuración del cliente *.ovpn en `/etc/openvpn/client/` y haga una copia de seguridad del original.

Siga [estos pasos](/index.php/OpenVPN#Update_systemd-resolved_script "OpenVPN") para asegurarse de que todo el tráfico de su red utilice VPN. Si usa systemd anterior a 229, siga [estos pasos](/index.php/OpenVPN#Update_resolv-conf_script "OpenVPN").

### Utilización

Conéctese a la VPN:

```
# openvpn /etc/openvpn/client/client_config_file.ovpn

```

Proporcione el **nombre de usuario de OpenVPN / IKEv2** obtenido de la [página de la cuenta ProtonVPN](https://account.protonvpn.com/settings).

Presione `Ctrl+C` para cerrar la conexión VPN.

### Consejos y trucos

#### Guardar autenticación de OpenVPN

Las credenciales de OpenVPN se pueden guardar en un archivo separado y leerse automáticamente:

 `/etc/openvpn/client/client_config_file.ovpn` 
```
auth-user-pass /etc/openvpn/client/login.conf

```
 `/etc/openvpn/client/login.conf` 
```
openvpn_username
openvpn_password

```

#### Activar VPN en el arranque

Para la configuración del servicio systemd, consulte [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

## protonvpn-cli

ProtonVPN proporciona una utilidad para acceder a VPN. Los detalles se pueden encontrar en el [sitio web oficial](https://protonvpn.com/support/linux-vpn-tool/) y el [repositorio GitHub](https://github.com/ProtonVPN/protonvpn-cli).

### Configuración

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [protonvpn-cli](https://aur.archlinux.org/packages/protonvpn-cli/).

Inicialice el cliente:

```
# protonvpn-cli -init

```

Introduzca su nombre de usuario y contraseña en **ProtonVPN Login** que debe haber configurado en la página de [Configuración de ProtonVPN](https://account.protonvpn.com/settings). Por ejemplo:

```
Enter OpenVPN username: ProtonVPN.user
Enter OpenVPN password:

```

Después de ingresar las credenciales, debe seleccionar su plan de suscripción. Por ejemplo, seleccione el plan gratuito:

```
[.]ProtonVPN Plans:
1) Free
2) Basic
3) Plus
4) Visionary
Enter Your ProtonVPN plan ID: 1

```

### Utilización

Conéctese a la VPN:

```
# protonvpn-cli -connect

```

Debería ver una lista detallada de países con todos los servidores disponibles. Seleccione el servidor preferido y haga clic en OK.

Luego seleccione el protocolo UDP o TCP y haga clic en OK nuevamente.

Si la conexión fue exitosa, verá la siguiente salida:

```
Connecting...
Connected!
New IP: X.X.X.X

```

## Interfaz gráfica

Su [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") puede proporcionar una interfaz gráfica para configurar la conexión OpenVPN. Busque en la configuración de conexión. De lo contrario, [NetworkManager#Installation](/index.php/NetworkManager#Installation "NetworkManager"), [NetworkManager#VPN support](/index.php/NetworkManager#VPN_support "NetworkManager") y [NetworkManager#Front-ends](/index.php/NetworkManager#Front-ends "NetworkManager") proporcionan información útil.

**Nota:** Es necesario ampliar la sección [#Configuración](#Configuración).