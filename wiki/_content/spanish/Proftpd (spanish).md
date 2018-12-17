**Estado de la traducción**
Este artículo es una traducción de [Proftpd](/index.php/Proftpd "Proftpd"), revisada por última vez el **2018-12-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Proftpd&diff=0&oldid=559253) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[proFtpd](http://proftpd.org/) (Pro FTP daemon) es un servidor FTP altamente sofisticado, que presenta una gran cantidad de opciones de configuración al usuario.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Acceso anónimo](#Acceso_anónimo)
*   [3 Véase también](#Véase_también)

## Instalación

[proftpd](https://aur.archlinux.org/packages/proftpd/) está disponible en el AUR. [Active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") e inicie `proftpd.service`.

## Configuración

El [archivo de configuración](http://www.proftpd.org/docs/howto/ConfigFile.html) está disponible en `/etc/proftpd.conf`. La página web del proyecto tiene una extensa [documentación](http://www.proftpd.org/docs/).

### Acceso anónimo

Para atajar un problema común, para que el acceso anónimo funcione con `/bin/false` como intérprete de órdenes para el usuario ftp (la configuración predeterminada), debe agregar la línea `RequireValidShell off` a `/etc/proftpd.conf`. De lo contrario, los inicios de sesión anónimos recibirán un error 530.

## Véase también

*   [BLFS: ProFTPD](http://www.linuxfromscratch.org/blfs/view/7.6/server/proftpd.html)