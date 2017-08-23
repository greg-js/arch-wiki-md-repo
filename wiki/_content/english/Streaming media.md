Businesses are storing their data on the network for ages now, but the past few years, there has been a trend in home networking to put all content on a central server and distributing it to the home computers and dedicated appliances on the network. This page offers an overview of the possible packages to stream digital media (video, audio and images, and in several cases also online content) from your server to your clients.

## Contents

*   [1 Servers](#Servers)
    *   [1.1 UPnP / DLNA](#UPnP_.2F_DLNA)
        *   [1.1.1 Deprecated / No Longer in Development](#Deprecated_.2F_No_Longer_in_Development)
    *   [1.2 MPD](#MPD)
*   [2 Clients](#Clients)
    *   [2.1 UPnP / DLNA](#UPnP_.2F_DLNA_2)

## Servers

### UPnP / DLNA

There are many UPnP or DLNA-compliant server and you can use Mpd too. Some of the them do not get along together. If you are experiencing problems, make sure you are not running two of them at the same time.

*   [Subsonic](/index.php/Subsonic "Subsonic")
*   [ReadyMedia](/index.php/ReadyMedia "ReadyMedia")
*   [Rygel](/index.php/Rygel "Rygel")
*   [PS3 Mediaserver](/index.php/PS3_Mediaserver "PS3 Mediaserver")
*   [Plex](/index.php/Plex "Plex")
*   [Emby](/index.php/Emby "Emby")
*   [Universal Media Server](/index.php/Universal_Media_Server "Universal Media Server")
*   [Serviio](http://serviio.org/) ([serviio](https://aur.archlinux.org/packages/serviio/))
*   [Coherence](http://coherence.beebits.net) ([coherence](https://aur.archlinux.org/packages/coherence/))

And here is a list of DLNA controller applications. These can be used to control a DLNA renderer and server:

*   [Upplay](http://www.lesbonscomptes.com/upplay/) ([upplay](https://aur.archlinux.org/packages/upplay/))
*   [Universal Media Server](/index.php/Universal_Media_Server "Universal Media Server") - the web interface allows pushing content to DLNA renderers

#### Deprecated / No Longer in Development

*   [uShare](/index.php/UShare "UShare")
*   [MediaTomb](/index.php/MediaTomb "MediaTomb")

### MPD

*   [MPD](/index.php/MPD "MPD")

## Clients

### UPnP / DLNA

*   [VLC media player](/index.php/VLC_media_player "VLC media player"), via View -> Playlist -> Local Network (in left sidebar) -> Universal Plug'n'Play
*   [Kodi](/index.php/Kodi "Kodi")
*   [Plex](/index.php/Plex "Plex")
*   [GNOME Videos](https://wiki.gnome.org/Apps/Videos) ([totem](https://www.archlinux.org/packages/?name=totem)), via the "Channels" tab, after having installed [grilo-plugins](https://www.archlinux.org/packages/?name=grilo-plugins), [gupnp-av](https://www.archlinux.org/packages/?name=gupnp-av) and [dleyna-server](https://www.archlinux.org/packages/?name=dleyna-server)