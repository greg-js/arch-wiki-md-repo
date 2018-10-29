Artículos relacionados

*   [Google Earth](/index.php/Google_Earth "Google Earth")

El proyecto **ArchMap** crea un mapa de usuarios de Arch Linux de todo el mundo.

## Contents

*   [1 Historia](#Historia)
    *   [1.1 Capturas de pantalla](#Capturas_de_pantalla)
*   [2 archmap](#archmap)
*   [3 Mapas](#Mapas)
    *   [3.1 OpenStreetMap](#OpenStreetMap)
    *   [3.2 Google Earth](#Google_Earth)
    *   [3.3 Mapas generados por los usuarios](#Mapas_generados_por_los_usuarios)
*   [4 Alístese](#Al.C3.ADstese)

## Historia

**ArchMap** fue creado originalmente por [User: xterminus](/index.php/User:Xterminus "User:Xterminus"). Creó archivos jpeg que se podían descargar desde esta página. Sin embargo, ya no tenía tiempo para mantenerlos, así que abandonó el proyecto.

Cuando se lanzó Google Earth para Linux, [User: brain0](/index.php/User:Brain0 "User:Brain0") volvió a crear el proyecto.

La tercera versión de ArchMap se basó en Google Maps.

La versión actual fue iniciada por [User: Alux](/index.php/User:Alux "User:Alux") con la ayuda de [User: Kyrias](/index.php/User:Kyrias "User:Kyrias") y [User: Fsckd](/index.php/User:Fsckd "User:Fsckd").

### Capturas de pantalla

He aquí algunas capturas de pantalla de cómo solía verse:

*   [Europa](http://archive.today/AZELb) - 2006
*   [EEUU](http://archive.today/aQwag) - 2006
*   [América del Sur](http://archive.today/HIlLi) - 2009

## archmap

`[archmap](https://github.com/guyfawcus/ArchMap/blob/master/archmap.py)` es un script de python que puede generar archivos *GeoJSON* , *KML* y *CSV* al analizar [esta lista](/index.php/ArchMap/List#List "ArchMap/List") de los usuarios de Arch Linux.

**Nota:** ArchMap se desarrolla actualmente en [GitHub](https://github.com/guyfawcus/ArchMap). Si tiene alguna sugerencia, por favor [publíquelas](https://bbs.archlinux.org/viewtopic.php?id=22518&p=2) en los foros o [cree un problema](https://github.com/guyfawcus/ArchMap/issues) en el repositorio.

La documentación está alojada en [readthedocs.org](http://archmap.readthedocs.io).

## Mapas

[Arch Women](https://archwomen.org/wiki/aw-tech:archmap) aloja archivos [GeoJSON](https://archwomen.org/media/archmap/archmap.geojson), *[KML](https://archwomen.org/media/archmap/archmap.kml)* y *[CSV](https://archwomen.org/media/archmap/archmap.csv)* pre-generados, así como la *[lista sin formato](https://archwomen.org/media/archmap/archmap-users.txt)* re-formateada que se hace con `archmap`. Estos archivos se actualizan cuatro veces al día: a las 00:00, 06:00, 12:00 y 18:00 UTC [[1]](https://archwomen.org/wiki/aw-tech:archmap#files) y se utilizan para hacer los mapas que se mencionan a continuación.

### OpenStreetMap

geojson.io es "una herramienta rápida y sencilla para crear, cambiar y publicar mapas", utiliza OpenStreetMap como capa base. [Este enlace](http://geojson.io/#data=data:text/x-url,https://archwomen.org/media/archmap/archmap.geojson) extraerá el archivo *GeoJSON* del servidor Arch Women y lo abrirá para editarlo en el sitio.

### Google Earth

Puede agregar las coordenadas a Google Earth de forma permanente:

*   Haga clic derecho en *Mis lugares*
*   Ir a *Agregar* -> *Enlace de red*
*   Ingrese "ArchMap" en el campo *Nombre* y coloque `[https://archwomen.org/media/archmap/archmap.kml](https://archwomen.org/media/archmap/archmap.kml)` en el campo *Enlace*, luego presione *OK*.

Puede actualizar los datos haciendo clic derecho en la carpeta ArchMap y seleccionando *Actualizar*.

### Mapas generados por los usuarios

[Este mapa](https://api.mapbox.com/styles/v1/erayaydin/cis93dj9j001v2xuge20kuq0h.html?fresh=true&title=true&access_token=pk.eyJ1IjoiZXJheWF5ZGluIiwiYSI6ImNpczdxMG1pNDAwMmYyb2xqY2Y1NXB5ZDUifQ.TUVUVEtsW6MHYsybhpZ3-w#5.32/38.578/32.784) creado por Eray Aydın el 24/08/2016

[Este mapa](https://data.dopsi.ch/archmap) se actualiza diariamente (alrededor de las 10:00am UTC) utilizando el script [ArchMap](http://github.com/guyfawcus/ArchMap). Los datos KML utilizados para representar el mapa están disponibles [aquí](https://data.dopsi.ch/archmap/archmap.kml), la lista de usuarios sin procesar [aquí](https://data.dopsi.ch/archmap/users.txt).

Algunas otras representaciones de los datos están alojadas en [CartoDB](https://alux.cartodb.com/viz/c1cd0e2a-5af7-11e4-afcd-0e9d821ea90d/embed_map) y [MapBox](https://a.tiles.mapbox.com/v3/alux.hclg4eg0/page.html?secure=1#4/39.63/-104.91). Sin embargo, estos pueden estar desactualizados, ya que deben ser actualizados manualmente por [alux](/index.php/User:Alux "User:Alux") al importar el archivo *GeoJSON*.

## Alístese

Vaya a la página [Lista ArchMap](/index.php/ArchMap/List "ArchMap/List"), siga las instrucciones y luego use el botón [**editar**] para agregarse al mapa.