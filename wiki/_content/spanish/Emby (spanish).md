**Estado de la traducción**
Este artículo es una traducción de [Emby](/index.php/Emby "Emby"), revisada por última vez el **2019-02-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Emby&diff=0&oldid=566070) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Emby](https://emby.media/) es un servidor multimedia personal, el cual tiene clientes para muchas plataformas. Se utiliza para organizar el home media personal, así como para reproducir en otros dispositivos. Hay una gran cantidad de canales que están respaldados por la comunidad, e incluso se pueden utilizar con tarjetas PVR y Tuner para proporcionar streaming de TV de forma remota.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [emby-server](https://www.archlinux.org/packages/?name=emby-server).

## Utilización

[Active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") e [inicie](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `emby-server.service`.

Acceda a Emby con el navegador web a través del siguiente enlace: [http://localhost:8096/](http://localhost:8096/)

Emby se ejecuta bajo el [usuario](/index.php/Users_and_groups_(Espa%C3%B1ol) "Users and groups (Español)") y [grupo de usuarios](/index.php/Users_and_groups_(Espa%C3%B1ol)#Administración_de_grupos "Users and groups (Español)") `emby`. Para permitir que Emby acceda a su biblioteca multimedia, o bien agregue el usuario `emby` al grupo que sea propietario de sus archivos:

```
sudo gpasswd -a emby audio

```

o bien [cambe su propietario](/index.php/File_permissions_and_attributes#Changing_ownership "File permissions and attributes") al usuario `emby`.