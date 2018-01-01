[Tvheadend](https://tvheadend.org/) is a TV streaming server and recorder. Tvheadend supports DVB-S/S2, DVB-C/C2, DVB-T, ATSC, ISDB-T, IPTV, SAT>IP and HDHomeRun as input sources.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 HDHomeRun](#HDHomeRun)
    *   [1.2 Playback Clients](#Playback_Clients)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 XMLTV](#XMLTV)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Use CAPMT (Linux Network DVBAPI) with OSCam](#Use_CAPMT_.28Linux_Network_DVBAPI.29_with_OSCam)

## Installation

Tvheadend is available from the [AUR](/index.php/AUR "AUR") as [tvheadend](https://aur.archlinux.org/packages/tvheadend/) or [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/) (development branch).

Since v4.2.1, [tvheadend](https://aur.archlinux.org/packages/tvheadend/) has been updated with the features and capabilities of the development branch, so feature wise they're roughly on par.

### HDHomeRun

HDHomeRun support should be working out-of-the-box in the [tvheadend](https://aur.archlinux.org/packages/tvheadend/) package.

By default the [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/) package does not have HDHomeRun support enabled. To enable you will need to edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and add `libhdhomerun` to the [depends](/index.php/PKGBUILD#depends "PKGBUILD") list. Finally remove `--disable-hdhomerun_static` and replace with `--enable-hdhomerun_client` in *build*.

### Playback Clients

*   [VLC](/index.php/VLC "VLC") — [vlc-htsp-plugin-git](https://aur.archlinux.org/packages/vlc-htsp-plugin-git/)
*   [Kodi](/index.php/Kodi "Kodi") — [kodi-addon-hts-pvrmanager](https://aur.archlinux.org/packages/kodi-addon-hts-pvrmanager/), [kodi-addon-pvr-hts](https://aur.archlinux.org/packages/kodi-addon-pvr-hts/) or [kodi-addon-pvr-hts-git](https://aur.archlinux.org/packages/kodi-addon-pvr-hts-git/)

## Usage

Once Tvheadend is installed [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") the `tvheadend.service`.

## Configuration

Once the service is running, configuration of Tvheadend is done through a web interface on [localhost:9981](http://localhost:9981).

The service should automatically generate Tvheadend username and passwords that are the same as your system. You can log in as root with your system's root password.

## XMLTV

If you want to obtain schedule data from an outside source like Schedules Direct, then you should also install [xmltv](https://aur.archlinux.org/packages/xmltv/).

## Tips and tricks

### Use CAPMT (Linux Network DVBAPI) with OSCam

[install](/index.php/Install "Install") [oscam-git](https://aur.archlinux.org/packages/oscam-git/) to provide a softcam for Tvheadend.

The following settings may be used when using DVB-API as Conditional Access Client:

| Parameter | Value |
| Client name | OSCam |
| Mode | OSCam net protocol (rev >= 10389) |
| IP Address (TCP mode) | localhost |
| Connect port: | 9000 |

Add the user *vdr* with *vdr* as password in OSCam.

Set *DVB Api Config* to use at least the following parameters:

| Parameter | Value |
| Boxtype | pc |
| User | vdr |
| PMT Mode | 4 |
| Listen port | 9000 |

[Restart](/index.php/Restart "Restart") `oscam.service` and `tvheadend.service` to apply the changes.