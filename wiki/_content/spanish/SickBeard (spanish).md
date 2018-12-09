**Estado de la traducción**
Este artículo es una traducción de [SickBeard](/index.php/SickBeard "SickBeard"), revisada por última vez el **2018-12-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=SickBeard&diff=0&oldid=558559) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Dropbox](/index.php/Dropbox "Dropbox")

[Sick Beard](http://sickbeard.com) es un PVR para usuarios de grupos de noticias (con soporte de torrent limitado). Busca nuevos episodios de sus programas favoritos y, cuando se publican, los descarga, los clasifica y los renombra, y, opcionalmente, genera metadatos para ellos. Actualmente es compatible con NZBs.org, NZBMatrix, NZBs'R'Us, Newzbin, Womble's Index, NZB.su, TVTorrents y EZRSS y obtiene la información de los programas de theTVDB.com y TVRage.com.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [sickbeard](https://aur.archlinux.org/packages/sickbeard/).

[Inicie/habilite](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `sickbeard.service`.

## Solución de problemas

### El daemon no se inicia

El script de systemd de Sickbeard asocia la aplicación a `/run/sickbeard.pid`. Si el arranque de sickbeard falla y el journalctl indica:

```
Unable to write PID file: No such file or directory [2]

```

usted puede:

*   reiniciar
*   ejecutar: `systemd-tmpfiles --create`

Esto creará el directorio, basándose en el archivo `/usr/lib/tmpfiles.d/sickbeard.conf` el cual es instalado por el paquete sickbeard.

Puede leer más sobre este problema [en este hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=158625).