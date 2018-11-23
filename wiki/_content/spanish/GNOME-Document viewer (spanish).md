**Estado de la traducción**
Este artículo es una traducción de [GNOME/Document viewer](/index.php/GNOME/Document_viewer "GNOME/Document viewer"), revisada por última vez el **2018-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNOME/Document_viewer&diff=0&oldid=556483) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El [visor de documentos](https://en.wikipedia.org/wiki/es:Evince "w:es:Evince") está específicamente diseñado para admitir los siguientes formatos de archivo: PDF, Postscript, djvu, tiff, dvi, XPS, soporte de SyncTex con gedit, libros de cómics (cbr, cbz, cb7 y cbt). Para obtener una lista completa de los formatos admitidos, véase [Formatos de documentos compatibles](https://wiki.gnome.org/Apps/Evince/SupportedDocumentFormats).

El visor de documentos utiliza la biblioteca poppler como backend.

**Nota:** El visor de documentos era conocido anteriormente como [Evince](https://wiki.gnome.org/Apps/Evince) hasta que la aplicación recibió nuevos nombres descriptivos, uno para cada idioma admitido. El nombre *Evince* todavía se utiliza en muchos lugares, como el nombre del ejecutable, algunos nombres de paquetes, algunas entradas de escritorio y algunos esquemas GSettings.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Solución de problemas](#Solución_de_problemas)
    *   [2.1 La impresora no aparece](#La_impresora_no_aparece)
    *   [2.2 La ampliación es limitada](#La_ampliación_es_limitada)
    *   [2.3 Los textos en PDF no se muestran correctamente](#Los_textos_en_PDF_no_se_muestran_correctamente)
    *   [2.4 La búsqueda inversa con SyncTeX no funciona](#La_búsqueda_inversa_con_SyncTeX_no_funciona)
*   [3 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [evince](https://www.archlinux.org/packages/?name=evince), o [evince-git](https://aur.archlinux.org/packages/evince-git/) para la versión de desarrollo. Evince instala gnome-desktop como dependencia.

Para una versión independiente instale [evince-no-gnome](https://aur.archlinux.org/packages/evince-no-gnome/) o la versión ligera [evince-light](https://aur.archlinux.org/packages/evince-light/) para tener soporte solamente de PDF.

## Solución de problemas

### La impresora no aparece

Actualice [gtk3](https://www.archlinux.org/packages/?name=gtk3) a la versión `3.22.26+47+g3a1a7135a2-1` o superior. En versiones anteriores de GTK+ 3, los backends de la impresora GTK+ se incluyeron en un paquete separado. [[1]](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/gtk3&id=54e7af64837e18355122e62ff565970620db3537)

### La ampliación es limitada

El aumento del tamaño de la memoria caché de la página de Evince le permite ampliar aún más, lo que es útil para documentos grandes. Por defecto, la configuración se establece en 50MiB. El aumento del tamaño del caché de la página obviamente aumenta el consumo de memoria de Evince cuando se amplía.

La siguiente orden aumenta el tamaño del caché de la página a un gigabyte:

```
$ gsettings set org.gnome.Evince page-cache-size 'uint32 1000'

```

### Los textos en PDF no se muestran correctamente

Intente establecer el parámetro `override-restrictions` a falso:

```
$ gsettings set org.gnome.Evince override-restrictions false

```

### La búsqueda inversa con SyncTeX no funciona

Compruebe que [python-dbus](https://www.archlinux.org/packages/?name=python-dbus) está [instalado](/index.php/Install_(Espa%C3%B1ol) "Install (Español)"). Tras esto `Ctrl+click` debería funcionar.

## Véase también

*   [Sitio web de Evince](https://wiki.gnome.org/Apps/Evince)
*   [Sitio web de Poppler](http://poppler.freedesktop.org/)
*   [Página "Referencia de PDF" de Adobe](http://www.adobe.com/devnet/pdf/pdf_reference.html)