# ArchMap

The **ArchMap** project creates a map of Arch Linux users all over the world.

## Contents

*   [1 History](#History)
    *   [1.1 Screenshots](#Screenshots)
*   [2 archmap](#archmap)
*   [3 Maps](#Maps)
    *   [3.1 OpenStreetMap](#OpenStreetMap)
    *   [3.2 Google Maps](#Google_Maps)
    *   [3.3 Google Earth](#Google_Earth)
*   [4 List yourself](#List_yourself)

## History

**ArchMap** was originally created by [xterminus](/index.php/User:Xterminus "User:Xterminus"). He created jpeg files that could be downloaded from this page. However, he didn't have the time to maintain them anymore, so he dropped the project.

When Google Earth for Linux was released, [brain0](/index.php/User:Brain0 "User:Brain0") recreated the project.

The third version of ArchMap was based on Google Maps.

The current version was started by [alux](/index.php/User:Alux "User:Alux") with help from [kyrias](/index.php/User:Kyrias "User:Kyrias") and [fsckd](/index.php?title=User:Fsckd&action=edit&redlink=1 "User:Fsckd (page does not exist)").

### Screenshots

Here are some screenshots of how it used to look:

*   [Europe](http://archive.today/AZELb) - 2006
*   [US](http://archive.today/aQwag) - 2006
*   [South America](http://archive.today/HIlLi) - 2009

## archmap

`[archmap](https://github.com/maelstrom59/ArchMap/blob/master/archmap.py)` is a python script that can generate _GeoJSON_, _KML_ and _CSV_ files by parsing [this list](/index.php/ArchMap/List#List "ArchMap/List") of Arch Linux users.

**Note:** ArchMap is currently under development on [GitHub](https://github.com/maelstrom59/ArchMap). If you have any suggestions, please [post them](https://bbs.archlinux.org/viewtopic.php?id=22518&p=2) in the forums or [create an issue](https://github.com/maelstrom59/ArchMap/issues) in the repository.

The documentation is hosted by [readthedocs.org](http://archmap.readthedocs.org).

## Maps

[Arch Women](https://archwomen.org/wiki/aw-tech:archmap) host pre-generated _[GeoJSON](https://archwomen.org/media/archmap/archmap.geojson)_, _[KML](https://archwomen.org/media/archmap/archmap.kml)_ and _[CSV](https://archwomen.org/media/archmap/archmap.csv)_ files that are made by `archmap`, these files are updated daily and are used to make the maps below.

### OpenStreetMap

geojson.io is _"a fast, simple tool to create, change, and publish maps"_, it uses OpenStreetMap as a base-layer. [This link](http://geojson.io/#data=data:text/x-url,https://archwomen.org/media/archmap/archmap.geojson) will pull the _GeoJSON_ file from the Arch Women server and open it up for editing on the site.

Some other renderings of the data are hosted by [CartoDB](https://alux.cartodb.com/viz/c1cd0e2a-5af7-11e4-afcd-0e9d821ea90d/embed_map) and [MapBox](https://a.tiles.mapbox.com/v3/alux.hclg4eg0/page.html?secure=1#4/39.63/-104.91). However, these may be out of date as they have to be updated manually by [alux](/index.php/User:Alux "User:Alux") importing the _GeoJSON_ file.

### Google Maps

To display the coordinates in Google Maps, enter [this link](https://archwomen.org/media/archmap/archmap.kml) to the _KML_ file into the search bar, here is [that search](https://maps.google.com/maps?hl=en&q=https%3A%2F%2Farchwomen.org%2Fmedia%2Farchmap%2Farchmap.kml).

### Google Earth

You can add the coordinates to Google Earth permanently:

*   Right click on _My Places_
*   Go to _Add_ -> _Network Link_
*   Enter "ArchMap" into the _Name_ field and put `[https://archwomen.org/media/archmap/archmap.kml](https://archwomen.org/media/archmap/archmap.kml)` into the _Link_ field, then press _OK_.

You can refresh the data by right-clicking the ArchMap folder and selecting _Refresh_.

## List yourself

Go to the [ArchMap List page](/index.php/ArchMap/List "ArchMap/List"), follow the instructions, then use the [**edit**] button to add yourself to the map.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ArchMap&oldid=392928](https://wiki.archlinux.org/index.php?title=ArchMap&oldid=392928)"