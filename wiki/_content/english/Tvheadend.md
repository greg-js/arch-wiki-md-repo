Tvheadend is a TV streaming server and recorder. Tvheadend supports DVB-S/S2, DVB-C/C2, DVB-T, ATSC, ISDB-T, IPTV, SAT>IP and HDHomeRun as input sources.

## Contents

*   [1 Installation](#Installation)
*   [2 HDHomeRun](#HDHomeRun)
*   [3 Setup](#Setup)
*   [4 Configuration](#Configuration)
*   [5 XMLTV](#XMLTV)
*   [6 Playback Clients](#Playback_Clients)

# Installation

Tvheadend is available from the [AUR](/index.php/AUR "AUR") as [tvheadend](https://aur.archlinux.org/packages/tvheadend/) and [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/). The development version is recommended, as it has many new features and capabilities.

# HDHomeRun

HDHomeRun support should be working by default in the [TVheadend](https://aur.archlinux.org/packages/TVheadend/) package.

By default [Tvheadend-git](https://aur.archlinux.org/packages/Tvheadend-git/) does not have HDHomeRun support enabled. To enable it you will need to edit the PKGBUILD to add `libhdhomerun` to the depends list. In the build() list remove `--disable-hdhomerun_static` and add `--enable-hdhomerun_client`.

# Setup

Once Tvheadend is installed you can run it by executing the following: `systemctl start tvheadend`

If you want Tvheadend to run on boot then enable the service with the following: `systemctl enable tvheadend`

# Configuration

Once the service is running configuration of Tvheadend is done through a web interface on [localhost:9981](http://localhost:9981).

The service should automatically generate Tvheadend username and passwords that are the same as your system. You can log in as root with your system's root password.

# XMLTV

If you want to obtain schedule data from an outside source like Schedules Direct, then you should also install [xmltv](https://aur.archlinux.org/packages/xmltv/).

# Playback Clients

There are a few options for Tvheadend clients. VLC can be used as a client with the [vlc-htsp-plugin-git](https://aur.archlinux.org/packages/vlc-htsp-plugin-git/) package. Kodi support can be added via the installation of [kodi-addon-hts-pvrmanager](https://aur.archlinux.org/packages/kodi-addon-hts-pvrmanager/) and either [kodi-addon-pvr-hts](https://aur.archlinux.org/packages/kodi-addon-pvr-hts/) or [kodi-addon-pvr-hts-git](https://aur.archlinux.org/packages/kodi-addon-pvr-hts-git/) (chose either the release or stable version based on which version of Kodi you have installed).