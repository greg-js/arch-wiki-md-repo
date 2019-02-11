**Estado de la traducción**
Este artículo es una traducción de [Wget](/index.php/Wget "Wget"), revisada por última vez el **2019-01-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Wget&diff=0&oldid=563573) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[GNU Wget](http://www.gnu.org/software/wget/) es un paquete de software libre para recuperar archivos utilizando [HTTP](/index.php/HTTP_(Espa%C3%B1ol) "HTTP (Español)"), HTTPS, [FTP](/index.php/FTP_(Espa%C3%B1ol) "FTP (Español)") y FTPS *(FTPS desde la versión 1.18)*. Es una herramienta de línea de órdenes no interactiva, por lo que puede ser llamada fácilmente desde scripts.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Automatización FTP](#Automatización_FTP)
    *   [2.2 Proxy](#Proxy)
    *   [2.3 Integración con pacman](#Integración_con_pacman)
*   [3 Utilización](#Utilización)
    *   [3.1 Utilización básica](#Utilización_básica)
    *   [3.2 Archivar un sitio web completo](#Archivar_un_sitio_web_completo)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [wget](https://www.archlinux.org/packages/?name=wget). La versión [git](/index.php/Git_(Espa%C3%B1ol) "Git (Español)") está presente en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") por el nombre [wget-git](https://aur.archlinux.org/packages/wget-git/).

## Configuración

La configuración se realiza en `/etc/wgetrc`. No solo el archivo de configuración predeterminado está bien documentado; alterarlo rara vez es necesario. Véase la página del manual para opciones más intrincadas.

### Automatización FTP

Normalmente, [SSH](/index.php/SSH_(Espa%C3%B1ol) "SSH (Español)") se utiliza para transferir archivos de forma segura en una red. Sin embargo, FTP es más ligero en recursos en comparación con scp y [rsync](/index.php/Rsync_(Espa%C3%B1ol) "Rsync (Español)") sobre SSH. FTP no es seguro, pero cuando se transfieren grandes cantidades de datos dentro de un entorno protegido por un cortafuegos en sistemas vinculados a la CPU, la utilización de FTP puede resultar beneficioso.

```
wget ftp://root:algunacontraseña@10.13.X.Y//ifs/home/test/big/"*.tar"

3,562,035,200 74.4M/s   en 47s

```

En este caso, Wget transfirió un archivo de 3.3 GiB a un ratio de 74.4MB/segundo.

En resumen, este procedimiento es:

*   programable (en scripts)
*   más rápido que ssh
*   utilizado fácilmente por lenguajes que pueden sustituir variables de cadena
*   capaz de utilizar comodines (*, ?, etc.)

### Proxy

Wget utiliza las variables de entorno proxy estándar. Véase [Ajustes del Proxy](/index.php/Proxy_settings_(Espa%C3%B1ol) "Proxy settings (Español)").

Para utilizar la función de autenticación proxy:

```
$ wget --proxy-user "DOMINIO\USUARIO" --proxy-password "CONTRASEÑA" URL

```

Los proxies que utilizan formularios de autenticación HTML no están cubiertos.

### Integración con pacman

Para que [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") utilice automáticamente Wget y un proxy con autenticación, coloque la orden Wget en `/etc/pacman.conf`, en la sección `[options]`:

```
XferCommand = /usr/bin/wget --proxy-user "dominio\usuario" --proxy-password="contraseña" --passive-ftp -q --show-progress -c -O %o %u

```

[Template:Atención](/index.php?title=Template:Atenci%C3%B3n&action=edit&redlink=1 "Template:Atención (page does not exist)")

## Utilización

Esta sección explica algunos de los escenarios de uso para Wget.

### Utilización básica

Uno de los casos de uso más básicos y comunes para Wget es descargar un archivo de Internet.

```
$ wget <url>

```

Cuando ya conoce la URL de un archivo para descargar, esto puede ser mucho más rápido que la rutina habitual, descargándolo en su navegador y moviéndolo manualmente al directorio correcto. No hace falta decir que, solo con el uso más simple, es probable que pueda ver algunas formas de utilizar esto para algunas descargas automáticas, si así lo desea.

### Archivar un sitio web completo

Wget puede archivar un sitio web completo al tiempo que conserva los enlaces de destino correctos cambiando los enlaces absolutos a enlaces relativos.

```
$ wget -np -r -k 'http://su-url-aquí'

```