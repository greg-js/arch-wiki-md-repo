**Estado de la traducción**
Este artículo es una traducción de [ProtonVPN](/index.php/ProtonVPN "ProtonVPN"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ProtonVPN&diff=0&oldid=543304) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [openvpn](/index.php/Openvpn "Openvpn")

[ProtonVPN](https://www.protonvpn.com) es un proveedor de [VPN](https://en.wikipedia.org/wiki/es:Red_privada_virtual "wikipedia:es:Red privada virtual") que utiliza el protocolo [OpenVPN](https://en.wikipedia.org/wiki/es:OpenVPN "wikipedia:es:OpenVPN").

Para seguir este tutorial, se debe tener una cuenta protonvpn.

## Contents

*   [1 Tutorial](#Tutorial)
    *   [1.1 Guardar la autenticación OpenVPN](#Guardar_la_autenticaci.C3.B3n_OpenVPN)
    *   [1.2 Activar VPN en el arranque](#Activar_VPN_en_el_arranque)
*   [2 Utilizar el intérprete de línea de órdenes de ProtonVPN](#Utilizar_el_int.C3.A9rprete_de_l.C3.ADnea_de_.C3.B3rdenes_de_ProtonVPN)

## Tutorial

[Instale](/index.php/Install "Install") el paquete [openvpn](https://www.archlinux.org/packages/?name=openvpn).

Inicie sesión en ProtonVPN y descargue uno o más archivos de configuración de OpenVPN.

Copie los archivos *.ovpn en `/etc/openvpn/client/`

Elija el archivo **.ovpn** correspondiente que se utilizará (se usa como ejemplo ca.protonvpn.com.tcp443.ovpn)

Copie el archivo con una nueva extensión (esto es solo para que mantenga intacto el archivo ovpn original)

```
# cp /etc/openvpn/client/ca.protonvpn.com.tcp443.ovpn /etc/openvpn/client/protonvpn.conf

```

Instale el script [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf). Guárdelo, por ejemplo, en `/etc/openvpn/update-resolv-conf` y hágalo ejecutable con [chmod](/index.php/Chmod "Chmod"). También hay un paquete AUR: [openvpn-update-resolv-conf-git](https://aur.archlinux.org/packages/openvpn-update-resolv-conf-git/) que se encarga de la instalación del script por usted. Este script garantiza que todo el tráfico hacia/desde Internet pase por la VPN y lo protege contra las fugas de DNS.

```
# chmod 755 /etc/openvpn/update-resolv-conf

```

Modifique el archivo **.conf** para usar el script update-resolv-conf.sh.

 `/etc/openvpn/client/protonvpn.conf` 
```
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf
down-pre

```

Inicie su VPN:

```
# openvpn /etc/openvpn/client/protonvpn.conf

```

Presione `Ctrl+C` para cerrar la conexión VPN.

### Guardar la autenticación OpenVPN

Si se cansa de ingresar su nombre de usuario y contraseña, puede guardar sus credenciales de OpenVPN en un archivo separado para que las lea automáticamente.

 `/etc/openvpn/client/protonvpn.conf` 
```
auth-user-pass /etc/openvpn/client/login.conf

```
 `/etc/openvpn/client/login.conf` 
```
openvpn_username
openvpn_password

```

### Activar VPN en el arranque

Para configurar el servicio de systemd, vea [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

## Utilizar el intérprete de línea de órdenes de ProtonVPN

ProtonVPN proporciona una utilidad para acceder a la VPN. Los detalles se pueden encontrar en [su sitio web](https://protonvpn.com/support/linux-vpn-tool/) y el repositorio de GitHub se puede encontrar [aquí](https://github.com/ProtonVPN/protonvpn-cli). Este paquete se puede instalar directamente desde [AUR](https://aur.archlinux.org/packages/protonvpn-cli/).