**Estado de la traducción**
Este artículo es una traducción de [Naemon](/index.php/Naemon "Naemon"), revisada por última vez el **2019-11-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Naemon&diff=0&oldid=589217) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Naemon](http://www.naemon.org/) es la nueva suite de monitoreo que tiene como objetivo ser más rápido y más estable, a la vez que brindarle una visión más clara del estado de su red.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Interfaz web](#Interfaz_web)
    *   [2.1 Configuración de Apache](#Configuración_de_Apache)
*   [3 Véase también](#Véase_también)

## Instalación

Instale [naemon](https://aur.archlinux.org/packages/naemon/) desde [AUR](/index.php/AUR "AUR").

Copie `/etc/naemon/examples/*` a `/etc/naemon/conf.d/` si desea comenzar con algunos servidores y servicios de ejemplo.

Instale los complementos de [monitoring-plugins](https://www.archlinux.org/packages/?name=monitoring-plugins) así como [fping](https://www.archlinux.org/packages/?name=fping).

## Interfaz web

Instale [thruk](https://aur.archlinux.org/packages/thruk/) y luego descomente:

 `/etc/naemon/naemon.cfg` 
```
broker_module=/usr/lib/naemon/naemon-livestatus/livestatus.so /var/cache/naemon/live

```

Thruk es una interfaz moderna y rápida. Pruebe la [demo](https://demo.thruk.org/thruk/cgi-bin/login.cgi).

### Configuración de Apache

Añada el usuario http al grupo naemon:

```
usermod -aG naemon http

```

Cargue los módulos e incluya naemon-thruk.conf:

 `/etc/httpd/conf/httpd.conf` 
```
LoadModule rewrite_module modules/mod_rewrite.so                            
LoadModule fcgid_module modules/mod_fcgid.so 

Include conf/extra/thruk.conf

```

Establezca thruk_user y thruk_group en naemon:

 `/etc/thruk/thruk_local.conf` 
```
thruk_user=naemon
thruk_group=naemon

```

Reinicie httpd y navegue a [http://localhost/thruk/](http://localhost/thruk/)

El nombre de usuario y la contraseña predeterminados son thrukadmin, thrukadmin.

## Véase también

*   [FAQ](http://www.naemon.org/documentation/faq/)
*   [op5 on Naemon, Nagios and the future](http://www.op5.com/blog/news/op5-naemon-nagios-future/)
*   [Andreas Ericsson: The future of Nagios](http://www.youtube.com/watch?v=YgbbyyNIiHc)