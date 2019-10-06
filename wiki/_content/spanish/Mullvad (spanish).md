**Estado de la traducción**
Este artículo es una traducción de [Mullvad](/index.php/Mullvad "Mullvad"), revisada por última vez el **2019-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Mullvad&diff=0&oldid=584433) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Mullvad](https://mullvad.net/en/) es un servicio VPN con sede en Suecia que utiliza [OpenVPN](/index.php/OpenVPN "OpenVPN") y [WireGuard](/index.php/WireGuard "WireGuard").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración manual](#Configuración_manual)
*   [3 Fugas de DNS](#Fugas_de_DNS)
*   [4 Véase también](#Véase_también)

## Instalación

El nuevo [cliente GUI oficial](https://mullvad.net/download/) está disponible como [mullvad-vpn](https://aur.archlinux.org/packages/mullvad-vpn/).

Después de la instalación, deberá activar e iniciar el servicio `mullvad-daemon.service` de [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

Alternativamente, puede usar el cliente anterior o [OpenVPN](/index.php/OpenVPN "OpenVPN") en un archivo de configuración para Mullvad como se explica en [#Configuración manual](#Configuración_manual).

## Configuración manual

Primero, asegúrese de que los paquetes [openvpn](https://www.archlinux.org/packages/?name=openvpn) y [openresolv](https://www.archlinux.org/packages/?name=openresolv) estén instalados y luego proceda a descargar el paquete del archivo de configuración OpenVPN de Mullvad desde [su sitio web](https://www.mullvad.net/download/config/) (en la pestaña «otras plataformas») y descomprima el archivo descargado en `/etc/openvpn/client/`.

Cambie el nombre de mullvad_linux.conf para que se use un nombre más corto con el servicio [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") más adelante:

```
# mv /etc/openvpn/client/mullvad_linux.conf /etc/openvpn/client/mullvad.conf

```

Para utilizar los servidores de nombres suministrados por Mullvad, se invoca el [script update-resolv-conf](/index.php/OpenVPN#Update_resolv-conf_script "OpenVPN") al iniciar y detener la conexión con OpenVPN para modificar [resolv.conf](/index.php/Resolv.conf "Resolv.conf") para incluir las direcciones IP correctas. Este script también se incluye en el archivo comprimido zip de configuración de Mullvad, pero debe moverse a `/etc/openvpn/` para que coincida con la ruta especificada en el archivo de configuración de Mullvad:

```
# mv /etc/openvpn/client/update-resolv-conf /etc/openvpn/

```

El script se puede mantener actualizado con el script [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf), que también contiene una solución para las fugas de DNS.

Después de la configuración, la conexión VPN puede ser [gestionada](/index.php/Enabled "Enabled") con `openvpn-client@mullvad.service`. Si el servicio no se inicia por un error como `Cannot open TUN/TAP dev /dev/net/tun: No such device (errno=19)`, es posible que deba reiniciar el sistema para activar OpenVPN creando el dispositivo de red correcto para la tarea.

## Fugas de DNS

Por defecto, las configuraciones openvpn de Mullvad permiten fugas de DNS y, para los casos habituales de uso de VPN, este es un defecto de privacidad desfavorable. El nuevo cliente GUI de Mullvad detiene automáticamente las fugas de DNS eliminando cada IP del servidor DNS de la configuración del sistema y reemplazándolas con una IP que señala al propio servidor DNS sin registro de Mullvad, válido durante la conexión VPN. Esta solución también se puede aplicar con el método plano de OpenVPN configurando [resolv.conf](/index.php/Resolv.conf "Resolv.conf") para usar **solo** la IP del servidor DNS Mullvad especificada en su [sitio web](https://www.mullvad.net/guides/dns-leaks/).

La versión del script de actualización de resolv.conf con [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf) implementa una solución diferente para las fugas mediante el uso del parámetro de interfaz exclusivo `-x` al ejecutar la orden `resolvconf`, pero esto puede causar otra forma de fuga de DNS al hacer que incluso cada dirección de red local se resuelva a través del servidor DNS proporcionado por Mullvad, como se indica en la [página de incidencias de GitHub para el script](https://github.com/masterkorp/openvpn-update-resolv-conf/issues/18).

## Véase también

*   [Mullvad client source code](https://github.com/mullvad/mullvadvpn-app)
*   [Mullvad FAQ](https://mullvad.net/en/faq/)