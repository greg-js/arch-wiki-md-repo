**Estado de la traducción**
Este artículo es una traducción de [GNOME/Web](/index.php/GNOME/Web "GNOME/Web"), revisada por última vez el **2018-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNOME/Web&diff=0&oldid=556384) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Web es el navegador web predeterminado para [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"). Web proporciona una interfaz simple y minimalista para acceder a internet. Aunque está desarrollado principalmente para GNOME, Web funciona también de manera aceptable en otros [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)").

**Nota:** Web era conocido como [Epiphany](http://projects.gnome.org/epiphany/) antes de la versión 3.4\. La aplicación recibió nuevos nombres descriptivos, uno para cada idioma admitido. El nombre *Epiphany* se utiliza todavía en muchos lugares, como el nombre del ejecutable, algunos nombres de paquetes, algunas entradas de escritorio y algunos esquemas GSettings.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Bloqueando anuncios](#Bloqueando_anuncios)
    *   [2.2 Aplicaciones Web](#Aplicaciones_Web)
    *   [2.3 Hoja de estilo personalizada](#Hoja_de_estilo_personalizada)
    *   [2.4 Tipografía](#Tipografía)
    *   [2.5 Vídeo](#Vídeo)
*   [3 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [epiphany](https://www.archlinux.org/packages/?name=epiphany). Si desea almacenar las contraseñas de inicio de sesión, instale [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

## Configuración

### Bloqueando anuncios

Activado de forma predeterminada, puede desactivarlo desmarcando *Intentar bloquear anuncios* en *Preferencias*. EasyList, EasyPrivacy y Fanboy-molestia son listas de bloqueo predeterminadas. Todas las listas se actualizan periódicamente.

**Nota:** Debido a que faltan algunas funciones, por ejemplo, la ocultación de elementos, Web no bloquea/oculta algunos anuncios. Véase este [aviso de error relacionado](https://bugzilla.gnome.org/show_bug.cgi?id=757824) para consultar su progreso.

Para obtener una lista de los filtros actualmente activados:

```
$ gsettings get org.gnome.Epiphany adblock-filters

```

Para establecer una nueva lista de filtros, por ejemplo [uBlock Origin default lists](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-easy-mode):

```
$ gsettings set org.gnome.Epiphany adblock-filters "['https://easylist.to/easylist/easylist.txt', 'https://easylist.to/easylist/easyprivacy.txt', 'https://easylist.to/easylist/fanboy-annoyance.txt', 'https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=1&mimetype=plaintext', 'https://www.malwaredomainlist.com/hostslist/hosts.txt', 'https://mirror.cedia.org.ec/malwaredomains/justdomains']"

```

Véase [EasyList](https://easylist.to/) y [Suscripciones conocidas de Adblock Plus](https://adblockplus.org/en/subscriptions)) para algunas de las listas más populares de bloqueadores de anuncios.

### Aplicaciones Web

Web puede crear aplicaciones web a partir de sitios web y añadirlas al menú del escritorio. Para configurarlos y eliminarlos, introduzca `about:applications` en la barra de direcciones.

### Hoja de estilo personalizada

Web admite hojas de estilo personalizadas que puede activar en **Tipografía y estilo** en **Preferencias**.

Utilice el siguiente ejemplo para configurar el diseño de la nueva pestaña y los colores de acuerdo con la variante oscura de Adwaita:

 `~/.config/epiphany/user-stylesheet.css` 
```
#overview {
  background-color: #2E3436 !important;
  max-width: 100% !important;
  max-height: 100% !important;
  position: fixed !important;
}

#overview .overview-title {
  color: white !important;
}

```

### Tipografía

Web no comprueba la configuración tipográfica de GNOME, pero sí la [Configuración de tipografía](/index.php/Font_configuration "Font configuration").

### Vídeo

Véase [GStreamer](/index.php/GStreamer_(Espa%C3%B1ol) "GStreamer (Español)") para la instalación del plugin necesario.

## Véase también

*   [Apps/Web - GNOME Wiki!](https://wiki.gnome.org/Apps/Web)