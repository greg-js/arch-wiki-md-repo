**Estado de la traducción**
Este artículo es una traducción de [Amarok](/index.php/Amarok "Amarok"), revisada por última vez el **2019-02-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Amarok&diff=0&oldid=567112) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Amarok](https://amarok.kde.org/) es un reproductor y organizador de música para Linux con una interfaz [Qt](/index.php/Qt "Qt") intuitiva que se integra muy bien con [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Personalización](#Personalización)
    *   [2.1 Integración con GNOME](#Integración_con_GNOME)
    *   [2.2 Scripts y applets](#Scripts_y_applets)
    *   [2.3 Barra de estado anímico](#Barra_de_estado_anímico)
*   [3 SHOUTcast](#SHOUTcast)
*   [4 Transmisión Ampache/MP3](#Transmisión_Ampache/MP3)
*   [5 Base de Datos de la colección](#Base_de_Datos_de_la_colección)
    *   [5.1 MySQL](#MySQL)
*   [6 Reproducción de CD de Audio](#Reproducción_de_CD_de_Audio)
*   [7 Firefly/Daap share](#Firefly/Daap_share)
*   [8 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [amarok](https://aur.archlinux.org/packages/amarok/).

Amarok depende ahora de Phonon, así que tendrá que tener un back-end seleccionado para ello. Vea [KDE#Phonon](/index.php/KDE#Phonon "KDE"). Podría necesitar instalar unos pocos [códecs](/index.php/Codecs_(Espa%C3%B1ol) "Codecs (Español)") para uso del back-end seleccionado.

## Personalización

### Integración con GNOME

Vea [Vista uniforme para aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)") para la integración visual de la GUI principal.

### Scripts y applets

Los nuevos scripts y applets pueden ser encontrados ya sea directo de Amarok (*Herramientas > Manejador de Script > Obtener más Scripts*) o en [kde-apps.org](http://kde-apps.org/content/search.php).

### Barra de estado anímico

La barra de estado anímico es una característica que cambia la barra desplazamiento de progreso estándar en una barra de desplazamiento de progreso de colores dependiendo del esatado de ánimo de la canción.

Instale [moodbar](https://aur.archlinux.org/packages/moodbar/) desde [AUR](/index.php/AUR "AUR").

Después vaya a *Configuración > Configure Amarok* y seleccione "Muestre moodbar en la barra de progreso".

Desde 2010 Amarok 2 **no** genera moodfiles, puede ya sea intentar seguir [éste tutorial](https://web.archive.org/web/20111219015904/https://amarok.kde.org/wiki/Moodbar) para crear los propios u obtener Amarok1 de AUR y dejar que genere todos los archivos .mood por usted. Para la solución de Amarok1 vaya a *Ajustes > Configurar Amarok*, y en la pestaña general seleccione las casillas "use moods" y "almacene archivos de datos moods con música".

## SHOUTcast

Para obtener SHOUTcast use el script "servicio SHOUTcast". Inicie Amarok, vaya a *Herramientas > Administrador de Script > Obtener Más Scripts*, busque *SHOUTcast* instalar *Servicio SHOUTcast*, reinicie Amarok. Así ya lo tiene en contexto "Internet".

Véase también: [¿Cómo puedo usar Amarok para transmitir mi propia estación de radio?](https://userbase.kde.org/Amarok/Manual/Various/FAQ/en#How_can_I_use_Amarok_to_stream_to_my_own_radio_station.3F), el cual recomienda [Internet DJ Console](http://giss.tv/sahabuntu/doc/idjc.html), disponible en AUR ([idjc](https://aur.archlinux.org/packages/idjc/)).

## Transmisión Ampache/MP3

Si está transmitiendo MP3s directamente o con el plugin Ampache, no será capaz de buscar en pistas si no está usando e backend [GStreamer](/index.php/GStreamer "GStreamer"). Instale los paquetes necesarios: [phonon-qt4-gstreamer](https://aur.archlinux.org/packages/phonon-qt4-gstreamer/) [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) [gst-libav](https://www.archlinux.org/packages/?name=gst-libav). Después vaya a Amarok en *Ajustes > Configurar Amarok > Playback > Configurar Phonon >* *tab* *Backend. Aquí haga GStreamer el backend preferido.*

## Base de Datos de la colección

Amarok 2.x puede usar Sqlite (default) o MySQL para almacenar la base de datos de colección. Los usuarios con colecciones grandes y con requerimentos de desempeño más demandantes podrían preferir usar MySQL.

### MySQL

Para una configuración básica de MySQL refiera a la página [MySQL](/index.php/MySQL "MySQL").

Cuando use Amarok con MySQL necesita crear un usuario MySQL que pueda accesar la base de datos. Para hacer uso, ingrese lo siguiente:

```
# mysql -p -u root
# CREATE DATABASE amarokdb;
# USE amarokdb;
# GRANT ALL ON amarokdb.* TO amarokuser@localhost IDENTIFIED BY 'password-user';
# FLUSH PRIVILEGES;
# quit

```

Esto crea una base de datos llamada 'amarokdb' y un usuario de nombre 'amarokuser' con contraseña 'password-user' quien puede acceder a dicha base de datos desde localhost. Si desea conectarse a la base de datos de su computadora desde una computadora diferente, cambie la línea a

```
# GRANT ALL ON amarok.* TO amarokuser@'%' IDENTIFIED BY  'password-user';

```

Para configurar amarok para que use MySQL, entre a la pantalla Congfigurar Amarok, escoja Base de Datos y marque "use base de datos MySQL externa". Entre al servidor (usualmente "localhost" si está local, en caso contrario el box remoto), el nombre de usuario ("amarokuser" en éste ejemplo) y la contraseña de usuario escojida. No olvide seleccionar la ruta de su colección de música.

## Reproducción de CD de Audio

Si no está usando KDE como su Entorno de Escritorio, Amarok podría no tener las utilidades que necesita para reproducir CDs de Audio. [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [audiocd-kio](https://www.archlinux.org/packages/?name=audiocd-kio) para obtener ésta funcionalidad.

## Firefly/Daap share

Para hacer visible Daap shares en Amarok habilite el plugin "DAAP Collection" en los ajustes de Amarok.

Instale [nss-mdns](https://www.archlinux.org/packages/?name=nss-mdns) y complete la línea de hosts en `/etc/nsswitch.conf` para que se vea:

```
hosts: files mdns4_minimal [NOTFOUND=return] nis dns mdns4

```

Inicie el servicio [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") `avahi-daemon`.

## Véase también

[List of applications#Audio players](/index.php/List_of_applications#Audio_players "List of applications")