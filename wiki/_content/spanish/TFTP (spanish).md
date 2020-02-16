**Estado de la traducción**
Este artículo es una traducción de [TFTP](/index.php/TFTP "TFTP"), revisada por última vez el **2020-02-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=TFTP&diff=0&oldid=591966) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El [Protocolo de transferencia de archivos trivial](https://en.wikipedia.org/wiki/es:TFTP o para actualizar la configuración y el firmware en dispositivos con memoria limitada, como enrutadores, teléfonos IP e impresoras.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Servidor](#Servidor)
    *   [1.1 tftp-hpa](#tftp-hpa)
    *   [1.2 atftp](#atftp)
    *   [1.3 dnsmasq](#dnsmasq)
*   [2 Cliente](#Cliente)
    *   [2.1 tftp-hpa](#tftp-hpa_2)
    *   [2.2 curl](#curl)

## Servidor

Hay varias implementaciones del servidor TFTP, algunas se listan a continuación y [iputils](https://www.archlinux.org/packages/?name=iputils) también incluye una versión de tftp.

**Nota:** Asegúrese de no iniciar diferentes implementaciones de TFTP al mismo tiempo. Fallarán con un error `tiene más de un socket`, porque solo uno puede escuchar el puerto TFTP predeterminado `69`.

### tftp-hpa

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) y después [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `tftpd.service`.

Para cambiar los parámetros del servicio modifique `/etc/conf.d/tftpd`.

[tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) requiere rutas absolutas en tus tftp gets. Si la ruta absoluta no es posible por alguna razón, considere utilizar en su lugar [atftp](https://www.archlinux.org/packages/?name=atftp).

### atftp

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [atftp](https://www.archlinux.org/packages/?name=atftp) y después [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `atftpd.service`.

Para cambiar los parámetros del servicio modifique `/etc/conf.d/atftpd`.

### dnsmasq

Véase [dnsmasq (Español)#Servidor TFTP](/index.php/Dnsmasq_(Espa%C3%B1ol)#Servidor_TFTP "Dnsmasq (Español)").

## Cliente

### tftp-hpa

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) y ejecute:

```
$ tftp

```

### curl

El estándar [curl](https://www.archlinux.org/packages/?name=curl) tiene la capacidad de conectarse a un servidor TFTP y subir un archivo mediante:

```
$ curl -T ARCHIVO tftp://SERVIDOR

```

O descargar un archivo mediante:

```
$ curl -o DESTINO tftp://SERVIDOR/archivo

```

Donde `archivo` es relativo al directorio raíz de TFTP.