Tvheadend is a TV streaming server and recorder. Tvheadend supports DVB-S/S2, DVB-C/C2, DVB-T, ATSC, ISDB-T, IPTV, SAT>IP and HDHomeRun as input sources.

## Contents

*   [1 Installation](#Installation)
*   [2 HDHomeRun](#HDHomeRun)
*   [3 Setup](#Setup)
*   [4 Configuration](#Configuration)
    *   [4.1 Unable to Log In](#Unable_to_Log_In)
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

## Unable to Log In

Some people have issues accessing the web interface with the [Tvheadend-git](https://aur.archlinux.org/packages/Tvheadend-git/) package. If the default of a blank username and password does not work, then it can be worked around by starting the service with the `tvheadend -C` command. This will let us create a username and password before restarting without -C. Begin by editing the services file at `/usr/lib/systemd/system/tvheadend.service`. On the `ExecStart` line we need to add the option `-C` like so `ExecStart=/usr/bin/tvheadend -f -p /var/run/tvheadend.pid $OPTIONS -C` 

Then run `systemctl daemon-reload` followed by `systemctl restart tvheadend`. You can now navigate to the configuration interface in a web browser [localhost:9981](http://localhost:9981/) and either follow the setup wizard to create a new user, or close the wizard and navigate to Configuration > Users > Access Entries tabs. Once your username and password are created and working, follow the above instructions again to remove the `-C` command, then reload and restart your service.

# XMLTV

If you want to obtain schedule data from an outside source like Schedules Direct, then you should also install [xmltv](https://aur.archlinux.org/packages/xmltv/).

# Playback Clients

There are a few options for Tvheadend clients. VLC can be used as a client with the [vlc-htsp-plugin-git](https://aur.archlinux.org/packages/vlc-htsp-plugin-git/) package. Kodi support can be added via the installation of [kodi-addon-hts-pvrmanager](https://aur.archlinux.org/packages/kodi-addon-hts-pvrmanager/) and either [kodi-addon-pvr-hts](https://aur.archlinux.org/packages/kodi-addon-pvr-hts/) or [kodi-addon-pvr-hts-git](https://aur.archlinux.org/packages/kodi-addon-pvr-hts-git/) (chose either the release or stable version based on which version of Kodi you have installed).