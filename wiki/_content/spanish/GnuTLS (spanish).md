**Estado de la traducción**
Este artículo es una traducción de [GnuTLS](/index.php/GnuTLS "GnuTLS"), revisada por última vez el **2018-12-19**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GnuTLS&diff=0&oldid=559519) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Según [Wikipedia](https://en.wikipedia.org/wiki/es:GnuTLS "wikipedia:es:GnuTLS"):

	**GnuTLS**, **GNU Transport Layer Security Library**, es una implementación de software libre de los protocolos SSL y TLS. Su propósito es ofrecer una Interfaz de programación de aplicaciones o API (del inglés Application Programming Interface) para aplicaciones que permite usar el protocolo de comunicaciones seguras sobre la capa de transporte de red.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
    *   [2.1 Generar una clave privada RSA](#Generar_una_clave_privada_RSA)
    *   [2.2 Generar una solicitud de firma de certificado](#Generar_una_solicitud_de_firma_de_certificado)
    *   [2.3 Generar un certificado autofirmado](#Generar_un_certificado_autofirmado)
*   [3 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gnutls](https://www.archlinux.org/packages/?name=gnutls).

Para lograr la integración con el [Servidor HTTP Apache](/index.php/Apache_HTTP_Server_(Espa%C3%B1ol) "Apache HTTP Server (Español)"), instale [mod_gnutls](/index.php/Mod_gnutls "Mod gnutls").

## Utilización

Véase [certtool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/certtool.1) para entender el comando utilizado en las siguientes secciones y el [documento informativo](https://www.gnutls.org/manual/html_node/index.html) para la documentación de la API.

### Generar una clave privada RSA

```
$ certtool -p --rsa --bits=*tamañodelaclave*

```

### Generar una solicitud de firma de certificado

```
$ certtool -q --load-privkey *clave_privada* --outfile *archivo*

```

### Generar un certificado autofirmado

```
$ certtool -s --load-privkey *clave_privada* --outfile *archivo*

```

## Véase también

*   [Página web oficial](https://www.gnutls.org/)