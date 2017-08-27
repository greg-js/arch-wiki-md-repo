[Tvheadend](https://tvheadend.org/) is a TV streaming server and recorder. Tvheadend supports DVB-S/S2, DVB-C/C2, DVB-T, ATSC, ISDB-T, IPTV, SAT>IP and HDHomeRun as input sources.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 HDHomeRun](#HDHomeRun)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 XMLTV](#XMLTV)
*   [5 Playback Clients](#Playback_Clients)

## Installation

Tvheadend is available from the [AUR](/index.php/AUR "AUR") as [tvheadend](https://aur.archlinux.org/packages/tvheadend/) and [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/) (development branch).

Since v4.2.1, [tvheadend](https://aur.archlinux.org/packages/tvheadend/) has been updated with the features and capabilities of the development branch, so featurewise they're roughly on par and [tvheadend](https://aur.archlinux.org/packages/tvheadend/) should be the more stable choice.

### HDHomeRun

HDHomeRun support should be working by default in the [TVheadend](https://aur.archlinux.org/packages/TVheadend/) package.

By default the [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/) and [tvheadend](https://aur.archlinux.org/packages/tvheadend/) do not have HDHomeRun support enabled. To enable you will need to edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and add `libhdhomerun` to the [depends](/index.php/PKGBUILD#depends "PKGBUILD") list. Finally remove `--disable-hdhomerun_static` and replace with `--enable-hdhomerun_client` in *build*.

## Usage

Once Tvheadend is installed [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") the `tvheadend.service`.

## Configuration

Once the service is running, configuration of Tvheadend is done through a web interface on [localhost:9981](http://localhost:9981).

The service should automatically generate Tvheadend username and passwords that are the same as your system. You can log in as root with your system's root password.

## XMLTV

If you want to obtain schedule data from an outside source like Schedules Direct, then you should also install [xmltv](https://aur.archlinux.org/packages/xmltv/).

## Playback Clients

*   [VLC](/index.php/VLC "VLC") — [vlc-htsp-plugin-git](https://aur.archlinux.org/packages/vlc-htsp-plugin-git/)
*   [Kodi](/index.php/Kodi "Kodi") — [kodi-addon-hts-pvrmanager](https://aur.archlinux.org/packages/kodi-addon-hts-pvrmanager/), [kodi-addon-pvr-hts](https://aur.archlinux.org/packages/kodi-addon-pvr-hts/) or [kodi-addon-pvr-hts-git](https://aur.archlinux.org/packages/kodi-addon-pvr-hts-git/)