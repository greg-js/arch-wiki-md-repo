**Estado de la traducción**
Este artículo es una traducción de [Isatapd](/index.php/Isatapd "Isatapd"), revisada por última vez el **2019-01-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Isatapd&diff=0&oldid=563470) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Daemon](/index.php/Daemon_(Espa%C3%B1ol) "Daemon (Español)")
*   [IPv6_-_6in4_Tunnel](/index.php/IPv6_-_6in4_Tunnel "IPv6 - 6in4 Tunnel")

[isatapd](http://www.saschahlusiak.de/linux/isatap.htm) es un cliente [ISATAP](https://en.wikipedia.org/wiki/es:ISATAP "wikipedia:es:ISATAP"). Es un programa daemon para crear y mantener un túnel ISATAP RFC 5214 en Linux.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [isatapd](https://www.archlinux.org/packages/?name=isatapd) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Configuración

El paquete agrega un script *rc.d* a `/etc/rc.d/isatapd` para ejecutar isatapd como un servicio del sistema. Necesita modificarlo para configurar su router. Cambie el valor de **ISATAPD_ROUTER** al nombre de host del router que desea utilizar.

**Nota:** El valor predeterminado de **ISATAPD_ROUTER** es **isatap.tsinghua.edu.cn**. Es el router proporcionado por la Universidad de Tsinghua.

Si desea modificar otras opciones en vez de utilizar los valores predeterminados, véase [la página oficial del proyecto](http://www.saschahlusiak.de/linux/isatap.htm) para obtener más información.

## Ejecutar

[Inicie y active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `isatapd.service`.