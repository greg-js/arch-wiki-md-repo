Tvheadend is a TV streaming server and recorder. Tvheadend supports DVB-S/S2, DVB-C/C2, DVB-T, ATSC, ISDB-T, IPTV, SAT>IP and HDHomeRun as input sources.

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

By default [Tvheadend-git](https://aur.archlinux.org/packages/Tvheadend-git/) does not have HDHomeRun support enabled. To enable it you will need to edit the PKGBUILD to add `libhdhomerun` to the depends list. In the build() list remove `--disable-hdhomerun_static` and add `--enable-hdhomerun_client`. This trick can also be used for [tvheadend](https://aur.archlinux.org/packages/tvheadend/) to link it dynamically to the most recent [libhdhomerun](https://aur.archlinux.org/packages/libhdhomerun/) instead of statically to an embedded one.

## Usage

Once Tvheadend is installed [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") the `tvheadend.service`.

## Configuration

Once the service is running, configuration of Tvheadend is done through a web interface on [localhost:9981](http://localhost:9981).

The service should automatically generate Tvheadend username and passwords that are the same as your system. You can log in as root with your system's root password.

## XMLTV

If you want to obtain schedule data from an outside source like Schedules Direct, then you should also install [xmltv](https://aur.archlinux.org/packages/xmltv/).

## Playback Clients

There are a few options for Tvheadend clients. VLC can be used as a client with the [vlc-htsp-plugin-git](https://aur.archlinux.org/packages/vlc-htsp-plugin-git/) package. Kodi support can be added via the installation of [kodi-addon-hts-pvrmanager](https://aur.archlinux.org/packages/kodi-addon-hts-pvrmanager/) and either [kodi-addon-pvr-hts](https://aur.archlinux.org/packages/kodi-addon-pvr-hts/) or [kodi-addon-pvr-hts-git](https://aur.archlinux.org/packages/kodi-addon-pvr-hts-git/) (chose either the release or stable version based on which version of Kodi you have installed).