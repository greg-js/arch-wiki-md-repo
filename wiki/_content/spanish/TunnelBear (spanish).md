**Estado de la traducción**
Este artículo es una traducción de [TunnelBear](/index.php/TunnelBear "TunnelBear"), revisada por última vez el **2019-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=TunnelBear&diff=0&oldid=584437) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[TunnelBear](https://www.tunnelbear.com) es un proveedor de VPN que utiliza el protocolo OpenVPN.

Para usar este tutorial, se debe tener una suscripción a Giant o Grizzly.

**Nota:** existe un método [más fácil](https://www.tunnelbear.com/updates/linux_support/) para utilizar el servicio TunnelBear para usuarios de Gnome.

## Tutorial

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [openvpn](https://www.archlinux.org/packages/?name=openvpn).

Descargue los [archivos de configuración de TunnelBear OpenVPN](https://s3.amazonaws.com/tunnelbear/linux/openvpn.zip) (también puede instalar el paquete [tunnelbear](https://aur.archlinux.org/packages/tunnelbear/) desde AUR).

Descomprima la carpeta y copie todos los archivos a:

```
$ /etc/openvpn/client/

```

No olvide cambiar los permisos:

```
# chmod 600 /etc/openvpn/client/*

```

Escoja el correspondiente **.ovpn** que se usará (TunnelBear Japan se usa en este ejemplo)

Renombre la extensión y elimine el espacio

```
# mv "/etc/openvpn/client/TunnelBear Japan.ovpn" /etc/openvpn/client/TunnelBearJapan.conf

```

Edite el archivo **.conf**

 `/etc/openvpn/client/TunnelBearJapan.conf` 
```
...
keepalive 10 30
auth-user-pass login.key
...

```

Cree **login.key**

 `/etc/openvpn/client/login.key` 
```
yourtunnelbearusername
yourtunnelbearpassword

```

[Inicie/active](/index.php/Start/enable "Start/enable") `openvpn-client@TunnelBearJapan.service`.

## Referencias

*   [TunnelBear Helper](https://github.com/JenniferMack/TunnelBear-Helper)
*   [Arch Wiki OpenVPN](/index.php/OpenVPN "OpenVPN")