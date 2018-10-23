**Estado de la traducción**
Este artículo es una traducción de [Nessus](/index.php/Nessus "Nessus"), revisada por última vez el **2018-10-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Nessus&diff=0&oldid=549955) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Nessus](https://en.wikipedia.org/wiki/es:Nessus "wikipedia:es:Nessus") es un [escáner de vulnerabilidades](https://en.wikipedia.org/wiki/Vulnerability_scanner "wikipedia:Vulnerability scanner") patentado, disponible de forma gratuita para uso personal. Hay [más de 40,000 complementos](http://www.tenable.com/plugins/) que cubren una amplia gama de fallos tanto locales como remotos.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración posterior a la instalación](#Configuraci.C3.B3n_posterior_a_la_instalaci.C3.B3n)
*   [3 Utilización](#Utilizaci.C3.B3n)
*   [4 Eliminación](#Eliminaci.C3.B3n)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [nessus](https://aur.archlinux.org/packages/nessus/).

**Nota:** A partir del 26 de abril de 2016, ya no es necesario aceptar y descargar el rpm de Nessus. Un script ejecutará y descargará el rpm del sitio de Nessus automáticamente. Si parece que no sucede nada, tenga paciencia, ya que el script se ejecuta de forma silenciosa. La instalación continuará después de que se descargue el rpm.

## Configuración posterior a la instalación

Registre su correo electrónico en [[1]](http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code) y espere a que se le envíe su clave por correo electrónico.

## Utilización

El paquete [nessus](https://aur.archlinux.org/packages/nessus/) proporciona un archivo de unidad `nessusd.service`, véase [systemd (Español)#Usar las unidades](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") para más detalles.

Acceda a la interfaz web en [https://localhost:8834](https://localhost:8834) y/o utilice la interfaz de línea de comandos (`/opt/nessus/sbin/nessuscli`). En la mayoría de los navegadores, deberá aceptar manualmente el certificado SSL que creó para el servidor.

## Eliminación

El paquete puede eliminarse con [pacman](/index.php/Pacman_(Espa%C3%B1ol)#Desinstalar_paquetes "Pacman (Español)"), pero los archivos creados por Nessus, como la base de datos de complementos que descarga, deben eliminarse manualmente:

**Nota:** Esto eliminará sus archivos de configuración de Nessus.

```
# rm -r /opt/nessus

```

## Véase también

*   [Documentación oficial en varios idiomas](http://www.tenable.com/products/nessus/documentation)