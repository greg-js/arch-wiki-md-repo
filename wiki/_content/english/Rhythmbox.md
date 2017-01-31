**Rhythmbox** is an audio player that plays and helps organize digital music. It is designed to work well under the [GNOME](/index.php/GNOME "GNOME") desktop using the [GStreamer](/index.php/GStreamer "GStreamer") media framework.

## Contents

*   [1 Installation](#Installation)
*   [2 Tips](#Tips)
    *   [2.1 Playing remote media from Internet sources (blip.tv, Jamendo, SHOUTcast)](#Playing_remote_media_from_Internet_sources_.28blip.tv.2C_Jamendo.2C_SHOUTcast.29)
    *   [2.2 How to activate the Cover Art plugin](#How_to_activate_the_Cover_Art_plugin)
    *   [2.3 What to do when the little red icon shows when you try to play radio stations](#What_to_do_when_the_little_red_icon_shows_when_you_try_to_play_radio_stations)
    *   [2.4 How to activate the DAAP Music Sharing](#How_to_activate_the_DAAP_Music_Sharing)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 What to do if you see an "Unknown Playback Error" message](#What_to_do_if_you_see_an_.22Unknown_Playback_Error.22_message)
        *   [3.1.1 Unknown Playback when streaming from an online radio station](#Unknown_Playback_when_streaming_from_an_online_radio_station)
        *   [3.1.2 Unknown Playback when streaming or playing from regular files](#Unknown_Playback_when_streaming_or_playing_from_regular_files)
    *   [3.2 "Error, impossible to activate plugin 'Audio CD Recorder'" shows up every time I start Rhythmbox](#.22Error.2C_impossible_to_activate_plugin_.27Audio_CD_Recorder.27.22_shows_up_every_time_I_start_Rhythmbox)
    *   [3.3 Slow start and "Unable to start mDNS browsing: MDNS service is not running" output](#Slow_start_and_.22Unable_to_start_mDNS_browsing:_MDNS_service_is_not_running.22_output)
    *   [3.4 Cannot activate "context pane" plugin](#Cannot_activate_.22context_pane.22_plugin)
    *   [3.5 Rhythmbox Startup is Slow](#Rhythmbox_Startup_is_Slow)
    *   [3.6 No cover are shown in the dedicated box](#No_cover_are_shown_in_the_dedicated_box)
    *   [3.7 Cannot enable MTP device support](#Cannot_enable_MTP_device_support)
    *   [3.8 Music files within the music library are not found](#Music_files_within_the_music_library_are_not_found)

## Installation

Install the [rhythmbox](https://www.archlinux.org/packages/?name=rhythmbox) package.

## Tips

### Playing remote media from Internet sources (blip.tv, Jamendo, SHOUTcast)

Rhythmbox takes advantage of the [Grilo](https://live.gnome.org/Grilo) framework to browse external sources such as SHOUTcast webradios and more.

You need to install the [grilo](https://www.archlinux.org/packages/?name=grilo) and [grilo-plugins](https://www.archlinux.org/packages/?name=grilo-plugins) packages. Then, be sure to enable the *Grilo Media Browser* plugin into Rhythmbox ("Edit" > "Plugins").

### How to activate the Cover Art plugin

If you want to use the cover art plugin, but are unable to do so, you need to install [gnome-python](https://www.archlinux.org/packages/?name=gnome-python).

After you do that, restart Rhythmbox.

This requirement also affects the Song Lyrics and Magnitune plugins, as well as serveral others.

### What to do when the little red icon shows when you try to play radio stations

First thing to do when the stop sign icon shows is to right-click the name of the station you are trying to listen to and open the Properties dialog box. Rhythmbox should give a bit more explanation about why it was unable to start playing the audio stream.

### How to activate the DAAP Music Sharing

1) First, install the [libdmapsharing](https://www.archlinux.org/packages/?name=libdmapsharing) package that is required for DAAP sharing.

2) You will need the avahi-daemon running. See [Avahi](/index.php/Avahi "Avahi") for full details on how to install and configure it. Here are some advices:

a) install [avahi](https://www.archlinux.org/packages/?name=avahi) and [nss-mdns](https://www.archlinux.org/packages/?name=nss-mdns)

b) You also need to edit `/etc/nsswitch.conf` to configure hostname resolution. Change the line

```
hosts: files myhostname dns

```

to:

```
hosts: files myhostname mdns_minimal [NOTFOUND=return] dns

```

c) start it [Start/enable](/index.php/Start/enable "Start/enable") `avahi-daemon.service`.

## Troubleshooting

### What to do if you see an "Unknown Playback Error" message

#### Unknown Playback when streaming from an online radio station

If you click on the radio stations and are shown a "Unknown Playback Error" error message. you probably do not have a gstreamer gnomevfs installed.

The package is called `gstreamer0.10-base-plugins-gnomevfs` and is available in the [AUR](https://aur.archlinux.org/packages.php?ID=35090)

After you install it, restart Rhythmbox.

#### Unknown Playback when streaming or playing from regular files

Alternatively, Rhythmbox will display the same error message when it does not have the correct codec to play that stream. You will need to identify what format the stream is (by looking at the command line error messages that Rhythmbox displays) and then install the correct Gstreamer codec for that particular audio stream.

For mp3-files install [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) and/or [gstreamer0.10-ugly-plugins](https://aur.archlinux.org/packages/gstreamer0.10-ugly-plugins/) depending on wheter you use the current and/or legacy version (see [GStreamer#Installation](/index.php/GStreamer#Installation "GStreamer")). You will also need [gst-libav](https://www.archlinux.org/packages/?name=gst-libav).

If you do not know which gstreamer plugin servers what audio formats, ask on IRC or just google it. For a full setup of rhythmbox, have a look at its optional dependencies: [rhythmbox](https://www.archlinux.org/packages/?name=rhythmbox).

### "Error, impossible to activate plugin 'Audio CD Recorder'" shows up every time I start Rhythmbox

You have two options:

1.  install [brasero](https://www.archlinux.org/packages/?name=brasero)
2.  disable the cd recording plugin: Run `dconf-editor`, navigate to `/org/gnome/rhythmbox/plugins/` and remove cd-recorder from active-plugins.

### Slow start and "Unable to start mDNS browsing: MDNS service is not running" output

You have two options:

1.  activate the DAAP Music Sharing (see [#How to activate the DAAP Music Sharing](#How_to_activate_the_DAAP_Music_Sharing) above)
2.  disable the DAAP plugin: Run `dconf-editor`, navigate to `/org/gnome/rhythmbox/plugins/` and remove DAAP from active-plugins.

### Cannot activate "context pane" plugin

You have to install [python-mako](https://www.archlinux.org/packages/?name=python-mako) and [pywebkitgtk](https://aur.archlinux.org/packages/pywebkitgtk/).

### Rhythmbox Startup is Slow

This can be easily fixed by disabling some of the plugins. For example, if you do not use a mediaplayer gnome-shell extension you do not need the MRPIS and D-bus plugins enabled.

### No cover are shown in the dedicated box

Creating a lastFM account and login in with the rhythmbox plugin can solve the problem.

### Cannot enable MTP device support

Install [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp).

### Music files within the music library are not found

Sometimes it helps to remove the rhythmbox library in order to rebuild it properly. To do this quit rhythmbox, delete (do not forget to make a backup of the file) `/.local/share/rhythmbox/rhythmdb.xml`, restart rhythmbox and rescan your music library.