**Estado de la traducción**
Este artículo es una traducción de [Burp suite](/index.php/Burp_suite "Burp suite"), revisada por última vez el **2019-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Burp_suite&diff=0&oldid=584507) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Del [sitio web oficial](http://portswigger.net/burp/):

	Burp Suite es una plataforma integrada para realizar pruebas de seguridad de aplicaciones web. Sus diversas herramientas funcionan a la perfección para respaldar todo el proceso de prueba, desde el mapeo inicial y el análisis de un incipiente ataque de una aplicación hasta la búsqueda y exploración de vulnerabilidades de seguridad.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Instalar certificado HTTPS en Firefox](#Instalar_certificado_HTTPS_en_Firefox)
*   [3 Véase también](#Véase_también)

## Instalación

Instale [burpsuite](https://aur.archlinux.org/packages/burpsuite/) desde [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

Esto instalará Burp Suite Community (edición gratuita).

## Configuración

Burp Proxy funcionará de forma inmediata con conexiones HTTP. Para HTTPS, primero se debe instalar el certificado de PortSwigger.

### Instalar certificado HTTPS en Firefox

Iniciar Burp:

```
$ burpsuite

```

Abra *Proxy -> Options*. En la sección *Proxy Listeners* añada una nueva interfaz. Establezca *Interface* a `127.0.0.1:8080` asegúrese de que la casilla de verificación *Running* esté activada

Navegue a `[http://127.0.0.1:8080/](http://127.0.0.1:8080/)` en Firefox, haga clic en el enlace *CA Certificate* en la parte superior derecha y guarde el archivo del certificado en alguna parte.

En Firefox (en Linux), abra el menú *Editar*, y en este haga clic en *Preferencias*, vaya a *Privadicad & Seguridad -> Certificados -> Ver certificados...*. Haga clic en *Importar...* y seleccione el archivo. Marque la casilla de verificación *Confiar en esta CA para identificar sitios web* y haga clic en *Aceptar*.

## Véase también

*   [Wikipedia:Burp suite](https://en.wikipedia.org/wiki/Burp_suite "wikipedia:Burp suite")
*   [Burp Suite video tutorials](http://portswigger.net/burp/tutorials/)